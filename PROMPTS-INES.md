# Les 4 prompts de la méthode

Toujours dans cet ordre. Entre deux étapes : vous relisez le fichier produit, vous corrigez, vous validez. C'est votre rôle de recette, appliqué au projet lui-même.

| Étape | Fichier produit | Qui valide |
|---|---|---|
| 1. Intention | docs/1-INTENTION.md | Inès |
| 2. Spécification | docs/2-SPEC.md | Inès |
| 3. Design | docs/3-DESIGN.md + maquettes | Inès |
| 4. Développement | le code, l'app en ligne, le tableau de tests | Inès, sur son téléphone |

---

## Prompt 1 : l'intention

```
Voici mon intention : <en 3 phrases : quel problème, pour qui, à quoi je verrai
que c'est réussi>.
Avant d'écrire quoi que ce soit, pose-moi au maximum 5 questions, une par une,
avec des choix proposés. Ensuite remplis docs/1-INTENTION.md, pousse-le, et
montre-moi le résultat. Ne code rien.
```

## Prompt 2 : la spécification

```
À partir de docs/1-INTENTION.md validé, remplis docs/2-SPEC.md : écrans, champs
(type, obligatoire, règle), règles métier (statuts, droits, e-mails), données
Supabase et critères d'acceptation numérotés au format « Étant donné / Quand /
Alors ». Liste dans « Questions ouvertes » tout ce que tu as dû supposer.
Pousse le fichier. Ne code rien.
```

## Prompt 3 : le design

```
Lance un sous-agent designer. À partir de docs/2-SPEC.md validé, il remplit
docs/3-DESIGN.md (couleurs, typographie, espacements, composants, états vide /
chargement / erreur / succès, règles mobile 390 px, contraste AA) et crée une
maquette de chaque écran en artefact pour que je la valide sur mon téléphone.
Il tranche les choix de style lui-même et m'explique ses choix en 5 lignes.
Pousse le fichier. Ne code pas l'application.
```

## Prompt 4 : le développement

```
Implémente docs/2-SPEC.md en respectant docs/3-DESIGN.md, un écran à la fois.
Pour chaque écran : code, npm run build, tests automatisés des critères
d'acceptation concernés, push sur main. À la fin, rends-moi un tableau
critère / réussi / échoué avec la cause, et l'URL à ouvrir sur mon téléphone.
Si la spec te semble fausse ou incomplète, arrête-toi et demande-moi au lieu de
la modifier.
```

---

## Pour faire évoluer l'app ensuite
Même chemin en plus court : « Ajoute à docs/2-SPEC.md <la nouveauté> avec ses critères d'acceptation, mets à jour docs/3-DESIGN.md si un nouveau composant est nécessaire, montre-moi, puis implémente après ma validation. »
