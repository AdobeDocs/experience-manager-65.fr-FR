---
title: Rendu et diffusion
description: Découvrez comment effectuer le rendu du contenu Adobe Experience Manager au moyen des servlets par défaut Sling pour effectuer le rendu JSON et d’autres formats.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 6%

---

# Rendu et diffusion{#rendering-and-delivery}

{{ue-over-mobile}}

Le contenu Adobe Experience Manager (AEM) peut facilement être rendu au moyen des [servlets par défaut Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) pour effectuer le rendu [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) et d’autres formats.

Ces rendus prêts à l’emploi parcourent généralement le référentiel et renvoient le contenu tel quel.

AEM, par le biais de Sling, prend également en charge le développement et le déploiement de rendus Sling personnalisés pour prendre le contrôle total du schéma et du contenu rendus.

Les rendus par défaut de Content Services comblent l’écart entre les paramètres par défaut Sling prêts à l’emploi et le développement personnalisé, ce qui permet de personnaliser et de contrôler de nombreux aspects du contenu rendu sans développement.

Le diagramme suivant montre le rendu de Content Services.

![chlimage_1-15](assets/chlimage_1-15.png)

## Demande de JSON {#requesting-json}

Utilisez **&lt;RESOURCE.caas`[.<EXPORT-CONFIG][.&lt;DEPTH-INT&gt;]`.json** pour demander le format JSON.

<table>
 <tbody>
  <tr>
   <td>RESSOURCE</td>
   <td>une ressource d’entité sous /content/entities<br /> ou <br /> une ressource de contenu sous /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACULTATIF</strong><br /> </p> <p>une configuration d’exportation trouvée sous /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Si elle est omise, la configuration d’exportation par défaut est appliquée. </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>FACULTATIF</strong><br /> récursivité en profondeur <br /> pour le rendu des enfants utilisé dans le rendu Sling</td>
  </tr>
 </tbody>
</table>

## Création de configurations d’exportation {#creating-export-configs}

Les configurations d’exportation peuvent être créées pour personnaliser le rendu JSON.

Vous pouvez créer un nœud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| Nom du nœud | Nom de la configuration (pour le rendu du sélecteur) |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant présente les propriétés des configurations d’exportation :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur par défaut (si non définie)</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Chaîne[]</td>
   <td>tout inclure</td>
   <td>sling:resourceType</td>
   <td>exclure les détails des nœuds avec le sling:resourceType spécifié de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Chaîne[]</td>
   <td>n’exclure rien</td>
   <td>sling:resourceType</td>
   <td>inclure des détails uniquement pour les nœuds avec sling:resourceType spécifié à partir de l’exportation JSON ;</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Chaîne[]</td>
   <td>n’exclure rien</td>
   <td>Préfixes de propriété</td>
   <td>exclure de l’exportation JSON les propriétés qui commencent par des préfixes spécifiés</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Chaîne[]</td>
   <td>n’exclure rien</td>
   <td>Noms des propriétés</td>
   <td>exclure des propriétés spécifiées de l’exportation JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Chaîne[]</td>
   <td>tout inclure</td>
   <td>Noms des propriétés</td>
   <td><p>si excludePropertyPrefixes est défini<br /> cela inclut les propriétés spécifiées même si elles correspondent au préfixe exclu,</p> <p>sinon (les propriétés sont ignorées) incluez uniquement ces propriétés</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Chaîne[]</td>
   <td>tout inclure</td>
   <td>noms des enfants</td>
   <td>exclure les enfants spécifiés de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Chaîne[]<br /> <br /> </td>
   <td>n’exclure rien</td>
   <td>noms des enfants</td>
   <td>inclure uniquement les enfants spécifiés de l’exportation JSON, exclure les autres</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Chaîne[]<br /> <br /> </td>
   <td>ne rien renommer</td>
   <td>&lt;nom_propriété_réelle&gt;,&lt;nom_propriété_de_remplacement&gt;</td>
   <td>renommer les propriétés à l’aide de remplacements</td>
  </tr>
 </tbody>
</table>

### Remplacements de l’exportation du type de ressource {#resource-type-export-overrides}

Créez un nœud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant affiche les propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur par défaut (si non définie)</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Chaîne[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Pour les types de ressources sling suivants, ne renvoyez pas l’exportation json par défaut de CaaS.<br /> Renvoyer une exportation JSON client en effectuant le rendu de la ressource sous la forme;<br /> &lt;RESOURCE&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurations d’exportation existantes de Content Services {#existing-content-services-export-configs}

Content Services comprend deux configurations d’exportation :

* par défaut (aucune configuration spécifiée)
* page (pour effectuer le rendu des pages du site)

#### Configuration d’exportation par défaut {#default-export-configuration}

La configuration d’exportation par défaut de Content Services est appliquée si une configuration est spécifiée dans l’URI demandé.

&lt;RESSOURCE>.caas[.&lt;DEPTH-INT>].json

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
   <td>Remplacements de JSON Sling</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuration de l’exportation de pages {#page-export-configuration}

Cette configuration étend la valeur par défaut pour inclure le regroupement des enfants sous un nœud enfant .

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### Ressources supplémentaires {#additional-resources}

Consultez les ressources ci-dessous pour en savoir plus sur les rubriques supplémentaires dans Content Services :

* [Développement de modèles](/help/mobile/administer-mobile-apps.md)
* [Création de Content Services](/help/mobile/develop-content-as-a-service.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)
