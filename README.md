# Leonardo Mannini - Sito Personale

Questo repository contiene il codice sorgente del mio sito personale, costruito con [Hugo](https://gohugo.io/) e il tema [Jughead](https://github.com/ananthb/jughead).

## Struttura del Sito

```
leonardoman9.github.io/
├── content/
│   ├── _index.md        # Homepage (il contenuto arriva da data/resume.json)
│   └── projects/        # Una pagina per progetto (slug = nome file)
├── data/
│   └── resume.json      # Dati CV in formato JSON Resume
├── layouts/             # Override del tema (homepage, header, footer, CV, progetti)
├── static/              # CSS custom, immagini dei progetti, CNAME
├── hugo.toml            # Configurazione principale
└── .github/workflows/   # Build e deploy su GitHub Pages
```

`public/` e `resources/` sono generati dalla build e non vanno committati.

## Guida alla Personalizzazione

### 1. Informazioni Generali del Sito

**File**: `hugo.toml`

```toml
baseURL = 'https://www.leonardomannini.com/' # Deve coincidere con static/CNAME
title = 'Leonardo Mannini'
copyright = 'Leonardo Mannini'
```

Le chiavi top-level vanno messe **prima** di qualsiasi sezione `[...]`, altrimenti TOML le assegna a quella sezione.

### 2. Profilo e Curriculum

**File**: `data/resume.json`

Questo file JSON contiene tutti i dati personali visualizzati nel sito:

- **Informazioni di base**: Modifica la sezione `basics` per cambiare nome, titolo, email, ecc.
- **Esperienza lavorativa**: Modifica l'array `work` aggiungendo/modificando posizioni lavorative
- **Formazione**: Aggiorna l'array `education` con titoli di studio
- **Competenze**: Modifica l'array `skills` per aggiornare le competenze
- **Progetti**: Gestisci l'array `projects` per aggiungere/rimuovere progetti

**IMPORTANTE**: Le date devono essere nel formato `YYYY-MM-DD` (es. `2025-01-01`).

- **Foto profilo**: metti l'immagine in `static/images/` e imposta `basics.image` (es. `"/images/profile.jpg"`).
- **Nuovo progetto**: aggiungilo all'array `projects` con uno `slug` e crea `content/projects/<slug>.md` con solo il `title`.

### 3. Personalizzazione del Layout

#### Menu di Navigazione

**File**: `hugo.toml`

```toml
[[menu.main]]
name = 'Projects'
url = '/projects/'
weight = 1
```

Per riattivare un blog: crea i post in `content/posts/`, aggiungi una voce `Blog` al menu e togli `disableKinds` se vuoi le pagine dei tag.

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

### 4. Immagini e Asset Statici

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

2. Installa Hugo **extended** (stessa versione della CI, vedi `.github/workflows/gh-pages.yml`) e Go, necessario per scaricare il tema come Hugo module:
   ```
   brew install hugo go
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
