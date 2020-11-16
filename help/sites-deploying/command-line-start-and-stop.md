---
title: Début et arrêt d’AEM à partir de la ligne de commande
seo-title: Début et arrêt d’AEM à partir de la ligne de commande
description: Découvrez comment démarrer et arrêter AEM à partir de la ligne de commande.
seo-description: Découvrez comment démarrer et arrêter AEM à partir de la ligne de commande.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 93%

---


# Début et arrêt d’AEM à partir de la ligne de commande{#command-line-start-and-stop}

## Démarrage d’Adobe Experience Manager à partir de la ligne de commande {#starting-adobe-experience-manager-from-the-command-line}

Le script `start` est disponible dans le répertoire *&lt;cq-installation>/bin*. Des versions sont fournies pour Unix et Windows. Le script démarre l’instance installée dans le répertoire *&lt;cq-installation>*.

Ces deux versions prennent en charge une liste de variables d’environnement qui peuvent être utilisées pour début et régler l’instance AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variable d’environnement </strong></td>
   <td><strong>Description </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Port TCP utilisé pour les scripts stop et status.<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nom de l’hôte.<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interface que doit écouter ce serveur.<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Mode(s) d’exécution séparé(s) par une virgule.<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nom du fichier JAR.<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Utilisation de JAAS (si la valeur est true).<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Chemin d’accès à la configuration JAAS.<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Options JVM par défaut.<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Remarque : Certains modes d’exécution, comme création et publication, doivent être définis avant le premier démarrage d’AEM. Ils ne peuvent pas être modifiés par la suite. Avant de configurer une instance AEM à utiliser en production, consultez la [documentation sur les modes d’exécution](/help/sites-deploying/configure-runmodes.md) pour plus d’informations.

### Exemple de script start.bat pour la plateforme Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemple de script start pour la plateforme Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Le script start lance Démarrage rapide d’AEM installé dans le dossier *&lt;cq-installation>/app*.

## Arrêt d’Adobe Experience Manager {#stopping-adobe-experience-manager}

Pour arrêter AEM, effectuez l’une des opérations suivantes :

* Selon la plateforme que vous utilisez :

   * Si vous avez démarré AEM à partir d’un script ou d’une ligne de commande, appuyez sur **Ctrl + C** pour arrêter le serveur.
   * Si vous avez utilisé le script start sous UNIX, vous devez utiliser le script stop pour arrêter AEM.

* Si vous avez démarré AEM en double-cliquant sur le fichier jar, cliquez sur le bouton **Activé** dans la fenêtre de démarrage (le bouton se transforme alors en **Désactivé**) pour arrêter le serveur.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Arrêt d’Adobe Experience Manager à partir de la ligne de commande {#stopping-adobe-experience-manager-from-the-command-line}

Le script `stop` est disponible dans le répertoire *&lt;cq-installation>/bin*. Des versions sont fournies pour Unix et Windows. Le script arrête l’instance en cours d’exécution installée dans le répertoire *&lt;cq-installation>*.

### Exemple de script stop pour la plateforme Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemple de script stop.bat pour la plateforme Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si vous souhaitez uniquement préconfigurer le référentiel (sans le déplacer), vous devez simplement :

* extraire `repository.xml` à l’emplacement requis ;

* update `repository.xml` as required

* créer `bootstrap.properties` et définir `repository.config`

Vous devez effectuer ces opérations avant de démarrer l’installation actuelle.

