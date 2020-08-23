---
title: Configuration des notifications électroniques
seo-title: Configuration des notifications électroniques
description: Découvrez comment configurer les notifications électroniques dans AEM.
seo-description: Découvrez comment configurer les notifications électroniques dans AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 77%

---


# Configuration des notifications électroniques{#configuring-email-notification}

AEM envoie des notifications aux utilisateurs qui :

* Ont souscrit aux événements de pages, par exemple la modification ou la réplication. La section [Boîte de réception de notifications](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) décrit comment s’abonner à ces événements.

* Ont souscrit aux événements de forums.
* Doivent effectuer une opération dans un workflow. La section [Étape du participant](/help/sites-developing/workflows-step-ref.md#participant-step) décrit comment déclencher la notification électronique dans un workflow.

Conditions préalables :

* L’utilisateur doit disposer d’une adresse électronique valide définie dans son profil.
* The **Day CQ Mail Service** needs to be properly configured.

Lorsque l’utilisateur est averti, il reçoit un courrier électronique dans la langue définie dans son profil. Chaque langue possède son propre modèle, qui peut être personnalisé. De nouveaux modèles de courrier électronique peuvent être ajoutés pour de nouvelles langues.

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

## Configuration du service de messagerie {#configuring-the-mail-service}

Pour qu’AEM puisse envoyer des courriers électroniques, le **service de messagerie Day CQ** doit être correctement configuré. Vous pouvez afficher la configuration dans la console Web. Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

Les contraintes suivantes s’appliquent :

* Le **port de serveur SMTP** doit être le port 25 ou supérieur.

* The **SMTP server host name** must not be blank.
* L’**adresse « De »** ne doit pas être vide.

Pour résoudre plus facilement un problème avec le **service de messagerie Day CQ**, vous pouvez examiner les journaux du service :

`com.day.cq.mailer.DefaultMailService`

La configuration ressemble à ce qui suit dans la console Web :

![chlimage_1-276](assets/chlimage_1-276.png)

## Configuration du canal de notification électronique {#configuring-the-email-notification-channel}

Lorsque vous vous abonnez à des notifications d’événement de page ou de forum, l’adresse électronique De est définie sur `no-reply@acme.com` par défaut. Vous pouvez modifier cette valeur en configurant le service **Notification par courrier électronique** dans la console Web.

Pour configurer l’adresse électronique De, ajoutez un nœud `sling:OsgiConfig` au référentiel. Procédez comme suit pour ajouter le nœud directement avec CRXDE Lite :

1. Dans CRXDE Lite, ajoutez un dossier nommé `config` sous votre dossier d’application.
1. Dans le dossier de configuration, ajoutez un noeud nommé :

   `com.day.cq.wcm.notification.email.impl.EmailChannel` de type `sling:OsgiConfig`

1. Add a `String` property to the node named `email.from`. Pour la valeur, indiquez l’adresse électronique que vous souhaitez utiliser.

1. Cliquez sur **Enregistrer tout**.

Utilisez la procédure suivante pour définir le nœud dans vos dossiers sources de module de contenu :

1. Dans votre `jcr_root/apps/*app_name*/config folder`application, créez un fichier nommé `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Ajoutez le fichier XML suivant pour représenter le nœud :

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Remplacez la valeur de l’attribut `email.from` (`name@server.com`) par votre adresse électronique.

1. Enregistrez le fichier.

## Configuration du service de notification électronique de workflow {#configuring-the-workflow-email-notification-service}

Lorsque vous recevez des notifications électroniques de workflow, l’adresse électronique De et le préfixe URL hôte sont définis sur les valeurs par défaut. Vous pouvez modifier ces valeurs en configurant le **service de notification électronique de workflow Day CQ** dans la console Web. Dans ce cas, il est recommandé de conserver le changement dans le référentiel.

La configuration par défaut se présente comme suit dans la console Web :

![chlimage_1-277](assets/chlimage_1-277.png)

### Modèles de courrier électronique pour la notification de page {#email-templates-for-page-notification}

Les modèles de courrier électronique pour les notifications de page se trouvent à l’emplacement suivant :

`/etc/notification/email/default/com.day.cq.wcm.core.page`

Le modèle en anglais par défaut (`en.txt`) est défini comme suit :

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personnalisation des modèles de courrier électronique pour la notification de page {#customizing-email-templates-for-page-notification}

Pour personnaliser le modèle de courrier électronique en anglais en vue de la notification de page :

1. Dans CRXDE, ouvrez le fichier :

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. Modifiez le fichier en fonction de vos besoins.
1. Enregistrez les modifications.

Le modèle doit avoir le format suivant :

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

&lt;text_x> pouvant combiner du texte statique et des variables de chaînes dynamiques. Les variables suivantes peuvent être utilisées dans le modèle de courrier électronique pour les notifications de page :

* `${time}`, la date et l’heure de l’événement.

* `${userFullName}`, le nom complet de l’utilisateur ayant déclenché l’événement.

* `${userId}`, l’ID de l’utilisateur ayant déclenché l’événement.
* `${modifications}`, décrit le type de événement de page et le chemin de page au format :

   &lt;type d&#39;événement de page> => &lt;chemin de page>

   Par exemple :

   PageModified => /content/geometrixx/fr/products

### Modèles de courrier électronique pour les notifications de forum {#email-templates-for-forum-notification}

Les modèles de courrier électronique pour les notifications de forum se trouvent dans l’emplacement suivant :

`/etc/notification/email/default/com.day.cq.collab.forum`

Le modèle en anglais par défaut (`en.txt`) est défini comme suit :

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personnalisation des modèles de courrier électronique pour les notifications de forum {#customizing-email-templates-for-forum-notification}

Pour personnaliser le modèle de courrier électronique en anglais en vue de la notification de forum :

1. Dans CRXDE, ouvrez le fichier :

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. Modifiez le fichier en fonction de vos besoins.
1. Enregistrez les modifications.

Le modèle doit avoir le format suivant :

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Where `<text_x>` can be a mix of static text and dynamic string variables.

Les variables suivantes peuvent être utilisées dans le modèle de courrier électronique pour les notifications de forum :

* `${time}`, la date et l’heure de l’événement.

* `${forum.path}`, le chemin d’accès à la page de forum.

### Modèles de courrier électronique pour la notification de workflow {#email-templates-for-workflow-notification}

Le modèle de courrier électronique pour les notifications de workflow (en anglais) se trouve à l’emplacement suivant :

`/etc/workflow/notification/email/default/en.txt`

Il est défini comme suit :

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personnalisation des modèles de courrier électronique pour la notification de workflow {#customizing-email-templates-for-workflow-notification}

Pour personnaliser le modèle de courrier électronique en anglais en vue de la notification d’événement de workflow :

1. Dans CRXDE, ouvrez le fichier :

   `/etc/workflow/notification/email/default/en.txt`

1. Modifiez le fichier en fonction de vos besoins.
1. Enregistrez les modifications.

Le modèle doit avoir le format suivant :

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Where `<text_x>` can be a mix of static text and dynamic string variables. Each line of an `<text_x>` item needs to be ended with a backslash ( `\`), except for the last instance, when the absence of the backslash indicates the end of the `<text_x>` string variable.
>
>Vous trouverez plus d’informations sur le format des modèles dans la méthode [javadocs of the Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-).

The method `${payload.path.open}` reveals the path to the payload of the workitem. For example, for a page in Sites then then `payload.path.open` would be similar to `/bin/wcmcommand?cmd=open&path=…`.; this is without the server name, which is why the template prepends this with `${host.prefix}`.

Les variables suivantes peuvent être utilisées dans le modèle de courrier électronique :

* `${event.EventType}`, type du événement
* `${event.TimeStamp}`, date et heure de l’événement
* `${event.User}`, utilisateur ayant déclenché l’événement
* `${initiator.home}`, le chemin du noeud initiateur

* `${initiator.name}`, le nom de l’initiateur

* `${initiator.email}`, adresse électronique de l’initiateur
* `${item.id}`, ID de l’élément de travail
* `${item.node.id}`, ID du nœud dans le modèle de workflow associé à cet élément de travail
* `${item.node.title}`, titre de l’élément de travail
* `${participant.email}`, adresse électronique du participant
* `${participant.name}`, nom du participant
* `${participant.familyName}`, nom de famille du participant
* `${participant.id}`, identifiant du participant
* `${participant.language}`, la langue du participant
* `${instance.id}`, l’ID de processus
* `${instance.state}`, l’état du processus
* `${model.title}`, titre du modèle de workflow
* `${model.id}`, ID du modèle de workflow

* `${model.version}`, version du modèle de workflow
* `${payload.data}`, la charge utile

* `${payload.type}`, le type de charge utile
* `${payload.path}`, chemin d’accès de la charge utile
* `${host.prefix}`, préfixe hôte, par exemple, http://localhost:4502

### Ajout d’un modèle de courrier électronique pour une nouvelle langue {#adding-an-email-template-for-a-new-language}

Pour ajouter un modèle pour une nouvelle langue :

1. Dans CRXDE, ajoutez un fichier `<language-code>.txt` ci-dessous :

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` : pour les notifications de page
   * `/etc/notification/email/default/com.day.cq.collab.forum` : pour les notifications de forum
   * `/etc/workflow/notification/email/default` : pour les notifications de processus

1. Adaptez le fichier à la langue.
1. Enregistrez les modifications.

>[!NOTE]
>
>The `<language-code>` used as the filename for the email template needs to be a two-letters lower-case language code that is recognized by AEM. Pour les codes de langue, AEM s’appuie sur la norme ISO-639-1.

## Configuration des notifications électroniques d’AEM Assets {#assetsconfig}

Quand les collections dans AEM Assets sont partagées ou non, les utilisateurs peuvent recevoir des notifications électroniques de la part d’AEM. Pour configurer les notifications électroniques, procédez comme suit.

1. Configurez le service de messagerie, comme décrit ci-dessus dans [Configuration du service de messagerie](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Connectez-vous à AEM en tant qu’administrateur. Cliquez sur **Outils** > **Opérations** > **Console web** pour ouvrir la configuration de la console web.
1. Modifiez la **servlet de collection de ressources de la gestion des actifs numériques Day CQ**. Sélectionnez **Envoyer un courrier électronique**. Cliquez sur **Enregistrer**.

