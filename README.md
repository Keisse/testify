# Clio — Trilha de História da Igreja

App estilo Duolingo para revisar o conteúdo do livro *História da Igreja*, página por página.

## Status atual

- `index.html` — protótipo funcional, single-file (HTML/CSS/JS puro, sem build).
- Conteúdo hoje: **páginas 283–291** (3 lições, 10 perguntas cada).
- Progresso salvo via `window.storage` (armazenamento nativo do artifact no Claude).

## Como rodar

Basta abrir `index.html` em qualquer navegador. Não tem dependências externas além da fonte
(Google Fonts, carregada via CDN).

## Formatos de pergunta implementados

- Completar palavra (letras soltas)
- Preencher lacunas (múltipla escolha)
- Ler e selecionar (interpretação de trecho)
- Montar frase em ordem
- Associar colunas (correção só no final, ligações podem ser desfeitas)
- **Timeline** (formato próprio): organizar períodos em ordem cronológica e ligar datas a eventos

## Roadmap

1. ✅ Protótipo com páginas 283–291
2. ⏳ Ir adicionando lições conforme novas páginas do livro forem enviadas (10 perguntas por lição)
3. ⏳ Subir para o GitHub (este repositório)
4. ⏳ Quando o conteúdo completo (~100 páginas) estiver mapeado e as tabelas de dados estiverem
   definidas, migrar o armazenamento de progresso para **Supabase** (ver `docs/database-plan.md`)

## Estrutura

```
.
├── index.html              # app completo (será dividido em módulos se crescer muito)
├── docs/
│   └── database-plan.md    # rascunho do esquema de tabelas para o Supabase (futuro)
└── README.md
```
