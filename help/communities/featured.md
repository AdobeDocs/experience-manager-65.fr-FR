---
title: Fonction de contenu proposé
seo-title: Fonction de contenu proposé
description: La fonction Contenu proposé permet aux visiteurs de site connectés de mettre en évidence le contenu.
seo-description: La fonction Contenu proposé permet aux visiteurs de site connectés de mettre en évidence le contenu.
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: cbb5a6bac5e9932fd36abf20d4424890080d39bf
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 10%

---


# Fonction de contenu proposé {#featured-content-feature}

## Présentation {#introduction}

La fonctionnalité de contenu incitatif fournit une zone pour les visiteurs du site connectés (membres de la communauté) dans l’environnement de publication afin de mettre en évidence le contenu pour :

* [Blogs](blog-feature.md)
* [Calendriers](calendar.md)
* [Forums](forum.md)
* [Idées](ideation-feature.md)
* [Q&amp;R](working-with-qna.md)

Une fois que le contenu est marqué comme étant présenté, il sera répertorié dans ce composant, qui peut être placé dans des landings page ou des zones spécifiques qui attirent facilement l&#39;attention des membres de la communauté.

La fonctionnalité de contenu peut être autorisée ou non par composant.

Cette section de la documentation décrit:

* Ajouter du contenu incitatif à un site communautaire.
* Configuration settings for the `Featured Content` component.

## Ajouter du contenu proposé sur une page {#adding-featured-content-to-a-page}

To add a `Featured Content` component to a page in author mode, use the component browser to locate

* `Communities / Featured Content`

et faites-le glisser sur une page où le contenu présenté doit apparaître.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-featured.md#essentials-for-client-side) are included, this is how the `Featured Content` component will appear:

![chlimage_1-13](assets/chlimage_1-13.png)

## Configuration du contenu proposé {#configuring-featured-content}

Select the placed `Featured Content` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-14](assets/chlimage_1-14.png)

![chlimage_1-15](assets/chlimage_1-15.png)

### Onglet Settings {#settings-tab}

Sous l’onglet **[!UICONTROL Paramètres]** , identifiez le contenu à inclure :

* **[!UICONTROL Nom d’affichage]**

   Titre de la liste du contenu incitatif. For example `Featured Questions` or `Featured Ideas`. La valeur par défaut est `Featured Content` laissée vide.

* **[!UICONTROL Emplacement du contenu proposé]**

   *(Obligatoire)* Accédez à la page contenant le contenu qui peut être une fonctionnalité (les composants de cette page doivent être configurés pour autoriser le contenu proposé). Par exemple, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite d’affichage]**

   Nombre maximal de contenu incitatif à afficher. La valeur par défaut est 5.

## Expérience des visiteurs {#site-visitor-experience}

La possibilité de marquer le contenu comme contenu phare nécessite des privilèges de modérateur.

Lorsqu’un modérateur vue du contenu publié, il a accès aux indicateurs de modération contextuels, qui comprennent le nouvel `Feature` indicateur.

![chlimage_1-16](assets/chlimage_1-16.png)

Une fois marquée comme fonction, l’indicateur de modération devient `Unfeature`.

La page contenant le `Featured Content` composant inclut désormais cette publication.

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` est un lien vers la publication active.

## Informations supplémentaires {#additional-information}

More information may be found on the [Featured Content](essentials-featured.md) page for developers.

Pour marquer le contenu comme proposé, voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.
