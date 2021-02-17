---
title: Bibliothèques de balises
seo-title: Bibliothèques de balises
description: Les bibliothèques de balises Granite, CQ et Sling vous donnent accès à des fonctions spécifiques à utiliser dans le script JSP de vos modèles et composants.
seo-description: Les bibliothèques de balises Granite, CQ et Sling vous donnent accès à des fonctions spécifiques à utiliser dans le script JSP de vos modèles et composants.
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 65%

---


# Bibliothèques de balises{#tag-libraries}

Les bibliothèques de balises Granite, CQ et Sling vous donnent accès à des fonctions spécifiques à utiliser dans le script JSP de vos modèles et composants.

## Bibliothèque de balises Granite {#granite-tag-library}

La bibliothèque de balises Granite comporte des fonctions bien utiles.

Lorsque vous développez le script JSP d’un composant d’IU Granite, il est recommandé d’inclure le code suivant au début du script :

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

Le fichier global déclare également la [bibliothèque Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

La balise `<ui:includeClientLib>` comprend une bibliothèque cliente html AEM, qui peut être un fichier js, un fichier CSS ou une bibliothèque de thèmes. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le fichier jsp. Cette balise est une enveloppe dite de commodité (convenience wrapper) utilisée autour de l’interface de service ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Elle présente les attributs suivants :

**catégories**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**thème**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**thème**  - Un indicateur indiquant uniquement les bibliothèques thématiques ou non devrait être inclus. Si cet attribut est omis, les deux ensembles sont inclus. S’applique uniquement aux inclusions JS et CSS pures (pas aux catégories ni aux inclusions de thème).

La balise `<ui:includeClientLib>` peut être utilisée comme suit dans un fichier jsp :

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## Bibliothèque de balises CQ {#cq-tag-library}

La bibliothèque de balises CQ comporte des fonctions bien utiles.

Pour utiliser la bibliothèque de balises CQ dans votre script, ce dernier doit commencer par le code suivant :

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Lorsque le fichier `/libs/foundation/global.jsp` est inclus dans le script, la bibliothèque taglib est automatiquement déclarée.

Lorsque vous développez le script jsp d’un composant AEM, il est recommandé d’inclure le code en début de script :

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Il déclare les balises sling, CQ et jstl et expose les objets de script régulièrement utilisés définis par la balise [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects). Cela raccourcit et simplifie le code jsp de votre composant.

### <cq:text> {#cq-text}

La balise `<cq:text>` est une balise pratique qui génère le texte du composant dans un JSP.

Il présente les attributs facultatifs ci-dessous :

**property** - Nom de la propriété à utiliser. Le nom est relatif à la ressource actuelle.

**valeur**  - Valeur à utiliser pour la sortie. Si cet attribut est présent, il annule l’utilisation de l’attribut property.

**oldValue**  : valeur à utiliser pour la sortie diff. Si cet attribut est présent, il annule l’utilisation de l’attribut property.

**escapeXml**  - Définit si les caractères  &lt;>, &amp;, &#39; et &quot; de la chaîne résultante doivent être convertis en codes d&#39;entité de caractères correspondants. La valeur par défaut est false. Notez que l’échappement est appliqué après la mise en forme facultative.

**format**  - Facultatif java.text.Format à utiliser pour le formatage du texte.

**noDiff**  - Supprime le calcul d&#39;une sortie diff, même si une information diff est présente.

**tagClass**  - nom de classe CSS d’un élément qui entoure une sortie non vide. Si elle est vide, aucun élément n’est ajouté.

**tagName**  : nom de l’élément qui entoure une sortie non vide. Cet attribut est défini, par défaut, sur DIV.

**espace réservé**  : valeur par défaut à utiliser pour le texte vide ou nul en mode d’édition, c’est-à-dire l’espace réservé. Notez que la vérification par défaut est effectuée après l’échappement et la mise en forme facultatifs ; en d’autres termes, elle est écrite telle quelle dans la sortie. Elle est définie par défaut sur :

`<div><span class="cq-text-placeholder">&para;</span></div>`

**par défaut**  : valeur par défaut à utiliser pour le texte vide ou nul. Notez que la vérification par défaut est effectuée après l’échappement et la mise en forme facultatifs ; en d’autres termes, elle est écrite telle quelle dans la sortie.

Voici quelques exemples d’utilisation de la balise `<cq:text>` dans un JSP :

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### <cq:setContentBundle> {#cq-setcontentbundle}

La balise `<cq:setContentBundle>` crée un contexte de localisation i18n et le stocke dans la variable de configuration `javax.servlet.jsp.jstl.fmt.localizationContext`.

Elle présente les attributs suivants :

**langue**  - Langue du paramètre régional pour laquelle récupérer le regroupement de ressources.

**source**  : source à partir de laquelle le paramètre régional doit être pris. Les valeurs définies peuvent être les suivantes :

* **statique**  : le paramètre régional est extrait de l’ `language` attribut si disponible, sinon du paramètre régional par défaut du serveur.

* **page**  - le paramètre régional est extrait de la langue de la page ou de la ressource active si elle est disponible, sinon de l’ `language` attribut si disponible, sinon du paramètre régional par défaut du serveur.

* **request**  - le paramètre régional est extrait du paramètre régional de la demande (  `request.getLocale()`).

* **auto**  : le paramètre régional est extrait de l’ `language` attribut si disponible, sinon de la langue de la page ou de la ressource active si disponible, sinon de la requête.

Si l’attribut `source` n’est pas défini :

* Si l&#39;attribut `language` est défini, l&#39;attribut `source` prend par défaut la valeur &quot;`static`.

* Si l&#39;attribut `language` n&#39;est pas défini, l&#39;attribut `source` prend par défaut la valeur `auto`.

Le &quot;lot de contenu&quot; peut être simplement utilisé par les balises JSTL `<fmt:message>` standard. La recherche des messages par clés est une opération en deux temps :

1. Tout d’abord, des traductions sont recherchées dans les propriétés JCR de la ressource sous-jacente qui est actuellement restituée. Cela vous permet de définir une boîte de dialogue de composant simple pour modifier ces valeurs.
1. Si le nœud ne contient pas de propriété dont le nom correspond exactement à celui de la clé, la solution de secours consiste à charger un lot de ressources à partir de la requête sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). La langue ou le paramètre régional de ce lot est défini par la langue et les attributs source de la balise `<cq:setContentBundle>`.

