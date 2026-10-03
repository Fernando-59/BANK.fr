# NeaBank — déploiement sur Render

## Déploiement
1. Pousse le projet sur GitHub, sans inclure `.venv/`, `neobank.db` ni aucun fichier `.env`.
2. Sur Render, crée un Blueprint à partir du dépôt et applique `render.yaml`.
3. Renseigne `MAIL_USERNAME` et `MAIL_PASSWORD` dans Render avec les identifiants SMTP Gmail. Pour Gmail, utilise un mot de passe d'application.
4. Render génère `SECRET_KEY` et `ADMIN_PASSWORD` et fournit `DATABASE_URL` depuis la base PostgreSQL déclarée dans le Blueprint. `ADMIN_USERNAME` est l'adresse utilisée pour se connecter à `/admin`.

## Configuration Gmail en local
1. Copie `.env.example` dans un fichier `.env` à la racine du projet.
2. Renseigne `MAIL_USERNAME` avec ton adresse Gmail et `MAIL_PASSWORD` avec un mot de passe d'application Google (pas le mot de passe normal de ton compte).
3. Redémarre Flask après avoir modifié `.env`. Ce fichier est ignoré par Git et ne doit jamais être envoyé sur GitHub.

## Admin
- Ouvre `/admin` et utilise l'adresse définie par `ADMIN_USERNAME` ainsi que `ADMIN_PASSWORD` dans Render > Environment. Au démarrage, le mot de passe haché en base est synchronisé depuis cette variable.
- Pour créer ou réinitialiser l'administrateur en local, exécute `.\.venv\Scripts\python.exe -m flask --app app create-admin`. La commande demande l'adresse puis le mot de passe deux fois sans l'afficher. Dans le Shell Render, exécute `flask --app app create-admin`.
- Sur Render, `ADMIN_PASSWORD` est la source de vérité au démarrage. Si tu réinitialises le compte avec la commande CLI, mets aussi `ADMIN_PASSWORD` à la même valeur dans les variables du service, sinon le mot de passe défini dans Render reprendra effet au prochain redémarrage.
