---
title: Création d’un composant de champ d’IU Granite
seo-title: Création d’un composant de champ d’IU Granite
description: L’IU Granite fournit toute une gamme de composants conçus pour être utilisés dans des formulaires, appelés champs.
seo-description: L’IU Granite fournit toute une gamme de composants conçus pour être utilisés dans des formulaires, appelés champs.
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 89%

---


# Création d’un composant de champ d’IU Granite{#creating-a-new-granite-ui-field-component}

L’IU Granite fournit toute une gamme de composants conçus pour être utilisés dans des formulaires. Ils sont appelés *champs* selon la terminologie de l’IU Granite. Les composants de formulaire Granite standard sont disponibles sous :

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Ces champs de formulaire d’IU Granite présentent un intérêt particulier dans la mesure où ils sont utilisés pour les [boîtes de dialogue de composant](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Pour plus d’informations sur les champs, consultez la [documentation de l’IU Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilisez la structure de base de l’IU Granite pour développer et/ou étendre les composants Granite. Elle comprend deux éléments :

* Côté serveur :

   * Une collection de composants de base

      * Base : modulaires, composables, pouvant être disposés en couche, réutilisables
      * Composants : composants Sling
   * Des aides au développement d’applications


* Côté client :

   * Une collection de clientlibs fournissant un certain vocabulaire (c’est-à-dire une extension du langage HTML) pour obtenir des motifs génériques d’interaction via une IU pilotée par hypermédia.

Le composant générique de l’interface utilisateur Granite `field` est composé de deux fichiers présentant un intérêt :

* `init.jsp` : gère le traitement générique ; le balisage et la description, et fournit la valeur de formulaire dont vous aurez besoin lors du rendu du champ.
* `render.jsp` : il s’agit de l’emplacement où le rendu du champ est effectué et doit être remplacé pour votre champ personnalisé ; il est inclus par `init.jsp`.

Reportez-vous à la [documentation de l’IU Granite – champ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) si vous souhaitez plus de détails.

Pour consulter des exemples, voir :

* `cqgems/customizingfield/components/colorpicker`

   * Fourni par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Ce mécanisme utilisant JSP, i18n et XSS ne sont pas fournis prêts à l’emploi. Cela signifie que vous devez internationaliser et placer les chaînes dans des séquences d’échappement. Le répertoire suivant contient les champs génériques d’une instance standard. Vous pouvez les utiliser comme référence :
>
>`/libs/granite/ui/components/foundation/form`,

## Création du script côté serveur pour le composant {#creating-the-server-side-script-for-the-component}

Le champ personnalisé doit remplacer uniquement le script `render.jsp`, où vous fournissez le balisage de votre composant. Vous pouvez considérer le JSP (c’est-à-dire le script de rendu) comme un wrapper pour votre balisage.

1. Créez un composant qui utilise la propriété `sling:resourceSuperType` à hériter de :

   `/libs/granite/ui/components/foundation/form/field`

1. Remplacez le script :

   `render.jsp`

   Dans ce script, vous devez générer le balisage hypermédia (par exemple, le balisage enrichi contenant l’affordance hypermédia), de sorte que le client sache interagir avec l’élément généré. Cela doit suivre le style de codage côté serveur de l’IU Granite.

   Lors de la personnalisation, vous *devez* avoir lu la valeur du formulaire (initialisée dans `init.jsp`) à partir de la requête à l’aide de :

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Pour plus de détails, reportez-vous à la mise en oeuvre des champs d’interface utilisateur Granite prêts à l’emploi ; par exemple, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Pour le moment, JSP est la méthode de script préférée, car il n’est pas aisé de transmettre des informations d’un composant à l’autre (ce qui est assez fréquent dans le cadre du formulaire/des champs) en HTL.

## Création de la bibliothèque cliente pour le composant {#creating-the-client-library-for-the-component}

Pour ajouter un comportement côté client spécifique à votre composant :

1. Créez une bibliothèque cliente de la catégorie `cq.authoring.dialog`.
1. Créez une bibliothèque cliente de catégorie `cq.authoring.dialog` et définissez votre `JS`/ `CSS` à l&#39;intérieur.

   Définissez votre `JS`/ `CSS` dans la bibliothèque cliente.

   >[!NOTE]
   >
   >Actuellement, l’IU Granite ne propose aucun écouteur ou crochet de dialogue prêt à l’emploi que vous pouvez utiliser directement pour ajouter un comportement JS. Ainsi, pour ajouter un comportement JS supplémentaire à votre composant, vous devez mettre en œuvre un crochet JS sur une classe personnalisée que vous attribuez ensuite à votre composant lors de la génération du balisage.

