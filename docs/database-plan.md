# Rascunho de tabelas — Supabase (futuro)

Este documento é só um ponto de partida. A migração para o Supabase só deve acontecer
**depois** que todo o conteúdo do livro (~100 páginas) estiver mapeado em lições e perguntas,
para não precisar remodelar o schema no meio do caminho.

Enquanto isso, o progresso do usuário fica salvo localmente via `window.storage` (armazenamento
nativo do artifact).

## Tabelas previstas

### `lessons`
| coluna | tipo | descrição |
|---|---|---|
| id | text (pk) | ex: `l1`, `l2` |
| title | text | título da lição |
| page_start | int | página inicial do livro |
| page_end | int | página final do livro |
| order_index | int | posição na trilha |

### `questions`
| coluna | tipo | descrição |
|---|---|---|
| id | uuid (pk) | |
| lesson_id | text (fk → lessons.id) | |
| type | text | `fill`, `word`, `match`, `select`, `order`, `timeline_periods`, `timeline_dates` |
| prompt | text | enunciado |
| payload | jsonb | dados específicos do tipo (opções, pares, itens da timeline etc.) |
| order_index | int | posição dentro da lição |

### `users`
| coluna | tipo | descrição |
|---|---|---|
| id | uuid (pk) | vem do Supabase Auth |
| display_name | text | |
| created_at | timestamptz | |

### `user_progress`
| coluna | tipo | descrição |
|---|---|---|
| id | uuid (pk) | |
| user_id | uuid (fk → users.id) | |
| lesson_id | text (fk → lessons.id) | |
| completed | boolean | |
| correct_count | int | |
| xp_earned | int | |
| completed_at | timestamptz | |

### `user_stats`
| coluna | tipo | descrição |
|---|---|---|
| user_id | uuid (pk, fk → users.id) | |
| total_xp | int | |
| current_streak | int | |
| longest_streak | int | |
| hearts | int | |
| updated_at | timestamptz | |

## Notas

- `payload` em `questions` fica em JSONB pra não precisar de uma tabela por tipo de pergunta —
  mais simples de evoluir enquanto o formato ainda está mudando (como já mudou várias vezes
  no protótipo).
- Quando migrarmos, dá pra escrever um script que lê o array `LESSONS` do `index.html` e faz o
  insert automático nas tabelas `lessons` e `questions`.
- RLS (Row Level Security) do Supabase vai precisar garantir que cada usuário só veja/edite o
  próprio `user_progress` e `user_stats`.
