---
title: Mise à niveau des formulaires de recherche personnalisée
seo-title: Mise à niveau des formulaires de recherche personnalisée
description: 'Cet article décrit les réglages nécessaires après une mise à niveau pour les formulaires de recherche personnalisés. '
seo-description: 'Cet article décrit les réglages nécessaires après une mise à niveau pour les formulaires de recherche personnalisés. '
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 63%

---


# Mise à niveau des formulaires de recherche personnalisée{#upgrading-custom-search-forms}

Dans AEM 6.2, l’emplacement du référentiel où les formulaires de recherche personnalisée sont stockées a changé. Lors de la mise à niveau, ils sont déplacés de leur position de la version 6.1 :

* /apps/cq/gui/content/facets

vers un nouvel emplacement :

* /conf/global/settings/cq/search/facets

Pour cette raison, les réglages manuels sont nécessaires après une mise à niveau pour que les formulaires puissent continuer à fonctionner.

Cela s’applique aux nouveaux formulaires de recherche ainsi qu’aux formulaires par défaut qui ont été personnalisés.

Pour plus d’informations, consultez la documentation sur les [facettes de recherche](/help/assets/search-facets.md). 

## Modification de la propriété resourceType {#changing-the-resourcetype-property}

Sauf indication contraire, la plupart des réglages qui doivent être effectués après la mise à niveau nécessitent de modifier la propriét`sling:resourceType` pour les formulaires de recherche personnalisée configurés. Cela est nécessaire pour que la propriété puisse indiquer l’emplacement correct du script de rendu.

Vous pouvez modifier la propriété en procédant comme suit :

1. Open CRXDE Lite by going to `https://server:port/crx/de/index.jsp`
1. Accédez à l’emplacement du nœud qui doit être ajusté, tel que spécifié dans la liste des [formulaires de recherche personnalisée](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) ci-dessous.
1. Cliquez sur le nœud. Dans le volet droit des propriétés, cliquez sur la propriété **sling:resourceType**, puis modifiez-la.
1. Enfin, enregistrez les modifications en appuyant sur le bouton **Tout enregistrer**.

## Liste de formulaires de recherche personnalisée {#list-of-custom-search-forms}

Vous trouverez ci-dessous une liste de tous les formulaires de recherche personnalisée et des modifications dont ils ont besoin après la mise à niveau. Ils se réfèrent aux noms dans `/conf/global/settings/cq/search/facets/sites/items`.

### Fulltext Predicate with node name &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1</td>
   <td>fulltext</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

Dans AEM 6.1, le prédicat de texte intégral standard fait partie du formulaire de recherche. Dans la version 6.2, le champ de texte intégral a été remplacé par OmniSearch. Ce predicate est ignoré par programmation et ne peut pas être supprimé.

**Action :** Supprimez le nœud entièrement. 

### Autres prédicats de texte intégral {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1</td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicats de navigateur de chemin d’accès {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpréates/pathprédicates</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicats de balises {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>tags</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la propriété **resourceType** (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicat d’état de page {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>pagestatuspréate</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/pagestatuspréate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

L’état de page a été remplacé par deux prédicats de propriétés d’options, l’un pour la publication et l’autre pour l’état LiveCopy.

**Actions:**

* Remove the `pagestatuspredicate` node
* Copier le nœud

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * vers `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copier le nœud

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * vers `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Make sure you set `listOrder` property for the `analyticspredicate` node to &quot;**8**&quot;. Cela est nécessaire pour éviter les conflits.

### Prédicats de plage de dates {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>daterangeprédicate</td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpréates/daterangeprédicate</td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Filtre masqué {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>type</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>granit/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>granit/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Aucun élément à ajuster.

### Prédicat Analyses {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicat de plage {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/plage-prédicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

>[!NOTE]
>
>Remarque : Contrairement à la version 6.1, le prédicat de plage ne génère pas le rendu d’une balise dans la barre de recherche.

### Prédicat de propriété d’options {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicat de plage de curseurs {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/sliderrangeprédicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicat de composants {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/component spredicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicat d’auteur {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/userprédicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicat de modèles {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1<br /><br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Type de ressource dans la version 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpréates/modèles/prédicate</p> </td>
  </tr>
  <tr>
   <td>Type de ressource dans la version 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

