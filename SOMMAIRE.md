# Sommaire — Introduction à R
**M1 Économie Appliquée & RNET — Université de La Réunion**
Marius LAHY — 2025-2026

---

## Partie I — Fondamentaux de R

### Séance 1 — Découverte et prise en main de R
`seances/01-decouverte.qmd`

- Pourquoi R ? Comparaison R vs Excel
- Installation : R (moteur) puis RStudio (interface)
- Interface RStudio : 4 panneaux, raccourcis clavier essentiels
- Projets RStudio — règle absolue : ne jamais utiliser `setwd()`
- Calcul et affectation : l'opérateur `<-`
- **Vecteurs** : création, indexation, vectorisation, fonctions statistiques
- **Types de données** : numérique, texte, logique, facteur — conversions
- **Matrices** : vecteurs en grille (même type)
- **Data frames** : tableaux à colonnes hétérogènes — exploration, accès
- **Listes** : conteneur universel (types mixtes)
- Récapitulatif des structures de données (diagramme)
- Valeurs manquantes (`NA`) — pièges fréquents
- Fonctions : arguments, aide (`?`), bonnes pratiques
- Bonnes pratiques : nommage, commentaires, structure d'un script

---

### Séance 2 — Introduction au tidyverse
`seances/02-tidyverse.qmd`

- Philosophie tidyverse — données « tidy » (une ligne = une observation)
- Format large vs format long — pourquoi le long est préférable
- **Le pipe `%>%`** — enchaîner des opérations (`x %>% f()` = `f(x)`)
  - Raccourci clavier : `Ctrl + Shift + M`
  - Le pipe natif `|>` (R ≥ 4.1) — comparaison et différences
- **`readr`** — importer des fichiers CSV (`read_csv()`, tibble, `glimpse()`)
- **Les 6 verbes `dplyr`** :
  - `filter()` — sélectionner des lignes
  - `select()` — choisir des colonnes
  - `mutate()` — créer/modifier des colonnes (`case_when()`)
  - `arrange()` — trier
  - `summarise()` — résumer
  - `group_by()` + `summarise()` — résumer par groupe
- **Jointures** : `left_join()`, `inner_join()`, `anti_join()`
- **`tidyr`** — restructuration :
  - `pivot_longer()` — large → long
  - `pivot_wider()` — long → large
  - `separate()` — séparer une colonne
- Exercice : analyse complète du jeu de données `gapminder`

---

## Partie II — Tidyverse avancé & Visualisation

### Séance 4 — Approfondissement du tidyverse
`seances/04-approfondissement.qmd`

| Package | Thème |
|---------|-------|
| `stringr` | Manipulation de chaînes de caractères |
| `forcats` | Variables catégorielles (facteurs) |
| `lubridate` | Dates et heures |
| `purrr` | Programmation fonctionnelle |

- **`stringr`** : `str_detect()`, `str_replace()`, `str_extract()`, `str_glue()`, regex
- **`forcats`** : `fct_reorder()`, `fct_infreq()`, `fct_recode()`, `fct_collapse()`, `fct_lump_n()`
- **`lubridate`** : `ymd()`, `dmy()`, composantes (`year()`, `month()`, `wday()`), arithmétique sur dates
- **`purrr`** : famille `map()` (`map_dbl()`, `map_chr()`, `map_dfr()`), `map2()`, `safely()`, `possibly()`
- Exercice : pipeline complet stringr → forcats → lubridate → purrr sur `gapminder`

---

### Séance 5 — Visualisation avec ggplot2
`seances/05-ggplot2.qmd`

- Pourquoi ggplot2 ? Comparaison avec `plot()` de base R
- **Grammaire graphique** : données + esthétiques + géométries + échelles + thèmes
- `aes()` — encoder des variables (x, y, color, fill, size, shape, alpha)
- **Construction progressive** d'un graphique (5 étapes commentées)
- **Géométries principales** :
  - `geom_point()` — nuage de points
  - `geom_line()` — séries temporelles
  - `geom_col()` / `geom_bar()` — barres
  - `geom_histogram()` — distribution continue
  - `geom_boxplot()` — boîte à moustaches
  - `geom_density()` — courbe de densité
- **Personnalisation** : `scale_*()`, `theme_*()`, `labs()`
- **Facettes** : `facet_wrap()`, `facet_grid()`
- **Export** : `ggsave()` — formats PNG, PDF, SVG
- Exercice : série de visualisations sur `gapminder` et `palmerpenguins`

---

## Partie III — Communication & Productivité

### Séance 7 — Rmarkdown et Quarto
`seances/07-rmarkdown.qmd`

