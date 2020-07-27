---
title: Sélection de manière dynamique d’un utilisateur ou d’un groupe pour les étapes de processus basés sur l’utilisation d’AEM Forms
seo-title: Sélection de manière dynamique d’un utilisateur ou d’un groupe pour les étapes de processus basés sur l’utilisation d’AEM Forms
description: 'Découvrez comment sélectionner un utilisateur ou un groupe pour un processus AEM Forms au moment de l’exécution. '
seo-description: 'Découvrez comment sélectionner un utilisateur ou un groupe pour un processus AEM Forms au moment de l’exécution. '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 95%

---


# Sélection de manière dynamique d’un utilisateur ou d’un groupe pour les étapes de processus basés sur l’utilisation d’AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Découvrez comment sélectionner un utilisateur ou un groupe pour un processus AEM Forms au moment de l’exécution.

Dans les grandes entreprises, il existe des exigences pour sélectionner de manière dynamique les utilisateurs d’un processus, par exemple, la sélection d’un agent de terrain pour servir un client en fonction de la proximité de l’agent avec le client. Dans ce cas, l’agent est sélectionné de manière dynamique.

Assign task and Adobe Sign steps of [Forms-centric workflows on OSGi](/help/forms/using/aem-forms-workflow.md) provide options to dynamically select a user. Vous pouvez utiliser des bundles ECMAScript ou OSGi pour sélectionner de manière dynamique une personne désignée pour l’étape Affecter une tâche ou pour sélectionner des signataires pour l’étape Signer un document.

## Utilisation de ECMAScript pour sélectionner de manière dynamique un utilisateur ou un groupe {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript est un langage de script. Il est utilisé pour les scripts et les applications serveur côté client. Effectuez les étapes suivantes pour sélectionner de manière dynamique un utilisateur ou un groupe à l’aide de ECMAScript :

1. Ouvrez CRXDE Lite. The URL is `https://'[server]:[port]'/crx/de/index.jsp`
1. Créez un fichier avec l’extension .ecma au chemin d’accès suivant. Si le chemin d’accès (structure du nœud) n’existe pas, créez-le :

   * (Path for Assign Task step) `/apps/fd/dashboard/scripts/participantChooser`
   * (Chemin de l’étape Signature) `/apps/fd/workflow/scripts/adobesign`

