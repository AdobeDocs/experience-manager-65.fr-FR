---
title: Routage du modèle SPA
seo-title: Routage du modèle SPA
description: Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.
seo-description: Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Routage du modèle SPA{#spa-model-routing}

Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.

>[!NOTE]
>
>L’éditeur d’application d’une seule page est la solution recommandée pour les projets nécessitant un rendu côté client basé sur la structure d’application d’une seule page (par exemple, Réagir ou Angulaire).

## Routage de projet {#project-routing}

L’application est propriétaire du routage et est ensuite implémentée par les développeurs frontaux du projet. Ce document décrit le routage spécifique au modèle renvoyé par le serveur AEM. La structure de données du modèle de page expose l’URL de la ressource sous-jacente. Le projet frontal peut utiliser toute bibliothèque personnalisée ou tierce fournissant des fonctionnalités de routage. Une fois qu&#39;un itinéraire attend un fragment de modèle, un appel à la `PageModelManager.getData()` fonction peut être effectué. Lorsqu’un itinéraire de modèle a changé, un événement doit être déclenché pour avertir les bibliothèques d’écoute telles que l’éditeur de page.

## Architecture {#architecture}

Pour une description détaillée, reportez-vous à la section [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) du document Plan directeur de l’application d’une seule page.

## ModelRouter {#modelrouter}

Lorsque cette option est activée, `ModelRouter` - encapsule les fonctions de l’API d’historique HTML5 `pushState` et `replaceState` pour garantir qu’un fragment donné du modèle est prérécupéré et accessible. Il informe ensuite le composant frontal enregistré que le modèle a été modifié.

## Routage manuel/automatique du modèle {#manual-vs-automatic-model-routing}

Le `ModelRouter` système automatise la récupération des fragments du modèle. Mais comme n&#39;importe quel outil automatisé, il comporte des limites. Au besoin, vous `ModelRouter` pouvez désactiver ou configurer la fonction afin d’ignorer les chemins à l’aide des propriétés des métadonnées (voir la section Propriétés des métadonnées du document Composant [de page](/help/sites-developing/spa-page-component.md) d’application d’une seule page). Les développeurs frontaux peuvent alors mettre en oeuvre leur propre couche de routage de modèle en demandant à l’opérateur `PageModelManager` de charger tout fragment de modèle donné à l’aide de la `getData()` fonction.

>[!NOTE]
>
>Actuellement, l&#39;exemple de projet React du journal We.Retail illustre l&#39;approche automatisée tandis que le projet Angular illustre l&#39;approche manuelle. Une approche semi-automatisée serait également un cas d&#39;utilisation valide.

>[!CAUTION]
>
>La version actuelle de `ModelRouter` ne prend en charge que l’utilisation d’URL pointant vers le chemin de ressource réel des points d’entrée du modèle Sling. Il ne prend pas en charge l&#39;utilisation d&#39;URL ou d&#39;alias Vanity.

## Contrat de routage {#routing-contract}

L’implémentation actuelle repose sur l’hypothèse que le projet SPA utilise l’API d’historique HTML5 pour le routage vers les différentes pages de l’application.

### Configuration{#configuration}

Le `ModelRouter` système prend en charge le concept de routage de modèle, car il écoute `pushState` et `replaceState` appelle pour prérécupérer les fragments de modèle. En interne, il déclenche le chargement `PageModelManager` du modèle correspondant à une URL donnée et déclenche un `cq-pagemodel-route-changed` événement que d’autres modules peuvent écouter.

Par défaut, ce comportement est automatiquement activé. Pour le désactiver, l’application sur une seule page doit effectuer le rendu de la propriété meta suivante :

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Note that every route of the SPA should correspond to an accessible resource in AEM (e.g., &quot; `/content/mysite/mypage"`) since the `PageModelManager` will automatically try to load the corresponding page model once the route is selected. Though, if needed, the SPA can also define a &quot;black list&quot; of routes that should be ignored by the `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
