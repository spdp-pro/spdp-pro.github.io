# AGENTS.md — Projet SPDP

Notes pour toute personne (ou assistant IA) qui reprend ce projet. À garder à jour, **en français**.

## En bref

**SPDP** (« Sensibilisation à la Protection des Données Personnelles ») est un projet scolaire :
BUT Informatique, semestre 1, séquence 2 « projet de communication numérique », fait en groupe de 4.

Le sujet : la protection des données personnelles, expliquée à **deux publics** :

| Public | Support | Où |
| --- | --- | --- |
| Non-experts (collégiens, lycéens, étudiants) | Vidéo courte verticale (format TikTok / Reels), 54 s | `video-spdp.mp4` |
| Professionnels (commerçants, artisans, professions libérales, TPE/PME, associations) | Site web explicatif | `index.html` |

La vidéo est aussi **intégrée au site** comme « kit de sensibilisation » que le professionnel peut montrer à ses salariés.

- Site en ligne : https://spdp-pro.github.io
- Vidéo seule : https://spdp-pro.github.io/video-spdp.mp4
- Dépôt GitHub : `spdp-pro/spdp-pro.github.io` (branche `main`)
- Un rapport explicatif accompagne le projet : « Rapport explicatif SPDP » (Google Drive de Solal, en .docx et .pdf).
  Il explique les choix (publics, supports, 10 stratégies de vulgarisation, outils, répartition du travail).

Répartition (d'après le rapport) : Solal a fait le **site** ; un camarade la **vidéo** ; les deux autres le **rapport**.

## Structure des fichiers

```
spdp-pro.github.io/
├── index.html              Tout le site : HTML + CSS (dans <style>) + JavaScript (dans <script>)
├── video-spdp.mp4          La vidéo (9:16, 54 s, ~9,4 Mo)
├── video-spdp-poster.jpg   Image affichée avant le lancement de la vidéo
├── diapo/
│   ├── index.html          Diaporama animé de la présentation orale (16 diapos)
│   └── TEXTE-ORAL.md       Texte à dire, diapo par diapo, réparti entre 4 personnes
├── AGENTS.md               Ce fichier
└── README.md               Présentation du projet
```

Pas de framework, pas de build, pas de `package.json` : **un seul fichier HTML statique**.
Dépendances externes chargées depuis Internet :
- Polices Google Fonts : Archivo, IBM Plex Sans, IBM Plex Mono.
- Icônes **Lucide** 0.460.0 via `unpkg.com` (les balises `<i data-lucide="...">` sont remplacées par des icônes au chargement).

## Contenu du site (`index.html`, dans l'ordre de la page)

1. **En-tête** collant : logo SPDP, menu (Données, Réflexes, Outils, RGPD, Vidéo, CNIL), bouton « Faire l'audit »,
   menu burger sur mobile, barre de progression de lecture.
2. **Accueil (hero)** : « Les données de vos clients sont sous votre responsabilité », publics visés,
   exemple de fiche du **registre des traitements** (article 30).
3. **Chiffres clés** : 72 h (art. 33), 1 mois (art. 12), 20 M€ ou 4 % du CA (art. 83), 2018.
4. **#donnees** : les 4 familles de données (identité, coordonnées, connexion/localisation, sensibles),
   encadrés « Chez vous », règle d'or.
5. **#reflexes** : 4 réflexes (A2F, mots de passe, messages urgents, confidentialité et mises à jour)
   + **exercice phishing** : repérer 3 pièges dans un faux e-mail de facture (clic sur les passages suspects).
6. **#outils** : VPN, antivirus, sauvegardes (règle 3-2-1), version entreprise / au quotidien.
7. **#rgpd** : obligations du RGPD article par article (5, 13, 15-22, 30, 32, 33, 37, 83) avec une frise qui se
   remplit au défilement.
8. **#kit** : la vidéo dans un faux téléphone, 8 chapitres cliquables (temps codés dans `data-t`),
   lecture auto quand elle est visible, son coupé par défaut.
9. **#audit** : audit flash de 9 cases à cocher → score /9, niveau (À renforcer / En bonne voie / Solide /
   Exemplaire), 3 prochaines actions. Les réponses sont gardées dans le navigateur (`localStorage`, clé `spdp-audit`),
   rien n'est envoyé.
10. **#cnil** : liens vers cnil.fr et cybermalveillance.gouv.fr.
11. **Pied de page** : rappel que le guide ne remplace pas un conseil juridique.

Détails techniques utiles :
- Couleurs en variables CSS dans `:root`, avec un **thème sombre automatique** (`prefers-color-scheme`).
- Animations désactivées si l'utilisateur le demande (`prefers-reduced-motion`).
- Mise en page adaptée au mobile (plusieurs `@media`).
- Si on change la vidéo, il faut mettre à jour les temps des chapitres (`data-t`) et la durée de secours
  `53.85` dans le script, ainsi que le texte « 54 s ».

