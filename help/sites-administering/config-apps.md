---
title: Configuration d’Applications AEM
seo-title: Configuration d’Applications AEM
description: Apprenez à configurer Applications AEM.
seo-description: Apprenez à configurer Applications AEM.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 60%

---


# Configuration d’Applications AEM{#configuring-for-aem-apps}

Adobe Experience Manager Apps offre la possibilité de mettre à jour le contenu de votre application par les airs (OTA, Over The Air). Le contenu mis à jour est stocké sur l’instance de publication. Pour permettre à l’application sur votre appareil de se connecter à l’instance de publication et de rechercher les mises à jour, l’instance de publication doit être configurée pour autoriser un en-tête de référent vide.

## Configuration d’un en-tête de référent vide {#configuring-empty-referrer-header}

Pour configurer le service de filtrage de référent :

* Ouvrez la console Apache Felix (**Configurations**) à l’adresse :
* https://&lt;serveur>:&lt;numéro_port>/system/console/configMgr
* Connectez-vous en tant qu’administrateur.
* Dans le menu **Configurations**, sélectionnez : *Filtre de Parrain Apache Sling*
* Cochez le champ Autoriser les champs vides pour autoriser les en-têtes de parrain vides/manquants.
* Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![chlimage_1-58](assets/chlimage_1-58a.png)

Pour plus d&#39;informations, consultez les sections [Paramètres de configuration OSGI](/help/sites-deploying/osgi-configuration-settings.md) et [Liste de contrôle de sécurité - Problèmes liés à la falsification de requête sur plusieurs sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).
