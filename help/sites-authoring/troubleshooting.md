---
title: Résolution des problèmes d’AEM lors de la création
seo-title: Troubleshooting AEM when Authoring
description: Problèmes pouvant survenir lors de l’utilisation d’AEM
seo-description: Some issues that you might encounter when using AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: ht
source-wordcount: '294'
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

      * `http://localhost:4502/sites.html/content?`
      * Ceci demandera la page directement auprès d’AEM et contournera le dispatcher. Si vous recevez la page mise à jour, ceci indique que vous devez vider la mémoire cache du dispatcher.
   * Contactez l’administrateur du système en cas de problèmes avec les files d’attente de réplication.


## Actions de composant non visibles dans la barre d’outils {#component-actions-not-visible-on-toolbar}

* **Problème** :

   * La plage entière des actions de composants applicables n’est pas visible lors de la modification d’une page de contenu dans l’environnement de création.

* **Raison** :

   * Dans de rares cas, une action précédente peut avoir un impact sur la barre d’outils.

* **Solution** :

   * Actualisez la page.
