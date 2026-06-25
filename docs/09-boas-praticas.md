# Boas Práticas com AWS CloudFormation

## Visão Geral

CloudFormation permite automatizar a criação de infraestrutura em escala.

Entretanto, a simples automação não garante qualidade.

A adoção de boas práticas é essencial para criar ambientes seguros, reutilizáveis e fáceis de manter.

---

# Problema de Negócio

À medida que a infraestrutura cresce, também cresce a complexidade.

Sem padrões claros surgem problemas como:

- duplicação de código;
- configurações inconsistentes;
- baixa manutenibilidade;
- aumento de riscos operacionais.

O objetivo é construir templates robustos e escaláveis.

---

# 1. Utilizar YAML

Preferir YAML ao JSON.

Exemplo:

```yaml
Resources:

  MyBucket:

    Type: AWS::S3::Bucket
```

Benefícios:

- maior legibilidade;
- manutenção simplificada.

---

# 2. Utilizar Parameters

Evitar valores fixos.

Ruim:

```yaml
InstanceType: t2.micro
```

Melhor:

```yaml
Parameters:

  InstanceType:
```

---

# 3. Utilizar Outputs

Facilita integração entre Stacks.

Exemplo:

```yaml
Outputs:
```

---

# 4. Modularizar Templates

Separar responsabilidades.

Exemplo:

```text
network-stack.yaml

security-stack.yaml

database-stack.yaml
```

---

# 5. Utilizar Nested Stacks

Para ambientes complexos.

Benefícios:

- reutilização;
- manutenção;
- escalabilidade.

---

# 6. Aplicar Tags

Exemplo:

```yaml
Tags:

  - Key: Project
    Value: CloudFormationLab
```

Permite:

- governança;
- auditoria;
- controle financeiro.

---

# 7. Restringir Acessos

Evitar:

```text
0.0.0.0/0
```

Sempre que possível.

Aplicar princípio do menor privilégio.

---

# 8. Utilizar IAM Roles

Evitar credenciais fixas.

Boa prática:

```text
IAM Role
```

---

# 9. Habilitar Monitoramento

Integrar:

- CloudWatch
- SNS
- EventBridge

---

# 10. Versionar Tudo

Armazenar templates em:

- GitHub
- GitLab
- Bitbucket

---

# 11. Validar Antes do Deploy

Executar:

```bash
aws cloudformation validate-template \
--template-body file://template.yaml
```

---

# 12. Utilizar Change Sets

Permite visualizar alterações antes da execução.

Benefícios:

- redução de riscos;
- maior previsibilidade.

---

# 13. Implementar Drift Detection

Detecta alterações manuais realizadas fora do CloudFormation.

---

# 14. Utilizar Naming Convention

Exemplo:

```text
project-environment-resource
```

---

## Exemplo

```text
cloudformation-dev-webserver
```

---

# Benefícios Obtidos

## Escalabilidade

Infraestrutura cresce de forma organizada.

---

## Segurança

Menor superfície de ataque.

---

## Governança

Melhor rastreabilidade.

---

## Reutilização

Templates reaproveitáveis.

---

## Produtividade

Provisionamento rápido.

---

# Aprendizados

A diferença entre um template funcional e um template profissional está na adoção consistente de boas práticas.

Essas recomendações refletem padrões utilizados em ambientes corporativos e arquiteturas modernas na AWS.

---

# Próximos Passos

- StackSets
- CDK
- Terraform
- GitHub Actions
- AWS CodePipeline

---

# Conclusão

Boas práticas não existem para aumentar burocracia.

Elas existem para reduzir riscos, melhorar a qualidade da infraestrutura e permitir crescimento sustentável ao longo do tempo.

Infraestrutura profissional não é apenas aquela que funciona.

É aquela que continua funcionando quando o ambiente cresce.
