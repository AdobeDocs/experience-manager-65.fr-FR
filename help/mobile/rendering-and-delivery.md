---
title: Rendu et diffusion
seo-title: Rendu et diffusion
description: Rendu et diffusion
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 11%

---

# Rendu et diffusion{#rendering-and-delivery}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM contenu peut facilement être rendu via [Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) pour effectuer le rendu de [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) et d’autres formats.

Ces rendus prêts à l’emploi parcourent généralement le référentiel et renvoient le contenu tel quel.

AEM, via Sling, prend également en charge le développement et le déploiement de rendus sling personnalisés pour prendre le contrôle total du schéma et du contenu rendus.

Les rendus par défaut de Content Services comblent l’écart entre les valeurs par défaut Sling prêtes à l’emploi et le développement personnalisé, ce qui permet la personnalisation et le contrôle de nombreux aspects du contenu rendu sans aucun développement.

Le diagramme suivant montre le rendu des services de contenu.

![chlimage_1-15](assets/chlimage_1-15.png)

## Requête JSON {#requesting-json}

Utilisez **&lt;RESOURCE.caas[.&lt;export-config>.][&lt;export-config>.** jsonto demande JSON.]

<table>
 <tbody>
  <tr>
   <td>RESSOURCE</td>
   <td>une ressource d’entité sous /content/entities<br /> ou <br /> une ressource de contenu sous /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACULTATIF</strong><br /> </p> <p>une configuration d’exportation trouvée sous /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Si elle est omise, la configuration d’exportation par défaut sera appliquée. </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong></strong><br /> <br /> Récursion FACULTATIVEdepth pour le rendu des enfants, utilisée dans le rendu Sling</td>
  </tr>
 </tbody>
</table>

## Création de configurations d’exportation {#creating-export-configs}

Il est possible de créer des configurations d’exportation pour personnaliser le rendu JSON.

Vous pouvez créer un noeud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| Nom du nœud | Nom de la configuration (pour le sélecteur de rendu) |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant affiche les propriétés des configurations d’exportation :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Par défaut (si, non défini)</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Chaîne[]</td>
   <td>inclure tout</td>
   <td>sling:resourceType</td>
   <td>exclure les détails des noeuds avec sling:resourceType spécifié de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Chaîne[]</td>
   <td>exclude</td>
   <td>sling:resourceType</td>
   <td>inclure des détails uniquement pour les noeuds avec sling:resourceType spécifié à partir de l’exportation JSON ;</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Chaîne[]</td>
   <td>exclude</td>
   <td>Préfixes de propriété</td>
   <td>exclure les propriétés commençant par des préfixes spécifiés de l’exportation JSON ;</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Chaîne[]</td>
   <td>exclude</td>
   <td>Noms des propriétés</td>
   <td>exclure des propriétés spécifiées de l’exportation JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Chaîne[]</td>
   <td>inclure tout</td>
   <td>Noms des propriétés</td>
   <td><p>si excludePropertyPrefixes set<br /> cela inclut les propriétés spécifiées même si le préfixe correspondant est exclu,</p> <p>else (exclure les propriétés ignorées) n’incluent que ces propriétés</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Chaîne[]</td>
   <td>inclure tout</td>
   <td>noms enfants</td>
   <td>exclure les enfants spécifiés de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Chaîne[]<br /> <br /> </td>
   <td>exclude</td>
   <td>noms enfants</td>
   <td>inclure uniquement des enfants spécifiés de l’exportation JSON ; exclure d’autres</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Chaîne[]<br /> <br /> </td>
   <td>renommer rien</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>renommer les propriétés à l’aide de remplacements</td>
  </tr>
 </tbody>
</table>

### Remplacements de l’exportation du type de ressource {#resource-type-export-overrides}

Créez un noeud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant présente les propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Par défaut (si, non défini)</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>Chaîne[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Pour les types de ressources sling suivants, ne renvoyez pas l’exportation json CaaS par défaut.<br /> Renvoie un export json client en effectuant le rendu de la ressource comme suit : <br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurations d’exportation de Content Services existantes {#existing-content-services-export-configs}

Content Services comprend deux configurations d’exportation :

* default (aucune configuration spécifiée)
* page (pour effectuer le rendu des pages du site)

#### Configuration d’exportation par défaut {#default-export-configuration}

La configuration d’exportation par défaut de Content Services est appliquée si une configuration est spécifiée dans l’URI demandé.

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Valeur</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,page-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Remplacements JSON Sling</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuration de l’exportation de page {#page-export-configuration}

Cette configuration étend la valeur par défaut pour inclure le regroupement des enfants sous un noeud enfant.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### Ressources supplémentaires {#additional-resources}

Consultez les ressources ci-dessous pour en savoir plus sur les rubriques supplémentaires dans Content Services :

* [Développement de modèles](/help/mobile/administer-mobile-apps.md)
* [Création de Content Services](/help/mobile/develop-content-as-a-service.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)