1. Ajoutez ECMAScript, qui possède la logique pour sélectionner de manière dynamique un utilisateur, au fichier .ecma. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   Pour des exemples de script, voir [Exemples de ECMAScript pour la sélection dynamique d’un utilisateur ou d’un groupe](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Ajoutez le nom d’affichage du script. Ce nom s’affiche dans les étapes du processus. Pour spécifier le nom :

   1. Développez le nœud du script, cliquez avec le bouton droit de la souris sur **[!UICONTROL jcr:content]**, puis cliquez sur **[!UICONTROL Mixins]**.
   1. Ajoutez la propriété `mix:title` dans la boîte de dialogue Modifier les mixins et cliquez sur **OK**.
   1. Ajoutez la propriété suivante au noeud jcr:content du script :

      | Nom | Type | Valeur |
      |--- |--- |--- |
      | jcr:title | Chaîne | Spécifiez le nom du script. Par exemple, sélectionnez l’agent de terrain le plus proche. Ce nom s’affiche dans les étapes Affecter une tâche et Signer un document. |

   1. Cliquez sur **Enregistrer tout**. Le script peut être sélectionné dans les composants du processus AEM.

      ![script](assets/script.png)

### Exemples de ECMAScript pour sélectionner de manière dynamique un utilisateur ou un groupe {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

L’exemple ECMAScript suivant sélectionne de manière dynamique une personne désignée pour l’étape Affecter une tâche. Dans ce script, un utilisateur est sélectionné en fonction du chemin de la charge utile. Avant d’utiliser ce script, veillez à ce que tous les utilisateurs mentionnés dans le script existent dans AEM. Dans le cas contraire, le processus associé peut échouer.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

L’exemple ECMAScript suivant sélectionne de manière dynamique une personne désignée pour l’étape Adobe Sign. Avant d’utiliser le script ci-dessous, assurez-vous que les informations utilisateur (adresses électroniques et numéros de téléphone) mentionnées dans le script sont correctes. Dans le cas contraire, le processus associé peut échouer.

>[!NOTE]
>
>Lors de l’utilisation de ECMAScript pour Adobe Sign, le script doit se trouver dans le référentiel crx à l’adresse /apps/fd/workflow/scripts/adobesign/ et doit disposer d’une fonction appelée getAdobeSignRecipients pour renvoyer une liste des utilisateurs.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Utilisation de l’interface Java pour sélectionner de manière dynamique un utilisateur ou un groupe {#use-java-interface-to-dynamically-choose-a-user-or-group}

Vous pouvez utiliser l’interface Java [RecipientInfoSpecifier](https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) pour choisir de manière dynamique un utilisateur ou un groupe pour les étapes Adobe Sign et Affecter une tâche. Vous pouvez créer un bundle OSGi qui utilise l’interface Java [RecipientInfoSpecifier](https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) et la déploie sur le serveur AEM Forms. Cela rend disponible à la sélection l’option dans les composants Affecter une tâche et Adobe Sign du processus AEM.

Vous avez besoin des fichiers jar [SDK client AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) et [granite jar](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) pour compiler l’exemple de code répertorié ci-dessous. Ajoutez ces fichiers jar en tant que dépendances externes au projet de bundle OSGi. Vous pouvez utiliser n’importe quel IDE Java pour créer un bundle OSGi. La procédure suivante fournit des étapes pour l’utilisation de Eclipse afin de créer un bundle OSGi :

1. Ouvrez l’IDE Eclipse. Accédez à **[!UICONTROL Fichier]**>**[!UICONTROL Nouveau projet]**.
1. Sur l’écran de sélection de l’assistant, sélectionnez **[!UICONTROL Projet Maven]** puis cliquez sur **[!UICONTROL Suivant]**.
1. Sur le nouveau projet Maven, conservez les valeurs par défaut, puis cliquez sur **[!UICONTROL Suivant]**. Sélectionnez un archétype et cliquez sur **[!UICONTROL Suivant]**. Par exemple, maven-archetype-quickstart. Spécifiez l’**[!UICONTROL ID du groupe]**, l’**[!UICONTROL ID de l’artefact]**,**[!UICONTROL la version]** et le **[!UICONTROL package]** pour le projet et cliquez sur **[!UICONTROL Terminer]**. La du projet est créée.
1. Ouvrez le fichier pom.xml pour modifier et remplacer tout le contenu du fichier par ce qui suit :

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Ajoutez le code source utilisant l’interface Java [RecipientInfoSpecifier](https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) pour sélectionner de manière dynamique un utilisateur ou un groupe pour l’étape Affecter une tâche. Pour un exemple de code, voir [Exemple pour la sélection dynamique d’un utilisateur ou d’un groupe à l’aide de l’interface Java](#-sample-scripts-for).
1. Ouvrez une invite de commande et accédez au répertoire contenant le projet de bundle OSGi. Utilisez la commande suivante pour créer le bundle OSGi :

   `mvn clean install`

1. Chargez le bundle sur un serveur AEM Forms. Vous pouvez utiliser AEM Package Manager pour importer le bundle sur le serveur AEM Forms.

Une fois le bundle importé, l’option de sélection de l’interface Java pour sélectionner de manière dynamique un utilisateur ou un groupe devient disponible pour les étapes Adobe Sign et Affecter une tâche.

### Exemples de code Java pour sélectionner de manière dynamique un utilisateur ou un groupe {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

L’exemple de code suivant sélectionne de manière dynamique une personne désignée pour l’étape Adobe Sign. Vous pouvez utiliser ce code dans un bundle OSGi. Avant d’utiliser le code répertorié ci-dessous, assurez-vous que les informations utilisateur (adresses électroniques et numéros de téléphone) mentionnées dans le code sont correctes. Si les informations utilisateur mentionnées dans le code sont incorrectes, le processus associé peut échouer.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

