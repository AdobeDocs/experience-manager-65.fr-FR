---
title: Activation de l’exportateur JSON pour un composant
description: Les composants peuvent être adaptés pour générer l’exportation JSON de leur contenu en fonction d’un framework de modeleur.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 69%

---

# Activation de l’exportateur JSON pour un composant{#enabling-json-export-for-a-component}

Les composants peuvent être adaptés pour générer l’exportation JSON de leur contenu en fonction d’un framework de modeleur.

## Vue d’ensemble {#overview}

L’exportation JSON est basée sur des [modèles Sling](https://sling.apache.org/documentation/bundles/models.html) et sur le framework d’[exportation des modèles Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (lequel s’appuie lui-même sur des [annotations Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Cela signifie que le composant doit disposer d’un modèle Sling s’il doit exporter le fichier JSON. Par conséquent, suivez ces deux étapes pour activer l’exportation JSON sur n’importe quel composant.

* [Définition d’un modèle Sling pour le composant](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotation de l’interface du modèle Sling](#annotate-the-sling-model-interface)

## Définition d’un modèle Sling pour le composant {#define-a-sling-model-for-the-component}

Il faut d’abord définir un modèle Sling pour le composant.

>[!NOTE]
>
>Pour obtenir un exemple d’utilisation des modèles Sling, voir [Développement d’exportateurs de modèles Sling dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=fr).

La classe de mise en œuvre des modèles Sling doit être annotée comme suit :

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Cela garantit que votre composant peut être exporté seul, à l’aide du sélecteur `.model` de l’extension `.json`.

En outre, cela indique que la classe de modèles Sling peut être adaptée dans l’interface `ComponentExporter`.

>[!NOTE]
>
>Les annotations Jackson ne sont pas spécifiées au niveau de la classe de modèle Sling, mais plutôt au niveau de l’interface de modèle. Cela permet de s’assurer que l’exportation du code JSON est considéré comme faisant partie de l’API du composant.

>[!NOTE]
>
>Les classes `ExporterConstants` et `ComponentExporter` proviennent du lot `com.adobe.cq.export.json`.

### Utilisation de plusieurs sélecteurs {#multiple-selectors}

Bien qu’il ne s’agisse pas d’un cas d’utilisation standard, il est possible de configurer plusieurs sélecteurs en plus du sélecteur `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Toutefois, dans ce cas, le sélecteur `model` doit être le premier et l’extension doit être `.json`.

## Annotation de l’interface du modèle Sling {#annotate-the-sling-model-interface}

Pour être prise en compte par la structure de l’exportateur JSON, l’interface du modèle doit mettre en oeuvre la variable `ComponentExporter` (ou `ContainerExporter`, s’il existe un composant de conteneur).

L’interface de modèle Sling correspondante (`MyComponent`) est alors marquée avec les [annotations Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) pour définir la manière dont les méthodes doivent être exportées (sérialisées).

L’interface de modèle doit être correctement annotée afin de définir les méthodes à sérialiser. Par défaut, toutes les méthodes qui respectent la convention de nommage habituelle pour les getters sont sérialisées et leur nom de propriété JSON est dérivé naturellement des noms getter. Cela peut être évité en utilisant `@JsonIgnore` ou `@JsonProperty` pour renommer la propriété JSON.

## Exemple {#example}

Les composants principaux prennent en charge l’exportation JSON depuis la version [1.1.0 des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) et peut être utilisé comme référence.

Pour obtenir un exemple, consultez la mise en œuvre du modèle Sling sur le composant principal de l’image et son interface annotée.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-core-wcm-components sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip).

## Documentation connexe {#related-documentation}

Pour plus d’informations, voir :

* la [rubrique Fragments de contenu du guide de l’utilisateur Assets](https://helpx.adobe.com/fr/erience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js).

* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)
* [Création à l’aide de fragments de contenu](/help/sites-authoring/content-fragments.md)
* [Exportateur JSON pour Content Services](/help/sites-developing/json-exporter.md)
* [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) et [composant Fragment de contenu](https://helpx.adobe.com/fr/experience-manager/core-components/using/content-fragment-component.html)
