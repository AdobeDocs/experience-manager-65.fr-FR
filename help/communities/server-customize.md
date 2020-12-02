---
title: Personnalisation côté serveur
seo-title: Personnalisation côté serveur
description: Personnalisation côté serveur en AEM Communities
seo-description: Personnalisation côté serveur en AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# Personnalisation côté serveur {#server-side-customization}

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

## API Java {#java-apis}

>[!NOTE]
>
>L’emplacement du package des API Communautés peut être modifié lors de la mise à niveau d’une version majeure vers la prochaine.

### Interface du composant social {#socialcomponent-interface}

Les composants sociaux sont des POJO qui représentent une ressource pour une fonction AEM Communities. Idéalement, chaque composant SocialComponent représente un type de ressource spécifique avec des balises GETters exposées qui fournissent des données au client afin que la ressource soit représentée de manière précise. Toute la logique métier et la logique de vue sont encapsulées dans SocialComponent, y compris les informations de session du visiteur du site, si nécessaire.

L’interface définit un ensemble de base de GETters nécessaires pour représenter une ressource. L’interface stipule les méthodes Map&lt;String, Object> getAsMap() et String toJSONString() nécessaires pour rendre les modèles Handlebars et exposer les points de terminaison GET JSON pour les ressources.

Toutes les classes SocialComponent doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponent`

### Interface SocialCollectionComponent {#socialcollectioncomponent-interface}

L’interface SocialCollectionComponent étend l’interface SocialComponent pour mieux représenter les ressources qui sont des collections d’autres ressources.

Toutes les classes SocialCollectionComponent doivent implémenter l’interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface SocialComponentFactory {#socialcomponentfactory-interface}

Une fabrique de composants sociaux (fabrique) enregistre un composant social avec la structure. La fabrique permet à la structure de savoir quels composants sociaux sont disponibles pour un type de ressource donné et leur rang de priorité lorsque plusieurs composants sociaux sont identifiés.

Un SocialComponentFactory est responsable de la création d’une instance du SocialComponent sélectionné, ce qui permet d’injecter toutes les dépendances dont le SocialComponent a besoin à partir de l’usine à l’aide des pratiques d’ID.

Un SocialComponentFactory est un service OSGi et a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Toutes les classes SocialComponentFactory doivent implémenter l&#39;interface `com.adobe.cq.social.scf.SocialComponentFactory`

Une implémentation de la méthode SocialComponentFactory.getPriority() doit renvoyer la valeur la plus élevée pour que la fabrique soit utilisée pour le type de ressource donné, comme retourné par getResourceType().

### Interface SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (gestionnaire) gère tous les composants SocialComponents enregistrés dans la structure et est responsable de la sélection de SocialComponentFactory à utiliser pour une ressource donnée (resourceType). Si aucune usine n&#39;est enregistrée pour un type de ressource spécifique, le gestionnaire renvoie une usine avec le type de ressource le plus proche pour la ressource donnée.

Un SocialComponentFactoryManager est un service OSGi et a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Un handle vers le service OSGi est obtenu en appelant `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Demandes du POST {#http-api-post-requests}

#### PostOperation, classe {#postoperation-class}

Les points de terminaison du POST d&#39;API HTTP sont des classes PostOperation définies en implémentant l&#39;interface `SlingPostOperation` (package `org.apache.sling.servlets.post`).

L&#39;implémentation du point de terminaison `PostOperation` définit `sling.post.operation` sur une valeur à laquelle l&#39;opération répondra. Toutes les requêtes du POST dont le paramètre a:operation est défini sur cette valeur seront déléguées à cette classe d&#39;implémentation.

Le `PostOperation` appelle le `SocialOperation` qui exécute les actions nécessaires pour l&#39;opération.

`PostOperation` reçoit le résultat de `SocialOperation` et renvoie la réponse appropriée au client.

#### Classe SocialOperation {#socialoperation-class}

Chaque point de terminaison `SocialOperation` étend la classe AbstractSocialOperation et remplace la méthode `performOperation()`. Cette méthode effectue toutes les actions nécessaires pour terminer l&#39;opération et renvoyer un `SocialOperationResult` ou sinon lancer un `OperationException`, auquel cas un état d&#39;erreur HTTP avec un message, s&#39;il est disponible, est renvoyé à la place de la réponse JSON normale ou du code d&#39;état HTTP de réussite.

L&#39;extension de `AbstractSocialOperation` permet la réutilisation de `SocialComponents` pour envoyer des réponses JSON.

#### SocialOperationResult, classe {#socialoperationresult-class}

La classe `SocialOperationResult` est renvoyée comme résultat de `SocialOperation` et est composée d&#39;un `SocialComponent`, d&#39;un code d&#39;état HTTP et d&#39;un message d&#39;état HTTP.

`SocialComponent` représente la ressource qui a été affectée par l&#39;opération.

Pour une opération de création, l&#39;élément `SocialComponent` inclus dans l&#39;élément `SocialOperationResult` représente la ressource qui vient d&#39;être créée et pour une opération de mise à jour, il représente la ressource qui a été modifiée par l&#39;opération. Aucun élément `SocialComponent` n&#39;est renvoyé pour une opération de suppression.

Les codes d’état HTTP de réussite utilisés sont les suivants :

* 201 pour les opérations de création
* 200 pour les opérations de mise à jour
* 204 pour les opérations de suppression

#### Classe OperationException {#operationexception-class}

Un `OperationExcepton` peut être envoyé lors de l&#39;exécution d&#39;une opération si la requête n&#39;est pas valide ou qu&#39;une autre erreur se produit, telle que des erreurs internes, des valeurs de paramètre erronées, des autorisations incorrectes, etc. Un `OperationException` est composé d&#39;un code d&#39;état HTTP et d&#39;un message d&#39;erreur, qui sont renvoyés au client comme réponse à `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

La structure des composants sociaux recommande que la logique métier responsable de l&#39;exécution de l&#39;opération ne soit pas implémentée dans la classe `SocialOperation`, mais plutôt déléguée à un service OSGi. L’utilisation d’un service OSGi pour la logique métier permet à un `SocialComponent`, agissant par un point de terminaison `SocialOperation`, d’être intégré à un autre code et d’appliquer une logique métier différente.

Toutes les classes `OperationService` s&#39;étendent `AbstractOperationService`, ce qui permet des extensions supplémentaires pouvant être associées à l&#39;opération en cours. Chaque opération du service est représentée par une classe `SocialOperation`. La classe `OperationExtensions` peut être appelée pendant l&#39;exécution de l&#39;opération en appelant les méthodes

* `performBeforeActions()`

   Permet les pré-contrôles/prétraitement et les validations
* `performAfterActions()`

   Permet de modifier davantage les ressources ou d’appeler des événements, workflows, etc. personnalisés

#### OperationExtension Class {#operationextension-class}

`OperationExtension` sont des éléments de code personnalisés qui peuvent être injectés dans une opération permettant de personnaliser les opérations en fonction des besoins de l’entreprise. Les utilisateurs du composant peuvent ajouter de manière dynamique et incrémentielle des fonctionnalités au composant. Le modèle extension/hook permet aux développeurs de se concentrer exclusivement sur les extensions elles-mêmes et élimine le besoin de copier et de remplacer des opérations et des composants entiers.

## Exemple de code {#sample-code}

Un exemple de code est disponible dans le référentiel [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud). Recherchez des projets avec le préfixe `aem-communities` ou `aem-scf`.

## Bonnes pratiques {#best-practices}

Vue de la section [Lignes directrices sur le codage](code-guide.md) pour connaître les différentes directives de codage et les meilleures pratiques pour les développeurs AEM Communities.

Voir aussi [Fournisseur de ressources d’Enregistrement (SRP) pour UGC](srp.md) pour en savoir plus sur l’accès au contenu généré par l’utilisateur.

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

