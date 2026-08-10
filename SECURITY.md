# Política de Segurança

Este repositório contém o README do meu perfil no GitHub — majoritariamente
conteúdo estático (Markdown/HTML), mas com algumas automações via GitHub
Actions. Práticas de segurança adotadas nas automações:

- **Permissões mínimas**: cada workflow declara explicitamente apenas as
  permissões (`permissions:`) de que precisa.
- **Runners auditados**: todos os jobs usam
  [step-security/harden-runner](https://github.com/step-security/harden-runner)
  para monitorar tráfego de rede inesperado durante a execução.
- **Dependências atualizadas**: o Dependabot mantém as versões das GitHub
  Actions em dia, abrindo PRs automaticamente (`.github/dependabot.yml`).
- **Revisão automática por IA**: todo PR passa por lint de Markdown,
  checagem de links quebrados e revisão automática do Claude Code antes do
  merge.
- **Code owners**: qualquer mudança no repositório exige revisão do
  proprietário (`.github/CODEOWNERS`).

## Reportando uma vulnerabilidade

Se você encontrar um problema de segurança relacionado às automações deste
repositório (por exemplo, exposição de segredos ou um workflow potencialmente
malicioso em um PR), entre em contato em **[juanpmoraes2@gmail.com](mailto:juanpmoraes2@gmail.com)**
em vez de abrir uma issue pública.
