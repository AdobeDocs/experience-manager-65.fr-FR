---
title: Cadre des composants sociaux
seo-title: Cadre des composants sociaux
description: Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés
seo-description: Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Cadre des composants sociaux {#social-component-framework}

Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés côté serveur et côté client.

Les avantages du cadre :

* **Fonctionnel**: Facilité d&#39;intégration immédiate avec peu ou pas de personnalisation pour 80 % des cas d&#39;utilisation.
* **Skinnable**: Utilisation cohérente des attributs HTML pour le style CSS.
* **Extensible**: L&#39;implémentation des composants est orientée objet et s&#39;appuie sur la logique métier - il est facile d&#39;ajouter une connexion d&#39;entreprise incrémentielle sur le serveur.
* **Souple**: Modèles JavaScript simples sans logique, facilement superposés et personnalisés.
* **Accessible**: L’API HTTP prend en charge la publication depuis n’importe quel client, y compris les applications mobiles.
* **Portable**: Intégrez/incorporez dans n&#39;importe quelle page Web construite sur n&#39;importe quelle technologie.

Explorez une instance d’auteur ou de publication à l’aide du guide [interactif Composants](components-guide.md)de la communauté.

## Présentation {#overview}

Dans SCF, un composant est constitué d’un POJO SocialComponent, d’un modèle Handlebars JS (pour effectuer le rendu du composant) et d’une page CSS (pour mettre en forme le composant).

Un modèle JS Handlebars peut étendre les composants JS modèle/pour gérer l&#39;interaction de l&#39;utilisateur avec le composant sur le client.

Si un composant doit prendre en charge la modification des données, l’implémentation de l’API SocialComponent peut être écrite pour prendre en charge la modification/l’enregistrement de données similaires aux objets de modèle/de données dans les applications Web traditionnelles. En outre, les opérations (contrôleurs) et un service d’opération peuvent être ajoutés pour gérer les demandes d’opération, exécuter une logique métier et appeler les API sur les objets de modèle/de données.

L’API SocialComponent peut être étendue pour fournir les données requises par un client pour une couche de  ou un client HTTP.

### Mode de rendu des pages pour le client {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### Personnalisation et extension des composants {#component-customization-and-extension}

Pour personnaliser ou étendre les composants, vous devez écrire uniquement les incrustations et extensions dans votre répertoire /apps, ce qui simplifie le processus de mise à niveau vers les versions ultérieures.

* Pour l’habillage :
   * Seul le [fichier CSS doit être modifié](client-customize.md#skinning-css).
* Pour l’apparence :
   * Modifiez le modèle JS et le fichier CSS.
* Pour Look, Feel et UX :
   * Modifiez le modèle JS, CSS et [étendez/remplacez Javascript](client-customize.md#extending-javascript).
* Pour modifier les informations disponibles pour le modèle JS ou le point de fin GET :
   * Etendez le composant [SocialComponent](server-customize.md#socialcomponent-interface).
* Pour ajouter un traitement personnalisé pendant les opérations :
   * Ecrivez une [extension OperationExtension](server-customize.md#operationextension-class).
* Pour ajouter une nouvelle opération personnalisée :
   * Créez une opération [de publication](server-customize.md#postoperation-class)Sling.
   * Utilisez [OperationServices](server-customize.md#operationservice-class) existant selon vos besoins.
   * Ajouter du code JavaScript pour appeler votre opération du côté client, le cas échéant.

## Structure côté serveur {#server-side-framework}

La structure fournit des API pour accéder aux fonctionnalités du serveur et prendre en charge l’interaction entre le client et le serveur.

### API Java {#java-apis}

Les API Java fournissent des classes et des interfaces abstraites qui sont facilement héritées ou sous-classées.

Les classes principales sont décrites sur la page Personnalisation [côté](server-customize.md) serveur.

Visitez la page [Aperçu](srp.md) des fournisseurs de ressources  pour en savoir plus sur l’utilisation de l’UGC.

### API HTTP {#http-api}

L’API HTTP prend en charge la personnalisation et le choix des plates-formes clientes pour les applications PhoneGap, les applications natives et d’autres intégrations et applications de mashups. De plus, l’API HTTP permet à un site communautaire de s’exécuter en tant que service sans client, de sorte que les composants de la structure puissent être intégrés à n’importe quelle page Web construite sur n’importe quelle technologie.

### API HTTP - Demandes GET {#http-api-get-requests}

Pour chaque composant Social, la structure fournit un point de terminaison API HTTP. Pour accéder au point de fin, envoyez une requête GET à la ressource avec un sélecteur &#39;.social.json&#39; + extension. En utilisant Sling, la requête est transmise au `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Transmet la ressource (resourceType) à `SocialComponentFactoryManager` et reçoit un SocialComponentFactory capable de sélectionner un `SocialComponent` représentant la ressource.

1. Appelle l’usine et reçoit une `SocialComponent` capacité de gestion de la ressource et de la demande.
1. Appelle le `SocialComponent`, qui traite la requête et renvoie une représentation JSON des résultats.
1. Renvoie la réponse JSON au client.

**`GET Request`**

Une servlet GET par défaut écoute les requêtes .social.json auxquelles le composant SocialComponent répond par un fichier JSON personnalisable.

![chlimage_1-26](assets/chlimage_1-26.png)

### API HTTP - Demandes POST {#http-api-post-requests}

Outre les opérations GET (Lecture), la structure définit un modèle de point de fin pour activer d’autres opérations sur un composant, y compris la création, la mise à jour et la suppression. Ces points de fin sont des API HTTP qui acceptent les entrées et répondent avec un code d’état HTTP ou un objet de réponse JSON.

Ce modèle de point de fin de structure rend les opérations CUD extensibles, réutilisables et testables.

**`POST Request`**

Il existe une opération Sling POST:operation pour chaque opération SocialComponent. La logique métier et le code de maintenance de chaque opération sont encapsulés dans un OperationService accessible via l’API HTTP ou depuis un autre service OSGi. Les crochets prennent en charge les extensions d’opération enfichables pour les actions avant/après.

![chlimage_1-27](assets/chlimage_1-27.png)

###  fournisseur de ressources  (SRP) {#storage-resource-provider-srp}

Pour en savoir plus sur la gestion des fichiers UGC stockés dans le magasin [de contenu de la](working-with-srp.md)communauté, voir :

* [Aperçu](srp.md) du fournisseur de ressources  - Présentation et aperçu de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes de l’utilitaire SRP API.
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.

### Personnalisations côté serveur {#server-side-customizations}

Visitez Personnalisations [côté](server-customize.md) serveur pour en savoir plus sur la personnalisation de la logique métier et du comportement d’un composant Communities côté serveur.

## Langage de modèle JS Handlebars {#handlebars-js-templating-language}

L’un des changements les plus visibles dans la nouvelle structure est l’utilisation du langage de modèle [Handlebars JS (HBS)](https://www.handlebarsjs.com/), une technologie open source populaire pour le rendu client-serveur.

Les scripts HBS sont simples, sans logique, compilent sur le serveur et le client, sont faciles à recouvrir et à personnaliser, et sont naturellement liés au client UX parce que HBS prend en charge le rendu côté client.

La structure fournit plusieurs [barres d’outils](handlebars-helpers.md) utiles lors du développement de composants sociaux.

Sur le serveur, lorsque Sling résout une requête GET, il identifie le script qui sera utilisé pour répondre à la requête. Si le script est un modèle HBS (.hbs), Sling déléguera la requête au moteur de barres de main. Le moteur de barres de main récupérera ensuite le composant SocialComponent à partir de la fabrique de composants sociaux appropriée, créera un contexte et rendra le code HTML.

### Aucune restriction d’accès {#no-access-restriction}

Les fichiers de modèle HBS (Handlebars) (.hbs) sont similaires aux fichiers de modèle .jsp et .html, sauf qu’ils peuvent être utilisés pour le rendu dans le navigateur client et sur le serveur. Par conséquent, un navigateur client demandant un modèle côté client recevra un fichier .hbs du serveur.

Pour ce faire, tous les modèles HBS du chemin de recherche sling (tous les fichiers .hbs situés sous /libs/ ou /apps) doivent pouvoir être récupérés par tout utilisateur à partir de l’auteur ou de la publication.

L&#39;accès HTTP aux fichiers .hbs peut ne pas être interdit.

### Ajouter ou inclure un composant Collectivités {#add-or-include-a-communities-component}

La plupart des composants de communautés doivent être *ajoutés* en tant que ressource adressable Sling. Un certain nombre de composants Communautés peuvent être *inclus* dans un modèle en tant que ressource non existante afin de permettre l’inclusion et la personnalisation dynamiques de l’emplacement où écrire le contenu généré par l’utilisateur (CU).

Dans les deux cas, les bibliothèques [clientes](clientlibs.md) requises du composant doivent également être présentes.

**Ajouter un composant**

L’ajout d’un composant fait référence au processus d’ajout d’une instance d’une ressource (composant), par exemple lorsque vous faites glisser le curseur depuis le navigateur du composant (Sidekick) vers une page en mode d’édition Auteur.

Le résultat est un noeud enfant JCR sous un noeud par, qui est adressable à Sling.

**Inclure un composant**

L’inclusion d’un composant fait référence au processus d’ajout d’une référence à une ressource [](srp.md#for-non-existing-resources-ners) &quot;non existante&quot; (aucun noeud JCR) dans le modèle, comme l’utilisation d’un langage de script.

A compter de la version 6.1 d’AEM, lorsqu’un composant est inclus dynamiquement au lieu d’être ajouté, il est possible de modifier les propriétés du composant en mode *conception *création.

Seuls quelques composants des communautés AEM sélectionnés peuvent être inclus dynamiquement. Ils sont :

* [Commentaires](essentials-comments.md)
* [Évaluation](rating-basics.md)
* [Révisions](reviews-basics.md)
* [Vote](essentials-voting.md)

Le Guide [des composants](components-guide.md) communautaires permet d&#39;éviter que des composants inclusifs ne soient ajoutés à l&#39;inclusion.

**Lors de l’utilisation du langage de modèle des barres de main** , la ressource non existante est incluse à l’aide de l’ [assistant](handlebars-helpers.md#include) d’inclusion en spécifiant son type de ressource :

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Lors de l’utilisation de JSP**, une ressource est incluse à l’aide de la balise [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Pour ajouter dynamiquement un composant à une page, au lieu de l’ajouter ou de l’inclure dans un modèle, voir Téléchargement [de](sideloading.md)composant.


### Handlebars Helpers {#handlebars-helpers}

Voir Aide-mémoire [SCF](handlebars-helpers.md) pour obtenir une  et une description des aides personnalisées disponibles dans SCF.

## Cadre côté client {#client-side-framework}

### Modèle- Javascript Framework {#model-view-javascript-framework}

La structure comprend une extension de [Backbone.js](https://www.backbonejs.org/), une structure JavaScript modèle-, pour faciliter le développement de composants interactifs riches. La nature orientée objet prend en charge un cadre extensible/réutilisable. La communication entre le client et le serveur est simplifiée au moyen de l’API HTTP.

La structure utilise les modèles de barres de contrôle côté serveur pour effectuer le rendu des composants pour le client. Les modèles sont basés sur les réponses JSON générées par l’API HTTP. Le se lie au code HTML généré par les modèles de barres de main et offre une interactivité.

### Conventions CSS {#css-conventions}

Les conventions suivantes sont recommandées pour la définition et l’utilisation des classes CSS :

* Utilisez des noms de sélecteur de classe CSS avec espacement de nom clair et évitez les noms génériques tels que &#39;titre&#39;, &#39;image&#39;, etc.
* Définissez des styles de sélecteur de classe spécifiques afin que les feuilles de style CSS fonctionnent correctement avec d’autres éléments et styles de la page. Par exemple : `.social-forum .topic-list .li { color: blue; }`
* Conservez les classes CSS pour la mise en forme séparée des classes CSS pour UX pilotées par JavaScript.

### Personnalisations côté client {#client-side-customizations}

Pour personnaliser l’apparence et le comportement d’un composant Communities côté client, consultez Personnalisations [côté](client-customize.md)client, qui comprend des informations sur :

* [Recouvrements](client-customize.md#overlays)
* [Extensions](client-customize.md#extensions)
* [Marquage HTML](client-customize.md#htmlmarkup)
* [Esquisse de CSS](client-customize.md#skinning-css)
* [Extension de JavaScript](client-customize.md#extending-javascript)
* [Clientlibs pour SCF](client-customize.md#clientlibs-for-scf)

## Fonctionnalités et composants essentiels {#feature-and-component-essentials}

Les informations essentielles pour les développeurs sont décrites dans la section [Fonctionnalités et composants essentiels](essentials.md) .

Vous trouverez des informations supplémentaires sur les développeurs dans la section [Instructions](code-guide.md) de codage.

## Résolution des incidents {#troubleshooting}

Les problèmes courants et les problèmes connus sont décrits dans la section [Résolution des problèmes](troubleshooting.md) .

