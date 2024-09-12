@import "../../../style/styles_epitech_stage.less"

# workflow_java.yml
Voici le workflow pour les projets Java contenant des sources, les explications sont en dessous...
```yaml
##
## SYMEXO PROJECT, 2024
## Refonte Usine Logicielle
## File description:
## make.yml
##
 
# ? Ce workflow consiste à vérifier la compilation du code, si la compilation réussi les tests paramétrés s'exécutent.
# ? Enfin, il envoie la lib générée sur Sonatype Nexus Repository et envoie le code sur Sonarqube pour une évaluation de celui-ci

name: Compilation et envoi sur Sonarqube et Sonatype Nexus d'un projet Java

on:
  push:
    branches-ignore:
      - "feature*"
  pull_request:
    branches-ignore:
      - "feature*"
  release:
    branches-ignore:
      - "feature*"

env:
  ContainerID: "e2b17b1dd4327005c8d0d8493f76b7644546116c87ba5fad70231fc5cffc5b34"

jobs:
  push_to_sonatype_and_sonarqube:
    runs_on: ubuntu-latest

    if: (github.event_name == 'push' || github.event_name == 'release')
    steps:

      - name: Checkout code and dependencies
        uses: actions/checkout@v2

      - name: Install Maven
        run: |
          sudo apt-get update
          sudo apt-get install -y maven

      - name: Install Java
        uses: actions/setup-java@v2
        with:
          java-version: '15'
          distribution: 'adopt'

      - name: Checkout dependencies
        run: |
          docker cp $ContainerID:/mnt/_data/.m2/. /root/.m2/

      - name: Deploy to Nexus
        run: |
          mvn clean deploy

      - name: SonarQube Scan
        uses: sonarsource/sonarqube-scan-action@master
        with:
          args: >
            -Dsonar.projectKey=${{ github.repository_owner }}.${{ github.event.repository.name }}
            -Dsonar.sources=src/main/java/
            -Dsonar.java.binaries=target/classes
            -Dsonar.inclusions=**/*
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          SONAR_HOST_URL: http://sonarqube-sonarqube-1:9000

      - name: Save dependencies
        run: |
          docker cp /root/.m2/. $ContainerID:/mnt/_data/.m2/

  # run_tests:
  #   needs: build
  #   timeout-minutes: 2
  #   runs-on: ubuntu-latest

  #   steps:
  #     - name: Checkout
  #       uses: actions/checkout@v2

  #     - name: run tests
  #       run: make tests_run

```
**FIN DU FICHIER**

## Initialisation
```yaml
on:
  push:
    branches-ignore:
      - "feature*"
  pull_request:
    branches-ignore:
      - "feature*"
  release:
    branches-ignore:
      - "feature*"
```
Ici, je définis **quand est-ce que le Workflow va s'exécuter**, dans ce cas, il s'exécuteras lors de **Pushs**, de **Realeases** et de **Pull Requests** tout en **ignorant les branche qui commencent par "feature"**

## Création du job **"push_to_sonatype_and_sonarqube"**
```yaml
  push_to_sonatype_and_sonarqube:
    runs_on: ubuntu-latest

    if: (github.event_name == 'push' || github.event_name == 'release')
```
Celui-ci tourne sous **ubuntu-latest** et **s'exécutera seulement si** l'action effectuée est un **push** ou une **release**.<br><br>

```yaml
 steps:

      - name: Checkout code
        uses: actions/checkout@v2

      - name: Install Maven
        run: |
          sudo apt-get update
          sudo apt-get install -y maven

      - name: Install Java
        uses: actions/setup-java@v2
        with:
          java-version: '15'
          distribution: 'adopt'

      - name: Checkout dependencies
        run: |
          docker cp $ContainerID:/mnt/_data/.m2/. /root/.m2/
```
Dans ces étapes nous **récupérons les dépendances et le code** tout en **installant Maven et Java** et en **créant et remplissant le fichier "settings-security.xml"** avec le mot de passe généré par la commande ```mvn --encrypt-password <password>``` qui nous sera utile lors de l'envoi sur Nexus Repository Manager.<br><br>

```yaml
      - name: Deploy to Nexus
        run: |
          mvn clean deploy

      - name: Save dependencies
        run: |
          docker cp /root/.m2/. $ContainerID:/mnt/_data/.m2/
```
Celle-ci va **compléter le "settings.xml"** avec toutes les informations nécessaire, dont le mot de passe de Nexus que nous avons crypter en utilisant la commande ```mvn --encrypt-password <password>```. Ensuite, il va **compiler** le projet et **envoyer tous les artéfacts générés sur Nexus Repository Manager** et enfin va enregistrer les dépendances utilisées directement dans un volume qui servira de cache.

