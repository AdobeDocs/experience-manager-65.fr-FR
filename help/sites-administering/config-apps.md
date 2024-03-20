---
title: Configuration des applications AEM
description: Découvrez comment utiliser les applications Adobe Experience Manager pour mettre à jour le contenu de votre application OTA (en direct).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 47%

---

# Configuration des applications AEM{#configuring-for-aem-apps}

Les applications Adobe Experience Manager vous permettent de mettre à jour le contenu de votre application OTA (en direct). Le contenu mis à jour est stocké sur l’instance de publication. Pour permettre à l’application sur votre appareil de se connecter à l’instance de publication et de rechercher les mises à jour, l’instance de publication doit être configurée de manière à autoriser un en-tête de référent vide.

## Configuration de l’en-tête de référent vide {#configuring-empty-referrer-header}

Pour configurer le service de filtrage de référent, procédez comme suit :

* Ouvrez la console Apache Felix (**Configurations**) dans :
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Connectez-vous en tant qu’administrateur.
* Dans le menu **Configurations**, sélectionnez : *Apache Sling Referrer Filter*
* Cochez le champ Autoriser les en-têtes vides pour autoriser les en-têtes de référent vides/manquants.
* Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![chlimage_1-58](assets/chlimage_1-58a.png)

Pour plus de détails, consultez les sections [Paramètres de configuration OSGI](/help/sites-deploying/osgi-configuration-settings.md) et [Liste de contrôle de sécurité - Problèmes de Cross-Site Request Forgery](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).
