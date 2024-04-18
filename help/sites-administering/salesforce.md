---
title: Intégration à Salesforce
description: Découvrez comment intégrer Adobe Experience Manager (AEM) à Salesforce.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 100%

---


# Intégration à Salesforce {#integrating-with-salesforce}

L’intégration de Salesforce à Adobe Experience Manager (AEM) fournit des fonctions de gestion de prospect et exploite les fonctions existantes prêtes à l’emploi de Salesforce. Vous pouvez configurer AEM pour publier des prospects sur Salesforce et créer des composants qui accèdent directement aux données à partir de Salesforce.

L’intégration bidirectionnelle et extensible entre AEM et Salesforce permet :

* Aux organisations d’utiliser et de modifier entièrement les données pour améliorer l’expérience client.
* Une participation des équipes marketing aux activités de vente.
* Aux organisations de transmettre et de recevoir automatiquement des données d’un magasin de données Salesforce.

Ce document répond aux questions suivantes :

* Comment configurer des services Cloud Salesforce (configuration de l’intégration AEM à Salesforce).
* Comment utiliser des informations de prospect/de contact Salesforce dans le contexte client et pour la personnalisation.
* Comment utiliser le modèle de workflow Salesforce pour publier des utilisateurs et utilisatrices AEM en tant que prospects dans Salesforce.
* Comment créer un composant qui affiche des données issues de Salesforce.

## Configuration de l’intégration AEM à Salesforce {#configuring-aem-to-integrate-with-salesforce}

Pour configurer l’intégration AEM à Salesforce, vous devez d’abord configurer une application d’accès à distance dans Salesforce. Ensuite, vous configurez le service cloud Salesforce pour qu’il soit dirigé vers cette application d’accès à distance.

>[!NOTE]
>
>Vous pouvez créer un compte développeur gratuit dans Salesforce.

Pour configurer l’intégration d’AEM à Salesforce :

