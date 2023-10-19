---
title: Notions fondamentales sur la messagerie
description: Découvrez les détails de l’utilisation et de l’utilisation du composant Messagerie pour inclure une fonction de messagerie sur un site web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# Notions fondamentales sur la messagerie {#messaging-essentials}

Cette page documente les détails de l’utilisation du composant Messagerie pour inclure une fonction de messagerie sur un site web.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

**Composer le message**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir <a href="/help/communities/configure-messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
  <tr>
   <td><strong>configuration de l'administrateur</strong></td>
   <td><a href="/help/communities/messaging.md">Configuration de la messagerie</a></td>
  </tr>
 </tbody>
</table>

**Liste des messages**

(Pour la boîte de réception, l’envoi et la corbeille)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir <a href="/help/communities/configure-messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
  <tr>
   <td><strong>configuration de l'administrateur</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
 </tbody>
</table>

Voir aussi [Personnalisations côté client](/help/communities/client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [Configuration de la messagerie](/help/communities/configure-messaging.md)
* [API clientes de messagerie](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) pour les composants SCF
* [API de messagerie](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) pour le service
* [Points de fin de messagerie](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personnalisations côté serveur](/help/communities/server-customize.md)

>[!CAUTION]
>
>Le paramètre String doit *not* contiennent une barre oblique à la fin &quot;/&quot; pour les méthodes MessageBuilder suivantes :
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>Par exemple :
>
>```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Site de la communauté {#community-site}

Une structure de site de communauté, créée à l’aide de l’assistant, inclut la fonction de messagerie lorsqu’elle est sélectionnée. Voir `User Management` des paramètres de [Console Sites de communauté](/help/communities/sites-console.md#user-management).

### Exemple de code : notification de réception de message {#sample-code-message-received-notification}

La fonction Messagerie sociale génère des événements pour les opérations, par exemple `send`, `marking read`, `marking delete`. Ces événements peuvent être capturés et les actions effectuées sur les données contenues dans l’événement.

L’exemple suivant illustre un gestionnaire d’événements qui écoute la fonction `message sent` et envoie un email à tous les destinataires du message à l’aide de la variable `Day CQ Mail Service`.

Pour tester l’exemple de script côté serveur, vous avez besoin d’un environnement de développement et de la possibilité de créer un lot OSGi :

1. Connectez-vous en tant qu’administrateur à ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Créez un `bundle node`in `/apps/engage/install` avec des noms arbitraires, tels que :

   * Nom symbolique : `com.engage.media.social.messaging.MessagingNotification`
   * Nom : Notification de message du tutoriel de prise en main
   * Description : un exemple de service pour envoyer une notification électronique aux utilisateurs lorsqu’ils reçoivent un message
   * Module: `com.engage.media.social.messaging.notification`

1. Accédez à `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`, puis :

   1. Supprimez le `Activator.java` de classe créée automatiquement.
   1. Créer une classe `MessageEventHandler.java`.
   1. Copiez et collez le code ci-dessous dans `MessageEventHandler.java`.

1. Cliquez sur **Enregistrer tout**.
1. Accédez à `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`, puis ajoutez toutes les instructions d’importation comme indiqué dans la variable `MessageEventHandler.java` code.
1. Créez le lot.
1. Assurez-vous que `Day CQ Mail Service`Le service OSGi est configuré.
1. Connectez-vous en tant qu’utilisateur de démonstration et envoyez un courrier électronique à un autre utilisateur.
1. Le destinataire reçoit un email concernant un nouveau message.

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
