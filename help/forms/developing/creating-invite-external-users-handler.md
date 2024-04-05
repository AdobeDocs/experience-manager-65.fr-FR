---
title: Créer un gestionnaire d’utilisateurs externes
description: Découvrez comment créer un gestionnaire d’utilisateurs et d’utilisatrices externes. Un gestionnaire d’utilisateurs et d’utilisatrices externes permet au service Rights Management d’inviter des utilisateurs et utilisatrices externes à devenir des utilisateurs et utilisatrices de Rights Management.
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 100%

---

# Créer un gestionnaire d’invitation d’utilisateurs externes {#create-invite-external-users-handler}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez créer un gestionnaire d’invitation d’utilisateurs externes pour le service Rights Management. Un gestionnaire d’invitation d’utilisateurs externes permet au service Rights Management d’inviter des utilisateurs externes à devenir des utilisateurs Rights Management. Lorsqu’un utilisateur devient utilisateur Rights Management, il peut effectuer certaines tâches, comme ouvrir un document PDF protégé par une politique. Une fois le gestionnaire d’invitation d’utilisateurs externes déployé dans AEM Forms, vous pouvez utiliser la console d’administration pour interagir avec celui-ci.

>[!NOTE]
>
>Un gestionnaire d’invitation d’utilisateurs externes est un composant AEM Forms. Avant de créer un gestionnaire d’invitation d’utilisateurs externes, il est recommandé de vous familiariser avec la création de composants.

**Résumé des étapes**

Pour développer un gestionnaire d’invitation d’utilisateurs externes, procédez comme suit :

1. Configurez votre environnement de développement.
1. Définissez l’implémentation du gestionnaire d’invitation d’utilisateurs externes.
1. Définissez le fichier XML du composant.
1. Déployez le gestionnaire d’invitation d’utilisateurs externes.
1. Testez le gestionnaire d’invitation d’utilisateurs externes.

## Configurer votre environnement de développement {#setting-up-development-environment}

Pour configurer votre environnement de développement, vous devez créer un projet Java, tel qu’un projet Eclipse. La version d’Eclipse prise en charge est la version `3.2.1` ou ultérieure.

La SPI Rights Management nécessite de spécifier le fichier `edc-server-spi.jar` dans le chemin d’accès de classe de votre projet. Si vous ne référencez pas ce fichier JAR, vous ne pouvez pas utiliser la SPI Rights Management dans votre projet Java. Ce fichier JAR est installé avec le SDK AEM Forms dans le dossier `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`.

En plus de l’ajout du fichier `edc-server-spi.jar` dans le chemin de classe de votre projet, vous devez également ajouter les fichiers JAR requis pour utiliser l’API du service Rights Management. Ces fichiers sont nécessaires pour utiliser l’API du service Rights Management dans le gestionnaire d’invitation d’utilisateurs externes.

## Définir l’implémentation du gestionnaire d’invitation d’utilisateurs externes {#define-invite-external-users-handler}

