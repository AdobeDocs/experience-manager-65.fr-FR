---
title: Début rapide de l'API Javadocument Security Service (SOAP)
seo-title: Début rapide de l'API Javadocument Security Service (SOAP)
description: Début rapide de l'API Javadocument Security Service (SOAP)
uuid: f3823a95-c8c2-42c8-8edc-3ab8ab4311dc
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b89293c4-ea2e-4fa4-9e5e-ef4f548e9608
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---


# Début rapide de l&#39;API Java du service de sécurité document (SOAP) {#document-security-service-javaapi-quick-start-soap}

Le Début rapide des API Java (SOAP) est disponible pour le service Rights Management :

[Début rapide (mode SOAP) : Création d’une stratégie à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-creating-a-policy-using-the-java-api)

[Début rapide (mode SOAP) : Modification d’une stratégie à l’aide de l’API Java](#quick-start-soap-mode-modifying-a-policy-using-the-java-api)

[Début rapide (mode SOAP) : Suppression d’une stratégie à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-deleting-a-policy-using-the-java-api)

[Début rapide (mode SOAP) : Application d’une stratégie à un document PDF à l’aide de l’API Java](#quick-start-soap-mode-applying-a-policy-to-a-pdf-document-using-the-java-api)

[Début rapide (mode SOAP) : Suppression d’une stratégie d’un document PDF à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-removing-a-policy-from-a-pdf-document-using-the-java-api)

[Début rapide (mode SOAP) : Révocation d’un document à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-revoking-a-document-using-the-java-api)

[Début rapide (mode SOAP) : Rétablissement de l’accès à un document révoqué à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-reinstating-access-to-a-revoked-document-using-the-java-api)

[Début rapide (mode SOAP) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-inspecting-policy-protected-pdf-documents-using-the-java-api)

[Début rapide (mode SOAP) : Création d’un filigrane à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-creating-a-pdf-watermark-using-the-java-api)

[Début rapide (mode SOAP) : Modification d’un filigrane à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-modifying-a-watermark-using-the-java-api)

[Début rapide (mode SOAP) : Recherche de événements à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-searching-for-events-using-the-java-api)

[Début rapide (mode SOAP) : Suppression d’une stratégie d’un document Word à l’aide de l’API Java](document-security-service-java-api.md#quick-start-soap-mode-removing-a-policy-from-a-word-document-using-the-java-api)

Les opérations AEM Forms peuvent être effectuées à l’aide de l’API AEM Forms fortement typée et le mode de connexion doit être défini sur SOAP.

>[!NOTE]
>
>Les Débuts rapides situés dans Programmation avec AEM Forms sont basés sur le système d&#39;exploitation Forms. Cependant, si vous utilisez un autre système d’exploitation, tel qu’UNIX, remplacez les chemins spécifiques à Windows par les chemins pris en charge par le système d’exploitation concerné. De même, si vous utilisez un autre serveur d’applications J2EE, veillez à spécifier des propriétés de connexion valides. Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Début rapide (mode SOAP) : Création d’une stratégie à l’aide de l’API Java {#quick-start-soap-mode-creating-a-policy-using-the-java-api}

L’exemple de code Java suivant crée une nouvelle stratégie nommée *Allow Copy*. Le jeu de stratégies auquel la stratégie est ajoutée est nommé *Jeu de stratégies global*. Ce jeu de stratégies existe par défaut. (Voir [Création de stratégies](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.um.api.infomodel.Principal;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 public class CreatePolicy {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
              //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
             //Create a Policy object that represents the new policy
             Policy myPolicy = InfomodelObjectFactory.createPolicy();
 
             //Set policy attributes that are used by the policy
             myPolicy.setName("Allow Copy");
             myPolicy.setDescription("This policy enables users to copy information from the PDF document");
             myPolicy.setPolicySetName("Global Policy Set");
             myPolicy.setOfflineLeasePeriod(30);
             myPolicy.setTracked(true);
 
             //Set the validity period to 30 days
             ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
             validityPeriod.setRelativeExpirationDays(30);
             myPolicy.setValidityPeriod(validityPeriod);
 
             //Create a PolicyEntry object
             PolicyEntry myPolicyEntry = InfomodelObjectFactory.createPolicyEntry();
 
             //Specify the permissions
             Permission onlinePermission = InfomodelObjectFactory.createPermission(Permission.OPEN_ONLINE) ;
             Permission copyPermission = InfomodelObjectFactory.createPermission(Permission.COPY);
 
             //Add permissions to the policy entry
             myPolicyEntry.addPermission(onlinePermission);
             myPolicyEntry.addPermission(copyPermission);
 
             //Create principal object
              Principal publisherPrincipal = InfomodelObjectFactory.createSpecialPrincipal(InfomodelObjectFactory.PUBLISHER_PRINCIPAL);
 
              //Add a principal object to the policy entry
              myPolicyEntry.setPrincipal(publisherPrincipal);
 
              //Attach the policy entry to the policy
              myPolicy.addPolicyEntry(myPolicyEntry);
 
              //Register the policy
             PolicyManager policyManager = rightsClient.getPolicyManager();
             policyManager.registerPolicy(myPolicy,"Global Policy Set");
             }
         catch (Exception ex)
             {
                 ex.printStackTrace();
             }
         }
 }
 
```

## Début rapide (mode SOAP) : Modification d’une stratégie à l’aide de l’API Java {#quick-start-soap-mode-modifying-a-policy-using-the-java-api}

L’exemple de code Java suivant modifie une stratégie nommée *Allow Copy* en définissant la période d’ouverture hors connexion à 40 jours. (Voir [Modification des stratégies](/help/forms/developing/protecting-documents-policies.md#modifying-policies).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 public class ModifyPolicySoap {
 
     public static void main(String[] args) {
         try
           {
                 //Set connection properties required to invoke AEM Forms using SOAP mode
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
                 //Create a ServiceClientFactory object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
                 //Create a RightsManagementClient object
                 RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
                 //Create a policy manager instance
                 PolicyManager policyManager = rightsClient.getPolicyManager();
 
                 //Retrieve an existing policy
                 Policy myPolicy = policyManager.getPolicy(
                     "Global Policy Set",
                     "Allow Copy") ;
 
                 //Modify policy attributes
                 myPolicy.setOfflineLeasePeriod(40);
                 myPolicy.setTracked(true);
 
                 //Set the validity period to 40 days
                 ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
                 validityPeriod.setRelativeExpirationDays(40);
                 myPolicy.setValidityPeriod(validityPeriod);
 
                 //Update the policy
                 policyManager.updatePolicy(myPolicy) ;
                   }
 
         catch (Exception ee)
             {
              ee.printStackTrace();
             }
     }
 }
```

## Début rapide (mode SOAP) : Suppression d’une stratégie à l’aide de l’API Java {#quick-start-soap-mode-deleting-a-policy-using-the-java-api}

L’exemple de code Java suivant supprime une stratégie nommée *Autoriser la copie*. (Voir [Suppression de stratégies](/help/forms/developing/protecting-documents-policies.md#deleting-policies).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class DeletePolicy {
 
     public static void main(String[] args) {
      try
       {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
          RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
          //Create a policy manager instance
          PolicyManager policyManager = rightsClient.getPolicyManager();
 
          //Delete the AllowCopy policy
          policyManager.deletePolicy("Global Policy Set", "Allow Copy") ;
           }
     catch (Exception ee)
         {
          ee.printStackTrace();
         }
     }
 }
 
```

## Début rapide (mode SOAP) : Application d’une stratégie à un document PDF à l’aide de l’API Java {#quick-start-soap-mode-applying-a-policy-to-a-pdf-document-using-the-java-api}

L’exemple de code Java suivant applique une stratégie nommée *Allow Copy* à un document PDF nommé *Loan.pdf*. Le jeu de stratégies auquel la stratégie est ajoutée est nommé *Jeu de stratégies global*. Le document protégé par une stratégie est enregistré en tant que fichier PDF nommé *PolicyProtectedLoanDoc.pdf. *(Voir [Application de stratégies aux Documents PDF](/help/forms/developing/protecting-documents-policies.md#applying-policies-to-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ApplyPolicySoap {
 
     public static void main(String[] args) {
     try
      {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a PDF document to which a policy is applied
         FileInputStream is = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Apply a policy to the PDF document
         RMSecureDocumentResult rmSecureDocument =  documentManager.protectDocument(
             inPDF,
             "LoanPDF",
             "Global Policy Set",
             "Allow Copy",
             null,
             null,
             null);
 
         //Retrieve the policy-protected PDF document
         Document protectPDF = rmSecureDocument.getProtectedDoc();
 
         //Save the policy-protected PDF document
         File myFile = new File("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         protectPDF.copyToFile(myFile);
       }
     catch (Exception ee)
      {
         ee.printStackTrace();
      }
     }
 }
```

## Début rapide (mode SOAP) : Suppression d’une stratégie d’un document PDF à l’aide de l’API Java {#quick-start-soap-mode-removing-a-policy-from-a-pdf-document-using-the-java-api}

L’exemple de code suivant supprime une stratégie d’un document PDF nommé *PolicyProtectedLoanDoc.pdf*. Le document PDF non sécurisé est enregistré sous *unProtectedLoan.pdf*. (Voir [Suppression de stratégies des Documents PDF](/help/forms/developing/protecting-documents-policies.md#removing-policies-from-pdf-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 
 public class RemovePolicy {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected PDF document from which to remove a policy
             FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Remove a policy from the policy-protected PDF document
             Document unsecurePDF =  documentManager.removeSecurity(inPDF);
 
             //Save the unsecured PDF document
             File myFile = new File("C:\\Adobe\UnProtectedLoan.pdf");
             unsecurePDF.copyToFile(myFile);
           }
 
          catch (Exception ee)
          {
           ee.printStackTrace();
          }
     }
 }
 
```

## Début rapide (mode SOAP) : Révocation d’un document à l’aide de l’API Java {#quick-start-soap-mode-revoking-a-document-using-the-java-api}

L’exemple de code Java suivant révoque un document protégé par une stratégie nommé *PolicyProtectedLoanDoc.pdf*. Un document PDF révisé se trouve à l’emplacement URL suivant `https://'[server]:[port]'/RightsManagement/UpdatedLoan.pdf`. (Voir [Révocation de l’accès aux Documents](/help/forms/developing/protecting-documents-policies.md#revoking-access-to-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 import java.net.URL;
 
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 
 public class RevokeDocument {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a policy-protected PDF document to revoke
         FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Obtain the license identifier value of the policy-protected document
         String revokeLic = documentManager.getLicenseId(inPDF);
 
         //Create a LicenseManager object
         LicenseManager licManager = rightsClient.getLicenseManager();
 
         //Specify the URL to where an updated document is located
         URL myURL = new URL("https://'[server]:[port]'/RightsManagement/UpdatedLoan.pdf");
 
         //Revoke the policy-protected PDF document
         licManager.revokeLicense(revokeLic, License.DOCUMENT_REVISED, myURL);
         }
      catch (Exception ee)
        {
             ee.printStackTrace();
        }
     }
 }
 
```

## Début rapide (mode SOAP) : Contrôle des documents PDF protégés par une stratégie à l’aide de l’API Java {#quick-start-soap-mode-inspecting-policy-protected-pdf-documents-using-the-java-api}

L’exemple de code Java suivant inspecte un document PDF protégé par une stratégie nommé *PolicyProtectedLoanDoc.pd* f. (Voir [Inspection des Documents PDF protégés par une stratégie](/help/forms/developing/protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 
 import java.io.FileInputStream;
 import java.util.Properties;
 import java.util.Date;
 import java.util.Calendar;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.*;
 
 public class InspectDocument {
 
     public static void main(String[] args) {
 
          try
           {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected PDF document to inspect
             FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Inspect the policy-protected document
             RMInspectResult inspectResult = documentManager.inspectDocument(inPDF);
 
             //Get the document name
             String documentName = inspectResult.getDocName();
 
             //Get the name of the policy
             String policyName = inspectResult.getPolicyName();
 
             //Get the name of the document publisher
             String pubName = inspectResult.getPublisherName();
 
             //Display the name of the policy-protected document and the policy
             System.out.println("The policy protected document "+documentName +" is protected with the policy "+policyName +". The name of the publisher is "+pubName+".");
 
               }
         catch (Exception ee)
             {
              ee.printStackTrace();
             }
     }
 }
 
 
```

## Début rapide (mode SOAP) : Rétablissement de l’accès à un document révoqué à l’aide de l’API Java {#quick-start-soap-mode-reinstating-access-to-a-revoked-document-using-the-java-api}

L’exemple de code Java suivant rétablit l’accès à un document PDF révoqué nommé *PolicyProtectedLoanDoc.pdf*. (Voir [Rétablissement de l&#39;accès aux Documents révoqués](/help/forms/developing/protecting-documents-policies.md#reinstating-access-to-revoked-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ReinstateDocument {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a revoked PDF document
         FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Obtain the license identifier value of the revoked PDF document
         String revokeLic = documentManager.getLicenseId(inPDF);
 
         //Create a LicenseManager object
         LicenseManager licManager = rightsClient.getLicenseManager();
 
         //Reinstate access to the revoked document
         licManager.unrevokeLicense(revokeLic);
         }
      catch (Exception ee)
        {
             ee.printStackTrace();
        }
     }
 }
 
```

## Début rapide (mode SOAP) : Création d’un filigrane PDF à l’aide de l’API Java {#quick-start-soap-mode-creating-a-pdf-watermark-using-the-java-api}

L’exemple de code Java suivant crée un filigrane PDF nommé &quot;Exemple de filigrane PDF&quot;. Ce filigrane contient un seul élément (voir [Création de filigranes](/help/forms/developing/protecting-documents-policies.md#creating-watermarks)).

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.util.Properties;
import com.adobe.edc.sdk.SDKException;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
import com.adobe.livecycle.rightsmanagement.client.WatermarkManager;
import com.adobe.livecycle.rightsmanagement.client.infomodel.InfomodelObjectFactory;
import com.adobe.livecycle.rightsmanagement.client.infomodel.PDRLException;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2Element;

public class PDFWatermarksSOAPMode {
    public static void main(String[] args) {
        // Set connection properties required to invoke Adobe AEM Forms
        // using SOAP mode
        try {
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'/");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE,
                    ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory object.
            ServiceClientFactory serviceClient = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a Document Security ServiceClient object.
            RightsManagementClient rmClient = new RightsManagementClient(
                    serviceClient);
            // Get the watermark manager which is used to add, delete or update
            // watermarks.
            WatermarkManager watermarkManager = rmClient.getWatermarkManager();

            // Registering and adding elements to the new watermarks.
            // Create a Watermark2 object using the InfomodelObjectFactory.
            Watermark2 newWatermark = InfomodelObjectFactory.createWatermark2();
            // Create a Watermark2Element object using the
            // InfomodelObjectFactory.
            Watermark2Element element1 = InfomodelObjectFactory
                    .createWatermark2Element();
            // Set the various properties such as name, description,custom text
            // and date.
            element1.setName("PDF element");
            element1.setDescription("This is a Sample PDF element.");
            // Set type of the watermark to Watermark2Element.TYPE_PDF.
            element1.setType(Watermark2Element.TYPE_PDF);
            // Create an IDf document form a PDF file.
            Document doc = new Document(new FileInputStream("C:\\Sample.pdf"));
            element1.setPDFContent(doc, "Watermark Doc");
            // Set the properties for this such rotation,opacity.
            element1.setOpacity(50);
            element1.setRotation(45);//45 degrees rotation.
            element1.setStartPage(5);
            element1.setStartPage(15);//Watermark appears only on pages 10 to 15.
            // Add it to the watermark.
            newWatermark.addWatermarkElement(element1);
            // Set the watermark name.
            newWatermark.setName("Sample PDF Watermark");
            // Register it.
            watermarkManager.registerWatermark2(newWatermark);
        } catch (PDRLException e) {
            System.out.println(e.getCause());
        } catch (SDKException e) {
            e.printStackTrace();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Création d’un filigrane de texte à l’aide de l’API Java {#quick-start-soap-mode-creating-a-text-watermark-using-the-java-api}

L’exemple de code Java suivant crée un filigrane de texte nommé *Exemple de filigrane de texte*. Ce filigrane contient un seul élément.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */

import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
import com.adobe.livecycle.rightsmanagement.client.WatermarkManager;
import com.adobe.livecycle.rightsmanagement.client.infomodel.InfomodelObjectFactory;
import com.adobe.livecycle.rightsmanagement.client.infomodel.PDRLException;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2Element;
import com.adobe.edc.sdk.SDKException;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import java.util.Properties;

public class TextWatermarks {
    public static void main(String[] args) {
        try {
            // Set connection properties required to invoke Adobe Document
            // Services using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'/");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE,
                    ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory object.
            ServiceClientFactory serviceClient = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a Document Security ServiceClient object.
            RightsManagementClient rmClient = new RightsManagementClient(
                    serviceClient);
            // Get the watermark manager which is used to add, delete or update
            // watermarks.
            WatermarkManager watermarkManager = rmClient.getWatermarkManager();

            // Registering and adding elements to the new watermarks.
            // Create a Watermark2 object using the InfomodelObjectFactory.
            Watermark2 newWatermark = InfomodelObjectFactory.createWatermark2();
            // Create a Watermark2Element object using the
            // InfomodelObjectFactory.
            Watermark2Element element1 = InfomodelObjectFactory
                    .createWatermark2Element();
            // Set the various properties such as name, description,custom text
            // and date.
            element1.setName("First element");
            element1.setDescription("This is a Sample Text Watermark Element.");
            element1.setUserNameIncluded(true);
            element1.setShowOnPrint(false);// This element will not appear on
                                            // print, but will only appear on
                                            // screen.
            // Set the type of the watermark element. It can either be
            // Watermark2Element.TYPE_TEXT or Watermark2Element.TYPE_PDF.
            element1.setType(Watermark2Element.TYPE_TEXT);
            // Provide opacity, rotation page range and other such settings.
            element1.setOpacity(50); // Opacity set to 50%.
            element1.setEndPage(1);// The watermark will appear only on first
                                    // page, start page is 1 by default.

            // Create a new element.
            Watermark2Element element2 = InfomodelObjectFactory
                    .createWatermark2Element();
            element2.setName("Second element");
            element2.setCustomText("Confidential");
            // Set type to Watermark2Element.TYPE_TEXT.
            element2.setType(Watermark2Element.TYPE_TEXT);
            // Provide opacity, rotation page range and other such settings.
            element2.setFontName("Times New Roman");
            element2.setFontSize(30);
            element2.setOpacity(30);// 30% opacity.
            element2.setRotation(45);// 45 degrees rotation.
            element2.setShowOnScreen(false);// This element will not appear on
                                            // screen, but will appear when we
                                            // print the document.

            // Add these elements to the watermark in the order in you want them
            // to be applied.
            newWatermark.addWatermarkElement(element1);// Will be applied first.
            newWatermark.addWatermarkElement(element2);// Will be applied on top
                                                        // of it.
            newWatermark.setName("Sample Text Watermark");
            watermarkManager.registerWatermark2(newWatermark);
        } catch (PDRLException e) {
            System.out.println(e.getCause());
        } catch (SDKException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Modification d’un filigrane de texte à l’aide de l’API Java {#quick-start-soap-mode-modifying-a-text-watermark-using-the-java-api}

L’exemple de code Java suivant modifie un filigrane nommé &quot;Exemple de filigrane de texte&quot; et définit l’opacité du premier élément sur 100.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */

import java.util.*;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class ModifyWatermarks {

    public static void main(String[] args) {
        try {
            // Set connection properties required to invoke AEM Forms using
            // SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(
                    factory);

            // Create a WatermarkManager object
            WatermarkManager myWatermarkManager = rightsClient
                    .getWatermarkManager();

            // Get the watermark to modify by name
            Watermark2 myWatermark = myWatermarkManager
                    .getWatermarkByName2("Sample Text Watermark");

            // Get the elements in the watermark.
            ArrayList<Watermark2Element> elements = myWatermark
                    .getWatermarkElements();
            // Iterate through the list and modify the opacity attribute of each
            // element.
            for (Iterator<Watermark2Element> iter = elements.iterator(); iter
                    .hasNext();) {
                Watermark2Element elem = iter.next();
                elem.setOpacity(100);
            }
            // Update the watermark
            myWatermarkManager.updateWatermark2(myWatermark);
        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Modification d’un filigrane à l’aide de l’API Java {#quick-start-soap-mode-modifying-a-watermark-using-the-java-api}

L’exemple de code Java suivant modifie un filigrane nommé *Confidential* en remplaçant la valeur de l’attribut `opacity` par 80.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
    * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 
 public class ModifyWatermarks {
 
     public static void main(String[] args) {
 
     try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Create a WatermarkManager object
         WatermarkManager myWatermarkManager =  rightsClient.getWatermarkManager();
 
         //Get the watermark to modify by name
         Watermark myWatermark = myWatermarkManager.getWatermarkByName("Confidential");
 
         //Modify the opacity attribute
         myWatermark.setOpacity(80);
 
         //Update the watermark
         myWatermarkManager.updateWatermark(myWatermark);
         }
 
     catch (Exception ex)
         {
         ex.printStackTrace();
         }
     }
 }
 
```

## Début rapide (mode SOAP) : Recherche de événements à l’aide de l’API Java {#quick-start-soap-mode-searching-for-events-using-the-java-api}

L’exemple de code Java suivant recherche le événement de création de stratégie.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.Event;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.EventSearchFilter;
 
 public class SearchEvents {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Create a EventManager instance
         EventManager eventManager = rightsClient.getEventManager();
 
         //Create a EventSearchFilter object
         EventSearchFilter eventSearchFilter = new EventSearchFilter();
 
         //Search for the POLICY_CREATE_EVENT event
         eventSearchFilter.setEventCode(EventManager.POLICY_CREATE_EVENT);
         Event[] events = eventManager.searchForEvents(eventSearchFilter,20) ;
 
         //Retrieve information about each event
         int index = events.length;
         Calendar rightNow = Calendar.getInstance();
 
         for (int i=0; i<index;i++)
         {
             Event myEvent = events[i];
 
             Date myDate = myEvent.getTimestamp();
             rightNow.setTime(myDate);
             System.out.println("Policy Created on " + rightNow.getTime().toString());
         }
          }
     catch (Exception ee)
         {
          ee.printStackTrace();
         }
     }
 }
 
