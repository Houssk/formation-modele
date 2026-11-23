# Le déroulé, étape par étape

Prompts validés par le passage de référence « Recette » (23/11/2026). **Copiez-les tels quels**, dans l'ordre. Remplacez seulement ce qui est entre `< >`.

Règle d'or : **un prompt, puis vous relisez, puis vous écrivez « validé »** avant le suivant. Les étapes marquées **[Inès]** se font à la main, hors de Claude.

| # | Étape | Qui | Temps | Produit |
|---|---|---|---|---|
| 0 | Créer le dépôt depuis le modèle | Inès | 2 min | votre dépôt |
| 1 | Vérifier l'environnement | Claude | 2 min | tableau OK / KO |
| 2 | Intention | Claude + Inès | 5 min | docs/1-INTENTION.md |
| 3 | Spécification | Claude + Inès | 5 min | docs/2-SPEC.md |
| 4 | Design | Claude + Inès | 10 min | docs/3-DESIGN.md + maquettes |
| 5 | Base de données | Claude | 5 min | projet Supabase |
| 6 | Développement | Claude | 15 min | le code sur main |
| 7 | Mise en ligne et clés | Inès | 5 min | l'URL de l'app |
| 8 | E-mails | Claude | 3 min | alerte vérifiée |
| 9 | Tests | Claude + Inès | 5 min | tableau C1, C2… réussi / échoué |
| 10 | Retour d'expérience | Claude | 2 min | JOURNAL.md |

---

## 0. [Inès] Créer votre dépôt
1. github.com/Houssk/formation-modele, « Use this template », « Create a new repository ».
2. Nom `<nom-du-projet>`, **Private**, « Create repository ».
3. Ouvrir Claude, onglet Code, environnement **Cloud**, choisir ce dépôt.

## 1. Vérifier l'environnement
```
Vérifie, sans rien créer : (1) que tu peux pousser sur ce dépôt (git push --dry-run),
(2) que les connecteurs Supabase, Vercel et Resend répondent avec un appel en lecture
(Supabase : liste des organisations ; Vercel : get_auth_user ; Resend : liste des domaines),
(3) que npm fonctionne. Rends un tableau OK / KO avec le message d'erreur exact en cas de KO.
```
Un KO ? Claude dit quoi cliquer. Ne passez pas à la suite avant que tout soit OK.

## 2. L'intention
```
Voici mon intention : <problème, pour qui, à quoi je verrai que c'est réussi>.
Déjà décidé : <ex. pas de connexion en version 1, téléphone d'abord, app de formation : rester simple>.
Pose-moi au maximum 5 questions fermées, regroupées en une seule fois, avec des
choix proposés. Puis remplis docs/1-INTENTION.md, pousse-le sur main et montre-le
moi. Ne code rien.
```
Relire avec `docs/exemples/recette/1-INTENTION.md` sous les yeux. Corriger si besoin, puis écrire « validé ».

## 3. La spécification
```
À partir de docs/1-INTENTION.md validé, remplis docs/2-SPEC.md : écrans, champs
(type, obligatoire, règle), règles métier (statuts, droits, e-mails), données
Supabase et critères d'acceptation numérotés C1, C2… au format « Étant donné /
Quand / Alors », chacun vérifiable par un test automatique. Respecte le hors
périmètre de l'intention. Liste dans « Questions ouvertes » tout ce que tu as dû
supposer. Pousse le fichier. Ne code rien.
```
C'est votre plan de test : relisez chaque critère comme un cas de recette. Répondez aux questions ouvertes, puis « validé ».

## 4. Le design
```
Lance un sous-agent designer. À partir de docs/2-SPEC.md validé, il crée dans
Claude Design (type « Design », sans design system) un canevas avec chaque écran
en 390 × 844, dans un style sobre <ex. : comme Vercel ou Supabase>. Il remplit
docs/3-DESIGN.md (couleurs avec contrastes MESURÉS par script, typographie,
espacements, composants, états vide / chargement / erreur / succès, règles mobile,
lien du canevas). Il tranche les choix de style et me les explique en 5 lignes.
Pousse le fichier. Ne code pas l'application.
```
Ouvrir le lien du canevas sur votre téléphone. Demander les retouches dans la conversation, puis « validé ».

