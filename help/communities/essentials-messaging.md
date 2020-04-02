---
title: Messaging Essentials
seo-title: Messaging Essentials
description: Présentation du composant de messagerie
seo-description: Présentation du composant de messagerie
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: a7c2d71798649050f2f7852251996c2edf1cf113

---


# Messaging Essentials {#messaging-essentials}

Cette page  les détails de l’utilisation du composant Messagerie pour inclure une fonction de messagerie sur un site Web.

## Essentials for Client-Side {#essentials-for-client-side}

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
   <td>voir <a href="/help/communities/configure-messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
  <tr>
   <td><strong>configuration admin</strong></td>
   <td><a href="/help/communities/messaging.md">Configuration de la messagerie</a></td>
  </tr>
 </tbody>
</table>

**Liste des messages**

(pour la boîte de réception, l’envoi et la corbeille)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messagerie/composants/hbs/messagebox</p> </td>
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
   <td>voir <a href="/help/communities/configure-messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
  <tr>
   <td><strong>configuration admin</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">Configuration de la messagerie</a></td>
  </tr>
 </tbody>
</table>

Voir aussi Personnalisations côté [client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [Configuration de la messagerie](/help/communities/configure-messaging.md)
* [API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) client de messagerie pour les composants SCF
* [API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) de messagerie pour le service
* [Points de fin de la messagerie](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [Personnalisations côté serveur](/help/communities/server-customize.md)

>[!CAUTION]
>
>Le paramètre String *ne doit pas* contenir de barre oblique à la fin &quot;/&quot; pour les méthodes MessageBuilder suivantes :
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>
Par exemple :
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### Site de la communauté {#community-site}

Une structure de site communautaire, créée à l’aide de l’assistant, inclut la fonction de messagerie lorsqu’elle est sélectionnée. Voir `User Management` Paramètres de la console [Sites](/help/communities/sites-console.md#user-management)de la communauté.

### Exemple de code : Notification de réception du message {#sample-code-message-received-notification}

La fonction de messagerie sociale renvoie des  pour des opérations, par exemple `send`, `marking read`, `marking delete`. Ces  peuvent être capturés et des actions peuvent être entreprises sur les données contenues dans le .

L’exemple suivant illustre un gestionnaire de  qui écoute les  de l’ `message sent` et envoie un courrier électronique à tous les de messages qui utilisent le `Day CQ Mail Service`.

Pour tester l’exemple de script côté serveur, vous devez disposer d’un de développement  et de la possibilité de créer un lot OSGi :

1. Connectez-vous en tant qu’administrateur à ` [CRXDE|Lite](https://localhost:4502/crx/de)`.
1. Créez une `bundle node`entrée `/apps/engage/install` avec des noms arbitraires, tels que :

   * Nom symbolique : `com.engage.media.social.messaging.MessagingNotification`
   * Nom : Notification de message du didacticiel de prise en main
   * Description : Exemple de service d’envoi d’une notification par courrier électronique aux utilisateurs lorsqu’ils reçoivent un message
   * Module: `com.engage.media.social.messaging.notification`

1. Accédez à `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`, puis à :

   1. Supprimez la `Activator.java` classe créée automatiquement.
   1. Créez une classe `MessageEventHandler.java`.
   1. Copiez et collez le code ci-dessous dans `MessageEventHandler.java`.

1. Cliquez sur **Enregistrer tout**.
1. Accédez à `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`et ajoutez toutes les instructions d’importation telles qu’elles sont écrites dans le `MessageEventHandler.java` code.
1. Créez le lot.
1. Vérifiez que le service `Day CQ Mail Service`OSGi est configuré.
1. Connectez-vous en tant qu’utilisateur de démonstration et envoyez un courrier électronique à un autre utilisateur.
1. Le reçoit un courrier électronique concernant un nouveau message.

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

