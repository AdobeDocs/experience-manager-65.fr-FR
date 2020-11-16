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

The `<ui:includeClientLib>` tag Includes a AEM html client library, which can be a js, a css, or a theme library. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le fichier jsp. Cette balise est une enveloppe dite de commodité (convenience wrapper) utilisée autour de l’interface de service ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Elle présente les attributs suivants :

**catégories** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**thème** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

Equivalent à: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**thème** - Un indicateur indiquant uniquement les bibliothèques thématiques ou non thématiques doit être inclus. Si cet attribut est omis, les deux ensembles sont inclus. S’applique uniquement aux inclusions JS et CSS pures (pas aux catégories ni aux inclusions de thème).

The `<ui:includeClientLib>` tag can be used as follows in a jsp:

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
>When the `/libs/foundation/global.jsp` file is included in the script, the taglib is automatically declared.

Lorsque vous développez le script jsp d’un composant AEM, il est recommandé d’inclure le code en début de script :

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

It declares the sling, CQ, and jstl taglibs and exposes the regularly used scripting objects defined by the [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) tag. Cela raccourcit et simplifie le code jsp de votre composant.

### <cq:text> {#cq-text}

The `<cq:text>` tag is a convenience tag that outputs component text in a JSP.

Il présente les attributs facultatifs ci-dessous :

**property** - Nom de la propriété à utiliser. Le nom est relatif à la ressource actuelle.

**value** - Valeur à utiliser pour la sortie. Si cet attribut est présent, il annule l’utilisation de l’attribut property.

**oldValue** - Valeur à utiliser pour la sortie diff. Si cet attribut est présent, il annule l’utilisation de l’attribut property.

**escapeXml** - Définit si les caractères &lt;, >, &amp;, &#39; et &quot; de la chaîne résultante doivent être convertis en codes d&#39;entité de caractères correspondants. La valeur par défaut est false. Notez que l’échappement est appliqué après la mise en forme facultative.

**format** - Facultatif java.text.Format à utiliser pour le formatage du texte.

**noDiff** - Supprime le calcul d&#39;une sortie diff, même si une information diff est présente.

**tagClass** - nom de classe CSS d’un élément qui entoure une sortie non vide. Si elle est vide, aucun élément n’est ajouté.

**tagName** : nom de l’élément qui entoure une sortie non vide. Cet attribut est défini, par défaut, sur DIV.

**espace réservé** : valeur par défaut à utiliser pour le texte vide ou nul en mode d’édition, c’est-à-dire l’espace réservé. Notez que la vérification par défaut est effectuée après l’échappement et la mise en forme facultatifs ; en d’autres termes, elle est écrite telle quelle dans la sortie. Elle est définie par défaut sur :

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** - valeur par défaut à utiliser pour le texte vide ou nul. Notez que la vérification par défaut est effectuée après l’échappement et la mise en forme facultatifs ; en d’autres termes, elle est écrite telle quelle dans la sortie.

Some examples how the `<cq:text>` tag can be used in a JSP:

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

The `<cq:setContentBundle>` tag creates an i18n localization context and stores it in the `javax.servlet.jsp.jstl.fmt.localizationContext` configuration variable.

Elle présente les attributs suivants :

**langue** : langue du paramètre régional pour laquelle récupérer le regroupement de ressources.

**source** : source à partir de laquelle le paramètre régional doit être extrait. Les valeurs définies peuvent être les suivantes :

* **static** : le paramètre régional est extrait de l’ `language` attribut si disponible, sinon du paramètre régional par défaut du serveur.

* **page** : le paramètre régional est extrait de la langue de la page ou de la ressource active si elle est disponible, sinon de l’attribut `language` s’il est disponible, sinon du paramètre régional par défaut du serveur.

* **request** : le paramètre régional est extrait du paramètre régional de la demande ( `request.getLocale()`).

* **auto** : le paramètre régional est extrait de l’ `language` attribut s’il est disponible, sinon de la langue de la page ou de la ressource en cours si disponible, sinon de la requête.

Si l’attribut `source` n’est pas défini :

* If the `language` attribute is set, the `source` attribute defaults to `` `static`.

* If the `language` attribute is not set, the `source` attribute defaults to `auto`.

The &quot;content bundle&quot; can be simply used by standard JSTL `<fmt:message>` tags. La recherche des messages par clés est une opération en deux temps :

1. Tout d’abord, des traductions sont recherchées dans les propriétés JCR de la ressource sous-jacente qui est actuellement restituée. Cela vous permet de définir une boîte de dialogue de composant simple pour modifier ces valeurs.
1. Si le nœud ne contient pas de propriété dont le nom correspond exactement à celui de la clé, la solution de secours consiste à charger un lot de ressources à partir de la requête sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). The language or locale for this bundle is defined by the language and source attributes of the `<cq:setContentBundle>` tag.

The `<cq:setContentBundle>` tag can be used as follows in a jsp.

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

The `<cq:include>` tag includes a resource into the current page.

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

