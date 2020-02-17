---
title: Personnalisation côté client
seo-title: Personnalisation côté client
description: Personnalisation du comportement ou de l’aspect côté client dans les communautés AEM
seo-description: Personnalisation du comportement ou de l’aspect côté client dans les communautés AEM
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personnalisation côté client {#client-side-customization}

| **[⇐ Fonctionnalités essentielles](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

Pour personnaliser l’aspect et/ou le comportement d’un composant Communautés AEM côté client, plusieurs approches sont possibles.

Deux approches principales consistent à superposer ou à étendre un composant.

[Le fait de superposer](#overlays) un composant modifie le composant par défaut et affecte chaque référence au composant.

[L’extension](#extensions) d’un composant, dont le nom est unique, limite la portée des modifications. Le terme &quot;extension&quot; est utilisé de manière interchangeable avec &quot;override&quot;.

## Recouvrements {#overlays}

Le chevauchement d’un composant permet d’apporter des modifications à un composant par défaut et d’affecter toutes les instances qui utilisent le composant par défaut.

L’incrustation s’effectue en modifiant une copie du composant par défaut dans le répertoire /**apps** , plutôt que de modifier le composant d’origine dans le répertoire /**libs** . Le composant est construit avec un chemin relatif identique, sauf que &#39;libs&#39; est remplacé par &#39;apps&#39;.

Le répertoire /apps est le premier répertoire recherché pour résoudre les requêtes. S’il n’est pas trouvé, la version par défaut du répertoire /libs est utilisée.

Le composant par défaut du répertoire /libs ne doit jamais être modifié car les correctifs et mises à niveau ultérieurs sont libres de modifier le répertoire /libs de la manière nécessaire tout en conservant les interfaces publiques.

Cela diffère de l&#39; [extension](#extensions) d&#39;un composant par défaut, où le désir est d&#39;apporter des modifications pour une utilisation spécifique, de créer un chemin d&#39;accès unique au composant et de faire référence au composant par défaut d&#39;origine dans le répertoire /libs comme type de super ressource.

Pour un exemple rapide de superposition du composant de commentaires, essayez le didacticiel [Recouvrement du composant de commentaires](overlay-comments.md).

## Extensions {#extensions}

L’extension (remplacement) d’un composant est une méthode permettant d’effectuer des modifications pour une utilisation spécifique sans affecter toutes les instances qui utilisent la valeur par défaut. Le composant étendu porte un nom unique dans le dossier /apps et fait référence au composant par défaut dans le dossier /libs. La conception et le comportement par défaut d’un composant ne sont donc pas modifiés.

Cela diffère du fait de [superposer](#overlays) le composant par défaut dans lequel la nature de Sling résout les références relatives au dossier apps/ avant de rechercher dans le dossier libs/, de sorte que la conception ou le comportement d’un composant est modifié globalement.

Pour un exemple rapide d’extension du composant de commentaires, essayez le didacticiel [Étendre le composant de commentaires](extend-comments.md).

## Liaison Javascript {#javascript-binding}

Le script HBS pour le composant doit être lié aux objets, modèles et vues JavaScript qui implémentent cette fonctionnalité.

La valeur de l’ `data-scf-component` attribut peut être la valeur par défaut, par exemple **`social/tally/components/hbs/rating`**, ou un composant étendu (personnalisé) pour une fonctionnalité personnalisée, telle que **weretail/components/hbs/rating**.

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

Toutes les propriétés définies sur un composant/une ressource sont accessibles en référençant les clés de propriété dans le modèle de barres de commandes :

`{{properties.<property_name>}}`

## Skinning CSS {#skinning-css}

Personnaliser les composants pour correspondre au thème global du site Web peut être réalisé en &quot;habillage&quot; - en modifiant les couleurs, les polices, les images, les boutons, les liens, l&#39;espacement et même le positionnement dans une certaine mesure.

L’habillage peut être réalisé en remplaçant sélectivement les styles de cadre ou en écrivant des feuilles de style entièrement nouvelles. Les composants SCF définissent des classes CSS d’espacement de noms, modulaires et sémantiques qui affectent les différents éléments qui composent un composant.

Pour habiller un composant :

1. Identifiez les éléments que vous souhaitez modifier (par exemple, zone de compositeur, boutons de barre d’outils, police du message, etc.).
1. Identifiez la classe/les règles CSS qui affectent ces éléments.
1. Créez un fichier de feuille de style (.css).
1. Incluez la feuille de style dans un dossier de bibliothèque client ([clientlibs](#clientlibs-for-scf)) pour votre site et assurez-vous qu’elle est incluse dans vos modèles et pages avec [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redéfinissez les classes CSS et les règles que vous avez identifiées (#2) dans votre feuille de style et ajoutez des styles.

Les styles personnalisés remplacent désormais les styles de cadre par défaut et le composant est rendu avec le nouvel habillage.

>[!CAUTION]
>
>Tout nom de classe CSS précédé du préfixe ** scf-js-&amp;ast;**a une utilisation spécifique dans le code JavaScript. Ces classes affectent l’état d’un composant (par exemple, bascule de masqué à visible) et ne doivent ni être remplacées ni supprimées.
>
>Pendant que scf-js-&amp;ast; n’affectent pas les styles, les noms de classe peuvent être utilisés dans les feuilles de style avec la mise en garde que, lorsqu’ils contrôlent l’état des éléments, il peut y avoir des effets secondaires.

## Extension de JavaScript {#extending-javascript}

Pour étendre une implémentation JavaScript de composants, vous devez uniquement

1. Créez un composant pour votre application avec un jcr:resourceSuperType défini sur la valeur de jcr:resourceType du composant étendu, par exemple social/forum/components/hbs/forum
1. Examinez le script JavaScript du composant SCF par défaut pour déterminer les méthodes à enregistrer à l’aide de SCF.registerComponent().
1. Copiez le script JavaScript du composant étendu ou démarrez à partir de zéro
1. Etendre la méthode
1. Utilisez SCF.registerComponent() pour enregistrer toutes les méthodes avec les valeurs par défaut ou les objets et vues personnalisés.

### forum.js : Exemple d’extension du forum - HBS {#forum-js-sample-extension-of-forum-hbs}

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

Les balises de script font partie intégrante de la structure côté client. Il s’agit de la colle qui permet de lier le balisage généré côté serveur aux modèles et aux vues côté client.

Les balises de script dans les scripts SCF ne doivent pas être supprimées lors du recouvrement ou du remplacement de composants. Les balises de script SCF créées automatiquement pour l’injection de JSON dans le code HTML sont identifiées par l’attribut `data-scf-json=`true.

## Clientlibs pour SCF {#clientlibs-for-scf}

L’utilisation de bibliothèques [côté](../../help/sites-developing/clientlibs.md) client (clientlibs) permet d’organiser et d’optimiser le code JavaScript et le code CSS utilisés pour générer le contenu sur le client.

Les clientlibs pour SCF suivent un modèle de dénomination très spécifique pour deux variantes, qui varie uniquement en fonction de la présence de &quot;author&quot; dans le nom de la catégorie :

| Variante Clientlib | Modèle pour la propriété Catégories |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;nom du composant> |
| auteur clientlib | cq.social.author.hbs.&lt;nom du composant> |

### Compléter les bibliothèques clientes {#complete-clientlibs}

Les clients complets (non-auteurs) incluent des dépendances et sont pratiques pour inclure avec ui:includeClientLib.

Ces versions se trouvent dans :

* /etc/clientlibs/social/hbs/&lt;nom du composant>

Par exemple :

* Noeud du dossier client : /etc/clientlibs/social/hbs/forum
* Catégories, propriété : cq.social.hbs.forum

Le guide [Composants](components-guide.md) de la communauté répertorie les clientlibs complets requis pour chaque composant SCF.

[Clientlibs for Communities Components](clientlibs.md) décrit comment ajouter des clientlibs à une page.

### Clientlibs Auteur {#author-clientlibs}

Les clientlibs de version d’auteur sont réduits au minimum JavaScript nécessaire pour implémenter le composant.

Ces clientlibs ne doivent jamais être inclus directement, mais ils peuvent être incorporés à d’autres clientlibs, qui sont fabriqués à la main pour un site.

Ces versions se trouvent dans le dossier libs SCF :

* /libs/social/&lt;fonction>/components/hbs/&lt;nom du composant>/clientlibs

Par exemple :

* Noeud du dossier client : /libs/social/forum/hbs/forum/clientlibs
* Catégories, propriété : cq.social.author.hbs.forum

Remarque : bien que les clients d’auteur n’intègrent jamais d’autres bibliothèques, ils répertorient leurs dépendances. Lorsqu’elles sont intégrées dans d’autres bibliothèques, les dépendances ne sont pas automatiquement extraites et doivent également être incorporées.

Les clients auteurs requis peuvent être identifiés en insérant &quot;auteur&quot; dans les clientlibs répertoriés pour chaque composant SCF du guide [Composants de la](components-guide.md)communauté.

### Considérations sur l’utilisation {#usage-considerations}

Chaque site est différent dans la manière dont il gère les bibliothèques client. Divers facteurs sont les suivants :

* Vitesse globale : Peut-être le désir est-il que le site soit réactif, mais il est acceptable que la première page soit un peu lente à charger. Si la plupart des pages utilisent le même code JavaScript, les différents scripts JavaScript peuvent être incorporés dans une bibliothèque cliente et référencés à partir de la première page à charger. Le code JavaScript de ce téléchargement unique reste mis en cache, ce qui réduit la quantité de données à télécharger pour les pages suivantes.
* Temps court jusqu’à la première page : Peut-être que le désir est que la première page se charge rapidement. Dans ce cas, le code JavaScript se trouve dans plusieurs petits fichiers à référencer uniquement lorsque cela est nécessaire.
* Un équilibre entre le chargement de la première page et les téléchargements suivants.

| **[⇐ Fonctionnalités essentielles](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

