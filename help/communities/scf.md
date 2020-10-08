---
title: Cadre des composantes sociales
seo-title: Cadre des composantes sociales
description: Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés
seo-description: Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---


# Cadre des composantes sociales {#social-component-framework}

Le cadre des composants sociaux (SCF) simplifie le processus de configuration, de personnalisation et d’extension des composants de communautés côté serveur et côté client.

Les avantages du cadre :

* **Fonctionnel**: Facilité d&#39;intégration immédiate avec peu ou pas de personnalisation pour 80 % des cas d&#39;utilisation.
* **Skinnable**: Utilisation cohérente des attributs HTML pour la mise en forme CSS.
* **Extensible**: La mise en oeuvre des composants est orientée objet et s&#39;appuie sur la logique métier - il est facile d&#39;ajouter une connexion d&#39;entreprise incrémentielle sur le serveur.
* **Flexible**: Modèles JavaScript simples sans logique, facilement superposés et personnalisés.
* **Accessible**: L’API HTTP prend en charge la publication depuis n’importe quel client, y compris les applications mobiles.
* **Portable**: Intégrez/incorporez dans toute page Web construite sur n&#39;importe quelle technologie.

Explorez une instance d’auteur ou de publication à l’aide du guide [interactif](components-guide.md)Community Components.

## Présentation {#overview}

Dans SCF, un composant est constitué d’un POJO SocialComponent, d’un modèle JS Handlebars (pour effectuer le rendu du composant) et de CSS (pour appliquer un style au composant).

Un modèle JS Handlebars peut étendre les composants JS de modèle/vue pour gérer l&#39;interaction de l&#39;utilisateur avec le composant sur le client.

Si un composant doit prendre en charge la modification des données, l’implémentation de l’API SocialComponent peut être écrite pour prendre en charge la modification/l’enregistrement de données similaires aux objets de modèle/de données dans les applications Web traditionnelles. En outre, des opérations (contrôleurs) et un service d&#39;opérations peuvent être ajoutés pour gérer les demandes d&#39;opération, exécuter une logique métier et appeler les API sur les objets de modèle/données.

L’API SocialComponent peut être étendue pour fournir les données requises par un client pour une couche de vue ou un client HTTP.

### Mode de rendu des pages pour le client {#how-pages-are-rendered-for-client}

![rendu de page scf](assets/scf-overview.png)

### Personnalisation et extension des composants {#component-customization-and-extension}

Pour personnaliser ou étendre les composants, vous écrivez uniquement les incrustations et extensions dans votre répertoire /apps, ce qui simplifie le processus de mise à niveau vers les versions ultérieures.

