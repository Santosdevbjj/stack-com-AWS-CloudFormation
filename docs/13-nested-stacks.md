## 🏗️ Nested Stacks com AWS CloudFormation

## Problema de Negócio

À medida que ambientes crescem, templates únicos tornam-se difíceis de manter.

## Problemas comuns:

- arquivos gigantes;
- duplicação de código;
- baixa reutilização;
- manutenção complexa.

---

## Contexto

Grandes organizações dividem infraestrutura em módulos.

## Exemplos:

- Rede
- Segurança
- Banco de Dados
- Monitoramento
- Aplicação

CloudFormation oferece Nested Stacks para resolver esse problema.

---

## Premissas

## Foram consideradas:

- Modularização da infraestrutura.
- Reutilização de componentes.
- Facilidade de manutenção.
- Escalabilidade do projeto.

---

## Estratégia da Solução

Uma stack principal orquestra stacks menores.

---

## Arquitetura

``` 

Root Stack
│
├── Network Stack
├── Firewall Stack
├── IAM Stack
├── Storage Stack
├── Monitoring Stack
└── WebServer Stack

```


---

## Template Utilizado

## Arquivo:

```

templates/nested-stack.yaml

```


## Recurso principal:


```

AWS::CloudFormation::Stack

```

---

## Vantagens

### Reutilização

Mesmo template pode ser usado em vários projetos.

### Manutenção

Alterações ficam isoladas.

### Escalabilidade

Projetos crescem sem gerar arquivos gigantes.

## Governança

Maior controle sobre componentes.

---

### Exemplo Real

### Uma empresa pode possuir:

Network Team
→ network-stack.yaml

Security Team
→ firewall-stack.yaml

Cloud Team
→ nested-stack.yaml

Cada equipe mantém sua própria stack.

---

## Insights

Nested Stacks representam uma prática comum em ambientes corporativos maduros.

São amplamente utilizadas em arquiteturas enterprise e ambientes de larga escala.

---

## Resultados

A solução entrega:

✅ Modularização

✅ Reutilização

✅ Governança

✅ Escalabilidade

✅ Manutenção simplificada

---

## Próximos Passos

- StackSets
- Multi-Account Deployments
- Multi-Region Deployments
- CI/CD com CloudFormation

---

## Aprendizados

Infraestrutura como código não é apenas automação.

É engenharia de software aplicada à infraestrutura.

Nested Stacks aproximam CloudFormation das melhores práticas utilizadas em ambientes corporativos de grande escala.
