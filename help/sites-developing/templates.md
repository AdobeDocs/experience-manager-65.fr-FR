---
title: Modèles
description: Les modèles sont utilisés lors de la création d’une page qui servira de base à la nouvelle page.
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 98%

---

# Modèles{#templates}

Les modèles sont souvent utilisés dans AEM :

* [Lorsque vous créez une page, vous sélectionnez un modèle](#templates-pages). Ce modèle est utilisé comme base pour la nouvelle page. Le modèle définit la structure de la page, le contenu initial et les [composants](/help/sites-authoring/default-components.md) qui peuvent être utilisés (propriétés de conception).

* [Lorsque vous créez un fragment de contenu, vous sélectionnez également un modèle](#templates-content-fragments). Ce modèle définit la structure, les éléments initiaux et les variations.

Les modèles suivants sont décrits en détail :

* [Modèles de pages – Modifiables](/help/sites-developing/page-templates-editable.md)
* [Modèles de page - Statiques](/help/sites-developing/page-templates-static.md)
* [Modèles de fragment de contenu](/help/sites-developing/content-fragment-templates.md)
* [Rendu de modèle adaptatif](/help/sites-developing/templates-adaptive-rendering.md)

## Modèles - Pages {#templates-pages}

AEM propose désormais deux types de modèles de base pour la création de pages :

>[!NOTE]
>
>Lorsque vous utilisez un modèle pour [créer une page](/help/sites-authoring/managing-pages.md#creating-a-new-page), il n’y a pas de différence visible (dans la page de création) et aucune indication du type de modèle utilisé.

### Modèles modifiables {#editable-templates}

Les modèles modifiables font aujourd’hui partie des bonnes pratiques de développement avec AEM.

Les avantages des modèles modifiables sont les suivants :

* ils peuvent être [créés](/help/sites-authoring/templates.md#creating-a-new-template-template-author) et [modifiés](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) par vos auteurs et autrices.

* Ils ont été introduits pour vous permettre de définir les éléments suivants pour toutes les pages créées avec le modèle :

   * la structure ;
   * le contenu initial ;
   * les politiques de contenu.

* Une fois la page créée, une connexion dynamique est conservée entre la page et le modèle. Ce lien signifie que les modifications apportées à la structure du modèle sont reflétées sur toutes les pages créées avec ce modèle. Les modifications apportées au contenu initial ne sont pas reflétées.
* Utilisent des politiques de contenu (modifiés à partir de l’éditeur de modèles) pour conserver les propriétés de conception (n’utilise pas le mode Conception dans l’éditeur de page).
* Sont stockés sous `/conf`.
* Consultez les [Modèles modifiables](/help/sites-developing/page-templates-editable.md) pour plus d’informations.

>[!NOTE]
>
>Consultez la section [Utiliser les modèles de page modifiables pour développer un site Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=fr).

### Modèles statiques {#static-templates}

Modèles statiques :

* ils doivent être définis et configurés par vos développeurs et développeuses.
* Le système de création de modèles d’AEM d’origine, disponible depuis de nombreuses versions.
* Un modèle statique est une hiérarchie de nœuds ayant la même structure que la page à créer, mais sans contenu réel.
* Ils sont copiés pour créer la page, aucune connexion dynamique n’existe par la suite.
* Ils utilisent le [Mode de conception](/help/sites-authoring/default-components-designmode.md) pour conserver les propriétés de conception.
* Sont stockés sous `/apps`.
* Consultez les [Modèles statiques](/help/sites-developing/page-templates-static.md) pour plus d’informations.

>[!NOTE]
>
>Depuis AEM version 6.5, l’utilisation des modèles statiques n’est plus considérée comme une bonne pratique. Privilégiez les modèles modifiables à la place.
>
>Les outils de [Modernisation d’AEM](modernization-tools.md) peuvent vous aider à migrer de modèles statiques à des modèles modifiables.

### Disponibilité des modèles {#template-availability}

>[!CAUTION]
>
>AEM offre plusieurs propriétés pour contrôler les modèles autorisés sous **Sites**. Cependant, leur combinaison peut conduire à des règles très complexes, difficiles à suivre et à gérer.
>
>Par conséquent, Adobe vous recommande de commencer simplement, en définissant :
>
>* uniquement la propriété `cq:allowedTemplates` ;
>
>* uniquement sur la racine du site.
>
>Pour consulter un exemple, reportez-vous à la section We.Retail : `/content/we-retail/jcr:content`
>
>Les propriétés `allowedPaths`, `allowedParents` et `allowedChildren` peuvent également être placées sur les modèles pour définir des règles plus élaborées. Cependant, dans la mesure du possible, il est *beaucoup* plus simple de définir d’autres propriétés `cq:allowedTemplates` dans des sous-sections du site si des restrictions supplémentaires des modèles autorisés s’imposent.
>
>Un autre avantage est que les propriétés `cq:allowedTemplates` peuvent être mises à jour par un auteur ou une autrice dans l’onglet **Avancé** des **Propriétés de la page**. Les autres propriétés de modèle ne peuvent pas être mises à jour à l’aide de l’interface utilisateur (standard). Il faudrait donc qu’un développeur ou une développeuse conserve les règles et qu’un déploiement du code soit effectué pour chaque modification.

Lors de la création d’une page dans l’interface d’administration du site, la liste des modèles disponibles dépend de l’emplacement de la nouvelle page et des restrictions d’emplacement spécifiées dans chaque modèle.

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

Voir [Modèles de fragments de contenu](/help/sites-developing/content-fragment-templates.md).
