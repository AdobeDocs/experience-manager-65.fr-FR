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
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
* Dans le menu **Configurations**, sélectionnez : *Filtre de référent Apache Sling*
* Cochez le champ Autoriser vide pour autoriser les en-têtes de référent vides/manquants.
* Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![chlimage_1-58](assets/chlimage_1-58a.png)

Pour plus d’informations, voir [Paramètres de configuration OSGI](/help/sites-deploying/osgi-configuration-settings.md) et [Liste de contrôle de sécurité - Problèmes avec falsification de requête intersites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) .
