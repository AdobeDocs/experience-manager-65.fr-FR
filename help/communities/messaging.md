---
title: Configuration de la messagerie
description: Découvrez la fonction de messagerie d’AEM Communities qui permet aux visiteurs (membres) du site connectés d’envoyer des messages les uns aux autres.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Configuration de la messagerie {#configure-messaging}

## Vue d’ensemble {#overview}

La fonction de messagerie d’AEM Communities permet aux visiteurs (membres) du site connectés d’envoyer entre eux des messages accessibles lorsqu’ils sont connectés au site.

La messagerie est activée pour un site communautaire en cochant une case lors de la [création d’un site communautaire](/help/communities/sites-console.md).

Cette page contient des informations sur la configuration par défaut et les réglages possibles.

Pour plus d’informations à l’intention des développeurs, voir [Notions fondamentales sur la messagerie](/help/communities/essentials-messaging.md).

## Service des opérations de messagerie {#messaging-operations-service}

La configuration [&#x200B; Service des opérations de messagerie AEM Communities &#x200B;](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifie le point de terminaison qui gère les requêtes liées aux messages, les dossiers que le service doit utiliser pour stocker les messages, et si les messages peuvent inclure des pièces jointes, quels types de fichiers sont autorisés.

Pour les sites de communauté créés à l’aide de `Communities Sites console`, il existe une instance du service, la boîte de réception étant définie sur `/mail/inbox`.

### Service des opérations de messagerie communautaire {#community-messaging-operations-service}

Comme illustré ci-dessous, il existe une configuration du service pour les sites créés avec l’ [assistant de création de site](/help/communities/sites-console.md). La configuration peut être visualisée ou modifiée en sélectionnant l’icône en forme de crayon en regard de la configuration.

![messaging-operations](assets/messaging-operations.png)

### Ajouter une nouvelle configuration {#add-new-configuration}

Pour ajouter une configuration, sélectionnez l’icône &quot;**+**&quot; en regard du nom du service :

* **Liste autorisée des champs de message**

  Indique les propriétés du composant Composer le message que les utilisateurs peuvent modifier et conserver. Si de nouveaux éléments de formulaire sont ajoutés, l’ID d’élément doit être ajouté si vous le souhaitez afin d’être stocké dans la SRP. La valeur par défaut est de deux entrées : *subject* et *content*.

* **Limite de taille de la zone de message**

  Nombre maximal d’octets dans la zone de message de chaque utilisateur. La valeur par défaut est *1073741824* (1 Go).

* **Limite du nombre de messages**

  Nombre total de messages autorisés par utilisateur. La valeur -1 indique qu’un nombre illimité de messages est autorisé, sous réserve de la limite de taille de la zone de message. La valeur par défaut est *1000* (10k).

* **Avertir l’échec de diffusion**

  Si cette case est cochée, avertissez l’expéditeur si la diffusion du message échoue à certains destinataires. La valeur par défaut est *checked*.

* **Identifiant de l’expéditeur de la diffusion d’échec**

  Nom de l’expéditeur qui apparaît dans le message en échec de la diffusion. La valeur par défaut est *failureNotifier*.

* **Chemin d’accès au modèle de message d’échec**

  Chemin d’accès absolu à la racine du modèle de message en échec de la diffusion. La valeur par défaut est */etc/notification/messaging/default*.

* **Nombre de reprises**

  Nombre de tentatives d’envoi d’un message qui ne parvient pas à être diffusé. La valeur par défaut est *3*.

* **Attente entre reprises**

  Nombre de secondes d’attente entre les tentatives de renvoi du message en cas d’échec de l’envoi. La valeur par défaut est *100* (secondes).

* **Compter la taille du pool de mise à jour**

  Nombre de threads simultanés utilisés pour la mise à jour du nombre. La valeur par défaut est *10*.

* **Chemin de la boîte de réception**

  (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*nom d’utilisateur*), à utiliser pour le dossier `inbox`. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/inbox*.

* **Chemin d’accès aux éléments envoyés**

  (*Obligatoire*) Chemin d’accès, relatif au noeud de l’utilisateur (/home/users/*nom d’utilisateur*), à utiliser pour le dossier `sent items`. Le chemin ne doit PAS se terminer par une barre oblique (/) à la fin. La valeur par défaut est */mail/stitems* .

* **Pièces jointes de support**

  Si cette case est cochée, les utilisateurs peuvent ajouter des pièces jointes à leurs messages. La valeur par défaut est *checked*.

* **Activer la messagerie de groupe**

  Si cette option est sélectionnée, les utilisateurs enregistrés peuvent envoyer des messages en bloc à un groupe de membres. La valeur par défaut est *désélectionné*.

* **Nombre maximal. of total recipients**

  Si la messagerie du groupe est activée, indiquez le nombre maximal de destinataires auxquels le message du groupe peut être envoyé à la fois. La valeur par défaut est *100*.

* **Taille du lot**

  Nombre de messages à grouper pour un envoi lors de l’envoi à un grand groupe de destinataires. La valeur par défaut est *100*.

* **Taille totale de la pièce jointe**

  Si supportAttachments est coché, cette valeur spécifie la taille totale maximale autorisée (en octets) de toutes les pièces jointes. La valeur par défaut est *104857600* (100 Mo).

* **liste bloquée de type pièce jointe**

  Liste bloquée des extensions de nom de fichier, précédée de &#39;**&#39;.**&#39;, qui est rejeté par le système. Si elle n’est pas placée sur la liste bloquée, l’extension est autorisée. Les extensions peuvent être ajoutées ou supprimées à l’aide des icônes &#39;**+**&#39; et &#39;**-**&#39;.

* **Types de pièces jointes autorisés**

  **(*Action requise*)** liste autorisée des extensions de nom de fichier, à l’opposé de la liste bloquée. Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles placées sur la liste bloquée, utilisez l’icône &quot;**-**&quot; pour supprimer l’entrée vide unique.

* **Sélecteur de service**

  (*Obligatoire*) Un chemin absolu (point de terminaison) par lequel le service est appelé (une ressource virtuelle). La racine du chemin choisi doit être incluse dans le paramètre de configuration *Chemins d’exécution* de la configuration OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), par exemple `/bin/`, `/apps/` et `/services/`. Pour sélectionner cette configuration pour la fonction de messagerie d’un site, ce point de terminaison est fourni comme valeur **`Service selector`** pour la fonction `Message List and Compose Message components` (voir [Fonctionnalité du message](/help/communities/configure-messaging.md)).

  La valeur par défaut est */bin/messaging* .

* **Liste autorisée de champ**

  Utilisez la **Liste autorisée Champs du message**.

>[!CAUTION]
>
>Chaque fois qu’une configuration `Messaging Operations Service` est ouverte pour modification, si `allowedAttachmentTypes.name` a été supprimé, une entrée vide est lue pour rendre la propriété configurable. Une seule entrée vide désactive efficacement les pièces jointes.
>
>Pour autoriser toutes les extensions de nom de fichier, à l’exception de celles placées sur la liste bloquée, utilisez l’icône &quot;**-**&quot; pour (à nouveau) supprimer l’entrée vide unique avant de cliquer sur **Enregistrer**.

## Messagerie de groupe {#group-messaging}

Pour permettre aux utilisateurs enregistrés d’envoyer des messages directs en masse aux groupes d’utilisateurs, veillez à **Activer la messagerie de groupe** dans les deux instances suivantes de la configuration **Messaging Operation Services** :

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Service des opérations de messagerie : console sociale**

![social-console-op-service](assets/social-console-op-service.png)

**Service d&#39;exploitation de messagerie : messagerie sociale**

![social-message-op-service](assets/social-message-op-service.png)

## Résolution des problèmes {#troubleshooting}

Pour résoudre les problèmes, une méthode consiste à activer le [débogage des messages dans le journal.](/help/sites-administering/troubleshooting.md)

Voir aussi [Enregistreurs et rédacteurs pour les services individuels](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Le package à surveiller est `com.adobe.cq.social.messaging`.
