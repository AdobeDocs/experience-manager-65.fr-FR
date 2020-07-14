---
title: Utilisation des adaptateurs Sling
seo-title: Utilisation des adaptateurs Sling
description: Sling propose un modèle Adaptateur permettant de convertir facilement les objets qui mettent en œuvre l’interface Adaptable.
seo-description: Sling propose un modèle Adaptateur permettant de convertir facilement les objets qui mettent en œuvre l’interface Adaptable.
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 4949eeb190f26850f80e1ad107f2057c661ed23d
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 42%

---


# Utilisation des adaptateurs Sling{#using-sling-adapters}

[Sling](https://sling.apache.org) propose un [modèle Adaptateur](https://sling.apache.org/site/adapters.html) permettant de convertir facilement les objets qui mettent en œuvre l’interface [Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29). This interface provides a generic [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) method that will translate the object to the class type being passed as the argument.

Par exemple, pour convertir un objet Resource en objet Node correspondant, vous pouvez simplement procéder comme suit :

```java
Node node = resource.adaptTo(Node.class);
```

## Cas d’utilisation {#use-cases}

Il existe plusieurs scénarios d’utilisation :

* Obtenir des objets spécifiques à l’implémentation.

   For example, a JCR-based implementation of the generic [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) interface provides access to the underlying JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).`

* Création de raccourcis d’objets qui nécessitent la transmission d’objets de contexte internes.

   For example, the JCR-based [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) holds a reference to the request&#39;s [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), which in turn is needed for many objects that will work based on that request session, such as the [`PageManager`](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) or [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Raccourci vers les services.

   A rare case - `sling.getService()` is simple as well.

### Valeur renvoyée nulle {#null-return-value}

`adaptTo()` peut renvoyer la valeur null.

Plusieurs raisons peuvent expliquer cela :

* Cette implémentation ne prend pas en charge le type cible.
* Une « adapter factory » qui gère ce cas n’est pas active (en raison de références de service manquantes, par exemple.)
* La condition interne a échoué.
* Le service n’est pas disponible.

Il est important de traiter ce cas de manière appropriée. Pour les rendus JSP, l’échec de JSP est acceptable si cela se traduit par un élément de contenu vide.

### Mise en cache {#caching}

To improve performance, implementations are free to cache the object returned from a `obj.adaptTo()` call. Si `obj` est identique, l’objet renvoyé l’est également.

Cette mise en cache est exécutée pour tous les scénarios basés sur `AdapterFactory`.

Cependant, il n’existe pas de règle absolue : l’objet peut soit être une nouvelle instance, soit une instance existante. Cela signifie que vous ne pouvez pas compter sur un comportement en particulier. Par conséquent, il est important, notamment dans `AdapterFactory`, que les objets soient réutilisables dans ce scénario.

### Fonctionnement {#how-it-works}

There are various ways that `Adaptable.adaptTo()` can be implemented:

* Par l’objet proprement dit ; implémentation de la méthode et mappage sur certains objets.
* By an [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)`, which can map arbitrary objects.

   Les objets doivent cependant implémenter l’interface `Adaptable` et étendre [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (qui transmet l’appel `adaptTo` à un gestionnaire d’adaptateur central).

   Cela autorise les hooks dans le mécanisme `adaptTo` pour les classes existantes, comme `Resource`.

* Une combinaison des deux.

Pour le premier cas, vous pouvez consulter les JavaDocs pour connaître les `adaptTo-targets` possibles. Cependant, pour des sous-classes spécifiques, telles que la ressource basée sur JCR, cela s’avère souvent impossible. Dans ce cas, les implémentations de `AdapterFactory` font généralement partie des classes privées d’un lot et ne sont donc pas exposées dans une API cliente ni répertoriées dans les JavaDocs. En théorie, il serait possible d’accéder à toutes les implémentations `AdapterFactory` à partir de l’exécutable de service [OSGi](/help/sites-deploying/configuring-osgi.md) et d’observer leurs configurations « adaptables » (sources et cibles), mais pas de les mapper entre elles. En définitive, cela dépend de la logique interne, qui doit être documentée, d’où cette référence.

## Référence {#reference}

### Sling {#sling}

[**Resource **](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)s’adapte à :

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>S’il s’agit d’une ressource basée sur un noeud JCR ou d’une propriété JCR référençant un noeud.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propriétés</a></td>
   <td>S’il s’agit d’une ressource basée sur une propriété JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Élément</a></td>
   <td>S’il s’agit d’une ressource basée sur JCR (nœud ou propriété).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Mapper</a></td>
   <td>Renvoie un mappage des propriétés, s’il s’agit d’une ressource basée sur un nœud JCR (ou une autre ressource prenant en charge les mappages de valeurs).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Renvoie un mappage simple d’emploi des propriétés, s’il s’agit d’une ressource basée sur un nœud JCR (ou une autre ressource prenant en charge les mappages de valeurs). Can also be achieved (more simply) by using<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (handles null case, etc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extension of <a href="https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> which allows the hierarchy of resources to be taken into account when looking for properties.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>Extension de <a href="https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>qui vous permet de modifier les propriétés sur ce noeud.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Returns the binary content of a file resource (if this is a JCR-node-based resource and the node type is <code>nt:file</code> or <code>nt:resource</code>; if this is a bundle resource; file content if this is a file system resource) or the data of a binary JCR property resource.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Renvoie une URL pointant vers la ressource (URL de référentiel de ce nœud s’il s’agit d’une ressource basée sur un nœud JCR ; URL de lot JAR s’il s’agit d’une ressource de type lot ; URL de fichier s’il s’agit d’une ressource de système de fichiers).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">Fichier</a></td>
   <td>S’il s’agit d’une ressource de système de fichiers.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Si cette ressource est un script (un fichier jsp, par exemple) pour lequel un moteur de script est enregistré auprès de sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Si cette ressource est un script (un fichier jsp, par exemple) pour lequel un moteur de script est enregistré auprès de sling ou s’il s’agit de ressource de servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">String</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"> Boolean</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"> Long</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"> Double</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"> Calendar</a><br /><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"> Value</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"> String[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"> Boolean[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"> Long[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"> Calendar[]</a><br /><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"> Value[]</a></td>
   <td>Renvoie la (les) valeur(s) s’il s’agit d’une ressource basée sur une propriété JCR (et que la valeur convient).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>S’il s’agit d’une ressource basée sur un nœud JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">Mise à jour </a></td>
   <td>S’il s’agit d’une ressource de nœud dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td>S'il s'agit d'un rendu dam:Asset (nt:file sous le dossier de rendu d'un dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>En fonction de la session JCR, s’il s’agit d’une ressource basée sur JCR et que l’utilisateur est autorisé à accéder à UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorisable</a></td>
   <td>L’interface Autorisé est la base commune de l’utilisateur et du groupe.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Utilisateur</a></td>
   <td>L’utilisateur est un objet Autorisé spécial qui peut être authentifié et emprunt d’identité.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Effectue une recherche sous la ressource (ou utilise setSearchIn()) s’il s’agit d’une ressource basée sur JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>État du workflow pour le nœud de charge utile de la page/du workflow donné.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>État de réplication de la ressource donnée ou de son sous-nœud jcr:content (vérifié en premier).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Renvoie une ressource de connecteur adaptée pour certains types, s’il s’agit d’une ressource basée sur JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>If this is a <code>cq:ContentSyncConfig</code> node resource.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>If this is below a <code>cq:ContentSyncConfig</code> node resource.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver **](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)s&#39;adapte à :

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>Session JCR de la requête, s’il s’agit d’un résolveur de ressources basé sur JCR (par défaut).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Basé sur la session JCR, s’il s’agit d’un résolveur de ressources basé sur JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager permet d'accéder aux objets autorisés et de les gérer, c'est-à-dire les utilisateurs et les groupes. UserManager est lié à une session particulière.
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorisable</a> </td>
   <td>Utilisateur actuel.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Utilisateur</a><br /> </td>
   <td>Utilisateur actuel.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>Pour externaliser des URL absolues, même avec l’objet de requête.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)s’adapte à :

Pas encore de cible, mais implémente l’interface Adaptable et peut être utilisé comme source dans une AdapterFactory personnalisée.

[**SlingHttpServletResponse **](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)s’adapte à :

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>S'il s'agit d'une réponse de réécriture sling.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**Page** s’adapte à :

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Ressource</a><br /> </td>
   <td>Ressource de la page.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Ressource étiquetée (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>Noeud de la page.</td>
  </tr>
  <tr>
   <td>…</td>
   <td>Tout ce à quoi la ressource de la page peut être adapté.</td>
  </tr>
 </tbody>
</table>

**Component** s’adapte à :

| [Ressource](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Ressource du composant. |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Ressource étiquetée (== this). |
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Noeud du composant. |
| … | Tout ce à quoi la ressource du composant peut être adapté. |

**Template** s’adapte à :

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Ressource</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Ressource du modèle.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Ressource étiquetée (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>Noeud de ce modèle.</td>
  </tr>
  <tr>
   <td>…</td>
   <td>Tout ce à quoi la ressource du modèle peut être adaptée.</td>
  </tr>
 </tbody>
</table>

#### Sécurité {#security}

**Authorizable**, **User** et **Group** s’adaptent à :

| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Renvoie le noeud d’accueil utilisateur/groupe. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Renvoie l’état de réplication pour le noeud d’accueil utilisateur/groupe. |

#### Gestion des actifs numériques {#dam}

**La ressource** s’adapte à :

| [Ressource](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Ressource de l’actif. |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Noeud de la ressource. |
| … | Tout ce à quoi la ressource de l&#39;actif peut être adapté. |

#### Balisage {#tagging}

**La balise** s’adapte à :

| [Ressource](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Ressource de la balise. |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Noeud de la balise . |
| … | Tout ce à quoi la ressource de la balise peut être adapté. |

#### Autres {#other}

Sling / JCR / OCM fournit, en outre, une ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` pour les objets OCM ([Object Content Mapping](https://jackrabbit.apache.org/object-content-mapping.html)) personnalisés.
