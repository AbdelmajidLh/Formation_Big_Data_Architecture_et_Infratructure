# Formation_Big_Data_Architecture_et_Infrastructure

Ce dépôt propose une formation pratique sur l'architecture et l'infrastructure Big Data. Il couvre l'installation de Docker, Spark, et Docker Compose, ainsi que la gestion des conteneurs et l'exécution d'analyses de données avec Spark et Scala. Idéal pour apprendre à déployer et gérer des environnements Big Data.

## Sécurisation des fichiers avec Transcrypt

Pour protéger et chiffrer des fichiers sensibles dans ce dépôt, nous utilisons **Transcrypt**, un outil permettant de chiffrer les fichiers versionnés dans Git avec un mot de passe. Cela garantit que seuls les utilisateurs autorisés peuvent accéder aux données sensibles.

### Installation de Transcrypt :
1. Cloner le dépôt de Transcrypt :
    ```bash
    git clone https://github.com/elasticdog/transcrypt.git
    ```

2. Ajouter Transcrypt à votre répertoire `~/bin` (pas besoin de privilèges root) :
    ```bash
    mkdir -p ~/bin
    ln -s ${PWD}/transcrypt ~/bin/transcrypt
    ```

3. Assurez-vous que `~/bin` est dans votre `PATH` :
    ```bash
    export PATH=$PATH:~/bin
    ```

4. Chiffrer ou déchiffrer les fichiers en fonction des besoins. Par exemple, pour déchiffrer les fichiers avec votre mot de passe :
    ```bash
    transcrypt --decrypt
    ```

Pour plus de détails sur l'utilisation de Transcrypt, consultez le dépôt officiel : [Transcrypt sur GitHub](https://github.com/elasticdog/transcrypt).
