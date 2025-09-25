# Jira — Task para Training Sessions

Use este conteúdo para criar a task no card "Training Sessions" (subtarefa ou issue relacionada, conforme fluxo).

## Summary

Training Sessions: Criação do material — Gemini + Cursor

## Description (texto simples)

Objetivo: preparar material de treinamento sobre Gemini (recursos avançados) e Cursor (prática guiada), com slides alinhados à identidade visual do Nubank.

Entregáveis:
- Slide deck Reveal.js em `/Users/rayssa.fernandes/Workspace/training-gemini-cursor-slides/index.html`
- Tema visual `nu-theme.css`
- README de uso

Critérios de aceitação:
- Slides cobrem agenda (Introdução, Gemini, Cursor, Encerramento)
- Inclui passo a passo para solicitar acesso ao Cursor
- Contém exemplos de prompts avançados do Gemini
- Design consistente com cores do Nubank

## Campos sugeridos

- Issue Type: Task
- Assignee: Rayssa Fernandes (ou responsável)
- Labels: `training`, `gemini`, `cursor`, `ai`
- Due date: [data do treinamento]
- Epic Link / Parent: card "Training Sessions"

## cURL (Atlassian Cloud API v3)

Substitua variáveis antes de executar.

```bash
export JIRA_BASE_URL="https://suaorg.atlassian.net"
export JIRA_EMAIL="seu.email@empresa.com"
export JIRA_API_TOKEN="xxxxxxxxxxxxxxxx"
export PROJECT_KEY="TRNG"              # projeto do board de Training Sessions
export TRAINING_CARD_KEY="TRNG-123"    # key do card "Training Sessions" (se for parent/link)

# 1) Criar a Task
curl -s -u "$JIRA_EMAIL:$JIRA_API_TOKEN" \
  -H 'Content-Type: application/json' \
  -X POST "$JIRA_BASE_URL/rest/api/3/issue" \
  -d "$(jq -n --arg project "$PROJECT_KEY" \
              --arg summary 'Training Sessions: Criação do material — Gemini + Cursor' \
              --arg desc 'Objetivo: preparar material de treinamento sobre Gemini (recursos avançados) e Cursor (prática guiada), com slides alinhados à identidade visual do Nubank.\n\nEntregáveis:\n- Slide deck Reveal.js em /Users/rayssa.fernandes/Workspace/training-gemini-cursor-slides/index.html\n- Tema visual nu-theme.css\n- README de uso\n\nCritérios de aceitação:\n- Slides cobrem agenda (Introdução, Gemini, Cursor, Encerramento)\n- Inclui passo a passo para solicitar acesso ao Cursor\n- Contém exemplos de prompts avançados do Gemini\n- Design consistente com cores do Nubank' \
              '{fields:{project:{key:$project},summary:$summary,issuetype:{name:"Task"},description:$desc}}')"

# 2) (Opcional) Vincular à issue "Training Sessions" existente
#   - Altere RELATION para o tipo disponível (ex.: "Relates", "Blocks")
export NEW_TASK_KEY="TRNG-XXX" # substitua pela key retornada no passo anterior
curl -s -u "$JIRA_EMAIL:$JIRA_API_TOKEN" \
  -H 'Content-Type: application/json' \
  -X POST "$JIRA_BASE_URL/rest/api/3/issueLink" \
  -d "{\n    \"type\": { \"name\": \"Relates\" },\n    \"inwardIssue\": { \"key\": \"$TRAINING_CARD_KEY\" },\n    \"outwardIssue\": { \"key\": \"$NEW_TASK_KEY\" }\n  }"
```

Notas:
- Se sua instância usar Epic Link como campo customizado, adicione esse campo ao payload da criação.
- Caso sua política exija descrição em ADF (Atlassian Document Format), troque `description` string por objeto ADF.
