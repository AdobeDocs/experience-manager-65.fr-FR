---
title: Protection d’un document au nom d’une autre personne
description: Découvrez comment le SDK Java&trade; d’AEM Forms Document Security propose des API pour un compte d’utilisateur afin de protéger un document au nom d’un autre utilisateur ou d’une autre utilisatrice.
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
exl-id: e5c80569-d3c0-4358-9b91-b98a64d1c004
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 100%

---

# Protection d’un document au nom d’une autre personne {#protect-a-document-on-behalf-of-another-user}

Le SDK Java™ d’AEM Forms Document Security fournit des API pour permettre à un compte d’utilisateur de protéger un document au nom d’un autre utilisateur ou d’une autre utilisatrice sans avoir les autorisations de modifier le document. Vous pouvez utiliser les API dans un processus de workflow ou par programmation en tant que service de document. Les nouvelles API sont les suivantes :

* **ProtectDocument :** utilisez l’API ProtectDocument pour appliquer une politique à un document au nom

  d’un autre compte d’utilisateur. Les autorisations du compte d’utilisateur utilisé pour appliquer la politique restent limitées à la protection du document. Cela n’octroie pas le droit d’ouvrir et d’afficher le document. RMSecureDocumentResult protectDocument(Document inDoc, String documentName, String policySetName, String policyName, RMLocale locale, boolean bExactMatchForNames)

* **createLicense :** utilisez l’API CreateLicense afin de créer une licence pour une politique au nom d’un autre compte d’utilisateur. PublishLicenseDTO createLicense(String policyId, String documentName, boolean logSecureDocEvent)
* **protectDocumentWithCoverPage :** utilisez l’API ProtectDocumentWithCoverPage pour appliquer une politique et ajouter une page de garde à un document au nom d’un autre utilisateur. Les autorisations du compte d’utilisateur utilisé pour appliquer la politique restent limitées à la protection du document. Cela n’octroie pas le droit d’ouvrir et d’afficher le document. RMSecureDocumentResult protectDocumentWithCoverPage(Document inDoc, String documentName, String policySetName, String policyName, Document coverDoc, boolean bExactMatchForNames)

## Utilisation des API pour protéger un document au nom d’une autre personne {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

Procédez comme suit pour protéger un document au nom d’un autre utilisateur ou d’une autre utilisatrice et sans obtenir les autorisations nécessaires pour le modifier :

1. Créez un jeu de politiques Par exemple, JeuPolitiques1.
1. Créez une politique dans le jeu de politiques nouvellement créé. Par exemple, Politique1 dans JeuPolitiques1.
1. Créez un utilisateur ou une utilisatrice avec le rôle Utilisateur final ou utilisatrice finale de Rights Management. Par exemple, User1. Fournissez les autorisations pour afficher les documents protégés à l’aide de Politique1 pour l’utilisateur nouvellement créé.
1. Créez un rôle. Par exemple, Role1. Octroyez l’autorisation d’appel de service au rôle nouvellement créé. Créez un utilisateur ou une utilisatrice avec le rôle nouvellement créé. Par exemple, User2. Vous pouvez utiliser User2 ou un administrateur ou une administratrice pour créer une connexion SDK et appeler le service protectDocument.

   Vous pouvez désormais exécuter l’exemple de code suivant pour protéger un document sans fournir les autorisations nécessaires pour modifier le document à l’utilisateur ou à l’utilisatrice qui le protège :

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```
