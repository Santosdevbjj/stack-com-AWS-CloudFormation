# Como Funcionam as Stacks no AWS CloudFormation

## Visão Geral

Stacks são o principal mecanismo de implantação do AWS CloudFormation.

Compreender seu funcionamento é essencial para criar ambientes confiáveis, reproduzíveis e escaláveis.

---

# Problema de Negócio

Uma empresa precisa provisionar dezenas de recursos:

- EC2
- VPC
- Subnets
- Security Groups
- RDS
- S3

Criar tudo manualmente exige tempo e aumenta a probabilidade de erro.

Além disso, recriar um ambiente idêntico torna-se extremamente difícil.

O CloudFormation resolve esse problema através das Stacks.

---

# O Que é uma Stack

Uma Stack é um conjunto de recursos AWS criado e gerenciado como uma única unidade.

Exemplo:

```text
Stack Produção

├── VPC
├── Subnets
├── Security Groups
├── EC2
├── Load Balancer
├── RDS
└── CloudWatch
```

Todos esses recursos são controlados por uma única Stack.

---

# Ciclo de Vida de uma Stack

## CREATE_IN_PROGRESS

A AWS iniciou o provisionamento.

---

## CREATE_COMPLETE

Todos os recursos foram criados com sucesso.

---

## UPDATE_IN_PROGRESS

A Stack está sendo atualizada.

---

## UPDATE_COMPLETE

Atualização concluída.

---

## DELETE_IN_PROGRESS

Recursos sendo removidos.

---

## DELETE_COMPLETE

Stack removida.

---

# Como o CloudFormation Cria Recursos

Quando uma Stack é criada:

1. Lê o template
2. Identifica recursos
3. Avalia dependências
4. Cria recursos na ordem correta
5. Retorna outputs

---

# Eventos da Stack

Durante a execução o CloudFormation gera eventos.

Exemplo:

```text
CREATE_IN_PROGRESS

CREATE_COMPLETE

UPDATE_IN_PROGRESS

UPDATE_COMPLETE
```

Esses eventos ajudam na auditoria e troubleshooting.

---

# Rollback Automático

Se ocorrer falha:

```text
CREATE_FAILED

ROLLBACK_IN_PROGRESS

ROLLBACK_COMPLETE
```

O CloudFormation remove automaticamente os recursos criados.

Isso evita ambientes inconsistentes.

---

# Nested Stacks

Stacks podem conter outras stacks.

Exemplo:

```text
Main Stack

├── Network Stack
├── Security Stack
├── Database Stack
└── Compute Stack
```

Benefícios:

- modularidade;
- reutilização;
- manutenção simplificada.

---

# Vantagens das Stacks

## Governança

Infraestrutura centralizada.

## Segurança

Mudanças controladas.

## Auditoria

Histórico completo.

## Escalabilidade

Provisionamento automatizado.

## Reutilização

Templates compartilháveis.

---

# Aprendizados Obtidos

Durante este laboratório ficou evidente que as Stacks são muito mais do que um mecanismo de criação de recursos.

Elas representam uma forma estruturada de gerenciar infraestrutura em escala, permitindo que ambientes complexos sejam reproduzidos de forma segura e previsível.

---

# Próximos Passos

- Nested Stacks
- Stack Policies
- StackSets
- Drift Detection
- CI/CD com CloudFormation

---

# Conclusão

Stacks são a unidade fundamental do AWS CloudFormation.

Elas permitem transformar infraestrutura em código, garantindo padronização, rastreabilidade e automação.

Dominar Stacks é um passo essencial para qualquer profissional que deseja atuar em Cloud Computing de forma profissional.
