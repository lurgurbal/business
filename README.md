# OptiSearcher

Site vitrine SEO en **HTML/CSS/JavaScript pur** (aucun framework) présentant un annuaire et un blog dédiés aux meilleurs outils d'intelligence artificielle gratuits en 2026.

🔗 **Démo en ligne :** [optisearcher.netlify.app](https://optisearcher.netlify.app)

---

## Sommaire

- [Aperçu](#-aperçu)
- [Fonctionnalités](#-fonctionnalités)
- [Structure du projet](#-structure-du-projet)
- [Pages du site](#-pages-du-site)
- [Stack technique](#-stack-technique)
- [Installation et déploiement](#-installation-et-déploiement)
- [SEO & Search Console](#-seo--search-console)
- [Personnalisation](#-personnalisation)
- [Licence](#-licence)

---

## Aperçu

OptiSearcher est une **Single Page Application (SPA)** construite sans framework : toute la navigation (accueil, blog, articles, plan du site, guide GSC, à propos, contact) est gérée en JavaScript vanilla via un système d'affichage/masquage de sections (`showPage()`), sans rechargement de page.

Le site contient :
- Une sélection éditoriale de **6 outils IA** (ChatGPT, Claude, Gemini, Perplexity, Canva IA, Microsoft Designer)
- **30 articles de blog** générés dynamiquement à partir d'un tableau de données JavaScript (`ARTICLES`)
- Un système de **filtres par catégorie** et de **pagination**
- Un **plan du site** listant tous les articles regroupés par catégorie
- Un **guide complet Google Search Console** pour l'indexation SEO
- Des emplacements publicitaires **Google AdSense** intégrés

##  Fonctionnalités

| Fonctionnalité | Description |
|---|---|
| Navigation SPA | Changement de page sans rechargement (`showPage(id)`) |
| Responsive | Menu hamburger mobile, grilles adaptatives |
| Filtrage | Filtres par catégorie sur la page blog |
| Pagination | 9 articles par page dans le blog |
| Plan du site | Vue d'ensemble des 30 articles par catégorie |
| Rendu dynamique | Cartes d'articles et d'outils générées via template literals JS |
| Checklist interactive | Checklist SEO à cocher sur la page Search Console |
| SEO on-page | Meta tags, Open Graph, données structurées Schema.org (`WebSite`) |
| Monétisation | Emplacements Google AdSense (bannières + sidebar) |

## Structure du projet

```
optisearcher/
├── index.html          # Fichier unique contenant tout le site
│   ├── <style>          # CSS avec variables custom (thème bleu/cyan)
│   ├── <body>            # Sections de pages (home, blog, sitemap, gsc, article, about, contact)
│   └── <script>          # Données (TOOLS, ARTICLES) + logique de rendu et navigation
└── README.md
```

> Le site est actuellement construit comme un **fichier HTML monolithique**. Voir la section [Personnalisation](#-personnalisation) pour des pistes de refactorisation en fichiers séparés (`styles.css`, `data.js`, `app.js`).

## Pages du site

| Page | ID | Contenu |
|---|---|---|
| Accueil | `page-home` | Hero, présentation de l'IA, outils vedettes, 12 derniers articles, CTA newsletter |
| Blog | `page-blog` | Liste complète des 30 articles avec filtres et pagination |
| Article | `page-article` | Contenu détaillé d'un article (12 templates dédiés + template générique) |
| Plan du site | `page-sitemap` | Tous les articles regroupés par catégorie |
| Search Console | `page-gsc` | Guide pas-à-pas pour indexer le site sur Google (vérification, sitemap XML, checklist) |
| À propos | `page-about` | Présentation de la mission du site |
| Contact | `page-contact` | Formulaire de contact (front-end uniquement, pas de backend connecté) |

### Catégories d'articles disponibles
Comparatif · Étudiants · Images IA · Rédaction · Travail · Guide · Productivité · Design · Carrière · Traduction · Développement · Vidéo · Créatif · Marketing · Santé · Éducation

## Stack technique

- **HTML5** sémantique
- **CSS3** — variables custom (`:root`), Flexbox/Grid, animations (`@keyframes`)
- **JavaScript vanilla (ES6+)** — aucune dépendance, aucun build step
- **Polices** — [Syne](https://fonts.google.com/specimen/Syne) (titres) & [DM Sans](https://fonts.google.com/specimen/DM+Sans) (texte) via Google Fonts
- **Google AdSense** — script asynchrone de monétisation
- **Schema.org** — balisage `WebSite` avec `SearchAction` pour le SEO

## Installation et déploiement

Aucune compilation n'est nécessaire — le site est un fichier HTML autonome.

### En local
```bash
git clone https://github.com/<ton-utilisateur>/optisearcher.git
cd optisearcher
# Ouvre simplement index.html dans ton navigateur,
# ou lance un serveur local :
python3 -m http.server 8000
```
Puis rends-toi sur `http://localhost:8000`.

### Déploiement (Netlify / Vercel / GitHub Pages)
Le site étant statique, il se déploie en un clic :
- **Netlify** : glisser-déposer le dossier, ou connecter le repo GitHub (build command : *aucune*, publish directory : `/`)
- **GitHub Pages** : Settings → Pages → Deploy from branch → `main` / `root`
- **Vercel** : import du repo, framework preset "Other"

## SEO & Search Console

Le site inclut sa propre page pédagogique `/gsc` expliquant comment :
1. Créer un compte Google Search Console
2. Vérifier la propriété du site (balise HTML)
3. Générer et soumettre un `sitemap.xml`
4. Demander l'indexation manuelle des articles
5. Suivre les métriques clés (clics, impressions, CTR, position moyenne)

> ⚠️ Le site étant en HTML pur, un fichier `sitemap.xml` doit être créé et maintenu manuellement (un exemple de structure est fourni dans le code de la page GSC).

## Personnalisation

Pour adapter le site à tes besoins :

- **Outils affichés** → modifie le tableau `TOOLS` dans le `<script>`
- **Articles de blog** → modifie le tableau `ARTICLES` (id, catégorie, titre, extrait, date, mots-clés)
- **Contenu détaillé d'un article** → ajoute une fonction `monArticleContent()` et référence-la dans l'objet `templates` de `generateArticleContent()`
- **Couleurs / thème** → modifie les variables CSS dans `:root` (`--b5`, `--ac`, etc.)
- **Emplacements publicitaires** → remplace `ca-pub-XXXXXXXXXX` par ton propre ID AdSense

## À faire / améliorations possibles

- [ ] Séparer HTML / CSS / JS en fichiers distincts pour la maintenabilité
- [ ] Générer automatiquement le `sitemap.xml` à partir du tableau `ARTICLES`
- [ ] Ajouter un vrai backend/API pour le formulaire de contact
- [ ] Créer des URLs propres par article (actuellement navigation en JS pur, sans routage réel)
- [ ] Ajouter des tests d'accessibilité (a11y)

## Licence

Ce projet est distribué sous licence de ton choix (MIT recommandée pour un projet open source). Ajoute un fichier `LICENSE` à la racine du repo si nécessaire.

---

*README généré pour le projet OptiSearcher — Le guide des meilleurs outils IA gratuits en 2026.*