## Envoi du code sur **SonarQube**
```yaml
      - name: SonarQube Scan
        uses: sonarsource/sonarqube-scan-action@master
        with:
          args: >
            -Dsonar.projectKey=${{ github.repository_owner }}.${{ github.event.repository.name }}
            -Dsonar.sources=src/main/java/
            -Dsonar.java.binaries=target/classes
            -Dsonar.inclusions=**/*
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          SONAR_HOST_URL: http://sonarqube-sonarqube-1:9000
```
Ici, j'**envoie le code sur SonarQube** à l'aide de son action, il visera les sources contenues dans ***src/main/java/*** et les artéfacts contenus dans ***target/classes*** en incluant tous les fichiers. Tout ça en utilisant le Jeton récupéré dans SonarQube et son URL. <br>

## Création du Job **"run_tests"**
```yaml
   run_tests:
     needs: build
     timeout-minutes: 2
     runs-on: ubuntu-latest

     steps:
       - name: Checkout
         uses: actions/checkout@v2

       - name: run tests
         run: make tests_run
```
Ce job **exécute les tests** qui sont paramétrés dans le Makefile, **en récupérant le code** et **exécutant la commande "make tests_run"**


# workflow_java_pom.yml
Les seules différences entre le workflow_java_pom et le workflow_java est que dans le workflow_java_pom.yml nous allons **retirer l'envoi du code vers SonarQube**.
<br><br><br><br><br>
# Code
## workflow_java.yml
```yaml
##
## SYMEXO PROJECT, 2024
## Refonte Usine Logicielle
## File description:
## make.yml
##
 
# ? Ce workflow consiste à vérifier la compilation du code, si la compilation réussi les tests paramétrés s'exécutent.
# ? Enfin, il envoie la lib générée sur Sonatype Nexus Repository et envoie le code sur Sonarqube pour une évaluation de celui-ci

name: Compilation et envoi sur Sonarqube et Sonatype Nexus d'un projet Java

on:
  push:
    branches-ignore:
      - "feature*"
  pull_request:
    branches-ignore:
      - "feature*"
  release:
    branches-ignore:
      - "feature*"

env:
  ContainerID: "e2b17b1dd4327005c8d0d8493f76b7644546116c87ba5fad70231fc5cffc5b34"

jobs:
  push_to_sonatype_and_sonarqube:
    runs_on: ubuntu-latest

    if: (github.event_name == 'push' || github.event_name == 'release')
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Install Maven
        run: |
          sudo apt-get update
          sudo apt-get install -y maven

      - name: Install Java
        uses: actions/setup-java@v2
        with:
          java-version: '15'
          distribution: 'adopt'

      - name: Checkout dependencies
        run: |
          mkdir -p /root/.m2/
          docker cp $ContainerID:/mnt/_data/.m2/. /root/.m2/

      - name: Deploy to Nexus
        run: |
          mvn clean deploy

      - name: SonarQube Scan
        uses: sonarsource/sonarqube-scan-action@master
        with:
          args: >
            -Dsonar.projectKey=${{ github.repository_owner }}.${{ github.event.repository.name }}
            -Dsonar.sources=src/main/java/
            -Dsonar.java.binaries=target/classes
            -Dsonar.inclusions=**/*
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          SONAR_HOST_URL: http://sonarqube-sonarqube-1:9000

      - name: Save dependencies
        run: |
          docker cp /root/.m2/. $ContainerID:/mnt/_data/.m2/

  # run_tests:
  #   needs: build
  #   timeout-minutes: 2
  #   runs-on: ubuntu-latest

  #   steps:
  #     - name: Checkout
  #       uses: actions/checkout@v2

  #     - name: run tests
  #       run: make tests_run

```

## workflow_java_pom.yml
```yaml
##
## SYMEXO PROJECT, 2024
## Refonte Usine Logicielle
## File description:
## make.yml
##
 
# ? Ce workflow consiste à vérifier la compilation du code, si la compilation réussi les tests paramétrés s'exécutent.
# ? Enfin, il envoie la lib générée sur Sonatype Nexus Repository et envoie le code sur Sonarqube pour une évaluation de celui-ci

name: Compilation et envoi sur Sonarqube et Sonatype Nexus d'un projet Java

on:
  push:
    branches-ignore:
      - "feature*"
  pull_request:
    branches-ignore:
      - "feature*"
  release:
    branches-ignore:
      - "feature*"

env:
  ContainerID: "e2b17b1dd4327005c8d0d8493f76b7644546116c87ba5fad70231fc5cffc5b34"

jobs:
  push_to_sonatype_and_sonarqube:
    runs_on: ubuntu-latest

    if: (github.event_name == 'push' || github.event_name == 'release')
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Install Maven
        run: |
          sudo apt-get update
          sudo apt-get install -y maven

      - name: Install Java
        uses: actions/setup-java@v2
        with:
          java-version: '15'
          distribution: 'adopt'

      - name: Checkout dependencies
        run: |
          mkdir -p /root/.m2/
          docker cp $ContainerID:/mnt/_data/.m2/. /root/.m2/

      - name: Deploy to Nexus and save dependencies
        run: |
          mvn clean deploy
          docker cp /root/.m2/. $ContainerID:/mnt/_data/.m2/

  # run_tests:
  #   needs: build
  #   timeout-minutes: 2
  #   runs-on: ubuntu-latest

  #   steps:
  #     - name: Checkout
  #       uses: actions/checkout@v2

  #     - name: run tests
  #       run: make tests_run
```