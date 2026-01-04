# Projet PRF
Projet pour programmation fonctionnelle

Ce projet nécessite Java 11 pour fonctionner correctement avec Scala 2.12 et Apache Spark 3.5.x.

### Dépendances principales :

1. Java 11
2. Scala 2.12
3. Apache Spark 3.5.1
4. Maven
5. IntelliJ IDEA

## Installation (Windows 10/11)

- Vérifier si Java 11 est installé :
  Double-cliquez sur : `scripts/Verifier_JDK.bat`
  Si le message “Java 11 non installé” apparaît, passez à l’étape suivante.

- Installer Java 11 :
  Lancez l'installateur Temurin 11 (HotSpot) [ici](https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_x64_windows_hotspot_11.0.21_9.msi)

- Importer le projet dans IntelliJ :
  - Ouvrir IntelliJ IDEA
  - Sélectionner "Open" → choisir le dossier du projet
  - Attendre l'importation Maven
  - Vérifier dans `File → Project Structure` que :
    - Project SDK = temurin-11
    - spark_module SDK = temurin-11

**IMPORTANT** : Le projet contient un seul module :  
✔ `spark_module` (le module Spark)

## Installation (macOS)

- Installer Temurin 11 (.pkg) [ici](https://github.com/adoptium/temurin11-binaries/releases)

- Ouvrir IntelliJ → SDK = temurin-11.

## Installation du Scala SDK dans IntelliJ (Windows & macOS)

Apache Spark ne peut pas fonctionner sans le plugin Scala et le Scala SDK. Voici la procédure pour compiler et exécuter le projet sur tous les PC :

### 1. Installer le plugin Scala
Dans IntelliJ :
- Ouvrir `File → Settings` (Windows) ou `IntelliJ IDEA → Settings` (macOS)
- Aller dans l'onglet `Plugins`
- Chercher `Scala` et cliquer sur `Install`
- Redémarrer IntelliJ

**⚠ Sans ce plugin, IntelliJ ne détecte pas Scala et le projet Spark ne compile pas.**

### 2. Activer Scala sur le module du projet
Après installation du plugin :
- Ouvrir `File → Project Structure`
- Aller dans `Modules` → Sélectionner le module `spark_module`
- Si un message apparaît en haut : `No Scala SDK in module — Setup Scala SDK`
  - Cliquer dessus et ajouter le SDK Scala (version 2.12.19).

### 3. Créer une Scala SDK (la première fois)
Si la liste est vide → cliquer sur `Create…` et choisir :
- Scala version : 2.12.19
- Sources auto-téléchargées (IntelliJ va télécharger automatiquement)

### 4. Vérifier que le Scala SDK est bien actif
Toujours dans `Project Structure` :
- Dans `Project` : SDK = temurin-11, Language level = SDK default
- Dans `Modules → spark_module → Dependencies` : Vous devez voir dans la liste `scala-sdk-2.12.19` avec `Scope = Compile`

### 5. Structure correcte du module (OBLIGATOIRE)
Vérifier que IntelliJ a bien détecté les bons dossiers :
- `src/main/scala` → Sources
- `src/main/java` → Sources
- `src/main/resources` → Resources
- `target/` → Excluded

Si ce n’est pas le cas, faites un clic droit sur `scala` → `Mark Directory as → Sources Root`, et sur `target` → `Mark Directory as → Excluded`


## Explication des fichiers du projet

### Fichiers principaux dans le dossier `src/main/scala` :

1. **`Partie_2_et_3_AnalyseTempo.scala`** :  
   Analyse des données de pollution sur des périodes temporelles. Ce fichier réalise des transformations basées sur les dates et heures pour calculer des statistiques comme les moyennes et les pics de pollution.

2. **`Partie_4_ModelisationAvecGraphX.scala`** :  
   Utilise **Spark GraphX** pour modéliser les relations entre les stations de pollution sous forme de graphes. Il étudie la propagation de la pollution au sein du réseau urbain.

3. **`Partie_2_et_3_PollutionSurStations.scala`** :  
   Analyse de la pollution mesurée dans différentes stations de mesure. Ce fichier calcule des statistiques comme la pollution moyenne, maximum et minimum par station.

4. **`Partie_2_AnalyseParDepartement.scala`** :  
   Analyse de la pollution par zone géographique (par exemple, par département), avec des comparaisons des niveaux de pollution entre différentes zones.

5. **`Partie_6_TempsReel.scala`** :  
   Gère le traitement des données en temps réel (streaming), y compris la détection et le signalement automatique des anomalies dans les flux de données de pollution.

6. **`Partie_5_Pre╠üdiction.scala`** :  
   Prédiction des niveaux de pollution futurs à l'aide de modèles de machine learning (probablement avec Spark MLlib), en utilisant des techniques comme la régression ou les forêts aléatoires.

7. **`generate_graph.scala`** :  
   Génère des graphiques de visualisation des données de pollution, probablement à l'aide de bibliothèques Java comme JFreeChart ou d'autres outils de visualisation intégrés dans Spark.

### Autres fichiers importants :

- **`pom.xml`** :  
  Fichier de configuration Maven qui gère les dépendances du projet et la structure du build.
  
- **`jfreechart.iml`** :  
  Fichier de configuration pour le projet dans IntelliJ IDEA.
  
- **`.gitignore`** :  
  Liste des fichiers à ignorer par Git, pour éviter de suivre des fichiers temporaires ou des dépendances spécifiques à l'environnement de développement.

Ces fichiers forment la base de l'application de traitement de données de pollution, en utilisant Apache Spark et la programmation fonctionnelle.

