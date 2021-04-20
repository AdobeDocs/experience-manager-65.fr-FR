---
title: Utilisation d’expressions SOM dans des formulaires adaptatifs
seo-title: Utilisation d’expressions SOM dans des formulaires adaptatifs
description: Découvrez comment extraire les expressions SOM d’un panneau de formulaire adaptatif.
seo-description: Découvrez comment extraire les expressions SOM d’un panneau de formulaire adaptatif.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 91%

---


# Utilisation d’expressions SOM dans des formulaires adaptatifs{#using-som-expressions-in-adaptive-forms}

Les formulaires adaptatif sont modélisés comme des pages AEM, représentées par des structures de contenu JCR dans le référentiel AEM. L’élément clé de la structure de contenu est le nœud du guideContainer. Sous le guideContainer, il existe un rootPanel pouvant contenir un panneau et des champs imbriqués.

Vous pouvez utiliser un modèle d’objet de script (SOM) pour référencer des valeurs, des propriétés et des méthodes dans un modèle d’objet de document (DOM) particulier. Un DOM organise les objets et les propriétés de mémoire dans une arborescence. Une expression SOM référence des champs ou des éléments de dessin et des panneaux.

L’image suivante illustre une structure de noeud à laquelle un formulaire adaptatif se traduit lorsque vous ajoutez des composants à un formulaire. Par exemple, vous pouvez ajouter un panneau au panneau racine et un bouton radio au panneau transformé en DOM à l’exécution. L’Expression SOM du champ de bouton radio dans le formulaire adaptatif est spécifiée comme `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Arborescence DOM](assets/hierarchy.png)

Arborescence DOM

Une expression SOM pour tout élément dans un formulaire adaptatif est précédée de `guide[0].guide1[0]`. La position d’un composant dans la hiérarchie de la structure de nœud est utilisée pour dériver son expression SOM.

![Arborescence DOM à deux boutons radio](assets/hierarchy_radio_button.png)

Arborescence DOM à deux boutons radio

L’expression SOM change lorsque vous modifiez la position des boutons radio dans le formulaire adaptatif. Dans le mode création, vous pouvez afficher l’expression SOM d’un champ ou d’un élément dans AEM Forms à l’aide de l’option Visualiser l’expression SOM. L’option apparaît dans le panneau et lorsque vous faites un clic droit sur le champ ou sur l’élément.

![Extraction des expressions SOM dans un formulaire adaptatif](assets/som-expressions.png)

Extraction des expressions SOM dans un formulaire adaptatif

Dans les panneaux, vous pouvez accéder à la fonction depuis la barre d’outils du panneau. La fonction facilite la création de scripts par les auteurs de formulaires adaptatifs.

![Extraction des expressions SOM à l’aide de la barre d’outils du panneau](assets/som-expression.png)

Extraction des expressions SOM à l’aide de la barre d’outils du panneau

Certaines API répertoriées dans [GuideBridge](https://helpx.adobe.com/fr/aem-forms/6/javascript-api/GuideBridge.html) utilisent l’expression SOM d’un élément. Par exemple, pour centrer l’attention sur un champ particulier d’un formulaire adaptatif, transmettez l’expression SOM correspondante à l’`getFocus`API dans le `guideBridge`.
