---
title: Créer des tableaux complexes accessibles dans des formulaires HTML5
description: Découvrez comment créer des tableaux accessibles dans des formulaires HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 100%

---

# Créer des tableaux complexes accessibles dans des formulaires HTML5 {#create-accessible-complex-tables-in-html-forms}

L’implémentation par défaut des tableaux dans les formulaires HTML5 utilise des éléments DIV HTML pour créer le rendu d’un tableau. Le rendu requiert l’utilisation de rôles ARIA pour répondre aux exigences en matière d’accessibilité.

Pour éviter des problèmes d’accessibilité avec les lecteurs d’écran qui ne prennent pas totalement en charge les rôles ARIA utilisés avec des tableaux de données, les formulaires HTML5 fournissent un rendu alternatif pour les tableaux. Ces tableaux sont basés sur le nouveau format de tableau introduit dans Designer prenant également en charge :

* Les en-têtes de ligne
* L’étendue de ligne

Pour utiliser le nouveau format dans les formulaires HTML5, indiquez que le tableau est complexe. Pour marquer le tableau en tant que tel, ajoutez la balise `extras` dans la source XML du sous-formulaire du tableau comme suit : 

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Les tableaux qui sont marqués en tant que *complexTable* suivent le rendu HTML natif, et fournissent une meilleure prise en charge de l’accessibilité pour certains lecteurs d’écran.  Pour créer une étendue de ligne, sélectionnez les cellules consécutives d’un tableau dans la même colonne, cliquez avec le bouton droit sur la sélection, puis cliquez sur **[!UICONTROL Fusionner les cellules]**.

>[!NOTE]
>
>La création d’une étendue de ligne fonctionne pour les cellules situées les plus à gauche uniquement.

Pour marquer une ligne comme en-tête de ligne, sélectionnez toutes les cellules d’une ligne, cliquez avec le bouton droit sur la sélection, puis cliquez sur **[!UICONTROL Marquer l’en-tête]**.

Pour marquer une cellule en tant qu’en-tête de colonne, sélectionnez une cellule de la colonne, cliquez avec le bouton droit sur la sélection, puis cliquez sur **[!UICONTROL Marquer l’en-tête]**.

Limitations dans le nouveau format *AccessibleTable* :

* Pas de prise en charge des champs extensibles si l’étendue de ligne est utilisée dans le tableau.
* Pas de prise en charge des tableaux imbriqués (tableaux dans des cellules de tableau).
* La prise en charge de l’étendue de ligne est limitée aux lignes d’en-tête et aux cellules d’en-tête.
* La prise en charge est limitée aux tableaux standard.
* Pas de prise en charge des préremplissages de données dans les tableaux avec une étendue de ligne > 1.
