---
title: Extension du suivi des événements
seo-title: Extension du suivi des événements
description: AEM Analytics vous permet d’effectuer le suivi des interactions utilisateur sur votre site web.
seo-description: AEM Analytics vous permet d’effectuer le suivi des interactions utilisateur sur votre site web.
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 53%

---


# Extension du suivi des événements{#extending-event-tracking}

AEM Analytics vous permet d’effectuer le suivi des interactions utilisateur sur votre site web. En tant que développeur, vous pouvez avoir besoin :

* de suivre la façon dont les visiteurs interagissent avec les composants Pour ce faire, [événements personnalisés.](#custom-events)
* [Accédez aux valeurs dans ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [d’ajouter des rappels d’enregistrement](#adding-record-callbacks).

>[!NOTE]
>
>Ces informations sont essentiellement génériques, mais elles utilisent [Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour des exemples spécifiques.
>
>Pour obtenir des informations générales sur le développement de composants et de boîtes de dialogue, voir [Développement de composants](/help/sites-developing/components.md).

## Événements personnalisés {#custom-events}

Les événements personnalisés suivent tout ce qui dépend de la disponibilité d’un élément spécifique sur la page. Cela inclut également les événements spécifiques à un modèle, car le composant de page est traité comme un autre composant.

### Suivi d’événements personnalisés lors du chargement d’une page {#tracking-custom-events-on-page-load}

Cela peut être fait à l&#39;aide du pseudo-attribut `data-tracking` (l&#39;ancien attribut d&#39;enregistrement est toujours pris en charge pour la compatibilité ascendante). Vous pouvez l’ajouter à n’importe quelle balise HTML.

La syntaxe de `data-tracking` est

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Vous pouvez transmettre n’importe quel nombre de paires clé-valeur comme second paramètre appelé charge utile.

En voici un exemple :

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

Au chargement de la page, tous les attributs `data-tracking` seront collectés et ajoutés au magasin de événements de ContextHub, où ils peuvent être mappés aux événements Adobe Analytics. Les événements non mappés ne seront pas suivis par Adobe Analytics. Voir [Connexion à Adobe Analytics](/help/sites-administering/adobeanalytics.md) pour plus d’informations sur le mappage des événements.

### Suivi d’événements personnalisés après le chargement d’une page {#tracking-custom-events-after-page-load}

Pour suivre des événements se produisant après le chargement d’une page (tels que des interactions utilisateur), utilisez la fonction JavaScript `CQ_Analytics.record` :

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Où :

* `events` est une chaîne ou un tableau de chaîne (pour plusieurs événements).

* `values` contient toutes les valeurs à suivre.
* `collect` est facultatif et renvoie un tableau contenant l’événement et l’objet de données.
* `options` est facultatif et contient des options de suivi de liens telles que l’élément HTML  `obj` et  ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` est un attribut nécessaire et il est recommandé de le définir sur  `<%=resource.getResourceType()%>`

Par exemple, avec la définition suivante, un utilisateur cliquant sur le lien **Aller en haut** entraîne le déclenchement de deux événements, `jumptop` et `headlineclick` :

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Accès aux valeurs dans ContextHub {#accessing-values-in-the-contexthub}

L’API JavaScript ContextHub possède une fonction `getStore(name)` qui renvoie le magasin spécifié, le cas échéant. La boutique possède une fonction `getItem(key)` qui renvoie la valeur de la clé spécifiée, si elle est disponible. La fonction `getKeys()` permet de récupérer un tableau de clés définies pour le magasin spécifique.

Vous pouvez être averti des modifications de valeur d&#39;un magasin en liant une fonction à l&#39;aide de la fonction `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

Le meilleur moyen d&#39;être informé de la disponibilité initiale de ContextHub est d&#39;utiliser la fonction `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Événements supplémentaires pour ContextHub :**

Toutes les boutiques sont prêtes :

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Une boutique spécifique :

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Voir aussi la [Référence API ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference) complète

## Ajout de rappels d’enregistrement {#adding-record-callbacks}

Les rappels avant et après sont enregistrés à l&#39;aide des fonctions `CQ_Analytics.registerBeforeCallback(callback,rank)` et `CQ_Analytics.registerAfterCallback(callback,rank)`.

Les deux fonctions prennent une fonction comme premier argument et un classement comme deuxième argument, ce qui détermine l’ordre dans lequel les rappels sont exécutés.

Si votre rappel renvoie false, les rappels suivants dans la chaîne d’exécution ne sont pas exécutés.
