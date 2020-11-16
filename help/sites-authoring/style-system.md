---
title: Système de style
seo-title: Système de style
description: Le système de style permet à un auteur de modèles de définir des classes de style dans la stratégie de contenu d’un composant, de façon à pouvoir sélectionner ces classes lors de la modification du composant sur une page. Ces styles peuvent être des variantes visuelles d’un composant, le rendant ainsi plus flexible.
seo-description: Le système de style permet à un auteur de modèles de définir des classes de style dans la stratégie de contenu d’un composant, de façon à pouvoir sélectionner ces classes lors de la modification du composant sur une page. Ces styles peuvent être des variantes visuelles d’un composant, le rendant ainsi plus flexible.
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
translation-type: tm+mt
source-git-commit: 0985ba24f7430381fccc40faf3a316d3abd85a30
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 96%

---


# Système de style{#style-system}

Le système de style permet à un auteur de modèles de définir des classes de style dans la stratégie de contenu d’un composant, de façon à pouvoir sélectionner ces classes lors de la modification du composant sur une page. Ces styles peuvent être des variantes visuelles d’un composant, le rendant ainsi plus flexible.

Cela rend inutile le développement d’un composant personnalisé pour chaque style ou la personnalisation d’une boîte de dialogue de composant pour activer une telle fonctionnalité de style. On obtient ainsi des composants plus réutilisables, pouvant être adaptés, rapidement et aisément, aux besoins des auteurs de contenu sans développement back-end dans AEM.

## Exemple d’utilisation  {#use-case}

Les auteurs de modèles doivent être en mesure de configurer non seulement le mode de fonctionnement des composants pour les auteurs de contenu, mais aussi diverses variantes visuelles d’un composant.

De même, les auteurs de contenu ne doivent pas seulement pouvoir structurer et organiser leur contenu. Ils doivent également être en mesure de choisir leur présentation visuelle.

Le système de style constitue une solution unifiée pour répondre à la fois aux exigences des auteurs de contenus et de modèles :

* Les auteurs de modèles peuvent définir des classes de style dans la stratégie de contenu des composants.
* Les auteurs de contenu peuvent sélectionner ces classes dans un menu déroulant lorsqu’ils modifient le composant sur une page pour appliquer les styles correspondants.

La classe de style est ensuite insérée sur l’élément wrapper du composant, de façon à ce que le développeur de composants n’ait pas besoin de gérer les styles (en plus de fournir leurs règles CSS).

## Présentation {#overview}

L’utilisation du système de style se passe généralement comme suit.

1. Le concepteur web crée différentes variantes visuelles d’un composant.

1. Le développeur HTML dispose de la sortie HTML des composants et des variantes visuelles à mettre en œuvre.

1. Le développeur HTML définit les classes CSS qui correspondent à chaque variante visuelle et qui doivent être insérées sur l’élément qui enveloppe les composants.

1. Le développeur HTML met en œuvre le code CSS correspondant (et, éventuellement, le code JS) pour que chaque variante visuelle ait l’apparence définie.

1. Le développeur AEM place le code CSS (et en option, JS) fourni dans une [bibliothèque cliente](/help/sites-developing/clientlibs.md) et le déploie.

1. Le développeur AEM ou l’auteur de modèles configure les modèles de page et modifie la stratégie de chaque composant stylisé, en ajoutant les classes CSS définies, en attribuant des noms conviviaux à chaque style et en indiquant les styles qui peuvent être combinés.

1. L’auteur des pages AEM peut alors choisir les styles conçus dans l’éditeur de page via le menu de style de la barre d’outils du composant.

Notez que seules les trois dernières étapes sont réalisées dans AEM. Cela signifie que l’ensemble du développement des codes CSS et JavaScript peut être réalisé sans AEM.

La mise en œuvre des styles nécessite uniquement le déploiement dans AEM et la sélection des modèles souhaités parmi les composants.

Le diagramme suivant illustre l’architecture du système de style.

![aem-style-system](assets/aem-style-system.png)

## Utilisation {#use}

