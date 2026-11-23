# Modèle de projet : formation Claude Code

Point de départ pour construire une application avec Claude Code, Supabase, Vercel et Resend.

## Démarrer
1. En haut de cette page : « Use this template », puis « Create a new repository ». Nom au choix, « Private ».
2. Dans l'application Claude : onglet Code, environnement Cloud, sélectionner votre nouveau dépôt.
3. Suivre `PROMPTS-INES.md`, étapes 1 à 10, dans l'ordre. Les étapes 0 et 7 se font à la main.

## Ce que contient le modèle
- `.claude/settings.json` : autorisations de Claude sur ce dépôt (il travaille sans demander à chaque commande ; les fichiers `.env` restent interdits en lecture).
- `CLAUDE.md` : les règles du projet, relues par Claude à chaque session.
- `.env.example` : la liste des variables à mettre dans Vercel, sans valeurs.
- `PROMPTS-INES.md` : le déroulé complet, prompts validés, temps et qui fait quoi.
- `docs/` : les trois fichiers à remplir avant de coder (intention, spécification, design), et `docs/exemples/recette/` : les mêmes fichiers remplis, pour modèle.
