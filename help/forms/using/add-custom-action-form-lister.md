---
title: Ajout d’une action personnalisée sur des éléments de liste de formulaire
seo-title: Ajout d’une action personnalisée sur des éléments de liste de formulaire
description: Les développeurs de formulaires peuvent ajouter des actions à la liste des formulaires sur la page Forms Portal. Par défaut, la liste des formulaires vous permet d’accéder au formulaire, de le remplir et de l’envoyer.
seo-description: Les développeurs de formulaires peuvent ajouter des actions à la liste des formulaires sur la page Forms Portal. Par défaut, la liste des formulaires vous permet d’accéder au formulaire, de le remplir et de l’envoyer.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%

---

# Ajout d’une action personnalisée sur des éléments de liste de formulaire{#adding-custom-action-on-form-lister-items}

Dans AEM Forms, vous pouvez créer une page de portail qui répertorie les formulaires disponibles. Par défaut, vous pouvez rechercher des formulaires et les répertorier sur une page de portail. Vous pouvez ouvrir des formulaires en vue de les compléter et envoyer vos informations. Seules les actions de rendu sont disponibles, prêtes à l’emploi, pour les formulaires répertoriés sur une page de portail. Pour plus d’informations sur les actions disponibles sur une page de portail, reportez-vous à la section [Création d’une page de portail de formulaires](../../forms/using/creating-form-portal-page.md). 

Vous pouvez ajouter d’autres options sur la page de portail. Ces options ou actions peuvent être personnalisées en adaptant le modèle de portail de formulaires.

Cet article explique comment créer un bouton pour envoyer directement le lien d’un formulaire à partir d’une page du portail de formulaires. Cette personnalisation nécessite la mise à jour du modèle pour le composant Search &amp; Lister.

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

Vous pouvez ajouter des actions semblables dans votre modèle personnalisé. Pour définir une fonction JavaScript, ajoutez-la sur un script de niveau page et liez-la à l’élément HTML requis. Dans l’exemple ci-dessus, l’expression `onclick` est la fonction liée.

Une fois les modifications apportées au modèle, la page d’exemple du portail contient un bouton permettant d’envoyer le lien du formulaire par courrier électronique, comme illustré ci-dessous.

![email](assets/email.png)
