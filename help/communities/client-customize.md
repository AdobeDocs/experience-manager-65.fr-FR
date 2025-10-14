---
title: Personnalisation côté client
description: Personnalisation du comportement ou de l’aspect côté client dans AEM Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Personnalisation côté client  {#client-side-customization}

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[Personnalisation côté serveur ⇒](server-customize.md)** |
|---|---|
|   | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |

Plusieurs méthodes permettent de personnaliser l’aspect et/ou le comportement d’un composant AEM Communities côté client.

Deux approches principales sont de superposer ou d’étendre un composant.

[Recouvrement](#overlays) un composant modifie le composant par défaut et affecte chaque référence au composant.

[Extension](#extensions) un composant, dont le nom est unique, limite la portée des modifications. Le terme &quot;extension&quot; est utilisé de manière interchangeable avec &quot;override&quot;.

## Recouvrements {#overlays}

Le recouvrement d’un composant est une méthode permettant d’apporter des modifications à un composant par défaut et d’affecter toutes les instances qui utilisent le composant par défaut.

La superposition est effectuée en modifiant une copie du composant par défaut dans le répertoire /**apps**, plutôt que de modifier le composant d’origine dans le répertoire /**libs**. Le composant est construit avec un chemin relatif identique, à l’exception près que &quot;libs&quot; est remplacé par &quot;apps&quot;.

Le répertoire /apps est le premier emplacement recherché pour résoudre les requêtes. S’il est introuvable, la version par défaut du répertoire /libs est utilisée.

Le composant par défaut du répertoire /libs ne doit jamais être modifié, car les correctifs et mises à niveau ultérieurs peuvent modifier le répertoire /libs de toute manière nécessaire tout en conservant les interfaces publiques.

Ceci diffère de [l’extension](#extensions) d’un composant par défaut dans lequel le désir est d’apporter des modifications pour une utilisation spécifique, en créant un chemin d’accès unique au composant et en utilisant le référencement du composant par défaut d’origine dans le répertoire /libs comme type de super-ressource.

Pour un exemple rapide de superposition du composant Commentaires, essayez le [tutoriel sur le composant Commentaires de superposition](overlay-comments.md).

## Extensions {#extensions}

L’extension (remplacement) d’un composant est une méthode permettant d’apporter des modifications pour une utilisation spécifique sans affecter toutes les instances qui utilisent la valeur par défaut. Le composant étendu est nommé de manière unique dans le dossier /apps et référence le composant par défaut dans le dossier /libs . Par conséquent, la conception et le comportement par défaut d’un composant ne sont pas modifiés.

Ceci diffère de la [superposition](#overlays) du composant par défaut dans lequel la nature de Sling résout les références relatives aux applications/dossiers avant la recherche dans le dossier libs/ , de sorte que la conception ou le comportement d’un composant est modifié globalement.

Pour un exemple rapide d’extension du composant Commentaires, essayez le [tutoriel Étendre le composant Commentaires](extend-comments.md).

## Liaison JavaScript {#javascript-binding}

Le script HBS du composant doit être lié aux objets, modèles et vues JavaScript qui implémentent cette fonctionnalité.

La valeur de l’attribut `data-scf-component` peut être la valeur par défaut, par exemple **`social/tally/components/hbs/rating`**, ou un composant étendu (personnalisé) pour les fonctionnalités personnalisées, comme **weretail/components/hbs/rating**.

Pour lier un composant, le script de composant entier doit être inclus dans un élément &lt;div> avec les attributs suivants :

* `data-component-id`=&quot;`{{id}}`&quot;

  résout la propriété id du contexte.

* `data-scf-component`=&quot;*&lt;resourceType>*

Par exemple, de `/apps/weretail/components/hbs/rating/rating.hbs` :

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriétés personnalisées {#custom-properties}

Lors de l’extension ou du recouvrement d’un composant, il est possible d’ajouter des propriétés à une boîte de dialogue modifiée.

Toutes les propriétés définies sur un composant/une ressource sont accessibles en référençant les clés de propriété dans le modèle handlebars :

`{{properties.<property_name>}}`

## Esquisse de CSS {#skinning-css}

Il est possible de personnaliser les composants pour qu’ils correspondent au thème global du site web en les &quot;peignant&quot; : en modifiant dans une certaine mesure les couleurs, les polices, les images, les boutons, les liens, l’espacement et même le positionnement.

L’habillage peut être réalisé en remplaçant sélectivement les styles de structure ou en écrivant des feuilles de style entièrement nouvelles. Les composants SCF définissent des classes CSS sémantiques, modulaires et avec espace de noms qui affectent les différents éléments qui constituent un composant.

Pour appliquer l’habillage d’un composant :

1. Identifiez les éléments à modifier (par exemple, la zone de compositeur, les boutons de la barre d’outils, la police du message, etc.).
1. Identifiez la classe/les règles CSS qui affectent ces éléments.
1. Créez un fichier de feuille de style (.css).
1. Incluez la feuille de style dans un dossier de bibliothèques clientes ([clientlibs](#clientlibs-for-scf)) pour votre site et assurez-vous qu’elle est incluse à partir de vos modèles et pages avec [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redéfinissez les classes CSS et les règles que vous avez identifiées (#2) dans votre feuille de style et ajoutez des styles.

Les styles personnalisés remplacent désormais les styles de structure par défaut et le composant est rendu avec le nouvel habillage.

>[!CAUTION]
>
>Tout nom de classe CSS précédé du préfixe `scf-js` a une utilisation spécifique dans le code JavaScript. Ces classes affectent l’état d’un composant (par exemple, basculez de masqué à visible) et ne doivent pas être remplacées ni supprimées.
>
>Bien que les classes `scf-js` n’affectent pas les styles, les noms de classe peuvent être utilisés dans les feuilles de style avec l’avertissement que, lorsqu’elles contrôlent les états des éléments, il peut y avoir des effets secondaires.

## Extension de JavaScript {#extending-javascript}

Pour étendre une mise en oeuvre JavaScript de composants, vous devez :

1. Créez un composant pour votre application avec un jcr:resourceSuperType défini sur la valeur de jcr:resourceType du composant étendu, par exemple, social/forum/components/hbs/forum.
1. Examinez le JavaScript du composant SCF par défaut pour déterminer les méthodes qui doivent être enregistrées à l’aide de SCF.registerComponent().
1. Copiez le JavaScript du composant étendu ou partez de zéro.
1. Étendez la méthode .
1. Utilisez SCF.registerComponent() pour enregistrer toutes les méthodes avec les valeurs par défaut ou les objets et vues personnalisés.

### forum.js : exemple d’extension de forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

Les balises de script font partie intégrante de la structure côté client. Il s’agit de la colle qui permet de lier les balises générées côté serveur aux modèles et aux vues côté client.

Les balises de script dans les scripts SCF ne doivent pas être supprimées lors du recouvrement ou du remplacement de composants. Les balises de script SCF créées automatiquement pour injecter du code JSON dans l’HTML sont identifiées avec l’attribut `data-scf-json=true`.

## Clientlibs pour SCF {#clientlibs-for-scf}

L’utilisation de [bibliothèques côté client](../../help/sites-developing/clientlibs.md) (clientlibs) permet d’organiser et d’optimiser JavaScript et CSS utilisés pour le rendu du contenu sur le client.

Les clientlibs pour SCF suivent un modèle de dénomination très spécifique pour deux variantes, qui varie uniquement en fonction de la présence de &quot;author&quot; dans le nom de la catégorie :

| Variante de bibliothèque cliente | Modèle de propriété Catégories |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;nom du composant> |
| clientlib de création | cq.social.author.hbs.&lt;nom du composant> |

### Complète Clientlibs {#complete-clientlibs}

Les clientlibs complètes (non-auteur) incluent des dépendances et sont pratiques pour inclure avec ui:includeClientLib.

Ces versions sont disponibles dans :

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Par exemple :

* Noeud de dossier client : `/etc/clientlibs/social/hbs/forum`
* Propriété Categories : `cq.social.hbs.forum`

Le [&#x200B; Guide des composants de la communauté &#x200B;](components-guide.md) répertorie les bibliothèques clientes complètes requises pour chaque composant SCF.

[Clientlibs for Communities Components](clientlibs.md) décrit comment ajouter des clientlibs à une page.

### Création de bibliothèques clientes {#author-clientlibs}

Les clientlibs de version de création sont réduites au minimum JavaScript nécessaire pour mettre en oeuvre le composant.

Ces clientlibs ne doivent jamais être directement incluses, mais sont disponibles pour être incorporées dans d’autres clientlibs, qui sont conçues à la main pour un site.

Ces versions se trouvent dans le dossier libs SCF :

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Par exemple :

* Noeud de dossier client : `/libs/social/forum/hbs/forum/clientlibs`
* Propriété Categories : `cq.social.author.hbs.forum`

Remarque : bien que les bibliothèques clientes de création n’incorporent jamais d’autres bibliothèques, elles répertorient leurs dépendances. Lorsqu’elles sont incorporées dans d’autres bibliothèques, les dépendances ne sont pas automatiquement extraites et doivent également être incorporées.

Les clientlibs d’auteur requises peuvent être identifiées en insérant &quot;author&quot; dans les clientlibs répertoriées pour chaque composant SCF dans le [guide des composants de communauté](components-guide.md).

### Considérations sur l’utilisation {#usage-considerations}

Chaque site est différent dans la manière dont il gère les bibliothèques clientes. Les facteurs suivants sont à prendre en compte :

* Vitesse globale : peut-être que le site souhaite être réactif, mais qu’il est acceptable que la première page soit un peu lente à charger. Si la plupart des pages utilisent le même JavaScript, les différentes JavaScript peuvent être incorporées dans une bibliothèque cliente et référencées à partir de la première page à charger. Le JavaScript de ce téléchargement unique reste mis en cache, ce qui réduit la quantité de données à télécharger pour les pages suivantes.
* Temps court jusqu’à la première page : peut-être que le désir est que la première page se charge rapidement. Dans ce cas, le JavaScript se trouve dans plusieurs petits fichiers à référencer uniquement lorsque cela s’avère nécessaire.
* Équilibre entre le chargement de la première page et les téléchargements ultérieurs.

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[Personnalisation côté serveur ⇒](server-customize.md)** |
|---|---|
|   | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |
