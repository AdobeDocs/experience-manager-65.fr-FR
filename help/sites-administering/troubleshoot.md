---
title: Dépannage d’Adobe Experience Manager
description: Découvrez les problèmes de dépannage avec AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 33%

---

# Dépannage d’Adobe Experience Manager {#troubleshooting-aem}

La section suivante décrit certains problèmes que vous pouvez rencontrer lors de l’utilisation d’AEM (Adobe Experience Manager), ainsi que des suggestions pour les résoudre.

>[!NOTE]
>
>Si vous résolvez les problèmes liés à la création dans AEM, reportez-vous à la section [Résolution des problèmes pour les auteurs.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>En cas de problème, il est également intéressant de consulter la liste des [Problèmes connus](/help/release-notes/release-notes.md) pour votre instance (Service Packs et version).

## Scénarios de dépannage pour les administrateurs {#troubleshooting-scenarios-for-administrators}

Le tableau suivant présente un aperçu des problèmes que les administrateurs peuvent résoudre :

<table>
 <tbody>
  <tr>
   <td><strong>Rôle</strong></td>
   <td><strong>Problème </strong></td>
  </tr>
  <tr>
   <td>Administrateur système</td>
   <td><p>Double-cliquer sur le fichier JAR Quickstart n’a aucun effet ou ouvre le fichier JAR avec un autre programme (par exemple, le gestionnaire d’archives).</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> </td>
   <td><p>Mon application qui s’exécute sur CRX génère des erreurs de mémoire insuffisante.</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> </td>
   <td><p>Après avoir double-cliqué sur Quickstart CM AEM, l’écran d’accueil d’AEM ne s’affiche pas dans le navigateur</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> <p>utilisateur administrateur</p> </td>
   <td><p>Création d’une image mémoire des threads</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> <p>utilisateur administrateur</p> </td>
   <td><p>Contrôle des sessions JCR non fermées</p> </td>
  </tr>
 </tbody>
</table>

## Problèmes d’installation {#installation-issues}

Voir [Problèmes d’installation courants](/help/sites-deploying/troubleshooting.md#common-installation-issues) pour plus d’informations sur les scénarios de dépannage suivants :

* Double-cliquer sur le fichier Quickstart jar n’a aucun effet sur le fichier JAR avec un autre programme (tel que le gestionnaire d’archives).
* Les applications s’exécutant sur CRX renvoient des erreurs de mémoire insuffisante.
* Après avoir double-cliqué sur Quickstart AEM, l’écran d’accueil d’AEM ne s’affiche pas dans le navigateur.

## Méthodes d’analyse de dépannage {#methods-for-troubleshooting-analysis}

### Créer une image mémoire des threads {#making-a-thread-dump}

Le thread dump est une liste de tous les threads Java™ actuellement principaux. Si AEM ne répond pas correctement, le thread dump peut vous aider à identifier les blocages ou d’autres problèmes.

### Utilisation de Sling Thread Dumper {#using-sling-thread-dumper}

1. Ouvrez le **Console web d’AEM**; par exemple, à l’adresse `https://localhost:4502/system/console/`.
1. Sélectionnez les **threads** dans l’onglet **Statut**.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilisation de jstack (ligne de commande) {#using-jstack-command-line}

1. Recherchez le PID (ID de processus) de l’instance Java™ AEM.

   Vous pouvez, par exemple, utiliser `ps -ef` ou `jps`.

1. Exécutez :

   `jstack <pid>`

1. Affiche le vidage des threads.

>[!NOTE]
>
>Vous pouvez ajouter les images mémoire des threads à un fichier journal en utilisant la redirection de sortie `>>` :
>
>`jstack <pid> >> /path/to/logfile.log`

Pour plus d’informations, consultez la section [Comment utiliser les images mémoire des threads d’une machine virtuelle Java (JVM)](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=en).

### Contrôle des sessions JCR non fermées {#checking-for-unclosed-jcr-sessions}

Lorsque la fonctionnalité est développée pour AEM WCM, il est possible d’ouvrir des sessions JCR (cela s’apparente à l’ouverture d’une connexion de base de données). Si les sessions ouvertes ne sont jamais fermées, votre système peut présenter les symptômes suivants :

* Le système devient plus lent.
* Vous pouvez voir une grande partie de CacheManager : resizeAll entrées dans le fichier journal ; le nombre suivant (size=&lt;x>) indique le nombre de caches. Chaque session ouvre plusieurs caches.
* Parfois, la mémoire du système est saturée (après quelques heures, jours ou semaines, selon la gravité).

Pour analyser les sessions non fermées et déterminer le code qui ne ferme pas une session, reportez-vous à l’article de la base de connaissances [Analyse des sessions non fermées](https://helpx.adobe.com/fr/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Utilisation de la console web Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

L’état des lots OSGi peut également donner une indication précoce des problèmes possibles.

1. Ouvrez le **Console web d’AEM**; par exemple, à l’adresse `https://localhost:4502/system/console/`.
1. Sélectionnez **Lots** dans l’onglet **OSGI**.
1. Vérifier :

   * le statut des lots. Si certains sont inactifs ou insatisfaits, essayez d’arrêter et de redémarrer le lot. Si le problème persiste, recherchez d’autres méthodes.
   * Si l’un des lots possède des dépendances manquantes. Ces détails sont visibles en cliquant sur le nom du lot individuel, qui est un lien (l’exemple suivant ne présente aucun problème) :

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
