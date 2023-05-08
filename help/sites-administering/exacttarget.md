---
title: Intégration à ExactTarget
seo-title: Integrating with ExactTarget
description: Découvrez comment intégrer AEM à ExactTarget.
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 59%

---

# Intégration à ExactTarget{#integrating-with-exacttarget}

L’intégration d’AEM à ExactTarget permet de gérer et d’envoyer un e-mail créé dans AEM par le biais d’ExactTarget. Cela permet également d’utiliser les fonctionnalités de gestion de prospect d’ExactTarget par le biais de formulaires AEM dans des pages AEM.

L’intégration offre les fonctionnalités suivantes :

* La possibilité de créer des emails dans AEM et de les publier dans ExactTarget pour distribution.
* Possibilité de définir l’action d’un formulaire AEM pour créer un abonné ExactTarget.

Une fois ExactTarget configuré, vous pouvez publier des newsletters ou des courriers électroniques dans ExactTarget. Voir [Publication de newsletters sur un service de messagerie](/help/sites-authoring/personalization.md).

## Création d’une configuration ExactTarget {#creating-an-exacttarget-configuration}

Il est possible d’ajouter des configurations ExactTarget par le biais d’outils ou de services cloud. Les deux méthodes sont décrites dans cette section.

### Configuration d’ExactTarget via Cloud Services {#configuring-exacttarget-via-cloudservices}

Pour créer une configuration ExactTarget en Cloud Services :

1. Sur la page d’accueil, cliquez sur **Services cloud**. (Ou accédez directement à `https://<hostname>:<port>/etc/cloudservices.html`).
1. Cliquez sur **ExactTarget**, puis sur **Configurer**. La fenêtre de configuration d’ExactTarget s’affiche.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Ajoutez un titre et, éventuellement, un nom, puis cliquez sur **Créer**. La fenêtre de configuration **Paramètres ExactTarget** s’affiche.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Saisissez le nom d’utilisateur et le mot de passe, puis sélectionnez un point de terminaison API (par exemple, **https://webservice.exacttarget.com/Service.asmx**).
1. Cliquez sur **Connectez-vous à ExactTarget.** Une boîte de dialogue s’affiche pour confirmer que vous êtes bien connecté. Cliquez sur **OK** pour fermer la fenêtre.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Sélectionnez un compte, le cas échéant. Le compte est destiné aux clients Enterprise 2.0. Cliquez sur **OK**.

   ExactTarget a été configuré. Si vous souhaitez modifier la configuration, cliquez sur **Modifier**. Pour accéder à ExactTarget, cliquez sur **Accéder à ExactTarget**.

1. AEM propose désormais la fonctionnalité Extension de données. Celle-ci permet d’importer des colonnes d’extensions de données ExactTarget. Il peut être configuré en cliquant sur le signe &quot;+&quot; en regard de la configuration ExactTarget créée. Vous pouvez sélectionner l’une des extensions de données existantes dans la liste déroulante. Pour plus d’informations sur la configuration des extensions de données, voir [Documentation d’ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   Les colonnes d’extension de données importées peuvent être utilisées ultérieurement par le biais de la variable **Texte et personnalisation** composant.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuration d’ExactTarget via les outils {#configuring-exacttarget-via-tools}

Pour créer une configuration ExactTarget dans les outils :

1. Sur la page d’accueil, cliquez sur **Outils**. Ou accédez-y directement en accédant à `https://<hostname>:<port>/misadmin#/etc`.
1. Sélectionnez **Outils**, **Configuration des Services cloud**, puis **ExactTarget**.
1. Cliquez sur **Nouveau** pour ouvrir la fenêtre **Créer une page**.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Saisissez le **Titre** et éventuellement la variable **Nom**, puis cliquez sur **Créer**.
1. Saisissez les informations de configuration conformément à l’étape 4 de la procédure précédente. Suivez cette procédure pour terminer la configuration d’ExactTarget.

### Ajout de plusieurs configurations {#adding-multiple-configurations}

Pour ajouter plusieurs configurations :

1. Sur la page d’accueil, cliquez sur **Services cloud** puis sur **ExactTarget**. Cliquez sur le bouton **Afficher les configurations** visible si une ou plusieurs configurations ExactTarget sont disponibles. Toutes les configurations disponibles sont répertoriées.
1. Cliquez sur le lien **+** en regard de Configurations disponibles. Cette action ouvre la fenêtre **Créer une configuration**. Suivez la procédure de configuration précédente pour créer une configuration.
