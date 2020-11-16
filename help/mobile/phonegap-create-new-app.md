---
title: Création d’une application AEM Mobile à l’aide de l’assistant de création
seo-title: Création d’une application AEM Mobile à l’aide de l’assistant de création
description: Les applications AEM Mobile sont basées sur un modèle qui définit une structure de page et des propriétés. Suivez cette page pour en savoir plus sur la création d’une application à partir d’un modèle d’application.
seo-description: Les applications AEM Mobile sont basées sur un modèle qui définit une structure de page et des propriétés. Suivez cette page pour en savoir plus sur la création d’une application à partir d’un modèle d’application.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---


# Création d’une application AEM Mobile à l’aide de l’assistant de création{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications AEM Mobile sont basées sur un modèle qui définit une structure de page et des propriétés. Vous pouvez configurer les propriétés d’application suivantes :

* **Titre :** Titre de l’application.
* **Chemin de destination :** Emplacement dans le référentiel dans lequel l’application est stockée. Conservez la valeur par défaut pour créer un chemin d’accès en fonction du nom de l’application.

* **Nom :** La valeur par défaut est la valeur de la propriété Title (Titre) dont les caractères d’espace sont supprimés. Le nom est utilisé dans AEM pour faire référence à l’application, par exemple pour le noeud de référentiel qui représente l’application.
* **Description :** Description de l’application.
* **URL du serveur :** URL qui fournit du contenu en direct (OTA) mis à jour vers l’application. La valeur par défaut est l’URL du serveur de publication de l’instance utilisée pour créer une application (provenant du service externalizer). Remarque : il doit s’agir d’une instance de serveur de publication et non d’un auteur, ce qui nécessite une authentification.

Vous pouvez également fournir un fichier image à utiliser comme miniature de l’application, sélectionner la configuration de PhoneGap Build à utiliser et sélectionner la configuration d’analyse des applications mobiles à utiliser. Cette image est uniquement utilisée comme miniature pour représenter votre application mobile dans la console des applications mobiles en Experience Manager.

Il existe d’autres onglets (et facultatifs) pour créer un service cloud et intégrer le module Adobe Mobile Services SDK dans votre application.

* Créer : Cliquez ici pour gérer les configurations et configurer votre service de génération build.phonegap.com. Ensuite, à partir de la liste déroulante, vous pourrez sélectionner le nouveau service PhoneGap build cloud créé.
* Analytics : Cliquez sur Gérer les configurations et configurez votre service cloud SDK [Mobile Services](https://docs.adobe.com/content/help/en/mobile-services/using/home.html) Adobe. Ensuite, dans la liste déroulante, vous pourrez sélectionner le nouveau service mobile à intégrer à votre application mobile.

## Utilisation de modèles d’application {#using-app-templates}

Les modèles d’application offrent un moyen facile d’exploiter les conceptions existantes créées par les développeurs, utilisées pour la création de nouvelles applications dans AEM.

Qu’est-ce qu’un modèle d’application ? Considérez-le comme un ensemble de modèles de page et de composants qui représentent une base ou une base d’application.
Lors de la création d’une application basée sur le modèle d’une autre application, vous obtenez une application dont le point de départ est représentatif de l’application à partir de laquelle elle a été créée.

Vous devez disposer d’un modèle d’application mobile existant (ou d’une application installée avec un modèle d’application) pour pouvoir utiliser cette fonction.

Le dernier pack d’exemples d’applications AEM comprend une version mise à jour de l’application Geometrixx avec un modèle d’application. Vous pouvez également installer le [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) qui fournit également un modèle.

Procédure de création d’une application à partir d’un modèle d’application :

1. Accédez au catalogue de l’application AEM Mobile : &lt;*server-url*>aem/apps.html/content/mobileapps
1. Sélectionnez **Créer** , puis **App** comme illustré ci-dessous.

![chlimage_1-158](assets/chlimage_1-158.png)

Sélectionnez un modèle d’application mis à votre disposition par un développeur AEM. Voir [Structure d’une application](/help/mobile/phonegap-structure-an-app.md) AEM Mobile pour obtenir de l’aide aux développeurs.

![chlimage_1-159](assets/chlimage_1-159.png)

Renseignez les détails de votre nouvelle application si nécessaire, y compris la modification facultative de l’image miniature. Ces valeurs peuvent être modifiées ultérieurement à partir du volet **Gérer l’application** .

![chlimage_1-160](assets/chlimage_1-160.png)

## Étapes suivantes {#the-next-steps}

Consultez les ressources suivantes pour en savoir plus sur les autres rôles de création :

* [Mosaïque Gestion de l’application](/help/mobile/phonegap-app-details-tile.md)
* [Modification de métadonnées d’application](/help/mobile/phonegap-editmetadata.md)
* [Définitions d’application](/help/mobile/phonegap-app-definitions.md)
* [Importation d’une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développer pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