## Rail de recherche d’administrateurs de ressources {#assets-admin-search-rail}

The nodes below refer to the names in `/conf/global/settings/dam/search/facets/assets/items`

### Fulltext Predicate with node name &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | fulltext |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/fulltextpréate |
| Type de ressource dans la version 6.2 | n/a |

Dans la version 6.1, le prédicat de texte intégral standard faisait partie du formulaire de recherche. Dans la version 6.2, le champ de texte intégral a été remplacé par OmniSearch. Ce predicate est ignoré par programmation et ne peut pas être supprimé. 

**Action :** Supprimez le nœud mentionné ci-dessus.

### Prédicats de navigateur de chemin d’accès {#path-browser-predicates-1}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | pathbrowser |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/pathbrowserprédicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/pathbrowserprédicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicats de type MIME {#mime-type-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | mimetype |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/optionspredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/optionspredicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/corail**&quot; comme dans la version 6.2 indiquée ci-dessus).

### Prédicats de taille de fichier {#file-size-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | filesize |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Action :** Ajustez `resourceType` tel qu’indiqué dans l’emplacement de la version 6.2 ci-dessus.

### Prédicat de dernière modification de la ressource {#asset-last-modified-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | assetlastmodifiedpredicate |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Action : Ajustez la propriété resourceType (ajoutez &quot;/coral&quot; comme dans l&#39;emplacement 6.2 indiqué ci-dessus).

### Prédicat de publication {#publish-predicate}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | publish |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/publishprédicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/publishprédicate |

**Actions:**

* Adjust the `resourceType` property (add &quot;**/coral**&quot; like in the 6.2 location indicated above)

* Add an `optionPaths` (of type String) property with the value: `/libs/dam/options/predicates/publish`

* Add `singleSelect` property with boolean value `true`.

### Prédicats d’état {#status-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | status |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/optionspredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/optionspredicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicats d’état d’expiration {#expiry-status-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | statut d&#39;expiration |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/expiredassetprédicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/expiredassetprédicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicats de validité de métadonnées {#metadata-validity-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | métadatavalidité |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/optionspredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/optionspredicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicats d’évaluation {#rating-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | Évaluation |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/ratingpréate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicats d’orientation {#orientation-predicate}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | Orientation |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/tagsfilterprédicate |
| Type de ressource dans la version 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Actions:**

* Adjust the `resourceType` property (add &quot;**/coral**&quot; like in the 6.2 location indicated above)

* Ajoutez une propriété `fieldLabel` avec la même valeur que la propriété `text` du même nœud.

* Ajoutez une propriété `emptyText` avec la même valeur que la propriété `text` du même nœud.

* Ajoutez une propriété `rootPath` avec la même valeur que la propriété `optionPaths` du même nœud.

### Prédicat de style {#style-predicate}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | style |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/tagsfilterprédicate |
| Type de ressource dans la version 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Actions:**

* Adjust the `resourceType` property (add &quot;**/coral**&quot; like in the 6.2 location indicated above)

* Ajoutez une propriété `fieldLabel` avec la même valeur que la propriété `text` du même nœud.

* Ajoutez une propriété `emptyText` avec la même valeur que la propriété `text` du même nœud.

* Ajoutez une propriété `rootPath` avec la même valeur que la propriété `optionPaths` du même nœud.

### Prédicats de format vidéo {#video-format-predicates}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | videoFormat |
|---|---|
| Type de ressource dans la version 6.1 | dam/gui/components/admin/customsearch/searchpréates/optionspredicate |
| Type de ressource dans la version 6.2 | dam/gui/coral/components/admin/customsearch/searchpréates/optionspredicate |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).

### Prédicat de ressource principale {#mainasset-predicate}

| Nœud(s) dans le formulaire de recherche par défaut dans la version 6.1 | mainasset |
|---|---|
| Type de ressource dans la version 6.1 | granit/ui/components/foundation/form/hidden |
| Type de ressource dans la version 6.2 | granit/ui/components/coral/foundation/form/hidden |

**Action :** Ajustez la `resourceType` propriété (ajoutez &quot;**/coral**&quot; comme dans l’emplacement 6.2 indiqué ci-dessus).
