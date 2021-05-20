---
title: Création et gestion de contenu d’application
seo-title: Création et gestion de contenu d’application
description: La gestion du contenu des applications nécessite un effort collectif des développeurs, des auteurs de contenu et des administrateurs.  Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications.
seo-description: La gestion du contenu des applications nécessite un effort collectif des développeurs, des auteurs de contenu et des administrateurs.  Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 7%

---

# Création et gestion du contenu de l’application{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La gestion du contenu de l’application nécessite un effort collectif des [développeurs](#developer), des [auteurs](#author) et [administrateurs](#administrator). Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications.

Enfin, les administrateurs publient stratégiquement le contenu de l’application mis à jour.

>[!NOTE]
>
>**Prérequis**:
>
>Dans [Déploiement et maintenance](/help/sites-deploying/deploy.md), les développeurs se sont familiarisés avec AEM système de composants et de modèles.

## Mosaïque Gérer le contenu de la page {#the-manage-page-content-tile}

>[!CAUTION]
>
>Si vous n’utilisez pas de modèle d’application prêt à l’emploi, vous devez configurer un gestionnaire de synchronisation de contenu pour permettre la publication du nouveau contenu de l’application.
>
>Pour plus d’informations, voir [Mobile with Content Sync](/help/mobile/phonegap-contentsync.md) dans la section destinée aux développeurs.

Ici, le contenu peut être créé, modifié et supprimé dans AEM Mobile de la même manière que dans AEM Sites.

La mosaïque **Gérer le contenu de page** affiche le nombre de pages de contenu géré et la dernière modification pour une charge utile particulière. Vous pouvez voir le détail du contenu pour créer, copier, déplacer, supprimer et mettre à jour des pages en cliquant sur chaque enregistrement de la mosaïque.

Une fois le contenu mis à jour, les administrateurs peuvent publier une payload de mise à jour de contenu en direct (OTA) pour les clients via la mosaïque **Gérer les packages de contenu.**

![chlimage_1-161](assets/chlimage_1-161.png)

Sélectionnez l’un des packages de contenu répertoriés pour créer ou modifier du contenu tel que la création, la modification ou la suppression de pages, la modification de la navigation et de l’ordre des pages, la création ou la mise à jour de contenu tel que la copie (texte) et le média.

Remarque *Tout est contenu*, ce qui signifie que les styles d’application, la copie (texte), le média, les pages, la navigation et le ciblage du contenu peuvent tous être modifiés et mis à jour OTA, sans avoir à se rendre dans une boutique d’applications.

Pour modifier le contenu AEM Mobile, *AEM auteurs *auront besoin d’une bonne compréhension de l’interface d’édition de contenu AEM : [Création de pages dans AEM.](/help/sites-authoring/qg-page-authoring.md)

## Mosaïque Gérer les packages de contenu {#the-manage-content-packages-tile}

Dans ce cas, *AEM les administrateurs* peuvent rapidement et facilement mettre à jour leurs applications pour offrir des expériences attrayantes et du contenu à jour afin de stimuler l’engagement de la marque et d’atteindre les objectifs de l’entreprise sans avoir à soumettre à nouveau un développeur ou une boutique d’applications.

![chlimage_1-162](assets/chlimage_1-162.png)

Une fois que *les auteurs AEM* ont ajouté ou modifié du contenu via la mosaïque Gérer le contenu, *AEM les administrateurs* peuvent envoyer ces modifications aux clients avec une mise à jour des packages de contenu.

L’action Package de contenu permet à l’*auteur AEM* de créer et de modifier le contenu de la page pendant que l’équipe de développement apporte des modifications à la conception et à l’implémentation d’une application hôte, y compris la navigation, le style, la logique côté serveur, les modèles et les composants, puis envoie ces modifications à des clients OTA sans avoir à soumettre à nouveau aux différents magasins pour distribution.

**Pour publier du contenu nouveau ou mis à jour**

Sélectionnez un module de contenu dans la mosaïque, dans cet exemple le module en anglais. Notez qu’une boîte de dialogue de mise à jour du contenu répertorie la configuration *Synchronisation du contenu* appropriée. Si le contenu de l’application a été modifié depuis une mise à jour précédente, l’état affiche *En attente*, comme illustré ci-dessous.

![chlimage_1-163](assets/chlimage_1-163.png)

Sélectionnez ensuite l’action **Stage** en haut à droite de la création de la mise à jour du contenu. Ajoutez les informations de mise à jour appropriées et appuyez sur Terminé.

![chlimage_1-164](assets/chlimage_1-164.png)

Le gestionnaire *Synchronisation du contenu* crée ensuite les modules requis en formant un delta (un module de *uniquement* ce qui a changé). Une fois terminé, ce module de contenu de mise à jour a été mis en scène comme illustré ci-dessous.

L’évaluation d’une mise à jour du contenu permet d’effectuer plusieurs mises à jour avant de les publier sur OTA sur des périphériques mobiles.

>[!NOTE]
>
>Le contenu intermédiaire peut être vérifié à l’aide de l’application AEM Vérifier avant publication.
>
>Voir [Démarrage rapide mobile pour AEM la vérification](/help/mobile/phonegap-mobile-quickstart.md) pour plus d’informations sur AEM vérification d’application.

![chlimage_1-165](assets/chlimage_1-165.png)

Lorsque vous êtes prêt à diffuser du nouveau contenu aux utilisateurs de votre application avec l’OTA de synchronisation de contenu, sélectionnez **Publier** comme illustré ci-dessous.

![chlimage_1-166](assets/chlimage_1-166.png)

### Étapes suivantes {#the-next-steps}

Une fois que vous avez appris à propos de la création et de la gestion du contenu de l’application dans le tableau de bord de l’application, consultez les ressources suivantes pour d’autres rôles de création :

* [Mosaïque Gestion de l’application](/help/mobile/phonegap-app-details-tile.md)
* [Modification de métadonnées d’application](/help/mobile/phonegap-editmetadata.md)
* [Définitions des applications](/help/mobile/phonegap-app-definitions.md)
* [Création d’une application à l’aide de l’assistant Créer une application](/help/mobile/phonegap-create-new-app.md)
* [Importation d’une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