```

## Début rapide (SOAP) : Application d’une stratégie à un document Word à l’aide de l’API Java {#quick-start-soap-applying-a-policy-to-a-word-document-using-the-java-api}

L’exemple de code Java suivant applique une stratégie nommée *Allow Copy* à un document Word nommé *Loan.doc*. Le jeu de stratégies auquel la stratégie est ajoutée est nommé *Jeu de stratégies global*. Le document protégé par une stratégie est enregistré en tant que fichier DOC nommé *PolicyProtectedLoanDoc.doc. *(Voir [Application de stratégies aux Documents PDF](/help/forms/developing/protecting-documents-policies.md#applying-policies-to-pdf-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ApplyPolicyWordDocument {
 
     public static void main(String[] args) {
     try
      {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a Word document to which a policy is applied
         FileInputStream is = new FileInputStream("C:\\Adobe\Loan.doc");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Apply a policy to the Word document
         RMSecureDocumentResult rmSecureDocument=  documentManager.protectDocument(
             inPDF,
             "Loan.doc",
             "Global Policy Set",
             "Allow Copy",
             null,
             null,
             null);
 
         //Retrieve the policy-protected Word document
         Document protectPDF = rmSecureDocument.getProtectedDoc();
 
         //Save the policy-protected Word document
         File myFile = new File("C:\\PolicyProtectedLoanDoc.doc");
         protectPDF.copyToFile(myFile);
       }
     catch (Exception ee)
      {
         ee.printStackTrace();
      }
     }
 }
 
```

