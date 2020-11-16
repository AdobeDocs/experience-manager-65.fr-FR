---
title: Résolution des incidents liés à AEM
seo-title: Résolution des incidents liés à AEM
description: Découvrez les problèmes de résolution des incidents liés à AEM.
seo-description: Découvrez les problèmes de résolution des incidents liés à AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 78%

---


# Résolution des incidents liés à AEM {#troubleshooting-aem}

La section ci-dessous traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour les résoudre.

>[!NOTE]
>
>Si vous résolvez les problèmes liés à la création dans AEM, voir [Résolution des incidents pour les créateurs](/help/sites-authoring/troubleshooting.md).

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter les [problèmes connus](/help/release-notes/known-issues.md) relatifs à votre instance (packs de version et service packs).

## Scénarios de résolution des incidents pour les administrateurs {#troubleshooting-scenarios-for-administrators}

Le tableau ci-dessous contient une présentation des incidents que les administrateurs peuvent avoir à résoudre :

<table>
 <tbody>
  <tr>
   <td><strong>Rôle(s)</strong></td>
   <td><strong>Problème </strong></td>
  </tr>
  <tr>
   <td>Administrateur système</td>
   <td><p>Lorsque vous double-cliquez sur le fichier Quickstart jar, rien ne se produit ou le fichier s’ouvre dans un autre programme (par exemple, le gestionnaire d’archives).</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> </td>
   <td><p>Mon application qui s’exécute sur CRX génère des erreurs de mémoire insuffisante.</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> </td>
   <td><p>L’écran de bienvenue AEM ne s’affiche pas dans le navigateur après avoir cliqué sur l’doublon AEM CM Quickstart</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> <p>utilisateur admin</p> </td>
   <td><p>Création d’une image mémoire des threads</p> </td>
  </tr>
  <tr>
   <td><p>Administrateur système</p> <p>utilisateur admin</p> </td>
   <td><p>Contrôle des sessions JCR non fermées</p> </td>
  </tr>
 </tbody>
</table>

## Problèmes d’installation {#installation-issues}

Pour plus d’informations sur les scénarios de résolution des incidents ci-dessous, voir [Problèmes d’installation fréquents](/help/sites-deploying/troubleshooting.md#common-installation-issues) :

* Un double clic sur le fichier .jar Quickstart n’a aucun effet, ou le fichier JAR est utilisé avec un autre programme (tel que le gestionnaire d’archive).
* Les applications qui s’exécutent sur CRX génèrent des erreurs de mémoire insuffisante.
* Après avoir double-cliqué sur Quickstart AEM, l’écran de bienvenue d’AEM ne s’affiche pas dans le navigateur.

## Méthodes d’analyse de la résolution des incidents {#methods-for-troubleshooting-analysis}

### Création d’une image mémoire des threads {#making-a-thread-dump}

L’image mémoire des threads est une liste de toutes les unités d’exécution Java actuellement actives. Si AEM ne répond pas correctement, l’image mémoire des threads peut vous aider à identifier des verrouillages ou d’autres problèmes.

### Utilisation du programme d’image mémoire des threads Sling {#using-sling-thread-dumper}

1. Open the **AEM Web Console**; for example at `https://localhost:4502/system/console/`.
1. Select the **Threads** under **Status** tab.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilisation de jstack (ligne de commande) {#using-jstack-command-line}

1. Recherchez le PID (ID de processus) de l’instance Java AEM.

   For example, you can use `ps -ef` or `jps`.

1. Exécuter:

   `jstack <pid>`

1. L’image mémoire des threads s’affiche.

>[!NOTE]
>
>You can append the thread dumps to a log file by using the `>>` output redirection:
>
>`jstack <pid> >> /path/to/logfile.log`

Pour plus d’informations, voir [Comment utiliser les images mémoire des threads d’une machine virtuelle Java (JVM)](https://helpx.adobe.com/cq/kb/TakeThreadDump.html).

### Contrôle des sessions JCR non fermées {#checking-for-unclosed-jcr-sessions}

Lorsque la fonctionnalité est développée pour AEM WCM, il est possible d’ouvrir des sessions JCR (cela s’apparente à l’ouverture d’une connexion de base de données). Si les sessions ouvertes ne sont jamais fermées, votre système peut rencontrer les symptômes suivants :

* Le système est ralenti.
* Vous pouvez voir beaucoup de CacheManager : resizeToutes les entrées du fichier journal ; le nombre suivant (size=&lt;x>) indique le nombre de caches ; chaque session ouvre plusieurs caches.
* Parfois, la mémoire du système est saturée (après quelques heures, jours ou semaines, selon la gravité).

Pour analyser les sessions non fermées et découvrir le code qui ne ferme pas une session, consulter l’article [Analyse des sessions non fermées](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html) de la base de connaissances.

### Utilisation de la console web d’Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Le statut des lots OSGi peut également fournir une indication précoce de problèmes éventuels.

1. Open the **AEM Web Console**; for example at `https://localhost:4502/system/console/`.
1. Select **Bundles** under **OSGI** tab.
1. Vérifiez :

   * le statut des lots. Si le statut est Inactif ou Insatisfait, essayez d’arrêter et de redémarrer le lot. Si le problème persiste, un examen plus approfondi peut être nécessaire à l’aide d’autres méthodes.
   * Si l’un des lots possède des dépendances manquantes. Ces informations peuvent être affichées en cliquant sur le nom de chaque lot, qui est un lien (l’exemple ci-dessous ne comporte aucun problème) :

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

