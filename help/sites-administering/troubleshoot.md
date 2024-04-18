---
title: Dépannage d’Adobe Experience Manager
description: Découvrez comment résoudre certains problèmes pouvant survenir avec Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 99%

---

# Dépannage d’Adobe Experience Manager {#troubleshooting-aem}

La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM (Adobe Experience Manager), ainsi que des suggestions pour les résoudre.

>[!NOTE]
>
>Si vous rencontrez des problèmes liés à l’instance de création AEM, reportez-vous à la section [Résolution des problèmes pour les auteurs.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter la liste des [problèmes connus](/help/release-notes/release-notes.md) relatifs à votre instance (packs de version et de services).

## Scénarios de dépannage pour l’administration {#troubleshooting-scenarios-for-administrators}

Le tableau suivant présente une vue d’ensemble des problèmes que l’administration peut résoudre :

<table>
 <tbody>
  <tr>
   <td><strong>Rôle</strong></td>
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

Consultez la section [Problèmes d’installation courants](/help/sites-deploying/troubleshooting.md#common-installation-issues) pour obtenir plus d’informations sur les scénarios de dépannage suivants :

* Lorsque vous double-cliquez sur le fichier Quickstart jar, rien ne se produit ou le fichier s’ouvre dans un autre programme (tel que le gestionnaire d’archives).
* Les applications s’exécutant sur CRX renvoient des erreurs de mémoire insuffisante.
* Après avoir double-cliqué sur Quickstart AEM, l’écran d’accueil d’AEM ne s’affiche pas dans le navigateur.

## Méthodes pour dépanner les analyses {#methods-for-troubleshooting-analysis}

### Créer une image mémoire des threads {#making-a-thread-dump}

L’image mémoire des threads consiste en une liste de toutes les unités d’exécution Java™ actuellement actives. Si AEM ne répond pas correctement, l’image mémoire des threads peut vous aider à identifier les blocages ou d’autres problèmes.

### Utiliser Sling Thread Dumper {#using-sling-thread-dumper}

1. Ouvrez la **console web AEM**, par exemple, à l’adresse `https://localhost:4502/system/console/`.
1. Sélectionnez les **threads** dans l’onglet **Statut**.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utiliser jstack (ligne de commande) {#using-jstack-command-line}

1. Recherchez le PID (ID de processus) de l’instance Java™ AEM.

   Vous pouvez, par exemple, utiliser `ps -ef` ou `jps`.

1. Exécutez :

   `jstack <pid>`

1. Permet d’afficher l’image mémoire des threads.

>[!NOTE]
>
>Vous pouvez ajouter les images mémoire des threads à un fichier journal en utilisant la redirection de sortie `>>` :
>
>`jstack <pid> >> /path/to/logfile.log`

Pour plus d’informations, consultez la section [Comment utiliser les images mémoire des threads d’une machine virtuelle Java (JVM)](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html).

### Contrôle des sessions JCR non fermées {#checking-for-unclosed-jcr-sessions}

Lorsque la fonctionnalité est développée pour AEM WCM, il est possible d’ouvrir des sessions JCR (cela s’apparente à l’ouverture d’une connexion de base de données). Si les sessions ouvertes ne sont jamais fermées, votre système peut présenter les symptômes suivants :

* Le système devient plus lent.
* Vous constatez qu’il y a de nombreuses entrées CacheManager: resizeAll dans le fichier journal. Le nombre (size=&lt;x>) ci-dessous affiche le nombre de caches. Chaque session ouvre plusieurs caches.
* Parfois, la mémoire du système est saturée (après quelques heures, jours ou semaines, selon la gravité).

Pour analyser les sessions non fermées et déterminer le code qui ne ferme pas une session, consultez l’article de la base de connaissances [Analyser les sessions non fermées](https://helpx.adobe.com/fr/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Utiliser la console web Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Le statut des lots OSGi peut également être un signe précurseur de problèmes potentiels.

1. Ouvez la **console web AEM**, par exemple, à l’adresse `https://localhost:4502/system/console/`.
1. Sélectionnez **Lots** dans l’onglet **OSGI**.
1. Vérifier :

   * le statut des lots. Si le statut est Inactif ou Non satisfait, essayez d’arrêter et de redémarrer le lot. Si le problème persiste, essayez une autre méthode.
   * Si l’un des lots possède des dépendances manquantes. Ces détails sont visibles en cliquant sur le nom du lot, qui consiste en un lien (l’exemple suivant ne présente aucun problème) :

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
