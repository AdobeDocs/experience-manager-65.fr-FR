---
title: Personnalisation côté serveur
description: Découvrez comment la personnalisation côté serveur dans les communautés Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personnalisation côté serveur {#server-side-customization}

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[Personnalisation côté client ⇒](client-customize.md)** |
|---|---|
|   | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |

## API Java™ {#java-apis}

>[!NOTE]
>
>L’emplacement du package des API Communities peut être modifié lors de la mise à niveau d’une version majeure vers une version suivante.

### Interface du composant Social {#socialcomponent-interface}

Les composants sociaux sont des POJO qui représentent une ressource pour une fonction AEM Communities. Idéalement, chaque composant Social représente un type de ressource spécifique avec des GETters exposés qui fournissent des données au client afin que la ressource soit correctement représentée. L’ensemble de la logique d’entreprise et d’affichage est encapsulé dans le composant Social, y compris les informations de session du visiteur du site, si nécessaire.

L’interface définit un ensemble de base de GETters nécessaires pour représenter une ressource. Il est important de noter que l’interface indique les méthodes Map&lt;String, Object> getAsMap() et String toJSONString() nécessaires pour effectuer le rendu des modèles Handlebars et exposer les points de terminaison JSON GET pour les ressources.

Toutes les classes SocialComponent doivent mettre en oeuvre l’interface `com.adobe.cq.social.scf.SocialComponent`

### Interface du composant SocialCollection {#socialcollectioncomponent-interface}

L’interface SocialCollectionComponent étend l’interface SocialComponent pour mieux représenter les ressources qui sont des collections d’autres ressources.

Toutes les classes SocialCollectionComponent doivent implémenter l’interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface SocialComponentFactory {#socialcomponentfactory-interface}

Une SocialComponentFactory (factory) enregistre un composant Social avec la structure. La fabrique permet à la structure de savoir quels composants sociaux sont disponibles pour un type de ressource donné et leur rang de priorité lorsque plusieurs composants sociaux sont identifiés.

SocialComponentFactory est responsable de la création d’une instance du composant Social sélectionné, ce qui permet d’injecter toutes les dépendances dont le composant Social a besoin à partir de la fabrique à l’aide des pratiques d’ID.

Un SocialComponentFactory est un service OSGi qui a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Toutes les classes SocialComponentFactory doivent mettre en oeuvre l’interface `com.adobe.cq.social.scf.SocialComponentFactory`

Une implémentation de la méthode SocialComponentFactory.getPriority() doit renvoyer la valeur la plus élevée pour la fabrique à utiliser pour le resourceType donné, comme renvoyée par getResourceType().

### Interface de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (responsable) gère tous les composants sociaux enregistrés dans la structure et est responsable de la sélection de SocialComponentFactory à utiliser pour une ressource donnée (resourceType). Si aucune usine n’est enregistrée pour un type de ressource spécifique, le gestionnaire renvoie une usine avec le type de super le plus proche pour la ressource donnée.

Un SocialComponentFactoryManager est un service OSGi qui a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Un gestionnaire du service OSGi est obtenu en appelant `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Demandes de POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Les points d’entrée du POST d’API HTTP sont des classes PostOperation définies par l’implémentation de l’interface `SlingPostOperation` (package `org.apache.sling.servlets.post`).

L’implémentation du point de terminaison `PostOperation` définit `sling.post.operation` sur une valeur à laquelle l’opération répond. Toutes les demandes de POST avec un paramètre:operation défini sur cette valeur sont déléguées à cette classe d’implémentation.

Le `PostOperation` appelle le `SocialOperation` qui effectue les actions nécessaires à l’opération.

`PostOperation` reçoit le résultat de `SocialOperation` et renvoie la réponse appropriée au client.

#### Classe SocialOperation {#socialoperation-class}

Chaque point d’entrée `SocialOperation` étend la classe AbstractSocialOperation et remplace la méthode `performOperation()`. Cette méthode effectue toutes les actions nécessaires pour terminer l’opération et renvoyer un `SocialOperationResult` ou lancer un `OperationException`. Dans ce cas, un état d’erreur HTTP avec un message, s’il est disponible, est renvoyé à la place de la réponse JSON normale ou du code d’état HTTP de succès.

L&#39;extension de `AbstractSocialOperation` permet la réutilisation de `SocialComponents` pour envoyer des réponses JSON.

#### Classe SocialOperationResult {#socialoperationresult-class}

La classe `SocialOperationResult` est renvoyée suite au `SocialOperation` et est composée d’un `SocialComponent`, d’un code d’état HTTP et d’un message d’état HTTP.

`SocialComponent` représente la ressource qui a été affectée par l’opération.

Pour une opération de création, le `SocialComponent` inclus dans le `SocialOperationResult` représente la ressource créée et pour une opération de mise à jour, il représente la ressource qui a été modifiée par l’opération. Aucun `SocialComponent` n’est renvoyé pour une opération de suppression.

Les codes d’état HTTP de succès utilisés sont les suivants :

* 201 pour les opérations de création
* 200 pour les opérations de mise à jour
* 204 pour les opérations de suppression

#### Classe OperationException {#operationexception-class}

Un `OperationExcepton` est généré lors de l’exécution d’une opération si la requête n’est pas valide ou si une autre erreur se produit. Par exemple, erreurs internes, valeurs de paramètre incorrectes ou autorisations incorrectes. Un `OperationException` est composé d’un code d’état HTTP et d’un message d’erreur, qui sont renvoyés au client comme réponse à `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

La structure de composants sociaux recommande que la logique commerciale responsable de l’opération ne soit pas implémentée dans la classe `SocialOperation`, mais déléguée à un service OSGi. L’utilisation d’un service OSGi pour une logique métier permet à un `SocialComponent`, exécuté par un point de terminaison `SocialOperation`, d’être intégré à d’autres codes et appliqué une logique métier différente.

Toutes les classes `OperationService` étendent `AbstractOperationService`, permettant des extensions supplémentaires pouvant se connecter à l’opération en cours d’exécution. Chaque opération du service est représentée par une classe `SocialOperation`. La classe `OperationExtensions` peut être appelée pendant l’exécution de l’opération en appelant les méthodes

* `performBeforeActions()`

  Permet les prévérifications/prétraitements et validations
* `performAfterActions()`

  Permet de modifier davantage les ressources ou d’appeler des événements personnalisés, des workflows, etc.

#### Classe OperationExtension {#operationextension-class}

Les classes `OperationExtension` sont des éléments de code personnalisés qui peuvent être injectés dans une opération permettant de personnaliser les opérations pour répondre aux besoins de l’entreprise. Les utilisateurs du composant peuvent ajouter des fonctionnalités de manière dynamique et incrémentielle au composant. Le modèle d’extension/crochet permet aux développeurs de se concentrer exclusivement sur les extensions elles-mêmes et élimine la nécessité de copier et de remplacer des opérations et des composants entiers.

## Exemple de code {#sample-code}

Un exemple de code est disponible dans le référentiel [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) . Recherchez des projets avec le préfixe `aem-communities` ou `aem-scf`.

## Bonnes pratiques {#best-practices}

Consultez la section [Consignes de codage](code-guide.md) pour connaître les différentes instructions de codage et les bonnes pratiques à l’intention des développeurs AEM Communities.

Voir aussi [Storage Resource Provider (SRP) pour UGC](srp.md) pour en savoir plus sur l’accès au contenu généré par l’utilisateur.

| **[⇐ Notions fondamentales sur les fonctionnalités](essentials.md)** | **[Personnalisation côté client ⇒](client-customize.md)** |
|---|---|
|   | **[Aide-mémoire SCF ⇒](handlebars-helpers.md)** |