La balise `<cq:setContentBundle>` peut être utilisée comme suit dans un fichier jsp.

Pour les pages qui définissent leur langue :

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Pour les pages personnalisées par l’utilisateur :

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### <cq:include> {#cq-include}

La balise `<cq:include>` inclut une ressource dans la page active.

Elle présente les attributs suivants :

**flush**

* Valeur booléenne qui indique si la sortie doit être vidée ou non avant d’inclure la cible.

**path**

* Chemin d’accès à l’objet de ressource à inclure dans le traitement de la requête en cours. S’il s’agit d’un chemin d’accès relatif, il est ajouté au chemin d’accès de la ressource en cours dont le script contient la ressource donnée. Les attributs path et resourceType ou script doivent être spécifiés.

**resourceType**

* Type de la ressource à inclure. Si le type de ressource est défini, le chemin d’accès doit correspondre exactement au chemin d’accès pointant vers un objet de ressource : dans ce cas, l’ajout de paramètres, de sélecteurs et d’extensions au chemin d’accès n’est pas pris en charge.
* Si la ressource à inclure est définie avec l’attribut path qui ne peut pas être résolu sur une ressource, il se peut que la balise crée un objet de ressource synthétique hors du chemin d’accès et de ce type de ressource.
* Les attributs path et resourceType ou script doivent être spécifiés.

**script**

* Script jsp à inclure. Les attributs path et resourceType ou script doivent être spécifiés.

**ignoreComponentHierarchy**

* Valeur booléenne qui contrôle si la hiérarchie des composants doit être ignorée pour la résolution du script. Si la valeur est définie sur true, seuls les chemins de recherche sont respectés.

**Exemple:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

Devriez-vous utiliser `<%@ include file="myScript.jsp" %>` ou `<cq:include script="myScript.jsp" %>` pour inclure un script ?

* La directive `<%@ include file="myScript.jsp" %>` informe le compilateur JSP d&#39;inclure un fichier complet dans le fichier actif. C’est comme si le contenu du fichier inclus était collé directement dans le fichier d’origine.
* Avec la balise `<cq:include script="myScript.jsp">`, le fichier est inclus au moment de l’exécution.

Devriez-vous utiliser `<cq:include>` ou `<sling:include>` ?

* Lorsque vous développez des composants AEM, Adobe vous recommande d’utiliser `<cq:include>`.
* `<cq:include>` vous permet d’inclure directement des fichiers de script en fonction de leur nom lors de l’utilisation de l’attribut script. L’héritage du type de composant et de ressource est alors pris en compte. Généralement, cela s’avère plus simple que d’observer une stricte conformité avec la résolution de script de Sling à l’aide de sélecteurs et d’extensions.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` a été abandonné depuis AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) devrait être utilisé à la place.

La balise `<cq:includeClientLib>` comprend une bibliothèque cliente html AEM, qui peut être un js, un css ou une bibliothèque de thèmes. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le fichier jsp. Cette balise est une enveloppe dite de commodité (convenience wrapper) utilisée autour de l’interface de service `com.day.cq.widget.HtmlLibraryManager`.

Elle présente les attributs suivants :

**catégories**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**thème**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

Équivalent à : `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**thème**  - Un indicateur indiquant uniquement les bibliothèques thématiques ou non devrait être inclus. Si cet attribut est omis, les deux ensembles sont inclus. S’applique uniquement aux inclusions JS et CSS pures (pas aux catégories ni aux inclusions de thème).

