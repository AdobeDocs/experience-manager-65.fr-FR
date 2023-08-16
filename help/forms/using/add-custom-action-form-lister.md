---
title: Ajouter une action personnalisée sur des éléments de liste de formulaire
seo-title: Adding custom action on form lister items
description: Les développeurs de formulaires peuvent ajouter d’autres actions à la liste des formulaires sur la page Forms Portal. Par défaut, la liste des formulaires vous permet d’accéder au formulaire, de le remplir et de l’envoyer.
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing lets you access the form, fill it, and submit it.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 32%

---

# Ajouter une action personnalisée sur des éléments de liste de formulaire{#adding-custom-action-on-form-lister-items}

Dans AEM Forms, vous pouvez créer une page de portail répertoriant les formulaires disponibles. Par défaut, vous pouvez rechercher et répertorier des formulaires sur une page de portail. Vous pouvez ouvrir des formulaires à remplir et envoyer vos informations. Seules les actions de rendu prêtes à l’emploi sont fournies pour les formulaires répertoriés sur une page de portail. Pour plus d’informations sur les actions disponibles sur une page de portail, reportez-vous à la section [Création d’une page de portail de formulaires](../../forms/using/creating-form-portal-page.md). 

Vous pouvez ajouter d’autres options à la page du portail. Ces options ou actions peuvent être personnalisées en personnalisant le modèle de Forms Portal.

Cet article explique comment créer un bouton pour envoyer le lien d’un formulaire, directement à partir d’une page Forms Portal. Cette personnalisation nécessite la mise à jour du modèle pour le composant Search &amp; Lister.

Le code requis pour ajouter l’action au modèle est disponible ci-dessous. L’attribut `onclick` situé dans le fragment de code dispose d’un script pour envoyer un lien d’un formulaire par courrier électronique.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

Vous pouvez ajouter des actions similaires dans votre modèle personnalisé. Pour définir une fonction JavaScript, ajoutez-la sur un script de niveau page et liez-la à l’élément de HTML requis. Dans l’exemple ci-dessus, l’expression `onclick` est la fonction liée.

Une fois les modifications apportées au modèle, la page d’exemple du portail contient un bouton permettant d’envoyer le lien du formulaire par courrier électronique, comme illustré ci-dessous.

![email](assets/email.png)
