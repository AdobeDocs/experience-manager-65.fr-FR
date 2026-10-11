---
title: Créer des tableaux complexes accessibles dans des formulaires HTML5
description: Découvrez comment créer des tableaux accessibles dans des formulaires HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
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
source-wordcount: '280'
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
