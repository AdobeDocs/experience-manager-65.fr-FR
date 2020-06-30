---
title: Personnalisation côté client
seo-title: Personnalisation côté client
description: Personnalisation du comportement ou de l’aspect côté client en AEM Communities
seo-description: Personnalisation du comportement ou de l’aspect côté client en AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: efa6c7be93908b2f264da4689caa9c02912c0f0a
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# Personnalisation côté client  {#client-side-customization}

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

Pour personnaliser l’aspect et/ou le comportement d’un composant AEM Communities côté client, plusieurs approches sont possibles.

Deux approches principales consistent à superposer ou à étendre un composant.

[Le fait de superposer](#overlays) un composant modifie le composant par défaut et affecte chaque référence au composant.

[L’extension](#extensions) d’un composant, dont le nom est unique, limite la portée des modifications. Le terme &quot;extension&quot; est utilisé de manière interchangeable avec &quot;override&quot;.

## Recouvrements {#overlays}

Le chevauchement d’un composant est une méthode permettant d’apporter des modifications à un composant par défaut et d’affecter toutes les instances qui utilisent le composant par défaut.

L&#39;incrustation s&#39;effectue en modifiant une copie du composant par défaut dans le répertoire /**apps** , plutôt que de modifier le composant d&#39;origine dans le répertoire /**libs** . Le composant est construit avec un chemin relatif identique, sauf que &#39;libs&#39; est remplacé par &#39;apps&#39;.

Le répertoire /apps est le premier répertoire recherché pour résoudre les requêtes. S&#39;il n&#39;est pas trouvé, la version par défaut située dans le répertoire /libs est utilisée.

Le composant par défaut du répertoire /libs ne doit jamais être modifié car les correctifs et mises à niveau futurs sont libres de modifier le répertoire /libs de toute manière nécessaire tout en conservant les interfaces publiques.

Cela diffère de l&#39; [extension](#extensions) d&#39;un composant par défaut où le désir est d&#39;apporter des modifications pour une utilisation spécifique, en créant un chemin d&#39;accès unique au composant et en se basant sur le référencement du composant par défaut d&#39;origine dans le répertoire /libs comme type de super ressource.

Pour un exemple rapide de superposition du composant de commentaires, essayez le didacticiel [](overlay-comments.md)Incrustation du composant de commentaires.

## Extensions {#extensions}

L’extension (remplacement) d’un composant est une méthode permettant d’apporter des modifications à une utilisation spécifique sans affecter toutes les instances qui utilisent la valeur par défaut. Le composant étendu porte un nom unique dans le dossier /apps et fait référence au composant par défaut dans le dossier /libs. Par conséquent, la conception et le comportement par défaut d&#39;un composant ne sont pas modifiés.

Il s’agit d’une différence par rapport au fait de [superposer](#overlays) le composant par défaut dans lequel la nature de Sling résout les références relatives aux applications/ dossiers avant de rechercher dans le dossier libs/, de sorte que la conception ou le comportement d’un composant est modifié globalement.

Pour un exemple rapide d&#39;extension du composant de commentaires, essayez le didacticiel [](extend-comments.md)Étendre le composant de commentaires.

## Liaison JavaScript {#javascript-binding}

Le script HBS pour le composant doit être lié aux objets, modèles et vues JavaScript qui implémentent cette fonctionnalité.

La valeur de l’ `data-scf-component` attribut peut être la valeur par défaut, telle que **`social/tally/components/hbs/rating`** ou un composant étendu (personnalisé) pour des fonctionnalités personnalisées, telles que **weretail/components/hbs/rating**.

Pour lier un composant, le script de composant entier doit être inclus dans un élément &lt;div> avec les attributs suivants :

* `data-component-id`=&quot;{{id}}&quot;

   résout la propriété id du contexte

* `data-scf-component`=&quot;*&lt;resourceType>*

Par exemple, de `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriétés personnalisées {#custom-properties}

Lors de l’extension ou du recouvrement d’un composant, il est possible d’ajouter des propriétés à une boîte de dialogue modifiée.

Toutes les propriétés définies sur un composant/une ressource sont accessibles en référençant les clés de propriété dans le modèle de barres de poignées :

`{{properties.<property_name>}}`

## Esquisse de CSS {#skinning-css}

La personnalisation des composants pour correspondre au thème global du site Web peut être réalisée en &quot;habillant&quot; - en modifiant les couleurs, les polices, les images, les boutons, les liens, l&#39;espacement et même le positionnement dans une certaine mesure.

L&#39;habillage peut être réalisé en remplaçant sélectivement les styles de cadre ou en écrivant des feuilles de style entièrement nouvelles. Les composants SCF définissent des classes CSS espacées de noms, modulaires et sémantiques qui affectent les différents éléments qui composent un composant.

Pour habiller un composant :

1. Identifiez les éléments que vous souhaitez modifier (par exemple, zone de compositeur, boutons de barre d’outils, police du message, etc.).
1. Identifiez la classe/les règles CSS qui affectent ces éléments.
1. Créez un fichier de feuille de style (.css).
1. Incluez la feuille de style dans un dossier de bibliothèque client ([clientlibs](#clientlibs-for-scf)) pour votre site et assurez-vous qu’elle est incluse dans vos modèles et pages avec [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redéfinissez les classes CSS et les règles que vous avez identifiées (#2) dans votre feuille de style et ajoutez des styles.

Les styles personnalisés remplacent désormais les styles de cadre par défaut et le composant est rendu avec le nouvel habillage.

>[!CAUTION]
>
>Tout nom de classe CSS précédé du préfixe `scf-js` a une utilisation spécifique dans le code JavaScript. Ces classes affectent l’état d’un composant (par exemple, bascule de masqué à visible) et ne doivent ni être remplacées ni supprimées.
>
>Bien que les `scf-js` classes n&#39;affectent pas les styles, les noms de classe peuvent être utilisés dans les feuilles de style avec la mise en garde que, dans la mesure où ils contrôlent l&#39;état des éléments, il peut y avoir des effets secondaires.


## Extension de JavaScript {#extending-javascript}

Pour étendre une implémentation JavaScript de composants, vous devez :

1. Créez un composant pour votre application avec un jcr:resourceSuperType défini sur la valeur de jcr:resourceType du composant étendu, par exemple social/forum/components/hbs/forum.
1. Examinez le script JavaScript du composant SCF par défaut pour déterminer les méthodes à enregistrer à l&#39;aide de SCF.registerComponent().
1. Copiez à partir de zéro le code JavaScript ou le début du composant étendu.
1. Étendez la méthode.
1. Utilisez SCF.registerComponent() pour enregistrer toutes les méthodes avec les valeurs par défaut ou les objets et vues personnalisés.

### forum.js : Exemple d&#39;extension du forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

Les balises de script font partie intégrante de la structure côté client. Il s’agit de la colle qui permet de lier les balises générées côté serveur aux modèles et vues côté client.

Les balises de script dans les scripts SCF ne doivent pas être supprimées lors du recouvrement ou du remplacement de composants. Les balises de script SCF créées automatiquement pour injecter JSON dans le code HTML sont identifiées avec l’attribut `data-scf-json=true`.

## Clientlibs pour SCF {#clientlibs-for-scf}

L’utilisation de bibliothèques [côté](../../help/sites-developing/clientlibs.md) client (clientlibs) permet d’organiser et d’optimiser le code JavaScript et le code CSS utilisés pour générer le contenu sur le client.

Les clientlibs pour SCF suivent un modèle de dénomination très spécifique pour deux variantes, qui varie uniquement en fonction de la présence de &quot;author&quot; dans le nom de la catégorie :

| Variante Clientlib | Modèle pour la propriété Catégories |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;nom du composant> |
| auteur clientlib | cq.social.author.hbs.&lt;nom du composant> |

### Compléter les bibliothèques clientes {#complete-clientlibs}

Les clientlibs complets (non-auteur) incluent des dépendances et sont pratiques pour inclure avec ui:includeClientLib.

Ces versions se trouvent dans :

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Par exemple :

* Noeud de dossier client : `/etc/clientlibs/social/hbs/forum`
* Catégories, propriété : `cq.social.hbs.forum`

Les composants [de la communauté guident](components-guide.md) les clientlibs complets requis pour chaque composant SCF.

[Clientlibs for Communities Components](clientlibs.md) décrit comment ajouter des clientlibs à une page.

### Clientlibs Auteur {#author-clientlibs}

Les clientlibs de version d’auteur sont réduits au minimum JavaScript nécessaire pour implémenter le composant.

Ces clientlibs ne doivent jamais être inclus directement, mais sont disponibles pour être incorporés à d&#39;autres clientlibs, qui sont fabriqués à la main pour un site.

Ces versions se trouvent dans le dossier libs SCF :

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Par exemple :

* Noeud de dossier client : `/libs/social/forum/hbs/forum/clientlibs`
* Catégories, propriété : `cq.social.author.hbs.forum`

Remarque : bien que les clientlibs d&#39;auteur n&#39;intègrent jamais d&#39;autres bibliothèques, ils font liste à leurs dépendances. Lorsqu’elles sont incorporées dans d’autres bibliothèques, les dépendances ne sont pas automatiquement extraites et doivent également être incorporées.

Les clientlibs d’auteur requis peuvent être identifiés en insérant &quot;author&quot; dans les clientlibs répertoriées pour chaque composant SCF dans le guide [Composants de la](components-guide.md)communauté.

### Considérations sur l’utilisation {#usage-considerations}

Chaque site est différent dans la manière dont il gère les bibliothèques client. Divers facteurs sont à prendre en compte :

* Vitesse globale : Peut-être le désir est-il que le site soit réactif, mais il est acceptable que la première page soit un peu lente à se charger. Si la plupart des pages utilisent le même code JavaScript, les différents scripts JavaScript peuvent être incorporés dans une bibliothèque cliente et référencés à partir de la première page à charger. Le script JavaScript de ce téléchargement unique reste en mémoire cache, ce qui réduit la quantité de données à télécharger pour les pages suivantes.
* Temps court jusqu&#39;à la première page : Peut-être que le désir est que la première page se charge rapidement. Dans ce cas, le code JavaScript se trouve dans plusieurs petits fichiers à référencer uniquement là où cela est nécessaire.
* Un équilibre entre le chargement de la première page et les téléchargements ultérieurs.

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

