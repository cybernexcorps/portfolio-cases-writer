# Portfolio Cases Writer

n8n workflow + prompts for generating DDVB portfolio cases for ddvb.ru.

## Structure

- `prompts/` — AI prompt files (fetched by n8n from GitHub raw URLs)
  - `perplexity-research.md` — Perplexity research system prompt
  - `case-writer.md` — Claude Sonnet case generation prompt
  - `humanizer.md` — GPT-4o humanization prompt
- `workflow/` — n8n workflow JSON

## Output Format

5-block site case (1,500-2,000 chars):
1. **Заголовок** — max 7-8 words, starts with action verb
2. **Ситуация** — market context + client background
3. **Задача** — bulleted list of agency tasks
4. **Решение** — work stages with logical transitions
5. **Творческая группа** — team composition from fixed role hierarchy

## Integration

Triggered via webhook from [ddvb-marketing-app](../ddvb-marketing-app/) `/cases-writer` module.

Webhook: `POST /portfolio-case/generate`
Callback: `POST /api/webhooks/n8n-callback` with `workflowType: 'portfolio_case'`
