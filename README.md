# HyDE Legal Retrieval — Dataset (Brazilian Jurisprudence)

A dataset of structured judicial decisions (*ementas*) from the Court of Justice
of Mato Grosso do Sul (TJMS), assembled for research on legal precedent retrieval
in Portuguese.

The corpus supports an **auto-retrieval** task: each query corresponds to exactly
one relevant document. The structured body of each ruling is used as the query,
and the keyword-dense header (legal thesis) is the target document to be retrieved.

---

## Contents

```
├── data/
│   ├── corpus/
│   │   └── structured_documents.json   # 501 structured ementas (corpus)
│   └── queries/
│       ├── queries.json                # full-body queries
│       ├── queries_short.json          # short queries (facts only)
│       ├── queries_medium.json         # medium queries (facts + controversy)
│       └── queries_long.json           # long queries (full structured body)
└── README.md
```

---

## Data Schema

### Corpus — `data/corpus/structured_documents.json`

A list of records, one per legal decision:

| Field | Type | Description |
|-------|------|-------------|
| `numero_processo` | string | Case number in the court system |
| `cdacordao` | string | Unique ruling ID — links each query to its target document |
| `classe` | string | Procedural class of the decision |
| `descricao` | string | Structured body (facts, controversy, reasoning) |
| `ementa` | string | Header (keyword-dense legal thesis) — the retrieval target |
| `word_count` | int | Word count of the structured body |

### Queries — `data/queries/`

Each query file is a list of records with the relevant document ID and the query
text:

| Field | Type | Description |
|-------|------|-------------|
| `cdacordao` | string | ID of the relevant document (its matching header in the corpus) |
| `query` | string | Query text |

The four query files differ in granularity:

- **`queries.json`** — the full structured body of each ruling.
- **`queries_short.json`** — facts only (section *I. CASO EM EXAME*).
- **`queries_medium.json`** — facts + controversy (sections *I* + *II*).
- **`queries_long.json`** — the complete structured body (all sections).

---

## License

This dataset contains only **publicly available legal documents**. Refer to the
TJMS jurisprudence system for the original sources.