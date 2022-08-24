---
title: Fonction de messagerie
seo-title: Messaging Feature
description: Configuration des composants de messagerie
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 13%

---

# Fonction de messagerie {#messaging-feature}

Outre les interactions publiques qui se produisent dans les forums et les commentaires, la fonction de messagerie d’AEM Communities permet aux membres de la communauté d’interagir de manière plus privée.

Cette fonctionnalité peut être incluse lors d’une [site communautaire](/help/communities/overview.md#communitiessites) est créée.

La fonctionnalité de messagerie permet d’effectuer les opérations suivantes :

**A** - envoyer un message à un ou plusieurs membres de la communauté ;

**B** - envoyer des messages directs dans [par lot vers les groupes de membres de la communauté](/help/communities/messaging.md#group-messaging)

**C** - envoyer un message avec des pièces jointes

**D** - transférer un message

**E** - réponse à un message

**F** - supprimer un message

**G** - restaurer un message supprimé

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Pour activer et modifier la fonction de messagerie, voir :

* [Configuration de la messagerie](/help/communities/messaging.md) pour les administrateurs
* [Notions fondamentales sur la messagerie](/help/communities/essentials-messaging.md) pour les développeurs

>[!NOTE]
>
>L’ajout de n’est pas pris en charge. `Compose Message, Message, or Message List` composants (disponibles dans `Communities`groupe de composants) à une page en mode d’édition de création.

## Configuration des composants de messagerie {#configure-messaging-components}

Lorsque la messagerie est activée pour un site de la communauté, elle est configurée sans autre configuration nécessaire. Les informations sont fournies si la configuration par défaut doit être modifiée.

### Configurer la liste des messages (zone de message) {#configure-message-list-message-box}

Modification de la configuration de la liste des messages pour **Boîte de réception**, **Éléments envoyés**, et **Corbeille** des pages de la fonction de messagerie, ouvrez le site dans [mode d’édition de l’auteur](/help/communities/sites-console.md#authoring-site-content).

1. Dans `Preview` , sélectionnez **Messages** pour ouvrir la page principale de messagerie. Sélectionnez ensuite l’une des options suivantes : **Boîte de réception**, **Éléments envoyés** ou **Corbeille** pour configurer le composant pour cette liste de messages.

1. Dans `Edit` , sélectionnez le composant sur la page.
1. Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant le `link` icône .
Une fois l’héritage annulé, il est possible de sélectionner l’icône de configuration pour ouvrir la boîte de dialogue de configuration.

1. Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’option `broken link` icône .

![configure-message-list](assets/configure-message-list.png)

#### Onglet Simple {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Sélecteur de service**

   (*Obligatoire*) Définissez cette variable sur la valeur de la propriété . **`serviceSelector.name`** de la [Service des opérations de messagerie AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Composer la page**

   (*Obligatoire*) La page à ouvrir lorsqu’un membre clique sur le bouton **`Reply`** bouton . La page cible devrait contenir le formulaire **Composer le message.**

* **Réponse/Afficher comme ressource**

   Si cette case est cochée, l’URL de réponse et l’URL de vue font référence à une ressource ; dans le cas contraire, les données sont transmises en tant que paramètres de requête dans l’URL.

* **Formulaire d’affichage de profil**

   Formulaire de profil à utiliser pour afficher le profil des expéditeurs.

* **Dossier de la corbeille**

   Si cette case est cochée, ce composant Liste de messages affiche uniquement les messages marqués comme supprimés (corbeille).

* **Chemins du dossier**

   (*Obligatoire*) en référençant les valeurs définies pour **inbox.path.name** et **stitems.path.name** dans le [Service des opérations de messagerie AEM Communities](/help/communities/messaging.md#messaging-operations-service). Lors de la configuration d’une `Inbox`, ajoutez une entrée à l’aide de la valeur de **inbox.path.name**. Lors de la configuration d’une `Outbox`, ajoutez une entrée à l’aide de la valeur de **stitems.path.name**. Lors de la configuration de pour `Trash`, ajoutez deux entrées avec les deux valeurs.

#### Onglet Affichage {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Bouton Marquer la lecture**

   Si cette case est cochée, une `Read`permettant de marquer un message comme lu.

* **Bouton Marquer comme non lu**

   Si cette case est cochée, une `Mark Unread` permettant de marquer un message comme lu.

* **Bouton Supprimer**

   Si cette case est cochée, une `Delete` permettant de marquer un message comme lu. La fonction de suppression est-elle dupliquée si **`Message Options`** est également cochée.

* **Options de message**

   Si cette case est cochée, s’affiche. **`Reply`**, **`Reply All`**, **`Forward`** et **`Delete`** des boutons permettant de renvoyer ou de supprimer un message. La fonction de suppression est-elle dupliquée si **`Delete Button`** est également cochée.

* **Messages par page**

   Le nombre spécifié est le nombre maximal de messages affichés par page dans un modèle de pagination. Si aucun chiffre n’est spécifié (si vous laissez le champ vide), tous les messages s’affichent sans pagination.

* **Modèles d’horodatage**

   Fournir des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.

* **Afficher l’utilisateur**

   Choisissez l’une **`Sender`** ou **`Recipients`** pour déterminer s&#39;il faut afficher l&#39;expéditeur ou les destinataires.

### Configurer Composer le message {#configure-compose-message}

Pour modifier la configuration de la page de composition de messages, ouvrez le site dans [mode d’édition de l’auteur](/help/communities/sites-console.md#authoring-site-content).

* Dans `Preview` , sélectionnez **Messages** pour ouvrir la page principale de messagerie. Sélectionnez ensuite le bouton Nouveau message pour ouvrir le `Compose Message` page.

* Dans `Edit` , sélectionnez le composant principal sur la page contenant le corps du message.
* Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant le `link` icône .
Une fois l’héritage annulé, il est possible de sélectionner l’icône de configuration pour ouvrir la boîte de dialogue de configuration.

* Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’option `broken link` icône .

![config-composer-message](assets/config-compose-message.png)

#### Onglet Simple {#basic-tab-1}

![basic-tab-composer](assets/basic-tab-compose.png)

* **URL de redirection**

   Saisissez l&#39;URL de la page affichée après l&#39;envoi du message. Par exemple, `../messaging.html`.

* **Annuler l’URL**

   Saisissez l&#39;URL de la page affichée si l&#39;expéditeur annule le message. Par exemple, `../messaging.html`.

* **Longueur maximale de l’objet du message**

   Nombre maximal de caractères autorisés dans le champ Objet. Par exemple, 500. La valeur par défaut n’est pas limitée.

* **Longueur maximale du corps du message**

   Nombre maximal de caractères autorisés dans le champ Contenu . Par exemple, 10000. La valeur par défaut n’est pas limitée.

* **Sélecteur de service**

   (*Obligatoire*) Définissez cette variable sur la valeur de la propriété . **`serviceSelector.name`** de la [Service des opérations de messagerie AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Onglet Affichage {#display-tab-1}

![display-tab-composer](assets/display-tab-compose.png)

* **Afficher le champ d’objet**

   Si cette case est cochée, le `Subject` et activer l’ajout d’un objet au message. Cette option n’est pas cochée par défaut.

* **Libellé du sujet**

   Saisissez le texte à afficher en regard de l’option `Subject` champ . La valeur par défaut est `Subject`.

* **Afficher le champ Pièce jointe**

   Si cette case est cochée, le `Attachment` et activer l’ajout de pièces jointes au message. Cette option n’est pas cochée par défaut.

* **Libellé de la pièce jointe**

   Saisissez le texte à afficher en regard de l’option `Attachment` champ . La valeur par défaut est **`Attach File`**.

* **Afficher le champ de contenu**

   Si cette case est cochée, le `Content` et activer l’ajout d’un corps de message. Cette option n’est pas cochée par défaut.

* **Libellé de contenu**

   Saisissez le texte à afficher en regard de l’option `Content` champ . La valeur par défaut est **`Body`**.

* **Avec l’éditeur de texte enrichi**

   Si cette case est cochée, elle indique l’utilisation d’une zone de texte de contenu personnalisée avec son propre éditeur de texte enrichi. Cette option n’est pas cochée par défaut.

* **Modèles d’horodatage**

   Fournir des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.
