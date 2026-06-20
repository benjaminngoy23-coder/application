# Déploiement FundFlow sur Dokploy

Ce dépôt est volontairement configuré pour **Dockerfile**, pas pour Nixpacks.

## 1. Déposer sur GitHub

Place directement à la racine du dépôt :

- `app.py`
- `Dockerfile`
- `.dockerignore`
- `.gitignore`
- `.env.example`

Ne place pas le ZIP lui-même dans le dépôt GitHub.

## 2. Réglages Dokploy

Dans l'application Dokploy :

- **Build Type** : `Dockerfile`
- **Dockerfile Path** : `Dockerfile`
- **Docker Context Path** : `.`
- **Docker Build Stage** : laisser vide
- **Publish Directory** : laisser vide

Variables d'environnement :

```env
PORT=8000
DATA_DIR=/app/data
```

## 3. Stockage persistant

Ajoute un volume persistant :

- **Mount path dans le conteneur** : `/app/data`

Sans ce volume, les comptes et les demandes peuvent être perdus lors d'un redéploiement.

## 4. Domaine

Dans Domains :

- **Container Port / Port interne** : `8000`
- Active HTTPS après que le DNS pointe correctement vers le serveur Dokploy.

## 5. Vérification

La route de contrôle est :

```text
/health
```

Elle doit répondre avec `ok: true`.

## Important

Ne sélectionne pas `Nixpacks`. Si Dokploy affiche encore `NIXPACKS BUILD FAILED`, le Build Type est resté sur Nixpacks : remplace-le par **Dockerfile**, enregistre, puis relance un nouveau déploiement sans cache.
