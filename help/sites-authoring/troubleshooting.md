---
title: Dépannage lors de la création dans AEM
description: Problèmes que vous pouvez rencontrer lors de l’utilisation d’AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 97%
---
# Résolution des problèmes d’AEM lors de la création{#troubleshooting-aem-when-authoring}

La section suivante traite de certains problèmes susceptibles d’être rencontrés lorsque vous utilisez AEM, ainsi que des suggestions pour résoudre ces problèmes.

>[!NOTE]
>
>Si vous rencontrez des problèmes, il est également intéressant de consulter les [problèmes connus](/help/release-notes/release-notes.md) relatifs à votre instance (packs de version et pack de services).

>[!NOTE]
>
>Les utilisateurs et utilisatrices disposant de droits d’administrateur et souhaitant résoudre les problèmes liés à AEM peuvent utiliser les méthodes de dépannage décrites dans la section [Dépannage dans AEM (pour les administrateurs et administratrices)](/help/sites-administering/troubleshoot.md). Si vous ne disposez pas des privilèges suffisants, veuillez contacter votre administrateur ou administratrice système pour en savoir plus sur le dépannage dans AEM.

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
