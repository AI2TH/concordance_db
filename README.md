# AI2TH Concordance & Interlinear Database Suite

Standardized, pre-indexed high-performance SQLite databases for biblical concordances, Strong's Greek/Hebrew lexicons, Treasury of Scripture Knowledge (TSK) cross-references, and interlinear original language texts.

All databases are pre-indexed for sub-millisecond lookups and optimized for mobile devices and servers alike.

## Database Catalog

| File | Records | Size | Description |
| :--- | :---: | :---: | :--- |
| **`strongs_dictionary.db`** | 14,298 entries | ~4.1 MB | Complete Hebrew (H1–H8674) & Greek (G1–G5624) Lexicon with lemmas, transliterations, pronunciations, definitions, and morphological glosses. |
| **`cross_references.db`** | 240,618 links | ~16.6 MB | Treasury of Scripture Knowledge (TSK) canonical cross-references connecting Old and New Testaments. Pre-indexed on source and target coordinates. |
| **`concordance_index.db`** | 65,083 words | ~1.5 MB | Multilingual concordance vocabulary index with frequency counts across English, Hebrew, Greek, Spanish, Tamil, Hindi, and more. |
| **`interlinear_greek_nt.db`** | 187,517 words | ~16.4 MB | Complete New Testament original Greek text (Books 40–66: Matthew to Revelation) with Strong's numbers, transliterations, and morphological glosses. |
| **`interlinear_hebrew_ot_law_history.db`** | 381,998 words | ~31.4 MB | Old Testament Hebrew Law and History (Books 1–17: Genesis to Esther) with Strong's numbers, transliterations, and glosses. |
| **`interlinear_hebrew_ot_poetry_prophets.db`** | 270,632 words | ~22.2 MB | Old Testament Hebrew Poetry and Prophets (Books 18–39: Job to Malachi) with Strong's numbers, transliterations, and glosses. |
| **`interlinear_septuagint_apocrypha.db`** | 148,711 words | ~10.9 MB | Septuagint Deuterocanonical Greek books (Books 67–88: Tobit, Judith, Wisdom, Sirach, Maccabees, etc.) with Strong's numbers and glosses. |
| **`concordance_verses_ot_law_history.db`** | 13,498 verses | ~68.8 MB | OT Law & History multilingual parallel verse text (EN, ES, FR, TA, HI, TE, ML, KN, EL, PT, IT, RU, DE) and 1536-dim semantic embeddings. |
| **`concordance_verses_ot_poetry_prophets.db`** | 9,647 verses | ~46.7 MB | OT Poetry & Prophets multilingual parallel verse text and 1536-dim semantic embeddings. |
| **`concordance_verses_nt.db`** | 7,957 verses | ~37.6 MB | NT multilingual parallel verse text and 1536-dim semantic embeddings. |

## Direct Download Endpoints

### 1. GitHub Raw (Global)
- `https://raw.githubusercontent.com/AI2TH/concordance_db/main/{database_name}.db`

### 2. jsDelivr Global Edge CDN
- `https://cdn.jsdelivr.net/gh/AI2TH/concordance_db@main/{database_name}.db`

## Instant SQLite ATTACH Usage

### Strong's Concordance Query
```sql
ATTACH DATABASE 'strongs_dictionary.db' AS strongs;
SELECT strongs_number, lemma, transliteration, definition 
FROM strongs.strongs_dictionary 
WHERE strongs_number = 'H7225';
DETACH DATABASE strongs;
```

### Interlinear Greek NT Lookup
```sql
ATTACH DATABASE 'interlinear_greek_nt.db' AS nt;
SELECT word_position, original_text, transliteration, strongs_number, gloss 
FROM nt.original_words 
WHERE book_number = 43 AND chapter = 1 AND verse_number = 1 
ORDER BY word_position;
DETACH DATABASE nt;
```

### Cross-References Lookup (John 3:16)
```sql
ATTACH DATABASE 'cross_references.db' AS tsk;
SELECT target_book, target_chapter, target_verse_start, target_verse_end, votes 
FROM tsk.cross_references 
WHERE source_book = 43 AND source_chapter = 3 AND source_verse_start = 16 
ORDER BY votes DESC;
DETACH DATABASE tsk;
```
