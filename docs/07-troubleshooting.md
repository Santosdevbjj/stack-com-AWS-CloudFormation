# Troubleshooting em AWS CloudFormation

## Visão Geral

Criar infraestrutura utilizando CloudFormation reduz erros operacionais, mas não elimina completamente problemas relacionados a permissões, rede, configuração de recursos e dependências.

Por isso, uma habilidade essencial para profissionais de Cloud Computing é a capacidade de diagnosticar e corrigir falhas durante a execução das Stacks.

Este documento apresenta os principais problemas encontrados durante implementações com AWS CloudFormation e suas respectivas soluções.

---

# Problema de Negócio

Imagine uma empresa que precisa provisionar rapidamente um ambiente para testes ou produção.

Se a Stack falhar:

- o projeto pode atrasar;
- equipes podem ficar bloqueadas;
- custos podem aumentar;
- a confiança na automação pode ser comprometida.

O objetivo é identificar rapidamente a causa raiz e restaurar a operação.

---

# Fluxo de Diagnóstico

```text
Stack Falhou

        ↓

Verificar Eventos

        ↓

Identificar Recurso

        ↓

Analisar Erro

        ↓

Corrigir Template

        ↓

Executar Novamente
```

---

# Erro: CREATE_FAILED

## Sintoma

A Stack entra no estado:

```text
CREATE_FAILED
```

---

## Causa

Falha na criação de algum recurso.

Exemplos:

- parâmetros inválidos;
- permissões insuficientes;
- dependências ausentes.

---

## Solução

Acessar:

```text
CloudFormation
→ Stacks
→ Events
```

Localizar o recurso que falhou e analisar a mensagem exibida.

---

# Erro: VPC Não Encontrada

## Sintoma

Mensagem semelhante a:

```text
No default VPC found
```

---

## Causa

A conta AWS não possui VPC padrão.

---

## Solução

Criar uma VPC padrão ou informar explicitamente:

```yaml
SubnetId:
  Type: AWS::EC2::Subnet::Id
```

---

# Erro: Security Group Inválido

## Sintoma

```text
InvalidGroup.NotFound
```

---

## Causa

O Security Group referenciado não existe.

---

## Solução

Verificar:

```yaml
SecurityGroupIds:
```

Confirmar IDs corretos.

---

# Erro: AccessDenied

## Sintoma

```text
AccessDenied
```

---

## Causa

Permissões IAM insuficientes.

---

## Solução

Validar políticas IAM.

Exemplo:

- EC2
- CloudFormation
- S3
- IAM
- CloudWatch

---

# Erro: Bucket Already Exists

## Sintoma

```text
Bucket name already exists
```

---

## Causa

Nomes de buckets S3 são globais.

---

## Solução

Utilizar nomes únicos.

Exemplo:

```text
sergio-cloudformation-lab-2026
```

---

# Erro: Template Validation Error

## Sintoma

```text
Template format error
```

---

## Causa

Problemas de sintaxe YAML.

---

## Solução

Executar validação:

```bash
aws cloudformation validate-template \
--template-body file://template.yaml
```

---

# Ferramentas de Diagnóstico

## CloudFormation Events

Identifica falhas em tempo real.

---

## CloudWatch

Monitora recursos provisionados.

---

## AWS CLI

Permite inspeção detalhada.

---

## CloudTrail

Audita operações executadas.

---

# Aprendizados

A maioria dos erros não está relacionada ao CloudFormation em si.

Normalmente os problemas estão ligados a:

- permissões;
- rede;
- parâmetros;
- dependências.

Compreender os eventos da Stack acelera significativamente a resolução.

---

# Próximos Passos

- CloudTrail
- AWS Config
- Drift Detection
- Change Sets

---

# Conclusão

Troubleshooting é uma das habilidades mais importantes para profissionais Cloud.

Saber interpretar eventos e diagnosticar falhas diferencia quem apenas utiliza ferramentas de quem realmente entende infraestrutura.
