---
title: Notions fondamentales sur le catalogue
seo-title: Notions fondamentales sur le catalogue
description: Présentation du catalogue
seo-description: Présentation du catalogue
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 4%

---

# Notions fondamentales sur le catalogue {#catalog-essentials}

Cette page fournit les informations essentielles pour utiliser la fonctionnalité de catalogue des sites de la communauté d’activation.

La fonctionnalité de catalogue, lorsqu’elle est incluse dans un site de communauté, permet aux membres de la communauté de parcourir et de sélectionner les ressources d’activation répertoriées dans un catalogue.

Le [ `enablement catalog` composant](catalog.md) permet aux membres de la communauté d’accéder à un catalogue de [ressources d’activation](resources.md). L’utilisation des balises d’AEM est une partie importante de la gestion de l’aspect des ressources d’activation dans un catalogue.

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
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learning.path</td>
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
   <td>Voir <a href="catalog.md">Fonctionnalité de catalogue</a></td>
  </tr>
 </tbody>
</table>

## Principes élémentaires côté serveur {#essentials-for-server-side}

### Fonction Catalogue {#catalog-function}

Une structure de site de communauté qui inclut la [fonction de catalogue](functions.md#catalog-function), comprend un composant `enablement catalog` configuré.

### Pré-filtres {#pre-filters}

Lorsqu’une fonction de catalogue a été ajoutée à un site de communauté, il est possible de restreindre les ressources d’activation et les chemins d’apprentissage qui apparaissent dans le catalogue en spécifiant un préfiltre. Pour ce faire, définissez les propriétés sur l’instance de la ressource de catalogue pour le site.

Utilisation de l’exemple du [tutoriel d’activation](getting-started-enablement.md) :

* À l’auteur
* Utilisation de [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Par exemple [https://&lt;serveur>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Accédez à la ressource de catalogue sur la page de catalogue.

   * Par exemple, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Ajout d’un noeud de filtres enfants

   * Sélectionnez le noeud `catalog`
   * Sélectionnez **[!UICONTROL Créer un noeud]**

      * Nom : `filters`
      * Type : `nt:unstructured`
      * Sélectionnez **[!UICONTROL Enregistrer tout]**.

* Ajoutez la propriété `se_resource-tags` au noeud `filters`

   * Sélectionnez le noeud `filters`
   * Ajout d’une propriété multiple

      * Nom : `se_resource-tags`
      * Type : chaîne
      * Valeur : *&lt;saisissez un [ID de balise](#pre-filter-tagids)*
         * Sélectionnez **[!UICONTROL Multi]**
         * Sélectionnez **[!UICONTROL Ajouter]**

            * Dans la boîte de dialogue contextuelle, sélectionnez `+` pour ajouter d’autres ID de balise préfiltrés.

* Republier le site de la communauté

![configure-catalog](assets/configure-catalog.png)

#### Préfiltrer les ID de balise {#pre-filter-tagids}

Le préfiltre [TagIDs](../../help/sites-developing/framework.md#tagid) doit correspondre exactement aux balises appliquées aux ressources d’activation. Elles sont visibles dans le dossier `resources` du site en tant que valeurs de la propriété `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### API de référence {#reference-apis}

* [API d’activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API de création de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)
