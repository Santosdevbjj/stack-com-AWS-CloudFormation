# Monitoramento e Eventos no AWS CloudFormation

## Visão Geral

Criar infraestrutura é apenas parte do trabalho.

Também é necessário monitorar:

- criação;
- atualização;
- exclusão;
- falhas.

O CloudFormation disponibiliza um sistema completo de eventos para acompanhar todo o ciclo de vida das Stacks.

---

# Problema de Negócio

Imagine uma empresa implantando dezenas de recursos simultaneamente.

Sem monitoramento seria difícil identificar:

- falhas;
- dependências quebradas;
- recursos não criados;
- problemas de configuração.

O resultado seria perda de produtividade e aumento do tempo de resolução.

---

# Contexto

Durante qualquer execução o CloudFormation gera eventos automaticamente.

Esses eventos mostram:

- o que está acontecendo;
- qual recurso está sendo criado;
- possíveis erros;
- status atual da Stack.

---

# Fluxo de Eventos

```text
CREATE_IN_PROGRESS

        ↓

Resource Creation

        ↓

CREATE_COMPLETE
```

---

# Principais Status

## CREATE_IN_PROGRESS

Indica que a Stack está sendo criada.

---

## CREATE_COMPLETE

Criação concluída com sucesso.

---

## CREATE_FAILED

Falha durante a criação.

---

## UPDATE_IN_PROGRESS

Atualização em andamento.

---

## UPDATE_COMPLETE

Atualização concluída.

---

## DELETE_IN_PROGRESS

Exclusão iniciada.

---

## DELETE_COMPLETE

Exclusão concluída.

---

# Rollback Automático

Uma das funcionalidades mais importantes do CloudFormation.

Exemplo:

```text
CREATE_FAILED

↓

ROLLBACK_IN_PROGRESS

↓

ROLLBACK_COMPLETE
```

Se ocorrer erro, os recursos criados são removidos automaticamente.

---

# Benefícios do Monitoramento

## Diagnóstico

Identificação rápida de falhas.

## Auditoria

Histórico completo de alterações.

## Governança

Rastreamento das operações.

## Confiabilidade

Maior controle operacional.

---

# Integração com CloudWatch

Eventos podem ser integrados ao:

- Amazon CloudWatch
- SNS
- Lambda
- EventBridge

Permitindo alertas automáticos.

---

# Exemplo de Fluxo Corporativo

```text
CloudFormation

      ↓

CloudWatch Events

      ↓

SNS

      ↓

E-mail / Slack / Teams
```

---

# Resultados Obtidos

Durante este laboratório foi possível:

- acompanhar eventos em tempo real;
- identificar recursos criados;
- validar execução da Stack;
- compreender o processo de rollback.

---

# Aprendizados

Monitoramento não serve apenas para detectar erros.

Ele fornece visibilidade operacional e aumenta a confiabilidade da infraestrutura.

Essa é uma prática essencial em ambientes corporativos.

---

# Próximos Passos

- CloudWatch Alarms
- SNS Notifications
- EventBridge
- AWS Config
- CloudTrail

---

# Conclusão

O monitoramento de eventos do CloudFormation fornece transparência durante todo o ciclo de vida da infraestrutura.

Ele transforma processos complexos em operações rastreáveis, auditáveis e muito mais seguras.
