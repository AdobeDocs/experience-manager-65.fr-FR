---
title: Extension du suivi des événements
description: AEM Analytics vous permet de suivre les interactions utilisateur sur votre site web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 71%

---

# Extension du suivi des événements{#extending-event-tracking}

AEM Analytics vous permet d’effectuer le suivi des interactions utilisateur sur votre site web. En tant que développeur, vous devrez peut-être :

* de suivre la façon dont les visiteurs interagissent avec les composants (cela peut être effectué à l’aide d’[événements personnalisés](#custom-events)) ;
* [d’accéder aux valeurs dans le contexte client](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub) ;
* [d’ajouter des rappels d’enregistrement](#adding-record-callbacks).

>[!NOTE]
>
>Ces informations sont essentiellement génériques, mais elles utilisent [Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour des exemples spécifiques.
>
>Pour obtenir des informations générales sur le développement de composants et de boîtes de dialogue, consultez [Développement de composants](/help/sites-developing/components.md).

## Événements personnalisés {#custom-events}

Les événements personnalisés effectuent le suivi de tout ce qui dépend de la disponibilité d’un composant spécifique sur la page. Cela inclut également les événements spécifiques au modèle, dans la mesure où le composant de page est traité comme un autre composant.

### Suivi des événements personnalisés au chargement de la page {#tracking-custom-events-on-page-load}

Ce type d’opération peut être réalisé en utilisant le pseudo-attribut `data-tracking` (l’ancien attribut d’enregistrement est toujours pris en charge pour la compatibilité descendante). Vous pouvez l’ajouter à n’importe quelle balise HTML.

La syntaxe de `data-tracking` est :

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Vous pouvez transmettre n’importe quel nombre de paires clé-valeur comme second paramètre, appelé payload.

Voici un exemple :

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

Au chargement de la page, tous les attributs `data-tracking` sont collectés et ajoutés à la boutique d’événement du ContextHub où ils peuvent être mappés aux événements Adobe Analytics. Les événements qui ne sont pas mappés ne sont pas suivis par Adobe Analytics. Consultez [Connexion à Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour plus d’informations sur le mappage d’événements.

### Suivi d’événements personnalisés après le chargement d’une page {#tracking-custom-events-after-page-load}

Pour suivre des événements se produisant après le chargement d’une page (tels que des interactions utilisateur), utilisez la fonction JavaScript `CQ_Analytics.record` :

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Où :

* `events` est une chaîne ou un tableau de chaîne (pour plusieurs événements).

* `values` contient toutes les valeurs à tracker
* `collect` est facultatif et renvoie un tableau contenant l’événement et l’objet de données.
* `options` est facultatif et contient des options de suivi des liens comme l’élément HTML `obj` et ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` est un attribut nécessaire, et il est recommandé de le définir sur `<%=resource.getResourceType()%>`.

 Par exemple, avec la définition suivante, un utilisateur cliquant sur le lien **Aller en haut** entraîne le déclenchement de deux événements, `jumptop` et `headlineclick` :

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Accès aux valeurs dans ContextHub {#accessing-values-in-the-contexthub}

L’API JavaScript ContextHub comporte une fonction `getStore(name)` qui renvoie le magasin spécifié, s’il est disponible. Le magasin dispose d’une fonction `getItem(key)` qui renvoie la valeur de la clé spécifiée, si elle est disponible. En utilisant la fonction `getKeys()`, il est possible de récupérer un tableau de clés définies pour le magasin spécifique.

Vous pouvez être averti des modifications de valeur sur un magasin en liant une fonction, à l’aide de la fonction `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

La meilleure façon d’être informé de la disponibilité initiale du ContextHub consiste à utiliser la fonction `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Événements supplémentaires pour ContextHub :**

Toutes les boutiques sont prêtes :

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Une boutique spécifique :

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Consultez également [Référence de l’API ContextHub](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Ajout de rappels d’enregistrement {#adding-record-callbacks}

Des rappels enregistrés avant et après à l’aide des fonctions `CQ_Analytics.registerBeforeCallback(callback,rank)` et `CQ_Analytics.registerAfterCallback(callback,rank)`.

Les deux fonctions prennent une fonction comme premier argument et un rang comme deuxième argument, ce qui détermine l’ordre d’exécution des rappels.

Si votre rappel renvoie false, les rappels suivants dans la chaîne d’exécution ne seront pas exécutés.
