# 🚀 Deploy de Stacks Utilizando AWS CLI

## Problema de Negócio

Em ambientes corporativos, criar recursos manualmente pelo console AWS pode gerar:

- inconsistências entre ambientes;
- erros humanos;
- baixa rastreabilidade;
- dificuldade de automação.

A utilização da AWS CLI permite executar deploys padronizados e reproduzíveis.

---

# Contexto

Neste projeto utilizamos o AWS CloudFormation para provisionar infraestrutura através de templates YAML.

O deploy via AWS CLI é amplamente utilizado por:

- Cloud Engineers
- DevOps Engineers
- SREs
- Cloud Architects

---

# Pré-requisitos

Antes de iniciar, certifique-se de possuir:

- Conta AWS ativa
- AWS CLI instalada
- Credenciais configuradas
- Permissões para CloudFormation
- Templates disponíveis localmente

Verifique a instalação:

```bash
aws --version
```

Exemplo:

```bash
aws-cli/2.x.x Python/3.x
```

---

# Configuração Inicial

Configure suas credenciais:

```bash
aws configure
```

Informe:

```text
AWS Access Key ID
AWS Secret Access Key
Default Region
Default Output Format
```

Exemplo:

```text
AWS Access Key ID: AKIA...
AWS Secret Access Key: ********
Default Region: us-east-1
Default Output Format: json
```

---

# Validando um Template

Antes do deploy:

```bash
aws cloudformation validate-template \
--template-body file://templates/webserver-stack.yaml
```

Saída esperada:

```json
{
  "Description": "Web Server Stack"
}
```

---

# Criando uma Stack

Exemplo utilizando o template WebServer:

```bash
aws cloudformation create-stack \
--stack-name WebServerStack \
--template-body file://templates/webserver-stack.yaml \
--parameters file://templates/parameters.json
```

---

# Monitorando o Deploy

Consultar status:

```bash
aws cloudformation describe-stacks \
--stack-name WebServerStack
```

Consultar eventos:

```bash
aws cloudformation describe-stack-events \
--stack-name WebServerStack
```

---

# Listando Stacks

```bash
aws cloudformation list-stacks
```

---

# Obtendo Outputs

```bash
aws cloudformation describe-stacks \
--stack-name WebServerStack \
--query "Stacks[0].Outputs"
```

---

# Atualizando uma Stack

```bash
aws cloudformation update-stack \
--stack-name WebServerStack \
--template-body file://templates/webserver-stack.yaml \
--parameters file://templates/parameters.json
```

---

# Insights

Deploys automatizados:

- reduzem erros;
- aceleram entregas;
- aumentam consistência;
- facilitam auditorias.

---

# Resultado

A infraestrutura passa a ser criada utilizando código versionado, eliminando dependência de configurações manuais.

---

# Próximos Passos

- Integrar AWS CLI com GitHub Actions
- Automatizar validações
- Criar pipelines CI/CD
- Implementar testes de infraestrutura
