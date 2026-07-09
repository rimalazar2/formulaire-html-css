# formulaire-html-css

Formulaire de contact HTML/CSS statique, déployé sur Vercel, connecté à Google Forms pour la collecte automatique des réponses dans Google Sheets.

**Démo en ligne :** [formulaire-html-css-chi.vercel.app](https://formulaire-html-css-chi.vercel.app)

## Description

Ce projet est un formulaire web permettant de recueillir les informations d'un candidat (Nom, Prénom, Email, Téléphone, Filière, Niveau d'étude, Message). Les données saisies sont envoyées directement vers un Google Form via JavaScript, sans rechargement de page, puis centralisées automatiquement dans une feuille Google Sheets pour traitement.

## Stack technique

- **HTML5** — structure du formulaire
- **CSS3** — mise en page et style
- **JavaScript (Vanilla)** — capture de la soumission et envoi des données
- **Google Forms** — réception des données
- **Google Sheets** — stockage et traitement des réponses
- **Vercel** — hébergement et déploiement continu (CI/CD via GitHub)

## Structure du projet

```
formulaire-html-css/
├── index.html      # Structure du formulaire + script d'envoi
├── style.css        # Mise en page et style
└── README.md         # Ce fichier
```

## Champs du formulaire

| Champ HTML (`name`) | Type | Champ Google Form |
|---|---|---|
| `nom` | texte | Nom |
| `prenom` | texte | Prénom |
| `email` | email | Email |
| `telephone` | tel | Téléphone |
| `filiere` | select | Filière ou domaine |
| `niveau` | select | Niveau d'étude |
| `message` | textarea | Message ou motivation |

## Fonctionnement de l'intégration

1. L'utilisateur remplit le formulaire sur le site.
2. Au clic sur **Envoyer**, le JavaScript intercepte la soumission (`e.preventDefault()`), empêchant le rechargement de page.
3. Les valeurs sont associées aux identifiants `entry.XXXXXX` correspondants du Google Form (récupérés via un lien prérempli).
4. Une requête `fetch()` en mode `no-cors` envoie les données vers l'URL `formResponse` du Google Form.
5. Google Forms enregistre la réponse, qui apparaît instantanément dans le Google Sheet lié.

> **Note technique :** le mode `no-cors` empêche de lire la vraie réponse HTTP (le navigateur affichera parfois un statut trompeur dans les DevTools). La vérification fiable se fait en consultant directement le Google Sheet après soumission.

## Lancer le projet en local

Aucune dépendance requise — il suffit d'ouvrir `index.html` dans un navigateur, ou d'utiliser un serveur local simple :

```bash
# Avec l'extension "Live Server" de VS Code
# ou avec Python :
python -m http.server 8000
```

## Déploiement

Le projet est connecté à Vercel via GitHub. Chaque `git push` sur la branche `main` déclenche automatiquement un nouveau déploiement.

```bash
git add .
git commit -m "Mise à jour du README"
git push origin main
```

## Difficultés rencontrées et solutions

- **Erreur 401 (fetch)** → résolue en vérifiant les paramètres du Google Form (aucune restriction de connexion n'était en réalité active — le souci venait d'un test avec `mode` mal configuré).
- **Confusion entre `entry.XXXXX` et URL du formulaire** → résolue via la génération d'un lien prérempli (`Obtenir le lien prérempli`) pour extraire les vrais identifiants de champs.
- **Cohérence des valeurs `<select>`** → les libellés des `<option>` HTML doivent correspondre exactement à ceux du Google Form pour éviter les incohérences de données.

## Auteur

GARBA.Ridwoine — Étudiant L2 IA & Génie Logiciel, ESCEN Lomé
Stage à l'ESCEN Labo — Jour 4
GitHub : [rimalazar2](https://github.com/rimalazar2)