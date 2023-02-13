---
title: Configuration des applications AEM
seo-title: Configuring for AEM Apps
description: Apprenez à configurer Applications AEM.
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '141'
ht-degree: 100%

---

# Configuration des applications AEM{#configuring-for-aem-apps}

Adobe Experience Manager Apps offre la possibilité de mettre à jour le contenu de votre application par les airs (OTA, Over The Air). Le contenu mis à jour est stocké sur l’instance de publication. Pour permettre à l’application sur votre appareil de se connecter à l’instance de publication et de rechercher les mises à jour, l’instance de publication doit être configurée pour autoriser un en-tête de référent vide.

## Configuration d’un en-tête de référent vide {#configuring-empty-referrer-header}

Pour configurer le service de filtrage de référent, procédez comme suit :

* Ouvrez la console Apache Felix (**Configurations**) dans :
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Connectez-vous en tant qu’administrateur.
* Dans le menu **Configurations**, sélectionnez : *Apache Sling Referrer Filter*
* Cochez le champ Autoriser vide pour autoriser les en-têtes vides/manquants.
* Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![chlimage_1-58](assets/chlimage_1-58a.png)

Pour plus de détails, consultez les sections [Paramètres de configuration OSGI](/help/sites-deploying/osgi-configuration-settings.md) et [Liste de contrôle de sécurité - Problèmes de Cross-Site Request Forgery](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).