Pour démontrer la fonctionnalité, nous utiliserons comme exemple l’implémentation de [WKND](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html), [composant de titre](https://www.adobe.com/go/aem_cmp_title_v2_fr) des composants principaux.

Les sections suivantes, [En tant qu’auteur de contenu](#as-a-content-author) et [En tant qu’auteur de modèles](#as-a-template-author), décrivent comment tester les fonctionnalités du système de style à l’aide du système de style de WKND.

Si vous souhaitez utiliser le système de style pour vos propres composants, procédez comme suit :

1. Installez les CSS en tant que bibliothèques clientes, comme évoqué dans la section [Aperçu](#overview).
1. Configurez les classes CSS que vous souhaitez rendre disponibles à vos auteurs de contenu, comme décrit dans la section [En tant qu’auteur de modèles](#as-a-template-author).
1. Les auteurs de contenu peuvent alors utiliser les styles, comme décrit dans la section [En tant qu’auteur de contenu](#as-a-content-author).

### En tant qu’auteur de contenu  {#as-a-content-author}

1. Après avoir installé le projet WKND, accédez à la page d’accueil principale de WKND `http://<host>:<port>/sites.html/content/wknd/language-masters/en` (en anglais) et modifiez la page.
1. Sélectionnez un composant **Titre** plus bas dans la page

   ![Système de style pour l’auteur](assets/style-system-author.png)

1. Appuyez ou cliquez sur le bouton **Styles** dans la barre d’outils du composant **Liste** pour ouvrir le menu des styles et changer l’apparence du composant.

   ![Sélection de styles](assets/style-system-author2.png)

   >[!NOTE]
   >
   >Dans cet exemple, les styles **Couleurs** (**Noir**, **Blanc** et **Gris**) s’excluent mutuellement, tandis que les options **Style** (**Souligné**, **Aligner à droite** et **Mini Espacement**) peuvent être combinées. Vous pouvez [configurer ce paramètre dans le modèle en tant qu’auteur du modèle](#as-a-template-author).

### En tant qu’auteur de modèles  {#as-a-template-author}

1. Alors que vous modifiez la page d’accueil de WKND (`http://<host>:<port>/sites.html/content/wknd/language-masters/en`) (en anglais), modifiez le modèle de la page via **Informations sur la page -> Modifier le modèle**.

   ![Modifier le modèle](assets/style-system-edit-template.png)

1. Modifiez la police du composant **Titre** en appuyant ou en cliquant sur le bouton **Stratégie** du composant.

   ![Modifier la stratégie](assets/style-system-edit-policy.png)

1. Dans l’onglet Styles des propriétés, vous pouvez voir comment les styles ont été configurés.

   ![Modification des propriétés](assets/style-system-properties.png)

   * **Nom de groupe** : les styles peuvent être regroupés dans le menu des styles que l’auteur du contenu voit pendant la configuration du style du composant.
   * **Les styles peuvent être combinés :** permet de sélectionner simultanément plusieurs styles au sein de ce groupe.
   * **Nom du style :** description du style que l’auteur de contenu verra pendant la configuration du style du composant.
   * **Classes CSS :** nom réel de la classe CSS associée au style.

   Utilisez les poignées pour définir l’ordre des groupes et des styles au sein des groupes. Utilisez les icônes d’ajout ou de suppression pour ajouter ou supprimer des groupes ou des styles dans les groupes.

>[!CAUTION]
>
>The CSS classes (as well as any necessary Javascript) configured as style properties of a component&#39;s policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.

## Configuration {#setup}

La version 2 ou supérieure des composants principaux est entièrement équipée pour tirer parti du système de style. Elle ne nécessite aucune configuration supplémentaire.

Les étapes suivantes ne sont nécessaires que pour activer le système de style pour vos propres composants personnalisés ou pour [activer l’onglet facultatif Styles dans la boîte de dialogue Modifier.](#enable-styles-tab-edit)

### Activer l’onglet Style dans la boîte de dialogue Conception {#enable-styles-tab-design}

Pour qu’un composant fonctionne avec le système de style d’AEM et affiche l’onglet Style dans sa boîte de dialogue de conception, le développeur de composants doit inclure cet onglet avec les paramètres suivants sur le composant :

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

Une fois le composant configuré, les styles définis par les auteurs de pages seront automatiquement insérés par AEM sur l’élément de décoration qu’AEM ajoute automatiquement autour de chaque composant modifiable. Le composant lui-même n’a besoin d’effectuer aucune autre action pour que cela se produise.

### Activer l’onglet Styles dans la boîte de dialogue Modifier {#enable-styles-tab-edit}

Depuis AEM version 6.5.3.0, un onglet Styles en option de la boîte de dialogue Modifier est désormais disponible. Contrairement à l’onglet de la boîte de dialogue Conception, celui de la boîte de dialogue Modifier n’est pas essentiel pour le fonctionnement du système de style. Il s’agit d’une autre interface facultative, utilisable par un auteur de contenu pour définir des styles.

L’onglet de la boîte de dialogue Modifier peut être inclus de la même manière que celui de la boîte de dialogue Conception :

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>L’onglet Styles de la boîte de dialogue Modifier n’est pas activé par défaut.

### Styles avec noms d’éléments  {#styles-with-element-names}

Les développeurs peuvent aussi configurer une liste de noms d’éléments autorisés pour les styles du composant avec la propriété de table de chaînes `cq:styleElements`. Ensuite, dans l’onglet Styles de la stratégie, dans la boîte de dialogue de conception, l’auteur de modèles peut aussi choisir un nom d’élément pour chaque style. Cela permet de définir le nom de l’élément wrapper.

Cette propriété est définie sur le nœud `cq:Component`. Par exemple :

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>Évitez de définir des noms d’éléments pour les styles pouvant être combinés. Lorsque plusieurs noms d’éléments sont définis, l’ordre de priorité est le suivant :
>
>1. HTL est prioritaire sur tout le reste : `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. Ensuite, au sein de plusieurs styles actifs, le premier style de la liste des styles configurés dans la stratégie du composant est sélectionné.
>1. Enfin, le nom `cq:htmlTag`/ `cq:tagName` du composant est considéré comme une valeur de repli.

>



Cette capacité à définir des noms de styles est utile pour les composants génériques, tels que le conteneur de mise en page ou le composant Fragment de contenu. Cela permet de leur donner davantage de sens.

Cela permet, par exemple, d’attribuer au conteneur de mise en page des balises comme `<main>`, `<aside>`, `<nav>`, etc.