## 5. La base de données
```
J'autorise explicitement la création du projet Supabase « <nom-du-projet> » dans mon
organisation, région eu-west-3 (plan gratuit, coût 0 $ attendu ; si un coût non nul
s'affiche, arrête-toi). Crée les tables et le bucket privé décrits dans docs/2-SPEC.md,
RLS partout, une migration par fichier dans supabase/migrations, appliquée avec le
connecteur, puis advisors sécurité. Enfin écris et lance un test des règles d'accès
avec la clé publishable : si l'hôte Supabase est bloqué par le réseau de la session,
propose de l'autoriser dans l'environnement.
```
- La phrase « J'autorise explicitement… » est indispensable : sans elle, Claude refuse de créer le projet.
- Si une carte « autoriser un hôte réseau » s'affiche : acceptez-la.

## 6. Le développement
```
Implémente docs/2-SPEC.md en respectant docs/3-DESIGN.md, en Next.js App Router,
TypeScript, sans librairie d'interface. Un écran à la fois : code, npm run build,
tests automatisés des critères concernés, push sur main. Les photos sont compressées
dans le navigateur et déposées directement dans Supabase Storage (jamais via une
route Vercel). Les e-mails partent d'une route serveur. Si la spec te semble fausse
ou incomplète, arrête-toi et demande-moi. À la fin, donne-moi les variables publiques
Supabase à saisir dans Vercel.
```

## 7. [Inès] Mise en ligne et clés (le connecteur Vercel ne peut pas créer le projet)
1. **Resend** : resend.com, API Keys, « Create API Key », droit « Sending access ». Copier la clé (elle ne s'affiche qu'une fois). **Jamais dans le chat.**
2. **Vercel** : vercel.com/new, « Import » sur votre dépôt. S'il n'apparaît pas : « Adjust GitHub App Permissions », ajouter le dépôt.
3. Avant « Deploy », Environment Variables :

| Variable | Valeur | Type |
|---|---|---|
| `NEXT_PUBLIC_SUPABASE_URL` | donnée par Claude à l'étape 6 | Plain |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | donnée par Claude (clé publique) | Plain |
| `ALERTE_EMAIL` | l'adresse de votre compte Resend | Plain |
| `RESEND_API_KEY` | la clé copiée au point 1 | **Sensitive** |

4. « Deploy ». Copier l'URL `https://<nom>.vercel.app`. Ensuite, chaque push sur main redéploie seul.
5. Une variable ajoutée après coup : Deployments, « Redeploy ».

## 8. Les e-mails
```
L'app est déployée sur <URL>. Les variables RESEND_API_KEY et ALERTE_EMAIL sont dans
Vercel. Vérifie que l'alerte e-mail part côté serveur uniquement et que l'enregistrement
se fait même si l'envoi échoue. Si tout est déjà en place, ne change rien et dis-le.
```

## 9. Les tests
```
Exécute les tests automatisés de chaque critère C1, C2… de docs/2-SPEC.md contre <URL>
(Playwright à 390 px pour les écrans, déjà installé : ne lance pas playwright install ;
script Node avec la clé publishable pour les règles d'accès). Rends un tableau
critère / réussi / échoué avec la cause. Puis crée une donnée de test qui déclenche
l'e-mail et vérifie avec le connecteur Resend qu'il est parti (statut, destinataire, heure).
```
Puis à la main, sur votre téléphone : refaire le parcours principal, photo comprise.

## 10. Le retour d'expérience
```
Ajoute à JOURNAL.md le retour d'expérience de cette session : ce qui a été fait et
l'URL, ce qui a coincé (message exact) et comment l'éviter, le prompt amélioré pour
la prochaine fois. Pousse-le.
```

---

## Faire évoluer l'app ensuite
```
Ajoute à docs/2-SPEC.md <la nouveauté> avec ses critères d'acceptation (numéros à la
suite). Mets à jour docs/3-DESIGN.md si un nouveau composant est nécessaire.
Montre-moi les deux fichiers et attends ma validation avant de coder.
```
