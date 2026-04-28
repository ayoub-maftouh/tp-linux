Parfait, puisque **Docker est déjà installé**, on va faire le TP **étape par étape**, exactement dans l’ordre, avec les commandes à taper.

Je vais te guider depuis **le lancement du cluster Hadoop/HBase** jusqu’aux manipulations HBase.

---

# **Étape 1 : Télécharger les fichiers du TP**

Tu dois récupérer le dossier `hadoop-main` depuis le dépôt GitLab.

Dans ton terminal :

```bash
git clone https://gitlab.com/dounia.zaidouni/hadoop.git
```

Ensuite :

```bash
cd hadoop
```

Puis vérifie les fichiers :

```bash
ls
```

Tu dois voir :

```bash
docker-compose-multiNodesHBASE.yml
lib_to_add
...
```

---

# **Étape 2 : Lancer les conteneurs Hadoop + HBase**

Toujours dans le dossier :

```bash
docker-compose -f docker-compose-multiNodesHBASE.yml up -d
```

Cette commande va lancer :

* `namenode`
* `datanode1`
* `datanode2`
* `hbase-master`
* `hbase-region`
* `zoo`

---

# **Étape 3 : Vérifier que les conteneurs tournent**

Tape :

```bash
docker ps
```

Tu dois voir plusieurs conteneurs actifs.

Exemple :

```bash
namenode
datanode1
datanode2
hbase-master
hbase-region
zoo
```

---

# **Étape 4 : Vérifier les interfaces Web**

Dans le navigateur :

### Hadoop NameNode :

```bash
http://localhost:9870
```

### HBase Master :

```bash
http://localhost:16010
```

### HBase Region :

```bash
http://localhost:16030
```

Si les pages s’ouvrent, le cluster fonctionne.

---

# **Étape 5 : Entrer dans le conteneur HBase Master**

Tape :

```bash
docker exec -it hbase-master /bin/bash
```

Tu seras dans :

```bash
root@hbase-master:/#
```

---

# **Étape 6 : Lancer le shell HBase**

Dans le conteneur :

```bash
cd /opt/hbase-2.5.10/
hbase shell
```

Puis :

```bash
status
```

Tu dois voir :

```bash
1 active master
1 servers
```

---

# **Étape 7 : Créer la table `registre_ventes`**

Dans `hbase shell` :

```bash
create 'registre_ventes','client','ventes'
```

Puis :

```bash
list
```

Tu dois voir :

```bash
registre_ventes
```

---

# **Étape 8 : Insérer les données**

Copie les commandes suivantes :

```bash
put 'registre_ventes', '101', 'client:nom', 'Mohamed A'
put 'registre_ventes', '101', 'client:ville', 'Casablanca'
put 'registre_ventes', '101', 'ventes:produit', 'Chaises'
put 'registre_ventes', '101', 'ventes:montant', '2000 MAD'

put 'registre_ventes', '102', 'client:nom', 'Amine B'
put 'registre_ventes', '102', 'client:ville', 'Sale'
put 'registre_ventes', '102', 'ventes:produit', 'Lampes'
put 'registre_ventes', '102', 'ventes:montant', '300 MAD'
```

---

# **Étape 9 : Vérifier l’insertion**

```bash
scan 'registre_ventes'
```

Tu verras les lignes insérées.

---

# **Étape 10 : Lire une valeur précise**

Exemple : produit du client 102

```bash
get 'registre_ventes','102',{COLUMN => 'ventes:produit'}
```

---

# **Étape 11 : Décrire la table**

```bash
describe 'registre_ventes'
```

Tu verras :

* familles de colonnes
* nombre de versions
* configuration

---

# **Étape 12 : Modifier une famille de colonnes**

Changer `VERSIONS` :

```bash
alter 'registre_ventes', { NAME => 'client', VERSIONS => 3 }
```

Vérifie :

```bash
describe 'registre_ventes'
```

---

# **Étape 13 : Supprimer la table**

```bash
disable 'registre_ventes'
drop 'registre_ventes'
```

Puis vérifier :

```bash
exists 'registre_ventes'
```

---

# **Étape 14 : Sortir du shell HBase**

```bash
exit
```

---

# **Étape 15 : Préparer le code Java**

Toujours dans le conteneur :

```bash
cd /
mkdir hbase-code
cd hbase-code
```

Créer le fichier :

```bash
vim HelloHBase.java
```

Puis colle le code Java donné dans le TP.

---

# **Étape 16 : Configurer CLASSPATH**

```bash
cd ~
vim .bashrc
```

Ajouter :

```bash
export CLASSPATH=/opt/hbase-2.5.10/lib/*
```

Puis :

```bash
source .bashrc
```

---

# **Étape 17 : Copier les bibliothèques nécessaires**

Sur la machine hôte (pas dans le conteneur) :

```bash
for file in ./lib_to_add/*; do
docker cp "$file" hbase-master:/opt/hbase-2.5.10/lib/
done
```

---

# **Étape 18 : Compiler le code Java**

Dans le conteneur :

```bash
cd /hbase-code
javac HelloHBase.java
```

---

# **Étape 19 : Exécuter le programme**

```bash
java -cp .:/opt/hbase-2.5.10/lib/* HelloHBase
```

Si tout va bien :

```bash
Adding user: user1
Adding user: user2
reading data...
mohamed
```

---

# **Étape 20 : Vérifier dans HBase shell**

Relance :

```bash
hbase shell
```

Puis :

```bash
scan 'user'
```

Tu verras les données insérées par Java.

---

Si tu veux, **la prochaine étape**, je peux t’aider à faire la **partie 3 du TP : chargement du fichier `purchases2.txt` dans HBase**, parce que c’est la partie la plus compliquée (HDFS + ImportTsv).
