# Carnet de bord · J2

Binôme : b09 · Membres : Hugo Lavaud, Mohand-Said · Nos réglages sont dans `atelier/cahier-personnel.json` : ne les recopiez pas ici.

## Mon positionnement (chacun de vous deux)

Pour chaque notion, chacun écrit « à l'aise » ou « à renforcer ». Ce n'est ni évalué ni classé : c'est votre point de départ pour le bilan individuel de fin de module.

| Notion | Membre 1 : Hugo Lavaud | Membre 2 : Mohand-Said |
|---|---|---|
| Structure HTML | à l'aise | à l'aise|
| CSS et responsive |à l'aise |à l'aise |
| JavaScript |à renforcer |à l'aise |
| DOM et événements | à renforcer |à renforcer |
| Git |à l'aise |à l'aise |
| Tests | à l'aise|à l'aise |

Chacun, en une phrase, son objectif personnel pour J2 et J3.

Membre 1 (Hugo Lavaud) : Savoir lire un test rouge et trouver la cause seul.

Membre 2 (Mohand-Said) : Savoir expliquer chaque fonction de Cap Web à l'oral, éditeur fermé

## R1 · Les tests automatisés

Les tests rouges du départ, et ce que vous en avez fait :

| Test rouge | Cause trouvée (une phrase) | Fichier | Message du commit `fix:` |
|---|---|---|---|
| refuse le vide et les espaces seuls | Vide testé avant le `trim()` | brain.js | fix: refuse les messages faits uniquement d'espaces |
| accepte 200 caractères et refuse 201 | Limite en dur à 280 au lieu de `LIMITE` | brain.js | fix: la longueur maximale utilise LIMITE au lieu de 280 |
| ignore la casse et les espaces autour | Pas de `trim()` dans `replyTo` | brain.js | fix: replyTo ignore les espaces autour du message |
| reconnaît les deux mots du cahier personnel… | Même cause | brain.js | (même commit) |
| répond à une phrase inconnue par un repli distinct | Repli = réponse de « aide » | brain.js | fix: une phrase inconnue reçoit une réponse de repli distincte |
| view.js affiche du texte… | `innerHTML` au lieu de `textContent` | view.js | fix: view.js affiche les messages en texte, sans innerHTML |

Avec l'agent : ce qu'il a proposé et que vous avez refusé, et pourquoi.

Rien refusé.

Pour aller plus loin : le nom renommé par votre commit `refactor:`, et pourquoi le nouveau est plus clair.

Non fait.

## R2 · Documenter le projet

Vos trois documents sont dans `atelier` : `README.md`, `SPEC.md` et `AGENTS.md`. Rien à recopier ici.

Pour aller plus loin, avec l'agent, les demandes du formateur :

| Demande | Ce qu'a fait l'agent | Votre décision | Règle d'`AGENTS.md` concernée (ou ajoutée) |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

## R3 · Premiers tests unitaires

| À remplir | Votre réponse |
|---|---|
| Fonction tirée | compterMots |
| Le rouge vu (message exact) | does not provide an export named 'compterMots' |
| Identifiant du commit `test:` | 1e1731f |
| Identifiant du commit `feat:` | 0a65ca6 |
| Casse volontaire : la ligne changée | return mots.length; → return 1; |
| Casse volontaire : le test devenu rouge | C1 : compte les mots séparés par un espace |
| Pour aller plus loin : la deuxième fonction | |

Les critères C1 à C5 de votre fonction, recopiés de la fiche :

- C1 : 'salut' donne 1, 'où est le refuge' donne 4.
- C2 : 'un   deux' donne 2, 'un\tdeux\ntrois' donne 3.
- C3 : '   salut   ' donne 1.
- C4 : '' et les espaces seuls donnent 0.
- C5 : ce qui n'est pas du texte donne 0, sans erreur.

## R4 · La revue de code

| Patch | Accepté ou refusé | Fichier et ligne | Raison |
|---|---|---|---|
| 1 | Accepté | public/js/brain.js | Ajoute « merci » sans rien casser, avec son test |
| 2 | Refusé | tests/contrat/brain.contrat.test.js, l. 69 et 86 | Les espaces sont retirés du contrat pour cacher le `trim()` supprimé dans `normaliser()` |
| 3 | Refusé | public/js/view.js, l. 13 | `createContextualFragment` injecte du HTML : `<b>gras</b>` s'affiche en gras (XSS) |

Pour aller plus loin : le patch que vous avez corrigé, et ce que vous avez changé.

## Fin de journée

Chacun, une phrase : ce que vous savez faire ce soir et que vous ne saviez pas faire ce matin. Relisez votre positionnement : une notion est-elle passée de « à renforcer » à « à l'aise » ?

Je sais lire un test rouge : son nom donne la règle, son message montre l'écart. Et je corrige le code, jamais le test.