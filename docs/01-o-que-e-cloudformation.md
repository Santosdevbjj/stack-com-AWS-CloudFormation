# O que é AWS CloudFormation

## Visão Geral

Provisionar infraestrutura manualmente é um dos principais fatores de inconsistência em ambientes de tecnologia.

Criar servidores, configurar redes, ajustar regras de segurança e provisionar serviços manualmente aumenta significativamente os riscos de:

- erros humanos;
- configurações inconsistentes;
- falhas de segurança;
- dificuldade de auditoria;
- baixa escalabilidade.

Para resolver esse problema, a AWS disponibiliza o CloudFormation, um serviço de Infrastructure as Code (IaC) que permite definir toda a infraestrutura utilizando arquivos de texto versionáveis.

Neste projeto utilizamos o AWS CloudFormation para automatizar a criação de recursos da AWS através de templates YAML.

---

# Problema de Negócio

Imagine uma empresa que precisa criar ambientes para:

- desenvolvimento;
- homologação;
- produção.

Se cada ambiente for criado manualmente:

- haverá diferenças entre configurações;
- o tempo de provisionamento será elevado;
- o risco de falhas operacionais aumentará.

Além disso, reproduzir um ambiente em caso de desastre torna-se um processo complexo.

O desafio é garantir consistência, rastreabilidade e velocidade na criação da infraestrutura.

---

# O que é Infrastructure as Code (IaC)

Infrastructure as Code é uma abordagem que trata a infraestrutura da mesma forma que tratamos software.

Em vez de clicar manualmente no console da AWS, descrevemos a infraestrutura através de código.

Exemplo:

```yaml
Resources:

  WebServer:

    Type: AWS::EC2::Instance

    Properties:

      InstanceType: t2.micro
```

O código torna-se:

- versionável;
- reutilizável;
- auditável;
- automatizável.

---

# O que é AWS CloudFormation

AWS CloudFormation é o serviço nativo da AWS para implementação de Infrastructure as Code.

Com ele podemos criar:

- EC2
- VPC
- Subnets
- Security Groups
- RDS
- S3
- IAM
- Load Balancers
- Auto Scaling Groups
- CloudWatch
- SNS

e centenas de outros recursos.

Tudo utilizando arquivos YAML ou JSON.

---

# Benefícios do CloudFormation

## Padronização

Todos os ambientes seguem exatamente a mesma configuração.

## Reprodutibilidade

A infraestrutura pode ser recriada quantas vezes forem necessárias.

## Controle de Versão

Os templates podem ser armazenados no GitHub.

## Auditoria

Todas as alterações ficam registradas.

## Automação

Integra facilmente com:

- GitHub Actions
- AWS CodePipeline
- Jenkins
- Azure DevOps

---

# Quando Utilizar CloudFormation

CloudFormation é indicado quando:

- existem múltiplos ambientes;
- há necessidade de escalabilidade;
- a infraestrutura precisa ser reproduzida;
- a empresa adota DevOps;
- existe preocupação com governança.

---

# Aprendizados Obtidos

Durante este laboratório foi possível compreender que o CloudFormation não é apenas uma ferramenta de automação.

Ele representa uma mudança de paradigma:

Antes:
Infraestrutura criada manualmente.

Depois:
Infraestrutura tratada como software.

Essa abordagem reduz riscos, aumenta produtividade e permite que equipes escalem operações com maior segurança.

---

# Próximos Passos

- Estudar Nested Stacks
- Implementar Change Sets
- Integrar com CI/CD
- Utilizar StackSets
- Explorar módulos reutilizáveis

---

# Conclusão

AWS CloudFormation é uma das ferramentas mais importantes para profissionais de Cloud Computing, DevOps e Arquitetura de Soluções.

Seu principal valor não está apenas em criar recursos automaticamente, mas em permitir que a infraestrutura seja documentada, versionada e reproduzida de forma confiável.

Em ambientes modernos, infraestrutura manual não escala.

Infrastructure as Code escala.
