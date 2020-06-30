---
title: Catalog Essentials
seo-title: Catalog Essentials
description: Présentation du catalogue
seo-description: Présentation du catalogue
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 5%

---


# Catalog Essentials {#catalog-essentials}

Cette page fournit les informations essentielles pour travailler avec la fonction de catalogue des sites de la communauté d&#39;activation.

La fonctionnalité de catalogue, lorsqu’elle est incluse dans un site communautaire, permet aux membres de la communauté de parcourir et de sélectionner les ressources d’activation répertoriées dans un catalogue.

The [ `enablement catalog` component](catalog.md) allows community members to access a catalog of [enablement resources](resources.md). L’utilisation de balises AEM est un élément important de la gestion de l’apparence des ressources d’activation dans un catalogue.

See [Tagging Enablement Resources](tag-resources.md).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activation/composants/hbs/catalogue</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /><br /> cq.social.enablement.hbs.resource cq.social.enablement.hbs.learning.path</td>
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
   <td>Voir Fonctionnalité <a href="catalog.md">du catalogue</a></td>
  </tr>
 </tbody>
</table>

## Essentials for Server-Side {#essentials-for-server-side}

### Fonction Catalogue {#catalog-function}

Une structure de site communautaire qui comprend la fonction [](functions.md#catalog-function)Catalogue, comprend un `enablement catalog` composant configuré.

### PréFiltres {#pre-filters}

Lorsqu’une fonction de catalogue a été ajoutée à un site communautaire, il est possible de limiter les ressources d’activation et les chemins d’apprentissage qui apparaissent dans le catalogue en spécifiant un préfiltre. Pour ce faire, définissez les propriétés sur l&#39;instance de la ressource de catalogue pour le site.

Utilisation de l’exemple du didacticiel [d’](getting-started-enablement.md)activation :

* Sur l’auteur
* Utilisation de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Par exemple [https://&lt;serveur>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Accédez à la ressource de catalogue sur la page de catalogue

   * Par exemple, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Ajouter un noeud de filtres enfant

   * Sélectionner le `catalog`noeud
   * Sélectionner **[!UICONTROL Créer un noeud]**

      * Nom : `filters`
      * Type : `nt:unstructured`
      * Select **[!UICONTROL Save All]**

* Ajouter `se_resource-tags` la propriété au `filters` noeud

   * Sélectionner le `filters` noeud
   * Ajouter une propriété multi

      * Nom (name) : `se_resource-tags`
      * Type : Chaîne
      * Valeur : *&lt;entrez un ID de[balise](#pre-filter-tagids)>*
         * Sélectionner **[!UICONTROL plusieurs]**
         * Sélectionner le **[!UICONTROL Ajoute]**

            * Dans la boîte de dialogue contextuelle, sélectionnez `+` l’option d’ajout d’identifiants de balise préfiltrés.

* Republier le site de la communauté

![chlimage_1-189](assets/chlimage_1-189.png)

#### Identifiants de balise préfiltrés {#pre-filter-tagids}

Les [TagID](../../help/sites-developing/framework.md#tagid) de préfiltre doivent correspondre exactement aux balises appliquées aux ressources d’activation. Elles sont visibles dans le `resources` dossier du site en tant que valeurs de la propriété `se_resource-tags`.

![chlimage_1-190](assets/chlimage_1-190.png)

### API de référence {#reference-apis}

* [API d&#39;activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API Rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API Rapports Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

