---
title: Configuration de Cloud Services
seo-title: Cloud Service Configurations
description: Vous pouvez étendre les instances existantes pour créer vos propres configurations.
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Configuration de Cloud Services{#cloud-service-configurations}

Les configurations apportent la logique et la structure de stockage des configurations de service.

Vous pouvez étendre les instances existantes pour créer vos propres configurations.

## Concepts {#concepts}

Les principes suivis dans le développement des configurations sont basés sur les concepts ci-après :

* Les services/adaptateurs sont utilisés pour récupérer la ou les configurations.
* Les configurations (par exemple les propriétés/paragraphes) sont héritées du ou des parents.
* Référencées à partir du(des) nœud(s) analytique(s) par chemin.
* Facilement extensibles.
* Permet de répondre à des configurations plus complexes, telles [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Prise en charge des dépendances (par ex., les modules externes [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) nécessitent une configuration [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)).

## Structure {#structure}

Le chemin de base des configurations est :

`/etc/cloudservices`.

Pour chaque type de configuration, un modèle et un composant sont fournis. Ainsi, une fois personnalisés, les modèles de configuration peuvent répondre à la plupart des besoins.

Afin de proposer une configuration pour un nouveau service, vous devez :

* créer une page de service dans

   `/etc/cloudservices`

* sous :

   * un modèle de configuration
   * un composant de configuration

Le modèle et le composant doivent hériter du `sling:resourceSuperType` du modèle de base :

`cq/cloudserviceconfigs/templates/configpage`

ou respectivement du composant de base

`cq/cloudserviceconfigs/components/configpage`

Le fournisseur de services doit également fournir la page de service :

`/etc/cloudservices/<service-name>`

### Modèle {#template}

Votre modèle étendra le modèle de base :

`cq/cloudserviceconfigs/templates/configpage`

et définissez un `resourceType` qui pointe vers le composant personnalisé.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Composants {#components}

Votre composant devrait étendre le composant de base :

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Après avoir configuré votre modèle et votre composant, vous pouvez ajouter votre configuration en ajoutant des sous-pages sous :

`/etc/cloudservices/<service-name>`

### Modèle de contenu {#content-model}

Le modèle de contenu est stocké sous la forme `cq:Page` sous :

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Les configurations sont stockées sous le sous-nœud `jcr:content`.

* Les propriétés fixes, définies dans une boîte de dialogue, doivent être stockées directement sur le `jcr:node`.
* Les éléments dynamiques (utilisant `parsys` ou `iparsys`) se servent d’un sous-nœud pour stocker les données du composant.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Pour la documentation de référence sur l’API, voir [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/Webservicesupport/package-summary.html).

### Intégration d’AEM {#aem-integration}

Les services disponibles sont répertoriés dans l’onglet **Services cloud** de la boîte de dialogue **Propriétés de la page** (de toute page héritant de `foundation/components/page` ou `wcm/mobile/components/page`).

L’onglet contient également :

* un lien vers l’emplacement où vous pouvez activer le service
* le choix d’une configuration (sous-nœud du service) à partir d’un champ de chemin

#### Chiffrement de mot de passe {#password-encryption}

Lorsque vous stockez des informations d’identification d’utilisateur pour le service, tous les mots de passe doivent être chiffrés.

Pour cela, il faut ajouter un champ de formulaire masqué. L’annotation `@Encrypted` doit être présente dans le nom de propriété de ce champ, par exemple, pour le champ `password`, le nom de la propriété serait écrit comme suit :

`password@Encrypted`

La propriété est alors automatiquement chiffrée (en utilisant le service `CryptoSupport`) par `EncryptionPostProcessor`.

>[!NOTE]
>
>Ceci est similaire aux annotations ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` standard.

>[!NOTE]
>
>Par défaut, `EcryptionPostProcessor` chiffre uniquement les requêtes `POST` effectuées sur `/etc/cloudservices`.

#### Propriétés supplémentaires pour les nœuds jcr:content de page de service {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Chemin d’accès de référence à un composant à inclure automatiquement dans la page.<br /> Ceci est utilisé pour des fonctionnalités supplémentaires et des inclusions JS.<br /> Cela inclut le composant sur la page où<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> est inclus (normalement avant la variable <code>body</code>).<br /> Dans le cas de Google Analytics et Target, nous utilisons ceci pour insérer des fonctionnalités supplémentaires, telles que des appels JavaScript, afin de suivre le comportement des visiteurs.</td>
  </tr>
  <tr>
   <td>description</td>
   <td>Brève description du service.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Description étendue du service.</td>
  </tr>
  <tr>
   <td>ranking</td>
   <td>Classement des services à utiliser dans les listes.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filtre permettant d’afficher les configurations dans la boîte de dialogue des propriétés de la page.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL du site Web du service.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Libellé de l’URL du service.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Chemin d’accès à la miniature du service.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Visibilité dans la boîte de dialogue des propriétés de page ; visible par défaut (facultatif)</td>
  </tr>
 </tbody>
</table>

### Cas d’utilisation {#use-cases}

Ces services sont fournis par défaut :

* [Extraits de module de tracking](/help/sites-administering/external-providers.md) (Google, WebTrends, etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consultez également [Création d’un service cloud personnalisé](/help/sites-developing/extending-cloud-config-custom-cloud.md).
