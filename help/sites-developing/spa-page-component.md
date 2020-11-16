---
title: Composant de page SPA
seo-title: Composant de page SPA
description: Dans un SPA, le composant de page ne fournit pas les éléments HTML de ses composants enfants, mais le délègue à la structure SPA. Ce document explique comment cela rend le composant de page d’un SPA unique.
seo-description: Dans un SPA, le composant de page ne fournit pas les éléments HTML de ses composants enfants, mais le délègue à la structure SPA. Ce document explique comment cela rend le composant de page d’un SPA unique.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 10%

---


# Composant de page SPA{#spa-page-component}

Dans un SPA, le composant de page ne fournit pas les éléments HTML de ses composants enfants, mais le délègue à la structure SPA. Ce document explique comment cela rend le composant de page d’un SPA unique.

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent un rendu côté client SPA structure (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

Le composant de page d’un SPA ne fournit pas les éléments HTML de ses composants enfants via un fichier JSP ou HTL et des objets de ressources. Cette opération est déléguée à la structure SPA. La représentation des composants enfants est récupérée sous la forme d’une structure de données JSON (c’est-à-dire le modèle). Les composants SPA sont ensuite ajoutés à la page conformément au modèle JSON fourni. La composition initiale du corps du composant de page diffère donc de celle du code HTML prérendu.

## Gestion du modèle de page {#page-model-management}

The resolution and the management of the page model is delegated to a provided [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) module. Le SPA doit interagir avec le `PageModelManager` module lorsqu&#39;il s&#39;initialise pour récupérer le modèle de page initial et s&#39;enregistrer pour les mises à jour du modèle - produit principalement lorsque l&#39;auteur modifie la page via l&#39;éditeur de page. Le `PageModelManager` est accessible par SPA projet sous la forme d&#39;un package npm. En tant qu&#39;interprète entre l&#39;AEM et le SPA, le `PageModelManager` est destiné à accompagner le SPA.

Pour autoriser la création de la page, une bibliothèque cliente nommée `cq.authoring.pagemodel.messaging` doit être ajoutée pour fournir un canal de communication entre le SPA et l’éditeur de page. Si le composant de page SPA hérite du composant page wcm/core, il existe les options suivantes pour rendre la catégorie de bibliothèque `cq.authoring.pagemodel.messaging` client disponible :

* Si le modèle est modifiable, ajoutez la catégorie de bibliothèque cliente à la stratégie de page.
* Ajoutez la catégorie de bibliothèque cliente à l’aide `customfooterlibs.html` du composant de page.

N&#39;oubliez pas de limiter l&#39;inclusion de la `cq.authoring.pagemodel.messaging` catégorie au contexte de l&#39;éditeur de page.

## Type de données de communication {#communication-data-type}

Le type de données de communication est défini comme un élément HTML dans le composant AEM Page à l’aide de l’ `data-cq-datatype` attribut. Lorsque le type de données de communication est défini sur JSON, les demandes de GET atteignent les points de terminaison du modèle Sling d’un composant. À la suite d’une mise à jour dans l’éditeur de page, la représentation JSON du composant mis à jour est envoyée à la bibliothèque modèle de page. La bibliothèque de modèles de page avertit ensuite les SPA de mises à jour.

**Composant de page SPA -`body.html`**

```
<div id="page"></div>
```

En plus d’être une bonne pratique pour ne pas retarder la génération du modèle DOM, la structure SPA exige que les scripts soient ajoutés à la fin du corps.

**Composant de page SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Propriétés des ressources de métadonnées qui décrivent le contenu SPA :

**Composant de page SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Le sélecteur de modèle par défaut est défini de manière statique lors de la demande de la représentation du modèle Sling d’un composant.

## Propriétés des métadonnées {#meta-properties}

* `cq:wcmmode`: Mode WCM des éditeurs (par exemple, page, modèle)
* `cq:pagemodel_root_url`: URL du modèle racine de l’application. Important lors de l’accès direct à une page enfant, car le modèle de page enfant est un fragment du modèle racine de l’application. Le modèle initial de l’application est ` [PageModelManager](/help/sites-developing/spa-page-component.md)` ensuite recomposé de manière systématique en entrant dans l’application à partir de son point d’entrée racine.

* `cq:pagemodel_router`: Activation ou désactivation ` [ModelRouter](/help/sites-developing/spa-routing.md)` de la `PageModelManager` bibliothèque

* `cq:pagemodel_route_filters`: Liste séparée par des virgules ou expressions régulières pour fournir des itinéraires que les ` [ModelRouter](/help/sites-developing/spa-routing.md)` doivent ignorer.

>[!CAUTION]
>
>Ce document utilise l&#39;application de Journal We.Retail à des fins de démonstration uniquement. Il ne doit être utilisé pour aucun travail de projet.
>
>Tout projet AEM doit tirer parti de l&#39;archétype [de projet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)AEM, qui prend en charge les projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la série de projets de la sériede projets de la série de .

## Synchronisation des incrustations de l’éditeur de page {#page-editor-overlay-synchronization}

La synchronisation des recouvrements est assurée par le même Mutation Observer que celui fourni par la `cq.authoring.page` catégorie.

## Configuration de la structure exportée JSON du modèle Sling {#sling-model-json-exported-structure-configuration}

Lorsque les fonctionnalités de routage sont activées, l’hypothèse est que l’exportation JSON du SPA contient les différents itinéraires de l’application grâce à l’exportation JSON du composant de navigation AEM. La sortie JSON du composant de navigation AEM peut être configurée dans la stratégie de contenu de page racine de l’application sur une seule page au moyen des deux propriétés suivantes :

* `structureDepth` : nombre correspondant à la profondeur de l’arborescence exportée
* `structurePatterns`: Regex de tableau de index correspondant à la page à exporter

Vous pouvez l’afficher dans l’exemple de contenu SPA dans `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
