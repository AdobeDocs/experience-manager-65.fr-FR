---
title: Démarrer et arrêter à partir de la ligne de commande
description: Découvrez comment démarrer et arrêter Adobe Experience Manager à partir de la ligne de commande.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# Démarrer et arrêter à partir de la ligne de commande{#command-line-start-and-stop}

## Démarrer Adobe Experience Manager à partir de la ligne de commande {#starting-adobe-experience-manager-from-the-command-line}

Le script `start` est disponible dans le répertoire *&lt;cq-installation>/bin*. Des versions sont fournies pour UNIX® et Windows. Le script démarre l’instance installée dans le répertoire *&lt;cq-installation>*.

Les deux versions prennent en charge une liste de variables d’environnement qui peuvent être utilisées pour démarrer et configurer l’instance Adobe Experience Manager (AEM).

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
   <td>Modes d’exécution séparés par une virgule<br /> </td>
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
>Certains modes d’exécution, dont l’instance de création et celle de publication, doivent être définis avant le premier démarrage d’AEM et ne peuvent pas être modifiés par la suite. Avant de configurer une instance d’AEM utilisée en production, consultez la [documentation sur les modes d’exécution](/help/sites-deploying/configure-runmodes.md) pour plus d’informations.

### Exemple de script start.bat pour la plateforme Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Exemple de script de démarrage de plateforme UNIX® {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Le script start lance le déploiement Quickstart AEM installé dans le dossier *&lt;cq-installation>/app*.

## Arrêter Adobe Experience Manager {#stopping-adobe-experience-manager}

Pour arrêter AEM, effectuez l’une des opérations suivantes :

* Selon la plateforme que vous utilisez :

   * Si vous avez démarré AEM à partir d’un script ou d’une ligne de commande, appuyez sur **Ctrl + C** pour arrêter le serveur.
   * Si vous avez utilisé le script de démarrage sous UNIX®, vous devez utiliser le script d’arrêt pour arrêter AEM.

* Si vous avez démarré AEM en double-cliquant sur le fichier jar, cliquez sur le bouton **Activé** dans la fenêtre de démarrage (le bouton devient alors **Désactivé**) pour arrêter le serveur.

  ![chlimage_1-63](assets/chlimage_1-63.png)

## Arrêt d’Adobe Experience Manager à partir de la ligne de commande {#stopping-adobe-experience-manager-from-the-command-line}

Le script `stop` est disponible dans le répertoire *&lt;cq-installation>/bin*. Des versions sont fournies pour UNIX® et Windows. Le script arrête l’instance en cours d’exécution installée dans le répertoire *&lt;cq-installation>*.

### Exemple de script d’arrêt de plateforme UNIX® {#unix-platform-stop-script-example}

```shell
./stop
```

### Exemple de script stop.bat pour la plateforme Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si vous souhaitez uniquement préconfigurer le référentiel (sans le relocaliser), il vous suffit d’effectuer les opérations suivantes :

* extraire `repository.xml` à l’emplacement requis ;

* mettre à jour `repository.xml` selon les besoins ;

* créer `bootstrap.properties` et définir `repository.config`.

Vous devez effectuer ces opérations avant de démarrer l’installation actuelle.
