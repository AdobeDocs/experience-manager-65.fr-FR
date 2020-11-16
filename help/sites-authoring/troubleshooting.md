---
title: Résolution des problèmes d’AEM lors de la création
seo-title: Résolution des problèmes d’AEM lors de la création
description: Problèmes pouvant survenir lors de l’utilisation d’AEM
seo-description: Problèmes pouvant survenir lors de l’utilisation d’AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%

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

      * `http://localhost:4502/sites.html/content?`
      * Ceci demandera la page directement auprès d’AEM et contournera le dispatcher. Si vous recevez la page mise à jour, ceci indique que vous devez vider la mémoire cache du dispatcher.
   * Contactez l’administrateur du système en cas de problèmes avec les files d’attente de réplication.


## Actions de composant non visibles dans la barre d’outils {#component-actions-not-visible-on-toolbar}

* **Problème** :

   * La plage entière des actions de composants applicables n’est pas visible lors de la modification d’une page de contenu dans l’environnement de création.

* **Raison**:

   * Dans de rares cas, une action précédente peut avoir un impact sur la barre d’outils.

* **Solution**:

   * Actualisez la page.

