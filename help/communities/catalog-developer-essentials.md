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
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 4%

---


# Catalog Essentials {#catalog-essentials}

Cette page fournit les informations essentielles pour travailler avec la fonction de catalogue des sites de la communauté d&#39;activation.

La fonctionnalité de catalogue, lorsqu’elle est incluse dans un site communautaire, permet aux membres de la communauté de parcourir et de sélectionner les ressources d’activation répertoriées dans un catalogue.

Le composant [ `enablement catalog`](catalog.md) permet aux membres de la communauté d&#39;accéder à un catalogue de [ressources d&#39;activation](resources.md). L’utilisation de balises AEM est un élément important de la gestion de l’apparence des ressources d’activation dans un catalogue.

Voir [Ressources d’activation du balisage](tag-resources.md).

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
   <td>Voir <a href="catalog.md">Fonction du catalogue</a></td>
  </tr>
 </tbody>
</table>

## Essentials for Server-Side {#essentials-for-server-side}

### Fonction Catalogue {#catalog-function}

Une structure de site communautaire qui comprend la fonction [Catalog](functions.md#catalog-function), comprend un composant `enablement catalog` configuré.

### PréFiltres {#pre-filters}

Lorsqu’une fonction de catalogue a été ajoutée à un site communautaire, il est possible de limiter les ressources d’activation et les chemins d’apprentissage qui apparaissent dans le catalogue en spécifiant un préfiltre. Pour ce faire, définissez les propriétés sur l&#39;instance de la ressource de catalogue pour le site.

Utilisation de l&#39;exemple du [didacticiel d&#39;activation](getting-started-enablement.md) :

* Sur l’auteur
* Utilisation de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Par exemple [https://&lt;serveur>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Accédez à la ressource de catalogue sur la page de catalogue

   * Par exemple, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Ajouter un noeud de filtres enfant

   * Sélectionnez le noeud `catalog`
   * Sélectionnez **[!UICONTROL Créer un noeud]**

      * Nom : `filters`
      * Type : `nt:unstructured`
      * Sélectionner **[!UICONTROL Enregistrer tout]**

* Ajouter la propriété `se_resource-tags` au noeud `filters`

   * Sélectionnez le noeud `filters`
   * Ajouter une propriété multi

      * Nom : `se_resource-tags`
      * Type : chaîne
      * Valeur : *&lt;entrez un [ID de balise&lt;a2/&quot;*](#pre-filter-tagids)
         * Sélectionner **[!UICONTROL Multi]**
         * Sélectionner **[!UICONTROL Ajouter]**

            * Dans la boîte de dialogue contextuelle, sélectionnez `+` pour ajouter d’autres ID de balise préfiltrés.

* Republier le site de la communauté

![configure-catalog](assets/configure-catalog.png)

#### Identifiants de balise préfiltrés {#pre-filter-tagids}

Le préfiltre [TagIDs](../../help/sites-developing/framework.md#tagid) doit correspondre exactement aux balises appliquées aux ressources d&#39;activation. Elles sont visibles dans le dossier `resources` du site en tant que valeurs de la propriété `se_resource-tags`.

![configure-filtres](assets/configure-catalog1.png)

### API de référence {#reference-apis}

* [API d&#39;activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API d&#39;analyse de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