* Pour l&#39;habillage :
   * Seule la [page CSS doit être modifiée](client-customize.md#skinning-css).
* Pour la recherche et le ressenti :
   * Modifiez le modèle JS et le fichier CSS.
* Pour Look, Feel et UX :
   * Modifiez le modèle JS, CSS et [étendez/remplacez Javascript](client-customize.md#extending-javascript).
* Pour modifier les informations disponibles pour le modèle JS ou pour le point de terminaison GET :
   * Étendez le [composant](server-customize.md#socialcomponent-interface)Social.
* Pour ajouter un traitement personnalisé pendant les opérations :
   * Écrivez une [opérationExtension](server-customize.md#operationextension-class).
* Pour ajouter une nouvelle opération personnalisée :
   * Créez une opération [de publication](server-customize.md#postoperation-class)Sling.
   * Utilisez [OperationServices](server-customize.md#operationservice-class) existant si nécessaire.
   * Ajoutez le code JavaScript pour appeler votre opération du côté client si nécessaire.

## Structure côté serveur {#server-side-framework}

La structure fournit des API pour accéder aux fonctionnalités du serveur et prendre en charge les interactions entre le client et le serveur.

### API Java {#java-apis}

Les API Java offrent des classes et des interfaces abstraites qui sont facilement héritées ou sous-classées.

Les classes principales sont décrites sur la page Personnalisation [côté](server-customize.md) serveur.

Visitez la section Présentation [des fournisseurs de ressources](srp.md) d&#39;Enregistrement pour en savoir plus sur l&#39;utilisation de l&#39;UGC.

### API HTTP {#http-api}

L’API HTTP facilite la personnalisation et le choix des plates-formes clientes pour les applications PhoneGap, les applications natives, ainsi que d’autres intégrations et applications hybrides. De plus, l&#39;API HTTP permet à un site communautaire de s&#39;exécuter en tant que service sans client, de sorte que les composants de la structure puissent être intégrés à n&#39;importe quelle page Web construite sur n&#39;importe quelle technologie.

### API HTTP - Demandes de GET {#http-api-get-requests}

Pour chaque composant Social, la structure fournit un point de terminaison API HTTP. Le point de terminaison est accessible en envoyant une demande de GET à la ressource avec un sélecteur &#39;.social.json&#39; + extension. En utilisant Sling, la demande est transmise au `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Transmet la ressource (resourceType) à la `SocialComponentFactoryManager` et reçoit un SocialComponentFactory capable de sélectionner un `SocialComponent` représentant la ressource.

1. Appelle l’usine et reçoit une `SocialComponent` capacité de traitement de la ressource et de la demande.
1. Appelle le `SocialComponent`, qui traite la requête et renvoie une représentation JSON des résultats.
1. Renvoie la réponse JSON au client.

**`GET Request`**

Une servlet de GET par défaut écoute les requêtes .social.json auxquelles le SocialComponent répond avec un JSON personnalisable.

![scf-framework](assets/scf-framework.png)

### API HTTP - Demandes de POST {#http-api-post-requests}

Outre les opérations de GET (lecture), la structure définit un modèle de point de terminaison pour activer d’autres opérations sur un composant, notamment Créer, Mettre à jour et Supprimer. Ces points de terminaison sont des API HTTP qui acceptent les entrées et répondent avec un code d’état HTTP ou un objet de réponse JSON.

Ce modèle de point de terminaison de la structure rend les opérations CUD extensibles, réutilisables et testables.

**`POST Request`**

Il existe une opération POST:Sling pour chaque opération SocialComponent. La logique métier et le code de maintenance de chaque opération sont encapsulés dans un OperationService accessible via l&#39;API HTTP ou depuis un autre service OSGi. Des crochets sont fournis pour la prise en charge des extensions d&#39;opération enfichables pour les actions avant/après.

![scf-post-request](assets/scf-post-request.png)

### Fournisseur de ressources d&#39;Enregistrement (SRP) {#storage-resource-provider-srp}

Pour en savoir plus sur la gestion des fichiers UGC stockés dans le magasin [de contenu de la](working-with-srp.md)communauté, voir :

* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire d&#39;API SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - Règles de codage.

### Personnalisations côté serveur {#server-side-customizations}

Visitez Personnalisations [côté](server-customize.md) serveur pour en savoir plus sur la personnalisation de la logique métier et du comportement d’un composant Communities côté serveur.

## Handlebars JS Template Language {#handlebars-js-templating-language}

L&#39;un des changements les plus notables dans la nouvelle structure est l&#39;utilisation du langage de modèle HBS ( [Handlebars JS template Language)](https://www.handlebarsjs.com/), une technologie open source populaire pour le rendu serveur-client.

Les scripts HBS sont simples, sans logique, compilent sur le serveur et le client, sont faciles à recouvrir et à personnaliser, et sont naturellement liés au client UX parce que HBS prend en charge le rendu côté client.

La structure fournit plusieurs barres de [poignées](handlebars-helpers.md) utiles lors du développement de composants sociaux.

Sur le serveur, lorsque Sling résout une demande de GET, il identifie le script qui sera utilisé pour répondre à la demande. Si le script est un modèle HBS (.hbs), Sling déléguera la requête au moteur Handlebars. Le moteur Handlebars récupère ensuite le composant SocialComponent de la SocialComponentFactory appropriée, crée un contexte et effectue le rendu du code HTML.

### Aucune restriction d&#39;accès {#no-access-restriction}

Les fichiers de modèle HBS (Handlebars) (.hbs) sont analogues aux fichiers de modèle .jsp et .html, sauf qu’ils peuvent être utilisés pour le rendu à la fois dans le navigateur client et sur le serveur. Par conséquent, un navigateur client demandant un modèle côté client recevra un fichier .hbs du serveur.

Pour ce faire, tous les modèles HBS du chemin de recherche sling (tous les fichiers .hbs situés sous /libs/ ou /apps) peuvent être extraits par tout utilisateur de l&#39;auteur ou de la publication.

L&#39;accès HTTP aux fichiers .hbs n&#39;est pas interdit.

### Ajouter ou inclure un composant Collectivités {#add-or-include-a-communities-component}

La plupart des composants de communautés doivent être *ajoutés* en tant que ressource adressable Sling. Un certain nombre de composants Communautés peuvent être *inclus* dans un modèle en tant que ressource non existante afin de permettre l’inclusion et la personnalisation dynamiques de l’emplacement où écrire le contenu généré par l’utilisateur (CU).

Dans les deux cas, les bibliothèques [clientes](clientlibs.md) requises du composant doivent également être présentes.

**Ajouter un composant**

L’Ajoute d’un composant fait référence au processus d’ajout d’une instance d’une ressource (composant), par exemple lorsqu’elle est glissée du navigateur de composants (sidekick) sur une page en mode d’édition de l’auteur.

Le résultat est un noeud enfant JCR sous un noeud par, qui est adressable à Sling.

**Inclure un composant**

L’inclusion d’un composant fait référence au processus d’ajout d’une référence à une ressource [](srp.md#for-non-existing-resources-ners) &quot;non existante&quot; (aucun noeud JCR) dans le modèle, par exemple en utilisant un langage de script.

A partir de AEM 6.1, lorsqu’un composant est inclus dynamiquement au lieu d’être ajouté, il est possible de modifier ses propriétés en mode création *design *.

Seuls quelques-uns des composants AEM Communities sélectionnés peuvent être inclus dynamiquement. Ils sont :

* [Commentaires](essentials-comments.md)
* [Évaluation](rating-basics.md)
* [Révisions](reviews-basics.md)
* [Vote](essentials-voting.md)

Le Guide [des composants](components-guide.md) de la communauté permet d&#39;éviter l&#39;ajout de composants inclusifs à des composants inclusifs.

**Lors de l&#39;utilisation du langage de modèle Handlebars** , la ressource non existante est incluse à l&#39;aide de l&#39; [Assistant](handlebars-helpers.md#include) d&#39;inclusion en spécifiant son type de ressource :

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**Lors de l’utilisation de JSP**, une ressource est incluse à l’aide de la balise [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Pour ajouter un composant à une page de manière dynamique, au lieu de l’ajouter ou de l’inclure dans un modèle, voir Téléchargement [de](sideloading.md)composant.

### Handlebars Helpers {#handlebars-helpers}

Pour obtenir une liste et une description des aides personnalisées disponibles dans SCF, reportez-vous à la section [Aide-mémoire](handlebars-helpers.md) SCF.

## Cadre côté client {#client-side-framework}

### Structure JavaScript Vue modèle {#model-view-javascript-framework}

La structure comprend une extension de [Backbone.js](https://www.backbonejs.org/), une structure JavaScript vue modèle, pour faciliter le développement de composants interactifs riches. La nature orientée objet prend en charge un cadre extensible/réutilisable. La communication entre le client et le serveur est simplifiée au moyen de l&#39;API HTTP.

La structure utilise les modèles de barres de contrôle côté serveur pour générer les composants pour le client. Les modèles sont basés sur les réponses JSON générées par l’API HTTP. Les vues se lient au code HTML généré par les modèles Handlebars et offrent une interactivité.

### Conventions CSS {#css-conventions}

Les conventions suivantes sont recommandées pour la définition et l’utilisation des classes CSS :

* Utilisez des noms de sélecteur de classe CSS clairement espacés dans les noms et évitez les noms génériques tels que &#39;titre&#39;, &#39;image&#39;, etc.
* Définissez des styles de sélecteur de classe spécifiques afin que les feuilles de style CSS fonctionnent correctement avec d’autres éléments et styles de la page. Par exemple : `.social-forum .topic-list .li { color: blue; }`
* Conservez les classes CSS pour la mise en forme séparées des classes CSS pour UX pilotées par JavaScript.

### Personnalisations côté client {#client-side-customizations}

Pour personnaliser l’apparence et le comportement d’un composant Communities côté client, reportez-vous à la section Personnalisations [côté](client-customize.md)client, qui comprend des informations sur :

* [Recouvrements](client-customize.md#overlays)
* [Extensions](client-customize.md#extensions)
* [Marquage HTML](client-customize.md#htmlmarkup)
* [Esquisse de CSS](client-customize.md#skinning-css)
* [Extension de JavaScript](client-customize.md#extending-javascript)
* [Clientlibs pour SCF](client-customize.md#clientlibs-for-scf)

## Fonctionnalités et composants essentiels {#feature-and-component-essentials}

Les informations essentielles pour les développeurs sont décrites dans la section [Fonctionnalités et composants essentiels](essentials.md) .

D&#39;autres informations sur les développeurs se trouvent dans la section [Coding Guidelines](code-guide.md) .

## Résolution des incidents {#troubleshooting}

Les problèmes courants et les problèmes connus sont décrits dans la section [Résolution des problèmes](troubleshooting.md) .

