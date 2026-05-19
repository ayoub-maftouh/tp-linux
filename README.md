Voici un guide étape par étape pour réaliser ce TP sur l'installation et la manipulation de MongoDB, ainsi que la création d'une API avec Node.js :

### **Étape 1 : Installation et Démarrage de MongoDB via Docker**

* 
**Vérification de Docker** : Assurez-vous que Docker est installé en tapant `docker-compose --version` dans votre terminal.


* 
**Préparation de l'environnement** : Créez un dossier `/home/user/Documents/MongoDB` et téléchargez-y les fichiers `docker-compose.yml` et `movieDetails.bson` depuis Moodle.


* 
**Lancement des services** : Placez-vous dans ce répertoire (`cd /home/user/Documents/MongoDB/`) et lancez le conteneur avec `docker-compose up -d`.


* 
**Accès au conteneur** : Entrez dans le terminal du conteneur avec `docker exec -it mongodb bash`, puis connectez-vous au shell MongoDB avec `mongosh -u admin -p admin123 --authenticationDatabase admin`.



### **Étape 2 : Restauration des Données et Requêtage**

* 
**Importation du fichier BSON** : Copiez le fichier de données dans votre conteneur avec `docker cp movieDetails.bson mongodb:/movieDetails.bson`.


* 
**Restauration** : Utilisez la commande `mongorestore` pour importer les données dans la base de données `cinema` et la collection `films`.


* 
**Tests de requêtes** : Connectez-vous à `mongosh`, sélectionnez la base avec `use cinema;` et testez des requêtes comme `db.films.count()` ou `db.films.findOne()`.


* 
**Gestion des index** : Exercez-vous à visualiser (`getIndexes()`), créer (`createIndex()`) et supprimer (`dropIndex()`) des index pour optimiser la recherche.


* 
**Recherches avancées** : Utilisez des filtres spécifiques comme `$in`, `$gt`, `$ne` et gérez l'affichage des champs avec la projection JSON. Triez les résultats avec la fonction `sort()`.


* 
**Opérations CRUD basiques** : Pratiquez l'insertion (`insertOne`, `insertMany`), la suppression (`deleteOne`, `drop`) et la mise à jour (`updateOne`, `$set`, `$inc`, `$push`) sur une base de test.



### **Étape 3 : Création de l'Application Node.js & MongoDB (Architecture MVC)**

* 
**Architecture du projet** : Créez un répertoire `node-mongo-mvc/` et mettez en place l'architecture requise avec les dossiers `models`, `controllers`, `routes`, `services` et `config`.


* **Configuration Docker et Node** :
* Remplissez le fichier `package.json` pour définir les dépendances comme Express et Mongoose.


* Éditez le fichier `docker-compose.yml` pour orchestrer les conteneurs MongoDB et Node.js simultanément.


* Configurez le `Dockerfile` pour créer l'image de votre application Node.js.




* **Développement de l'API** :
* 
**Base de données** : Configurez la connexion Mongoose dans `config/db.js`.


* 
**Modèle** : Définissez le schéma des produits (nom et prix) dans `models/product.model.js`.


* 
**Service** : Centralisez les méthodes de manipulation des produits (`create`, `findAll`, etc.) dans `services/product.service.js`.


* 
**Contrôleur** : Gérez les requêtes HTTP et les réponses dans `controllers/product.controller.js`.


* 
**Routes** : Associez les méthodes HTTP aux fonctions du contrôleur dans `routes/product.route.js`.


* 
**Initialisation** : Liez l'ensemble des éléments et démarrez le serveur sur le port 3000 dans `app.js`.




* 
**Déploiement** : Arrêtez les anciens conteneurs (`docker-compose down`) puis construisez et lancez la nouvelle application avec `docker-compose up --build`.



### **Étape 4 : Tests des Services REST avec Postman**

* 
**Installation** : Installez le client Postman avec `sudo snap install postman`.


* **Test du CRUD** : Dans Postman, créez une collection et importez les commandes cURL fournies dans le document pour tester chaque point d'accès de votre API :
* 
**CREATE** : Testez la création de produits ("Laptop", "Phone") avec des requêtes POST sur `/api/products`.


* 
**READ** : Récupérez la liste de tous les produits (GET sur `/api/products`) ou un produit ciblé via son ID.


* 
**UPDATE** : Modifiez un produit existant (par exemple en "Laptop Pro") en utilisant une requête PUT et son ID.


* 
**DELETE** : Supprimez un produit avec une requête DELETE pointant sur son ID.




* 
**Vérification technique** : Connectez-vous au terminal `mongosh` de votre nouveau conteneur, sélectionnez `use mvcdb;`, et utilisez `db.products.find()` pour valider visuellement que les données ont bien été modifiées en base.



### **Étape 5 : Rédaction du Rapport**

* En binôme, rassemblez toutes vos manipulations, explications et captures d'écran (terminaux et Postman) dans un rapport final détaillé.
