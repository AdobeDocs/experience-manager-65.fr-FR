---
title: Personnalisation côté serveur
description: Découvrez comment la personnalisation côté serveur dans Adobe Experience Manager Communities.
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
source-wordcount: '897'
ht-degree: 1%

---

# Personnalisation côté serveur {#server-side-customization}

| ⇐ Feature Essentials ](essentials.md)****[ | ⇒ de personnalisation côté client ](client-customize.md)****[ |
|---|---|
|   | ⇒ des assistants Handlebars SCF ](handlebars-helpers.md)****[ |

## API Java™ {#java-apis}

>[!NOTE]
>
>L’emplacement du package des API de Communities peut changer lors de la mise à niveau d’une version majeure vers la suivante.

### Interface des composants sociaux {#socialcomponent-interface}

Les composants sociaux sont des POJO qui représentent une ressource pour une fonctionnalité AEM Communities. Idéalement, chaque SocialComponent représente un resourceType spécifique avec des GETters exposés qui fournissent des données au client afin que la ressource soit représentée avec précision. Toute la logique commerciale et de vue est encapsulée dans le composant social, y compris les informations de session du visiteur du site, si nécessaire.

L’interface définit un ensemble de base de termes GET nécessaires pour représenter une ressource. Il est important de noter que l’interface spécifie les méthodes Map&lt;String, Object> getAsMap() et String toJSONString() qui sont nécessaires pour effectuer le rendu des modèles Handlebars et exposer les points d’entrée GET JSON pour les ressources.

Toutes les classes SocialComponent doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponent`

### Interface du composant SocialCollection {#socialcollectioncomponent-interface}

L’interface SocialCollectionComponent étend l’interface SocialComponent pour mieux représenter les ressources qui sont des collections d’autres ressources.

Toutes les classes SocialCollectionComponent doivent implémenter l&#39;interface com.adobe.cq.social.scf.SocialCollectionComponent

### Interface de SocialComponentFactory {#socialcomponentfactory-interface}

Un SocialComponentFactory (usine) enregistre un SocialComponent auprès du framework. La fabrique fournit un moyen d’indiquer au framework quels composants sociaux sont disponibles pour un type de ressource donné et leur rang de priorité lorsque plusieurs composants sociaux sont identifiés.

Un SocialComponentFactory est chargé de créer une instance du SocialComponent sélectionné, ce qui permet d’injecter toutes les dépendances nécessaires au SocialComponent depuis la fabrique à l’aide de pratiques d’identification.

Un SocialComponentFactory est un service OSGi et a accès à d’autres services OSGi qui peuvent être transmis au SocialComponent par l’intermédiaire d’un constructeur.

Toutes les classes SocialComponentFactory doivent implémenter l’interface `com.adobe.cq.social.scf.SocialComponentFactory`

Une implémentation de la méthode SocialComponentFactory.getPriority() doit renvoyer la valeur la plus élevée pour que la fabrique soit utilisée pour le resourceType donné, tel que renvoyé par getResourceType().

### Interface de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (gestionnaire) gère tous les composants sociaux enregistrés dans le framework et est chargé de sélectionner le socialComponentFactory à utiliser pour une ressource donnée (resourceType). Si aucune fabrique n&#39;est enregistrée pour un resourceType spécifique, le gestionnaire renvoie une fabrique avec le super type le plus proche pour la ressource donnée.

Un SocialComponentFactoryManager est un service OSGi qui a accès à d’autres services OSGi qui peuvent être transmis au SocialComponent par l’intermédiaire d’un constructeur.

Un handle vers le service OSGi est obtenu en appelant `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP - Requêtes POST {#http-api-post-requests}

#### Classe PostOperation {#postoperation-class}

Les points d’entrée POST de l’API HTTP sont des classes PostOperation définies en implémentant l’interface `SlingPostOperation` (`org.apache.sling.servlets.post` de package).

L’implémentation du point d’entrée `PostOperation` définit la `sling.post.operation` sur une valeur à laquelle l’opération répond. Toutes les requêtes POST avec un paramètre :operation défini sur cette valeur sont déléguées à cette classe d’implémentation.

Le `PostOperation` appelle la `SocialOperation` qui effectue les actions nécessaires à l’opération.

Le `PostOperation` reçoit le résultat du `SocialOperation` et renvoie la réponse appropriée au client.

#### Classe d’opération sociale {#socialoperation-class}

Chaque point d’entrée `SocialOperation` étend la classe AbstractSocialOperation et remplace la `performOperation()` de méthode. Cette méthode effectue toutes les actions nécessaires pour terminer l’opération et renvoyer un `SocialOperationResult` ou, à défaut, lancer une `OperationException`. Dans ce cas, un statut d’erreur HTTP avec un message, le cas échéant, est renvoyé à la place de la réponse JSON normale ou du code de statut HTTP de succès.

L’extension de `AbstractSocialOperation` permet la réutilisation de `SocialComponents` pour envoyer des réponses JSON.

#### SocialOperationResult, classe {#socialoperationresult-class}

La classe `SocialOperationResult` est renvoyée à la suite de l’`SocialOperation` et est composée d’un `SocialComponent`, d’un code d’état HTTP et d’un message d’état HTTP.

Le `SocialComponent` représente la ressource qui a été affectée par l’opération.

Pour une opération Créer , la `SocialComponent` incluse dans le `SocialOperationResult` représente la ressource créée et pour une opération Mettre à jour , elle représente la ressource qui a été modifiée par l’opération. Aucune `SocialComponent` n’est renvoyée pour une opération de suppression.

Les codes d’état HTTP de succès utilisés sont les suivants :

* 201 pour les opérations Créer
* 200 pour les opérations de mise à jour
* 204 pour les opérations de suppression

#### Classe OperationException {#operationexception-class}

Une `OperationExcepton` est générée lors de l’exécution d’une opération si la requête n’est pas valide ou si une autre erreur se produit. Par exemple, des erreurs internes, des valeurs de paramètre incorrectes ou des autorisations incorrectes. Un `OperationException` est composé d’un code d’état HTTP et d’un message d’erreur, qui sont renvoyés au client en tant que réponse au `PostOperatoin`.

#### Classe OperationService {#operationservice-class}

La structure des composants sociaux recommande que la logique commerciale responsable de l’exécution de l’opération ne soit pas implémentée dans la classe `SocialOperation`, mais plutôt déléguée à un service OSGi. L’utilisation d’un service OSGi pour la logique commerciale permet à un `SocialComponent`, sur lequel agit un point d’entrée `SocialOperation`, d’être intégré à d’autres codes et d’appliquer une logique commerciale différente.

Toutes les classes de `OperationService` étendent `AbstractOperationService`, ce qui permet à d’autres extensions de se connecter à l’opération en cours d’exécution. Chaque opération du service est représentée par une classe `SocialOperation`. La classe `OperationExtensions` peut être appelée lors de l’exécution de l’opération en appelant les méthodes .

* `performBeforeActions()`

  Permet les prévérifications/prétraitements et les validations.
* `performAfterActions()`

  Permet de modifier davantage les ressources ou d’appeler des événements personnalisés, des workflows, etc.

#### OperationExtension, classe {#operationextension-class}

Les classes `OperationExtension` sont des éléments de code personnalisés qui peuvent être injectés dans une opération afin de personnaliser les opérations pour répondre aux besoins de l’entreprise. Les consommateurs du composant peuvent ajouter des fonctionnalités au composant de manière dynamique et incrémentielle. Le modèle extension/hook permet aux développeurs de se concentrer exclusivement sur les extensions elles-mêmes et supprime la nécessité de copier et de remplacer des opérations et des composants entiers.

## Exemple de code {#sample-code}

L’exemple de code est disponible dans le référentiel [GitHub Adobe Experience Cloud](https://github.com/Adobe-Marketing-Cloud). Recherchez des projets dotés du préfixe `aem-communities` ou `aem-scf`.

## Bonnes pratiques {#best-practices}

Consultez la section [Consignes de codage](code-guide.md) pour obtenir diverses consignes de codage et bonnes pratiques pour les développeurs AEM Communities.

Consultez également la section [Fournisseur de ressources de stockage (SRP) pour le contenu créé par l’utilisateur](srp.md) pour en savoir plus sur l’accès au contenu généré par l’utilisateur.

| ⇐ Feature Essentials ](essentials.md)****[ | ⇒ de personnalisation côté client ](client-customize.md)****[ |
|---|---|
|   | ⇒ des assistants Handlebars SCF ](handlebars-helpers.md)****[ |
