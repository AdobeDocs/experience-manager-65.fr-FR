---
title: Création d’un gestionnaire d’invitation d’utilisateurs externes
description: Création d’un gestionnaire d’invitation d’utilisateurs externes
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---


# Création d&#39;un gestionnaire d&#39;invitation d&#39;utilisateurs externes {#create-invite-external-users-handler}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Vous pouvez créer un gestionnaire d’invitation d’utilisateurs externes pour le service de Rights Management. Un gestionnaire d’invite d’utilisateurs externes permet au service de Rights Management d’inviter des utilisateurs externes à devenir des utilisateurs Rights Management. Lorsqu’un utilisateur devient un utilisateur Rights Management, il peut effectuer des tâches, telles que l’ouverture d’un document PDF protégé par une stratégie. Une fois que le gestionnaire d’invite d’utilisateurs externes est déployé dans AEM Forms, vous pouvez utiliser Administration Console pour interagir avec celui-ci.

>[!NOTE]
>
>Un gestionnaire d’invitation d’utilisateurs externes est un composant AEM Forms. Avant de créer un gestionnaire d’invitation d’utilisateurs externes, il est recommandé de se familiariser avec la création de composants.

**Résumé des étapes**

Pour développer un gestionnaire d&#39;invitation d&#39;utilisateurs externes, vous devez effectuer les étapes suivantes :

1. Configurez votre environnement de développement.
1. Définissez l’implémentation du gestionnaire d’invitation d’utilisateurs externes.
1. Définissez le fichier XML du composant.
1. Déployez le gestionnaire Inviter des utilisateurs externes.
1. Testez le gestionnaire Inviter des utilisateurs externes.

## Configuration de votre environnement de développement {#setting-up-development-environment}

Pour configurer votre environnement de développement, vous devez créer un nouveau projet Java, tel qu’un projet Eclipse. La version d’Eclipse prise en charge est `3.2.1` ou ultérieure.

Le Rights Management SPI requiert que le fichier `edc-server-spi.jar` soit défini dans le chemin de classe de votre projet. Si vous ne référencez pas ce fichier JAR, vous ne pouvez pas utiliser l’interface SPI Rights Management dans votre projet Java. Ce fichier JAR est installé avec le SDK AEM Forms dans le dossier `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`.

Outre l’ajout du fichier `edc-server-spi.jar` au chemin de classe de votre projet, vous devez également ajouter les fichiers JAR requis pour utiliser l’API Rights Management Service. Ces fichiers sont nécessaires à l’utilisation de l’API Rights Management Service dans le gestionnaire Inviter des utilisateurs externes.

## Définition de l&#39;implémentation du gestionnaire d&#39;invite d&#39;utilisateurs externes {#define-invite-external-users-handler}

Pour développer un gestionnaire d&#39;invite d&#39;utilisateurs externes, vous devez créer une classe Java qui implémente l&#39;interface `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Cette classe contient une méthode appelée `invitedUser`, que le service de Rights Management appelle lorsque des adresses électroniques sont envoyées à l’aide de la page **Ajouter les utilisateurs invités** accessible via Administration Console.

La méthode `invitedUser` accepte une instance `java.util.List`, qui contient des adresses électroniques de type chaîne envoyées à partir de la page **Ajouter les utilisateurs invités**. La méthode `invitedUser` renvoie un tableau d&#39;objets `InvitedUserProviderResult`, qui est généralement un mappage d&#39;adresses électroniques avec des objets Utilisateur (ne renvoient pas de valeur nulle).

>[!NOTE]
>
>Outre la démonstration de la création d’un gestionnaire d’invite d’utilisateurs externes, cette section utilise également l’API AEM Forms.

L&#39;implémentation du gestionnaire d&#39;invite d&#39;utilisateurs externes contient une méthode définie par l&#39;utilisateur nommée `createLocalPrincipalAccount`. Cette méthode accepte une valeur de chaîne qui spécifie une adresse électronique comme valeur de paramètre. La méthode `createLocalPrincipalAccount` suppose la préexistence d&#39;un domaine local appelé `EDC_EXTERNAL_REGISTERED`. Vous pouvez configurer ce nom de domaine comme bon vous semble ; toutefois, pour une application de production, vous pouvez vouloir l’intégrer à un domaine d’entreprise.

La méthode `createUsers` effectue une itération sur chaque adresse électronique et crée un objet User correspondant (un utilisateur local dans le domaine `EDC_EXTERNAL_REGISTERED`). Enfin, la méthode `doEmails` est appelée. Cette méthode est délibérément laissée sous la forme d’un stub dans l’échantillon. Dans une mise en oeuvre de production, il contiendrait une logique d’application permettant d’envoyer des messages électroniques d’invitation aux utilisateurs nouvellement créés. L’exemple montre le flux logique d’une application réelle.

### Définition de l&#39;implémentation du gestionnaire d&#39;invite d&#39;utilisateurs externes {#user-handler-implementation}

L’implémentation du gestionnaire d’utilisateurs externes suivante invite les utilisateurs externes à accepter les adresses électroniques envoyées à partir de la page Ajouter les utilisateurs invités accessible via Administration Console.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>Cette classe Java est enregistrée en tant que fichier JAVA nommé InviteExternalUsersSample.java.

