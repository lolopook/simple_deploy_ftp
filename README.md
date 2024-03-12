# Déploiement avec GitHub Actions sur un serveur FTP

Ce guide vous montre comment configurer un déploiement automatique de votre projet sur un serveur FTP à l'aide de GitHub Actions.

## Prérequis

-   Un compte GitHub
-   Un référentiel GitHub contenant votre projet
-   Un serveur FTP avec les informations d'identification appropriées

## Étapes de configuration

### 1. Créer un fichier de workflow

Dans votre référentiel GitHub, créez un nouveau fichier dans le dossier `.github/workflows` et nommez-le `deploy.yml`. Ce fichier contiendra les instructions pour le workflow de déploiement.

### 2. Définir le workflow

Ouvrez le fichier `deploy.yml` et définissez le workflow en utilisant la syntaxe YAML. Voici un exemple de workflow simple qui se déclenche lorsque vous poussez vers la branche principale et déploie les fichiers sur votre serveur FTP :

    name: Déploiement FTP 
    on:
      push:
        branches:
          - main
    jobs:
      build:
        runs-on: ubuntu-latest
    
        steps:
        - name: Vérifier le code
          uses: actions/checkout@v2
    
        - name: Déployer sur FTP
          uses: samueldebruyn/debian-ftp-deploy-action@v2
          with:
          ftp-server: ${{ secrets.FTP_SERVER }}  
          ftp-username: ${{ secrets.FTP_USERNAME }}  
          ftp-password: ${{ secrets.FTP_PASSWORD }}  
          local-dir: .         
          remote-dir: /path/to/remote/directory
      

### 3. Ajouter des secrets

Dans votre référentiel GitHub, accédez à la section "Paramètres" et cliquez sur "Secrets". Ajoutez les secrets suivants :

-   `FTP_SERVER`  : adresse de votre serveur FTP
-   `FTP_USERNAME`  : nom d'utilisateur FTP
-   `FTP_PASSWORD`  : mot de passe FTP

Ces secrets seront utilisés pour authentifier le workflow de déploiement sur votre serveur FTP.

### 4. Pousser vers la branche principale

Une fois que vous avez configuré le workflow et ajouté les secrets, poussez le fichier `deploy.yml` vers la branche principale de votre référentiel. Le workflow de déploiement se déclenchera automatiquement et déploiera les fichiers sur votre serveur FTP.

## Conclusion

Dans ce guide, nous avons vu comment configurer un déploiement automatique sur un serveur FTP à l'aide de GitHub Actions. En suivant ces étapes simples, vous pouvez facilement automatiser votre processus de déploiement et gagner du temps et des efforts.