## Début rapide (mode SOAP) : Suppression d’une stratégie d’un document Word à l’aide de l’API Java {#quick-start-soap-mode-removing-a-policy-from-a-word-document-using-the-java-api}

L&#39;exemple de code suivant supprime une stratégie d&#39;un document Word nommé *PolicyProtectedLoanDoc.doc*. Le document Word non sécurisé est enregistré sous *unProtectedLoan.doc*. (Voir [Suppression de stratégies des Documents Word](/help/forms/developing/protecting-documents-policies.md#removing-policies-from-word-documents).)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdkK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 
 public class RemovePolicyWordDocument {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected Word document from which to remove a policy
             FileInputStream is = new FileInputStream("C:\\PolicyProtectedLoanDoc.doc");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Remove a policy from the policy-protected Word document
             Document unsecurePDF =  documentManager.removeSecurity(inPDF);
 
             //Save the unsecured Word document
             File myFile = new File("C:\\Adobe\UnProtectedLoan.doc");
             unsecurePDF.copyToFile(myFile);
           }
 
          catch (Exception ee)
          {
           ee.printStackTrace();
          }
     }
 }
 
 
```

## Début rapide (mode SOAP) : Création d’une stratégie abstraite à l’aide de l’API Java {#quick-start-soap-mode-creating-an-abstract-policy-using-the-java-api}

L’exemple de code Java suivant crée une nouvelle stratégie abstraite appelée AllowCopy. Le jeu de stratégies auquel la stratégie est ajoutée est nommé Jeu de stratégies global. Ce jeu de stratégies existe par défaut. (voir Création de stratégies).

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */

import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class CreateAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke forms server using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicy abstractPolicy = InfomodelObjectFactory.createAbstractPolicy();

        abstractPolicy.setName("AllowCopy");
        abstractPolicy.setDescription("This abstract policy helps users to create policy that copy information from the PDF document");
        abstractPolicy.setPolicySetName("Global Policy Set");

        abstractPolicy.setOfflineLeasePeriod(30);
        abstractPolicy.setTracked(true);
        abstractPolicy.setEncryptAttachmentsOnly(false);

        ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
        validityPeriod.setRelativeExpirationDays(30);

        abstractPolicy.setValidityPeriod(validityPeriod);

        //Adding publisher permissions.
        AbstractPolicyEntry userPolicyEntry = InfomodelObjectFactory.createAbstractPolicyEntry();

        Permission onlinePermission = InfomodelObjectFactory.createPermission(Permission.OPEN_ONLINE);
        Permission copyPermission = InfomodelObjectFactory.createPermission(Permission.COPY);

        userPolicyEntry.addPermission(onlinePermission);
        userPolicyEntry.addPermission(copyPermission);

        abstractPolicy.addAbstractPolicyEntry(userPolicyEntry);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        abstractPolicyManager.registerAbstractPolicy(abstractPolicy, "Global Policy Set");

        AbstractPolicy abstractPolicy1 = abstractPolicyManager.getAbstractPolicy("Global Policy Set","AllowCopy");

        System.out.println("The Abstract Policy was successfully created:" + abstractPolicy1.getName());

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Modification d’une stratégie abstraite à l’aide de l’API Java {#quick-start-soap-mode-modifying-an-abstract-policy-using-the-java-api}

L’exemple de code Java suivant modifie une stratégie abstraite nommée AllowCopy. Le jeu de stratégies dans lequel la stratégie est modifiée est nommé Jeu de stratégies global. Ce jeu de stratégies existe par défaut. (voir Création de stratégies).

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */
import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class ModifyingAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke forms server using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        AbstractPolicy abstractPolicy = abstractPolicyManager.getAbstractPolicy("Global Policy Set","AllowCopy");

        //Modify policy attributes
        abstractPolicy.setOfflineLeasePeriod(40);
        abstractPolicy.setTracked(true);

        //Set the validity period to 40 days
        ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
        validityPeriod.setRelativeExpirationDays(40);
        abstractPolicy.setValidityPeriod(validityPeriod);

        abstractPolicyManager.updateAbstractPolicy(abstractPolicy);

        System.out.println("The Abstract Policy was updated:" + abstractPolicy.getName());

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Suppression d’une stratégie abstraite à l’aide de l’API Java {#quick-start-soap-mode-deleting-an-abstract-policy-using-the-java-api}

L&#39;exemple de code Java suivant supprime une stratégie abstraite nommée AllowCopy. Le jeu de stratégies à partir duquel la stratégie est supprimée est nommé Jeu de stratégies global. Ce jeu de stratégies existe par défaut. (voir Création de stratégies).

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming with AEM Forms
 * with forms server
 */
import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;

public class DeleteAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke AEM Forms using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        abstractPolicyManager.deleteAbstractPolicy("Global Policy Set", "AllowCopy");

        System.out.println("The Abstract Policy was deleted:");

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## Début rapide (mode SOAP) : Protect d’un PDF dans le flux de travail des instructions pour un utilisateur existant, à l’aide de l’API Java {#quick-start-soap-mode-protect-a-pdf-in-statement-workflow-for-an-existing-user-using-the-java-api}

L’exemple de code Java suivant illustre la méthode de protection d’un Document dans le flux de travail des instructions pour un utilisateur existant.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */
import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
import com.adobe.edc.common.dto.PublishLicenseDTO;

public class protectStatementWorkFlowExistingUserSoap {

    public static void main(String args[]) {

        try{

            //Set connection properties required to invoke forms server using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

            //Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

            //Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(factory);

            DocumentManager documentManager = rightsClient.getDocumentManager();

            //Reference a PDF document to which a policy is applied
            FileInputStream is = new FileInputStream("C:\\Adobe\\Sample.pdf");
            Document inPDF = new Document(is);

            //Get the License for existing user
            PublishLicenseDTO publishLicense = documentManager.getPublishLicenseForUser("DefaultDom","wblue");

            //protect the PDF document using license
            RMSecureDocumentResult rmSecureDocument = documentManager.protectDocument(inPDF, publishLicense);

            //Retrieve the policy-protected PDF document
            Document protectedDocument = rmSecureDocument.protectedDoc;

            //Save the policy-protected PDF document
            String outputFile = "C:\\Adobe\\PolicyProtectedSample.pdf";
            File myFile = new File(outputFile);
            protectedDocument.copyToFile(myFile);

            System.out.println("Protected the PDF With policy");

        }catch(Exception ex){
            ex.printStackTrace();
        }

}

}
```

