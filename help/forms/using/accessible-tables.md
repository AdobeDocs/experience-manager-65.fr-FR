---
title: Créer des tableaux complexes accessibles dans des formulaires HTML5
seo-title: Créer des tableaux complexes accessibles dans des formulaires HTML5
description: Découvrez comment créer des tableaux accessibles dans des formulaires HTML5.
seo-description: Découvrez comment créer des tableaux accessibles dans des formulaires HTML5.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Créer des tableaux complexes accessibles dans des formulaires HTML5 {#create-accessible-complex-tables-in-html-forms}

L’implémentation par défaut des tableaux dans les formulaires HTML5 utilise des éléments DIV HTML pour créer le rendu d’un tableau. Le rendu requiert l’utilisation de rôles ARIA pour répondre aux exigences en matière d’accessibilité.

Pour éviter des problèmes d’accessibilité avec les lecteurs d’écran qui ne prennent pas entièrement en charge les rôles ARIA utilisés avec les tableaux de données, les formulaires HTML5 fournissent un autre rendu pour les tableaux. Ces tableaux sont basés sur le nouveau format de tableau introduit dans Designer prenant également en charge :

* les en-têtes de ligne ;
* l’étendue de ligne.

Pour utiliser le nouveau format dans les formulaires HTML5, indiquez que le tableau est complexe. Pour marquer le tableau en tant que tel, ajoutez la balise `extras` dans la source XML du sous-formulaire du tableau comme suit : 

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

The tables which are marked as *complexTable* follow the native HTML rendition, and provide better accessibility support for certain screen readers.  Pour créer une étendue de ligne, sélectionnez les cellules consécutives d’un tableau dans la même colonne, cliquez avec le bouton droit de la souris sur la sélection, puis cliquez sur l’option **[!UICONTROL Fusionner les cellules]**.

***Remarque :**la création d’une étendue de ligne fonctionne pour les cellules situées les plus à gauche uniquement.*

Pour marquer une ligne comme en-tête de ligne, sélectionnez toutes les cellules d’une ligne, cliquez avec le bouton droit de la souris sur la sélection, puis cliquez sur **[!UICONTROL En-tête de repère]**.

Pour marquer une cellule en tant qu’en-tête de colonne, sélectionnez une cellule de la colonne, cliquez avec le bouton droit de la souris sur la sélection, puis cliquez sur **[!UICONTROL Marquer l’en-tête]**.

Limitations in new *AccessibleTable* format:

* Absence de prise en charge des champs extensibles si l’étendue de ligne est utilisée dans le tableau
* Pas de prise en charge des tableaux imbriqués (tableaux dans les cellules d’un tableau)
* La prise en charge de l’étendue de ligne est limitée aux lignes d’en-tête et aux cellules d’en-tête
* La prise en charge est limitée aux tableaux standard
* Pas de prise en charge des préremplissages de données dans les tableaux avec une étendue de ligne > 1

