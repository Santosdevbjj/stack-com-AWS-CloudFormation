# Infrastructure as Code com AWS CloudFormation

![AWS](https://img.shields.io/badge/AWS-CloudFormation-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-Infrastructure%20as%20Code-232F3E?style=for-the-badge&logo=terraform&logoColor=white)
![YAML](https://img.shields.io/badge/Templates-YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-00C851?style=for-the-badge)

---

## 1. Problema de Negócio

Equipes de engenharia que provisionam infraestrutura manualmente enfrentam um problema silencioso e caro: **cada clique no Console AWS é um risco de configuração inconsistente**.

Em ambientes corporativos com múltiplos ambientes — desenvolvimento, homologação e produção — esse risco se multiplica. Surgem divergências entre ambientes, falhas de segurança por configurações esquecidas, dificuldade de auditoria e ausência total de rastreabilidade. Quando um incidente ocorre, reproduzir o ambiente original vira um trabalho arqueológico.

**O desafio central é transformar infraestrutura de um processo artesanal e frágil em um ativo de engenharia: versionado, auditável e reproduzível.**

---

## 2. Contexto

A AWS disponibiliza centenas de serviços que podem ser provisionados em minutos, mas à medida que a infraestrutura cresce, o gerenciamento manual se torna inviável.

Organizações maduras tratam infraestrutura como software. Cada recurso — VPC, Security Group, instância EC2, banco de dados RDS — é descrito em código, revisado via Pull Request, versionado no Git e implantado de forma automatizada. Essa disciplina tem nome: **Infrastructure as Code (IaC)**.

O AWS CloudFormation é o serviço nativo da AWS para IaC. Em vez de clicar manualmente:

```yaml
Resources:
  WebServer:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
```

E a AWS cria, atualiza e remove recursos automaticamente, com rollback automático em caso de falha.

Este projeto simula a jornada de uma organização que migra da infraestrutura manual para IaC completa, cobrindo todos os componentes de uma arquitetura corporativa AWS.

---

## 3. Premissas da Análise

Para desenvolvimento deste projeto foram adotadas as seguintes premissas:

- **AWS CloudFormation** como ferramenta principal de IaC, sem dependência de ferramentas de terceiros
- **Templates YAML** como formato padrão, por maior legibilidade e menor verbosidade em relação ao JSON
- **Arquitetura modular** com stacks independentes e responsabilidades isoladas
- **Princípio do menor privilégio** aplicado desde o template, não como camada posterior
- **Versionamento completo** via GitHub, com templates tratados como código de produção
- **Rollback automático** habilitado como mecanismo de segurança em todos os deploys
- **Tagging consistente** em todos os recursos para governança e rastreabilidade de custos

---

## 4. Estratégia da Solução

A solução foi arquitetada em **11 stacks independentes**, cada uma com responsabilidade única, orquestradas por uma Nested Stack raiz. Essa abordagem espelha padrões usados em ambientes enterprise de larga escala.

```
Root Stack (nested-stack.yaml)
│
├── 🌐 Network Stack        → VPC, Subnets, IGW, Route Tables
├── 🔥 Firewall Stack       → Security Groups (SSH, HTTP, HTTPS)
├── 🖥️  WebServer Stack      → EC2 + Apache + UserData
├── 🗄️  Storage Stack        → S3 com versionamento e criptografia AES-256
├── 🔐 IAM Stack            → Roles, Policies, Instance Profiles
├── 📊 Monitoring Stack     → CloudWatch Alarms (CPU > 80%)
├── 📣 SNS Stack            → Tópicos de alerta e notificações por e-mail
├── ⚖️  Load Balancer Stack  → ALB com Target Group e Health Check
├── 📈 Auto Scaling Stack   → ASG com Launch Template (min 1 / max 3)
├── 🗃️  Database Stack       → RDS MySQL 8.0 com criptografia e backup
└── 🏗️  Nested Stack         → Orquestração de todos os componentes acima
```

**Por que modularizar em vez de um único template?**

Em projetos reais, equipes distintas gerenciam domínios distintos. A equipe de rede mantém `network-stack.yaml`; a equipe de segurança mantém `firewall-stack.yaml`. Nested Stacks permitem que cada time evolua seu componente de forma independente sem risco de conflitos ou regressões nos demais.

---

## 5. Arquitetura da Solução

```
Internet
    │
    ▼
Internet Gateway
    │
    ▼
VPC (10.0.0.0/16)
    │
    ├── Public Subnet
    │       │
    │       ├── Application Load Balancer
    │       │       │
    │       │       └── Auto Scaling Group
    │       │               │
    │       │               └── EC2 (Apache HTTP Server)
    │       │
    │       └── Security Group (HTTP 80 / HTTPS 443 / SSH 22)
    │
    └── Private Subnet
            │
            └── RDS MySQL 8.0 (criptografado, sem acesso público)

Transversal:
    ├── S3 (versionamento + AES-256)
    ├── IAM Role (menor privilégio — S3ReadOnly)
    ├── CloudWatch Alarm (CPU > 80% → SNS)
    └── SNS Topic (alertas por e-mail)
```

---

## 6. Templates Desenvolvidos

### 🌐 Network Stack — `templates/network-stack.yaml`

Provisiona a fundação de rede com VPC dedicada, subnet pública com rota para a internet e Internet Gateway. Exporta `VpcId` e `PublicSubnetId` via Outputs para consumo por outras stacks.

**Decisão técnica:** `EnableDnsHostnames: true` habilitado para que instâncias EC2 recebam DNS público automaticamente, eliminando a necessidade de configuração manual posterior.

---

### 🔥 Firewall Stack — `templates/firewall-stack.yaml`

Security Group parametrizável com regras para SSH, HTTP e HTTPS. O IP de SSH é configurável via parâmetro `SSHLocation` com validação de formato CIDR.

**Decisão técnica:** SSH configurado como parâmetro (não hardcoded em `0.0.0.0/0`) para forçar restrição por IP do operador. Em produção, o valor correto é `203.0.113.x/32`, nunca acesso irrestrito.

---

### 🖥️ WebServer Stack — `templates/webserver-stack.yaml`

EC2 com Amazon Linux 2 provisionada via SSM Parameter Store (AMI sempre atualizada). Apache HTTP Server instalado e habilitado automaticamente via `UserData`. Outputs expõem `PublicIP`, `PublicDNS` e `WebsiteURL`.

**Decisão técnica:** AMI resolvida via `AWS::SSM::Parameter::Value` em vez de ID fixo, eliminando o risco de deploy em AMI desatualizada com vulnerabilidades conhecidas.

---

### 🗄️ Storage Stack — `templates/storage-stack.yaml`

Bucket S3 com versionamento habilitado, criptografia server-side AES-256 e bloqueio total de acesso público (`BlockPublicAcls`, `BlockPublicPolicy`, `RestrictPublicBuckets`).

**Decisão técnica:** Criptografia e bloqueio público configurados no template, não como configuração posterior. Segurança não é opcional — ela nasce no código.

---

### 🔐 IAM Stack — `templates/iam-stack.yaml`

IAM Role com `AssumeRolePolicyDocument` restrito ao serviço EC2 e política gerenciada `AmazonS3ReadOnlyAccess`. Instance Profile associado para uso direto por instâncias.

**Decisão técnica:** Role em vez de Access Keys. Credenciais temporárias rotacionadas automaticamente pela AWS eliminam o risco de vazamento de credenciais estáticas — um dos vetores de ataque mais comuns em ambientes cloud.

---

### 📊 Monitoring Stack — `templates/monitoring-stack.yaml`

CloudWatch Alarm parametrizado por `InstanceId`, configurado para disparar quando CPUUtilization superar 80% por 5 minutos consecutivos. `TreatMissingData: notBreaching` evita falsos alertas durante períodos de manutenção.

---

### 📣 SNS Stack — `templates/sns-stack.yaml`

Tópico SNS com subscription de e-mail parametrizável. Integra-se ao CloudWatch Alarm para notificações operacionais em tempo real.

---

### ⚖️ Load Balancer Stack — `templates/loadbalancer-stack.yaml`

Application Load Balancer internet-facing com Security Group dedicado, Target Group com Health Check em `/` e Listener na porta 80. Outputs expõem `LoadBalancerDNS` e `TargetGroupArn`.

---

### 📈 Auto Scaling Stack — `templates/autoscaling-stack.yaml`

Launch Template com UserData para Apache e Auto Scaling Group configurado com `MinSize: 1`, `MaxSize: 3`, `DesiredCapacity: 2`, distribuído em duas subnets públicas para alta disponibilidade.

**Decisão técnica:** Launch Template em vez de Launch Configuration (deprecated). Templates suportam versionamento nativo, permitindo rollback de configuração de instância sem recriar o ASG.

---

### 🗃️ Database Stack — `templates/database-stack.yaml`

RDS MySQL 8.0 com `PubliclyAccessible: false`, `StorageEncrypted: true`, `BackupRetentionPeriod: 7` dias e `DeletionProtection: false` (adequado para laboratório). Senha gerenciada via parâmetro `NoEcho` para nunca aparecer em logs.

---

### 🏗️ Nested Stack — `templates/nested-stack.yaml`

Stack raiz que orquestra todas as stacks acima via `AWS::CloudFormation::Stack`, referenciando templates armazenados em S3. Outputs consolidam os IDs das stacks filhas para rastreabilidade.

---

## 7. Estrutura do Projeto

```
stack-com-AWS-CloudFormation/
│
├── templates/
│   ├── network-stack.yaml
│   ├── firewall-stack.yaml
│   ├── webserver-stack.yaml
│   ├── storage-stack.yaml
│   ├── iam-stack.yaml
│   ├── monitoring-stack.yaml
│   ├── sns-stack.yaml
│   ├── loadbalancer-stack.yaml
│   ├── autoscaling-stack.yaml
│   ├── database-stack.yaml
│   ├── nested-stack.yaml
│   └── parameters.json
│
├── docs/
│   ├── 01-o-que-e-cloudformation.md
│   ├── 02-conceitos-fundamentais.md
│   ├── 03-como-funcionam-stacks.md
│   ├── 04-stack-ec2-webserver.md
│   ├── 05-stack-firewall-security-group.md
│   ├── 06-monitoramento-e-eventos.md
│   ├── 07-troubleshooting.md
│   ├── 08-cleanup.md
│   ├── 09-boas-praticas.md
│   ├── 10-network-stack.md
│   ├── 11-storage-stack.md
│   ├── 12-iam-stack.md
│   ├── 13-nested-stacks.md
│   ├── 14-boas-praticas-cloudformation.md
│   └── 15-insights-e-aprendizados.md
│
├── examples/
│   ├── deploy-cli.md
│   ├── deploy-console.md
│   └── delete-stack.md
│
└── README.md
```

---

## 8. Como Executar

### Pré-requisitos

- Conta AWS ativa com permissões para CloudFormation, EC2, S3, IAM, RDS, CloudWatch, SNS
- AWS CLI instalada e configurada (`aws configure`)
- Git

### Validar template antes do deploy

```bash
aws cloudformation validate-template \
  --template-body file://templates/webserver-stack.yaml
```

### Criar stack individual

```bash
aws cloudformation create-stack \
  --stack-name WebServerStack \
  --template-body file://templates/webserver-stack.yaml \
  --parameters file://templates/parameters.json \
  --capabilities CAPABILITY_NAMED_IAM
```

### Monitorar eventos em tempo real

```bash
aws cloudformation describe-stack-events \
  --stack-name WebServerStack \
  --query "StackEvents[*].[ResourceStatus,ResourceType,LogicalResourceId]" \
  --output table
```

### Obter outputs após criação

```bash
aws cloudformation describe-stacks \
  --stack-name WebServerStack \
  --query "Stacks[0].Outputs"
```

### Atualizar stack existente

```bash
aws cloudformation update-stack \
  --stack-name WebServerStack \
  --template-body file://templates/webserver-stack.yaml \
  --parameters file://templates/parameters.json \
  --capabilities CAPABILITY_NAMED_IAM
```

### Remover stack (cleanup de custos)

```bash
aws cloudformation delete-stack \
  --stack-name WebServerStack
```

> ⚠️ Buckets S3 com objetos não são removidos automaticamente. Esvazie o bucket antes de excluir a Storage Stack.

---

## 9. Decisões Técnicas e Trade-offs

| Decisão | Alternativa Considerada | Motivo da Escolha |
|---|---|---|
| CloudFormation nativo | Terraform | Integração nativa com serviços AWS, sem state file externo, menor surface de ataque |
| YAML em vez de JSON | JSON | Legibilidade superior, suporte a comentários, padrão de mercado para CloudFormation |
| Nested Stacks | Template único monolítico | Separação de responsabilidades, manutenção por domínio, escalabilidade corporativa |
| AMI via SSM Parameter | AMI ID hardcoded | AMI sempre atualizada, elimina risco de deploy em imagem com CVEs conhecidos |
| IAM Role em vez de Access Keys | Access Keys estáticas | Credenciais temporárias rotacionadas pela AWS, sem risco de vazamento |
| `PubliclyAccessible: false` no RDS | Acesso público para teste | Segurança desde o template; banco de dados nunca deve ter acesso público direto |
| Launch Template no ASG | Launch Configuration | Launch Configuration está deprecated; Templates suportam versionamento nativo |
| `TreatMissingData: notBreaching` | `missing` (default) | Evita alertas falsos durante manutenção planejada ou reinicialização de instâncias |

---

## 10. Insights da Análise

**Infraestrutura é software — e deve ser tratada como tal.**

A maior descoberta deste projeto não foi técnica. Foi conceitual: os mesmos princípios que tornam código de aplicação confiável — versionamento, revisão, testes, documentação — se aplicam integralmente à infraestrutura. CloudFormation não é uma ferramenta de automação. É uma disciplina de engenharia.

**Segurança não é uma camada — é um atributo do template.**

Configurar `StorageEncrypted: true`, `BlockPublicAcls: true` e IAM Roles com menor privilégio desde a criação do template elimina toda uma classe de vulnerabilidades que surgem quando segurança é tratada como etapa posterior ao provisionamento.

**Rollback automático muda a cultura de deploy.**

Em ambientes sem IaC, uma falha durante o provisionamento frequentemente deixa recursos órfãos e ambientes parcialmente criados. O CloudFormation reverte automaticamente para o estado anterior em caso de falha, tornando deploys atômicos — ou funcionam completamente, ou não funcionam.

**Modularização não é burocracia — é governança.**

Separar a infraestrutura em stacks por domínio (rede, segurança, dados, computação) replica a estrutura de times de organizações maduras. Cada equipe é dona de seu template, pode evoluí-lo independentemente e o impacto de cada mudança fica isolado.

---

## 11. Resultados Obtidos

Ao final do projeto foi possível:

- Provisionar **arquitetura AWS completa** com 11 componentes interdependentes via código
- Eliminar **100% do provisionamento manual** — nenhum recurso foi criado pelo Console
- Demonstrar **rollback automático** em cenários de falha controlada
- Implementar **segurança por design**: criptografia, menor privilégio e bloqueio público configurados no template
- Criar **infraestrutura reproduzível** em qualquer conta AWS a partir de um único comando
- Estruturar **documentação técnica** em 15 documentos cobrindo fundamentos, troubleshooting e boas práticas

---

## 12. Próximos Passos

**Automação e CI/CD**
- Pipeline com GitHub Actions para validação e deploy automatizado de templates
- CloudFormation StackSets para deploy multi-conta e multi-região

**Observabilidade avançada**
- Drift Detection para identificar alterações manuais fora do CloudFormation
- AWS Config Rules para conformidade contínua
- Security Hub integrado para postura de segurança centralizada

**Maturidade de infraestrutura**
- Change Sets obrigatórios antes de qualquer atualização em produção
- AWS Organizations com Service Control Policies (SCPs)
- Estudo comparativo com Terraform e AWS CDK

---

## Autor

**Sérgio Luiz dos Santos**  
Systems Analyst · Cloud & AI Solutions Specialist · DIO Campus Expert  
15+ anos em ambientes mission-critical — Banco Bradesco S.A.

[![Portfólio](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)

---

*Projeto desenvolvido como parte da Formação AWS Cloud Foundations — DIO.*  
*Infraestrutura moderna não é criada manualmente. Ela é projetada, versionada, automatizada e tratada como software.*
