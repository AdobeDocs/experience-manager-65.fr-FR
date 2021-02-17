---
title: Extension de ContextHub
seo-title: Extension de ContextHub
description: Définissez de nouveaux types de modules et de magasins ContextHub lorsque ceux qui sont fournis ne répondent pas à vos besoins en termes de solution.
seo-description: Définissez de nouveaux types de modules et de magasins ContextHub lorsque ceux qui sont fournis ne répondent pas à vos besoins en termes de solution.
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 97%

---


# Extension de ContextHub{#extending-contexthub}

Définissez de nouveaux types de modules et de magasins ContextHub lorsque ceux qui sont fournis ne répondent pas à vos besoins en termes de solution.

## Création de candidats de magasin personnalisés  {#creating-custom-store-candidates}

Les magasins ContextHub sont créés à partir de candidats de magasin enregistrés. Pour créer un magasin personnalisé, vous devez créer et enregistrer un candidat de magasin.

Le fichier JavaScript contenant le code qui crée et enregistre le candidat de magasin doit être inclus dans un [dossier de bibliothèque cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La catégorie du dossier doit correspondre au schéma suivant :

```xml
contexthub.store.[storeType]
```

La partie `[storeType]` de la catégorie correspond au `storeType` auprès duquel le candidat de magasin est enregistré. (voir [Enregistrement d’un candidat de magasin ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Par exemple, pour le storeType `contexthub.mystore`, la catégorie du dossier de bibliothèque cliente doit être `contexthub.store.contexthub.mystore`.

### Création d’un candidat de magasin ContextHub {#creating-a-contexthub-store-candidate}

Pour créer un candidat de magasin, vous utilisez la fonction [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) afin d’étendre l’un des magasins de base :

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Notez que chaque magasin de base étend le magasin [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core).

L’exemple suivant crée l’extension la plus simple du candidat de magasin `ContextHub.Store.PersistedStore` :

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

En réalité, vos candidats de magasin personnalisés définissent des fonctions supplémentaires ou remplacent la configuration initiale du magasin. Plusieurs [exemples de candidats de magasin](/help/sites-developing/ch-samplestores.md) sont installés dans le référentiel sous `/libs/granite/contexthub/components/stores`. Pour tirer profit de ces exemples, utilisez CRXDE Lite afin d’ouvrir les fichiers JavaScript.

### Enregistrement d’un candidat de magasin ContextHub {#registering-a-contexthub-store-candidate}

Enregistrez un candidat de magasin pour l’intégrer dans la structure ContextHub et permettre la création de magasins à partir de celui-ci. Pour enregistrer un candidat de magasin, utilisez la fonction [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la classe `ContextHub.Utils.storeCandidates`.

Lorsque vous enregistrez un candidat de magasin, vous attribuez un nom au type de magasin. Lorsque vous créez un magasin à partir du candidat, vous utilisez le type de magasin pour identifier le candidat sur lequel il repose.

Lorsque vous enregistrez un candidat de magasin, vous indiquez sa priorité. Lorsqu’un candidat de magasin est enregistré avec le même type qu’un candidat déjà enregistré, c’est le candidat ayant la priorité la plus élevée qui est utilisé. Par conséquent, vous pouvez remplacer les candidats de magasin existants par les nouvelles implémentations.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Dans la plupart des cas, un seul candidat est nécessaire et la priorité peut être définie sur `0`. Toutefois, si vous êtes intéressé, vous pouvez en apprendre davantage sur les [enregistrements plus avancés](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies), qui permettent de choisir l’une des implémentations de magasin en fonction de la condition JavaScript (`applies`) et de la priorité du candidat.

## Création de types de modules d’interface utilisateur ContextHub {#creating-contexthub-ui-module-types}

Vous pouvez créer des types de modules d’interface utilisateur personnalisés lorsque ceux qui sont [installés avec ContextHub](/help/sites-developing/ch-samplemodules.md) ne répondent pas à vos attentes. Pour créer un type de module d’interface utilisateur, créez un moteur de rendu de module en étendant la classe `ContextHub.UI.BaseModuleRenderer`, puis en l’enregistrant auprès de `ContextHub.UI`.

Pour créer un moteur de rendu de module d’interface utilisateur, créez un objet `Class` contenant le logiciel qui effectue le rendu de ce module. Votre classe doit, au minimum, effectuer les actions suivantes :

* Étendez la classe `ContextHub.UI.BaseModuleRenderer`. Cette classe est l’implémentation de base de tous les moteurs de rendu de module d’IU. L’objet `Class` définit une propriété nommée `extend` que vous utilisez pour désigner cette classe comme celle en cours d’extension.

* Indiquez une configuration par défaut. Créez une propriété `defaultConfig`. Cette propriété est un objet qui contient les propriétés définies pour le module d’IU [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type), ainsi que toute autre propriété dont vous avez besoin.

La source de `ContextHub.UI.BaseModuleRenderer` se trouve à l’adresse /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Pour enregistrer le moteur de rendu, utilisez la méthode [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) de la classe `ContextHub.UI`. Vous devez indiquer un nom pour le type de module. Lorsque les administrateurs créent un module d’IU basé sur ce moteur de rendu, ils spécifient ce nom.

Créez et enregistrez la classe du module de rendu dans une fonction anonyme à exécution automatique. L’exemple suivant est basé sur le code source du module d’IU contexthub.browserinfo. Ce module est une extension simple de la classe `ContextHub.UI.BaseModuleRenderer`.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

Le fichier JavaScript contenant le code qui crée et enregistre le module de rendu doit être inclus dans un [dossier de bibliothèque cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La catégorie du dossier doit correspondre au schéma suivant :

```xml
contexthub.module.[moduleType]
```

La partie `[moduleType]` de la catégorie correspond au `moduleType` auprès duquel le moteur de rendu du module est enregistré. Par exemple, pour le `moduleType` de `contexthub.browserinfo`, la catégorie du dossier de bibliothèque cliente doit être `contexthub.module.contexthub.browserinfo`.
