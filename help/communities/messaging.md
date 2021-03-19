---
title: Configurer la messagerie
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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Configurer la messagerie {#configure-messaging}

## Présentation {#overview}

La fonction de messagerie pour AEM Communities permet aux visiteurs (membres) du site connectés d&#39;envoyer des messages les uns aux autres qui sont accessibles lorsqu&#39;ils sont connectés au site.

La messagerie est activée pour un site communautaire en cochant une case lors de la création [du site communautaire](/help/communities/sites-console.md).

Cette page contient des informations sur la configuration par défaut et les ajustements possibles.

Pour plus d’informations pour les développeurs, voir [Messaging Essentials](/help/communities/essentials-messaging.md).

## Service des opérations de messagerie {#messaging-operations-service}

La configuration [Service d&#39;opérations de messagerie d&#39;AEM Communities ](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifie le point de terminaison qui traite les demandes liées à la messagerie, les dossiers que le service doit utiliser pour stocker les messages et si les messages peuvent inclure des pièces jointes, quels types de fichiers sont autorisés.

Pour les sites communautaires créés à l&#39;aide de `Communities Sites console`, il existe déjà une instance du service, la boîte de réception étant définie sur `/mail/inbox`.

### Service des opérations de messagerie communautaire {#community-messaging-operations-service}

Comme indiqué ci-dessous, il existe une configuration du service pour les sites créés avec l&#39;[assistant de création de site](/help/communities/sites-console.md). La configuration peut être affichée ou modifiée en sélectionnant l&#39;icône représentant un crayon en regard de la configuration.

![messagerie-opérations](assets/messaging-operations.png)

### Ajouter une nouvelle configuration {#add-new-configuration}

Pour ajouter une nouvelle configuration, sélectionnez l’icône plus &quot;**+**&quot; en regard du nom du service :

* **Liste autorisée Champs de message**

   Indique les propriétés du composant Composer un message que les utilisateurs peuvent modifier et conserver. Si de nouveaux éléments de formulaire sont ajoutés, l’ID d’élément doit être ajouté si vous souhaitez le stocker dans SRP. La valeur par défaut est de deux entrées : *sujet* et *contenu*.

* **Limite de taille de la zone de message**

   Nombre maximal d’octets dans la zone de message de chaque utilisateur. La valeur par défaut est *1073741824* (1 Go).

* **Limite du nombre de messages**

   Nombre total de messages autorisés par utilisateur. La valeur -1 indique qu’un nombre illimité de messages est autorisé, sous réserve de la taille limite de la zone de message. La valeur par défaut est *10000* (10k).

* **Avertir l&#39;échec de la diffusion**

   Si cette case est cochée, avertissez l&#39;expéditeur si la diffusion de messages ne parvient pas à certains destinataires. La valeur par défaut est *cochée*.

* **ID de l&#39;expéditeur de la diffusion d&#39;échec**

   Nom de l&#39;expéditeur qui apparaît dans le message d&#39;échec de la diffusion. La valeur par défaut est *failureNotifier*.

* **Chemin du modèle de message d’échec**

   Chemin d’accès absolu à la racine du modèle de message d’échec de la diffusion. La valeur par défaut est */etc/notification/messaging/default*.

* **Nombre de Reprises**

   Nombre de tentatives de renvoi d’un message dont la remise a échoué. La valeur par défaut est *3*.

* **Attendre entre les Reprises**

   Nombre de secondes d&#39;attente entre les tentatives de renvoi du message en cas d&#39;échec de l&#39;envoi. La valeur par défaut est *100* (secondes).

* **Compter la taille du pool de mise à jour**

   Nombre de threads simultanés utilisés pour la mise à jour du nombre. La valeur par défaut est *10*.

* **Chemin d’accès de boîte de réception**

   (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*nom_utilisateur*), à utiliser pour le dossier `inbox`. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/inbox*.

* **Chemin d&#39;accès aux éléments envoyés**

   (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*nom_utilisateur*), à utiliser pour le dossier `sent items`. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/stitems*.

* **Pièces jointes d&#39;assistance**

   Si cette case est cochée, les utilisateurs peuvent ajouter des pièces jointes à leurs messages. La valeur par défaut est *cochée*.

* **Activer la messagerie de groupe**

   Si cette option est sélectionnée, les utilisateurs enregistrés peuvent envoyer un message en masse à un groupe de membres. La valeur par défaut est *désélectionnée*.

* **Nombre maximal. de tous les destinataires**

   Si la messagerie de groupe est activée, indiquez le nombre maximal de destinataires auxquels le message de groupe peut être envoyé à la fois. La valeur par défaut est *100*.

* **Taille du lot**

   Nombre de messages à traiter par lots pour un envoi lors de l&#39;envoi à un grand groupe de destinataires. La valeur par défaut est *100*.

* **Taille totale de la pièce jointe**

   Si supportAttachments est coché, cette valeur spécifie la taille totale maximale autorisée (en octets) de toutes les pièces jointes. La valeur par défaut est *104857600* (100 Mo).

* **Liste bloquée de type de pièce jointe**

   Liste bloquée des extensions de nom de fichier, précédée de &quot;**&quot;.**&quot;, cela sera rejeté par le système. Si elle n’est pas placée sur la liste bloquée, l’extension est autorisée. Les extensions peuvent être ajoutées ou supprimées à l&#39;aide des icônes &#39;**+**&#39; et &#39;**-**&#39;.

* **Types de pièces jointes autorisés**

   **(*Action requise*)** liste autorisée des extensions de nom de fichier, à l’opposé de la liste bloquée. Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles placées sur la liste bloquée, utilisez l’icône &quot;**-**&quot; pour supprimer l’entrée vide unique.

* **Sélecteur de service**

   (*Obligatoire*) Chemin absolu (point de terminaison) par lequel le service est appelé (une ressource virtuelle). La racine du chemin choisi doit être incluse dans le paramètre de configuration *Chemins d&#39;exécution* d&#39;OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), tel que `/bin/`, `/apps/` et `/services/`. Pour sélectionner cette configuration pour la fonction de messagerie d&#39;un site, ce point de terminaison est fourni en tant que valeur **`Service selector`** pour `Message List and Compose Message components` (voir [Fonction du message](/help/communities/configure-messaging.md)).

   La valeur par défaut est */bin/messaging*.

* **Liste autorisée de champ**

   Utilisez la Liste autorisée **Champs de message**.

>[!CAUTION]
>
>Chaque fois qu&#39;une configuration `Messaging Operations Service` est ouverte pour modification, si `allowedAttachmentTypes.name` a été supprimée, une entrée vide est ajoutée pour rendre la propriété configurable. Une seule entrée vide désactive efficacement les pièces jointes.
>
>Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles placées sur la liste bloquée, utilisez l’icône &quot;**-**&quot; pour (à nouveau) supprimer l’entrée vide unique avant de cliquer sur **Enregistrer**.

## Messagerie de groupe {#group-messaging}

Pour permettre aux utilisateurs enregistrés d&#39;envoyer des messages directs en bloc aux groupes d&#39;utilisateurs, veillez à **activer la messagerie de groupe** dans les deux instances suivantes de la configuration **Messaging Operation Services** :

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Service des opérations de messagerie : console sociale**

![social-console-op-service](assets/social-console-op-service.png)

**Service des opérations de messagerie : messagerie sociale**

![message social-op-service](assets/social-message-op-service.png)

## Résolution des incidents {#troubleshooting}

Une façon de résoudre les problèmes consiste à activer les [messages de débogage dans le journal.](/help/sites-administering/troubleshooting.md)

Voir aussi [Journaliseurs et écrivains pour les services individuels](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Le package à surveiller est `com.adobe.cq.social.messaging`.