Should you use `<%@ include file="myScript.jsp" %>` or `<cq:include script="myScript.jsp" %>` to include a script?

* The `<%@ include file="myScript.jsp" %>` directive informs the JSP compiler to include a complete file into the current file. C’est comme si le contenu du fichier inclus était collé directement dans le fichier d’origine.
* With the `<cq:include script="myScript.jsp">` tag, the file is included at runtime.

Should you use `<cq:include>` or `<sling:include>`?

* Lorsque vous développez des composants AEM, Adobe vous recommande d’utiliser `<cq:include>`.
* `<cq:include>` vous permet d’inclure directement des fichiers de script en fonction de leur nom lors de l’utilisation de l’attribut script. L’héritage du type de composant et de ressource est alors pris en compte. Généralement, cela s’avère plus simple que d’observer une stricte conformité avec la résolution de script de Sling à l’aide de sélecteurs et d’extensions.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` est devenu obsolète depuis AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) devrait être utilisé à la place.

The `<cq:includeClientLib>` tag Includes a AEM html client library, which can be a js, a css or a theme library. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le fichier jsp. Cette balise est une enveloppe dite de commodité (convenience wrapper) utilisée autour de l’interface de service `com.day.cq.widget.HtmlLibraryManager`.

Elle présente les attributs suivants :

**catégories** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**thème** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

Equivalent to: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

Equivalent à: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**thème** - Un indicateur indiquant uniquement les bibliothèques thématiques ou non thématiques doit être inclus. Si cet attribut est omis, les deux ensembles sont inclus. S’applique uniquement aux inclusions JS et CSS pures (pas aux catégories ni aux inclusions de thème).

The `<cq:includeClientLib>` tag can be used as follows in a jsp:

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

The `<cq:defineObjects>` tag exposes the following, regularly used, scripting objects which can be referenced by the developer. It also exposes the objects defined by the [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) tag.

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
>When the `/libs/foundation/global.jsp` file is included in the script, the `<cq:defineObjects />` tag is automatically included.

### <cq:requestURL> {#cq-requesturl}

The `<cq:requestURL>` tag writes the current request URL to the JspWriter. The two tags [ `<cq:addParam>`](#amp-lt-cq-addparam) and [ `<cq:removeParam>`](#amp-lt-cq-removeparam) and may be used inside the body of this tag to modify the current request URL before it is written.

Cela vous permet de créer des liens vers la page en cours avec des paramètres variables. Cela vous permet, par exemple, de transformer la requête :

`mypage.html?mode=view&query=something` en `mypage.html?query=something`.

The use of `addParam` or `removeParam` only changes the occurrence of the given parameter, all other parameters are unaffected.

`<cq:requestURL>` n’a aucun attribut.

Exemples :

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

The `<cq:addParam>` tag adds a request parameter with the given name and value to the enclosing [ `<cq:requestURL>`](#amp-lt-cq-requesturl) tag.

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

The `<cq:removeParam>` tag removes a request parameter with the given name and value from the enclosing [ `<cq:requestURL>`](#amp-lt-cq-requesturl) tag. Si aucune valeur n’est indiquée, tous les paramètres portant le nom spécifié sont supprimés.

Elle présente les attributs suivants :

**name**

* Nom du paramètre à supprimer

Exemple :

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Bibliothèque de balises Sling {#sling-tag-library}

La bibliothèque de balises Sling comporte des fonctions Sling bien utiles.

Lorsque vous utilisez la bibliothèque de balises Sling dans votre script, ce dernier doit commencer par le code suivant :

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>When the `/libs/foundation/global.jsp` file is included in the script, the sling taglib is automatically declared.

### <sling:include> {#sling-include}

The `<sling:include>` tag includes a resource into the current page.

Elle présente les attributs suivants :

**flush**

* Valeur booléenne qui indique si la sortie doit être vidée ou non avant d’inclure la cible.

**ressource**

* Objet de ressource à inclure dans le traitement de la requête en cours. L’attribut resource ou path doit être spécifié. Si les deux attributs sont spécifiés, l’attribut resource est prioritaire.

**path**

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
>The resolution of the resource and the script that are included with the `<sling:include>` tag is the same as for a normal sling URL resolution. Par défaut, les sélecteurs, l’extension, etc. de la requête en cours sont également utilisés pour le script inclus. They can be modified through the tag attributes: for example `replaceSelectors="foo.bar"` allows you to overwrite the selectors.

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

The `<sling:defineObjects>` tag exposes the following, regularly used, scripting objects which can be referenced by the developer:

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

## Bibliothèque de balises JSTL {#jstl-tag-library}

The [JavaServer Pages Standard Tag Library](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contains a lot of useful and standard tags. The core, formatting and functions taglibs are defined by the `/libs/foundation/global.jsp` as shown in the following snippet.

### Extrait de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

After importing the `/libs/foundation/global.jsp` file as described before, you can use the `c`, `fmt` and `fn` prefixes to access to those taglibs. La documentation officielle de la JSTL est disponible [ici](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
