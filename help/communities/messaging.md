---
title: Configuration de la messagerie
seo-title: Configuration de la messagerie
description: Messagerie des communautés
seo-description: Messagerie des communautés
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# Configuration de la messagerie {#configure-messaging}

## Présentation {#overview}

La fonction de messagerie pour les communautés AEM permet aux (membres) du site connectés d’envoyer des messages qui sont accessibles lorsqu’ils sont connectés au site.

La messagerie est activée pour un site communautaire en cochant une case lors de la création [d&#39;un site](/help/communities/sites-console.md)communautaire.

Cette page contient des informations sur la configuration par défaut et les ajustements possibles.

For additional information for developers, see [Messaging Essentials](/help/communities/essentials-messaging.md).

## Service des opérations de messagerie {#messaging-operations-service}

Le service [de messagerie](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities de configuration identifie le point de fin qui traite les demandes liées à la messagerie, les dossiers que le service doit utiliser pour le stockage des messages et, si les messages peuvent inclure des pièces jointes, les types de fichiers autorisés.

Pour les sites de la communauté créés à l’aide du `Communities Sites console`, une instance du service existe déjà, avec la boîte de réception définie sur `/mail/inbox`.

### Service des opérations de messagerie communautaire {#community-messaging-operations-service}

Comme illustré ci-dessous, il existe une configuration du service pour les sites créés avec l&#39;assistant [de création de](/help/communities/sites-console.md)site. Vous pouvez afficher ou modifier la configuration en sélectionnant l’icône représentant un crayon en regard de la configuration.

![messagerie-opérations](assets/messaging-operations.png)

### Ajouter une nouvelle configuration {#add-new-configuration}

Pour ajouter une nouvelle configuration, sélectionnez l’icône + &quot;**+**&quot; en regard du nom du service :

* **Liste blanche des champs de message**

   Spécifie les propriétés du composant Composer un message que les utilisateurs peuvent modifier et conserver. Si de nouveaux éléments de formulaire sont ajoutés, l’ID d’élément doit être ajouté si vous souhaitez le stocker dans SRP. La valeur par défaut est de deux entrées : *sujet* et *contenu*.

* **Taille limite de la zone de message**

   nombre maximal d’octets dans la zone de message de chaque utilisateur. La valeur par défaut est *1073741824* (1 Go).

* **Limite du nombre de messages**

   Nombre total de messages autorisés par utilisateur. La valeur -1 indique qu’un nombre illimité de messages est autorisé, sous réserve de la taille limite de la zone de message. La valeur par défaut est *10000* (10 000).

* **Avertir l&#39; du en cas d&#39;échec**

   Si cette option est cochée, avertissez l’expéditeur si l’de messages ne parvient pas à certains. Default is *checked*.

* **ID de l&#39;expéditeur  d&#39;échec**

   Nom de l’expéditeur qui apparaît dans le message  échec de l’. La valeur par défaut est *failureNotifier*.

* **Chemin du modèle de message d’échec**

   Chemin d’accès absolu à la racine du modèle de message d’échec  du. La valeur par défaut est */etc/notification/messaging/default*.

* **Nombre de**

   Nombre de tentatives de renvoi d’un message qui ne parvient pas à être remis. La valeur par défaut est *3*.

* **Attendre entre les**

   Nombre de secondes d’attente entre les tentatives de renvoi du message en cas d’échec de l’envoi. Default is *100* (seconds).

* **Compter la taille du pool de mise à jour**

   Nombre de threads simultanés utilisés pour la mise à jour du nombre. La valeur par défaut est *10*.

* **Chemin d’accès de boîte de réception**

   (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*username*), à utiliser pour le **`inbox`** dossier. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/inbox*.

* **Chemin d’accès aux éléments envoyés**

   (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*username*), à utiliser pour le **`send items`** dossier. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/stitems* .

* **Pièces jointes de support**

   Si cette option est cochée, les utilisateurs peuvent ajouter des pièces jointes à leurs messages. Default is *checked*.

* **Activer la messagerie de groupe**

   Si cette option est sélectionnée, les utilisateurs enregistrés peuvent envoyer un message en masse à un groupe de membres. La valeur par défaut est *désélectionnée*.

* **Nombre maximum. du total des**

   Si la messagerie du groupe est activée, indiquez le nombre maximal d’auxquels le message du groupe peut être envoyé à la fois. La valeur par défaut est *100*.

* **Taille du lot**

   Nombre de messages à regrouper pour une envoi lors de l’envoi à un grand groupe de. La valeur par défaut est *100*.

* **Taille totale des pièces jointes**

   Si supportAttachments est coché, cette valeur spécifie la taille totale maximale autorisée (en octets) de toutes les pièces jointes. Default is *104857600* (100 MB).

* **noir type de pièce jointe**

   Liste noire des extensions de nom de fichier, avec le préfixe &#39;**.**&quot;, cela sera rejeté par le système. Si elle n’est pas, l’extension est autorisée. Les extensions peuvent être ajoutées ou supprimées à l’aide des icônes &quot;**+**&quot; et &quot;**-**&quot;.

* **Types de pièces jointes autorisés**

   **(*Action requise*)** Liste blanche des extensions de nom de fichier, à l’opposé de la liste noire. Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles, utilisez l’icône &quot;**-**&quot; pour supprimer l’entrée vide unique.

* **Sélecteur de service**

   (*Obligatoire*) Chemin absolu (point de terminaison) par lequel le service est appelé (ressource virtuelle). La racine du chemin choisi doit être incluse dans le paramètre de configuration Chemins *d&#39;* exécution de la configuration OSGi [ , par exemple `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), `/bin/`et `/apps/``/services/`. Pour sélectionner cette configuration pour la fonction de messagerie d’un site, ce point de fin est fourni comme **`Service selector`** valeur pour la `Message List and Compose Message components` (voir Fonction [de](/help/communities/configure-messaging.md)message).

   La valeur par défaut est */bin/messaging* .

* **Liste blanche des champs**

   Utiliser la liste blanche des champs **de message**.

>[!CAUTION]
>
>Chaque fois qu’une `Messaging Operations Service` configuration est ouverte pour modification, si `allowedAttachmentTypes.name` elle a été supprimée, une entrée vide est ajoutée pour rendre la propriété configurable. Une seule entrée vide désactive les pièces jointes.
>
>Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles, utilisez l’icône &quot;**-**&quot; pour (à nouveau) supprimer l’entrée vide unique avant de cliquer sur **Enregistrer**.


## Group Messaging {#group-messaging}

Pour permettre aux utilisateurs enregistrés d’envoyer des messages directs en bloc aux groupes d’utilisateurs, veillez à **activer la messagerie** de groupe dans les deux instances suivantes de la configuration des services **d’opération de** messagerie :

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Service des opérations de messagerie : console sociale**

![social-console-op-service](assets/social-console-op-service.png)

**Service des opérations de messagerie : messagerie sociale**

![message social-op-service](assets/social-message-op-service.png)

## Résolution des incidents {#troubleshooting}

Une manière de résoudre les problèmes consiste à activer les messages de [débogage dans le journal.](/help/sites-administering/troubleshooting.md)

Voir aussi [Journaux et Ecrivains pour les services](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)individuels.

Le package à surveiller est `com.adobe.cq.social.messaging`.
