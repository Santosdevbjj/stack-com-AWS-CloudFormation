# 🖥️ Deploy de Stacks Utilizando o Console AWS

## Problema de Negócio

Nem todos os profissionais trabalham inicialmente com automação via CLI.

Compreender o fluxo pelo Console AWS ajuda a visualizar o comportamento do CloudFormation antes da automação completa.

---

# Contexto

O AWS CloudFormation permite criar recursos através de templates YAML ou JSON diretamente pelo Console AWS.

---

# Passo 1 — Acessar o CloudFormation

Abra:

https://console.aws.amazon.com/cloudformation

Clique em:

```text
Create Stack
```

---

# Passo 2 — Escolher Template

Selecione:

```text
Template is ready
```

Escolha:

```text
Upload a template file
```

Envie:

```text
templates/webserver-stack.yaml
```

Clique em:

```text
Next
```

---

# Passo 3 — Nome da Stack

Exemplo:

```text
WebServerStack
```

---

# Passo 4 — Informar Parâmetros

Exemplo:

```text
InstanceType = t2.micro
MyIP = 0.0.0.0/0
```

---

# Passo 5 — Configurações

Mantenha os padrões para:

- Tags
- Notifications
- Rollback

Clique:

```text
Next
```

---

# Passo 6 — Revisão

Revise:

- Nome da Stack
- Recursos
- Parâmetros

Clique:

```text
Submit
```

---

# Passo 7 — Monitoramento

Acompanhe:

```text
CREATE_IN_PROGRESS
```

Depois:

```text
CREATE_COMPLETE
```

---

# Visualizando Recursos

Acesse a aba:

```text
Resources
```

Exemplo:

- EC2 Instance
- Security Group

---

# Visualizando Eventos

Acesse:

```text
Events
```

Exemplo:

```text
CREATE_IN_PROGRESS
CREATE_COMPLETE
```

---

# Visualizando Outputs

Acesse:

```text
Outputs
```

Exemplo:

```text
WebsiteURL
```

---

# Testando o Ambiente

Abra a URL exibida em Outputs.

Resultado esperado:

```html
Hello World!
```

---

# Insights

O Console AWS facilita:

- aprendizado;
- validação inicial;
- troubleshooting.

Porém ambientes corporativos normalmente utilizam automação via CLI ou CI/CD.

---

# Resultado

Deploy realizado com sucesso através da interface gráfica do CloudFormation.

---

# Próximos Passos

- Utilizar AWS CLI
- Automatizar deploys
- Integrar GitHub Actions
- Implementar Infraestrutura como Código completa
