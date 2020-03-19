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
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Fonction de messagerie {#messaging-feature}

Outre les interactions visibles publiquement qui se produisent dans les forums et les commentaires, la fonction de messagerie des communautés AEM permet aux membres de la communauté d’interagir de manière plus privée.

This feature can be included when a [community site](/help/communities/overview.md#communitiessites) is created.

La fonction de messagerie permet d’effectuer les opérations suivantes :

**A** - envoyer un message à un ou plusieurs membres **B** de la communauté - envoyer des messages directs en [masse aux groupes](/help/communities/messaging.md#group-messaging)membres de la communauté C **C** - envoyer un message avec des pièces jointesD - faire suivre un messageE - répondre à un messageF - supprimer un messageG - restaurer un message supprimé&#x200B;****************

![message-section](assets/messaging-section.png) de message- ![restauration-message](assets/restore-message.png)

Pour activer et modifier la fonction de messagerie, voir :

* [Configuration de la messagerie](/help/communities/messaging.md) pour les administrateurs
* [Messaging Essentials](/help/communities/essentials-messaging.md) pour les développeurs

>[!NOTE]
>
>Il n’est pas pris en charge d’ajouter `Compose Message, Message, or Message List` des composants (trouvés dans le groupe de `Communities`composants) à une page en mode d’édition Auteur.

## Configuration des composants de messagerie {#configure-messaging-components}

Lorsque la messagerie est activée pour un site communautaire, elle est configurée sans autre configuration nécessaire. Les informations sont fournies s’il est nécessaire de modifier la configuration par défaut.

### Configuration du  de message (boîte de message) {#configure-message-list-message-box}

Pour modifier la configuration du de messages pour la **boîte** de réception, les éléments **envoyés et les pages** de corbeille **de la fonction de messagerie, ouvrez le site en mode d’édition de l’** [auteur.](/help/communities/sites-console.md#authoring-site-content)

1. En `Preview`mode, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite **Boîte** de réception **, Éléments** envoyés ou **Corbeille** pour configurer le composant pour ce de messages.

1. En `Edit` mode, sélectionnez le composant sur la page.
1. Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant l’ `link`icône.
Une fois l’héritage annulé, il est possible de sélectionner l’icône Configurer pour ouvrir la boîte de dialogue de configuration.

1. Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’ `broken link` icône.

![configure-message-](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Sélecteur de service**

   (*Required*) Set this to the value of the property **`serviceSelector.name`** from the [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **Composer la page**

   (*Obligatoire*) Page à ouvrir lorsqu’un membre clique sur le **`Reply`** bouton. La page cible devrait contenir le formulaire **Composer le message.**

* **Répondre/comme ressource**

   Si cette option est cochée, l’URL de réponse et l’URL de  de réponse font référence à une ressource. Dans le cas contraire, les données sont transmises sous la forme de paramètres de dans l’URL.

* **Formulaire d’affichage de**

   Formulaire  à utiliser pour afficher le des expéditeurs.

* **Dossier Corbeille**

   Si cette option est cochée, ce composant  message affiche uniquement les messages marqués comme supprimés (corbeille).

* **Chemins du dossier**

   (*Obligatoire*) Référence aux valeurs définies pour **inbox.path.name** et **stitems.path.name** dans le service de messagerie des communautés [AEM. ](/help/communities/messaging.md#messaging-operations-service) Lors de la configuration pour une `Inbox`, ajoutez une entrée à l’aide de la valeur de **inbox.path.name**. Lors de la configuration d’une `Outbox`, ajoutez une entrée à l’aide de la valeur de **stitems.path.name**. Lors de la configuration pour `Trash`, ajoutez deux entrées avec les deux valeurs.

#### Onglet Affichage {#display-tab}

![display-tab-message-](assets/display-tab-message-list.png)

* **Bouton Marquer la lecture**

   If checked, displays a `Read`button allowing a message to be marked as read.

* **Bouton Marquer comme non lu**

   If checked, displays a `Mark Unread` button allowing a message to be marked as read.

* **Bouton Supprimer**

   If checked, displays a `Delete`button allowing a message to be marked as read. Will duplicate the delete functionality if **`Message Options`** is also checked.

* **Options de message**

   Si cette option est cochée, affiche **`Reply`**, **`Reply All`**, **`Forward`** **`Delete`** et des boutons permettant de renvoyer ou de supprimer un message. Will duplicate the delete functionality if **`Delete Button`** is also checked.

* **Messages par page**

   Le nombre spécifié correspond au nombre maximal de messages affichés par page dans un schéma de pagination. Si aucun chiffre n’est spécifié (si vous laissez le champ vide), tous les messages s’affichent sans pagination.

* **Modèles d’horodatage**

   Fournissez des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.

* **Afficher l’utilisateur**

   Choisissez l’un **`Sender`** ou **`Recipients`** l’autre pour déterminer s’il faut afficher l’expéditeur ou les.

### Configurer le message de composition {#configure-compose-message}

Pour modifier la configuration de la page de composition des messages, ouvrez le site en mode [d’édition de l’](/help/communities/sites-console.md#authoring-site-content)auteur.

* En `Preview` mode, sélectionnez le lien **Messages** pour ouvrir la page de messagerie principale. Sélectionnez ensuite le bouton Nouveau message pour ouvrir la `Compose Message` page.

* En `Edit` mode, sélectionnez le composant principal sur la page contenant le corps du message.
* Pour accéder à la boîte de dialogue de configuration, annulez l’héritage en sélectionnant l’ `link` icône.
Une fois l’héritage annulé, il est possible de sélectionner l’icône Configurer pour ouvrir la boîte de dialogue de configuration.

* Une fois la configuration terminée, il est nécessaire de restaurer l’héritage en sélectionnant l’ `broken link` icône.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL de redirection**

   Entrez l’URL de la page affichée après l’envoi du message. Par exemple, `../messaging.html`.

* **Annuler l’URL**

   Entrez l’URL de la page affichée si l’expéditeur annule le message. Par exemple, `../messaging.html`.

* **Longueur maximale de l’objet du message**

   Nombre maximal de caractères autorisés dans le champ Objet. Par exemple, 500. La valeur par défaut n’est pas une limite.

* **Longueur maximale du corps du message**

   Nombre maximal de caractères autorisés dans le champ Contenu. Par exemple, 10000. La valeur par défaut n’est pas une limite.

* **Sélecteur de service**

   (*Required*) Set this to the value of the property **`serviceSelector.name`** from the [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### Onglet Affichage {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Afficher le champ Objet**

   Si cette option est cochée, affichez le `Subject` champ et activez l’ajout d’un objet au message. Cette option n’est pas cochée par défaut.

* **Étiquette du sujet**

   Entrez le texte à afficher en regard du `Subject` champ. La valeur par défaut est `Subject`.

* **Afficher le champ Pièce jointe**

   Si cette option est cochée, affichez le `Attachment` champ et activez l’ajout de pièces jointes au message. Cette option n’est pas cochée par défaut.

* **Libellé de la pièce jointe**

   Entrez le texte à afficher en regard du `Attachment` champ. La valeur par défaut est **`Attach File`**.

* **Afficher le champ de contenu**

   Si cette option est cochée, affichez le `Content` champ et activez l’ajout d’un corps de message. Cette option n’est pas cochée par défaut.

* **Libellé de contenu**

   Entrez le texte à afficher en regard du `Content` champ. La valeur par défaut est **`Body`**.

* **Avec l’éditeur de texte enrichi**

   Si cette option est cochée, cela signifie l’utilisation d’une zone de texte Contenu personnalisée avec son propre éditeur de texte enrichi. Cette option n’est pas cochée par défaut.

* **Modèles d’horodatage**

   Fournissez des modèles d’horodatage pour une ou plusieurs langues. Des valeurs sont fournies par défaut pour en, de, fr, it, es, ja, zh_CN et ko_KR.

