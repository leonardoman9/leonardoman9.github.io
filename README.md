# Leonardo Mannini - Sito Personale

Questo repository contiene il codice sorgente del mio sito personale, costruito con [Hugo](https://gohugo.io/) e il tema [Jughead](https://github.com/ananthb/jughead).

## Struttura del Sito

```
leonardoman9.github.io/
├── content/             # Contenuti del sito
│   ├── _index.md        # Contenuto homepage
│   ├── posts/           # Articoli del blog
│   └── resume.md        # Pagina del CV
├── data/                
│   └── resume.json      # Dati CV in formato JSON Resume
├── layouts/             # Layout personalizzati
│   ├── index.html       # Homepage personalizzata
│   ├── _default/        # Layout default
│   └── partials/        # Componenti riutilizzabili
├── static/              # Asset statici (CSS, immagini, ecc.)
├── hugo.toml            # Configurazione principale
└── .github/workflows/   # Configurazione CI/CD
```

## Guida alla Personalizzazione

### 1. Informazioni Generali del Sito

**File**: `hugo.toml`

```toml
title = "Leonardo Mannini"              # Titolo del sito
copyright = "Leonardo Mannini"          # Copyright (no simbolo © o anno)
baseURL = 'https://leonardoman9.github.io/' # URL base
```

### 2. Profilo e Curriculum

**File**: `data/resume.json`

Questo file JSON contiene tutti i dati personali visualizzati nel sito:

- **Informazioni di base**: Modifica la sezione `basics` per cambiare nome, titolo, email, ecc.
- **Esperienza lavorativa**: Modifica l'array `work` aggiungendo/modificando posizioni lavorative
- **Formazione**: Aggiorna l'array `education` con titoli di studio
- **Competenze**: Modifica l'array `skills` per aggiornare le competenze
- **Progetti**: Gestisci l'array `projects` per aggiungere/rimuovere progetti

**IMPORTANTE**: Le date devono essere nel formato `YYYY-MM-DD` (es. `2025-01-01`).

### 3. Gestione degli Articoli Blog

**Directory**: `content/posts/`

Per creare un nuovo post:

1. Crea un nuovo file Markdown in `content/posts/` (es. `nuovo-post.md`)
2. Aggiungi il frontmatter all'inizio:

```
+++
title = "Titolo del Post"
date = 2025-04-14T12:00:00+01:00
draft = false
tags = ["tag1", "tag2"]
categories = ["categoria"]
# Opzionale:
mermaid = true  # Per includere diagrammi
katex = true    # Per formule matematiche
+++

Contenuto dell'articolo...
```

Per evidenziare un post nella homepage, aggiungi `categories = ["featured"]`.

### 4. Personalizzazione del Layout

#### Menu di Navigazione

**File**: `hugo.toml`

```toml
# Menu principale
[[menu.main]]
name = "Blog"
url = "/posts/"
weight = 1

[[menu.main]]
name = "Resume"
url = "/resume/"
weight = 2

# Aggiungi nuove voci così:
[[menu.main]]
name = "Progetti"
url = "/projects/"
weight = 3
```

#### Stile e CSS

**File**: `static/css/custom.css`
**Collegamento**: `hugo.toml` nella sezione `[params]`

```toml
[params]
customCSS = ["/css/custom.css"]
```

#### Footer

**File**: `layouts/partials/footer.html`

Modifica questo file per personalizzare completamente il footer.

#### Homepage

**File**: `layouts/index.html`

Modifica questo file per cambiare struttura e stile della homepage.

### 5. Immagini e Asset Statici

**Directory**: `static/`

- Immagini: `static/images/`
- File PDF: `static/docs/`
- Altri asset: `static/assets/`

Per aggiungere un'immagine e usarla nel contenuto:

1. Carica l'immagine in `static/images/`
2. Riferiscila con `/images/nome-file.jpg`

## Workflow di Sviluppo e Deployment

### Sviluppo Locale

1. Clona il repository:
   ```
   git clone https://github.com/leonardoman9/leonardoman9.github.io.git
   cd leonardoman9.github.io
   ```

2. Installa Hugo (se non già installato):
   ```
   brew install hugo
   ```

3. Avvia il server di sviluppo:
   ```
   hugo server
   ```

4. Visita `http://localhost:1313/` per visualizzare il sito in locale

### Modifiche e Deployment

Il sito usa **GitHub Actions** per il deployment automatico. Workflow in `.github/workflows/gh-pages.yml`.

Per aggiornare il sito in produzione:

1. Crea/modifica i file necessari localmente
2. Testa le modifiche con `hugo server`
3. Commit delle modifiche:
   ```
   git add .
   git commit -m "Descrizione delle modifiche"
   ```
4. Push su GitHub:
   ```
   git push origin main
   ```
5. GitHub Actions costruirà automaticamente il sito e lo pubblicherà nel branch `gh-pages`
6. Attendi qualche minuto affinché GitHub Pages aggiorni il sito live

### Modifiche Dirette in Produzione

Per piccole modifiche, puoi usare l'interfaccia web di GitHub:

1. Vai su https://github.com/leonardoman9/leonardoman9.github.io
2. Naviga al file da modificare
3. Clicca sull'icona della matita per editare
4. Effettua le modifiche
5. Aggiungi un messaggio di commit e conferma
6. Il workflow di GitHub Actions si attiverà automaticamente

## Risoluzione Problemi

- **Errori di build**: Controlla i log in GitHub Actions
- **Problemi CSS**: Verifica i selettori in `static/css/custom.css`
- **JSON Resume**: Verifica la validità del JSON e il formato delle date

## Riferimenti Utili

- [Documentazione Hugo](https://gohugo.io/documentation/)
- [JSON Resume Schema](https://jsonresume.org/schema/)
- [Tema Jughead](https://github.com/ananthb/jughead)
- [GitHub Pages](https://docs.github.com/en/pages)
