# Criando uma Stack EC2 Web Server com AWS CloudFormation

## Visão Geral

Uma das tarefas mais comuns em Cloud Computing é disponibilizar aplicações web de forma rápida, padronizada e reproduzível.

Neste laboratório foi criada uma Stack CloudFormation capaz de provisionar automaticamente:

- Instância Amazon EC2
- Security Group
- Servidor Apache HTTP
- Página Web de teste
- URL pública para acesso

Tudo utilizando Infrastructure as Code (IaC).

---

# Problema de Negócio

Imagine uma equipe de desenvolvimento que precisa criar ambientes de teste constantemente.

Se cada servidor for criado manualmente:

- o tempo de provisionamento aumenta;
- erros de configuração se tornam frequentes;
- ambientes ficam inconsistentes.

O desafio é garantir que qualquer ambiente seja criado de forma idêntica e repetível.

---

# Contexto

Empresas modernas trabalham com:

- múltiplos ambientes;
- pipelines CI/CD;
- escalabilidade;
- recuperação de desastres.

Nesses cenários, criar servidores manualmente não é sustentável.

CloudFormation permite automatizar esse processo.

---

# Arquitetura da Solução

```text
CloudFormation Stack

├── Security Group
│
└── EC2 Instance
      │
      └── Apache HTTP Server
                │
                └── Página Hello World
```

---

# Template Utilizado

O template cria:

## Security Group

Permite acesso HTTP na porta 80.

```yaml
SecurityGroupIngress:

  - IpProtocol: tcp
    FromPort: 80
    ToPort: 80
```

---

## EC2 Instance

Provisiona uma máquina virtual Amazon Linux.

```yaml
Type: AWS::EC2::Instance
```

---

## UserData

Executa comandos automaticamente durante a inicialização.

```bash
yum update -y
yum install -y httpd
systemctl start httpd
```

---

# Decisões Técnicas

## Amazon Linux

Escolhido por:

- compatibilidade com AWS;
- manutenção simplificada;
- suporte oficial.

---

## Apache HTTP Server

Selecionado por:

- simplicidade;
- ampla adoção;
- facilidade de demonstração.

---

## CloudFormation YAML

Escolhido devido:

- legibilidade;
- facilidade de manutenção;
- ampla utilização pelo mercado.

---

# Benefícios da Solução

## Padronização

Todos os servidores são criados da mesma forma.

## Automação

Sem necessidade de configuração manual.

## Reprodutibilidade

O ambiente pode ser recriado a qualquer momento.

## Governança

Toda infraestrutura fica documentada.

---

# Resultado Obtido

Ao executar a Stack:

- Security Group criado;
- EC2 provisionada;
- Apache instalado automaticamente;
- Página Hello World publicada.

A URL do servidor é retornada através da seção Outputs.

---

# Aprendizados

Durante este laboratório foi possível compreender:

- estrutura de um template CloudFormation;
- uso de Parameters;
- criação de Resources;
- utilização de Outputs;
- automação com UserData.

---

# Próximos Passos

- HTTPS com ACM
- Load Balancer
- Auto Scaling
- CloudWatch Monitoring
- Deploy automatizado

---

# Conclusão

A Stack EC2 Web Server demonstra como Infrastructure as Code reduz erros operacionais e acelera a entrega de ambientes.

Mesmo sendo um exemplo simples, ela representa a base de arquiteturas utilizadas diariamente em ambientes corporativos.
