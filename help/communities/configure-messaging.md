---
title: Fonctionnalité de messagerie
description: Découvrez comment configurer la fonctionnalité de messagerie d’AEM Communities pour permettre aux membres de la communauté d’interagir entre eux de manière plus privée.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---

# Fonctionnalité de messagerie {#messaging-feature}

Outre les interactions publiques qui se produisent dans les forums et les commentaires, la fonction de messagerie d’AEM Communities permet aux membres de la communauté d’interagir de manière plus privée.

Cette fonctionnalité peut être incluse lors de la création d’un [site communautaire](/help/communities/overview.md#communitiessites).

La fonctionnalité de messagerie vous permet d’effectuer les opérations suivantes :

**A** - envoyer un message à un ou plusieurs membres de la communauté

**B** - envoyer des messages directs en [masse aux groupes de membres de la communauté](/help/communities/messaging.md#group-messaging)

**C** - envoyer un message avec des pièces jointes

**D** - transférer un message

**E** - Réponse à un message

**F** - supprimer un message

**G** - restaurer un message supprimé

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Pour activer et modifier la fonction de messagerie, voir :

* [Configuration de la messagerie](/help/communities/messaging.md) pour les administrateurs
* [Notions fondamentales sur la messagerie](/help/communities/essentials-messaging.md) pour les développeurs

>[!NOTE]
>
>Il n’est pas possible d’ajouter des composants `Compose Message, Message, or Message List` (présents dans le groupe `Communities`component) à une page en mode d’édition de création.

## Configuration des composants de messagerie {#configure-messaging-components}

Lorsque la messagerie est activée pour un site de la communauté, elle est configurée sans autre configuration nécessaire. Les informations sont fournies si la configuration par défaut doit être modifiée.

### Configurer la liste des messages (zone de message) {#configure-message-list-message-box}

Pour modifier la configuration de la liste des messages pour les pages **Boîte de réception**, **Éléments envoyés** et **Corbeille** de la fonction de messagerie, ouvrez le site en [mode de modification de l’auteur](/help/communities/sites-console.md#authoring-site-content).

1. En mode `Preview`, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite **Boîte de réception**, **Éléments envoyés** ou **Corbeille** pour configurer le composant pour cette liste de messages.

1. En mode `Edit`, sélectionnez le composant sur la page.
1. Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant l’icône `link`.
Une fois l’héritage annulé, il est possible de sélectionner l’icône de configuration pour ouvrir la boîte de dialogue de configuration.

1. Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’icône `broken link`.

![configure-message-list](assets/configure-message-list.png)

#### Onglet Simple {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Sélecteur de service**

  (*Obligatoire*) Définissez-le sur la valeur de la propriété **`serviceSelector.name`** du [ Service de messagerie AEM Communities ](/help/communities/messaging.md#messaging-operations-service).

* **Composer la page**

  (*Obligatoire*) Page à ouvrir lorsqu’un membre clique sur le bouton **`Reply`**. La page cible doit contenir le formulaire **Composer le message**.

* **Répondre/Afficher en tant que ressource**

  Si cette case est cochée, l’URL de réponse et l’URL d’affichage référencent une ressource, ou si des données sont transmises en tant que paramètres de requête dans l’URL.

* **Formulaire d’affichage de profil**

  Formulaire de profil à utiliser pour afficher le profil des expéditeurs.

* **Dossier de corbeille**

  Si cette case est cochée, ce composant Liste de messages affiche uniquement les messages marqués comme supprimés (corbeille).

* **Chemins du dossier**

  (*Obligatoire*) Référencement des valeurs définies pour **inbox.path.name** et **stitems.path.name** dans le [service des opérations de messagerie AEM Communities](/help/communities/messaging.md#messaging-operations-service). Lors de la configuration pour un `Inbox`, ajoutez une entrée à l’aide de la valeur **inbox.path.name**. Lors de la configuration pour un `Outbox`, ajoutez une entrée à l’aide de la valeur de **stitems.path.name**. Lors de la configuration pour `Trash`, ajoutez deux entrées avec les deux valeurs.

#### Onglet Affichage {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Bouton Marquer la lecture**

  Si cette case est cochée, affiche un bouton `Read` permettant de marquer un message comme lu.

* **Bouton Marquer comme non lu**

  Si cette case est cochée, affiche un bouton `Mark Unread` permettant de marquer un message comme lu.

* **Bouton Supprimer**

  Si cette case est cochée, affiche un bouton `Delete` permettant de marquer un message comme lu. Duplique la fonctionnalité de suppression si **`Message Options`** est également coché.

* **Options de message**

  Si cette case est cochée, affiche les boutons **`Reply`**, **`Reply All`**, **`Forward`** et **`Delete`** permettant de renvoyer ou de supprimer un message. Duplique la fonctionnalité de suppression si **`Delete Button`** est également coché.

* **Messages Par Page**

  Le nombre spécifié est le nombre maximal de messages affichés par page dans un modèle de pagination. Si aucun nombre n’est spécifié (laissez le champ vide), tous les messages sont affichés et il n’y a pas de pagination.

* **Modèles d’horodatage**

  Fournir des modèles d’horodatage pour une ou plusieurs langues. La valeur par défaut est en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Afficher l’utilisateur**

  Choisissez **`Sender`** ou **`Recipients`** pour déterminer si l&#39;expéditeur ou les destinataires doivent être affichés.

### Configurer Composer le message {#configure-compose-message}

Pour modifier la configuration de la page de composition de messages, ouvrez le site en [mode d’édition de l’auteur](/help/communities/sites-console.md#authoring-site-content).

* En mode `Preview`, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite le bouton Nouveau message pour pouvoir ouvrir la page `Compose Message`.

* En mode `Edit`, sélectionnez le composant principal sur la page contenant le corps du message.
* Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant l’icône `link`.
Une fois l’héritage annulé, il est possible de sélectionner l’icône de configuration pour ouvrir la boîte de dialogue de configuration.

* Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’icône `broken link`.

![config-composer-message](assets/config-compose-message.png)

#### Onglet Simple {#basic-tab-1}

![basic-tab-composer](assets/basic-tab-compose.png)

* **URL de redirection.**

  Saisissez l&#39;URL de la page affichée après l&#39;envoi du message. Par exemple, `../messaging.html`.

* **Annuler l’URL**

  Saisissez l&#39;URL de la page affichée si l&#39;expéditeur annule le message. Par exemple, `../messaging.html`.

* **Longueur maximale de l’objet du message**

  Nombre maximal de caractères autorisés dans le champ Objet. Par exemple, 500. La valeur par défaut n’est pas limitée.

* **Longueur maximale du corps du message**

  Nombre maximal de caractères autorisés dans le champ Contenu . Par exemple, 10 000. La valeur par défaut n’est pas limitée.

* **Sélecteur de service**

  (*Obligatoire*) Définissez-le sur la valeur de la propriété **`serviceSelector.name`** du [ Service de messagerie AEM Communities ](/help/communities/messaging.md#messaging-operations-service).

#### Onglet Affichage {#display-tab-1}

![display-tab-composer](assets/display-tab-compose.png)

* **Afficher le champ d’objet**

  Si cette case est cochée, affichez le champ `Subject` et activez l’ajout d’un objet au message. La valeur par défaut n’est pas cochée.

* **Libellé du sujet**

  Saisissez le texte que vous souhaitez afficher en regard du champ `Subject`. La valeur par défaut est `Subject`.

* **Afficher le champ de fichier joint**

  Si cette case est cochée, affichez le champ `Attachment` et activez l’ajout de pièces jointes au message. La valeur par défaut n’est pas cochée.

* **Joindre le libellé du fichier**

  Saisissez le texte que vous souhaitez afficher en regard du champ `Attachment`. La valeur par défaut est **`Attach File`**.

* **Afficher le champ de contenu**

  Si cette case est cochée, affichez le champ `Content` et activez l’ajout d’un corps de message. La valeur par défaut n’est pas cochée.

* **Étiquette de contenu**

  Saisissez le texte que vous souhaitez afficher en regard du champ `Content`. La valeur par défaut est **`Body`**.

* **Avec l’éditeur de texte enrichi**

  Si cette case est cochée, elle indique l’utilisation d’une zone de texte de contenu personnalisée avec son propre éditeur de texte enrichi. La valeur par défaut n’est pas cochée.

* **Modèles d’horodatage**

  Fournir des modèles d’horodatage pour une ou plusieurs langues. La valeur par défaut est en, de, fr, it, es, ja, zh_CN, ko_KR.
