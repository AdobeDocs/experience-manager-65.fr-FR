---
title: Création d’une application AEM Mobile à l’aide de l’assistant de création
seo-title: Creating a new AEM Mobile app using create wizard
description: Les applications AEM Mobile sont basées sur un plan directeur qui définit une structure et des propriétés de page. Consultez cette page pour en savoir plus sur la création d’une application basée sur un modèle d’application.
seo-description: AEM Mobile apps are based on a blueprint that defines a page structure and properties. Follow this page to learn about how to create a new app based on an app template.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Création d’une application AEM Mobile à l’aide de l’assistant de création{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications AEM Mobile sont basées sur un plan directeur qui définit une structure et des propriétés de page. Vous pouvez configurer les propriétés de l’application suivantes :

* **Titre :** Titre de l’application.
* **Chemin de destination :** Emplacement dans le référentiel où l’application est stockée. Laissez la valeur par défaut pour créer un chemin d’accès en fonction du nom de l’application.

* **Nom :** La valeur par défaut est la valeur de la propriété Title avec les caractères d’espace supprimés. Le nom est utilisé dans AEM pour faire référence à l’application, par exemple pour le noeud de référentiel qui représente l’application.
* **Description :** Description de l’application.
* **URL du serveur :** URL qui fournit des mises à jour de contenu en vol (OTA) à l’application. La valeur par défaut est l’URL du serveur de publication de l’instance utilisée pour créer une application (provenant du service externalizer). Notez qu’il doit s’agir d’une instance de serveur de publication plutôt que d’un auteur, ce qui nécessite une authentification.

Vous pouvez également fournir un fichier image à utiliser comme miniature de l’application, sélectionner la configuration de PhoneGap Build à utiliser et sélectionner la configuration d’analyse de l’application mobile à utiliser. Cette image est utilisée uniquement comme miniature pour représenter votre application mobile dans la console des applications mobiles en Experience Manager.

Il existe des onglets supplémentaires (et facultatifs) pour créer le service cloud et intégrer le module SDK Mobile Services Adobe dans votre application.

* Build : Cliquez sur Gérer les configurations et configurez ici votre service de génération build build.phonegap.com. Ensuite, dans la liste déroulante, vous pourrez sélectionner le nouveau service cloud PhoneGap Build.
* Analytics : Cliquez sur Gérer les configurations et configurez vos [SDK Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) service cloud. Ensuite, dans la liste déroulante, vous pourrez sélectionner le service mobile nouvellement créé à intégrer à votre application mobile.

## Utilisation des modèles d’application {#using-app-templates}

Les modèles d’application offrent un moyen simple d’exploiter les conceptions existantes créées par les développeurs, utilisées pour créer de nouvelles applications dans AEM.

Qu’est-ce qu’un modèle d’application ? Considérez-le comme un ensemble de modèles de page et de composants qui représentent une ligne de base ou une base d’une application.
Lors de la création d’une application basée sur le modèle d’une autre application, vous obtenez une application dont le point de départ est représentatif de l’application à partir de laquelle elle a été créée.

Pour utiliser cette fonctionnalité, vous devez disposer d’un modèle d’application mobile (ou d’une application installée avec un modèle d’application).

Le dernier package d’exemples d’applications AEM comprend une version mise à jour de l’application Geometrixx avec un modèle d’application. Vous pouvez également installer le [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) qui fournit également un modèle.

Procédure de création d’une application basée sur un modèle d’application :

1. Accédez au catalogue d’applications AEM Mobile : &lt;*server-url*>aem/apps.html/content/mobileapps
1. Sélectionner **Créer** puis choisissez **Application** comme illustré ci-dessous

![chlimage_1-158](assets/chlimage_1-158.png)

Sélectionnez un modèle d’application mis à votre disposition par un développeur AEM. Voir [Structure d’une application AEM Mobile](/help/mobile/phonegap-structure-an-app.md) pour obtenir de l’aide sur les développeurs.

![chlimage_1-159](assets/chlimage_1-159.png)

Renseignez les détails de votre nouvelle application si nécessaire, y compris éventuellement la modification de son image miniature. Ces valeurs peuvent être modifiées ultérieurement à partir du **Gérer l’application** mosaïque.

![chlimage_1-160](assets/chlimage_1-160.png)

## Les étapes suivantes {#the-next-steps}

Consultez les ressources suivantes pour en savoir plus sur les autres rôles de création :

* [Mosaïque Gérer l’application](/help/mobile/phonegap-app-details-tile.md)
* [Modification des métadonnées d’application](/help/mobile/phonegap-editmetadata.md)
* [Définitions des applications](/help/mobile/phonegap-app-definitions.md)
* [Importation d’une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