## Début rapide (mode SOAP) : Protect a PDF in Statement Workflow for a new User, using Java API {#quick-start-soap-mode-protect-a-pdf-in-statement-workflow-for-a-new-user-using-the-java-api}

L’exemple de code Java suivant montre comment protéger un document dans le flux de travail des instructions. Il s&#39;agit d&#39;un processus en deux étapes :

* Un nouvel utilisateur, une nouvelle licence et une nouvelle stratégie sont créés.
* L’utilisateur est associé à la licence et à la stratégie et le document est protégé.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7.  commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote forms server instance and there is a
 * firewall between the client application and forms server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with forms server
 */
import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;

import com.adobe.idp.um.api.infomodel.PrincipalSearchFilter;
import com.adobe.idp.um.api.infomodel.PrincipalReference;
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
import com.adobe.edc.common.dto.PublishLicenseDTO;
import com.adobe.idp.um.api.infomodel.User;
import com.adobe.idp.um.api.impl.UMBaseLibrary;

public class protectStatementWorkFlowSoap {

    public static void main(String args[]) {

        try{

            //Set connection properties required to invoke forms server using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

            //Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

            //Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(factory);

            DirectoryManagerServiceClient directoryManagerServiceClient = new DirectoryManagerServiceClient(factory);

            DocumentManager documentManager = rightsClient.getDocumentManager();

            AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

            //Reference a PDF document to which a policy is applied
            FileInputStream is = new FileInputStream("C:\\Adobe\\Sample.pdf");
            Document inPDF = new Document(is);

            //Create user
            String userName = "wblue";
            User user = UMBaseLibrary.createUser(userName, "DefaultDom", userName);
            user.setCommonName(userName);
            user.setGivenName(userName);
            user.setFamilyName("User");
            directoryManagerServiceClient.createLocalUser(user, "password");

            //Ensure that the user was added
            //Create a PrincipalSearchFilter to find the user by ID
            List userList = new ArrayList<PrincipalReference>();
            PrincipalSearchFilter psf = new PrincipalSearchFilter();
            psf.setUserIdAbsolute(user.getUserid());
            psf.setRetrieveOnlyActive();
            List p = directoryManagerServiceClient.findPrincipalReferences(psf);
            PrincipalReference principal = (PrincipalReference)(p.get(0));
            userList.add(principal);

            //Create Policy From AbstractPolicy "test2"
            String newPolicyId = abstractPolicyManager.createPolicyFromAbstractPolicy("Global Policy Set", "PolicyFromAbstractPolicy_AllowCopy","Global Policy Set", "AllowCopy", userList);

            System.out.println("Created policy from abstract policy: " + newPolicyId);

            //Create License for the Policy
            PublishLicenseDTO publishLicense = documentManager.createLicense(newPolicyId, user.getUserid(), "DefaultDom");

            //get the license id from license object
            String licID = publishLicense.getLicenseId();

            //Associate User with License and Policy
            documentManager.associateUserWithLicenseAndPolicy("DefaultDom", user.getUserid(), licID, newPolicyId);

            //protect the PDF document using license
            RMSecureDocumentResult rmSecureDocument = documentManager.protectDocument(inPDF, publishLicense);

            //Retrieve the policy-protected PDF document
            Document protectedDocument = rmSecureDocument.protectedDoc;

            //Save the policy-protected PDF document
            String outputFile = "C:\\Adobe\\PolicyProtected"+ user.getUserid()+".pdf";
            File myFile = new File(outputFile);
            protectedDocument.copyToFile(myFile);

            System.out.println("Protected the PDF With policy");

        }catch(Exception ex){
            ex.printStackTrace();
        }

}

}
```

