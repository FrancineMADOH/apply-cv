# apply-cv — Job Application Assistant for Claude Code

**One command. Your CVs in. A complete application dossier out.**

`/apply` reads your CV files, analyses the job offer, decides GO / NO-GO, selects and adapts the best CV, writes the application email, and updates your tracking file — automatically.

---

## Installation

In any Claude Code session, run:

```
/plugin marketplace add FrancineMADOH/apply-cv
```

That's it. The `/apply` command is now available in your project.

---

## Setup

1. Create a folder for your job search (e.g. `job-search-2026/`)
2. Drop your CV file(s) inside — any format works: `.md`, `.pdf`, `.docx`, `.txt`
3. You can have multiple CV variants (e.g. one for BA roles, one for PM roles) — the plugin picks the best one for each offer automatically

```
job-search-2026/
├── CV_Jane_Doe_BusinessAnalyst.pdf
├── CV_Jane_Doe_ProjectManager.docx
└── offre.txt          ← paste the job offer here
```

---

## Usage

1. Paste the job offer into a file (e.g. `offre.txt`) in your job search folder
2. Run:

```
/apply offre.txt
```

The plugin will:

| Step | What happens |
|---|---|
| 0 | Reads all your CVs and extracts your profile |
| 1 | Reads and summarises the job offer |
| 2 | Decides **GO**, **GO WITH RESERVATIONS**, or **NO-GO** |
| 3 | Creates a `candidatures/YYYY-MM-DD_company_role/` folder |
| 3 | Selects the best CV and adapts it to the offer → `CV_YourName_Company.md` |
| 3 | Writes an offer analysis → `analyse_offre.md` |
| 3 | Writes a ready-to-send email → `email_candidature.md` |
| 4 | Updates (or creates) `candidatures/tracking.md` |
| 5 | Displays a final summary |

**If NO-GO:** only the decision and reason are shown. No folder is created.

---

## Output structure

After running `/apply offre.txt`, your folder looks like this:

```
job-search-2026/
├── CV_Jane_Doe_BusinessAnalyst.pdf
├── CV_Jane_Doe_ProjectManager.docx
├── offre.txt
└── candidatures/
    ├── tracking.md
    └── 2026-05-16_acme_business-analyst/
        ├── offre.txt
        ├── CV_Jane_Doe_Acme.md        ← adapted CV (export to PDF/Word as you like)
        ├── analyse_offre.md           ← detailed alignment analysis
        └── email_candidature.md       ← ready-to-send email
```

The adapted CV is always generated as `.md`. Open it in any Markdown editor, copy it into your CV tool (Canva, Word, etc.), and export to PDF.

---

## Tips

- **Multiple CVs = better results.** The more variants you provide, the more precisely the plugin can match your profile to each offer.
- **Works in French and English.** The plugin detects the offer language and generates all documents in that language.
- **Tracking file.** `candidatures/tracking.md` is created automatically on first use. Update the `Status` column as your applications progress (`A_ENVOYER` → `ENVOYE` → `ENTRETIEN` → `REFUSE` / `OFFRE`).

---

## Example

See the [`example/`](./example/) folder for a sample CV and a sample offer file.

---

## License

MIT — free to use, fork, and adapt.

---
---

# apply-cv — Assistant de candidature pour Claude Code

**Une commande. Vos CVs en entrée. Un dossier de candidature complet en sortie.**

`/apply` lit vos fichiers CV, analyse l'offre d'emploi, décide GO / NO-GO, sélectionne et adapte le meilleur CV, rédige l'email de candidature, et met à jour votre fichier de suivi — automatiquement.

---

## Installation

Dans n'importe quelle session Claude Code, exécutez :

```
/plugin marketplace add FrancineMADOH/apply-cv
```

C'est tout. La commande `/apply` est maintenant disponible dans votre projet.

---

## Configuration

1. Créez un dossier pour votre recherche d'emploi (ex. `recherche-emploi-2026/`)
2. Déposez-y votre ou vos CVs — tous les formats sont acceptés : `.md`, `.pdf`, `.docx`, `.txt`
3. Vous pouvez avoir plusieurs variantes de CV (ex. un pour les postes BA, un pour les postes Chef de Projet) — le plugin choisit automatiquement le plus adapté à chaque offre

```
recherche-emploi-2026/
├── CV_Prenom_Nom_BusinessAnalyst.pdf
├── CV_Prenom_Nom_ChefDeProjet.docx
└── offre.txt          ← collez l'offre d'emploi ici
```

---

## Utilisation

1. Copiez l'offre d'emploi dans un fichier (ex. `offre.txt`) dans votre dossier de recherche
2. Lancez :

```
/apply offre.txt
```

Le plugin va :

| Étape | Ce qui se passe |
|---|---|
| 0 | Lit tous vos CVs et extrait votre profil |
| 1 | Lit et résume l'offre d'emploi |
| 2 | Décide **GO**, **GO AVEC RÉSERVES** ou **NO-GO** |
| 3 | Crée un dossier `candidatures/AAAA-MM-JJ_entreprise_poste/` |
| 3 | Sélectionne le meilleur CV et l'adapte à l'offre → `CV_Prenom_Nom_Entreprise.md` |
| 3 | Rédige une analyse de l'offre → `analyse_offre.md` |
| 3 | Rédige un email prêt à envoyer → `email_candidature.md` |
| 4 | Met à jour (ou crée) `candidatures/tracking.md` |
| 5 | Affiche un récapitulatif final |

**En cas de NO-GO :** seule la décision et la raison sont affichées. Aucun dossier n'est créé.

---

## Structure générée

Après `/apply offre.txt`, votre dossier ressemble à ceci :

```
recherche-emploi-2026/
├── CV_Prenom_Nom_BusinessAnalyst.pdf
├── CV_Prenom_Nom_ChefDeProjet.docx
├── offre.txt
└── candidatures/
    ├── tracking.md
    └── 2026-05-16_acme_business-analyst/
        ├── offre.txt
        ├── CV_Prenom_Nom_Acme.md        ← CV adapté (à exporter en PDF/Word)
        ├── analyse_offre.md             ← analyse détaillée de l'alignement
        └── email_candidature.md         ← email prêt à envoyer
```

Le CV adapté est toujours généré en `.md`. Ouvrez-le dans un éditeur Markdown, copiez-le dans votre outil de mise en page (Canva, Word...) et exportez en PDF.

---

## Conseils

- **Plusieurs CVs = meilleurs résultats.** Plus vous fournissez de variantes, plus le plugin peut cibler précisément chaque offre.
- **Fonctionne en français et en anglais.** Le plugin détecte la langue de l'offre et génère tous les documents dans cette langue.
- **Fichier de suivi.** `candidatures/tracking.md` est créé automatiquement à la première utilisation. Mettez à jour la colonne `Status` au fil de vos candidatures (`A_ENVOYER` → `ENVOYE` → `ENTRETIEN` → `REFUSE` / `OFFRE`).

---

## Exemple

Consultez le dossier [`example/`](./example/) pour un CV exemple et une offre exemple.

---

## Licence

MIT — libre d'utilisation, de fork et d'adaptation.
