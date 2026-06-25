# Limpeza de Recursos (Cleanup)

## Visão Geral

Um dos princípios fundamentais da computação em nuvem é pagar apenas pelos recursos utilizados.

Por isso, após concluir laboratórios e testes, é essencial remover todos os recursos provisionados para evitar custos desnecessários.

Este documento apresenta o processo de limpeza dos recursos criados durante este projeto.

---

# Problema de Negócio

Em ambientes corporativos, recursos esquecidos geram:

- desperdício financeiro;
- riscos de segurança;
- ambientes não gerenciados;
- aumento da complexidade operacional.

Uma boa governança exige processos claros de encerramento e remoção.

---

# Recursos Criados

Durante este laboratório foram utilizados:

- CloudFormation Stacks
- EC2
- Security Groups
- S3
- IAM
- CloudWatch
- SNS
- RDS

---

# Estratégia de Limpeza

A estratégia recomendada é remover os recursos através da própria Stack.

Isso garante:

- consistência;
- rastreabilidade;
- remoção ordenada.

---

# Excluindo uma Stack

Acessar:

```text
AWS Console
→ CloudFormation
→ Stacks
```

Selecionar:

```text
MyTestStack
```

Escolher:

```text
Delete
```

---

# Fluxo de Exclusão

```text
DELETE_IN_PROGRESS

        ↓

Remoção dos Recursos

        ↓

DELETE_COMPLETE
```

---

# Verificando Exclusão

Após a remoção:

Verificar:

- EC2
- Security Groups
- S3
- CloudWatch
- SNS

Nenhum recurso deve permanecer ativo.

---

# Exclusão de Buckets S3

Antes de excluir:

1. Esvaziar bucket
2. Excluir bucket

---

## Passo 1

```text
S3
→ Bucket
→ Empty
```

---

## Passo 2

```text
Delete Bucket
```

---

# Boas Práticas de Cleanup

## Utilizar Tags

Exemplo:

```yaml
Tags:

  - Key: Environment
    Value: Lab
```

Facilita identificação posterior.

---

## Automatizar Exclusões

Utilizar:

- Lambda
- EventBridge
- Lifecycle Policies

---

## Revisar Custos

Consultar:

```text
AWS Billing Dashboard
```

---

# Benefícios

## Redução de Custos

Evita cobranças indevidas.

---

## Segurança

Remove recursos expostos.

---

## Governança

Mantém o ambiente organizado.

---

# Aprendizados

Criar infraestrutura é importante.

Remover infraestrutura corretamente é igualmente importante.

Ambientes corporativos maduros possuem processos bem definidos tanto para provisionamento quanto para descomissionamento.

---

# Próximos Passos

- AWS Budgets
- Cost Explorer
- Lifecycle Policies
- Resource Groups

---

# Conclusão

Uma estratégia eficiente de cleanup reduz custos, melhora a governança e demonstra maturidade operacional.

Na nuvem, recursos esquecidos podem se transformar rapidamente em desperdício financeiro.
