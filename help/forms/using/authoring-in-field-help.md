---
title: Création d’une aide contextuelle pour les champs de formulaire
seo-title: Authoring in-context help for form fields
description: AEM Forms vous permet d’ajouter une aide contextuelle aux champs et aux panneaux de formulaires adaptatifs sous forme de texte ou de contenu multimédia enrichi, y compris des vidéos.
seo-description: AEM Forms lets you add in-context help to adaptive form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: Adaptive Forms
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 43%

---

# Création d’une aide contextuelle pour les champs de formulaire{#authoring-in-context-help-for-form-fields}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

## Présentation {#introduction}

Dans certains cas, les utilisateurs finaux qui remplissent un formulaire ne sont pas toujours sûrs des informations qu’ils doivent indiquer dans un champ spécifique. Pour résoudre ces problèmes, les formulaires adaptatifs prennent en charge l’ajout de texte ou d’une aide contextuelle enrichie à un champ de formulaire. Cela contribue à améliorer l’expérience de remplissage du formulaire et évite toute ambiguïté pour les utilisateurs finaux.

Cet article explique comment les auteurs de formulaires peuvent ajouter une aide contextuelle lors de la création d’un Forms adaptatif.

## Ajout d’une aide contextuelle {#add-in-context-help}

Vous pouvez spécifier une aide contextuelle à l’aide des options suivantes dans la section Contenu de l’aide de l’onglet Propriétés de la barre latérale.

* [Description courte](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Description longue](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Aide contextuelle pour les champs de formulaire](assets/descriptions.png)

>[!NOTE]
>
>La description longue remplace la description courte. Si vous avez spécifié les deux, seule la description longue s’affiche.

### Description courte {#short-description}

Le champ Description courte permet de fournir des conseils rapides et courts sur le remplissage d’un champ de formulaire. Le texte spécifié dans le champ Description courte s’affiche sous forme d’info-bulle lorsque vous placez le pointeur de la souris sur le champ.

![Description courte pour l’ajout d’une aide contextuelle pour des champs de formulaire](assets/tooltip.png)

>[!NOTE]
>
>Sélectionnez **Toujours afficher la description courte** pour afficher en permanence le texte de l’aide sous le champ.

![Aide contextuelle courte affichée en permanence sous le champ](assets/short1.png)

### Description longue {#long-description}

Vous pouvez utiliser le champ Description longue pour saisir un texte long ou incorporer du contenu multimédia enrichi, dont des vidéos, pour apporter une aide contextuelle. Par exemple, l’illustration ci-dessous montre comment incorporer une vidéo pour apporter une aide contextuelle.

![Ajout de contenu multimédia enrichi comme aide contextuelle pour les champs de formulaire](assets/long-descriptions.png)

L’ajout d’une description longue affiche une **?** en regard du champ. Cliquez sur l’icône pour afficher le contenu ajouté à la section Description longue.

![Exemple d’aide contextuelle sous forme de contenu multimédia enrichi](assets/photoshop.png)

### Aide au niveau d’un panneau {#panel-level-help}

Outre l’aide contextuelle pour les champs de formulaire, vous pouvez spécifier une aide au niveau d’un panneau sous l’onglet Contenu de l’aide du panneau Modifier.

![Ajout d’une aide contextuelle pour un panneau de formulaire](assets/panel-level-help.png)

L’ajout d’une aide pour le panneau affiche une **?** en regard de la description du panneau. Cliquez sur l’icône pour afficher le contenu ajouté à la section Contenu de l’aide de la boîte de dialogue de modification du panneau.

![Exemple d’aide contextuelle au niveau d’un panneau](assets/photoshop-1.png)
