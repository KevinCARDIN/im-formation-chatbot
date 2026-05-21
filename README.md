# Module 1 — Bulle chatbot (Railway)

Mini-page hébergeant le widget de chat n8n en mode bulle flottante,
à intégrer en iframe dans les leçons ThriveCart Learn.

## Configuration avant déploiement

1. Ouvrir `index.html`.
2. Remplacer `__N8N_WEBHOOK_URL__` par ta **Production URL** du node *Chat Trigger* n8n
   (elle finit par `/chat`). Le workflow n8n doit être **Actif**.
3. (Optionnel) Personnaliser dans le bloc `i18n.en` :
   - `title`, `subtitle`, `inputPlaceholder`
   - `initialMessages` (liste des bulles d'accueil)

## Déploiement Railway

1. Pousser ce dossier sur un repo GitHub (ou utiliser la Railway CLI).
2. Sur railway.app → **New Project → Deploy from GitHub repo** → choisir le repo.
3. Railway détecte Node, lance `npm start` (le script `serve` est dans `package.json`).
4. Settings → **Networking → Generate Domain** → tu obtiens une URL publique
   du type `https://<nom>.up.railway.app`.

## Configurer le CORS dans n8n

Dans le node **Chat Trigger** → Options → **Allowed Origins (CORS)** :
mettre l'URL Railway exacte (ex: `https://<nom>.up.railway.app`).
⚠️ Pas le domaine ThriveCart : c'est la page Railway qui appelle n8n.

## Intégration dans une leçon ThriveCart

Dans le bloc HTML de la leçon, coller :

```html
<iframe
  src="https://<nom>.up.railway.app/"
  allowtransparency="true"
  style="position:fixed; bottom:0; right:0;
         width:min(420px,100vw); height:min(640px,90vh);
         border:0; background:transparent; z-index:99999;"
  title="Assistant formation">
</iframe>
```

→ Bulle flottante en bas à droite, qui s'ouvre/se ferme normalement.

## Limite connue

L'iframe est une zone fixe ~420×640 en bas à droite : la zone transparente
y intercepte les clics. Vérifier qu'aucun bouton important de ThriveCart
n'est dessous. Réglable en réduisant la taille de l'iframe.
