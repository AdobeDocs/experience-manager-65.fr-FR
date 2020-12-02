---
title: Fonction de messagerie
seo-title: Fonction de messagerie
description: Configuration des composants de messagerie
seo-description: Configuration des composants de messagerie
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 13%

---


# Fonction de messagerie {#messaging-feature}

Outre les interactions visibles par le public qui se produisent dans les forums et les commentaires, la fonction de messagerie d&#39;AEM Communities permet aux membres de la communauté d&#39;interagir entre eux de manière plus privée.

Cette fonctionnalité peut être incluse lors de la création d&#39;un [site communautaire](/help/communities/overview.md#communitiessites).

La fonction de messagerie permet de :

**A** - envoyer un message à un ou plusieurs membres de la communauté

**B** - envoyer des messages directs en  [vrac aux groupes de membres de la communauté](/help/communities/messaging.md#group-messaging)

**C** - envoyer un message avec des pièces jointes

**D** - transférer un message

**E** - répondre à un message

**F** - supprimer un message

**G** - restaurer un message supprimé

![section de messagerie](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Pour activer et modifier la fonction de messagerie, voir :

* [Configuration de ](/help/communities/messaging.md) la messagerie pour les administrateurs
* [Messaging ](/help/communities/essentials-messaging.md) Essentials pour les développeurs

>[!NOTE]
>
>Il n&#39;est pas pris en charge d&#39;ajouter des composants `Compose Message, Message, or Message List` (trouvés dans le `Communities`groupe de composants) à une page en mode d&#39;édition Auteur.

## Configurer les composants de messagerie {#configure-messaging-components}

Lorsque la messagerie est activée pour un site communautaire, elle est configurée sans autre configuration nécessaire. Les informations sont fournies s’il est nécessaire de modifier la configuration par défaut.

### Configurer la Liste de message (boîte de message) {#configure-message-list-message-box}

Pour modifier la configuration de la liste des messages pour les pages **Boîte de réception**, **Éléments envoyés** et **Corbeille** de la fonction de messagerie, ouvrez le site en [mode de modification de l&#39;auteur](/help/communities/sites-console.md#authoring-site-content).

1. En mode `Preview`, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite **Boîte de réception**, **Éléments envoyés** ou **Corbeille** pour configurer le composant pour cette liste de messages.

1. En mode `Edit`, sélectionnez le composant sur la page.
1. Pour accéder à la boîte de dialogue de configuration, annulez l&#39;héritage en sélectionnant l&#39;icône `link`.
Une fois l&#39;héritage annulé, il est possible de sélectionner l&#39;icône de configuration pour ouvrir la boîte de dialogue de configuration.

1. Une fois la configuration terminée, il est nécessaire de restaurer l&#39;héritage en sélectionnant l&#39;icône `broken link`.

![configure-message-liste](assets/configure-message-list.png)

#### Onglet de base {#basic-tab}

![tableau de base-tabulation-messagelist](assets/basic-tab-messagelist.png)

* **Sélecteur de service**

   (*Obligatoire*) Définissez cette valeur sur la valeur de la propriété **`serviceSelector.name`** du [Service d&#39;opérations de messagerie AEM Communities ](/help/communities/messaging.md#messaging-operations-service).

* **Composer la page**

   (*Obligatoire*) Page à ouvrir lorsqu&#39;un membre clique sur le bouton **`Reply`**. La page cible devrait contenir le formulaire **Composer le message.**

* **Réponse/Vue en tant que ressource**

   Si cette option est cochée, l’URL de réponse et l’URL de Vue font référence à une ressource ; dans le cas contraire, les données sont transmises en tant que paramètres de requête dans l’URL.

* **Formulaire d&#39;affichage de profil**

   Profil à utiliser pour afficher le profil des expéditeurs.

* **Dossier Corbeille**

   Si cette case est cochée, ce composant de Liste de messages affiche uniquement les messages marqués comme supprimés (corbeille).

* **Chemins des dossiers**

   (*Obligatoire*) Référence aux valeurs définies pour **inbox.path.name** et **stitems.path.name** dans le [service d&#39;opérations de messagerie AEM Communities ](/help/communities/messaging.md#messaging-operations-service). Lors de la configuration pour un `Inbox`, ajoutez une entrée en utilisant la valeur **inbox.path.name**. Lors de la configuration pour un `Outbox`, ajoutez une entrée en utilisant la valeur **stitems.path.name**. Lors de la configuration de `Trash`, ajoutez deux entrées avec les deux valeurs.

#### Onglet Affichage {#display-tab}

![display-tab-message-liste](assets/display-tab-message-list.png)

* **Bouton Marquer la lecture**

   Si cette case est cochée, affiche un bouton `Read`permettant de marquer un message comme lu.

* **Bouton Marquer comme non lu**

   Si cette case est cochée, affiche un bouton `Mark Unread` permettant de marquer un message comme lu.

* **Bouton Supprimer**

   Si cette case est cochée, affiche un bouton `Delete` permettant de marquer un message comme lu. Duplicata la fonctionnalité de suppression si **`Message Options`** est également coché.

* **Options de message**

   Si cette case est cochée, affiche les boutons **`Reply`**, **`Reply All`**, **`Forward`** et **`Delete`** permettant de renvoyer ou de supprimer un message. Duplicata la fonctionnalité de suppression si **`Delete Button`** est également coché.

* **Messages par page**

   Le nombre spécifié correspond au nombre maximal de messages affichés par page dans un schéma de pagination. Si aucun chiffre n’est spécifié (si vous laissez le champ vide), tous les messages s’affichent sans pagination.

* **Modèles d’horodatage**

   Fournissez des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.

* **Afficher l’utilisateur**

   Choisissez **`Sender`** ou **`Recipients`** pour déterminer si l&#39;expéditeur ou les Destinataires doivent s&#39;afficher.

### Configurer le message de composition {#configure-compose-message}

Pour modifier la configuration de la page de composition du message, ouvrez le site en [mode d’édition de l’auteur](/help/communities/sites-console.md#authoring-site-content).

* En mode `Preview`, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite le bouton Nouveau message pour ouvrir la page `Compose Message`.

* En mode `Edit`, sélectionnez le composant principal sur la page contenant le corps du message.
* Pour accéder à la boîte de dialogue de configuration, annulez l&#39;héritage en sélectionnant l&#39;icône `link`.
Une fois l&#39;héritage annulé, il est possible de sélectionner l&#39;icône de configuration pour ouvrir la boîte de dialogue de configuration.

* Une fois la configuration terminée, il est nécessaire de restaurer l&#39;héritage en sélectionnant l&#39;icône `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### Onglet de base {#basic-tab-1}

![simple-tabulation-composition](assets/basic-tab-compose.png)

* **URL de redirection**

   Entrez l&#39;URL de la page affichée après l&#39;envoi du message. Par exemple, `../messaging.html`.

* **Annuler l’URL**

   Entrez l&#39;URL de la page affichée si l&#39;expéditeur annule le message. Par exemple, `../messaging.html`.

* **Longueur maximale de l’objet du message**

   Nombre maximal de caractères autorisés dans le champ Objet. Par exemple, 500. La valeur par défaut n’est pas une limite.

* **Longueur maximale du corps du message**

   Nombre maximal de caractères autorisés dans le champ Contenu. Par exemple, 10000. La valeur par défaut n’est pas une limite.

* **Sélecteur de service**

   (*Obligatoire*) Définissez cette valeur sur la valeur de la propriété **`serviceSelector.name`** du [Service d&#39;opérations de messagerie AEM Communities ](/help/communities/messaging.md#messaging-operations-service).

#### Onglet Affichage {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Afficher le champ Objet**

   Si cette case est cochée, affichez le champ `Subject` et activez l&#39;ajout d&#39;un objet au message. Cette option n’est pas cochée par défaut.

* **Étiquette de sujet**

   Entrez le texte à afficher en regard du champ `Subject`. La valeur par défaut est `Subject`.

* **Afficher le champ Pièce jointe**

   Si cette case est cochée, affichez le champ `Attachment` et activez l&#39;ajout de pièces jointes au message. Cette option n’est pas cochée par défaut.

* **Libellé de la pièce jointe**

   Entrez le texte à afficher en regard du champ `Attachment`. La valeur par défaut est **`Attach File`**.

* **Afficher le champ de contenu**

   Si cette case est cochée, affichez le champ `Content` et activez l’ajout d’un corps de message. Cette option n’est pas cochée par défaut.

* **Libellé du contenu**

   Entrez le texte à afficher en regard du champ `Content`. La valeur par défaut est **`Body`**.

* **Avec l’éditeur de texte enrichi**

   Si cette option est cochée, indique l’utilisation d’une zone de texte Contenu personnalisée avec son propre éditeur de texte enrichi. Cette option n’est pas cochée par défaut.

* **Modèles d’horodatage**

   Fournissez des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.

