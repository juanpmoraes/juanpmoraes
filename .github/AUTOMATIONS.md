# 🤖 Automações deste repositório

Resumo do que já está configurado em `.github/` e o que falta habilitar
manualmente (o token usado pela automação não tem permissão de admin sobre
configurações do repositório/organização).

## O que já está pronto

| Automação | Arquivo | O que faz |
|---|---|---|
| CI (lint + links) | `workflows/ci.yml` | Roda em todo push/PR: lint de Markdown, checagem de links quebrados e lint dos próprios workflows (`actionlint`) |
| Dependabot | `dependabot.yml` | Abre PRs automaticamente toda semana atualizando versões de GitHub Actions |
| Auto-merge Dependabot | `workflows/auto-merge-dependabot.yml` | Aprova e faz merge automático de PRs do Dependabot (patch/minor) assim que a CI passar |
| Revisão de PR por IA | `workflows/claude-pr-review.yml` | Claude analisa cada PR (bugs, segurança, links quebrados, clareza) e comenta |
| Assistente por menção | `workflows/claude-assistant.yml` | Comente `@claude` em qualquer issue/PR para pedir ajustes ou explicações |
| Atividade recente automática | `workflows/refresh-activity.yml` | Toda semana, abre um PR atualizando a seção "Atividade recente" do README |
| Code owners | `CODEOWNERS` | Exige revisão do dono em qualquer mudança |
| Política de segurança | `../SECURITY.md` | Como reportar problemas de segurança nas automações |

## Passos manuais necessários (uma vez só)

1. **Segredo do Claude** — em `Settings → Secrets and variables → Actions →
   New repository secret`, crie `ANTHROPIC_API_KEY` com uma chave da API da
   Anthropic. Sem isso, `claude-pr-review.yml` e `claude-assistant.yml` não
   funcionam.
2. **Auto-merge** — em `Settings → General → Pull Requests`, marque
   *"Allow auto-merge"*. Necessário para `auto-merge-dependabot.yml`.
3. **Proteção da branch `main`** — em `Settings → Branches → Add branch
   protection rule` para `main`:
   - "Require a pull request before merging"
   - "Require status checks to pass before merging" → selecione os checks
     `Markdown Lint`, `Check Links` e `Lint Workflows` (aparecem após a
     primeira execução da CI)
   - "Require review from Code Owners"
4. **Code security and analysis** — em `Settings → Code security and
   analysis`, confirme que *Dependabot alerts*, *Dependabot security
   updates* e *Secret scanning* (com *push protection*) estão habilitados.

Sem os passos 1–2, os workflows correspondentes ficam inofensivos (apenas
não fazem nada / falham de forma visível), então não há risco em mergear
este PR antes de configurá-los.
