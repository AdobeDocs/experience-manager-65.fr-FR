---
title: Modèles de fragment de contenu
seo-title: Modèles de fragment de contenu
description: Les modèles de fragment de contenu sont utilisés pour créer des fragments de contenu avec du contenu structuré.
seo-description: Les modèles de fragment de contenu sont utilisés pour créer des fragments de contenu avec du contenu structuré.
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 98%

---


# Modèles de fragment de contenu{#content-fragment-models}

Les modèles de fragment de contenu définissent la structure du contenu pour vos [fragments de contenu](/help/assets/content-fragments/content-fragments.md).

## Activation des modèles de fragment de contenu   {#enable-content-fragment-models}

>[!CAUTION]
>
>Si vous n’activez pas **les modèles de fragment de contenu**, l’option **Créer** n’est pas disponible pour la création de modèles.

Pour activer les modèles de fragment de contenu, vous devez :

* Activez l’utilisation des modèles de fragments de contenu dans le [navigateur de configuration](/help/sites-administering/configurations.md).
* appliquer la configuration à votre dossier de ressources.

### Activation des modèles de fragment de contenu dans Configuration Manager    {#enable-content-fragment-models-in-configuration-manager}

Pour [créer un nouveau modèle de fragment de contenu](#creating-a-content-fragment-model), vous **devez** d’abord activer ces modèles à l’aide du gestionnaire de configuration :

>[!CAUTION]
>
>L’utilisation des sous-configurations (les configurations imbriquées dans une configuration) n’est pas prise en charge avec les fragments de contenu.

1. Accédez à **Outils**, **Général**, puis ouvrez l’**Explorateur de configurations**.

1. Utilisez le bouton **Créer** pour ouvrir la boîte de dialogue.

   1. Spécifiez un **Titre**.
   1. Sélectionnez **Modèles de fragment de contenu** pour activer leur utilisation.

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Sélectionnez **Créer** pour enregistrer la définition.

<!-- 1. Select the location appropriate to your website. -->

### Application de la configuration à votre dossier de ressources {#apply-the-configuration-to-your-assets-folder}

Lorsque la configuration **globale** est activée pour les modèles de fragment de contenu, tous les modèles que les utilisateurs créent peuvent être utilisés dans n’importe quel dossier de ressources.

Pour utiliser d’autres configurations (c’est-à-dire à l’exclusion de la version globale) avec un dossier de ressources comparable, vous devez définir la connexion. Pour ce faire, vous devez utiliser **Configuration** dans l’onglet **Cloud Services** des **Propriétés du dossier** du dossier approprié.

## Création d’un modèle de fragment de contenu {#creating-a-content-fragment-model}

1. Accédez à **Outils**, **Ressources**, puis ouvrez les **modèles de fragment de contenu**.
1. Accédez au fichier adapté votre [configuration](#enable-content-fragment-models).
1. Utilisez le bouton **Créer** pour ouvrir l’assistant.

   >[!CAUTION]
   >
   >Si[ l’utilisation des modèles de contenu du fragment n’a pas été activée](#enable-content-fragment-models), l’option **Créer** n’est pas disponible.

1. Spécifiez le **Titre du modèle**. Vous pouvez également ajouter une **description** si nécessaire.

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. Utilisez le bouton **Créer** pour enregistrer le modèle vide. Un message indique que l’action a réussi. Vous pouvez alors sélectionner **Ouvrir** pour publier immédiatement le modèle ou **Terminé** pour revenir à la console.

## Définition de votre modèle de fragment de contenu  {#defining-your-content-fragment-model}

Le modèle de fragment de contenu définit la structure des fragments de contenu qui en résultent. À l’aide de l’éditeur de modèles, vous pouvez ajouter et configurer les champs obligatoires :

>[!CAUTION]
>
>La modification d’un modèle de fragment de contenu existant peut avoir un impact sur les fragments dépendants.

1. Accédez à **Outils**, **Ressources**, puis ouvrez les **modèles de fragment de contenu**.

1. Accédez au dossier contenant votre modèle de fragment de contenu.
1. Ouvrez le modèle requis pour l’**édition**. Utilisez l’action rapide ou sélectionnez le modèle puis l’action dans la barre d’outils.

   Une fois ouvert, l’éditeur de modèles affiche :

   * à gauche : les champs déjà définis
   * à droite : les **types de données** disponibles pour la création des champs (et les **propriétés** à utiliser une fois les champs créés).

   >[!NOTE]
   >
   >Lorsqu’un champ est **obligatoire**, le **libellé** indiqué dans le volet de gauche est signalé par un astérisque (*****).

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **Pour ajouter un champ**

   * Faites glisser un type de données à l’emplacement souhaité pour un champ :

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * Une fois qu’un champ a été ajouté au modèle, le panneau de droite affiche les **propriétés** qui peuvent être définies pour ce type de données spécifique. Vous pouvez définir ce qui est obligatoire pour ce champ. Par exemple :

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   Pour le type données **texte multiligne**, il est possible de définir le **type par défaut** en tant que :
   * **Texte enrichi**

   * **Texte (Markdown)**

   * **Texte brut**

   Si elle n’est pas spécifiée, la valeur par défaut **Texte enrichi** est utilisée pour ce champ.
   La modification du **type par défaut** dans un modèle de fragment de contenu prend effet uniquement sur un fragment de contenu existant et lié après l’ouverture et l’enregistrement du fragment dans l’éditeur.

1. **Pour supprimer un champ**

   Sélectionnez le champ, puis cliquez/appuyez sur l’icône représentant une corbeille. Vous serez alors invité à confirmer l’opération.

   ![cf-32](assets/cf-32.png)

1. Après avoir ajouté tous les champs requis et défini les propriétés, utilisez le bouton **Enregistrer** pour conserver la définition. Par exemple :

   ![cfm-6420-14](assets/cfm-6420-14.png)

## Suppression d’un modèle de fragment de contenu {#deleting-a-content-fragment-model}

>[!CAUTION]
La suppression d’un modèle de fragment de contenu peut avoir un impact sur les fragments dépendants.

Pour supprimer un modèle de fragment de contenu :

1. Accédez à **Outils**, **Ressources**, puis ouvrez les **modèles de fragment de contenu**.

1. Accédez au dossier contenant votre modèle de fragment de contenu.
1. Sélectionnez votre modèle, puis utilisez l’option **de suppression** de la barre d’outils.

   >[!NOTE]
   Si le modèle est référencé, un avertissement s’affiche. Prenez alors les mesures qui s’imposent.

## Publication d’un modèle de fragment de contenu  {#publishing-a-content-fragment-model}

Les modèles de fragment de contenu doivent être publiés avant ou pendant la publication des fragments de contenu dépendants.

Pour publier un modèle de fragment de contenu :

1. Accédez à **Outils**, **Ressources**, puis ouvrez les **modèles de fragment de contenu**.

1. Accédez au dossier contenant votre modèle de fragment de contenu.
1. Sélectionnez votre modèle, puis l’option de **publication** dans la barre d’outils.

   >[!NOTE]
   Si vous publiez un fragment de contenu pour lequel le modèle n’a pas encore été publié, une liste de sélection indique cela, ainsi que le fait que le modèle sera publié avec le fragment.

