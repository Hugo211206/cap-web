# Bilan individuel · Hugo Lavaud

## Niveau de départ

| Notion | Mardi |
|---|---|
| Structure HTML | à l'aise |
| CSS et responsive | à l'aise |
| JavaScript | à renforcer |
| DOM et événements | à renforcer |
| Git | à l'aise |
| Tests | à l'aise |

## Deux acquis, chacun prouvé par un commit

1. **Lire un test rouge et corriger le code, jamais le test.** Le nom du test donne la règle, son message montre l'écart. Preuve : `f601b91` (fix: replyTo ignore les espaces autour du message), un seul `trim()` manquant qui faisait rougir deux tests du contrat.
2. **Afficher le texte de l'utilisateur sans injecter de HTML (DOM).** `textContent` et `append` au lieu d'`innerHTML` : `<b>gras</b>` s'affiche tel quel. Preuve : `0512ea3` (fix: view.js affiche les messages en texte, sans innerHTML).

## Deux points à renforcer

1. **Git au quotidien** : faire des commits d'un seul fichier avec `git add -- fichier` plutôt que tout embarquer, et comprendre un push refusé (historiques différents, `--force`). Mardi, un commit a emporté des fichiers qui n'avaient rien à y faire.
2. **JavaScript asynchrone** : écrire seul une fonction `async` avec `await`, `try` et `catch`, comme `demanderConseil` (`2258ab0`), et savoir expliquer pourquoi une réponse 404 ne déclenche pas le `catch` sans `reponse.ok`.

## Objectif

Savoir expliquer chaque fonction de Cap Web à l'oral, éditeur fermé, et écrire seul une nouvelle fonctionnalité avec son test d'abord (rouge, puis vert).
