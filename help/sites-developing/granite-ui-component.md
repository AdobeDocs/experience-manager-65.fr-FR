---
title: Créer un composant de champ d’IU Granite
description: L’interface utilisateur Granite fournit toute une gamme de composants conçus pour être utilisés dans les formulaires, appelés champs.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 28%

---

# Créer un composant de champ d’IU Granite{#creating-a-new-granite-ui-field-component}

L’IU Granite fournit toute une gamme de composants conçus pour être utilisés dans des formulaires. Ils sont appelés *champs* selon la terminologie de l’IU Granite. Les composants de formulaire Granite standard sont disponibles sous :

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Ces champs de formulaire de l’IU Granite sont particulièrement intéressants, car ils sont utilisés pour [boîtes de dialogue de composant](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Pour plus d’informations sur les champs, voir [Documentation de l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Utilisez la structure de base de l’IU Granite pour développer et/ou étendre les composants Granite. Celui-ci comporte deux éléments :

* côté serveur :

   * un ensemble de composants de base ;

      * foundation : modulaire, composable, lisible, réutilisable
      * Composants : composants Sling

   * aide au développement des applications

* côté client :

   * un ensemble de clientlibs fournissant un certain vocabulaire (c’est-à-dire une extension du langage de HTML) pour obtenir des modèles d’interaction génériques par le biais d’une interface utilisateur pilotée par Hypermedia.

Le composant d’IU Granite générique `field` se compose de deux fichiers d’intérêt :

* `init.jsp`: gère le traitement générique ; l’étiquetage, la description et fournissent la valeur de formulaire dont vous avez besoin lors du rendu de votre champ.
* `render.jsp`: c’est là que le rendu réel du champ est effectué et doit être remplacé pour votre champ personnalisé ; est inclus par `init.jsp`.

Voir [Documentation de l’IU Granite - Champ](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) pour plus d’informations.

Pour consulter des exemples, voir :

* `cqgems/customizingfield/components/colorpicker`

   * fourni par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Ce mécanisme utilisant JSP, i18n et XSS ne sont pas fournis prêts à l’emploi. Cela signifie que vous devez internationaliser et échapper vos chaînes. Le répertoire suivant contient les champs génériques d&#39;une instance standard. Vous pouvez les utiliser comme référence :
>
>Référentiel `/libs/granite/ui/components/foundation/form`

## Création du script côté serveur pour le composant {#creating-the-server-side-script-for-the-component}

Le champ personnalisé doit remplacer uniquement le script `render.jsp`, où vous fournissez le balisage de votre composant. Vous pouvez considérer le JSP (c’est-à-dire le script de rendu) comme un wrapper pour vos balises.

1. Créez un composant qui utilise la variable `sling:resourceSuperType` pour hériter de :

   `/libs/granite/ui/components/foundation/form/field`

1. Remplacez le script :

   `render.jsp`

   Dans ce script, générez le balisage hypermédia (c’est-à-dire enrichi, contenant l’abordage hypermédia) afin que le client sache interagir avec l’élément généré. Cela doit respecter le style de codage côté serveur de l’IU Granite.

   Lors de la personnalisation, vous *devez* avoir lu la valeur du formulaire (initialisée dans `init.jsp`) à partir de la requête à l’aide de :

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Pour plus d’informations, reportez-vous à la mise en oeuvre des champs d’interface utilisateur Granite prêts à l’emploi ; par exemple, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Actuellement, JSP est la méthode de script préférée, car la transmission d’informations d’un composant à un autre (fréquente dans le contexte d’un formulaire/de champs) n’est pas facile à réaliser dans HTL.

## Création de la bibliothèque-client pour le composant {#creating-the-client-library-for-the-component}

Pour ajouter un comportement client spécifique à votre composant :

1. Créez une bibliothèque cliente de la catégorie `cq.authoring.dialog`.
1. Créez une bibliothèque cliente de la catégorie `cq.authoring.dialog` et définissez votre `CSS`/`JS` à l’intérieur de celle-ci.

   Définissez votre `CSS`/`JS` à l’intérieur de la bibliothèque cliente.

   >[!NOTE]
   >
   >Actuellement, l’interface utilisateur Granite ne fournit aucun écouteur ou crochets prêts à l’emploi que vous pouvez utiliser directement pour ajouter un comportement JS. Ainsi, pour ajouter un comportement JS supplémentaire à votre composant, vous devez implémenter un crochet JS à une classe personnalisée que vous affectez ensuite à votre composant pendant la génération du balisage.
