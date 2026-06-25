## 🚀 Implementando sua Primeira Stack com AWS CloudFormation

"AWS" (https://img.shields.io/badge/AWS-CloudFormation-orange)
"IaC" (https://img.shields.io/badge/IaC-Infrastructure%20as%20Code-blue)
"YAML" (https://img.shields.io/badge/YAML-Templates-red)
"Cloud" (https://img.shields.io/badge/Cloud-AWS-yellow)
"Status" (https://img.shields.io/badge/Status-Concluído-success)

---

## 📖 Visão Geral

A criação manual de infraestrutura em nuvem costuma gerar inconsistências, retrabalho, falhas de configuração e dificuldades de auditoria.

Em ambientes corporativos, equipes precisam provisionar servidores, redes, armazenamento, permissões e monitoramento de forma rápida, segura e reproduzível.

Este projeto demonstra como utilizar o AWS CloudFormation para automatizar a criação de infraestrutura utilizando o conceito de Infrastructure as Code (IaC).

Ao longo deste laboratório foram desenvolvidos diversos templates CloudFormation que simulam componentes reais de uma arquitetura corporativa AWS, incluindo:

- Redes
- Segurança
- Servidores Web
- Armazenamento
- IAM
- Monitoramento
- Banco de Dados
- Auto Scaling
- Load Balancer
- Nested Stacks

Mais do que criar recursos AWS, o objetivo deste projeto é demonstrar como transformar infraestrutura em código versionável, auditável e reutilizável.

---

## 🎯 Problema de Negócio

Imagine uma empresa que precisa criar rapidamente novos ambientes para:

- desenvolvimento;
- homologação;
- produção.

Quando tudo é feito manualmente pelo Console AWS, surgem problemas como:

- configurações inconsistentes;
- erros humanos;
- dificuldade de reproduzir ambientes;
- falta de governança;
- aumento de custos operacionais.

O desafio é criar uma abordagem capaz de:

- padronizar ambientes;
- reduzir falhas;
- aumentar produtividade;
- acelerar implantações.

---

## 🌎 Contexto

A AWS disponibiliza centenas de serviços que podem ser provisionados em minutos.

Porém, à medida que a infraestrutura cresce, torna-se inviável gerenciar tudo manualmente.

Foi exatamente para resolver esse problema que a AWS criou o CloudFormation, permitindo definir infraestrutura através de arquivos YAML ou JSON.

Nesse modelo:

``` 
Infraestrutura = Código

```

Em vez de clicar no Console AWS:

```

Clique → Configuração → Clique → Configuração

```

Utilizamos:

```

Resources:
  WebServer:
    Type: AWS::EC2::Instance

```

E deixamos a AWS criar tudo automaticamente.

---

## 📌 Premissas

Para desenvolvimento deste projeto foram consideradas as seguintes premissas:

- Uso do AWS CloudFormation como ferramenta principal de IaC.
- Templates escritos em YAML.
- Arquitetura modular.
- Recursos desacoplados.
- Aplicação de boas práticas AWS.
- Versionamento completo via GitHub.
- Foco educacional e profissional.

---

## 🏗️ O Que é AWS CloudFormation?

AWS CloudFormation é o serviço de Infraestrutura como Código (IaC) da AWS.

Ele permite:

✅ Criar recursos automaticamente

✅ Atualizar ambientes de forma controlada

✅ Reproduzir arquiteturas inteiras

✅ Versionar infraestrutura

✅ Reduzir erros operacionais

Com CloudFormation, uma infraestrutura pode ser criada utilizando apenas um arquivo YAML.

---

## 🎯 Objetivos do Projeto

Este projeto foi desenvolvido para:

- compreender o funcionamento do CloudFormation;
- aprender Infraestrutura como Código;
- praticar criação de stacks;
- automatizar provisionamento de recursos;
- documentar boas práticas AWS;
- construir um portfólio profissional de Cloud Computing.

---

## 🛠️ Estratégia da Solução

A solução foi organizada em múltiplas stacks independentes.

```

CloudFormation Project
│
├── Network
├── Firewall
├── WebServer
├── Storage
├── IAM
├── Monitoring
├── SNS
├── Load Balancer
├── Auto Scaling
├── Database
└── Nested Stack

```


Essa abordagem permite:

- modularização;
- manutenção simplificada;
- reutilização de componentes;
- escalabilidade futura.

---

## 📂 Estrutura do Projeto

```

stack-com-AWS-CloudFormation
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
├── examples/
│   ├── deploy-cli.md
│   ├── deploy-console.md
│   └── delete-stack.md
│
└── README.md

```


---

## ⚙️ Tecnologias Utilizadas

### Cloud

- AWS CloudFormation
- Amazon EC2
- Amazon VPC
- Amazon S3
- IAM
- CloudWatch
- SNS
- RDS
- Auto Scaling
- Elastic Load Balancer

## Infraestrutura

- YAML
- Infrastructure as Code (IaC)

## Versionamento

- Git
- GitHub

---

## 🚀 Templates Desenvolvidos

### Network Stack

Responsável por:

- VPC
- Subnets
- Internet Gateway
- Route Tables

---

### Firewall Stack

Responsável por:

- Security Groups
- Regras HTTP
- Regras SSH

---

### Web Server Stack

Responsável por:

- EC2
- Apache HTTP Server
- User Data

---

### Storage Stack

Responsável por:

- Buckets S3
- Versionamento
- Criptografia

---

### IAM Stack

Responsável por:

- Roles
- Policies
- Governança

---

### Monitoring Stack

Responsável por:

- CloudWatch
- Alarmes
- Métricas

---

### SNS Stack

Responsável por:

- Notificações
- Alertas operacionais

---

### Load Balancer Stack

Responsável por:

- Application Load Balancer
- Distribuição de tráfego

---

### Auto Scaling Stack

Responsável por:

- Escalabilidade automática
- Alta disponibilidade

---

### Database Stack

Responsável por:

- Amazon RDS
- Persistência de dados

---

### Nested Stack

Responsável por:

- Orquestração de múltiplos templates

---

## 🚀 Como Executar

Validar Template


```

aws cloudformation validate-template \
--template-body file://templates/webserver-stack.yaml

```


---

## Criar Stack

```

aws cloudformation create-stack \
--stack-name WebServerStack \
--template-body file://templates/webserver-stack.yaml \
--parameters file://templates/parameters.json

```

---

## Monitorar

```

aws cloudformation describe-stack-events \
--stack-name WebServerStack

```

---

## Excluir Stack

```

aws cloudformation delete-stack \
--stack-name WebServerStack

```

---

## 💡 Principais Insights

Durante o desenvolvimento deste projeto ficou evidente que:

### Infraestrutura é Software

Infraestrutura moderna deve ser:

- versionada;
- documentada;
- auditável;
- reproduzível.

---

### Automação reduz erros

Toda configuração manual é candidata a erro.

CloudFormation transforma processos manuais em processos previsíveis.

---

### Segurança deve nascer no template

Boas práticas de IAM e Security Groups devem ser aplicadas desde o início.

---

### Modularização facilita manutenção

Separar recursos em múltiplas stacks torna a arquitetura mais sustentável.

---

## 📈 Resultados Obtidos

Ao final deste laboratório foi possível:

✅ Criar múltiplas stacks AWS

✅ Automatizar provisionamento

✅ Aplicar Infraestrutura como Código

✅ Estruturar templates reutilizáveis

✅ Implementar monitoramento

✅ Aplicar princípios de segurança

✅ Utilizar versionamento profissional

✅ Construir documentação completa

---

## 🎓 Aprendizados

Os principais aprendizados foram:

- funcionamento interno do CloudFormation;
- relacionamento entre recursos;
- gerenciamento de dependências;
- monitoramento de eventos;
- tratamento de falhas;
- organização de templates corporativos;
- boas práticas de arquitetura AWS.

---

## 🔮 Próximos Passos

Evoluções futuras deste projeto:

- CI/CD com GitHub Actions
- CloudFormation StackSets
- Multi-Region Deploy
- AWS Config
- Security Hub
- AWS Organizations
- Integração com Terraform para estudos comparativos

---

## 🏆 Conclusão

Este projeto demonstrou como o AWS CloudFormation permite transformar infraestrutura em código, reduzindo erros operacionais e aumentando a produtividade das equipes.

Mais do que aprender comandos ou templates YAML, o principal aprendizado foi compreender uma mudança de mentalidade:

«Infraestrutura moderna não é criada manualmente.

Infraestrutura moderna é projetada, versionada, automatizada e tratada como software.»

Essa é uma das competências mais valorizadas atualmente para profissionais de Cloud, DevOps, Platform Engineering e Arquitetura de Soluções.

---

## 👨‍💻 Autor

Sérgio Luiz dos Santos

Tecnologia da Informação | Cloud Computing | Infraestrutura | Dados | Inteligência Artificial


[![Portfólio](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)

---



Projeto desenvolvido como parte da formação AWS Cloud Foundations e estudos práticos de AWS CloudFormation.


