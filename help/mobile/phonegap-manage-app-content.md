---
title: Création et gestion de contenu d’application
description: La gestion du contenu de l’application nécessite un effort collectif de la part des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, qui sont basées sur des modèles et des composants générés par les développeurs d’applications.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---

# Création et gestion de contenu d’application{#creating-and-managing-app-content}

{{ue-over-mobile}}

La gestion du contenu de l’application nécessite un effort collectif de la part des [développeurs](#developer), [auteurs](#author) et [administrateurs](#administrator). Les auteurs manipulent les pages, qui sont basées sur des modèles et des composants générés par les développeurs d’applications.

Enfin, les administrateurs publient stratégiquement le contenu de l’application mise à jour.

>[!NOTE]
>
>**Prérequis** :
>
>Dans [Déploiement et maintenance](/help/sites-deploying/deploy.md), les développeurs se sont familiarisés avec les composants système et les modèles dans Adobe Experience Manager (AEM).

## La Mosaïque Gérer Le Contenu De La Page {#the-manage-page-content-tile}

>[!CAUTION]
>
>Si vous n’utilisez pas de modèle d’application prêt à l’emploi, vous devez configurer un gestionnaire de synchronisation de contenu pour permettre la publication en direct de nouveau contenu d’application.
>
>Voir [Mobile avec synchronisation de contenu](/help/mobile/phonegap-contentsync.md) dans la section du développeur pour plus d’informations.

Ici, le contenu peut être créé, modifié et supprimé dans AEM Mobile de la même manière que dans AEM Sites.

La mosaïque **Gérer le contenu de la page** indique le nombre de pages de contenu géré et la date de dernière modification pour une payload particulière. Vous pouvez explorer le contenu pour créer, copier, déplacer, supprimer et mettre à jour des pages en cliquant sur chaque enregistrement de la mosaïque.

Une fois le contenu mis à jour, les administrateurs peuvent publier une payload de mise à jour de contenu en direct (OTA) pour les clients via la mosaïque **Gérer les packages de contenu**.

![chlimage_1-161](assets/chlimage_1-161.png)

Sélectionnez l’un des packages de contenu répertoriés pour créer ou modifier du contenu tel que la création, la modification ou la suppression de pages, la modification de la navigation et de l’ordre des pages, la création ou la mise à jour de contenu tel que la copie (texte) et le média.

Notez *tout est contenu*, ce qui signifie que les styles d’application, la copie (texte), les médias, les pages, la navigation et le ciblage du contenu peuvent tous être modifiés et mis à jour en direct, sans passer par une boutique d’applications.

Pour modifier le contenu d’AEM Mobile, les *auteurs AEM* auront besoin d’une bonne compréhension de l’interface d’édition du contenu d’AEM : [création de pages dans AEM.](/help/sites-authoring/qg-page-authoring.md)

## La Mosaïque Gérer Les Packages De Contenu {#the-manage-content-packages-tile}

Ici, les *administrateurs d’AEM* peuvent mettre à jour rapidement et facilement leurs applications pour offrir des expériences attrayantes et du contenu à jour afin de stimuler l’engagement de la marque et d’atteindre les objectifs commerciaux, le tout sans avoir besoin d’une nouvelle soumission de la part du développeur ou de l’App Store.

![chlimage_1-162](assets/chlimage_1-162.png)

Une fois que les *auteurs AEM* ont ajouté ou modifié du contenu via la mosaïque Gérer le contenu, les *administrateurs AEM* peuvent transmettre ces modifications aux clients avec une mise à jour des packages de contenu.

L’action Package de contenu permet à l’*auteur AEM* de créer et de modifier le contenu de la page pendant que l’équipe de développement apporte des modifications à la conception et à l’implémentation de l’application hôte, notamment la navigation, le style, la logique côté serveur, les modèles et les composants, puis de transmettre ces modifications en direct aux clients sans avoir à les soumettre à nouveau aux différents magasins pour distribution.

**Pour publier du contenu nouveau ou mis à jour**

Sélectionnez un package de contenu dans la mosaïque, dans cet exemple le package en anglais. Notez qu’une boîte de dialogue de mise à jour du contenu répertorie la configuration *Synchronisation du contenu* appropriée. Si le contenu de l&#39;application a été modifié depuis une mise à jour précédente, le statut s&#39;affiche *En attente*, comme illustré ci-dessous.

![chlimage_1-163](assets/chlimage_1-163.png)

Ensuite, sélectionnez l’action **Phase** en haut à droite pour créer la mise à jour du contenu. Ajoutez les informations de mise à jour appropriées et appuyez sur Terminé.

![chlimage_1-164](assets/chlimage_1-164.png)

Le gestionnaire *Synchronisation du contenu* crée ensuite les packages requis en formant un delta (un package de *uniquement* ce qui a changé). Une fois terminée, cette mise à jour du package de contenu a été effectuée, comme illustré ci-dessous.

L’évaluation d’une mise à jour de contenu permet d’effectuer plusieurs mises à jour avant de les publier sur OTA sur des appareils mobiles.

>[!NOTE]
>
>Le contenu intermédiaire peut être vérifié à l’aide de l’application AEM Verify avant publication.
>
>Voir [Démarrage rapide mobile pour AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) pour plus d’informations sur l’application AEM Verify.

![chlimage_1-165](assets/chlimage_1-165.png)

Lorsque vous êtes prêt à diffuser du nouveau contenu aux utilisateurs de votre application avec l’OTA de synchronisation de contenu, sélectionnez **Publish** comme illustré ci-dessous.

![chlimage_1-166](assets/chlimage_1-166.png)

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez appris à créer et gérer du contenu d’application dans le tableau de bord de l’application, consultez les ressources suivantes pour d’autres rôles de création :

* [La Mosaïque Gérer L’Application](/help/mobile/phonegap-app-details-tile.md)
* [Modification Des Métadonnées De L’Application](/help/mobile/phonegap-editmetadata.md)
* [Définitions d’application](/help/mobile/phonegap-app-definitions.md)
* [Création d’une application à l’aide de l’assistant Créer une application](/help/mobile/phonegap-create-new-app.md)
* [Importer une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
