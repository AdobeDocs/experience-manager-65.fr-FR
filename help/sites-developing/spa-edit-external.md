---
title: Modification d’une SPA externe dans AEM
description: Ce document décrit les étapes recommandées pour charger une SPA autonome vers une instance AEM, ajouter des sections de contenu modifiables et permettre la création.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 99%

---

# Modification d’une SPA externe dans AEM {#editing-external-spa-within-aem}

Lorsque vous décidez du niveau d’intégration que vous souhaitez entre votre SPA externe et votre AEM, vous devez souvent modifier et afficher la SPA dans AEM.

## Présentation {#overview}

Ce document décrit les étapes recommandées pour charger une SPA autonome vers une instance AEM, ajouter des sections de contenu modifiables et permettre la création.

## Conditions préalables {#prerequisites}

Les conditions préalables sont simples.

* Assurez-vous que l’instance d’AEM s’exécute localement.
* Créez un projet de base de SPA AEM à l’aide de [l’archétype de projet AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr?#available-properties)
   * Il servira de base au projet AEM qui sera mis à jour pour inclure la SPA externe.
   * Pour les exemples de ce document, nous utilisons [le projet SPA WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=fr#spa-editor) comme point de départ.
* Gardez la SPA React externe que vous souhaitez intégrer active et à portée de main.

## Chargement de la SPA vers le projet AEM {#upload-spa-to-aem-project}

Vous devez tout d’abord charger la SPA externe vers votre projet AEM.

1. Remplacez `src` dans le dossier de projet `/ui.frontend` par le dossier `src` de votre application React.
1. Incluez toutes les dépendances supplémentaires dans le `package.json` de l’application dans le fichier `/ui.frontend/package.json`.
   * Vérifiez que les versions des dépendances du SDK de la SPA font partie des [versions recommandées.](spa-getting-started-react.md#dependencies)
1. Incluez toutes les personnalisations dans le dossier `/public`.
1. Incluez tous les scripts ou styles intégrés ajoutés dans le fichier `/public/index.html`.

## Configuration de la SPA distante {#configure-remote-spa}

Maintenant que la SPA externe fait partie de votre projet AEM, vous devez la configurer dans AEM.

### Inclusion des modules du SDK SPA Adobe {#include-spa-sdk-packages}

Pour tirer parti des fonctionnalités de SPA AEM, vous pouvez utiliser les dépendances des trois modules suivants.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` fournit l’API permettant d’initialiser un gestionnaire de modèle et de récupérer le modèle à partir de l’instance AEM. Ce modèle peut ensuite être utilisé pour effectuer le rendu des composants AEM à l’aide d’API provenant de `@adobe/aem-react-editable-components` et `@adobe/aem-spa-component-mapping`.

#### Installation {#installation}

Exécutez la commande npm suivante pour installer les modules requis.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Initialisation de ModelManager {#model-manager-initialization}

Avant le rendu de l’application, [`ModelManager`](spa-blueprint.md#pagemodelmanager) doit être initialisé pour gérer la création du `ModelStore` AEM.

Cette opération doit être effectuée dans le fichier `src/index.js` de votre application ou à l’endroit où la racine de l’application est générée.

Pour ce faire, nous pouvons utiliser l’API `initializationAsync` fournie par le `ModelManager`.

La capture d’écran suivante montre comment activer l’initialisation de `ModelManager` dans une application React simple. La seule contrainte est que `initializationAsync` doit être appelé avant `ReactDOM.render()`.

![Initialiser ModelManager](assets/external-spa-initialize-modelmanager.png)

Dans cet exemple, `ModelManager` est initialisé et un `ModelStore` vide est créé.

`initializationAsync` peut éventuellement accepter un objet `options` comme paramètre :

* `path` - Lors de l’initialisation, le modèle au niveau du chemin d’accès défini est récupéré et stocké dans le `ModelStore`. Vous pouvez l’utiliser pour récupérer le `rootModel` à l’initialisation, si nécessaire.
* `modelClient` - Permet de fournir un client personnalisé chargé de récupérer le modèle.
* `model` - Un objet `model` transmis en tant que paramètre généralement renseigné lors de l’[utilisation de SSR.](spa-ssr.md)

### Composants feuille AEM modifiables {#authorable-leaf-components}

1. Créez/identifiez un composant AEM pour lequel un composant React modifiable sera créé. Dans cet exemple, nous utilisons le composant texte du projet WKND.

   ![Composant texte WKND](assets/external-spa-text-component.png)

1. Créez un simple composant texte React dans la SPA. Dans cet exemple, un nouveau fichier `Text.js` a été créé avec le contenu suivant.

   ![Text.js](assets/external-spa-textjs.png)

1. Créez un objet de configuration pour spécifier les attributs requis pour activer la modification AEM.

   ![Créer un objet de configuration](assets/external-spa-config-object.png)

   * `resourceType` est nécessaire pour pouvoir mapper le composant React au composant AEM et activer la modification lors de l’ouverture dans l’éditeur AEM.

1. Utilisez la fonction Wrapper `withMappable`.

   ![Utiliser withMappable](assets/external-spa-withmappable.png)

   Cette fonction Wrapper mappe le composant React au `resourceType` AEM spécifié dans la configuration et active les capacités de modification en l’ouvrant dans l’éditeur AEM. Pour les composants autonomes, cette fonction récupère également le contenu du modèle pour le nœud spécifique.

   >[!NOTE]
   >
   >Dans cet exemple, il existe des versions distinctes du composant : les composants AEM encapsulés et les composants React non encapsulés. La version encapsulée doit être utilisée lors de l’utilisation explicite du composant. Lorsque le composant fait partie d’une page, vous pouvez continuer à utiliser le composant par défaut comme dans l’éditeur de SPA.

1. Générez le contenu dans le composant.

   Les propriétés JCR du composant texte apparaissent comme suit dans AEM.

   ![Propriétés du composant texte](assets/external-spa-text-properties.png)

   Ces valeurs sont transmises en tant que propriétés au nouveau du composant React `AEMText` et peuvent être utilisées pour générer le contenu.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   C’est ainsi que le composant apparaîtra une fois que les configurations AEM sont terminées.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >Dans cet exemple, nous avons apporté d’autres personnalisations au composant rendu pour qu’il corresponde au composant texte existant. Cette personnalisation n’est toutefois pas liée à la création dans AEM.

#### Ajout de composants modifiables à la page {#add-authorable-component-to-page}

Une fois les composants React modifiables créés, nous pouvons les utiliser dans toute l’application.

Prenons un exemple de page dans lequel nous devons ajouter un texte du projet SPA WKND. Pour cet exemple, nous voulons afficher le texte « Hello World! » à `/content/wknd-spa-react/us/en/home.html`.

1. Déterminez le chemin d’accès du nœud à afficher.

   * `pagePath` : page qui contient le nœud, dans notre exemple `/content/wknd-spa-react/us/en/home`
   * `itemPath` : chemin d’accès au nœud dans la page, dans notre exemple `root/responsivegrid/text`
      * Il s’agit des noms des éléments contenant sur la page.

   ![Chemin du nœud](assets/external-spa-path.png)

1. Ajoutez le composant à la position requise sur la page.

   ![Ajouter des composants à la page](assets/external-spa-add-component.png)

   Le composant `AEMText` peut être ajouté à la position requise sur la page avec les valeurs `pagePath` et `itemPath` définies en tant que propriétés. `pagePath` est une propriété obligatoire.

#### Vérification de la modification du contenu texte dans AEM {#verify-text-edit}

Nous pouvons maintenant tester le composant sur notre instance AEM en cours d’exécution.

1. Exécutez la commande Maven suivante à partir du répertoire `aem-guides-wknd-spa` pour générer et déployer le projet sur AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Sur votre instance AEM, accédez à `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Modification de la SPA dans AEM](assets/external-spa-edit-aem.png)

Le composant `AEMText` est désormais modifiable sur AEM.

### Pages AEM modifiables {#aem-authorable-pages}

1. Identifiez une page à ajouter pour la création dans la SPA. Cet exemple utilise `/content/wknd-spa-react/us/en/home.html`.
1. Créez un fichier (ex. `Page.js`) pour le composant de page modifiable. Ici, nous pouvons réutiliser le composant de page fourni dans `@adobe/cq-react-editable-components`.
1. Répétez l’étape 4 de la section [Composants feuille AEM modifiables.](#authorable-leaf-components) Utilisez la fonction Wrapper `withMappable` sur le composant.
1. Comme précédemment, appliquez `MapTo` aux types de ressources AEM pour tous les composants enfants de la page.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >Dans cet exemple, nous utilisons le composant texte React non encapsulé au lieu du composant `AEMText` encapsulé créé précédemment. En effet, lorsque le composant fait partie d’une page ou d’un conteneur et n’est pas autonome, le conteneur s’occupe de mapper le composant de manière récursive et d’activer les fonctionnalités de création ; le Wrapper supplémentaire n’est donc pas nécessaire pour chaque enfant.

1. Pour ajouter une page autorisée dans la SPA, suivez les mêmes étapes de la section [Ajout de composants modifiables à la page.](#add-authorable-component-to-page) Ici, nous pouvons cependant passer l’étape de la propriété `itemPath`.

#### Vérification du contenu de la page sur AEM {#verify-page-content}

Pour vérifier que la page peut être modifiée, suivez les mêmes étapes que dans la section [Vérification de la modification du contenu texte dans AEM.](#verify-text-edit)

![Modification d’une page dans AEM](assets/external-spa-edit-page.png)

La page est désormais modifiable dans AEM avec un conteneur de disposition et un composant texte enfant.

### Composants feuille virtuels {#virtual-leaf-components}

Dans les exemples précédents, nous avons ajouté des composants au SPA avec le contenu AEM existant. Toutefois, il arrive que le contenu n’ait pas encore été créé dans AEM, mais qu’il doive être ajouté ultérieurement par l’auteur du contenu. Pour ce faire, le développeur principal peut ajouter des composants aux emplacements appropriés dans la SPA. Ces composants affichent des espaces réservés lorsqu’ils sont ouverts dans l’éditeur dans AEM. Une fois que le contenu est ajouté par l’auteur du contenu dans ces espaces réservés, les nœuds sont créés dans la structure JCR et le contenu est conservé. Le composant créé permet le même ensemble d’opérations que les composants feuille autonomes.

Dans cet exemple, nous réutilisons le composant `AEMText` créé précédemment. Nous voulons ajouter un nouveau texte sous le composant texte existant sur la page d’accueil WKND. L’ajout de composants est le même que pour les composants feuille normaux. Cependant, `itemPath` peut être mis à jour avec le chemin d’accès pour le nouveau composant.

Puisque le nouveau composant doit être ajouté sous le texte existant sous `root/responsivegrid/text`, le nouveau chemin d’accès sera `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

Le composant `TestPage` ressemble à ce qui suit après l’ajout du composant virtuel.

![Test du composant virtuel](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Assurez-vous que le composant `AEMText` a son `resourceType` défini dans la configuration pour activer cette fonction.

Vous pouvez maintenant déployer les modifications sur AEM en suivant les étapes de la section [Vérification de la modification du contenu texte dans AEM.](#verify-text-edit) Un espace réservé sera affiché pour le nœud encore non existant `text_20`.

![Le nœud text_20 dans aem](assets/external-spa-text20-aem.png)

Lorsque l’auteur du contenu met à jour ce composant, un nœud `text_20` est créé sur `root/responsivegrid/text_20` dans `/content/wknd-spa-react/us/en/home`.

![Le nœud text20](assets/external-spa-text20-node.png)

#### Exigences et restrictions {#limitations}

Il existe un certain nombre d’exigences à satisfaire pour ajouter des composants feuille virtuels, ainsi que certaines restrictions.

* La propriété `pagePath` est obligatoire pour créer un composant virtuel.
* Le nœud de page fourni au chemin d’accès dans `pagePath` doit exister dans le projet AEM.
* Le nom du nœud à créer doit être fourni dans le `itemPath`.
* Le composant peut être créé à n’importe quel niveau.
   * Si nous fournissons un `itemPath='text_20'` dans l’exemple précédent, le nœud sera créé directement sous la page, c.-à-d. `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* Le chemin d’accès où le nœud doit être créé doit être valide lorsqu’il est fourni par `itemPath`.
   * Dans cet exemple, `root/responsivegrid` doit exister pour que le nœud `text_20` puisse y être créé.
* Seule la création de composants feuille est prise en charge. Les conteneurs et pages virtuels seront pris en charge dans les versions futures.

## Personnalisations supplémentaires {#additional-customizations}

Si vous avez suivi les exemples précédents, votre SPA externe est désormais modifiable dans AEM. Cependant, vous pouvez personnaliser encore davantage d’autres aspects de votre SPA externe.

### ID de nœud racine {#root-node-id}

Par défaut, nous supposons que l’application React est rendue dans un `div` de l’ID d’élément `spa-root`. Il est possible si nécessaire de personnaliser cette fonction.

Par exemple, supposons que nous ayons une SPA dans lequel l’application est rendue dans un `div` de l’ID d’élément `root`. Il faut que cet élément se reflète dans trois fichiers.

1. Dans le fichier `index.js` de l’application React (ou à l’endroit où `ReactDOM.render()` est appelé)

   ![ReactDOM.render() dans le fichier index.js](assets/external-spa-root-index.png)

1. Dans le fichier `index.html` de l’application React

   ![Index.html de l’application](assets/external-spa-index.png)

1. Dans le corps du composant de page de l’application AEM, opération possible en deux étapes :

   1. Créez un fichier `body.html` pour le composant de page.

   ![Création d’un fichier body.html](assets/external-spa-update-body.gif)

   1. Ajoutez le nouvel élément racine dans le nouveau fichier `body.html`.

   ![Ajouter l’élément racine à body.html](assets/external-spa-add-root.png)

### Modification d’une SPA React avec le routage {#editing-react-spa-with-routing}

Si l’application SPA React externe comporte plusieurs pages, [elle peut utiliser le routage pour déterminer la page ou le composant à rendre.](spa-routing.md) Le cas d’utilisation typique consiste à faire correspondre l’URL actuellement principale au chemin d’accès fourni pour un itinéraire. Pour activer la modification sur de telles applications activées pour le routage, le chemin d’accès à comparer doit être modifié pour pouvoir s’adapter aux informations spécifiques à AEM.

Dans l’exemple suivant, nous avons une application React simple de deux pages. La page à rendre est déterminée en comparant le chemin d’accès fourni au routeur avec l’URL active. Par exemple, si nous suivons `mydomain.com/test`, `TestPage` sera rendu.

![Routage dans une SPA externe](assets/external-spa-routing.png)

Pour activer la modification dans AEM pour cet exemple de SPA, vous devez suivre les étapes suivantes.

1. Identifiez le niveau racine pour AEM.

   * Pour notre échantillon, nous considérons `wknd-spa-react/us/en` comme la racine du SPA. Cela signifie que tout ce qui précède ce chemin ne concerne que des pages ou du contenu AEM.

1. Créez une page au niveau requis.

   * Dans cet exemple, la page à modifier est `mydomain.com/test`. `test` se trouve dans le chemin racine de l’application. Ce paramètre doit également être conservé lors de la création de la page dans AEM. Par conséquent, nous pouvons créer une page au niveau racine défini à l’étape précédente.
   * La page créée doit porter le même nom que la page à modifier. Dans cet exemple, pour `mydomain.com/test`, la page créée doit être `/path/to/aem/root/test`.

1. Ajoutez des assistants pour le routage de la SPA.

   * La page nouvellement créée n’affichera pas encore le contenu attendu dans AEM. Cette absence est due au fait que le routeur cherche le chemin d’accès `/test` alors que le chemin d’accès principal d’AEM est `/wknd-spa-react/us/en/test`. Pour prendre en compte la partie spécifique à AEM de l’URL, nous devons ajouter des fonctions d’aide côté SPA.

   ![Fonction d’aide au routage](assets/external-spa-router-helper.png)

   * La fonction d’aide `toAEMPath` fournie par `@adobe/cq-spa-page-model-manager` peut être utilisée pour cela. Elle adapte le chemin d’accès fourni pour que le routage intègre les portions spécifiques à AEM lorsque l’application est ouverte sur une instance AEM. Elle accepte trois paramètres :
      * Le chemin d’accès requis pour le routage
      * L’URL d’origine de l’instance AEM dans laquelle la SPA est modifiée
      * La racine du projet sur AEM, telle que déterminée lors de la première étape
   * Ces valeurs peuvent être définies en tant que variables d’environnement pour plus de flexibilité.



1. Vérifiez la modification de la page dans AEM.

   * Déployez le projet pour AEM et accédez à la page `test` créée. Le contenu de la page est désormais rendu et les composants AEM sont modifiables.

## Ressources supplémentaires {#additional-resources}

Les documents de référence suivants peuvent être utiles pour comprendre le fonctionnement des SPA dans le contexte d’AEM.

* [Archétype de projet AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr)
* [Projet de SPA WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=fr)
* [Prise en main des SPA dans AEM avec React](spa-getting-started-react.md)
* [Documents de référence relatifs aux SPA (référence de l’API)](spa-reference-materials.md)
* [Plan directeur d’applications sur une seule page (SPA) et PageModelManager](spa-blueprint.md#pagemodelmanager)
* [Routage du modèle de SPA ](spa-routing.md)
* [SPA et rendu côté serveur ](spa-ssr.md)
