---
title: Créer un composant de champ d’IU Granite
description: L’interface utilisateur Granite fournit toute une gamme de composants conçus pour être utilisés dans les formulaires. Ils sont appelés champs.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 100%

---

# Créer un composant de champ d’IU Granite{#creating-a-new-granite-ui-field-component}

L’IU Granite fournit toute une gamme de composants conçus pour être utilisés dans des formulaires. Ils sont appelés *champs* selon la terminologie de l’IU Granite. Les composants de formulaire Granite standard sont disponibles sous :

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Ces champs de formulaire de l’interface utilisateur Granite sont particulièrement intéressants, car ils sont utilisés pour les [boîtes de dialogue de composant](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Pour plus d’informations sur les champs, reportez-vous à la [documentation sur l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Utilisez le framework de base de l’interface utilisateur de Granite pour développer et/ou étendre les composants Granite. Il comporte deux éléments :

* côté serveur :

   * une collection de composants de base

      * base : modulaire, composable, lisible, réutilisable
      * Composants : composants Sling

   * aide au développement des applications

* côté client :

   * une collection de bibliothèques clientes fournissant un certain vocabulaire (c’est-à-dire une extension du langage HTML) pour obtenir des modèles d’interaction génériques par le biais d’une interface utilisateur pilotée par Hypermedia.

Le composant d’IU Granite générique `field` se compose de deux fichiers d’intérêt :

* `init.jsp` : gère le traitement générique ; le balisage et la description, et fournit la valeur de formulaire dont vous avez besoin lors du rendu du champ.
* `render.jsp` : il s’agit de l’emplacement où le rendu du champ est effectué, il doit être remplacé pour votre champ personnalisé ; il est inclus par `init.jsp`.

Voir [Documentation de l’interface utilisateur Granite - Champ](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) pour plus d’informations.

Pour consulter des exemples, voir :

* `cqgems/customizingfield/components/colorpicker`

   * fourni par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Ce mécanisme utilisant JSP, i18n et XSS ne sont pas fournis prêts à l’emploi. Cela signifie que vous devez internationaliser et échapper vos chaînes. Le répertoire suivant contient les champs génériques d’une instance standard. Vous pouvez les utiliser comme référence :
>
>Référentiel `/libs/granite/ui/components/foundation/form`

## Création du script côté serveur pour le composant {#creating-the-server-side-script-for-the-component}

Le champ personnalisé doit remplacer uniquement le script `render.jsp`, où vous fournissez le balisage de votre composant. Vous pouvez considérer le JSP (c’est-à-dire le script de rendu) comme un wrapper pour votre balisage.

1. Créez un composant qui utilise la propriété `sling:resourceSuperType` à hériter de :

   `/libs/granite/ui/components/foundation/form/field`

1. Remplacez le script :

   `render.jsp`

   Dans ce script, générez le balisage hypermédia (c’est-à-dire enrichi, contenant l’abordage hypermédia) afin que le client puisse interagir avec l’élément généré. Cela doit respecter le style de codage côté serveur de l’interface utilisateur de Granite.

   Lors de la personnalisation, vous *devez* avoir lu la valeur du formulaire (initialisée dans `init.jsp`) à partir de la requête à l’aide de :

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Pour plus d’informations, consultez la mise en œuvre des champs prêts à l’emploi de l’interface utilisateur de Granite, par exemple, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Actuellement, privilégiez JSP comme méthode de script, car la transmission d’informations d’un composant à un autre (fréquente dans le contexte d’un formulaire/de champs) n’est pas facile à réaliser en HTL.

## Créer la bibliothèque cliente pour le composant {#creating-the-client-library-for-the-component}

Pour ajouter un comportement client spécifique à votre composant :

1. Créez une bibliothèque cliente de la catégorie `cq.authoring.dialog`.
1. Créez une bibliothèque cliente de la catégorie `cq.authoring.dialog` et définissez votre `CSS`/`JS` à l’intérieur de celle-ci.

   Définissez votre `CSS`/`JS` à l’intérieur de la bibliothèque cliente.

   >[!NOTE]
   >
   >Actuellement, l’interface utilisateur Granite ne fournit aucun écouteur ou hook prêts à l’emploi pour ajouter un comportement JS. Ainsi, pour ajouter un comportement JS supplémentaire à votre composant, vous devez implémenter un hook JS à une classe personnalisée que vous affectez ensuite à votre composant pendant la génération du balisage.
