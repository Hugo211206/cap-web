# Cap Web

## À quoi sert Cap Web

Cap Web est un petit chatbot à règles, dans une page web : on écrit un message, il répond.
Il ne s'agit pas d'une IA : il reconnaît quelques mots (« salut », « aide », « test » et trois mots propres au binôme : « horaires », « tarifs » et « billets ») et donne une réponse de repli pour le reste. Écrivez « conseil » : il demande un conseil au serveur.
Le projet sert à apprendre le HTML, le CSS, le JavaScript, le DOM, les tests automatisés et Git.

## Installer et lancer

Il faut Node 24.20 ou plus, et Git. Dans un terminal PowerShell (si PowerShell refuse `npm`, tapez `npm.cmd`) :

1. Récupérer le projet, puis entrer dans le dossier `atelier` :
   ```powershell
   git clone https://github.com/Hugo211206/cap-web.git
   cd cap-webtelier
   ```
2. Vérifier la version de Node :
   ```powershell
   node --version
   ```
3. Installer les outils (une vulnérabilité est annoncée : ne lancez pas `npm audit fix`) :
   ```powershell
   npm ci
   ```
4. Seulement si `cahier-personnel.json` n'existe pas : le créer, puis l'ouvrir dans l'éditeur pour y mettre votre limite (160 à 400, par pas de 10) et vos deux mots :
   ```powershell
   Copy-Item cahier-personnel.exemple.json cahier-personnel.json
   ```
5. Lancer Cap Web, puis ouvrir http://127.0.0.1:3000 dans le navigateur (Ctrl+C l'arrête) :
   ```powershell
   npm start
   ```
6. Dans un second terminal, lancer les tests (la ligne `fail` doit afficher `fail 0`), puis la vérification du style du code (aucune erreur attendue) :
   ```powershell
   npm test
   npm run lint
   ```

Si le port 3000 est déjà pris (erreur `EADDRINUSE`), tapez `$env:PORT=3001` avant `npm start`, et ouvrez http://127.0.0.1:3001.

## Les 3 modules de `public/js`

- `brain.js` : le cerveau. Il contient la limite, les mots reconnus et les réponses, et exporte des fonctions pures, sans accès à la page : `validateMessage` vérifie un message (texte, non vide, pas trop long), `replyTo` choisit la réponse et `compterMots` compte les mots d'un message.
- `view.js` : l'affichage. `renderMessages` dessine l'historique de la conversation dans la page, en texte seulement (jamais de HTML injecté). Il ne décide d'aucune réponse.
- `app.js` : le câblage. Il écoute le formulaire, appelle `validateMessage` puis `replyTo` (ou `/api/conseil` pour « conseil »), ajoute les messages à l'historique, le sauvegarde dans le navigateur (`localStorage`) et demande l'affichage à `view.js`. Il met aussi à jour le compteur de caractères et affiche la version dans le pied de page.

## Arborescence

```
atelier/
├── public/              la page servie au navigateur
│   ├── index.html       la structure de la page
│   ├── styles.css       la mise en forme, version mobile comprise
│   └── js/
│       ├── brain.js     les règles : validateMessage, replyTo, compterMots
│       ├── view.js      l'affichage de la conversation
│       └── app.js       le câblage : formulaire, compteur, version, conseil
├── server/
│   ├── app.js           le serveur : fichiers publics, /version.json, /api/conseil
│   └── start.js         lance le serveur sur http://127.0.0.1:3000
├── tests/               les tests automatisés (npm test)
│   └── contrat/         le contrat du formateur, à ne jamais modifier
├── scripts/             les outils de contrôle (dépendances, tests, build)
├── README.md            ce fichier
├── SPEC.md              la spécification
└── AGENTS.md            les conventions du projet
```

## La route `/api/conseil`

Le serveur (`server/app.js`) répond à `GET /api/conseil` par un objet JSON avec un conseil tiré au hasard parmi trois, par exemple :

```json
{ "conseil": "Lisez le message d’un test rouge avant de toucher au code." }
```

Pour l'essayer : `npm start`, puis ouvrir http://127.0.0.1:3000/api/conseil. Dans la page, le message « conseil » appelle cette route ; si le serveur ne répond pas, Cap Web affiche « Le serveur ne répond pas : conseil indisponible. ». Le test est dans `tests/conseil.test.js`.
