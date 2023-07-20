---
title: Intégrer à ExactTarget
description: Découvrez comment intégrer Adobe Experience Manager à ExactTarget.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 43%

---

# Intégrer à ExactTarget{#integrating-with-exacttarget}

L’intégration d’Adobe Experience Manager (AEM) à ExactTarget vous permet de gérer et d’envoyer des emails créés dans AEM par le biais d’ExactTarget. Il vous permet également d’utiliser les fonctionnalités de gestion des pistes d’ExactTarget au moyen d’AEM de formulaires sur les pages AEM.

L’intégration offre les fonctionnalités suivantes :

* La possibilité de créer des emails dans AEM et de les publier dans ExactTarget pour distribution.
* Possibilité de définir l’action d’un formulaire AEM pour créer un abonné ExactTarget.

Une fois ExactTarget configuré, vous pouvez publier des newsletters ou des courriers électroniques dans ExactTarget. Voir [Publication de newsletters sur un service de messagerie](/help/sites-authoring/personalization.md).

## Création d’une configuration ExactTarget {#creating-an-exacttarget-configuration}

Les configurations ExactTarget peuvent être ajoutées au moyen des services cloud ou des outils. Les deux méthodes sont décrites dans cette section.

### Configuration d’ExactTarget au moyen des services cloud {#configuring-exacttarget-via-cloudservices}

Pour créer une configuration ExactTarget en Cloud Services :

1. Sur la page d’accueil, cliquez sur **Services cloud**. (Ou accédez directement à `https://<hostname>:<port>/etc/cloudservices.html`).
1. Cliquez sur **ExactTarget**, puis sur **Configurer**. La fenêtre de configuration d’ExactTarget s’affiche.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Ajoutez un titre et, éventuellement, un nom, puis cliquez sur **Créer**. La fenêtre de configuration **Paramètres ExactTarget** s’affiche.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Saisissez le nom d’utilisateur et le mot de passe, puis sélectionnez un point de fin API (par exemple, **https://webservice.exacttarget.com/Service.asmx**).
1. Cliquez sur **Connectez-vous à ExactTarget.** Une fois que vous êtes connecté, une boîte de dialogue de réussite s’affiche. box Click **OK** pour quitter la fenêtre.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Sélectionnez un compte, le cas échéant. Le compte est destiné aux clients Enterprise 2.0. Cliquez sur **OK**.

   ExactTarget a été configuré. Si vous souhaitez modifier la configuration, cliquez sur **Modifier**. Pour accéder à ExactTarget, cliquez sur **Accéder à ExactTarget**.

1. AEM propose désormais la fonctionnalité Extension de données. Celle-ci permet d’importer des colonnes d’extensions de données ExactTarget. Il peut être configuré en cliquant sur le signe &quot;+&quot; en regard de la configuration ExactTarget créée. Vous pouvez sélectionner l’une des extensions de données existantes dans la liste déroulante. Pour plus d’informations sur la configuration des extensions de données, voir [Documentation d’ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   Les colonnes d’extension de données importées peuvent être utilisées ultérieurement par le biais de la variable **Texte et personnalisation** composant.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuration d’ExactTarget au moyen des outils {#configuring-exacttarget-via-tools}

Pour créer une configuration ExactTarget dans les outils :

1. Sur la page d’accueil, cliquez sur **Outils**. Ou accédez-y directement en accédant à `https://<hostname>:<port>/misadmin#/etc`.
1. Sélectionnez **Outils**, **Configuration des Services cloud**, puis **ExactTarget**.
1. Cliquez sur **Nouveau** pour ouvrir la fenêtre **Créer une page**.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Saisissez le **Titre** et éventuellement la variable **Nom**, puis cliquez sur **Créer**.
1. Saisissez les informations de configuration conformément à l’étape 4 de la procédure précédente. Suivez cette procédure pour terminer la configuration d’ExactTarget.

### Ajouter plusieurs configurations {#adding-multiple-configurations}

Pour ajouter plusieurs configurations :

1. Sur la page d’accueil, cliquez sur **Services cloud** puis sur **ExactTarget**. Cliquez sur **Afficher les configurations** qui s’affiche si une ou plusieurs configurations ExactTarget sont disponibles. Toutes les configurations disponibles sont répertoriées.
1. Cliquez sur le lien **+** en regard de Configurations disponibles. Cette action ouvre la fenêtre **Créer une configuration**. Suivez la procédure de configuration précédente pour créer une configuration.
