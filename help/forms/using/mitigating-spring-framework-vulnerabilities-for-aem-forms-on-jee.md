---
title: Atténuation des vulnérabilités du framework Spring pour AEM Forms sur JEE
description: Atténuation des vulnérabilités du framework Spring pour AEM Forms sur JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: f704b58a-7bd8-401e-8d7e-2cc3b580c570
source-git-commit: d2ae4817720cae92b038789804124e0c2465f9c8
workflow-type: ht
source-wordcount: '563'
ht-degree: 100%

---

# Atténuation des vulnérabilités du framework Spring pour AEM Forms sur JEE

Ce document fournit des instructions relatives à la résolution de deux vulnérabilités critiques du framework Spring qui affectent AEM Forms sur JEE :

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)** : vulnérabilité de traversée de répertoires dans les frameworks web fonctionnels
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)** : exception de correspondance de la sensibilité à la casse dans DataBinder dans le framework Spring

## Versions affectées

- Adobe Experience Manager 6.5 Forms sur JEE
- Versions AEM 6.5 Forms en disponibilité générale jusqu’à 6.5.22.0

## Résolution

### Solutions spécifiques à la version

| Version d’AEM Forms | Action requise |
|-------------------|-----------------|
| 6.5.22.0 | &#x200B;1. [Téléchargez le correctif pour votre environnement](/help/release-notes/aem-forms-hotfix.md). </br> 2. Pour installer ce correctif, suivez les instructions pour [installer le pack de services pour AEM Forms sur JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). |
| 6.5.17.0 - 6.5.21.0 | [Appliquez les étapes d’atténuation manuelles](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | &#x200B;1. [Installez le dernier pack de services](/help/release-notes/release-notes.md)<br>2. [Implémentez la solution appropriée](#version-specific-solutions) en fonction de votre version mise à jour. |

> **Note** : AEM Forms ne prend officiellement en charge que les six packs de service les plus récents. Les utilisateurs et les utilisatrices possédant des versions plus anciennes doivent d’abord effectuer la mise à niveau vers le dernier pack de services puis installer le correctif requis.

## Considérations relatives au déploiement

### Pour les environnements en clusters

Lorsque vous travaillez sur un déploiement en clusters :

- Appliquez des remplacements de fichiers JAR (étape n°4) sur **tous les nœuds** du cluster.
- Conservez la cohérence en utilisant des versions de fichier JAR identiques sur tous les serveurs.
- Effectuez les mises à jour sur tous les nœuds avant de lancer tout redémarrage de service.
- Implémentez une stratégie de redémarrage coordonnée afin de réduire au minimum les temps d’arrêt du système.

### Pour les environnements à nœud unique

Lorsque vous travaillez sur un déploiement autonome :

- Suivez un processus simplifié, car il n’y a aucun serveur de localisation à gérer.
- Ignorez toute étape liée à la configuration ou au démarrage du serveur de localisation.
- Suivez toutes les autres étapes comme indiqué, en particulier les remplacements des fichiers JAR et les mises à jour des manifestes.
- Redémarrez votre serveur d’applications après avoir implémenté toutes les modifications.

## Étapes d’atténuation manuelles

1. Arrêtez les serveurs d’applications.
1. Arrêtez les serveurs de localisation.
1. Supprimez les fichiers JAR Spring du fichier Core EAR :
   1. Accédez à `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. Ouvrez le fichier `adobe-core-<appserver>.ear` à l’aide d’un outil de gestion d’archives. `<appserver>` peut être JBoss, WebLogic ou WebSphere, en fonction de votre environnement :
   - **Pour JBoss :** accédez au dossier `ear/lib` et supprimez les fichiers JAR suivants :
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Pour WebLogic ou WebSphere :** supprimez les fichiers JAR suivants de la racine de l’EAR :
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Pour tous les serveurs d’applications :** au niveau racine du `adobe-core-<appserver>.ear`, ouvrez le fichier `adobe-dscf.jar` et modifiez le fichier `META-INF/MANIFEST.MF` pour supprimer toute référence aux fichiers JAR suivants :
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Remplacez les fichiers JAR de la distribution Geode :
   1. Accéder à `<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. Remplacez les fichiers JAR existants par les versions mises à jour :
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   Pour obtenir les fichiers JAR les plus récents, téléchargez le fichier spring-6.1.14-jars.zip à partir de la [distribution logicielle Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip) et extrayez le fichier ZIP pour accéder aux fichiers JAR mis à jour du framework Spring.

   1. Mettez à jour les fichiers MANIFEST.MF dans les fichiers JAR suivants :
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   Pour chaque fichier JAR :
   - Ouvrez le fichier JAR à l’aide d’un outil de gestion d’archives.
   - Recherchez et extrayez le fichier `META-INF/MANIFEST.MF`.
   - Modifiez le fichier MANIFEST.MF dans un éditeur de texte.
   - Recherchez la section « Class-Path » et mettez à jour toutes les références du framework Spring :
      - `spring-core-<version>.jar` vers `spring-core-6.1.14.jar`
      - `spring-web-<version>.jar` vers `spring-web-6.1.14.jar`
      - `spring-context-<version>.jar` vers `spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar` vers `spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar` vers `spring-jcl-6.1.14.jar`
   - Enregistrez le fichier MANIFEST.MF modifié.
   - Remplacez le fichier MANIFEST.MF d’origine dans le fichier JAR par votre version mise à jour.
   - Enregistrez le fichier JAR.

   1. Problèmes courants auxquels faire attention :
      - Vérifiez qu’il n’existe aucune entrée en double dans le manifeste.
      - Utilisez des fins de ligne appropriées.
      - Vérifiez que tous les fichiers JAR référencés existent aux emplacements spécifiés.

   1. Étapes de vérification :
      - Vérifiez si le manifeste a correctement été mis à jour.
      - Vérifiez que toutes les dépendances Spring sont correctement référencées.
      - Assurez-vous qu’il ne reste aucune référence d’une ancienne version.
      - Testez l’application pour vous assurez qu’il n’y a aucun problème de chargement de classe.

1. Ouvrez le gestionnaire de configuration.

1. Redémarrez les serveurs :
   - Démarrez les serveurs de localisation à l’aide de JDK 17.
   - Démarrez les serveurs d’applications à l’aide de la même version du JDK (JDK 8 ou JDK 11) que celle utilisée précédemment.
