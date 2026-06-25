# Criando uma Stack de Firewall com Security Groups

## Visão Geral

Segurança é um dos pilares fundamentais da computação em nuvem.

Neste laboratório foi criada uma Stack responsável por provisionar regras de firewall utilizando Security Groups da AWS.

---

# Problema de Negócio

Servidores expostos diretamente à internet representam um dos maiores riscos para qualquer organização.

Portas abertas indevidamente podem permitir:

- invasões;
- vazamento de dados;
- indisponibilidade de serviços.

O desafio é controlar rigorosamente quem pode acessar os recursos da infraestrutura.

---

# Contexto

Na AWS, Security Groups funcionam como firewalls virtuais.

Eles controlam:

- tráfego de entrada;
- tráfego de saída;
- protocolos;
- portas;
- intervalos de IP.

---

# Arquitetura da Solução

```text
Internet

     │

     ▼

Security Group

 ├── Porta 22 (SSH)
 └── Porta 80 (HTTP)

     │

     ▼

EC2 Instance
```

---

# Estratégia da Solução

Foi criada uma Stack CloudFormation contendo:

```yaml
AWS::EC2::SecurityGroup
```

com regras específicas para:

- SSH
- HTTP

---

# Regras Implementadas

## SSH

```yaml
FromPort: 22
ToPort: 22
```

Permite administração remota.

A recomendação é restringir para:

```text
Meu_IP/32
```

---

## HTTP

```yaml
FromPort: 80
ToPort: 80
```

Permite acesso ao site.

---

# Decisões Técnicas

## Restrição SSH

Acesso administrativo não deve ficar aberto para toda internet.

Boa prática:

```text
203.0.113.10/32
```

---

## HTTP Público

Necessário para disponibilizar aplicações web.

```text
0.0.0.0/0
```

---

# Benefícios

## Segurança

Redução da superfície de ataque.

## Controle

Gerenciamento centralizado.

## Auditoria

Configuração documentada.

## Automação

Provisionamento repetível.

---

# Resultados Obtidos

Ao executar a Stack:

- Security Group criado;
- regras aplicadas automaticamente;
- ambiente preparado para receber workloads.

---

# Aprendizados

Foi possível compreender:

- funcionamento de Security Groups;
- conceito de firewall na AWS;
- boas práticas de segurança;
- automação de controles de acesso.

---

# Próximos Passos

- HTTPS (443)
- Security Group Referencing
- AWS WAF
- Network ACLs
- AWS Firewall Manager

---

# Conclusão

Firewalls são a primeira linha de defesa de qualquer infraestrutura.

Automatizar sua criação através do CloudFormation garante consistência, segurança e governança.
