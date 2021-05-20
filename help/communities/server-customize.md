---
title: Personnalisation côté serveur
seo-title: Personnalisation côté serveur
description: Personnalisation côté serveur dans AEM Communities
seo-description: Personnalisation côté serveur dans AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Personnalisation côté serveur {#server-side-customization}

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[⇒ de personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |

## API Java {#java-apis}

>[!NOTE]
>
>L’emplacement du package des API Communities peut être modifié lors de la mise à niveau d’une version majeure vers une version suivante.

### Interface du composant Social {#socialcomponent-interface}

Les composants sociaux sont des POJO qui représentent une ressource pour une fonction AEM Communities. Idéalement, chaque composant Social représente un type de ressource spécifique avec des GETters exposés qui fournissent des données au client afin que la ressource soit correctement représentée. Toute la logique commerciale et la logique d’affichage sont encapsulées dans le composant Social, y compris les informations de session du visiteur du site, si nécessaire.

L’interface définit un ensemble de base de GETters nécessaires pour représenter une ressource. L’important est que l’interface indique les méthodes Map&lt;String, Object> getAsMap() et String toJSONString() nécessaires pour effectuer le rendu des modèles Handlebars et exposer les points de terminaison JSON GET pour les ressources.

Toutes les classes SocialComponent doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponent`

### Interface du composant SocialCollection {#socialcollectioncomponent-interface}

L’interface SocialCollectionComponent étend l’interface SocialComponent pour mieux représenter les ressources qui sont des collections d’autres ressources.

Toutes les classes SocialCollectionComponent doivent implémenter l’interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface SocialComponentFactory {#socialcomponentfactory-interface}

Une SocialComponentFactory (factory) enregistre un composant Social avec la structure. La fabrique permet à la structure de savoir quels composants sociaux sont disponibles pour un type de ressource donné et leur rang de priorité lorsque plusieurs composants sociaux sont identifiés.

SocialComponentFactory est responsable de la création d’une instance du composant Social sélectionné, ce qui permet d’injecter toutes les dépendances dont le composant Social a besoin à partir de la fabrique à l’aide des pratiques d’ID.

Un SocialComponentFactory est un service OSGi qui a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Toutes les classes SocialComponentFactory doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponentFactory`

Une implémentation de la méthode SocialComponentFactory.getPriority() doit renvoyer la valeur la plus élevée afin que la fabrique soit utilisée pour le resourceType donné comme renvoyé par getResourceType().

### Interface de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (responsable) gère tous les composants sociaux enregistrés dans la structure et est responsable de la sélection de SocialComponentFactory à utiliser pour une ressource donnée (resourceType). Si aucune usine n’est enregistrée pour un type de ressource spécifique, le responsable renvoie une usine avec le super type le plus proche pour la ressource donnée.

Un SocialComponentFactoryManager est un service OSGi qui a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Pour obtenir une gestion du service OSGi, appelez `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Demandes de POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Les points d’entrée du POST d’API HTTP sont des classes PostOperation définies par l’implémentation de l’interface `SlingPostOperation` (package `org.apache.sling.servlets.post`).

L’implémentation `PostOperation` du point de terminaison définit `sling.post.operation` sur une valeur à laquelle l’opération répondra. Toutes les demandes de POST avec un paramètre:operation défini sur cette valeur seront déléguées à cette classe d’implémentation.

`PostOperation` appelle la `SocialOperation` qui effectue les actions nécessaires à l’opération.

`PostOperation` reçoit le résultat de `SocialOperation` et renvoie la réponse appropriée au client.

#### Classe SocialOperation {#socialoperation-class}

Chaque point de terminaison `SocialOperation` étend la classe AbstractSocialOperation et remplace la méthode `performOperation()`. Cette méthode effectue toutes les actions nécessaires pour terminer l’opération et renvoyer une balise `SocialOperationResult` ou lancer une balise `OperationException`, auquel cas un état d’erreur HTTP avec un message, le cas échéant, est renvoyé à la place de la réponse JSON normale ou du code d’état HTTP de succès.

L’extension de `AbstractSocialOperation` permet de réutiliser `SocialComponents` pour envoyer des réponses JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La classe `SocialOperationResult` est renvoyée en résultat de `SocialOperation` et est composée d’un `SocialComponent`, d’un code d’état HTTP et d’un message d’état HTTP.

`SocialComponent` représente la ressource qui a été affectée par l’opération.

Pour une opération de création, la valeur `SocialComponent` incluse dans la valeur `SocialOperationResult` représente la ressource qui vient d’être créée et, pour une opération de mise à jour, elle représente la ressource qui a été modifiée par l’opération. Aucun `SocialComponent` n’est renvoyé pour une opération de suppression.

Les codes d’état HTTP de succès utilisés sont les suivants :

* 201 pour les opérations de création
* 200 pour les opérations de mise à jour
* 204 pour les opérations de suppression

#### Classe OperationException {#operationexception-class}

Un `OperationExcepton` peut être généré lors de l’exécution d’une opération si la requête n’est pas valide ou si une autre erreur se produit, comme des erreurs internes, des valeurs de paramètre incorrectes, des autorisations incorrectes, etc. Un `OperationException` est composé d’un code d’état HTTP et d’un message d’erreur, qui sont renvoyés au client comme réponse à `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

La structure de composants sociaux recommande que la logique commerciale responsable de l’opération ne soit pas implémentée dans la classe `SocialOperation`, mais plutôt déléguée à un service OSGi. L’utilisation d’un service OSGi pour une logique métier permet à un `SocialComponent`, agissant selon un point de terminaison `SocialOperation`, d’être intégré à d’autres codes et d’avoir une logique métier différente appliquée.

Toutes les classes `OperationService` étendent `AbstractOperationService`, permettant des extensions supplémentaires pouvant se connecter à l’opération en cours. Chaque opération du service est représentée par une classe `SocialOperation`. La classe `OperationExtensions` peut être appelée pendant l’exécution de l’opération en appelant les méthodes

* `performBeforeActions()`

   Permet les prévérifications/prétraitements et validations
* `performAfterActions()`

   Permet de modifier davantage les ressources ou d’appeler des événements personnalisés, des workflows, etc.

#### Classe OperationExtension {#operationextension-class}

`OperationExtension` Les classes sont des éléments de code personnalisés qui peuvent être injectés dans une opération permettant de personnaliser les opérations pour répondre aux besoins de l’entreprise. Les utilisateurs du composant peuvent ajouter des fonctionnalités de manière dynamique et incrémentielle au composant. Le modèle d’extension/crochet permet aux développeurs de se concentrer exclusivement sur les extensions elles-mêmes et élimine la nécessité de copier et de remplacer des opérations et des composants entiers.

## Exemple de code {#sample-code}

Un exemple de code est disponible dans le référentiel [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) . Recherchez des projets dont le préfixe est `aem-communities` ou `aem-scf`.

## Bonnes pratiques {#best-practices}

Consultez la section [Consignes de codage](code-guide.md) pour connaître les instructions de codage et les bonnes pratiques à l’intention des développeurs AEM Communities.

Voir aussi [Fournisseur de ressources de stockage (SRP) pour UGC](srp.md) pour en savoir plus sur l’accès au contenu généré par l’utilisateur.

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[⇒ de personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |
