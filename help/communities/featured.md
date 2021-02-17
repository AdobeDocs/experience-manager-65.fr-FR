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
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 9%

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
* Paramètres de configuration du composant `Featured Content`.

## Ajouter du contenu proposé à une page {#adding-featured-content-to-a-page}

Pour ajouter un composant `Featured Content` à une page en mode création, utilisez l’explorateur de composants pour localiser

* `Communities / Featured Content`

et faites-le glisser sur une page où le contenu présenté doit apparaître.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](essentials-featured.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Featured Content` apparaîtra :

![featuredcontent](assets/featuredcontent.png)

## Configuration du contenu proposé {#configuring-featured-content}

Sélectionnez le composant `Featured Content` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Onglet Settings {#settings-tab}

Sous l&#39;onglet **[!UICONTROL Paramètres]**, identifiez le contenu à inclure :

* **[!UICONTROL Nom d’affichage]**

   Titre de la liste du contenu incitatif. Par exemple `Featured Questions` ou `Featured Ideas`. La valeur par défaut est `Featured Content` si elle est laissée vide.

* **[!UICONTROL Emplacement du contenu proposé]**

   *(Obligatoire)* Accédez à la page contenant le contenu qui peut être une fonctionnalité (les composants de cette page doivent être configurés pour autoriser le contenu proposé). Par exemple, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite d’affichage]**

   Nombre maximal de contenu incitatif à afficher. La valeur par défaut est 5.

## Expérience des visiteurs {#site-visitor-experience}

La possibilité de marquer le contenu comme contenu phare nécessite des privilèges de modérateur.

Lorsqu’un modérateur vue du contenu publié, il a accès aux indicateurs de modération contextuels, qui comprennent le nouvel indicateur `Feature`.

![site-visiteur-expérience](assets/site-visitor-experience.png)

Une fois marquée comme fonction, l&#39;indicateur de modération devient `Unfeature`.

La page contenant le composant `Featured Content` inclut désormais cette publication.

![site-visiteur-experience1](assets/site-visitor-experience1.png)

`Read More` est un lien vers la publication active.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Contenu phare](essentials-featured.md) à l&#39;intention des développeurs.

Pour marquer le contenu comme étant présenté, voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).
