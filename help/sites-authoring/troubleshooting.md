---
title: Dépannage lors de la création dans AEM
description: Problèmes que vous pouvez rencontrer lors de l’utilisation d’AEM.
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '295'
ht-degree: 100%

---

# Résolution des problèmes d’AEM lors de la création{#troubleshooting-aem-when-authoring}

La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter les [problèmes connus](/help/release-notes/release-notes.md) relatifs à votre instance (packs de version et pack de services).

>[!NOTE]
>
>Les utilisateurs et utilisatrices disposant de droits d’administrateur et souhaitant résoudre les problèmes liés à AEM peuvent utiliser les méthodes de dépannage décrites dans la section [Dépannage dans AEM (pour les administrateurs et administratrices)](/help/sites-administering/troubleshoot.md). Si vous ne disposez pas des privilèges suffisants, contactez votre administrateur ou administratrice système pour en savoir plus sur le dépannage dans AEM.

## Ancienne version de la page toujours visible sur le site de publication {#old-page-version-still-on-published-site}

* **Problème** :

   * Vous avez réalisé des modifications sur une page et répliqué la page sur le site de publication, mais c’est toujours l’*ancienne* version de la page qui s’affiche sur le site de publication.

* **Raison** :

   * Cela peut être dû à plusieurs raisons, le plus souvent le cache (votre navigateur local ou le Dispatcher), bien que cela puisse parfois venir d’un problème avec la file d’attente de réplication.

* **Solutions** :

   * Il existe alors plusieurs possibilités :
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

   * Dans de rares cas, une action précédente peut avoir eu un impact sur la barre d’outils.

* **Solution** :

   * Actualisez la page.
