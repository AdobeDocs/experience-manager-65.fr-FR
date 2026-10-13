---
title: Modifiier les styles par défaut des formulaires HTML5
description: Le style de formulaires HTML5 est basé sur le code CSS. Vous pouvez modifier les styles par défaut du formulaire.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 99%
---
# Modifiier les styles par défaut des formulaires HTML5{#changing-default-styles-of-html-forms}

Les formulaires HTML5 sont rendu utilisant des fonctionnalités HTML5 et le style du formulaire rendu est fait utilisant CSS. L’apparence par défaut des formulaires HTML5 est similaire à son rendu PDF. Les développeurs et développeuses peuvent utiliser des CSS personnalisés pour modifier l’apparence par défaut des formulaires HTML5.

Cet article contient des informations détaillées sur la modification du style d’un formulaire HTML5 et l’article [Introduction aux styles](/help/forms/using/css-styles.md) contient des informations détaillées sur divers aspects de style de formulaires HTML5. Assurez-vous d’avoir lu l’article Introduction aux styles avant d’effectuer les étapes mentionnées dans cet article.

Les deux images qui suivent montrent la différence entre les styles par défaut et les styles personnalisés.

![pictures-002-small](assets/pictures-002-small.png)

## Donner du style à vos formulaires {#style-your-forms}

1. **Sélectionner un profil auquel ajouter des styles personnalisés**

   Accédez à l’interface de CRX DE à lʼadresse suivante :**https://&lt;server>:&lt;port>/crx/de** et créez un profil ou sélectionnez un profil existant. Pour savoir comment créer un profil, consultez [Création d’un profil](/help/forms/using/custom-profile.md).

1. **Création d’une feuille de style CSS pour le style des formulaires HTML5**

   Accédez au dossier dans lequel vous avez créé le rendu de profil et créez un fichier de feuille de style CSS. Les étapes à suivre sont :

   1. Cliquez avec le bouton droit sur le dossier et sélectionnez **Créer** -> **Créer un fichier** à partir du menu

   1. Dans la boîte de dialogue Création de fichier, entrez le nom de la feuille de style. Assurez-vous d’utiliser l’extension .css (par exemple stylesheet.css)
   1. Dans le volet du navigateur, ouvrez le fichier CSS que vous avez créé.
   1. Définissez les classes CSS des composants dont vous souhaitez modifier le style et ajoutez des styles dans ces classes.

   Pour savoir quelles classes CSS il convient de créer pour un composant particulier de vos formulaires HTML5, consultez [Introduction aux styles](/help/forms/using/css-styles.md).

1. **Inclusion de la feuille de style dans le rendu de profil**

   Ouvrez la page Rendu du profil (fichier jsp) dans CRX DE et insérez le fichier CSS dans la page juste en dessous de la bibliothèque cliente XFA. Effectuez les étapes suivantes pour inclure le fichier CSS dans le profil.

   1. Recherchez la ligne suivante dans la page du rendu :

      &lt;cq:includeClientLib categories=« xfaforms.profile » />

   1. Insérez les éléments suivants sous la ligne ci-dessus pour inclure la feuille de style :

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Enregistrez le fichier.
