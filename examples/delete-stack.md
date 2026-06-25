# 🧹 Removendo uma Stack no AWS CloudFormation

## Problema de Negócio

Recursos não utilizados continuam gerando custos.

Ao finalizar testes ou laboratórios é importante remover a infraestrutura provisionada.

---

# Contexto

O CloudFormation gerencia todo o ciclo de vida dos recursos criados por uma stack.

Ao excluir uma stack, o serviço remove automaticamente os recursos associados.

---

# Exclusão Pelo Console AWS

## Passo 1

Abra:

```text
CloudFormation
```

---

## Passo 2

Selecione a stack.

Exemplo:

```text
WebServerStack
```

---

## Passo 3

Clique em:

```text
Delete
```

---

## Passo 4

Confirme:

```text
Delete Stack
```

---

## Passo 5

Acompanhe:

```text
DELETE_IN_PROGRESS
```

---

## Passo 6

Aguarde:

```text
DELETE_COMPLETE
```

A stack desaparecerá da lista.

---

# Exclusão Pela AWS CLI

Comando:

```bash
aws cloudformation delete-stack \
--stack-name WebServerStack
```

---

# Consultando o Status

```bash
aws cloudformation describe-stacks \
--stack-name WebServerStack
```

Enquanto existir:

```text
DELETE_IN_PROGRESS
```

---

# Monitorando Eventos

```bash
aws cloudformation describe-stack-events \
--stack-name WebServerStack
```

---

# Verificando Exclusão

```bash
aws cloudformation list-stacks
```

A stack não deverá mais aparecer como ativa.

---

# Atenção ao Amazon S3

Caso tenha criado buckets manualmente:

1. Esvazie o bucket
2. Remova os objetos
3. Exclua o bucket

O CloudFormation não remove buckets que contenham arquivos.

---

# Problemas Comuns

## Bucket não vazio

Erro:

```text
Bucket is not empty
```

Solução:

```text
Excluir todos os objetos antes da remoção.
```

---

## Recursos protegidos

Erro:

```text
DELETE_FAILED
```

Solução:

```text
Remover políticas de proteção ou dependências.
```

---

# Insights

A exclusão controlada é tão importante quanto o provisionamento.

Uma boa governança cloud exige:

- controle de custos;
- limpeza de ambientes;
- rastreabilidade.

---

# Resultado

Todos os recursos provisionados pela stack são removidos de forma centralizada e segura.

---

# Próximos Passos

- Automatizar limpeza de ambientes
- Criar ambientes temporários
- Implementar políticas de lifecycle
- Integrar governança financeira na AWS