Pour développer un gestionnaire d’invitation d’utilisateurs externes, vous devez créer une classe Java qui implémente l’interface `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Cette classe contient une méthode nommée `invitedUser`, que le service Rights Management appelle lorsque les adresses électroniques sont envoyées à l’aide de la page **Ajout d’utilisateurs invités** accessible via la console d’administration.

La méthode `invitedUser` accepte une instance `java.util.List` qui contient des adresses e-mail de type chaîne envoyées à partir de la page **Ajout d’utilisateurs invités**. La méthode `invitedUser` renvoie un tableau d’objets `InvitedUserProviderResult`, qui est généralement un mappage d’adresses e-mail aux objets Utilisateur (ne renvoyez pas la valeur null).

>[!NOTE]
>
>En plus de présenter comment créer un gestionnaire d’invitation d’utilisateurs externes, cette section utilise également l’API AEM Forms.

L’implémentation du gestionnaire d’invitation d’utilisateurs externes contient une méthode définie par l’utilisateur nommée `createLocalPrincipalAccount`. Cette méthode accepte une valeur de chaîne qui indique une adresse électronique comme valeur de paramètre. La méthode `createLocalPrincipalAccount` suppose la préexistence d’un domaine local appelé `EDC_EXTERNAL_REGISTERED`. Vous pouvez configurer ce nom de domaine comme vous le souhaitez ; toutefois, pour une application de production, vous pouvez vouloir l’intégrer à un domaine d’entreprise.

La méthode `createUsers` effectue une itération sur chaque adresse électronique et crée un objet Utilisateur correspondant (un utilisateur local dans le domaine `EDC_EXTERNAL_REGISTERED`). Enfin, la méthode `doEmails` est appelée. Cette méthode est délibérément laissée sous la forme d’un bulletin dans l’échantillon. Dans une implémentation destinée à la production, elle contiendrait la logique de l’application pour envoyer des messages d’invitation par e-mail aux utilisateurs et utilisatrices nouvellement créés. Il est laissé dans l’exemple pour démontrer le flux logique d’application d’une application réelle.

### Définir l’implémentation du gestionnaire d’invitation d’utilisateurs externes {#user-handler-implementation}

L’implémentation suivante du gestionnaire d’invitation d’utilisateurs externes accepte les adresses électroniques envoyées à partir de la page Ajouter des utilisateurs invités, accessible via la console d’administration.

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

## Définir un fichier XML du composant du gestionnaire d’autorisations {#define-component-xml-authorization-handler}

Vous devez définir un fichier XML composant pour déployer le composant du gestionnaire d’utilisateurs et d’utilisatrices externes. Un fichier XML de composant existe pour chaque composant et fournit des métadonnées sur le composant.

Le fichier `component.xml` suivant est utilisé pour le gestionnaire d’invitation d’utilisateurs externes. Notez que le nom du service est `InviteExternalUsersSample` et que l’opération exposée par ce service est nommée `invitedUser`. Le paramètre d’entrée est une instance `java.util.List` et la valeur de sortie est un tableau d’instances `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`.

### Définir un fichier XML de composant pour le gestionnaire d’invitation d’utilisateurs externes {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
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

## Regrouper le gestionnaire d’invitation d’utilisateurs externes {#packaging-invite-external-users-handler}

Pour déployer le gestionnaire d’invitations d’utilisateurs externes vers AEM Forms, vous devez compresser votre projet Java dans un fichier JAR. Vous devez vous assurer que les fichiers JAR externes dont dépend la logique commerciale du gestionnaire d’utilisateurs et d’utilisatrices externes, tels que les fichiers `edc-server-spi.jar` et `adobe-rightsmanagement-client.jar`, sont également inclus dans le fichier JAR. De même, le fichier XML du composant doit être présent. Le fichier `component.xml` et les fichiers JAR externes doivent se trouver à la racine du fichier JAR.

>[!NOTE]
>
>L’illustration ci-dessous présente une classe `BootstrapImpl`. Cette section n’explique pas comment créer une classe `BootstrapImpl`.

L’illustration suivante montre le contenu du projet Java inclus dans le fichier JAR du gestionnaire d’utilisateurs et d’utilisatrices externes.

![Inviter des utilisateurs](assets/ci_ci_InviteUsers.png)

A. Fichiers JAR externes requis par le composant B. Fichier JAVA

Vous devez compresser le gestionnaire d’utilisateurs et d’utilisatrices externes dans un fichier JAR. Dans le diagramme précédent, remarquez que les fichiers .JAVA sont répertoriés. Une fois compressés dans un fichier JAR, les fichiers .CLASS correspondants doivent également être spécifiés. Sans les fichiers .CLASS, le gestionnaire d’autorisations ne fonctionne pas.

>[!NOTE]
>
>Après avoir compressé le gestionnaire d’autorisation externe dans un fichier JAR, vous pouvez déployer le composant dans AEM Forms. Un seul gestionnaire d’invitations d’utilisateurs externes peut être déployé à un moment donné.

>[!NOTE]
>
>Vous pouvez également déployer un composant par programmation.

## Tester le gestionnaire d’invitations d’utilisateurs externes {#testing-invite-external-users-handler}

Pour tester le gestionnaire d’invitations d’utilisateurs externes, vous pouvez ajouter des utilisateurs externes à inviter en utilisant la console d’administration.

Pour ajouter des utilisateurs externes à l’invitation à l’aide de la console d’administration :

1. Déployez le fichier JAR du gestionnaire d’utilisateurs et d’utilisatrices externes à l’aide de Workbench.
1. Redémarrez le serveur d’applications.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

1. Connectez-vous à Administration Console.
1. Cliquez sur **[!UICONTROL Services]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configuration]** > Invité **[!UICONTROL Enregistrement d’utilisateur]**.
1. Activez l’enregistrement des utilisateurs invités en cochant la case **[!UICONTROL Activer l’enregistrement des utilisateurs invités]**. Sous **[!UICONTROL Utiliser le système d’enregistrement intégré]**, cliquez sur **[!UICONTROL Non]**. Enregistrez vos paramètres.
1. Sur la page d’accueil de la console d’administration, cliquez sur **[!UICONTROL Paramètres]** > **[!UICONTROL User Management]** > **[!UICONTROL Gestion des domaines]**.
1. Cliquez sur **[!UICONTROL Nouveau domaine local]**. Sur la page suivante, créez un domaine dont le nom et la valeur de l’identifiant sont `EDC_EXTERNAL_REGISTERED`. Enregistrez vos modifications.
1. Sur la page d’accueil de la console d’administration, cliquez sur **[!UICONTROL Services]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Utilisateurs invités et locaux]**. La page **[!UICONTROL Ajouter un utilisateur invité]** s’affiche.
1. Saisissez les adresses e-mail (étant donné que le gestionnaire d’invitations d’utilisateurs externes actuel n’envoie pas réellement d’e-mail, les adresses e-mail ne doivent pas nécessairement être valides). Cliquez sur **[!UICONTROL OK]**. Les utilisateurs sont invités dans le système.
1. Sur la page d’accueil de la console d’administration, cliquez sur **[!UICONTROL Paramètres]** > **[!UICONTROL User Management]** > **[!UICONTROL Utilisateurs et groupes]**.
1. Dans le champ **[!UICONTROL Rechercher]**, saisissez une adresse e-mail que vous avez spécifiée. Cliquez sur **[!UICONTROL Rechercher]**. L’utilisateur que vous avez invité apparaît comme un utilisateur dans le domaine local `EDC_EXTERNAL_REGISTERED`.

>[!NOTE]
>
>Le gestionnaire d’invitations d’utilisateurs externes échoue si le composant est arrêté ou désinstallé.
