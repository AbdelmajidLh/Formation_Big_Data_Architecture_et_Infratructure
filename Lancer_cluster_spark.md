Voici une version structurée de ton contenu sous format Markdown, optimisé pour une documentation professionnelle sur GitHub :

```md
# Formation Big Data : Installation et Configuration de Spark avec Docker

## 1. Télécharger et installer Docker sur Ubuntu
Suivre la documentation officielle pour installer Docker sur Ubuntu : [Installation Docker Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

### Étapes :
1. Mettre à jour les paquets :
    ```bash
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    ```

2. Ajouter la clé GPG officielle de Docker :
    ```bash
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    ```

3. Ajouter le dépôt Docker aux sources Apt :
    ```bash
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

4. Mettre à jour les sources et installer Docker :
    ```bash
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

## 2. Télécharger et installer Apache Spark
Téléchargez la dernière version de Spark depuis le site officiel : [Téléchargement Spark](https://spark.apache.org/downloads.html).

### Étapes :
1. Décompresser l'archive dans le dossier de la formation :
    ```bash
    tar -xvzf spark-*.tgz
    ```

## 3. Installer Docker Compose
Installez Docker Compose via les paquets apt :
```bash
sudo apt-get install docker-compose
```

## 4. Télécharger le Docker Compose Bitnami pour Spark
Télécharger le fichier `docker-compose.yml` depuis le dépôt GitHub de Bitnami :
```bash
curl -LO https://raw.githubusercontent.com/bitnami/containers/main/bitnami/spark/docker-compose.yml
```

## 5. Modifier le fichier Docker Compose pour ajouter des volumes
Ajoutez les volumes nécessaires dans le fichier `docker-compose.yml` selon vos besoins.

## 6. Lancer Docker en mode détaché
Démarrez les conteneurs en mode détaché :
```bash
docker-compose up -d
```

## 7. Vérifier les conteneurs en cours d'exécution
Listez les conteneurs actifs :
```bash
docker container ls
```

## 8. Accéder à l'interface d'administration de Spark
Ouvrez l'interface web de Spark à l'adresse suivante :
```
localhost:8080
```
Récupérez l'URL du maître Spark (`spark://<hostname>:<port>`).

## 9. Utiliser Spark Shell (2 méthodes)

### Méthode 1 : Utilisation en local
1. Naviguez vers le dossier Spark :
    ```bash
    cd spark-3.5/bin/
    ```

2. Lancez le shell Spark :
    ```bash
    ./spark-shell --master spark://<hostname>:<port>
    ```

### Méthode 2 : Utilisation dans un conteneur Docker
1. Identifiez l'ID du conteneur maître Spark :
    ```bash
    docker container ls
    ```

2. Accédez au conteneur maître :
    ```bash
    docker exec -it <container_id> /bin/bash
    ```

3. Lancez Spark Shell depuis le conteneur :
    ```bash
    cd /opt/bitnami/spark/
    bin/spark-shell --master spark://<hostname>:<port>
    ```

## 10. Exécuter une analyse avec Spark (Scala)

### Exemple de script Spark Scala :

```scala
import spark.implicits._
import spark.sql

val inputFile = sc.textFile("/test-files/dups.txt")
val sqlContext = new org.apache.spark.sql.SQLContext(sc)

case class Dup(name: String, value: Int)
val dupDF = inputFile.map(_.split(",")).map(e => Dup(e(0).trim, e(1).trim.toInt)).toDF()

// Créer une table temporaire
dupDF.createOrReplaceTempView("dupsTable")

// Grouper par 'name' et faire la somme de 'value'
dupDF.groupBy("name").sum("value")
  .withColumnRenamed("name", "Name")
  .withColumnRenamed("sum(value)", "Sum")
  .show()
```

---

Ce guide couvre l'installation et l'utilisation de Docker, Spark, ainsi que l'exécution de scripts Spark pour analyser des données en Scala.
```
