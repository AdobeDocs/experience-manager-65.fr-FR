---
title: Rendu et  de
seo-title: Rendu et  de
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b

---


# Rendu et  de{#rendering-and-delivery}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le contenu AEM peut facilement être rendu par le biais des servlets [par défaut](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) Sling pour générer [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) et d’autres formats.

Ces rendus prêts à l’emploi parcourent généralement le référentiel et renvoient le contenu tel quel.

AEM, via Sling, prend également en charge le développement et le déploiement de rendus sling personnalisés afin de prendre le contrôle total du et du contenu rendus.

Les rendus par défaut de Content Services comblent l’écart entre les valeurs par défaut standard de Sling et le développement personnalisé, ce qui permet de personnaliser et de contrôler de nombreux aspects du contenu rendu sans développement.

Le diagramme suivant illustre le rendu des services de contenu.

![chlimage_1-15](assets/chlimage_1-15.png)

## Demande de fichier JSON {#requesting-json}

Utilisez **&lt;RESOURCE.cas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** pour demander JSON.

<table>
 <tbody>
  <tr>
   <td>RESSOURCE</td>
   <td>une ressource d'entité sous /content/entités<br /> ou <br /> une ressource de contenu sous /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACULTATIF</strong><br /> </p> <p>une configuration d’exportation a été trouvée sous /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /><br /> Si la configuration d’exportation par défaut est omise, elle sera appliquée. </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>Récursion de profondeur facultative</strong><br /> <br /> pour le rendu des enfants, comme utilisé dans le rendu Sling</td>
  </tr>
 </tbody>
</table>

## Création de configurations d’exportation {#creating-export-configs}

Vous pouvez créer des configurations d’exportation pour personnaliser le rendu JSON.

Vous pouvez créer un noeud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| Nom du nœud | Nom de la configuration (pour le sélecteur de rendu) |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant présente les propriétés des configurations d’exportation :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur par défaut (si, non définie)</strong></td>
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
   <td>exclure rien</td>
   <td>sling:resourceType</td>
   <td>inclure uniquement les détails des noeuds avec sling:resourceType spécifié à partir de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Chaîne[]</td>
   <td>exclure rien</td>
   <td>Préfixes de propriété</td>
   <td>exclure les propriétés  avec des préfixes spécifiés de l’exportation JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Chaîne[]</td>
   <td>exclure rien</td>
   <td>Noms des propriétés</td>
   <td>exclure des propriétés spécifiées de l’exportation JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Chaîne[]</td>
   <td>inclure tout</td>
   <td>Noms des propriétés</td>
   <td><p>si excludePropertyPrefixes est défini<br /> , cela inclut les propriétés spécifiées, même si le préfixe correspondant est exclu,</p> <p>else (exclure les propriétés ignorées) n’inclut que ces propriétés</p> </td>
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
   <td>exclure rien</td>
   <td>noms enfants</td>
   <td>inclure uniquement les enfants spécifiés de l’exportation JSON, exclure d’autres</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Chaîne[]<br /> <br /> </td>
   <td>renommer rien</td>
   <td>&lt;nom_propriété_réelle&gt;,&lt;nom_propriété_de_remplacement&gt;</td>
   <td>renommer les propriétés à l’aide de remplacements</td>
  </tr>
 </tbody>
</table>

### Remplacements de l&#39;exportation du type de ressource {#resource-type-export-overrides}

Créez un noeud de configuration sous */apps/mobileapps/caas/exportConfigs.*

| nom est | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

Le tableau suivant présente les propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur par défaut (si, non définie)</strong></td>
   <td><strong>Valeur</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Chaîne[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Pour les types de ressource sling suivants, ne renvoyez pas l’exportation JSON CaaS par défaut.<br /> Renvoyer une exportation Json client en restituant la ressource en tant que ;<br /> &lt;RESSOURCE&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurations d’exportation Content Services existantes {#existing-content-services-export-configs}

Content Services comprend deux configurations d’exportation :

* default (aucune configuration spécifiée)
* (pour rendre les pages du site)

#### Configuration de l’exportation par défaut {#default-export-configuration}

La configuration d’exportation par défaut de Content Services est appliquée si une configuration est spécifiée dans l’URI requis.

&lt;RESOURCE>.cas[.&lt;DEPTH-INT>].json

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
   <td>jcr:,sling:,cq:,oak:,pge-</td>
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
   <td>Remplacements de Sling JSON</td>
   <td>fondation/composants/image<br /> wcm/foundation/components/image<br /> mobileapps/cas/components/data/contentRéférence<br /> mobileapps/cas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuration de l’exportation de page {#page-export-configuration}

Cette configuration étend la valeur par défaut pour inclure le regroupement des enfants sous un noeud enfant.

&lt;SITE_PAGE>.cas.page[.&lt;DEPTH-INT>].json

### Ressources supplémentaires {#additional-resources}

Reportez-vous aux ressources ci-dessous pour en savoir plus sur d’autres rubriques de Content Services :

* [Développement de modèles](/help/mobile/administer-mobile-apps.md)
* [Création de Content Services](/help/mobile/develop-content-as-a-service.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)