## Le diaporama de la présentation orale (`diapo/`)

- En ligne : https://spdp-pro.github.io/diapo/ — page séparée, la page d'accueil du site n'y renvoie pas.
- 16 diapos pour environ 11 minutes, 4 parties : Hugo (intro), Louison (vidéo), Solal (site), Thomas (adaptation et conclusion). Le texte est dans `diapo/TEXTE-ORAL.md`
  **et** dans les balises `<aside class="notes">` de `diapo/index.html` : si on change l'un, changer l'autre.
- Fonctionnement : une « scène » fixe de 1920 x 1080 mise à l'échelle de l'écran (bandes noires si l'écran n'est pas
  en 16:9). Animations en CSS (classes `up`, `pop`, `left`, `draw`… avec un délai `--d`), lancées quand la diapo
  reçoit la classe `on`. Fond animé dessiné dans un `<canvas>` (réseau de points). Aucune bibliothèque externe.
- Commandes : flèches / Espace / clic = navigation, F = plein écran, N = notes de l'orateur, T = thème clair,
  ? = aide. Le numéro de diapo est dans l'adresse (`#5`).
- La diapo 6 lit `../video-spdp.mp4` (la vidéo du site) : garder le diaporama dans le même dépôt que la vidéo.
- Hors ligne : tout marche, seules les polices Google sont remplacées par celles du système.

## Voir le site

- **En ligne** : ouvrir https://spdp-pro.github.io dans Google Chrome.
- **En local** : ouvrir `index.html` dans Chrome (double-clic). Il faut Internet pour les polices et les icônes.
  Si la vidéo ne se lance pas en local, lancer un petit serveur dans le dossier :
  `python3 -m http.server 8000`, puis aller sur http://localhost:8000.

## Publier (GitHub Pages)

Le site est publié automatiquement par **GitHub Pages** : comme le dépôt s'appelle `spdp-pro.github.io`,
tout ce qui est poussé sur la branche `main` est en ligne quelques minutes après.

```
git pull --rebase
git add .
git commit -m "Ce que j'ai changé"
git push
```

Toujours demander l'accord de l'utilisateur avant de commit / push.

## Historique (git)

- 2026-10-06 : première version du site (`index.html`) envoyée sur GitHub.
- 2026-10-06 : essai d'un nom de domaine (fichier `CNAME` avec `spdp-pro.com` puis `spdp-pro.fr`), puis **supprimé** :
  le site est resté sur l'adresse `spdp-pro.github.io`.
- 2026-10-13 : refonte complète du site pour les professionnels + ajout de la vidéo et de son image.
- 2026-10-14 : rapport explicatif rédigé (hors dépôt, sur Google Drive).
- 2026-11-10 : ajout de `AGENTS.md`, `README.md` et du diaporama animé `diapo/` pour la présentation orale.

## État d'avancement

**Terminé et en ligne** : le site, la vidéo, le rapport. **Prêt** : le diaporama de l'oral (`diapo/`). Le projet correspond à ce que décrit le rapport
(publics, sections, exercice phishing, audit de 9 questions, vidéo intégrée, liens CNIL).

## Points à améliorer (idées, rien d'obligatoire)

- **Icônes dépendantes d'Internet** : si `unpkg.com` ne répond pas, toutes les icônes disparaissent.
  On pourrait copier le fichier Lucide dans le dépôt.
- **Vidéo lourde dans git** (~9,4 Mo) : correct pour GitHub Pages, mais à ne pas remplacer trop souvent
  (chaque version reste dans l'historique). Une version plus compressée chargerait plus vite sur mobile.
- **Sous-titres de la vidéo** : la vidéo a des sous-titres incrustés, mais pas de piste `<track>` pour les
  lecteurs d'écran.
- **Mentions légales / crédits** : pas de page « qui sommes-nous » ni de mention du projet BUT et du groupe ;
  pas de lien vers le rapport.
- **Partage** : pas de balises Open Graph (aperçu quand on partage le lien) ni de favicon.
- **Rapport** : quelques fautes à corriger (« non expert » → « non-experts », « professionels », espaces avant les
  parenthèses et les points).
- Les chiffres et articles du RGPD sont justes à la date d'octobre 2026 ; à revérifier si le projet est repris plus tard.

## Règles pour travailler sur ce projet

- Répondre et écrire **en français**, simplement (l'utilisateur est débutant).
- Ouvrir les pages dans **Google Chrome** (Claude in Chrome), pas dans le navigateur interne.
- Rester dans le dossier `~/DevClaude/spdp-pro.github.io` (un dossier par projet dans `DevClaude`).
- Ce projet n'a **aucun lien** avec le projet e-commerce de l'utilisateur.
