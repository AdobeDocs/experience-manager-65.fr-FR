---
title: Notions fondamentales sur le catalogue
seo-title: Catalog Essentials
description: Présentation du catalogue
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 6%

---

# Notions fondamentales sur le catalogue {#catalog-essentials}

Cette page fournit les informations essentielles pour utiliser la fonctionnalité de catalogue des sites de la communauté d’activation.

La fonctionnalité de catalogue, lorsqu’elle est incluse dans un site de communauté, permet aux membres de la communauté de parcourir et de sélectionner les ressources d’activation répertoriées dans un catalogue.

Le [ `enablement catalog` component](catalog.md) permet aux membres de la communauté d’accéder à un catalogue de [ressources d&#39;activation](resources.md). L’utilisation des balises d’AEM est une partie importante de la gestion de l’aspect des ressources d’activation dans un catalogue.

Voir [Balisage des ressources d’activation](tag-resources.md).

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="catalog.md">Fonctionnalité du catalogue</a></td>
  </tr>
 </tbody>
</table>

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

### Fonction Catalogue {#catalog-function}

Une structure de site de communauté qui inclut [Fonction Catalog](functions.md#catalog-function), inclut une `enablement catalog` composant.

### Pré-filtres {#pre-filters}

Lorsqu’une fonction de catalogue a été ajoutée à un site de communauté, il est possible de restreindre les ressources d’activation et les chemins d’apprentissage qui apparaissent dans le catalogue en spécifiant un préfiltre. Pour ce faire, définissez les propriétés sur l’instance de la ressource de catalogue pour le site.

En utilisant l’exemple de la fonction [Tutoriel sur l’activation](getting-started-enablement.md):

* À l’auteur
* Utilisation [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Par exemple : [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Accédez à la ressource de catalogue sur la page de catalogue.

   * Par exemple, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Ajout d’un noeud de filtres enfants

   * Sélectionnez la `catalog`node
   * Sélectionner **[!UICONTROL Créer un noeud]**

      * Nom : `filters`
      * Type : `nt:unstructured`
      * Sélectionnez **[!UICONTROL Enregistrer tout]**

* Ajouter `se_resource-tags` à la propriété `filters` node

   * Sélectionnez la `filters` node
   * Ajout d’une propriété multiple

      * Nom : `se_resource-tags`
      * Type : chaîne
      * Valeur : *&lt;enter a=&quot;&quot; span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />TagID](#pre-filter-tagids)>*[
         * Sélectionner **[!UICONTROL Multi]**
         * Sélectionnez **[!UICONTROL Ajouter]**

            * Dans la boîte de dialogue contextuelle, sélectionnez `+` pour ajouter d’autres ID de balise préfiltrés

* Republier le site de la communauté

![configure-catalog](assets/configure-catalog.png)

#### Préfiltrer les ID de balise {#pre-filter-tagids}

Le préfiltre [ID de balise](../../help/sites-developing/framework.md#tagid) doit correspondre exactement aux balises appliquées aux ressources d’activation. Elles sont visibles dans la variable `resources` dossier du site comme valeurs de la propriété `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### API de référence {#reference-apis}

* [API d’activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de création de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
