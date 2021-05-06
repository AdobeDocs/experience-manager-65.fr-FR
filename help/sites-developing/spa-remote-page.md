---
title: Composant RemotePage
description: Le composant RemotePage est un composant de page personnalisé permettant de modifier les SPA React distantes dans AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
translation-type: tm+mt
source-git-commit: a92358d187aa78e05dd9b5a7bd4ae14bf0972f62
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---

# Composant RemotePage {#remote-page-component}

Lorsque vous décidez du niveau d’intégration vous souhaitez avoir entre votre SPA externe et votre instance AEM, il est souvent évident que vous devez être capable d’afficher et de modifier la SPA dans AEM. Le composant RemotePage est un composant de page personnalisé destiné uniquement à cette fin.

## Présentation {#overview}

Le composant RemotePage récupère toutes les ressources nécessaires à partir du `asset-manifest.json` généré par l’application et l’utilise pour effectuer le rendu des SPA dans AEM.

* La page distante vous permet d&#39;injecter les scripts et feuilles de style d&#39;un SPA dans le corps d&#39;un composant AEM Page.
* Les Composants Frontières virtuels permettent de marquer les sections comme modifiables dans AEM SPA Editor.
* Ensemble, un SPA hébergé sur un autre domaine peut être rendu modifiable dans AEM.

Voir l&#39;article [Modification d&#39;un SPA externe dans AEM](spa-edit-external.md) pour plus d&#39;informations sur les SPA externes modifiables dans l&#39;.

## Conditions préalables {#requirements}

* Activer CORS en développement
* Configurer l’URL distante dans les propriétés de page
* Effectuer le rendu de la SPA dans AEM
* L’application Web doit utiliser un manifeste de fichier de bundler comme l’un des suivants et exposer un fichier asset-manifest.json à la racine du domaine qui liste dans une propriété entrypoints tous les fichiers CSS et JS à charger :
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![Points d’entrée](assets/asset-manifest-entrypoints.png)

* L&#39;application doit être capable d&#39;initialiser dans un `<div id="root"></div>` sous l&#39;élément body. Si une autre annotation est attendue pour l’application à instancier, elle doit être ajustée en conséquence dans les scripts HTL du composant proxy qui possède une balise `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Restrictions {#limitations}

* L’implémentation actuelle du composant RemotePage ne prend en charge que les applications React distantes.
* La page CSS interne définie dans le fichier HTML racine de l’application ainsi que la page CSS intégrée sur le nœud DOM racine ne seront pas disponibles lors du rendu à distance dans AEM.

## Détails techniques {#technical-details}

Comme le reste du projet de SPA AEM, le composant RemotePage est disponible en open source. Pour obtenir les détails techniques complets concernant le composant RemotePage, [consultez le référentiel GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
