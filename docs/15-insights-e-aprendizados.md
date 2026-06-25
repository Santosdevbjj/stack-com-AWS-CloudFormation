## 🎓 Insights e Aprendizados do Projeto

## Problema de Negócio

Empresas precisam implantar infraestrutura rapidamente sem comprometer:

- segurança;
- confiabilidade;
- governança;
- escalabilidade.

Historicamente, ambientes criados manualmente apresentam:

- inconsistências;
- falhas de configuração;
- dependência de pessoas específicas;
- dificuldades de auditoria.

---

## Contexto

Durante este laboratório foi utilizada a abordagem de Infraestrutura como Código (IaC) através do AWS CloudFormation.

O objetivo não foi apenas criar recursos AWS.

O objetivo foi compreender como organizações modernas automatizam ambientes de produção.

---

## Premissas

Foram considerados:

- Ambientes reproduzíveis.
- Boas práticas AWS.
- Versionamento em GitHub.
- Arquiteturas corporativas.
- Reutilização de componentes.

---

## Estratégia Aplicada

O projeto foi estruturado em múltiplas stacks:

```

Network
Firewall
Storage
IAM
WebServer
Monitoring
SNS
Load Balancer
Auto Scaling
Database
Nested Stack

```


Cada stack possui uma responsabilidade específica.

---

## Principais Insights

### 1. CloudFormation é Engenharia de Infraestrutura

Antes deste projeto:

Infraestrutura parecia apenas configuração.

Depois deste projeto:

Infraestrutura passou a ser tratada como software.

---

## 2. Automação reduz erros

Configurações manuais são suscetíveis a falhas.

Templates versionados garantem:

- consistência;
- repetibilidade;
- previsibilidade.

---

## 3. Segurança deve nascer no template

Não é algo adicionado depois.

Boas práticas devem estar incorporadas desde a criação:

- IAM
- Security Groups
- Monitoramento
- Criptografia

---

## 4. Modularização é essencial

Projetos pequenos podem utilizar um único template.

Projetos corporativos exigem:

- separação de responsabilidades;
- Nested Stacks;
- componentes reutilizáveis.

---

## 5. CloudFormation aproxima Infraestrutura e Desenvolvimento

Conceitos típicos de software passam a fazer parte da infraestrutura:

- versionamento;
- revisão de código;
- documentação;
- testes.

---

## Resultados Obtidos

Ao final do projeto foi possível:

✅ Compreender os fundamentos do CloudFormation

✅ Criar stacks completas

✅ Automatizar recursos AWS

✅ Aplicar conceitos de IaC

✅ Estruturar templates reutilizáveis

✅ Seguir boas práticas de segurança

✅ Documentar tecnicamente a solução

---

## Visão de Mercado

As habilidades praticadas neste projeto são amplamente utilizadas por:

- Cloud Engineers
- DevOps Engineers
- Platform Engineers
- Site Reliability Engineers (SRE)
- Cloud Architects

Empresas que utilizam AWS em larga escala dependem fortemente de automação de infraestrutura.

---

## O Que Eu Faria em uma Próxima Versão

- Integração com CI/CD
- Testes automatizados de templates
- Multi-Region Deployment
- Multi-Account Deployment
- CloudFormation StackSets
- Integração com AWS Config
- Integração com Security Hub

---

## Conclusão

Este projeto demonstrou que CloudFormation vai muito além da criação de recursos.

Ele representa uma mudança de mentalidade.

Em vez de configurar servidores manualmente, passamos a definir infraestrutura como código, permitindo que ambientes inteiros sejam criados, modificados e auditados de forma segura e reproduzível.

Essa abordagem reduz riscos operacionais, melhora a governança e aproxima a infraestrutura das melhores práticas de engenharia de software.

---

## Aprendizado Final

O mercado não valoriza quem apenas conhece serviços da AWS.

O mercado valoriza profissionais capazes de transformar tecnologia em soluções reproduzíveis, seguras e alinhadas aos objetivos do negócio.

Esse é o verdadeiro propósito da Infraestrutura como Código.