- Pourquoi les documents reproductibles ? Problèmes du copier-coller Word
- Rmarkdown (`.Rmd`) vs Quarto (`.qmd`) — recommandation : Quarto
- **En-tête YAML** : titre, auteur, date, format, `toc`, `execute`
- **Syntaxe Markdown** : titres, gras/italique, listes, liens, images, tableaux, équations LaTeX
- **Chunks R** : options `echo`, `eval`, `fig-width`, `cache`, `label`
- Code inline : `` `r expr` ``
- **Callouts** Quarto : `.callout-note`, `.callout-tip`, `.callout-warning`, `.callout-caution`
- Tableaux : `knitr::kable()`, package `gt`
- **Compiler** : bouton Render, `quarto::quarto_render()`, export PDF avec TinyTeX
- Structure recommandée d'un rapport d'analyse
- Exercice : rapport HTML sur le développement économique en Afrique

---

### Séance 8 — Productivité avec l'IA dans R
`seances/08-ia-r.qmd`

- **Assistants IA** : GitHub Copilot (intégré RStudio), ChatGPT, Claude, Gemini, Perplexity
- Ce que l'IA fait bien / mal — hallucinations, données de formation périmées
- **Rédiger un bon prompt** : contexte + tâche + contraintes + exemple
- **Débogage avec l'IA** : fournir le code + le message d'erreur + le résultat attendu
- **IA locale avec Ollama** (données confidentielles, sans internet) :
  - Installer Ollama + `ollama pull qwen2.5:0.5b`
  - Package R `ollamar` — `chat()` avec messages système
  - Application : nettoyage d'adresses réunionnaises (`adresses_messy.csv`)
  - `rowwise() %>% mutate(chat(...))` — traitement ligne par ligne
  - Export CSV → géocodage sur [adresse.data.gouv.fr](https://adresse.data.gouv.fr/tools/batch-geocodage)
- Limites : hallucinations, confidentialité, dépendance excessive
- **Workflow recommandé** : documentation → essai personnel → StackOverflow → IA
- Exercice : débogage guidé + prompt engineering

---

## Travaux Pratiques

### TP 1 — Manipulation de données agricoles tropicales
`seances/03-tp1.qmd` | Données : `data/agriculture_tropicale.csv`

15 pays × 5 cultures (canne, vanille, café, girofle, noix de coco) × 2000-2022

| Partie | Thème | Compétences |
|--------|-------|-------------|
| 1 | Exploration initiale | `glimpse()`, `summary()`, `count()` |
| 2 | Nettoyage & transformation | `is.na()`, `mutate()`, `case_when()` |
| 3 | Filtrage & sélection | `filter()`, `select()`, opérateurs logiques |
| 4 | Agrégation | `group_by()`, `summarise()`, `arrange()` |
| 5 | Restructuration | `pivot_longer()`, `pivot_wider()` |
| 6 | Défi final | Pipeline complet, `write_csv()` |

---

### TP 2 — Visualisation — Données biodiversité & économiques
`seances/06-tp2.qmd` | Données : `data/biodiversite_mascareignes.csv` + `gapminder` + `palmerpenguins`

| Partie | Thème | Type de graphique |
|--------|-------|-----------------|
| 1 | Choisir le bon graphique | Réflexion guidée |
| 2 | Développement mondial | Heatmap temporelle, Dumbbell chart |
| 3 | Visualisations écologiques | Morphologie manchots, biodiversité Mascareignes |
| 4 | Mini-projet individuel | Thème libre (économie OI ou biodiversité tropicale) |

---

## Données du cours

| Fichier | Description | Lignes |
|---------|-------------|--------|
| `data/agriculture_tropicale.csv` | Productions agricoles tropicales (FAOSTAT-style) | 1 633 |
| `data/biodiversite_mascareignes.csv` | Espèces UICN par île et groupe taxonomique | 177 |
| `data/adresses_messy.csv` | Adresses réunionnaises non normalisées (TP Ollama) | 101 |

Packages R utilisés (intégrés, aucune installation supplémentaire nécessaire) :
`gapminder`, `palmerpenguins`, `broom`, `skimr`, `knitr`, `gt`, `leaflet`, `ollamar`

---

## Ressources

- Site du cours : branche `claude/r-course-quarto-site-fC6dz` → GitHub Pages / Posit Connect
- Repo GitHub : [github.com/joellahy/cours-R](https://github.com/joellahy/cours-R)
- Cheatsheets : [rstudio.github.io/cheatsheets](https://rstudio.github.io/cheatsheets/)
- R for Data Science (2e) : [r4ds.hadley.nz](https://r4ds.hadley.nz)
- Guide R (Larmarange, FR) : [larmarange.github.io/guide-R](https://larmarange.github.io/guide-R/)
- utilitR (INSEE, FR) : [book.utilitr.org](https://book.utilitr.org)
- Géocodage BAN : [adresse.data.gouv.fr/tools/batch-geocodage](https://adresse.data.gouv.fr/tools/batch-geocodage)

---

*Dernière mise à jour : septembre 2026*
