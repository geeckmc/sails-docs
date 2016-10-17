# Ressources

### Aperçu

Les ressources designent l'ensemble des fichiers  [statiques] (https://fr.wikipedia.org/wiki/Page_web_statique) (js, css, images, etc) sur votre serveur que vous voulez rendre accesible a vos visiteurs.Dans le framework sails ces fichiers se trouvent dans le repertoire `assets/` a la racine du projet. Une fois lancer vous pouvez ajouter des fichiers au repertoire assets ou en modifié ceux qui y sont. Pour des raisons de performance sails déplace au chargement ces fichiers vers le repertoire caché (`.tmp/public/`).

> Cette étape intermédiaire (déplacement des fichiers depuis`assets/` vers `.tmp/public/`) permet à Sails de pré-processer les ressources pour une utilisation côté client pour des choses commes LESS, CoffeeScript, SASS, spritesheets, Jade templates, etc.

Le contenu de ce dossier `.tmp/public` est la raisons pour laquelle Sails sert actuellement d'envirronement d'exécution.  Cela est légerment équivalent au dossier "public" dans [express](https://github.com/expressjs), ou au repertoire `www/` du serveur Apache.


### intergiciel(middleware) Statique

De façon transparente Sails utilise les mediateur [static middleware](http://www.senchalabs.org/connect/static.html) de Express pour servir vos ressources. Vous pouvez configurer cet intergiciel (e.g. le cache) dans le fichier [`/config/http.js`](http://sailsjs.org/documentation/reference/sails.config/sails.config.http.html).

##### `index.html`
Sails bien entendu honore la convention web`index.html`.  Par example, si vous crée une ressources html `assets/foo.html` dans votre projet, Il sera accessible à`http://localhost:1337/foo.html`.  Mais si vous le creer dans le sous repertoire `foo` comme suit `assets/foo/index.html`, il sera disponible aux adresses`http://localhost:1337/foo/index.html` et `http://localhost:1337/foo`.

##### Priorité
Il est important de noté que l'intergiciel [middleware](http://stephensugden.com/middleware_guide/) est installé **après** le routeur de Sails.  Donc si vous definisser vos [chemin](routes) personnalisés (http://sailsjs.org/documentation/concepts/Routes?q=custom-routes), mais que vous avez aussi vos ressources dans le repertoire `assets` avec un conflits de chemin, la route défini plutôt sera priorisé. Par example, si vou crée un fichier `assets/index.html`, sans définir de route pour celui-ci dans le fichier [`config/routes.js`](http://sailsjs.org/documentation/reference/sails.config/sails.config.routes.html) , Il servira de page d'acceuil pour votre application. Mais a partir du moments ou vous définissez une route personnalisé comme ceci: `'/': 'FooController.bar'`, celle ci deviendra prioritaire.



<docmeta name="displayName" value="Assets">
