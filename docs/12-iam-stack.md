🔐 IAM Stack com AWS CloudFormation

Problema de Negócio

Um dos maiores riscos em ambientes cloud é o excesso de permissões.

Quando usuários recebem privilégios administrativos desnecessários:

- aumentam riscos de vazamento;
- aumentam riscos de invasão;
- aumentam falhas operacionais.

---

Contexto

O AWS IAM controla:

- autenticação;
- autorização;
- permissões;
- políticas de acesso.

Ele é um dos pilares do modelo de segurança AWS.

---

Premissas

Foram consideradas:

- Aplicação do princípio do menor privilégio.
- Segregação de responsabilidades.
- Auditoria de acessos.
- Gestão centralizada.

---

Estratégia da Solução

A stack cria:

- IAM Role
- IAM Policy
- Managed Policies
- Associações entre recursos

---

Arquitetura

IAM Policy
      │
IAM Role
      │
EC2 / Lambda / ECS

---

Template Utilizado

Arquivo:

templates/iam-stack.yaml

Recursos utilizados:

AWS::IAM::Role
AWS::IAM::Policy

---

Decisões Técnicas

Foi utilizada Role em vez de Access Keys.

Motivos:

- mais segurança;
- rotação automática de credenciais;
- aderência às boas práticas AWS.

---

Insights

Muitos incidentes de segurança ocorrem devido a permissões excessivas.

CloudFormation permite padronizar controles de acesso desde o início.

---

Resultados

A solução entrega:

✅ Controle centralizado

✅ Segurança padronizada

✅ Menor risco operacional

✅ Infraestrutura auditável

---

Próximos Passos

- IAM Identity Center
- MFA obrigatório
- Permission Boundaries
- SCPs em AWS Organizations

---

Aprendizados

Segurança em nuvem não começa no firewall.

Ela começa na gestão correta de identidades e permissões.
