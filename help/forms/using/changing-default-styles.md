---
title: Modifiier les styles par défaut des formulaires HTML5
description: Le style de HTML5 forms est basé sur CSS. Vous pouvez modifier les styles par défaut du formulaire.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 51%

---

# Modifiier les styles par défaut des formulaires HTML5{#changing-default-styles-of-html-forms}

Les formulaires HTML5 sont rendu utilisant des fonctionnalités HTML5 et le style du formulaire rendu est fait utilisant CSS. L’apparence par défaut des formulaires HTML5 est similaire à son rendu PDF. Les développeurs peuvent utiliser une page CSS personnalisée pour modifier l’aspect par défaut des formulaires HTML5.

Cet article contient des informations détaillées sur la modification du style d’un formulaire HTML5 et l’article [Introduction aux styles](/help/forms/using/css-styles.md) contient des informations détaillées sur divers aspects de style de formulaires HTML5. Assurez-vous d’avoir lu l’article Introduction aux styles avant d’effectuer les étapes mentionnées dans cet article.

Les deux images qui suivent montrent la différence entre les styles par défaut et les styles personnalisés.

![pictures-002-small](assets/pictures-002-small.png)

## Donner du style à vos formulaires {#style-your-forms}

1. **Sélection d’un profil pour ajouter des styles personnalisés**

   Accédez à l’interface de CRX DE à lʼadresse suivante :**https://&lt;server>:&lt;port>/crx/de** et créez un profil ou sélectionnez un profil existant. Pour savoir comment créer un profil, voir [Création d’un profil](/help/forms/using/custom-profile.md)

1. **Création d’une feuille de style CSS pour le style des formulaires HTML5**

   Accédez au dossier dans lequel vous avez créé le rendu de profil et créez un fichier de feuille de style CSS. Les étapes à suivre sont :

   1. Cliquez avec le bouton droit sur le dossier et sélectionnez **create** > **créer un fichier** à partir du menu

   1. Dans la boîte de dialogue de création de fichier, saisissez le nom de la feuille de style. Veillez à utiliser l’extension .css (par exemple, stylesheet.css).
   1. Dans le volet du navigateur, ouvrez le fichier CSS que vous avez créé.
   1. Définissez les classes CSS des composants dont vous souhaitez modifier le style et ajoutez des styles dans ces classes.

   Pour savoir quelles classes CSS créer pour un composant particulier de vos formulaires HTML5, voir [Présentation des styles](/help/forms/using/css-styles.md).

1. **Inclure la feuille de style dans le rendu de profil**

   Ouvrez la page Rendu du profil (fichier jsp) dans CRX DE et insérez le fichier CSS dans la page juste en dessous de la bibliothèque cliente XFA. Effectuez les étapes suivantes pour inclure le fichier CSS dans le profil.

   1. Recherchez la ligne suivante dans la page du rendu :

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. Insérez les éléments suivants sous la ligne ci-dessus pour inclure la feuille de style :

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Enregistrez le fichier.