>[!CAUTION]
>
>Vous devez installer le package d’intégration de [l’API Salesforce Force](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) pour pouvoir poursuivre la procédure. Pour plus d’informations sur l’utilisation des packages, consultez la page [Utilisation des packages](/help/sites-administering/package-manager.md#package-share)

1. Dans AEM, accédez à **Services cloud**. Dans Services tiers, cliquez sur **Configurer maintenant** dans **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Créez une configuration, par exemple : **développeur**.

   >[!NOTE]
   >
   >La nouvelle configuration redirige vers une nouvelle page : **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Il s’agit exactement de la valeur que vous devez spécifier dans l’adresse URL de rappel lors de la création de l’application d’accès à distance dans Salesforce. Ces valeurs doivent correspondre.

1. Connectez-vous à votre compte Salesforce (ou si vous n’en avez pas, créez-en un, à l’adresse [https://developer.force.com](https://developer.salesforce.com)).
1. Dans Salesforce, sélectionnez **Créer** > **Applications** pour accéder à **Applications connectées** (dans les anciennes versions de Salesforce, le workflow est **Déployer** > **Accès à distance**).
1. Cliquez sur **Nouveau** pour pouvoir connecter AEM à Salesforce.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Saisissez le **nom de l’application connectée**, le **nom de l’API** et l’**adresse électronique de contact**. Cochez la case **Activer les paramètres OAuth**, saisissez l’**adresse URL de rappel** et ajoutez une portée OAuth (accès intégral, par exemple). L’adresse URL de rappel se présente comme suit : `http://localhost:4502/etc/cloudservices/salesforce/developer.html`.

   Modifiez le nom et le numéro de port du serveur et le nom de la page correspondant à votre configuration.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Cliquez sur **Enregistrer** pour enregistrer la configuration Salesforce. Salesforce crée une **clé du client** et un **secret du client**, dont vous avez besoin pour la configuration d’AEM.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Patientez plusieurs minutes (jusqu’à 15 minutes) le temps que l’application d’accès à distance dans Salesforce s’active.

1. Dans AEM, accédez à **Services cloud** et à la configuration de Salesforce que vous avez créée précédemment (par exemple, **développeur**). Cliquez sur **Modifier** et saisissez la clé du client et le secret client à partir de salesforce.com.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | URL de connexion | Il s’agit du point d’entrée d’autorisation Salesforce. Sa valeur est prérenseignée et convient dans la plupart des cas. |
   |---|---|
   | Clé du client | Saisissez la valeur obtenue à partir de la page Enregistrement de l’application d’accès à distance sur salesforce.com. |
   | Secret du client | Saisissez la valeur obtenue à partir de la page Enregistrement de l’application d’accès à distance sur salesforce.com. |

1. Cliquez sur **Connexion à Salesforce** pour vous connecter. Salesforce vous demande d’autoriser votre configuration à vous connecter à Salesforce.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   Dans AEM, une boîte de dialogue de confirmation s’affiche pour confirmer que vous êtes bien connecté.

1. Accédez à la page principale de votre site web et cliquez sur **Propriétés de la page**. Ensuite, sélectionnez **Services cloud**, ajoutez **Salesforce** et sélectionnez la configuration appropriée (par exemple, **développeur**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   Vous pouvez maintenant utiliser le modèle de workflow pour publier des prospects sur Salesforce et créer des composants qui accèdent aux données de Salesforce.

## Export des utilisateurs et utilisatrices AEM en tant que prospects Salesforce {#exporting-aem-users-as-salesforce-leads}

Si vous souhaitez exporter un utilisateur ou une utilisatrice AEM en tant que prospect Salesforce, configurez le workflow pour publier des prospects vers Salesforce.

Pour exporter des utilisateurs et utilisatrices AEM en tant que prospects Salesforce, procédez comme suit :

1. Accédez au workflow Salesforce à l’adresse `http://localhost:4502/workflow` en cliquant avec le bouton droit sur le workflow **Exportation de Salesforce.com** et en cliquant sur **Démarrer**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Sélectionnez l’utilisateur ou l’utilisatrice AEM à créer en tant que prospect comme **Payload** de ce workflow (accueil > utilisateurs). Veillez à sélectionner le nœud de profil de l’utilisateur ou de l’utilisatrice, car il contient des informations telles que **Prénom**, et  **NomDeFamille**, qui sont mappées aux champs Salesforce **Prénom** et **NomDeFamille**.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Avant de lancer ce workflow, le nœud de prospect dans AEM doit comporter certains champs obligatoires avant d’être publié dans Salesforce. Ces champs sont **Prénom**, **NomDeFamille**, **Entreprise** et **E-mail**. Pour afficher la liste complète des correspondances entre un utilisateur ou une utilisatrice AEM et un prospect Salesforce, consultez la section [Configuration du mappage entre un utilisateur AEM et un prospect Salesforce](#mapping-configuration-between-aem-user-and-salesforce-lead).

1. Cliquez sur **OK**. Les informations de l’utilisateur sont exportées vers salesforce.com. Vous pouvez le vérifier à l’adresse salesforce.com.

   >[!NOTE]
   >
   >Les journaux d’erreurs indiquent si un prospect est importé. Pour plus d’informations, consultez le journal d’erreur.

### Configuration du workflow d’export Salesforce.com {#configuring-the-salesforce-com-export-workflow}

Si nécessaire, configurez le workflow d’export Salesforce.com pour qu’il corresponde à la bonne configuration sur Salesforce.com, ou pour apporter d’autres modifications.

Pour configurer le workflow d’export Salesforce.com :

1. Accédez à `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`.

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Ouvrez l’étape d’exportation de salesforce.com, sélectionnez l’onglet **Arguments**, sélectionnez la configuration appropriée et cliquez sur **OK**. De plus, si vous souhaitez que le workflow recrée un prospect supprimé dans Salesforce, cochez cette case.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### Configuration du mappage entre un utilisateur AEM et un prospect Salesforce {#mapping-configuration-between-aem-user-and-salesforce-lead}

Pour afficher ou modifier la configuration des correspondances actuelle entre un utilisateur AEM et un prospect Salesforce, ouvrez le gestionnaire de configuration :`https://<hostname>:<port>/system/console/configMgr` et cherchez **Configuration des correspondances d’un prospect Salesforce**.

1. Ouvrez le gestionnaire de configuration en cliquant sur **Console web** ou en accédant directement à `https://<hostname>:<port>/system/console/configMgr.`.
1. Cherchez **Configuration du mappage d’un prospect Salesforce**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Modifiez les correspondances, au besoin. La correspondance par défaut suit le modèle **aemUserAttribute=sfLeadAttribute**. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Configuration du magasin de contexte client Salesforce {#configuring-salesforce-client-context-store}

Le magasin de contexte client Salesforce affiche des informations sur la personne actuellement connectée, qui complètent les informations déjà disponibles dans AEM. Il extrait ces informations supplémentaires de Salesforce en fonction de la connexion de l’utilisateur ou de l’utilisatrice à Salesforce.

Pour effectuer cette opération, configurez les éléments suivants :

1. Liez un utilisateur ou une utilisatrice AEM à un identifiant Salesforce via le composant Salesforce Connect.
1. Ajoutez les données de profil Salesforce dans la page de contexte client afin de définir les propriétés que vous souhaitez afficher.
1. (Facultatif) Créez un segment qui utilise les données du magasin de contexte client Salesforce. 

### Liaison d’un utilisateur ou d’une utilisatrice AEM à un identifiant Salesforce {#linking-an-aem-user-with-a-salesforce-id}

Mappez un utilisateur ou une utilisatrice AEM à un identifiant Salesforce afin de les charger dans le contexte client. Dans un scénario réel, vous effectueriez la liaison en fonction des données connues de l’utilisateur ou de l’utilisatrice avec la validation. À des fins de démonstration, dans cette procédure, vous utilisez le composant **Salesforce Connect**.

1. Accédez à un site web dans AEM, connectez-vous, puis glissez et déposez le composant **Salesforce Connect** depuis le Sidekick.

   >[!NOTE]
   >
   >Si le composant **Salesforce Connect** n’est pas disponible, accédez au mode **Conception** et sélectionnez-le pour le rendre disponible dans le mode **Édition**.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   Lorsque vous faites glisser le composant vers la page, il affiche **Lien vers Salesforce=Désactivé**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >Ce composant n’est fourni qu’à titre de démonstration. Dans le cas de scénarios réels, il existe une autre méthode pour lier/associer des utilisateurs et utilisatrices à des prospects.

1. Après avoir fait glisser le composant dans la page, ouvrez-le pour le configurer. Sélectionnez la configuration, le type de contact et le prospect ou le contact Salesforce, puis cliquez sur **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM lie l’utilisateur au contact ou au prospect Salesforce.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Ajout de données Salesforce au contexte client {#adding-salesforce-data-to-client-context}

Vous pouvez charger des données utilisateur dans le contexte client à partir de Salesforce à des fins de personnalisation :

1. Ouvrez le contexte client que vous souhaitez étendre en y accédant, par exemple, `http://localhost:4502/etc/clientcontext/default/content.html.`.

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. Faites glisser le composant **Données du profil Salesforce** vers le contexte du client.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. Ouvrez le composant en double-cliquant dessus. Sélectionnez **Ajouter un élément** et sélectionnez une propriété dans la liste déroulante. Ajoutez autant de propriétés que vous le souhaitez et sélectionnez **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. À présent, les propriétés spécifiques à Salesforce s’affichent dans le contexte client.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Création d’un segment à l’aide des données du magasin de contexte client Salesforce {#building-a-segment-using-data-from-salesforce-client-context-store}

Vous pouvez créer un segment qui utilise les données de l’entrepôt de contexte client Salesforce. Pour ce faire :

1. Accédez à la segmentation dans AEM en sélectionnant **Outils** > **Segmentation** ou en consultant [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Créez ou mettez à jour un segment pour inclure des données de Salesforce. Pour plus d’informations, reportez-vous à [Segmentation](/help/sites-administering/campaign-segmentation.md).

## Recherche de prospects {#searching-leads}

AEM est fourni avec un exemple de composant Recherche, qui cherche des prospects dans Salesforce en fonction des critères déterminés. Ce composant vous montre comment utiliser l’API REST Salesforce pour rechercher des objets Salesforce. Pour déclencher un appel vers salesforce.com, liez une page avec une configuration Salesforce.

>[!NOTE]
>
>Voici un exemple de composant, qui montre comment utiliser l’API REST Salesforce pour créer une requête portant sur des objets Salesforce. Utilisez-le comme exemple pour créer des composants plus complexes en fonction de vos besoins.

Pour utiliser ce composant :

1. Accédez à la page dans laquelle vous souhaitez utiliser cette configuration. Ouvrez les propriétés de la page et sélectionnez **Services Cloud.** Cliquez sur **Ajouter des services**, sélectionnez **Salesforce** et la configuration appropriée, puis cliquez sur **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Faites glisser le composant Recherche de Salesforce vers la page (sous réserver qu’elle a été activée. Pour l’activer, accédez au mode Conception et ajoutez-le à la zone appropriée.

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. Ouvrez le composant Recherche, spécifiez les paramètres de recherche et cliquez sur **OK**.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM affiche les prospects spécifiés dans votre composant Recherche correspondant aux critères spécifiés.

   ![chlimage_1-87](assets/chlimage_1-87.png)
