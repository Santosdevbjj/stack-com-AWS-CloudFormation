## AWS Well-Architected Framework

Boas práticas de IaC da AWS

Documentação de nível Open Source



---

Estrutura do repositório

```

stack-com-AWS-CloudFormation/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   │
│   ├── 01-o-que-e-cloudformation.md
│   ├── 02-conceitos-fundamentais.md
│   ├── 03-como-funcionam-stacks.md
│   ├── 04-stack-ec2-webserver.md
│   ├── 05-stack-firewall-security-group.md
│   ├── 06-monitoramento-e-eventos.md
│   ├── 07-troubleshooting.md
│   ├── 08-cleanup.md
│   ├── 09-boas-praticas.md
│   └── 10-insights-e-aprendizados.md
│
├── templates/
│   │
│   ├── webserver-stack.yaml
│   ├── firewall-stack.yaml
│   └── parameters.json
│
├── images/
│   │
│   ├── architecture.png
│   ├── create-stack.png
│   ├── stack-events.png
│   ├── outputs.png
│   └── firewall.png
│
├── diagrams/
│   ├── architecture.drawio
│   └── cloudformation-stack.drawio
│
├── examples/
│   ├── deploy-cli.md
│   ├── deploy-console.md
│   └── delete-stack.md
│
└── assets/
      ├── banner.png
      └── aws-cloudformation-logo.png


```

---

README principal

☁️ Implementando sua Primeira Stack com AWS CloudFormation

> Automatizando infraestrutura na AWS através de Infrastructure as Code (IaC), utilizando CloudFormation para provisionar servidores EC2 e regras de segurança reproduzíveis e versionadas.




---

Problema de Negócio

Provisionar infraestrutura manualmente gera:

configurações inconsistentes;

erros humanos;

dificuldade de reproduzir ambientes;

maior tempo de implantação;

ausência de versionamento.


Em ambientes corporativos, esses problemas comprometem a escalabilidade e a governança da infraestrutura.


---

Contexto

Equipes modernas adotam Infrastructure as Code (IaC) para:

padronizar ambientes;

automatizar deploys;

reduzir erros operacionais;

facilitar auditorias;

aumentar a velocidade de entrega.


O AWS CloudFormation permite transformar infraestrutura em código utilizando templates YAML ou JSON.


---

Objetivo

Demonstrar como utilizar o AWS CloudFormation para:

✔ Criar Stacks

✔ Provisionar uma instância EC2

✔ Criar um Web Server Apache

✔ Configurar Security Groups

✔ Implementar regras de Firewall

✔ Monitorar eventos da Stack

✔ Remover recursos com segurança


---

Arquitetura

Internet
                     │
                     ▼
             Security Group
               (porta 80)
                     │
                     ▼
              Amazon EC2
             Apache Web Server
                     │
                     ▼
              Hello World Page


---

Tecnologias Utilizadas

AWS CloudFormation

Amazon EC2

Amazon Linux 2

Security Groups

Amazon S3

YAML

Infrastructure as Code (IaC)



---

Estrutura do Projeto

docs/
templates/
images/
examples/
diagrams/


---

Implementações Realizadas

1. O que é AWS CloudFormation

Explicação dos conceitos:

Stack

Template

Resources

Parameters

Outputs

Logical IDs


Arquivo:

docs/01-o-que-e-cloudformation.md


---

2. Criando Stacks

Implementação:

Template:

templates/webserver-stack.yaml

Recursos provisionados:

EC2

Apache HTTP Server

Security Group


Resultado:

Página:

Hello World


---

3. Criando Stacks de Firewall

Template:

templates/firewall-stack.yaml

Regras implementadas:

HTTP:

80

SSH:

22

CIDR personalizado

Security Groups reutilizáveis.


---

Estratégia da Solução

Entendimento do problema

Eliminar provisionamento manual.

Modelagem da solução

CloudFormation + YAML.

Provisionamento

EC2 + Security Group.

Monitoramento

Eventos da Stack.

Outputs

DNS público do servidor.

Limpeza

Delete Stack.


---

Insights

Infrastructure as Code oferece:

repetibilidade;

rastreabilidade;

versionamento;

facilidade de rollback;

redução de erros humanos.



---

Resultados

Foi possível:

✔ Provisionar infraestrutura automaticamente.

✔ Criar servidores reproduzíveis.

✔ Implementar regras de segurança.

✔ Utilizar templates reutilizáveis.

✔ Praticar conceitos fundamentais de IaC.


---

Próximos Passos

Nested Stacks;

Change Sets;

StackSets;

Mappings;

Conditions;

Outputs avançados;

Integração com CI/CD;

AWS SAM;

CDK;

Terraform;

Multi-account deployments.



---

Arquivos importantes

templates/webserver-stack.yaml

Servidor Apache.

