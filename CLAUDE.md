# CLAUDE.md : règles du projet

Ce fichier est relu par Claude au début de chaque session. Modifiez-le librement : c'est le règlement de votre projet.

## Qui je suis
- Je m'appelle Inès. Je viens du test logiciel (recette, plans de test), pas du développement.
- Réponds en français, phrases courtes, sans jargon. Un terme technique inévitable = une ligne d'explication.
- Quand une action manuelle est nécessaire : étapes numérotées, clic par clic, avec le lien direct.
- Si ma demande est ambiguë, pose-moi une question au lieu de deviner.

## Ce qu'on construit
<!-- À compléter au début du projet : le nom de l'app, à quoi elle sert, pour qui. -->
- Application : [NOM]
- Objectif : [EN UNE PHRASE]
- Utilisateurs : [QUI]

## Outils
- Code : Next.js (App Router, TypeScript), CSS simple, pas de librairie d'interface.
- Données et fichiers : Supabase (connecteur Supabase), région eu-west-3 (Paris).
- Mise en ligne : Vercel (connecteur Vercel). Chaque push sur main redéploie l'app.
- E-mails : Resend, toujours envoyés côté serveur (route API), jamais depuis le navigateur.

## Règles fixes
- **Aucune clé secrète** dans le code, dans le dépôt ou dans le chat. Les clés vont dans Vercel > Settings > Environment Variables, saisies par moi. Dans le dépôt : `.env.example` uniquement.
- **Connecteur Vercel : ne jamais passer `teamId` ni `slug`** (compte Hobby : provoque un refus 403). Si Vercel répond `repo_not_found`, dis-moi d'autoriser le dépôt dans l'app GitHub Vercel.
- **Base de données** : toute modification = un nouveau fichier `supabase/migrations/NNNN_nom.sql`, appliqué avec le connecteur, puis vérification des « advisors » sécurité. RLS activée sur chaque table, buckets privés.
- **Avant toute action irréversible** (supprimer une table, un projet, des données) : explique ce qui va se passer et attends mon accord.
- **Après chaque modification** : `npm run build`, corrige jusqu'à ce que ça passe, puis commit et push sur main.
- **Mobile d'abord** : écran de 390 px, texte lisible, boutons d'au moins 48 px, libellés visibles au-dessus des champs.

## Comment on teste
- J'écris le plan de test (cas, attendu) avant de demander le code.
- Tu automatises ce plan (Playwright pour les écrans, SQL pour les règles d'accès), tu l'exécutes et tu rends un tableau réussi / échoué avec la cause.
- Toujours tester : un cas normal, un champ vide, un fichier trop lourd, une personne non autorisée, l'affichage sur téléphone.

## Fin de chaque session
Ajoute un retour d'expérience court dans `JOURNAL.md` et pousse-le :
- ce qui a été fait, et l'URL à vérifier sur mon téléphone ;
- ce qui a coincé (message exact) et comment l'éviter ;
- le prompt amélioré à utiliser la prochaine fois.
