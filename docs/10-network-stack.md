## 🌐 Network Stack com AWS CloudFormation

## Problema de Negócio

Empresas modernas precisam implantar aplicações de forma rápida, segura e repetível.

## Quando redes são configuradas manualmente:

- surgem erros de configuração;
- equipes perdem produtividade;
- ambientes ficam inconsistentes;
- auditorias tornam-se difíceis.

O desafio é criar uma infraestrutura de rede padronizada, reutilizável e versionada.

---

## Contexto

Toda aplicação AWS depende de uma camada de rede.

## Essa camada normalmente inclui:

- VPC
- Subnets
- Internet Gateway
- Route Tables
- Security Controls

## Sem uma arquitetura de rede bem definida:

- aplicações podem ficar inacessíveis;
- recursos podem ficar expostos à internet;
- custos podem aumentar.

---

## Premissas

Para este projeto foram consideradas as seguintes premissas:

- Utilização de uma VPC dedicada.
- Separação entre recursos públicos e privados.
- Comunicação segura entre componentes.
- Infraestrutura definida como código.
- Reutilização em múltiplos ambientes.

---

## Estratégia da Solução

## A stack de rede cria automaticamente:

1. VPC
2. Subnets Públicas
3. Subnets Privadas
4. Internet Gateway
5. Route Tables
6. Associação de Rotas

---

## Estrutura da Solução

```
Internet
    │
Internet Gateway
    │
VPC
├── Public Subnet
│   ├── EC2
│   └── Load Balancer
│
└── Private Subnet
    ├── RDS
    └── Application Servers

```
---

### Template CloudFormation

## Arquivo:

```
templates/network-stack.yaml

```


## Principais recursos:

```

AWS::EC2::VPC
AWS::EC2::Subnet
AWS::EC2::InternetGateway
AWS::EC2::RouteTable

```

---

## Insights

Infraestrutura de rede costuma representar a fundação de qualquer ambiente AWS.

## Uma boa arquitetura reduz:

- riscos de segurança;
- falhas operacionais;
- tempo de provisionamento.

---

## Resultados

Com essa stack é possível:

✅ Criar ambientes reproduzíveis

✅ Automatizar configurações

✅ Eliminar erros manuais

✅ Seguir boas práticas AWS

---

## Próximos Passos

- Implementar NAT Gateway
- Multi-AZ
- VPC Endpoints
- Transit Gateway
- IPv6

---

## Aprendizados

A rede é a base da arquitetura em nuvem.

Automatizar sua criação com CloudFormation aumenta segurança, governança e escalabilidade.
