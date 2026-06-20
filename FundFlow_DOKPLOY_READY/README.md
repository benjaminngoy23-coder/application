# FundFlow — version Dokploy

Application web autonome en Python 3.12 avec base SQLite persistante.

## Démarrage local

```bash
python app.py
```

## Déploiement

Suivre `DEPLOIEMENT_DOKPLOY.md` et utiliser impérativement le Build Type **Dockerfile**.

## Données

En production, monter un volume persistant sur `/app/data`.
