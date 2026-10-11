---
title: Utiliser des expressions SOM dans des formulaires adaptatifs
description: Découvrez comment extraire des expressions SOM d’un panneau de formulaire adaptatif.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
exl-id: 6a158e18-b7d0-45fb-b4fc-4770e66982b4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 100%
---
# Utiliser des expressions SOM dans des formulaires adaptatifs{#using-som-expressions-in-adaptive-forms}

Les formulaires adaptatifs sont modélisés comme des pages AEM, représentées par des structures de contenu JCR dans le référentiel AEM. L’élément clé de la structure de contenu est le nœud guideContainer. Sous guideContainer, il existe un rootPanel qui peut contenir un panneau et des champs imbriqués.

Vous pouvez utiliser un modèle d’objet de script (SOM) pour référencer des valeurs, des propriétés et des méthodes dans un modèle d’objet de document (DOM) particulier. Un DOM organise les objets et les propriétés de mémoire dans une hiérarchie d’arborescence. Une expression SOM référence des champs/éléments de dessin et des panneaux.

L’image suivante illustre une structure de nœud d’un formulaire adaptatif traduite lorsque vous ajoutez des composants à un formulaire. Par exemple, vous pouvez ajouter un panneau au panneau racine et un bouton radio au panneau transformé en DOM à l’exécution. L’expression SOM du champ de bouton radio du formulaire adaptatif est spécifiée comme `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Arborescence DOM](assets/hierarchy.png)

Arborescence DOM

Une expression SOM pour tout élément dans un formulaire adaptatif est précédée de `guide[0].guide1[0]`. La position d’un composant dans la hiérarchie de la structure de nœud est utilisée pour dériver son expression SOM.

![Arborescence DOM à deux boutons radio](assets/hierarchy_radio_button.png)

Arborescence DOM à deux boutons radio

L’expression SOM change lorsque vous modifiez la position des boutons radio dans le formulaire adaptatif. En mode création, vous pouvez afficher l’expression SOM d’un champ ou d’un élément dans AEM Forms à l’aide de l’option Afficher l’expression SOM. L’option apparaît dans le panneau et lorsque vous cliquez avec le bouton droit sur le champ ou sur l’élément.

![Extraction des expressions SOM dans un formulaire adaptatif](assets/som-expressions.png)

Extraction des expressions SOM dans un formulaire adaptatif

Dans les panneaux, vous pouvez accéder à la fonction depuis la barre d’outils du panneau. La fonction facilite la création de scripts par les auteurs de formulaires adaptatifs.

![Extraction des expressions SOM à l’aide de la barre d’outils du panneau](assets/som-expression.png)

Extraction des expressions SOM à l’aide de la barre d’outils du panneau

Certaines API répertoriées dans [GuideBridge](https://helpx.adobe.com/fr/aem-forms/6/javascript-api/GuideBridge.html) utilisent l’expression SOM d’un élément. Par exemple, pour centrer l’attention sur un champ particulier d’un formulaire adaptatif, transmettez l’expression SOM correspondante à l’`getFocus`API dans le `guideBridge`.
