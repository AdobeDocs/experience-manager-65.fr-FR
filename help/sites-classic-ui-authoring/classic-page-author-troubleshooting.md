---
title: Résolution des problèmes d’AEM lors de la création
seo-title: Résolution des problèmes d’AEM lors de la création
description: La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.
seo-description: La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 91%

---


# Résolution des problèmes d’AEM lors de la création{#troubleshooting-aem-when-authoring}

La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter les [problèmes connus](/help/release-notes/known-issues.md) relatifs à votre instance (packs de version et service packs).

>[!NOTE]
>
>Les utilisateurs disposant de privilèges administrateur désireux de résoudre les problèmes affectant AEM peuvent utiliser les méthodes de dépannage décrites à la section [Dépannage d’AEM (pour les administrateurs)](/help/sites-administering/troubleshoot.md). Si vous ne possédez pas les privilèges d’accès suffisants, contactez votre administrateur système au sujet du dépannage d’AEM.

## Ancienne version de la page toujours visible sur le site de publication {#old-page-version-still-on-published-site}

* **Problème** :

   * Vous avez modifié une page et l’avez répliquée sur le site de publication, mais l’*ancienne* version de la page est toujours visible sur le site de publication.

* **Raison**:

   * Les raisons peuvent être multiples, mais sont généralement liées à la mémoire cache (de votre navigateur local ou du dispatcher), bien qu’il s’agisse parfois d’un problème de la file d’attente de réplication.

* **Solutions**:

   * Plusieurs solutions sont possibles :
   * Vérifiez que la page a bien été répliquée. Vérifiez l’état de la page et, si nécessaire, l’état de la file d’attente de réplication.
   * Effacez la mémoire cache du navigateur local et accédez de nouveau à votre page.
   * Ajoutez `?` à la fin de l’URL de la page. Par exemple :

      `http://localhost:4502/sites.html/content?`

      Ceci demandera la page directement auprès d’AEM et contournera le dispatcher. Si vous recevez la page mise à jour, ceci indique que vous devez vider la mémoire cache du dispatcher.

   * Contactez l’administrateur du système en cas de problèmes avec les files d’attente de réplication.

## Sidekick non visible {#sidekick-not-visible}

* **Problème** :

   * Le sidekick n’est pas visible lors de la modification d’une page de contenu dans l’environnement de création.

* **Raison**:

   * Dans de rares cas, il se peut que vous ayez positionné l’en-tête de votre sidekick en dehors de votre fenêtre active. Ceci signifie que vous ne pouvez pas le repositionner.

* **Solution**:

   * Fermez votre session en cours et rouvrez-la. Le sidekick revient à sa position par défaut.

## Rechercher et remplacer - Toutes les instances ne sont pas remplacées {#find-replace-not-all-instances-are-replaced}

* **Problème:**

   * When using the **Find &amp; Replace** option it can happen that not all instances of the `find` term are replaced on a page.

* **Raison**:

   * The capability of **Find &amp; Replace** depends on how the content is saved, and whether it can be searched upon. Par exemple, un texte de blog est stocké dans la propriété `jcr:text`, qui n’est pas configurée pour faire l’objet de recherches. L’étendue par défaut du servlet de recherche et de remplacement couvre les propriétés suivantes :

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solution**:

   * Ces définitions peuvent être modifiées dans la configuration du **servlet Day CQ WCM Find Replace** à l’aide de la **console Web**, par exemple à l’adresse

      `http://localhost:4502/system/console/configMgr`

