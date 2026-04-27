# EquiLibre Coaching — Documentation Projet

> Version 1.2 — Avril 2026  
> Développé par : JulienBechkri  
> Client : Coach indépendante (profil RH, Normandie/Paris)

---

## Table des matières

1. [Contexte & Objectifs](#1-contexte--objectifs)
2. [Spécifications fonctionnelles](#2-spécifications-fonctionnelles)
3. [Architecture du projet](#3-architecture-du-projet)
4. [Design System](#4-design-system)
5. [Pages & Contenu](#5-pages--contenu)
6. [SEO](#6-seo)
7. [Déploiement](#7-déploiement)
8. [Mémoire projet — Décisions & contexte](#8-mémoire-projet--décisions--contexte)
9. [Prochaines étapes](#9-prochaines-étapes)

---

## 1. Contexte & Objectifs

### La cliente
- Coach indépendante, ancienne DRH
- 15 ans d'expérience en ressources humaines
- Basée en Normandie (Eure · 27), intervient aussi sur Paris et en visio
- Spécialités : coaching de managers, équicoaching, séminaires d'entreprise

### Ce qui la différencie
- **Background RH terrain** (DRH groupe 800 personnes) → elle parle le langage de l'entreprise
- **Équicoaching** (coaching avec médiation équine) → rareté forte sur le marché
- **Double cible** : entreprises (prioritaire) + particuliers (secondaire)

### Objectifs du site
| Priorité | Objectif |
|----------|----------|
| 1 | Générer des prises de contact (leads) |
| 2 | Référencement Google (SEO local + national) |
| 3 | Image professionnelle, crédible et humaine |
| 4 | Valoriser l'équicoaching comme différenciateur fort |

---

## 2. Spécifications fonctionnelles

### Fonctionnalités présentes

- **Navigation** : menu sticky avec dropdowns, hamburger mobile, maillage interne
- **Formulaire de contact** : HTML natif (à brancher sur un service d'envoi d'e-mail : Formspree, Netlify Forms…)
- **Prise de RDV** : intégration Calendly (placeholder — URL à remplacer)
- **Blog** : statique HTML (3 articles rédigés + page listing)
- **Scroll reveal** : animations d'apparition au scroll (IntersectionObserver)
- **Compteurs animés** : statistiques (15 ans, 200 managers…)
- **FAQ Accordion** : pages coaching et équicoaching
- **Responsive / Mobile first** : breakpoints 480 / 768 / 1024px — géré via `css/style.css` + `css/mobile.css` (overrides des inline styles)

### Fonctionnalités non incluses (à prévoir v2)
- CMS (Netlify CMS, Decap, ou autre) pour gestion des articles de blog
- Newsletter (Mailchimp / Brevo)
- Analytics (Google Analytics 4 ou Plausible)
- Chat / WhatsApp flottant
- Témoignages dynamiques

---

## 3. Architecture du projet

```
equilibre-coaching/
│
├── index.html                  ← Page d'accueil (orientée entreprises)
├── a-propos.html               ← Parcours + certifications + valeurs
├── coaching-managers.html      ← Page SEO prioritaire entreprises
├── coaching-entreprises.html   ← Accompagnement DRH / RH
├── coaching-individuel.html    ← Particuliers (transition, bilan, sens)
├── equicoaching.html           ← Page différenciante signature
├── seminaires.html             ← Séminaires & team building
├── blog.html                   ← Listing des articles
├── blog-article-1.html         ← "Manager en difficulté" (~900 mots)
├── blog-article-2.html         ← "Équicoaching & leadership" (~800 mots)
├── blog-article-3.html         ← "100 premiers jours manager" (~950 mots)
├── contact.html                ← Formulaire + Calendly + carte zones
│
├── css/
│   ├── style.css               ← Design system complet (variables, composants)
│   └── mobile.css              ← Overrides responsive (inline styles, grids, boutons)
│
├── js/
│   └── main.js                 ← Interactions (navbar, FAQ, counters, reveal)
│
├── images/                     ← Dossier vide (photos à ajouter)
│
├── STRATEGIE-SEO.md            ← Plan SEO 3 mois + 40 mots-clés
└── DOCUMENTATION.md            ← Ce fichier (v1.2)
```

### Dépendances externes
| Ressource | Usage | Chargement |
|-----------|-------|------------|
| Google Fonts — Playfair Display + Inter | Typographie | Via `<link>` dans chaque `<head>` |
| Aucune librairie JS | — | Vanilla JS uniquement |
| Aucun framework CSS | — | CSS custom (variables + BEM-like) |

> **Choix volontaire** : zéro dépendance npm, zéro build step. Le site s'ouvre en double-cliquant sur `index.html` ou via n'importe quel serveur statique.

---

## 4. Design System

Défini dans `css/style.css` via variables CSS (`:root`).

### Couleurs
| Variable | Valeur | Usage |
|----------|--------|-------|
| `--color-primary` | `#1D3D2F` | Vert forêt — couleur dominante |
| `--color-primary-light` | `#2A5540` | Hover, dégradés |
| `--color-primary-dark` | `#132B20` | Hero, footer alternatif |
| `--color-secondary` | `#C4914A` | Or chaleureux — accents, CTA |
| `--color-secondary-light` | `#D4A96A` | Hover secondary |
| `--color-accent` | `#7B3F20` | Brun terre — détails |
| `--color-light` | `#FAF7F2` | Fond sections alternées |
| `--color-dark` | `#1A1A1A` | Footer, textes sombres |

### Typographie
| Variable | Police | Usage |
|----------|--------|-------|
| `--font-heading` | Playfair Display | Titres H1–H4 |
| `--font-body` | Inter | Corps de texte, UI |

### Composants CSS disponibles
- `.btn`, `.btn-primary`, `.btn-secondary`, `.btn-white`, `.btn-outline-white`, `.btn-lg`, `.btn-sm`
- `.card`, `.testimonial-card`, `.blog-card`
- `.cta-banner`, `.page-hero`
- `.section-header`, `.section-label`
- `.stats-grid`, `.stat-item`
- `.problem-list`, `.check-list`, `.process-steps`
- `.feature-grid`, `.feature-item`
- `.faq-list`, `.faq-item`
- `.form-group`, `.form-row`
- `.zones-grid`, `.zone-tag`
- `.article-content` (pour les articles de blog)
- `.reveal`, `.reveal-delay-1/2/3/4` (animations)
- `.grid-2`, `.grid-3`, `.grid-4`

---

## 5. Pages & Contenu

### Maillage interne (liens entre pages)
```
index.html
  ├── coaching-managers.html
  ├── coaching-entreprises.html
  ├── equicoaching.html
  ├── seminaires.html
  ├── a-propos.html
  └── contact.html

coaching-managers.html
  ├── coaching-entreprises.html
  ├── equicoaching.html
  └── contact.html

equicoaching.html
  ├── coaching-managers.html
  ├── seminaires.html
  └── contact.html

blog.html
  ├── blog-article-1.html
  ├── blog-article-2.html
  └── blog-article-3.html
```

### Placeholders à remplacer
| Placeholder | Emplacement | Valeur attendue |
|-------------|-------------|-----------------|
| `[Prénom NOM]` | Toutes les pages | Nom réel de la coach |
| `[votre-lien-calendly]` | contact.html | URL Calendly réelle |
| `[votre@email.com]` | contact.html | Email professionnel |
| `[Numéro de téléphone]` | contact.html, footer | Téléphone réel |
| `[Lien LinkedIn]` | footer | URL profil LinkedIn |
| `[SIRET]` | Mentions légales | Numéro SIRET |

---

## 6. SEO

### Structure SEO par page
Chaque page possède :
- `<title>` optimisé (60-70 caractères)
- `<meta name="description">` (150-160 caractères)
- `<link rel="canonical">` (à mettre à jour avec le vrai domaine)
- `<h1>` unique
- `Schema.org` JSON-LD (Person, Service, FAQPage selon les pages)
- Maillage interne vers pages connexes

### Mots-clés prioritaires
| Page | Mot-clé principal |
|------|------------------|
| index.html | coaching entreprise Normandie |
| coaching-managers.html | coaching manager Normandie, coach manager en difficulté |
| equicoaching.html | équicoaching entreprise, coaching avec chevaux leadership |
| coaching-entreprises.html | coach RH entreprise, accompagnement DRH |
| seminaires.html | séminaire coaching entreprise Normandie |

### SEO local ciblé
- Évreux (Eure · 27)
- Normandie
- Région parisienne
- France entière (visio)

> Détail complet dans `STRATEGIE-SEO.md`

---

## 7. Déploiement

### Hébergement actuel
- **Dépôt GitHub** : https://github.com/LaBeck53/equilibre-coaching
- **GitHub Pages** : https://labeck53.github.io/equilibre-coaching/
- **Branche de déploiement** : `main` / root `/`

### Pour mettre à jour le site
```bash
# Dans le dossier du projet
git add .
git commit -m "Description des modifications"
git push origin main
# GitHub Pages se met à jour automatiquement en ~1 minute
```

### Domaine personnalisé (optionnel)
Pour utiliser un domaine type `equilibre-coaching.fr` :
1. Acheter le domaine (OVH, Gandi, Namecheap…)
2. Dans GitHub Pages → Custom domain → entrer le domaine
3. Chez le registrar, créer un enregistrement CNAME : `www` → `labeck53.github.io`
4. Activer "Enforce HTTPS"

---

## 8. Mémoire projet — Décisions & contexte

### Pourquoi ce stack (HTML/CSS/JS pur) ?
- La cliente n'a pas de développeur en interne
- Zéro maintenance technique requise
- Déploiement immédiat sur GitHub Pages (gratuit)
- Performance maximale (pas de JS framework)
- Modifiable facilement par n'importe quel dev ou via un éditeur de code

### Pourquoi GitHub Pages ?
- Demande d'un ami de la cliente qui avait utilisé ce système
- Gratuit, stable, versionné
- URL de démo partageable immédiatement

### Choix de design
- Vert forêt + or → évoque la nature (équicoaching), le premium, la Normandie
- Playfair Display → sérieux, élégance, crédibilité professionnelle
- Inter → lisibilité maximale pour le corps de texte
- Pas de photos pour l'instant (dossier `images/` vide) → à intégrer en v2

### Structure de contenu
- La page d'accueil est orientée **entreprises en priorité** (DRH, dirigeants) conformément à la stratégie de la cliente
- L'équicoaching est traité comme une page à part entière (pas une sous-rubrique) car c'est le principal différenciateur
- Les 3 articles de blog sont rédigés pour le SEO longue traîne + valeur ajoutée

### Périmètre non traité (v1)
- Pas de formulaire fonctionnel (besoin Formspree ou Netlify Forms)
- Pas de vrai Calendly (placeholder)
- Pas de photos réelles
- Pas de mentions légales complètes
- Pas de politique de cookies / RGPD

### Décisions UX notables
- **Panneau hero droit masqué sur mobile** (`display:none`) : le bloc "Ce que vous allez obtenir" est caché sur mobile pour que le CTA reste visible sans scroll. Décision validée par le client (avril 2026). À reconsidérer en v2 si on veut enrichir l'argumentaire mobile.
- **css/mobile.css séparé** : les inline styles du HTML ne peuvent pas être overridés par des media queries classiques sans `!important`. Le fichier `mobile.css` centralise tous ces overrides. Ne pas mettre ces règles dans `style.css` pour garder la lisibilité.

---

## 9. Historique des versions

| Version | Date | Changements |
|---------|------|-------------|
| v1.0 | Avril 2026 | Création initiale — 12 pages, CSS, JS, 3 articles |
| v1.1 | Avril 2026 | Ajout `DOCUMENTATION.md` |
| v1.2 | Avril 2026 | Fix responsive mobile — `css/mobile.css` injecté dans les 12 pages |

---

## 10. Prochaines étapes

### Court terme (avant partage client)
- [ ] Remplacer tous les placeholders `[Prénom NOM]`, email, tél, Calendly
- [ ] Ajouter une vraie photo de la coach dans `a-propos.html`
- [ ] Mettre à jour les URLs canoniques avec le vrai domaine
- [ ] Brancher le formulaire de contact (Formspree gratuit recommandé)

### Moyen terme (v2)
- [ ] Domaine personnalisé (ex: `equilibre-coaching.fr`)
- [ ] Google Analytics 4 ou Plausible
- [ ] Google Search Console + sitemap XML
- [ ] Google Business Profile (Évreux)
- [ ] Ajouter des témoignages clients réels
- [ ] Page mentions légales + politique de confidentialité (RGPD)
- [ ] Optimisation images (WebP, lazy loading)

### Long terme (v3)
- [ ] CMS léger pour que la cliente gère son blog elle-même
- [ ] Newsletter (Brevo recommandé)
- [ ] Chatbot / WhatsApp flottant
- [ ] Traductions (EN) si développement international

---

*Dernière mise à jour : avril 2026 — v1.2*
