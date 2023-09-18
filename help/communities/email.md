---
title: Configuration du courrier électronique
description: Configuration des emails pour Communities
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 6%

---

# Configuration du courrier électronique {#configuring-email}

AEM Communities utilise le courrier électronique pour :

* [Notifications de communautés](notifications.md)
* [Abonnements des communautés](subscriptions.md)

Par défaut, la fonctionnalité de courrier électronique n’est pas fonctionnelle, car elle nécessite la spécification d’un serveur SMTP et d’un utilisateur SMTP.

>[!CAUTION]
>
>Les emails de notifications et d’abonnements ne doivent être configurés que sur la variable [éditeur principal](deploy-communities.md#primary-publisher).

## Configuration du service de messagerie par défaut {#default-mail-service-configuration}

Le service de messagerie par défaut est requis pour les notifications et les abonnements.

* Connectez-vous à l’éditeur principal avec les privilèges d’administrateur et accédez au [Console web](../../help/sites-deploying/configuring-osgi.md):

   * Par exemple : [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Recherchez la variable `Day CQ Mail Service`.
* Sélectionnez l’icône de modification.

Reposez-vous sur la documentation de [Configuration des notifications par e-mail](../../help/sites-administering/notification.md), mais avec une différence dans ce champ `"From" address` is *not* obligatoire et doit être laissé vide.

Par exemple (renseigné avec des valeurs à des fins d’illustration uniquement) :

![email-config](assets/email-config.png)

* **[!UICONTROL Nom d’hôte du serveur SMTP]**

  *(Obligatoire)* Le serveur SMTP à utiliser.

* **[!UICONTROL Port du serveur SMTP]**

  *(Obligatoire)* Le port du serveur SMTP doit être 25 ou supérieur.

* **[!UICONTROL Utilisateur SMTP]**

  *(Obligatoire)* Utilisateur SMTP.

* **[!UICONTROL Mot de passe SMTP]**

  *(Obligatoire)* Mot de passe de l’utilisateur SMTP.

* **[!UICONTROL Adresse &quot;De&quot;]**

  Laissez vide
* **[!UICONTROL SMTP use SSL]**

  Si cette case est cochée, un e-mail sécurisé est envoyé. Vérifiez que le port est défini sur 465 ou selon les besoins pour un serveur SMTP.
* **[!UICONTROL Debug email]**

  Si cette case est cochée, la journalisation des interactions serveur SMTP est activée.

## Configuration des emails AEM Communities {#aem-communities-email-configuration}

Une fois que la variable [service de messagerie par défaut](#default-mail-service-configuration) est configuré, les deux instances existantes de la fonction `AEM Communities Email Reply Configuration` La configuration OSGi, incluse dans la version, devient fonctionnelle.

Seule l&#39;instance pour les abonnements doit être paramétrée lors de l&#39;autorisation de la réponse par email.

1. [Email](#configuration-for-notifications) instance :

   Pour les notifications, qui ne prennent pas en charge les messages de réponse, et qui ne doivent pas être modifiées.

1. [Abonnements-email](#configuration-for-subscriptions) instance :

   Nécessite une configuration pour activer entièrement la création d’une publication à partir d’un courrier électronique de réponse.

Pour accéder aux instances de configuration des emails des communautés :

* Connectez-vous à l’éditeur principal avec les privilèges d’administrateur et accédez au [Console web](../../help/sites-deploying/configuring-osgi.md)

   * Par exemple : [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localiser `AEM Communities Email Reply Configuration`.

![email-response-config](assets/email-reply-config.png)

### Configuration des notifications {#configuration-for-notifications}

L’instance de `AEM Communities Email Reply Configuration` La configuration OSGi avec l’e-mail de nom est la fonctionnalité de notifications immédiates. Cette fonctionnalité n’inclut pas la réponse par courrier électronique.

Ne modifiez pas cette configuration.

* Recherchez la variable `AEM Communities Email Reply Configuration`.
* Sélectionnez l’icône de modification.
* Vérifiez que la variable **Nom** is `email`.

* Vérifiez que **Créer une publication à partir d’un courrier électronique de réponse** is `unchecked`.

![configure-email-response](assets/configure-email-reply.png)

### Configuration pour les abonnements {#configuration-for-subscriptions}

Pour les abonnements Communities, il est possible d’activer ou de désactiver la possibilité pour un membre de publier du contenu en répondant à un email.

* Recherchez la variable `AEM Communities Email Reply Configuration`.
* Sélectionnez l’icône de modification.
* Vérifiez que la variable **Nom** is `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nom]**

  *(Obligatoire)* `subscriptions-email`. Ne Pas Modifier.

* **[!UICONTROL Créer une publication à partir d’un courrier électronique de réponse]**

  Si cette case est cochée, le destinataire d’un email d’abonnement peut publier du contenu en envoyant une réponse. La valeur par défaut est cochée.
* **[!UICONTROL Ajout d’un ID suivi à l’en-tête]**

  La valeur par défaut est `Reply-To`.

* **[!UICONTROL Longueur maximale de l’objet]**

  Si l’identifiant de suivi est ajouté à l’objet, il s’agit de la longueur maximale de l’objet, à l’exception de l’identifiant suivi, après lequel il est rogné. Cela doit être aussi petit que possible pour éviter la perte des informations d’ID trackées. La valeur par défaut est 200.

* **[!UICONTROL Adresse électronique &quot;Réponse&quot;]**

  Adresse électronique utilisée comme adresse de réponse. La valeur par défaut est `no-reply@example.com`.

* **[!UICONTROL Réponse au délimiteur]**

  Si l’ID de suivi est ajouté à l’en-tête de réponse, ce délimiteur est utilisé. Par défaut : `+` (signe plus).

* **[!UICONTROL Préfixe d’ID de suivi dans l’objet]**

  Si l’identifiant de suivi est ajouté à l’objet, ce préfixe est utilisé. La valeur par défaut est `post#`.

* **[!UICONTROL Préfixe d’ID de suivi dans le corps du message]**

  Si l’identifiant de suivi est ajouté au corps du message, ce préfixe est utilisé. La valeur par défaut est `Please do not remove this:`.

* **[!UICONTROL Email en tant que HTML]**: si cette case est cochée, le type de contenu de l’email est défini comme `"text/html;charset=utf-8"`. La valeur par défaut est cochée.

* **[!UICONTROL Nom d’utilisateur par défaut]**

  Ce nom n’est utilisé pour aucun utilisateur de nom. La valeur par défaut est `no-reply@example.com`.

* **[!UICONTROL Chemin d’accès racine des modèles]**

  L’email est créé à l’aide d’un modèle stocké dans ce chemin racine. La valeur par défaut est `/etc/community/templates/subscriptions-email`.

## Configuration de l’importateur d’interrogations {#configure-polling-importer}

Pour que le courrier électronique soit importé dans le référentiel, il est nécessaire de configurer un importateur d’interrogations et de configurer ses propriétés manuellement dans le référentiel.

### Ajouter un nouvel importateur d’interrogations {#add-new-polling-importer}

* Connectez-vous à l’éditeur principal avec les privilèges d’administrateur et accédez à la console de l’importateur d’interrogations :

  Par exemple : [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Sélectionnez **[!UICONTROL Ajouter]**

  ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL Type]**

  *(Obligatoire)* Menu déroulant à sélectionner `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obligatoire)* Le serveur de mail sortant. Par exemple, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importer dans le chemin]**&amp;ast;

  *(Obligatoire)* Définissez sur . `/content/usergenerated/mailFolder/postEmails`
en accédant à la `postEmails`et sélectionnez **OK**.

* **[!UICONTROL Intervalle de mise à jour en secondes]**

  *(Facultatif)* Le serveur de messagerie configuré pour le service de messagerie par défaut peut avoir des exigences concernant la valeur de l’intervalle de mise à jour. Par exemple, Gmail peut nécessiter un intervalle de `300`.

* **[!UICONTROL Connexion]**

  *(Facultatif)*

* **[!UICONTROL Password]**

  *(Facultatif)*

* Sélectionnez **[!UICONTROL OK]**.

### Ajuster le protocole pour le nouvel importateur d’interrogations {#adjust-protocol-for-new-polling-importer}

Une fois la nouvelle configuration d’interrogation enregistrée, il est nécessaire de modifier davantage les propriétés de l’importateur d’emails d’abonnement pour modifier le protocole de `POP3` to `emailreply`.

Utilisation [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Connectez-vous à l’éditeur principal avec les privilèges d’administrateur et accédez à [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importateurs/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Sélectionnez la configuration nouvellement créée et modifiez les propriétés suivantes :

   * **feedType**: Remplacer `pop3s` avec **`emailreply`**
   * **source**: remplacer le protocole de la source `pop3s://` avec **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

Les triangles rouges indiquent les propriétés modifiées. Veillez à enregistrer les modifications :

* Sélectionnez **[!UICONTROL Enregistrer tout]**.