La balise `<cq:includeClientLib>` peut être utilisée comme suit dans un fichier jsp :

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### <cq:defineObjects> {#cq-defineobjects}

La balise `<cq:defineObjects>` expose les objets de script suivants, régulièrement utilisés, qui peuvent être référencés par le développeur. Il expose également les objets définis par la balise [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* Objet de contexte de composant actif de la requête (interface com.day.cq.wcm.api.components.ComponentContext).

**component**

* Objet de composant AEM actif de la ressource en cours (interface com.day.cq.wcm.api.components.Component).

**currentDesign**

* Objet de conception actif de la page en cours (interface com.day.cq.wcm.api.designer.Design).

**currentPage**

* Objet de page AEM WCM en cours (interface com.day.cq.wcm.api.Page).

**currentStyle**

* Objet de style actuel de la cellule en cours (interface com.day.cq.wcm.api.designer.Style).

**designer**

* Objet designer utilisé pour accéder aux informations de conception (interface com.day.cq.wcm.api.designer.Designer).

**editContext**

* Objet de contexte de modification du composant AEM (interface com.day.cq.wcm.api.components.EditContext).

**pageManager**

* Objet de gestionnaire de page pour les opérations au niveau de la page (interface com.day.cq.wcm.api.PageManager).

**pageProperties**

* Objet des propriétés de la page en cours (org.apache.sling.api.resource.ValueMap).

**propriétés**

* Objet des propriétés de la ressource en cours (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* Objet de conception de la page de ressources (interface com.day.cq.wcm.api.designer.Design).

**resourcePage**

* Objet de la page de ressources (interface com.day.cq.wcm.api.Page).
* Il possède les attributs suivants :

**requestName**

* Hérité de sling

**responseName**

* Hérité de sling

**resourceName**

* Hérité de sling

**nodeName**

* Hérité de sling

**logName**

* Hérité de sling

**resourceResolverName**

* Hérité de sling

**slingName**

* Hérité de sling

**componentContextName**

* spécifique à wcm

**editContextName**

* spécifique à wcm

**propertiesName**

* spécifique à wcm

**pageManagerName**

* spécifique à wcm

**currentPageName**

* spécifique à wcm

**resourcePageName**

* spécifique à wcm

**pagePropertiesName**

* spécifique à wcm

**componentName**

* spécifique à wcm

**designerName**

* spécifique à wcm

**currentDesignName**

* spécifique à wcm

**resourceDesignName**

* spécifique à wcm

**currentStyleName**

* spécifique à wcm

**Exemple**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Lorsque le fichier `/libs/foundation/global.jsp` est inclus dans le script, la balise `<cq:defineObjects />` est automatiquement incluse.

### <cq:requestURL> {#cq-requesturl}

La balise `<cq:requestURL>` écrit l’URL de requête actuelle à JspWriter. Les deux balises [ `<cq:addParam>`](#amp-lt-cq-addparam) et [ `<cq:removeParam>`](#amp-lt-cq-removeparam) peuvent être utilisées dans le corps de cette balise pour modifier l’URL de requête active avant qu’elle ne soit écrite.

Cela vous permet de créer des liens vers la page en cours avec des paramètres variables. Cela vous permet, par exemple, de transformer la requête :

`mypage.html?mode=view&query=something` en `mypage.html?query=something`.

L&#39;utilisation de `addParam` ou `removeParam` ne modifie que l&#39;occurrence du paramètre donné, tous les autres paramètres ne sont pas affectés.

`<cq:requestURL>` n’a aucun attribut.

Exemples :

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

La balise `<cq:addParam>` ajoute un paramètre de requête avec le nom et la valeur donnés à la balise [ `<cq:requestURL>`](#amp-lt-cq-requesturl) qui l&#39;entoure.

Elle présente les attributs suivants :

**name**

* Nom du paramètre à ajouter

**value**

* Valeur du paramètre à ajouter

**Exemple:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

La balise `<cq:removeParam>` supprime un paramètre de requête avec le nom et la valeur donnés de la balise [ `<cq:requestURL>`](#amp-lt-cq-requesturl) qui l&#39;entoure. Si aucune valeur n’est indiquée, tous les paramètres portant le nom spécifié sont supprimés.

Elle présente les attributs suivants :

**name**

* Nom du paramètre à supprimer

Exemple :

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Bibliothèque de balises Sling  {#sling-tag-library}

La bibliothèque de balises Sling comporte des fonctions Sling bien utiles.

Lorsque vous utilisez la bibliothèque de balises Sling dans votre script, ce dernier doit commencer par le code suivant :

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Lorsque le fichier `/libs/foundation/global.jsp` est inclus dans le script, la bibliothèque sling taglib est automatiquement déclarée.

### <sling:include> {#sling-include}

La balise `<sling:include>` inclut une ressource dans la page active.

Elle présente les attributs suivants :

**vider**

* Valeur booléenne qui indique si la sortie doit être vidée ou non avant d’inclure la cible.

**ressource**

* Objet de ressource à inclure dans le traitement de la requête en cours. L’attribut resource ou path doit être spécifié. Si les deux attributs sont spécifiés, l’attribut resource est prioritaire.

**chemin**

* Chemin d’accès à l’objet de ressource à inclure dans le traitement de la requête en cours. S’il s’agit d’un chemin d’accès relatif, il est ajouté au chemin d’accès de la ressource en cours dont le script contient la ressource donnée. L’attribut resource ou path doit être spécifié. Si les deux attributs sont spécifiés, l’attribut resource est prioritaire.

**resourceType**

* Type de la ressource à inclure. Si le type de ressource est défini, le chemin d’accès doit correspondre exactement au chemin d’accès pointant vers un objet de ressource : dans ce cas, l’ajout de paramètres, de sélecteurs et d’extensions au chemin d’accès n’est pas pris en charge.
* Si la ressource à inclure est définie avec l’attribut path qui ne peut pas être résolu sur une ressource, il se peut que la balise crée un objet de ressource synthétique hors du chemin d’accès et de ce type de ressource.

**replaceSelectors**

* Lors de la distribution, les sélecteurs sont remplacés par la valeur de cet attribut.

**addSelectors**

* Lors de la distribution, la valeur de cet attribut est ajoutée aux sélecteurs.

**replaceSuffix**

* Lors de la distribution, le suffixe est remplacé par la valeur de cet attribut.

>[!NOTE]
>
>La résolution de la ressource et du script inclus avec la balise `<sling:include>` est identique à celle d’une résolution d’URL sling normale. Par défaut, les sélecteurs, l’extension, etc. de la requête en cours sont également utilisés pour le script inclus. Ils peuvent être modifiés à l’aide des attributs de balise : par exemple, `replaceSelectors="foo.bar"` vous permet de remplacer les sélecteurs.

Exemples :

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### <sling:defineObjects> {#sling-defineobjects}

La balise `<sling:defineObjects>` expose les objets de script suivants, régulièrement utilisés, qui peuvent être référencés par le développeur :

**slingRequest**

* L’objet SlingHttpServletRequest, qui permet d’accéder aux informations d’en-tête de la requête HTTP, étend l’objet HttpServletRequest standard et donne accès à des éléments spécifiques à Sling tels que la ressource, des informations sur le chemin d’accès, le sélecteur, etc.

**slingResponse**

* Objet SlingHttpServletResponse permettant d’accéder à la réponse HTTP créée par le serveur. Actuellement, il est identique à l’objet HttpServletResponse à partir duquel il s’étend.**request**
* Objet de requête JSP standard qui est un objet HttpServletRequest pur.**response**
* Objet de réponse JSP standard qui est un objet HttpServletResponse pur.

**resourceResolver**

* Objet ResourceResolver en cours. Il est identique à slingRequest.getResourceResolver()

.**sling**

* Objet SlingScriptHelper contenant des méthodes pratiques pour les scripts, principalement sling.include(&#39;/some/other/resource&#39;) pour inclure les réponses d’autres ressources dans cette réponse (intégration de fragments HTML d’en-tête, par exemple) et sling.getService(foo.bar.Service.class) pour récupérer les services OSGi disponibles dans Sling (notation de classe en fonction du langage de script).

**ressource**

* Objet de ressource en cours à gérer en fonction de l’URL de la requête. Il est identique à slingRequest.getResource().

**currentNode**

* Si la ressource en cours pointe vers un nœud JCR (ce qui est généralement le cas dans Sling), cela permet d’accéder directement à l’objet Nœud. Dans le cas contraire, cet objet n’est pas défini.

**log**

* Fournit un enregistreur SLF4J pour consigner des événements dans le système de journalisation Sling depuis des scripts, par exemple : log.info(&quot;Exécution de mon script&quot;).

* Il possède les attributs suivants :

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**Exemple :**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Bibliothèque de balises JSTL  {#jstl-tag-library}

La [bibliothèque de balises standard des pages JavaServer](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contient beaucoup de balises utiles et standard. Les balises de base, de formatage et de fonctions sont définies par `/libs/foundation/global.jsp` comme le montre le fragment de code suivant.

### Extrait de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Après avoir importé le fichier `/libs/foundation/global.jsp` comme décrit précédemment, vous pouvez utiliser les préfixes `c`, `fmt` et `fn` pour accéder à ces balises. La documentation officielle de la JSTL est disponible [ici](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
