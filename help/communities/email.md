---
title: Configuration du courrier électronique
seo-title: Configuration du courrier électronique
description: Configuration des emails pour Communities
seo-description: Configuration des emails pour Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Administrator
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 7%

---

# Configuration de l’adresse électronique {#configuring-email}

AEM Communities utilise le courrier électronique pour :

* [Notifications de communautés](notifications.md)
* [Abonnements des communautés](subscriptions.md)

Par défaut, la fonctionnalité de courrier électronique n’est pas fonctionnelle, car elle nécessite la spécification d’un serveur SMTP et d’un utilisateur SMTP.

>[!CAUTION]
>
>Les emails pour les notifications et les abonnements ne doivent être configurés que sur l’[Principal éditeur](deploy-communities.md#primary-publisher).

## Configuration du service de messagerie par défaut {#default-mail-service-configuration}

Le service de messagerie par défaut est requis pour les notifications et les abonnements.

* Connectez-vous à l’éditeur Principal avec les privilèges d’administrateur et accédez à la [console web](../../help/sites-deploying/configuring-osgi.md) :

   * Par exemple, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Recherchez le `Day CQ Mail Service`.
* Sélectionnez l’icône de modification.

Cela est basé sur la documentation de [Configuration de la notification électronique](../../help/sites-administering/notification.md), mais avec une différence dans le fait que le champ `"From" address` n’est pas *obligatoire et doit être laissé vide.*

Par exemple (renseigné avec des valeurs à des fins d’illustration uniquement) :

![email-config](assets/email-config.png)

* **[!UICONTROL Nom d’hôte du serveur SMTP]**

   *(Obligatoire)* Serveur SMTP à utiliser.

* **[!UICONTROL Port du serveur SMTP]**

   *(Obligatoire)* Le port du serveur SMTP doit être supérieur ou égal à 25.

* **[!UICONTROL Utilisateur SMTP]**

   *(Obligatoire)* Utilisateur SMTP.

* **[!UICONTROL Mot de passe SMTP]**

   *(Obligatoire)* Mot de passe de l’utilisateur SMTP.

* **[!UICONTROL Adresse &quot;De&quot;]**

   Laissez vide
* **[!UICONTROL SMTP use SSL]**

   Si cette case est cochée, un courrier électronique sécurisé est envoyé. Assurez-vous que le port est défini sur 465 ou selon les besoins pour le serveur SMTP.
* **[!UICONTROL Debug email]**

   Si cette case est cochée, la journalisation des interactions serveur SMTP est activée.

## Configuration des emails AEM Communities {#aem-communities-email-configuration}

Une fois le [service de messagerie par défaut](#default-mail-service-configuration) configuré, les deux instances existantes de la configuration OSGi `AEM Communities Email Reply Configuration`, incluses dans la version, deviennent fonctionnelles.

Seule l&#39;instance pour les abonnements doit être paramétrée plus précisément lors de l&#39;autorisation de la réponse par email.

1. [](#configuration-for-notifications) EmailInstance :

   Pour les notifications, qui ne prennent pas en charge les messages de réponse, et ne doivent pas être modifiées.

1. [Subscriptions-](#configuration-for-subscriptions) emailInstance :

   Nécessite une configuration pour activer entièrement la création d’une publication à partir d’un courrier électronique de réponse.

Pour accéder aux instances de configuration des emails des communautés :

* Connectez-vous à l’éditeur Principal avec les privilèges d’administrateur et accédez à la [console web](../../help/sites-deploying/configuring-osgi.md)

   * Par exemple, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Recherchez `AEM Communities Email Reply Configuration`.

![email-response-config](assets/email-reply-config.png)

### Configuration des notifications {#configuration-for-notifications}

L’instance de `AEM Communities Email Reply Configuration` configuration OSGi avec l’adresse électronique Nom est une fonction de aussitôt. Cette fonctionnalité n’inclut pas la réponse par courrier électronique.

Cette configuration ne doit pas être modifiée.

* Recherchez le `AEM Communities Email Reply Configuration`.
* Sélectionnez l’icône de modification.
* Vérifiez que le **nom** est `email`.

* Vérifiez que **La création d’une publication à partir du courrier électronique de réponse** est `unchecked`.

![configure-email-response](assets/configure-email-reply.png)

### Configuration pour les abonnements {#configuration-for-subscriptions}

Pour les abonnements Communities, il est possible d’activer ou de désactiver la possibilité pour un membre de publier du contenu en répondant à un email.

* Recherchez le `AEM Communities Email Reply Configuration`.
* Sélectionnez l’icône de modification.
* Vérifiez que le **nom** est `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Name]** (Nom)

   *(Obligatoire)* `subscriptions-email`. Ne Pas Modifier.

* **[!UICONTROL Créer une publication à partir d’un courrier électronique de réponse]**

   Si cette case est cochée, le destinataire de l’email d’abonnement peut publier du contenu en envoyant une réponse. Cette option est cochée par défaut.
* **[!UICONTROL Ajout d’un ID suivi à l’en-tête]**

   La valeur par défaut est `Reply-To`.

* **[!UICONTROL Longueur maximale de l’objet]**

   Si l’identifiant de suivi est ajouté à l’objet, il s’agit de la longueur maximale de l’objet, à l’exception de l’identifiant suivi, après lequel il sera rogné. Notez que cette valeur doit être aussi petite que possible pour éviter que les informations d’ID trackées ne soient perdues. La valeur par défaut est 200.

* **[!UICONTROL Adresse électronique &quot;Réponse&quot;]**

   Adresse électronique utilisée comme adresse de réponse. La valeur par défaut est `no-reply@example.com`.

* **[!UICONTROL Réponse au délimiteur]**

   Si l’ID de suivi est ajouté à l’en-tête de réponse, ce délimiteur est utilisé. La valeur par défaut est `+` (signe plus).

* **[!UICONTROL Préfixe d’ID de suivi dans l’objet]**

   Si l’identifiant de suivi est ajouté à l’objet, ce préfixe est utilisé. La valeur par défaut est `post#`.

* **[!UICONTROL Préfixe d’ID de suivi dans le corps du message]**

   Si l’identifiant de suivi est ajouté au corps du message, ce préfixe sera utilisé. La valeur par défaut est `Please do not remove this:`.

* **[!UICONTROL Email au format HTML]** : Si cette case est cochée, le type de contenu de l’email est défini sur  `"text/html;charset=utf-8"`. Cette option est cochée par défaut.

* **[!UICONTROL Nom d’utilisateur par défaut]**

   Ce nom ne sera utilisé pour aucun nom d’utilisateur. La valeur par défaut est `no-reply@example.com`.

* **[!UICONTROL Chemin d’accès racine des modèles]**

   Le message électronique est créé en utilisant un modèle stocké à cet emplacement racine. La valeur par défaut est `/etc/community/templates/subscriptions-email`.

## Configurer l’importateur d’interrogations {#configure-polling-importer}

Pour que le courrier électronique soit importé dans le référentiel, il est nécessaire de configurer un importateur d’interrogations et de configurer ses propriétés manuellement dans le référentiel.

### Ajouter un nouvel importateur d’interrogations {#add-new-polling-importer}

* Connectez-vous à l’éditeur Principal avec les privilèges d’administrateur et accédez à la console de l’importateur d’interrogations :

   Par exemple, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Sélectionnez **[!UICONTROL Ajouter]**

   ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL Type]**

   *(Obligatoire)* Faites glisser le curseur pour sélectionner  `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(Obligatoire)* Serveur de messagerie sortant. Par exemple, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importer dans Path]**&amp;ast;

   *(Obligatoire)* Définissez cette variable sur  `/content/usergenerated/mailFolder/postEmails`
en accédant au  `postEmails`dossier et en sélectionnant  **OK**.

* **[!UICONTROL Intervalle de mise à jour en secondes]**

   *(Facultatif)* Le serveur de messagerie configuré pour le service de messagerie par défaut peut avoir des exigences concernant la valeur de l’intervalle de mise à jour. Par exemple, Gmail peut nécessiter un intervalle `300`.

* **[!UICONTROL Connexion]**

   *(Facultatif)*

* **[!UICONTROL Mot de passe]**

   *(Facultatif)*

* **[!UICONTROL Cliquez sur OK]**.

### Ajuster le protocole pour le nouvel importateur d’interrogations {#adjust-protocol-for-new-polling-importer}

Une fois la nouvelle configuration d’interrogation enregistrée, il est nécessaire de modifier davantage les propriétés de l’importateur d’emails d’abonnement afin de modifier le protocole de `POP3` en `emailreply`.

Utilisation de [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) :

* Connectez-vous à l’éditeur Principal avec les privilèges d’administrateur et accédez à [https://&lt;serveur>:&lt;port>/crx/de/index.jsp#/etc/importateurs/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Sélectionnez la configuration nouvellement créée et modifiez les propriétés suivantes :

   * **feedType** : Remplacer  `pop3s` par  **`emailreply`**
   * **source** : Remplacer le protocole de la source  `pop3s://` par  **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

Les triangles rouges indiquent les propriétés modifiées. Veillez à enregistrer les modifications :

* Sélectionnez **[!UICONTROL Enregistrer tout]**.
