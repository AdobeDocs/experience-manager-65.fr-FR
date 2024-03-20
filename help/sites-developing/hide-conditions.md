---
title: Utilisation de conditions de masquage
description: Vous pouvez utiliser des conditions de masquage pour déterminer si une ressource de composant est générée ou non.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 71%

---

# Utilisation de conditions de masquage {#using-hide-conditions}

Vous pouvez utiliser des conditions de masquage pour déterminer si une ressource de composant est générée ou non. Par exemple, lorsqu’un créateur de modèles configure le composant principal [composant de liste](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=fr) dans le [éditeur de modèles](/help/sites-authoring/templates.md) et décide de désactiver les options pour créer la liste en fonction des pages enfants. La désactivation de cette option dans la boîte de dialogue de conception définit une propriété de sorte que lorsque le composant de liste est rendu, la condition de masquage est évaluée et l’option d’affichage des pages enfants n’est pas affichée.

## Vue d’ensemble {#overview}

Les boîtes de dialogue peuvent devenir complexes avec de nombreuses options pour l’utilisateur, qui ne peut utiliser qu’une fraction des options à sa disposition. Cela peut entraîner une surcharge des expériences de l’interface utilisateur pour les utilisateurs et utilisatrices.

En utilisant les conditions de masquage, les administrateurs et administratrices, les développeurs et développeuses, et les super-utilisateurs et super-utilisatrices disposent d’un moyen de masquer les ressources en fonction d’un ensemble de règles. Cette fonction leur permet de décider quelles ressources afficher lorsqu’un créateur ou une créatrice modifie le contenu.

>[!NOTE]
>
>Le masquage d’une ressource à partir d’une expression ne remplace pas les autorisations ACL. Le contenu reste modifiable mais ne s’affiche pas.

## Détails relatifs à la mise en œuvre et à l’utilisation {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` est chargé de filtrer les ressources en fonction de l’existence et de la valeur de la propriété `granite:hide`, située sur le champ à filtrer. L’implémentation de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` comprend une instance de `FilteringResourceWrapper.`

L’implémentation utilise l’[API ELResolver](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) de Granite et ajoute une variable personnalisée `cqDesign` via ExpressionCustomizer.

Voici quelques exemples de conditions de masquage sur un nœud de conception situé sous `etc/design` ou sous la forme d’une politique de contenu.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Lors de la définition de votre expression de masquage, tenez compte des points suivants :

* Pour être valide, la portée dans laquelle se trouve la propriété doit être exprimée (`cqDesign.myProperty`, par exemple).
* Les valeurs sont en lecture seule.
* Les fonctions (si nécessaire) doivent être limitées à un ensemble donné fourni par le service.

## Exemple {#example}

Vous trouverez des exemples de conditions de masquage dans AEM et dans les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) en particulier. Par exemple, envisagez la variable [composant principal de liste](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=fr).

[En utilisant l’éditeur de modèles](/help/sites-authoring/templates.md), l’auteur de modèles peut définir, dans la boîte de dialogue de conception, les options du composant de liste mises à la disposition de l’auteur de pages. Des options telles que l’autorisation d’une liste statique, d’une liste de pages enfants, d’une liste de pages balisées, etc., peuvent être activées ou désactivées.

Si un créateur ou une créatrice de modèles choisit de désactiver l’option des pages enfants, une propriété de conception est définie et une condition de masquage est évaluée par rapport à cette propriété, ce qui fait que l’option ne s’affiche pas pour le créateur ou la créatrice de la page.

1. Par défaut, le créateur ou la créatrice de la page peut utiliser le composant principal Liste pour créer une liste à l’aide de pages enfants en sélectionnant l’option **Pages enfants**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Dans la boîte de dialogue de création du composant principal Liste, l’auteur de modèles peut sélectionner l’option **Désactiver les enfants** pour éviter que l’option de génération d’une liste sur la base de pages enfants ne soit présentée à l’auteur de pages.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Un nœud de politique est créé sous `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` avec une propriété `disableChildren` définie sur `true`.
1. La condition de masquage est définie comme la valeur d’une propriété `granite:hide` sur le nœud de propriété de boîte de dialogue `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. La valeur de `disableChildren` est extraite de la configuration de conception et l’expression `${cqDesign.disableChildren}` est évaluée sur `false`, ce qui signifie que le rendu de l’option ne sera pas effectué dans le cadre du composant.

   Pour afficher l’expression de masquage en tant que valeur de la propriété `granite:hide` dans GitHub, cliquez [ici](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. L’option **Pages enfants** n’est plus rendue pour l’auteur de pages lors de l’utilisation du composant de liste.

   ![chlimage_1-221](assets/chlimage_1-221.png)