templates/firewall-stack.yaml

Firewall com Security Groups.

docs/

Documentação detalhada.


---

Referências

AWS Documentation

AWS Well-Architected Framework

AWS CloudFormation User Guide


---

Arquivos que eu criaria

templates/webserver-stack.yaml

AWSTemplateFormatVersion: '2010-09-09'

Description: Web Server Stack

Parameters:

  InstanceType:
    Type: String
    Default: t2.micro

Resources:

  WebServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: HTTP access

      SecurityGroupIngress:

        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

  WebServer:

    Type: AWS::EC2::Instance

    Properties:

      ImageId: ami-id

      InstanceType: !Ref InstanceType

      SecurityGroupIds:
        - !Ref WebServerSecurityGroup

Outputs:

  InstanceId:

    Value: !Ref WebServer


---

templates/firewall-stack.yaml

AWSTemplateFormatVersion: '2010-09-09'

Description: Firewall Stack

Resources:

  FirewallSecurityGroup:

    Type: AWS::EC2::SecurityGroup

    Properties:

      GroupDescription: Security Group

      SecurityGroupIngress:

        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: x.x.x.x/32

        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

About do GitHub

Seguindo seu padrão dos pipes:

Provisionamento manual de infraestrutura gera erros e falta de padronização | Automação de recursos AWS utilizando CloudFormation e Infrastructure as Code | Ambientes reproduzíveis, seguros e escaláveis

---

A pasta templates/ deve seguir uma abordagem profissional de Infrastructure as Code, permitindo reutilização e separação entre o template e os valores dos parâmetros. O arquivo parameters.json servirá para alimentar os templates webserver-stack.yaml e firewall-stack.yaml, facilitando mudanças de ambiente sem alterar o código da infraestrutura.

📂 templates/parameters.json

[
  {
    "ParameterKey": "LatestAmiId",
    "ParameterValue": "/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"
  },
  {
    "ParameterKey": "InstanceType",
    "ParameterValue": "t2.micro"
  },
  {
    "ParameterKey": "MyIP",
    "ParameterValue": "0.0.0.0/0"
  },
  {
    "ParameterKey": "VpcId",
    "ParameterValue": "vpc-xxxxxxxx"
  },
  {
    "ParameterKey": "SubnetId",
    "ParameterValue": "subnet-xxxxxxxx"
  },
  {
    "ParameterKey": "KeyName",
    "ParameterValue": "my-keypair"
  },
  {
    "ParameterKey": "Environment",
    "ParameterValue": "dev"
  },
  {
    "ParameterKey": "ProjectName",
    "ParameterValue": "cloudformation-lab"
  },
  {
    "ParameterKey": "SSHLocation",
    "ParameterValue": "203.0.113.10/32"
  },
  {
    "ParameterKey": "HTTPPort",
    "ParameterValue": "80"
  },
  {
    "ParameterKey": "HTTPSPort",
    "ParameterValue": "443"
  },
  {
    "ParameterKey": "SSHPort",
    "ParameterValue": "22"
  },
  {
    "ParameterKey": "AllowedCIDR",
    "ParameterValue": "0.0.0.0/0"
  }
]


---

Estrutura esperada da pasta templates

templates/
│
├── webserver-stack.yaml
├── firewall-stack.yaml
└── parameters.json


---

Objetivo dos parâmetros

Parâmetro	Finalidade

LatestAmiId	Recupera automaticamente a AMI Amazon Linux 2 mais recente
InstanceType	Tipo da instância EC2
MyIP	Faixa de IP permitida para acesso HTTP
VpcId	VPC onde os recursos serão criados
SubnetId	Sub-rede utilizada pela EC2
KeyName	Chave SSH para acesso à instância
Environment	Ambiente (dev, test, prod)
ProjectName	Nome do projeto
SSHLocation	IP autorizado para SSH
HTTPPort	Porta HTTP
HTTPSPort	Porta HTTPS
SSHPort	Porta SSH
AllowedCIDR	Intervalo CIDR permitido



---

Exemplo de utilização

AWS CLI

aws cloudformation create-stack \
  --stack-name MyTestStack \
  --template-body file://templates/webserver-stack.yaml \
  --parameters file://templates/parameters.json

Atualização da Stack

aws cloudformation update-stack \
  --stack-name MyTestStack \
  --template-body file://templates/webserver-stack.yaml \
  --parameters file://templates/parameters.json

Exclusão da Stack

aws cloudformation delete-stack \
  --stack-name MyTestStack

Esse parameters.json foi pensado em nível profissional (FAANG), permitindo evolução futura para:

Multiambiente (dev, homolog, prod);

Nested Stacks;

CI/CD com GitHub Actions;

AWS CodePipeline;

StackSets;

Múltiplas regiões;

Infraestrutura escalável e reutilizável. 




---




