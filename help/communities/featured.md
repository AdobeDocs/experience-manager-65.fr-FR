---
title: Fonctionnalité Contenu proposé
description: La fonctionnalité Contenu mis en page permet aux visiteurs connectés du site de mettre en évidence le contenu.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 6%

---

# Fonctionnalité Contenu proposé {#featured-content-feature}

## Présentation {#introduction}

La fonctionnalité de contenu présenté fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement de publication afin de mettre en évidence le contenu pour :

* [Blogs](blog-feature.md)
* [Calendriers](calendar.md)
* [Forums](forum.md)
* [Idées](ideation-feature.md)
* [Q&amp;R](working-with-qna.md)

Une fois que le contenu est marqué comme présenté, il est répertorié dans ce composant, qui peut être placé dans des pages d’entrée spécifiques ou des zones qui attirent facilement l’attention des membres de la communauté.

La possibilité d’afficher du contenu peut être autorisée ou non par composant.

Cette section de la documentation décrit :

* Ajout de contenu présenté à un site communautaire.
* Paramètres de configuration de la variable `Featured Content` composant.

## Ajout de contenu proposé à une page {#adding-featured-content-to-a-page}

Pour ajouter une `Featured Content` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Featured Content`

Faites-le glisser sur une page où le contenu présenté doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](essentials-featured.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Featured Content` Le composant apparaît :

![featuredcontent](assets/featuredcontent.png)

## Configuration du contenu proposé {#configuring-featured-content}

Sélectionnez le `Featured Content` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Onglet Paramètres {#settings-tab}

Sous , **[!UICONTROL Paramètres]** , identifiez le contenu à afficher :

* **[!UICONTROL Nom d’affichage]**

  Titre de la liste du contenu présenté. Par exemple : `Featured Questions` ou `Featured Ideas`. Par défaut : `Featured Content` s’il est vide.

* **[!UICONTROL Emplacement du contenu proposé]**

  *(Obligatoire)* Accédez à la page contenant le contenu qui peut être présenté (les composants de cette page doivent être configurés sur Autoriser le contenu proposé). Par exemple, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite d’affichage]**

  Nombre maximal de contenus présentés à afficher. La valeur par défaut est 5.

## Expérience du visiteur du site {#site-visitor-experience}

La capacité à marquer le contenu comme contenu présenté nécessite des privilèges de modérateur.

Lorsqu’un modérateur affiche du contenu publié, il a accès aux indicateurs de modération contextuelle, qui incluent la nouvelle `Feature` Indicateur.

![site-visiteur-expérience](assets/site-visitor-experience.png)

Une fois qu’il est marqué comme fonction, l’indicateur de modération devient `Unfeature`.

La page contenant la variable `Featured Content` inclut désormais cette publication.

![site-visitor-experience1](assets/site-visitor-experience1.png)

La variable `Read More` liens vers la publication active.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Contenu en vedette](essentials-featured.md) pour les développeurs.

Pour marquer le contenu comme présenté, voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).
