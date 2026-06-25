# Conceitos Fundamentais do AWS CloudFormation

## Visão Geral

Antes de criar stacks em produção é fundamental compreender os principais componentes que compõem o AWS CloudFormation.

Esses conceitos são a base para qualquer implementação de Infrastructure as Code na AWS.

---

# Problema de Negócio

Empresas frequentemente enfrentam dificuldades para manter ambientes consistentes.

O problema geralmente não está na criação dos recursos, mas na ausência de padronização.

CloudFormation resolve esse desafio através de componentes estruturados que trabalham em conjunto.

---

# Arquitetura Conceitual

```text
Template
    ↓

Stack

    ↓

Resources

    ↓

Infrastructure
```

---

# Templates

Templates são arquivos que descrevem a infraestrutura.

Podem ser escritos em:

- YAML
- JSON

Exemplo:

```yaml
Resources:

  MyBucket:

    Type: AWS::S3::Bucket
```

O template representa o projeto da infraestrutura.

---

# Stacks

Uma Stack é uma instância de um template.

Podemos imaginar:

Template = Planta do edifício

Stack = Edifício construído

O mesmo template pode gerar várias stacks.

Exemplo:

- Dev Stack
- Homolog Stack
- Production Stack

---

# Resources

Resources representam os serviços AWS que serão criados.

Exemplos:

- AWS::EC2::Instance
- AWS::S3::Bucket
- AWS::RDS::DBInstance
- AWS::IAM::Role

A seção Resources é o coração do template.

---

# Parameters

Permitem tornar os templates reutilizáveis.

Exemplo:

```yaml
Parameters:

  InstanceType:

    Type: String

    Default: t2.micro
```

Assim o mesmo template pode criar diferentes tipos de instância.

---

# Outputs

Retornam informações após a criação da stack.

Exemplo:

```yaml
Outputs:

  InstanceId:

    Value: !Ref WebServer
```

São muito utilizados em integrações entre stacks.

---

# Mappings

Permitem criar tabelas de consulta.

Exemplo:

```yaml
Mappings:
```

Podem variar configurações por região.

---

# Conditions

Permitem lógica condicional.

Exemplo:

Criar recurso apenas em produção.

---

# Intrinsic Functions

São funções internas do CloudFormation.

Principais:

- Ref
- GetAtt
- Join
- Sub
- ImportValue

Exemplo:

```yaml
!Ref WebServer
```

---

# Dependências

CloudFormation cria dependências automaticamente.

Exemplo:

Uma instância EC2 depende de um Security Group.

A ordem correta é gerenciada automaticamente.

---

# Change Sets

Permitem visualizar alterações antes da execução.

Benefícios:

- reduzir riscos;
- validar mudanças;
- evitar indisponibilidade.

---

# Aprendizados

Compreender os conceitos fundamentais é mais importante do que decorar sintaxe.

O profissional que entende:

- Templates
- Resources
- Parameters
- Outputs

consegue evoluir rapidamente para arquiteturas mais complexas.

---

# Próximos Passos

- Nested Stacks
- Cross Stack References
- StackSets
- Macros
- CloudFormation Registry

---

# Conclusão

Os conceitos fundamentais do CloudFormation formam a base para ambientes modernos baseados em Infrastructure as Code.

Dominar esses elementos é essencial para qualquer profissional que deseja atuar com Cloud Engineering, DevOps ou Arquitetura de Soluções.