## Définition du fichier XML du composant pour le gestionnaire d&#39;autorisations {#define-component-xml-authorization-handler}

Vous devez définir un fichier XML de composant pour déployer le composant de gestionnaire d’invite d’utilisateurs externes. Un fichier XML de composant existe pour chaque composant et fournit des métadonnées sur ce composant.

Le fichier `component.xml` suivant est utilisé pour le gestionnaire d’invitation d’utilisateurs externes. Notez que le nom du service est `InviteExternalUsersSample` et que l&#39;opération exposée par ce service est nommée `invitedUser`. Le paramètre input est une instance `java.util.List` et la valeur output est un tableau d&#39;instances `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`.

### Définition du fichier XML du composant pour le gestionnaire d’invite d’utilisateurs externes {#component-xml-invite-external-users-handler}

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## Création d’un package du gestionnaire d’invite des utilisateurs externes {#packaging-invite-external-users-handler}

Pour déployer le gestionnaire d’invitation d’utilisateurs externes en AEM Forms, vous devez compresser votre projet Java dans un fichier JAR. Vous devez vous assurer que les fichiers JAR externes sur lesquels dépend la logique métier du gestionnaire d’invite des utilisateurs externes, tels que les fichiers `edc-server-spi.jar` et `adobe-rightsmanagement-client.jar`, sont également inclus dans le fichier JAR. De plus, le fichier XML du composant doit être présent. Le fichier `component.xml` et les fichiers JAR externes doivent se trouver à la racine du fichier JAR.

>[!NOTE]
>
>Dans l&#39;illustration ci-dessous, une classe `BootstrapImpl` s&#39;affiche. Cette section ne décrit pas comment créer une classe `BootstrapImpl`.

L’illustration suivante présente le contenu du projet Java inclus dans le fichier JAR du gestionnaire d’utilisateurs externes invités.

![Inviter des utilisateurs](assets/ci_ci_InviteUsers.png)

A. Fichiers JAR externes requis par le composant B. Fichier JAVA

Vous devez compresser le gestionnaire d’invite d’utilisateurs externes dans un fichier JAR. Dans le diagramme précédent, notez que les fichiers .JAVA sont répertoriés. Une fois compressés dans un fichier JAR, les fichiers .CLASS correspondants doivent également être spécifiés. Sans les fichiers .CLASS, le gestionnaire d’autorisations ne fonctionne pas.

>[!NOTE]
>
>Après avoir compressé le gestionnaire d’autorisations externe dans un fichier JAR, vous pouvez déployer le composant sur AEM Forms. Un seul gestionnaire d’utilisateurs externes d’invitation peut être déployé à un moment donné.

>[!NOTE]
>
>Vous pouvez également déployer un composant par programmation.

## Test du gestionnaire d’invite d’utilisateurs externes {#testing-invite-external-users-handler}

Pour tester le gestionnaire d’invitation d’utilisateurs externes, vous pouvez ajouter des utilisateurs externes à inviter à l’aide d’Administration Console.

Pour ajouter des utilisateurs externes à inviter à l’aide d’Administration Console :

1. Déployez le fichier JAR du gestionnaire d’invite d’utilisateurs externes à l’aide de Workbench.
1. Redémarrez le serveur d’applications.
1. Connectez-vous à Administration Console.
1. Cliquez sur **[!UICONTROL Services]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuration]** > Invité **[!UICONTROL Enregistrement d’utilisateur]**.
1. Activez l’enregistrement des utilisateurs invités en cochant la case **[!UICONTROL Activer l’enregistrement des utilisateurs invités]**. Sous **[!UICONTROL Utiliser le système d&#39;enregistrement intégré]**, cliquez sur **[!UICONTROL Non]**. Enregistrez vos paramètres.
1. Dans la page d&#39;accueil Administration Console, cliquez sur **[!UICONTROL Paramètres]** > **[!UICONTROL User Management]** > **[!UICONTROL Gestion des domaines]**.
1. Cliquez sur **[!UICONTROL Nouveau domaine local]**. Sur la page suivante, créez un domaine dont le nom et la valeur d’identificateur sont `EDC_EXTERNAL_REGISTERED`. Enregistrez vos modifications.
1. Dans la page d&#39;accueil Administration Console, cliquez sur **[!UICONTROL Services]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Utilisateurs invités et locaux]**. La page **[!UICONTROL Ajouter l’utilisateur invité]** s’affiche.
1. Entrez les adresses électroniques (puisque le gestionnaire d’invitation des utilisateurs externes n’envoie pas réellement de messages électroniques, l’adresse électronique n’a pas besoin d’être valide). Cliquez sur **[!UICONTROL OK]**. Les utilisateurs sont invités dans le système.
1. Dans la page d&#39;accueil Administration Console, cliquez sur **[!UICONTROL Paramètres]** > **[!UICONTROL User Management]** > **[!UICONTROL Utilisateurs et groupes]**.
1. Dans le champ **[!UICONTROL Rechercher]**, entrez une adresse électronique que vous avez spécifiée. Cliquez sur **[!UICONTROL Rechercher]**. L’utilisateur que vous avez invité s’affiche en tant qu’utilisateur dans le domaine `EDC_EXTERNAL_REGISTERED` local.

>[!NOTE]
>
>Le gestionnaire d’utilisateurs externes d’invitation échoue si le composant est arrêté ou désinstallé.
