---
title: Personnalisation côté client
description: Personnalisation du comportement ou de l’apparence côté client dans AEM Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%
---
# Personnalisation côté client  {#client-side-customization}

| ⇐ Feature Essentials [&#128279;](essentials.md)**&#x200B;**|[&#x200B;  ⇒ de personnalisation côté serveur &#x200B;](server-customize.md)**&#x200B;** |
|---|---|
|   | ⇒ des assistants Handlebars SCF [&#128279;](handlebars-helpers.md)**&#x200B;** |

Pour personnaliser l’apparence et/ou le comportement d’un composant AEM Communities côté client, il existe plusieurs approches.

Deux approches principales consistent à recouvrir ou étendre un composant.

[Recouvrement](#overlays) un composant modifie le composant par défaut et affecte chaque référence au composant.

[L’extension &#x200B;](#extensions)’un composant, qui porte un nom unique, limite la portée des modifications. Le terme « extend » est utilisé de manière interchangeable avec « override ».

## Recouvrements {#overlays}

Le recouvrement d’un composant permet d’apporter des modifications à un composant par défaut et d’affecter toutes les instances qui utilisent le paramètre par défaut.

Pour ce faire, modifiez une copie du composant par défaut dans le répertoire /**apps**, plutôt que le composant d’origine dans le répertoire /**libs**. Le composant est construit avec un chemin relatif identique, sauf que « libs » est remplacé par « apps ».

Le répertoire /apps est la première recherche effectuée pour résoudre des demandes. S’il est introuvable, la version par défaut du répertoire /libs est utilisée.

Le composant par défaut du répertoire /libs ne doit jamais être modifié, car les correctifs et mises à niveau ultérieurs sont libres de modifier le répertoire /libs de toute manière nécessaire tout en conservant les interfaces publiques.

Cette opération diffère de l’extension d’un composant par défaut [extension](#extensions), où le souhait est d’apporter des modifications pour une utilisation spécifique, en créant un chemin d’accès unique au composant et en s’appuyant sur le référencement du composant par défaut d’origine dans le répertoire /libs comme type de super ressource.

Pour obtenir un exemple rapide de recouvrement du composant Commentaires, consultez le tutoriel [Recouvrement du composant Commentaires](overlay-comments.md).

## Extensions {#extensions}

L’extension (remplacement) d’un composant est une méthode permettant d’apporter des modifications pour une utilisation spécifique sans affecter toutes les instances qui utilisent la valeur par défaut. Le composant étendu est nommé de manière unique dans le dossier /apps et fait référence au composant par défaut dans le dossier /libs. Par conséquent, la conception et le comportement par défaut d’un composant ne sont pas modifiés.

Cela diffère du [recouvrement](#overlays) composant par défaut où la nature de Sling résout les références relatives au dossier apps/ avant la recherche dans le dossier libs/ , de sorte que la conception ou le comportement d’un composant est modifié globalement.

Pour obtenir un exemple rapide d’extension du composant Comments, consultez le tutoriel [Extension du composant Comments](extend-comments.md).

## Liaison JavaScript {#javascript-binding}

Le script HBS du composant doit être lié aux objets, modèles et vues JavaScript qui implémentent cette fonctionnalité.

La valeur de l’attribut `data-scf-component` peut être la valeur par défaut, par exemple **`social/tally/components/hbs/rating`**, ou un composant étendu (personnalisé) pour les fonctionnalités personnalisées, par exemple **weretail/components/hbs/rating**.

Pour lier un composant, l’intégralité du script du composant doit être incluse dans un élément &lt;div> avec les attributs suivants :

* `data-component-id`=&quot;`{{id}}`&quot;

  résout sur la propriété id à partir du contexte

* `data-scf-component`=« *&lt;resourceType>*

Par exemple, depuis `/apps/weretail/components/hbs/rating/rating.hbs` :

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriétés personnalisées {#custom-properties}

Lors de l’extension ou du recouvrement d’un composant, il est possible d’ajouter des propriétés à une boîte de dialogue modifiée.

Toutes les propriétés définies sur un composant/une ressource sont accessibles en référençant les clés de propriété dans le modèle Handlebars :

`{{properties.<property_name>}}`

## CSS d’application de la peau {#skinning-css}

La personnalisation des composants pour qu’ils correspondent au thème global du site web peut être réalisée en « créant l’habillage », c’est-à-dire en modifiant les couleurs, les polices, les images, les boutons, les liens, l’espacement et même le positionnement dans une certaine mesure.

La peau peut être créée en remplaçant de manière sélective les styles de structure ou en écrivant des feuilles de style entièrement nouvelles. Les composants SCF définissent des classes CSS d’espace de noms, modulaires et sémantiques qui affectent les différents éléments qui constituent un composant.

Pour appliquer l’enveloppe à un composant :

1. Identifiez les éléments à modifier (par exemple, la zone du compositeur, les boutons de la barre d’outils, la police du message, etc.).
1. Identifiez la classe/les règles CSS qui affectent ces éléments.
1. Créez un fichier de feuille de style (.css).
1. Incluez la feuille de style dans un dossier de bibliothèque cliente ([clientlibs](#clientlibs-for-scf)) pour votre site et assurez-vous qu’elle est incluse dans vos modèles et pages avec [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redéfinissez les classes et règles CSS que vous avez identifiées (#2) dans votre feuille de style et ajoutez des styles.

Les styles personnalisés remplacent désormais les styles de structure par défaut et le composant est rendu avec le nouvel habillage.

>[!CAUTION]
>
>Tout nom de classe CSS précédé du préfixe `scf-js` a une utilisation spécifique dans le code JavaScript. Ces classes affectent l’état d’un composant (par exemple, le fait de passer de masqué à visible) et ne doivent ni être remplacées ni supprimées.
>
>Bien que les classes `scf-js` n&#39;affectent pas les styles, les noms de classe peuvent être utilisés dans les feuilles de style, mais il est à noter que, dans la mesure où ils contrôlent les états des éléments, il peut y avoir des effets secondaires.

## Extension de JavaScript {#extending-javascript}

Pour étendre l’implémentation d’un JavaScript de composants, vous devez :

1. Créez un composant pour votre application avec un jcr:resourceSuperType défini sur la valeur du jcr du composant étendu:resourceType par exemple, social/forum/components/hbs/forum.
1. Examinez le JavaScript du composant SCF par défaut pour déterminer les méthodes à enregistrer à l’aide de SCF.registerComponent().
1. Copiez le JavaScript du composant étendu ou commencez à partir de zéro.
1. Étendez la méthode .
1. Utilisez SCF.registerComponent() pour enregistrer toutes les méthodes avec les valeurs par défaut ou les objets et vues personnalisés.

### forum.js : Exemple d’extension de forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## Balises de script {#script-tags}

Les balises de script font partie intégrante de la structure côté client. Ils constituent la colle qui permet de lier les balises générées côté serveur aux modèles et vues côté client.

Les balises de script dans les scripts SCF ne doivent pas être supprimées lors du remplacement de composants. Les balises de script SCF créées automatiquement pour injecter du code JSON dans HTML sont identifiées avec l’attribut `data-scf-json=true`.

## Bibliothèques clientes pour SCF {#clientlibs-for-scf}

L’utilisation de [&#x200B; bibliothèques côté client &#x200B;](../../help/sites-developing/clientlibs.md) (clientlibs) permet d’organiser et d’optimiser le JavaScript et le CSS utilisés pour effectuer le rendu du contenu sur le client.

Les bibliothèques clientes pour SCF suivent un modèle de dénomination très spécifique pour deux variantes, qui ne varient que par la présence de « author » dans le nom de la catégorie :

| Variante Clientlib | Modèle de la propriété Catégories |
|--- |--- |
| bibliothèque cliente complète | cq.social.hbs.&lt;nom du composant> |
| bibliothèque cliente de création | cq.social.author.hbs.&lt;nom du composant> |

### Bibliothèque cliente complète {#complete-clientlibs}

Les bibliothèques clientes complètes (hors création) incluent des dépendances et sont pratiques à inclure dans l’interface utilisateur:includeClientLib.

Ces versions se trouvent dans :

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Par exemple :

* Nœud du dossier client : `/etc/clientlibs/social/hbs/forum`
* Propriété Catégories : `cq.social.hbs.forum`

Le [guide des composants de communauté](components-guide.md) répertorie toutes les bibliothèques clientes requises pour chaque composant SCF.

[Clientlibs pour les composants de communautés](clientlibs.md) décrit comment ajouter des bibliothèques clientes à une page.

### Créer des bibliothèques clientes {#author-clientlibs}

Les bibliothèques clientes de la version de création sont réduites au JavaScript minimal nécessaire à l’implémentation du composant.

Ces clientlibs ne doivent jamais être directement incluses, mais sont plutôt disponibles pour être intégrées à d’autres clientlibs, qui sont conçues à la main pour un site.

Ces versions se trouvent dans le dossier SCF libs :

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Par exemple :

* Nœud du dossier client : `/libs/social/forum/hbs/forum/clientlibs`
* Propriété Catégories : `cq.social.author.hbs.forum`

Remarque : bien que les bibliothèques clientes de création n’incorporent jamais d’autres bibliothèques, elles répertorient leurs dépendances. Lorsqu’elles sont incorporées dans d’autres bibliothèques, les dépendances ne sont pas automatiquement extraites et doivent également être incorporées.

Les bibliothèques clientes de création requises peuvent être identifiées en insérant « author » dans les bibliothèques clientes répertoriées pour chaque composant SCF dans le [guide des composants de la communauté](components-guide.md).

### Considérations relatives à l’utilisation {#usage-considerations}

Chaque site est différent dans la manière dont il gère les bibliothèques clientes. Divers facteurs comprennent :

* Vitesse globale : peut-être que le souhait est que le site soit réactif, mais il est acceptable que la première page soit un peu lente à charger. Si la plupart des pages utilisent le même JavaScript, les différents JavaScript peuvent être incorporés dans une bibliothèque cliente et référencés à partir de la première page à charger. Le JavaScript de ce téléchargement unique reste en cache, ce qui réduit la quantité de données à télécharger pour les pages suivantes.
* Délai court jusqu’à la première page : il est peut-être préférable que la première page se charge rapidement. Dans ce cas, le JavaScript se trouve dans plusieurs petits fichiers à référencer uniquement là où cela est nécessaire.
* Équilibre entre le premier chargement de page et les téléchargements suivants.

| ⇐ Feature Essentials [&#128279;](essentials.md)**&#x200B;**|[&#x200B;  ⇒ de personnalisation côté serveur &#x200B;](server-customize.md)**&#x200B;** |
|---|---|
|   | ⇒ des assistants Handlebars SCF [&#128279;](handlebars-helpers.md)**&#x200B;** |
