---
title: Personnalisation côté serveur
seo-title: Personnalisation côté serveur
description: Personnalisation côté serveur dans les communautés AEM
seo-description: Personnalisation côté serveur dans les communautés AEM
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Personnalisation côté serveur {#server-side-customization}

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

## API Java {#java-apis}

>[!NOTE]
>
>L’emplacement du package des API de communautés peut changer lors de la mise à niveau d’une version majeure vers la prochaine.


### Interface SocialComponent {#socialcomponent-interface}

Les composants sociaux sont des POJO qui représentent une ressource pour une fonctionnalité de communautés AEM. Idéalement, chaque composant SocialComponent représente un type de ressource spécifique avec des objets GETters exposés qui fournissent des données au client afin que la ressource soit correctement représentée. Toute logique métier et toute logique de  sont encapsulées dans SocialComponent, y compris les informations de session de l’de site, si nécessaire.

L’interface définit un ensemble de base de GETters nécessaires pour représenter une ressource. Il est important de noter que l’interface spécifie les méthodes Map&lt;String, Object> getAsMap() et String toJSONString() nécessaires pour rendre les modèles Handlebars et exposer les points de fin GET JSON pour les ressources.

Toutes les classes SocialComponent doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponent`

### Interface SocialCollectionComponent {#socialcollectioncomponent-interface}

L’interface SocialCollectionComponent étend l’interface SocialComponent pour mieux représenter les ressources qui sont des collections d’autres ressources.

Toutes les classes SocialCollectionComponent doivent implémenter l’interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface SocialComponentFactory {#socialcomponentfactory-interface}

Une fabrique SocialComponentFactory (fabrique) enregistre un composant SocialComponent avec la structure. La fabrique permet à la structure de savoir quels composants sociaux sont disponibles pour un type de ressource donné et leur rang de priorité lorsque plusieurs composants sociaux sont identifiés.

Un SocialComponentFactory est responsable de la création d’une instance du composant SocialComponent sélectionné, ce qui permet d’injecter toutes les dépendances dont le composant SocialComponent a besoin à partir de l’usine à l’aide des pratiques d’ID.

Un SocialComponentFactory est un service OSGi et a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Toutes les classes SocialComponentFactory doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponentFactory`

Une implémentation de la méthode SocialComponentFactory.getPriority() doit renvoyer la valeur la plus élevée afin que la fabrique soit utilisée pour la ressourceType donnée, comme renvoyée par getResourceType().

### Interface SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

Le gestionnaire SocialComponentFactoryManager (responsable) gère tous les composants sociaux enregistrés dans la structure et est responsable de la sélection de SocialComponentFactory à utiliser pour une ressource donnée (resourceType). Si aucune usine n&#39;est enregistrée pour un type de ressource spécifique, le gestionnaire renvoie une usine avec le type de super-type le plus proche pour la ressource donnée.

Un SocialComponentFactoryManager est un service OSGi et a accès à d’autres services OSGi qui peuvent être transmis à SocialComponent par l’intermédiaire d’un constructeur.

Un handle vers le service OSGi est obtenu en appelant `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Demandes POST {#http-api-post-requests}

#### PostOperation, classe {#postoperation-class}

Les points de fin POST de l’API HTTP sont des classes PostOperation définies par l’implémentation de l’ `SlingPostOperation` interface (package `org.apache.sling.servlets.post`).

L’implémentation du `PostOperation` point `sling.post.operation` de terminaison définit une valeur à laquelle l’opération répondra. Toutes les requêtes POST avec un paramètre:operation défini sur cette valeur seront déléguées à cette classe d’implémentation.

L’ `PostOperation` opérateur appelle le `SocialOperation` qui effectue les actions nécessaires pour l’opération.

Le `PostOperation` client reçoit le résultat du `SocialOperation` et renvoie la réponse appropriée au client.

#### SocialOperation, classe {#socialoperation-class}

Chaque `SocialOperation` point de fin étend la classe AbstractSocialOperation et remplace la méthode `performOperation()`. Cette méthode effectue toutes les actions nécessaires pour terminer l’opération et renvoyer une erreur `SocialOperationResult` ou renvoyer une erreur `OperationException`, auquel cas un état d’erreur HTTP avec un message, s’il est disponible, est renvoyé à la place de la réponse JSON normale ou du code d’état HTTP de réussite.

L’extension `AbstractSocialOperation` permet la réutilisation de `SocialComponents` pour envoyer des réponses JSON.

#### SocialOperationResult, classe {#socialoperationresult-class}

La `SocialOperationResult` classe est renvoyée comme résultat du `SocialOperation` et est composée d’un message d’état `SocialComponent`, HTTP et HTTP.

Le `SocialComponent` représente la ressource qui a été affectée par l’opération.

Pour une opération de création, le `SocialComponent` inclus dans le `SocialOperationResult` représente la ressource qui vient d&#39;être créée et pour une opération de mise à jour, il représente la ressource qui a été modifiée par l&#39;opération. Non `SocialComponent` renvoyé pour une opération de suppression.

Les codes d’état HTTP de réussite utilisés sont les suivants :

* 201 pour les opérations de création
* 200 pour les opérations de mise à jour
* 204 pour les opérations de suppression

#### OperationException, classe {#operationexception-class}

Une erreur `OperationExcepton` peut être générée lors de l’exécution d’une opération si la requête n’est pas valide ou si une autre erreur se produit, telle que des erreurs internes, des valeurs de paramètre incorrectes, des autorisations incorrectes, etc. Un `OperationException` est composé d’un code d’état HTTP et d’un message d’erreur, qui sont renvoyés au client en tant que réponse au `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

La structure des composants sociaux recommande que la logique métier responsable de l’exécution de l’opération ne soit pas implémentée dans la `SocialOperation` classe, mais déléguée à un service OSGi. L’utilisation d’un service OSGi pour la logique métier permet à un `SocialComponent`point de terminaison d’agir en fonction d’un `SocialOperation` point de terminaison d’être intégré à un autre code et d’appliquer une logique métier différente.

Toutes les `OperationService` classes s’étendent `AbstractOperationService`, ce qui permet des extensions supplémentaires qui peuvent se connecter à l’opération en cours. Chaque opération du service est représentée par une `SocialOperation` classe. La `OperationExtensions` classe peut être appelée pendant l&#39;exécution de l&#39;opération en appelant les méthodes

* `performBeforeActions()`

   Autorise les pré-contrôles/prétraitement et validations
* `performAfterActions()`

   Permet d’apporter d’autres modifications aux ressources ou d’appeler des  personnalisées, des , etc.

#### OperationExtension, classe {#operationextension-class}

`OperationExtension` sont des éléments de code personnalisés qui peuvent être injectés dans une opération permettant de personnaliser les opérations en fonction des besoins de l’entreprise. Les utilisateurs du composant peuvent ajouter dynamiquement et progressivement des fonctionnalités au composant. Le modèle extension/hook permet aux développeurs de se concentrer exclusivement sur les extensions elles-mêmes et élimine le besoin de copier et de remplacer des opérations et des composants entiers.

## Exemple de code {#sample-code}

L’exemple de code est disponible dans le référentiel [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) . Recherchez des projets avec le préfixe `aem-communities` ou `aem-scf`.

## Bonnes pratiques {#best-practices}

 la section [Coding Guidelines](code-guide.md) pour connaître les différentes directives de codage et les bonnes pratiques pour les développeurs de communautés AEM.

Voir aussi [fournisseur de ressources  (SRP) pour en savoir plus sur l’accès au contenu généré par l’utilisateur par l’UGC](srp.md) .

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté client](client-customize.md)** |
|---|---|
|  | **[Aide-mémoire SCF →](handlebars-helpers.md)** |

