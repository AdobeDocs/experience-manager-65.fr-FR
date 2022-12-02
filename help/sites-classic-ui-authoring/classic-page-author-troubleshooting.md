---
title: Résolution des problèmes d’AEM lors de la création
seo-title: Troubleshooting AEM when Authoring
description: La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.
seo-description: The following section covers some issues that you might encounter when using AEM, together with suggestions on how to troubleshoot them.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 100%

---

# Résolution des problèmes d’AEM lors de la création{#troubleshooting-aem-when-authoring}

La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter les [problèmes connus](/help/release-notes/release-notes.md) relatifs à votre instance (packs de version et service packs).

>[!NOTE]
>
>Les utilisateurs disposant de privilèges administrateur désireux de résoudre les problèmes affectant AEM peuvent utiliser les méthodes de dépannage décrites à la section [Dépannage d’AEM (pour les administrateurs)](/help/sites-administering/troubleshoot.md). Si vous ne possédez pas les privilèges d’accès suffisants, contactez votre administrateur système au sujet du dépannage d’AEM.

## Ancienne version de la page toujours visible sur le site de publication {#old-page-version-still-on-published-site}

* **Problème** :

   * Vous avez modifié une page et l’avez répliquée sur le site de publication, mais l’*ancienne* version de la page est toujours visible sur le site de publication.

* **Raison** :

   * Les raisons peuvent être multiples, mais sont généralement liées à la mémoire cache (de votre navigateur local ou du dispatcher), bien qu’il s’agisse parfois d’un problème de la file d’attente de réplication.

* **Solutions** :

   * Plusieurs solutions sont possibles :
   * Vérifiez que la page a bien été répliquée. Vérifiez le statut de la page et, si nécessaire, le statut de la file d’attente de réplication.
   * Effacez la mémoire cache du navigateur local et accédez de nouveau à votre page.
   * Ajoutez `?` à la fin de l’URL de la page. Par exemple :

      `http://localhost:4502/sites.html/content?`

      Ceci demandera la page directement auprès d’AEM et contournera le dispatcher. Si vous recevez la page mise à jour, ceci indique que vous devez vider la mémoire cache du dispatcher.

   * Contactez l’administrateur du système en cas de problèmes avec les files d’attente de réplication.

## Sidekick non visible {#sidekick-not-visible}

* **Problème** :

   * Le sidekick n’est pas visible lors de la modification d’une page de contenu dans l’environnement de création.

* **Raison** :

   * Dans de rares cas, il se peut que vous ayez positionné l’en-tête de votre sidekick en dehors de votre fenêtre active. Ceci signifie que vous ne pouvez pas le repositionner.

* **Solution** :

   * Fermez votre session en cours et rouvrez-la. Le sidekick revient à sa position par défaut.

## Rechercher et remplacer - Toutes les instances ne sont pas remplacées {#find-replace-not-all-instances-are-replaced}

* **Problème :**

   * Si vous utilisez l’option **Rechercher et remplacer**, il se peut que certaines instances du terme `find` ne soient pas remplacées sur une page.

* **Raison** :

   * Le fonctionnement de l’option **Rechercher et remplacer** dépend de la façon dont le contenu est enregistré et s’il peut faire l’objet de recherches. Par exemple, un texte de blog est stocké dans la propriété `jcr:text`, qui n’est pas configurée pour faire l’objet de recherches. L’étendue par défaut du servlet de recherche et de remplacement couvre les propriétés suivantes :

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solution** :

   * Ces définitions peuvent être modifiées dans la configuration du **servlet Rechercher et remplacer de la gestion de contenu Web Day CQ** à l’aide de la **console Web**, par exemple à l’adresse

      `http://localhost:4502/system/console/configMgr`
