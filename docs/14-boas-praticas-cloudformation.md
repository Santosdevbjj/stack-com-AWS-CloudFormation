🚀 Boas Práticas com AWS CloudFormation

Problema de Negócio

Muitas empresas iniciam sua jornada em nuvem criando recursos manualmente.

Com o crescimento do ambiente surgem problemas como:

- inconsistência entre ambientes;
- dificuldade de auditoria;
- configurações não documentadas;
- erros humanos;
- aumento do custo operacional.

O desafio é criar uma infraestrutura previsível, segura e facilmente reproduzível.

---

Contexto

O AWS CloudFormation é uma ferramenta de Infraestrutura como Código (IaC).

Ele permite definir recursos da AWS utilizando arquivos YAML ou JSON.

Porém, utilizar CloudFormation sem seguir boas práticas pode gerar:

- templates difíceis de manter;
- dependências complexas;
- falhas de segurança;
- baixa reutilização.

---

Premissas

As recomendações deste documento consideram:

- Ambientes corporativos.
- Projetos versionados no GitHub.
- Múltiplos desenvolvedores trabalhando simultaneamente.
- Necessidade de auditoria e governança.
- Escalabilidade da solução.

---

Estratégia da Solução

A adoção das boas práticas está baseada em cinco pilares:

1. Padronização
2. Segurança
3. Modularização
4. Observabilidade
5. Governança

---

1. Utilize Parâmetros

Evite valores fixos dentro dos templates.

❌ Ruim

InstanceType: t2.micro

✅ Melhor

InstanceType: !Ref InstanceType

Benefícios:

- reutilização;
- flexibilidade;
- menor manutenção.

---

2. Utilize Outputs

Exponha informações relevantes após o deploy.

Exemplo:

Outputs:
  WebsiteURL:
    Value: !Sub "http://${WebServer.PublicDnsName}"

Benefícios:

- integração entre stacks;
- facilidade operacional.

---

3. Modularize Templates

Evite templates gigantes.

Prefira:

network-stack.yaml
firewall-stack.yaml
storage-stack.yaml
iam-stack.yaml
webserver-stack.yaml

Benefícios:

- manutenção simplificada;
- reutilização;
- organização.

---

4. Utilize Nested Stacks

Quando o projeto crescer:

Root Stack
├── Network
├── Security
├── Storage
├── Compute
└── Monitoring

Benefícios:

- escalabilidade;
- separação de responsabilidades.

---

5. Evite Hardcoding

Nunca fixe:

- IDs de AMI;
- VPC IDs;
- Subnet IDs;
- nomes de buckets.

Prefira parâmetros e referências.

---

6. Aplique o Princípio do Menor Privilégio

IAM deve conceder apenas o necessário.

❌ AdministratorAccess

✅ Políticas específicas

Benefícios:

- redução de riscos;
- conformidade;
- auditoria.

---

7. Utilize Tags

Todas as stacks devem possuir tags.

Exemplo:

Tags:
  - Key: Environment
    Value: Production

Benefícios:

- governança;
- controle financeiro;
- rastreabilidade.

---

8. Habilite Monitoramento

Integre:

- CloudWatch
- SNS
- Logs
- Alarmes

Infraestrutura sem monitoramento é infraestrutura cega.

---

9. Documente Tudo

Um template sem documentação gera dependência de conhecimento tácito.

Todo template deve possuir:

- objetivo;
- parâmetros;
- outputs;
- exemplos de uso.

---

10. Versione no GitHub

Infraestrutura é código.

Portanto deve seguir:

- Pull Requests;
- Revisões;
- Histórico de mudanças;
- Controle de versões.

---

Insights

Empresas maduras não criam infraestrutura.

Elas criam processos repetíveis para criar infraestrutura.

CloudFormation permite transformar conhecimento operacional em ativos reutilizáveis.

---

Resultados

Ao seguir essas práticas é possível:

✅ Reduzir falhas humanas

✅ Melhorar segurança

✅ Aumentar produtividade

✅ Facilitar auditorias

✅ Escalar ambientes com confiança

---

Próximos Passos

- CI/CD com CloudFormation
- CloudFormation StackSets
- AWS Organizations
- AWS Config
- CloudFormation Drift Detection

---

Aprendizados

Infraestrutura como Código não é apenas automação.

É uma disciplina de engenharia que transforma ambientes complexos em sistemas previsíveis, auditáveis e escaláveis.
