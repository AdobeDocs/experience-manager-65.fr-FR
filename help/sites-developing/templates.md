---
title: Modèles
seo-title: Modèles
description: Les modèles de sont utilisés lors de la création d’une page qui servira de base à la nouvelle page
seo-description: Les modèles de sont utilisés lors de la création d’une page qui servira de base à la nouvelle page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 27276945a0bdb20410f4c0e98868ea5ce1c09a47
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 90%

---


# Modèles{#templates}

Les modèles sont utilisés à divers endroits dans AEM :

* Lors de la [création d’une page, vous devez sélectionner un modèle](#templates-pages). C’est la base pour créer la page. Le modèle définit la structure de la page créée, le contenu initial et les [composants](/help/sites-authoring/default-components.md) qui peuvent être utilisés (propriétés de conception).

* Lorsque vous [créez un fragment de contenu, vous devez également sélectionner un modèle](#templates-content-fragments). Ce modèle définit la structure, les éléments initiaux et les variations.

Les modèles suivants sont décrits en détail :

* [Modèles de pages - Modifiables](/help/sites-developing/page-templates-editable.md)
* [Modèles de page - Statiques](/help/sites-developing/page-templates-static.md)
* [Modèles de fragment de contenu](/help/sites-developing/content-fragment-templates.md)
* [Rendu de modèle adaptatif](/help/sites-developing/templates-adaptive-rendering.md)

## Modèles - Pages {#templates-pages}

AEM propose désormais deux types de modèles de base pour la création de pages :

>[!NOTE]
>
>Lorsque vous utilisez un modèle pour [créer une page](/help/sites-authoring/managing-pages.md#creating-a-new-page), il n’y a pas de différence visible (dans la page de création) et aucune indication du type de modèle utilisé.

### Modèles modifiables {#editable-templates}

Les modèles modifiables sont maintenant considérés comme les meilleures pratiques pour le développement avec AEM.

Avantages des modèles modifiables :

* Peuvent être [créés](/help/sites-authoring/templates.md#creating-a-new-template-template-author) et [modifiés](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) par vos auteurs.

* Sont proposés pour vous permettre de définir ce qui suit pour toutes les pages créées avec le modèle :

   * la structure
   * le contenu initial
   * les stratégies de contenu

* Une fois la nouvelle page créée, une connexion dynamique est maintenue entre la page et le modèle. Cela signifie que les modifications apportées à la structure du modèle sont répercutées sur les pages créées avec ce modèle (les modifications apportées au contenu initial ne le sont pas).
* Utilisent des stratégies de contenu (modifiés à partir de l’éditeur de modèles) pour conserver les propriétés de conception (n’utilise pas le mode Conception dans l’éditeur de page).
* Sont stockés sous `/conf`
* Consultez [Modèles modifiables](/help/sites-developing/page-templates-editable.md) pour plus d’informations. 

>[!NOTE]
>
>Un article de la communauté AEM est disponible pour expliquer comment développer un site Experience Manager avec des modèles modifiables, voir [Création d’un site Web Adobe Experience Manager 6.5 à l’aide de modèles modifiables](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Modèles statiques {#static-templates}

Les modèles statiques :

* Doivent être définis et configurés par vos développeurs.
* Il s&#39;agissait du système de modèle d&#39;AEM d&#39;origine et il a été disponible pour de nombreuses versions.
* Un modèle statique est une hiérarchie de nœuds qui a la même structure que la page à créer, mais sans contenu réel.
* Sont copiés pour créer la nouvelle page, aucune connexion dynamique n’existe après cela.
* Utilisez le [mode Conception](/help/sites-authoring/default-components-designmode.md) pour conserver les propriétés de conception.
* Sont stockés sous `/apps`
* Consultez [Modèles statiques](/help/sites-developing/page-templates-static.md) pour plus d’informations.

>[!NOTE]
>
>À l&#39;AEM 6.5, l&#39;utilisation de modèles statiques n&#39;est pas considérée comme une bonne pratique. Privilégiez les modèles modifiables à la place.
>
>[AEM ](modernization-tools.md) ModernisationTools peut vous aider à migrer des modèles statiques vers des modèles modifiables.

### Disponibilité des modèles {#template-availability}

>[!CAUTION]
>
>AEM offre plusieurs propriétés pour contrôler les modèles autorisés sous **Sites**. Cependant, leur combinaison peut conduire à des règles très complexes, difficiles à suivre et à gérer.
>
>Par conséquent, Adobe vous recommande de commencer simplement, en définissant :
>
>* uniquement la propriété `cq:allowedTemplates` ;
   >
   >
* uniquement sur la racine du site.
>
>
Pour un exemple, voir We.Retail : `/content/we-retail/jcr:content`
>
>Les propriétés `allowedPaths`, `allowedParents` et `allowedChildren` peuvent également être placées sur les modèles pour définir des règles plus élaborées. Cependant, dans la mesure du possible, il est *beaucoup* plus simple de définir d’autres propriétés `cq:allowedTemplates` dans des sous-sections du site si des restrictions supplémentaires des modèles autorisés s’imposent.
>
>Un autre avantage est que les propriétés `cq:allowedTemplates` peuvent être mises à jour par un auteur dans l’onglet **Avancé** des **Propriétés de la page**. Les autres propriétés de modèle ne peuvent pas être mises à jour à l’aide de l’interface utilisateur (standard). Il faudrait donc qu’un développeur conserve les règles et qu’un déploiement du code soit effectué pour chaque modification.

Lors de la création d’une page dans l’interface admin du site, la liste des modèles disponibles dépend de l’emplacement de la nouvelle page et des restrictions de positionnement spécifiées dans chaque modèle.

Les propriétés suivantes déterminent si un modèle `T` peut être utilisé pour qu’une nouvelle page soit placée en tant qu’enfant de la page `P`. Chacune de ces propriétés est une chaîne à valeurs multiples contenant aucune ou plusieurs expressions régulières utilisées pour la correspondance avec les chemins :

* La propriété `cq:allowedTemplates` du sous-nœud `jcr:content` de `P` ou un ancêtre de `P`.

* La propriété `allowedPaths` de `T`.

* La propriété `allowedParents` de `T`.

* La propriété `allowedChildren` du modèle de `P`.

L’évaluation fonctionne comme suit :

* La première propriété `cq:allowedTemplates` non vide détectée dans la hiérarchie de page commençant par `P` est comparée au chemin de `T`. Si aucune des valeurs ne correspond, `T` est rejeté.

* Si `T` a une propriété `allowedPaths` non vide, mais qu’aucune des valeurs ne correspond au chemin de `P`, `T` est rejeté.

* Si les deux propriétés ci-dessus sont vides ou inexistantes, `T` est rejeté sauf s’il appartient à la même application que `P`. `T` appartient à la même application que `P` si et seulement si le nom du deuxième niveau du chemin de `T` est identique à celui du deuxième niveau du chemin de `P`. Par exemple, le modèle `/apps/geometrixx/templates/foo` appartient à la même application que la page `/content/geometrixx`.

* Si `T` a une propriété `allowedParents` non vide, mais qu’aucune des valeurs ne correspond au chemin de `P`, `T` est rejeté.

* Si le modèle de `P` a une propriété `allowedChildren` non vide, mais qu’aucune des valeurs ne correspond au chemin de `T`, `T` est rejeté.

* Dans tous les autres cas, `T` est autorisé.

Le diagramme suivant illustre le processus d’évaluation de modèle :

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitation des modèles utilisés dans les pages enfants {#limiting-templates-used-in-child-pages}

Pour limiter les modèles servant à créer des pages enfants sous une page donnée, utilisez la propriété `cq:allowedTemplates` du nœud `jcr:content` de la page pour spécifier la liste des modèles à autoriser en tant que pages enfants. Chaque valeur de la liste doit être un chemin absolu vers un modèle pour une page enfant autorisée, par exemple `/apps/geometrixx/templates/contentpage`.

Vous pouvez appliquer la propriété `cq:allowedTemplates` sur le nœud `jcr:content` du modèle pour que cette configuration soit appliquée à toutes les pages nouvellement créées qui utilisent ce modèle.

Si vous souhaitez ajouter d’autres contraintes, par exemple concernant la hiérarchie des modèles, vous pouvez appliquer les propriétés `allowedParents/allowedChildren` sur le modèle. Vous pouvez ensuite spécifier explicitement que les pages créées à partir d’un modèle T doivent être des parents/enfants de pages créées à partir d’un modèle T.

## Modèles - Fragments de contenu {#templates-content-fragments}

Voir [Modèles de fragment de contenu](/help/sites-developing/content-fragment-templates.md) pour plus d’informations.
