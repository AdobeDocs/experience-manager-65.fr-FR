---
title: Débuts rapides de l’API du service Forms
seo-title: Débuts rapides de l’API du service Forms
description: Utilisez les Débuts rapides pour l’API du service Forms.
seo-description: Utilisez les Débuts rapides pour l’API du service Forms.
uuid: dfce259a-e392-4929-ad7e-6d902faceaeb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 9fe48243-24c6-4e08-9886-148cd99dec87
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---


# Débuts rapides de l’API du service Forms {#forms-service-api-quick-starts}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Les Débuts rapides suivants sont disponibles pour le service Forms :

[Début rapide (mode SOAP) : Rendu d’un formulaire PDF interactif à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api)

[Début rapide (mode SOAP) : Rendu d’un formulaire sur le client à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Début rapide (mode SOAP) : Rendu d’un formulaire basé sur des fragments à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Début rapide (mode SOAP) : Rendu d’un formulaire avec droits d’utilisation à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Début rapide (mode SOAP) : Rendu d’un formulaire HTML à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Début rapide (mode SOAP) : Rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Début rapide (mode SOAP) : Gestion des PDF forms envoyés en tant que XML à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Début rapide (mode SOAP) : Gestion des PDF forms envoyés au format PDF à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Début rapide (mode SOAP) : Gestion des formulaires HTML envoyés en tant que XML à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Début rapide (mode SOAP) : Création de Documents PDF avec des données XML envoyées à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)

[Début rapide (mode SOAP) : Préremplissage de Forms avec des dispositions souple à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Début rapide (mode SOAP) : Gestion d’un formulaire contenant un script de calcul à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api)

[Début rapide (mode SOAP) : Optimisation des performances à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Début rapide (mode SOAP) : Rendu par valeur à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Début rapide (mode SOAP) : Transmission de documents au service Forms à l’aide de l’API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

La logique d’application qui utilise l’API du service Forms est implémentée en tant que servlets Java. Les opérations AEM Forms peuvent être effectuées à l’aide de l’API AEM Forms fortement typée et le mode de connexion doit être défini sur SOAP.

>[!NOTE]
>
>Les débuts rapides situés dans Programmation avec v sont basés sur le serveur Forms puisque vous utilisez un autre système d’exploitation, tel que Unix, remplacez les chemins spécifiques Windows par les chemins pris en charge par le système d’exploitation approprié. De même, si vous utilisez un autre serveur d’applications J2EE, assurez-vous de spécifier des propriétés de connexion valides. Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Conseil** : Le site Web Adobe Developer contient l&#39;article suivant qui explique comment créer une application ASP.NET qui appelle le service Forms et effectue le rendu des formulaires. Voir [Création d&#39;applications ASP.NET de rendu de formulaire](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).

## Début rapide (mode SOAP) : Rendu d’un formulaire PDF interactif à l’aide de l’API Java {#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api}

L’exemple de code suivant rend un formulaire PDF interactif nommé *Loan.xdp* à un navigateur Web client. Un fichier est joint au formulaire. Notez que la conception de formulaire fait partie d’une application et est référencée à l’aide de la valeur URI racine de contenu `repository:///`. (Voir [Rendu des PDF forms interactifs](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFForm extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Set run-time options using a PDFFormRenderSpec instance
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
             pdfFormRenderSpec.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Specify file attachments to attach to the form
             FileInputStream fileAttachment = new FileInputStream("C:\\rideau1.jpg");
             Document attachment1 = new Document(fileAttachment);
             String fileName = "rideau1.jpg";
             Map fileAttachments = new HashMap();
             fileAttachments.put(fileName, attachment1);
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         fileAttachments            //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse objects content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 }
```

## Début rapide (mode SOAP) : Rendu d’un formulaire sur le client à l’aide de l’API Java {#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api}

L’exemple de code suivant présente un formulaire nommé *Loan.xdp* au client à l’aide de l’API Java du service Forms. Notez que la conception de formulaire fait partie d’une application et est référencée à l’aide de la valeur URI racine de contenu `repository:///`. (Voir [Rendu de Forms sur le client](/help/forms/developing/rendering-forms.md#rendering-forms-at-the-client).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFFormClient extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values required by the renderPDFForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set a run-time option required to render a form on the client
         PDFFormRenderSpec pdfRenderSpec = new PDFFormRenderSpec();
         pdfRenderSpec.setRenderAtClient(RenderAtClient.Yes);
 
         //Specify URI values required to render a form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method to render
         //an interactive PDF form on the client
         FormsResult formOut = formsClient.renderPDFForm(
                 formName,
                 oInputData,
                 pdfRenderSpec,
                 uriValues,
                 null
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
          }
     }
 }
 
```

## Début rapide (mode SOAP) : Rendu d’un guide (obsolète) à l’aide de l’API Java {#quick-start-soap-mode-rendering-a-guide-deprecated-using-the-java-api}

L’exemple de code suivant montre comment rendre un Guide (obsolète) nommé *TLALifeClaim.xdp* à un navigateur Web client.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import java.io.InputStream;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormGuide extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
     try{
 
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Specify the parameters for the renderActivityGuide method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/TLALifeClaim.xdp";
         byte[] cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Cache the PDF form
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set Form Guide run-time options
         ActivityGuideRenderSpec renderSpec = new ActivityGuideRenderSpec();
         renderSpec.setGuidePDF(false);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
 
         //Invoke the renderFormGuide method
         FormsResult formOut = formsClient.renderFormGuide(
                 formName,            //formQuery
                 oInputData,          //inDataDoc
                 pdfFormRenderSpec,    //pdfFormRenderSpec
                 renderSpec,           //activityGuideRenderSpec
                 uriValues              //urlSpec
                 );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
     }catch (Exception e) {
              System.out.println("The following exception occured: "+e.getMessage());
               }
      }
 }
 
```

## Début rapide (mode SOAP) : Rendu d’un formulaire basé sur des fragments à l’aide de l’API Java {#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api}

L’exemple de code suivant montre comment générer un formulaire basé sur des fragments. Le nom de la conception de formulaire est *PurchaseOrderDynamic.xdp* et se trouve dans le référentiel AEM Forms (le fichier XDP est stocké dans un dossier nommé FormsFolder situé dans le référentiel). Les fragments référencés par le formulaire POFragment doivent également être situés dans le référentiel. (Voir [Rendu de Forms basé sur des fragments](/help/forms/developing/rendering-forms.md#rendering-forms-based-on-fragments).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragments extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/PurchaseOrderDynamic.xdp";
 
             FileInputStream myFormData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
             Document oInputData = new Document(myFormData);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

## Début rapide (mode SOAP) : Rendu d’un formulaire avec droits d’utilisation à l’aide de l’API Java {#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api}

L’exemple de code suivant montre comment rendre un formulaire avec droits d’utilisation sur un navigateur Web client. Les droits d’utilisation définis dans cet exemple de code permettent à un utilisateur d’ajouter des commentaires dans le formulaire et d’enregistrer des données de formulaire. (Voir [Rendu de Forms prenant en charge les droits](/help/forms/developing/rendering-forms.md#rendering-rights-enabled-forms).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class RenderUsageRightsForms extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a FormsServiceClient object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values for the renderPDFFormWithUsageRights method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set run-time options
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set usage-rights run-time options
         ReaderExtensionSpec reOptions = new ReaderExtensionSpec();
         reOptions.setReCredentialAlias("RE2");
         reOptions.setReCommenting(true);
         reOptions.setReFillIn(true);
 
         //Specify URI values required to render the form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
         //Render a rights-enabled PDF form
         FormsResult formOut = formsClient.renderPDFFormWithUsageRights(
             formName,            //formQuery
             oInputData,          //inDataDoc
             pdfFormRenderSpec,   //renderFormOptionsSpec
             reOptions,              //applicationWebRoot
             uriValues            //targetURL
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
     }catch (Exception e) {
          System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
 
 
```

## Début rapide (mode SOAP) : Rendu d’un formulaire HTML à l’aide de l’API Java {#quick-start-soap-mode-rendering-an-html-form-using-the-java-api}

L’exemple de code suivant affiche un formulaire HTML à l’aide de l’API Java du service Forms. Une barre d’outils est ajoutée au formulaire HTML, ainsi que deux pièces jointes. En outre, la valeur de l&#39;agent utilisateur est obtenue à partir de l&#39;objet `HttpServletRequest`. (Voir [Rendu de Forms au format HTML](/help/forms/developing/rendering-forms.md#rendering-forms-as-html).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderHTMLForms extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
 
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
 
                 //Obtain the user agent value from the HttpServletRequest object
                 String userAgent = req.getHeader("user-agent");
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Set style information that controls the presentation of the HTML form
                 htmlRS.setStyleGenerationLevel(StyleGenerationLevel.InlineAndInternalStyles);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleSubmittedHTMLForm");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
                 }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
                      }
             }
 }
 
 
 
 
```

## Début rapide (mode SOAP) : Rendu d’un formulaire HTML utilisant un fichier CSS à l’aide de l’API Java {#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api}

L’exemple de code suivant génère un formulaire HTML à l’aide de l’API Client du service Forms. Le nom du fichier CSS personnalisé référencé est *custom.css*. (Voir [Rendu de Forms HTML à l’aide de fichiers CSS personnalisés](/help/forms/developing/rendering-forms.md#rendering-html-forms-using-custom-css-files).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 import java.io.FileInputStream;
 
 
 public class RenderHTMLCSS extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Specify a custom CSS file to use
                 htmlRS.setCustomCSSURI("C:\\Adobe\custom.css");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
             }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
              }
     }
 }
```

## Début rapide (mode SOAP) : Rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java {#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api}

L’exemple de code suivant affiche un formulaire HTML avec une barre d’outils en français. L’emplacement du fichier fscmenu.xml est C:\Adobe (ce dossier doit se trouver sur le serveur hébergeant AEM Forms). Notez que la valeur du paramètre régional est `fr_FR`. La section qui explique comment générer un formulaire HTML avec une barre d’outils personnalisée affiche la syntaxe du fichier fscmenu.xml utilisé dans ce début rapide. (Voir [Rendu de Forms HTML avec des barres d’outils personnalisées](/help/forms/developing/rendering-forms.md#rendering-html-forms-with-custom-toolbars).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderCustomToolbar extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the URI location of the
                 // fscmenu.xml file that contains French
                 htmlRS.setToolbarURI("C:\\Adobe");
 
                 //Specify the locale value
                 htmlRS.setLocale("fr_FR");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
                 }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
                      }
             }
 }
 
```

## Début rapide (mode SOAP) : Gestion des PDF forms envoyés en tant que XML à l’aide de l’API Java {#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api}

L’exemple de code suivant traite un formulaire envoyé au format XML. La valeur de type de contenu transmise à la méthode `processFormSubmission` est `CONTENT_TYPE=text/xml`. Les valeurs qui correspondent aux champs `mortgageAmount`, `lastName` et `firstName` s’affichent. Une méthode définie par l&#39;utilisateur, `getNodeText`, est utilisée dans ce début rapide. Il accepte une instance `org.w3c.dom.Document` et une valeur de chaîne qui spécifie le nom du noeud. Cette méthode renvoie une valeur de chaîne qui représente la valeur du noeud. (Voir [Gestion du Forms envoyé](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 9. commons-discovery.jar (required for SOAP mode)
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
               System.out.println("THE CONTENT TYPS IS" +myContentType);
 
                if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 }
              }
             }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
 
```

>[!NOTE]
>
>Lorsque vous utilisez un objet `com.adobe.idp.Document` et un `org.w3c.dom.Document` dans la même application, remplissez les conditions `org.w3c.dom.Document`.

## Début rapide (mode SOAP) : Gestion des PDF forms envoyés au format PDF à l’aide de l’API Java {#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api}

L’exemple de code suivant traite un formulaire envoyé en tant que données PDF. La valeur de type de contenu transmise à la méthode `processFormSubmission` est `CONTENT_TYPE=application/pdf`. Le formulaire envoyé est enregistré en tant que fichier PDF nommé *tempPDF.pdf*. En outre, comme le formulaire est envoyé au format PDF, les pièces jointes peuvent être récupérées. Toutes les pièces jointes sont enregistrées au format JPEG. (Voir [Gestion du Forms envoyé](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleSubmittedPDFData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/pdf",
             "",
             processSpec);
 
             //Determine if the form contains file attachments
             //It is assumed that file attachments are JPG files
             List fileAttachments = formOut.getAttachments();
 
             //Create an Iterator object and iterate through
             //the List object
             Iterator iter = fileAttachments.iterator();
             int i = 0 ;
             while (iter.hasNext()) {
                 Document file = (Document)iter.next();
                 file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg"));
                 i++;
             }
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/pdf")){
 
                     //Get the form data
                     Document myPDFfile = formOut.getOutputContent();
 
                     //Create a PDF object
                     File myPDFFile = new File("C:\\Adobe\tempPDF.pdf");
 
                     //Populate the PDF file
                     myPDFfile.copyToFile(myPDFFile);
                     pp.println("<p> The PDF file is saved as C:\\Adobe\tempPDF.pdf") ;
 
                 }
               }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 }
 
 
 
```

## Début rapide (mode SOAP) : Gestion des formulaires HTML envoyés en tant que XML à l’aide de l’API Java {#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api}

L’exemple de code suivant traite un formulaire HTML envoyé sous forme de données XML. La valeur de type de contenu transmise à la méthode `processFormSubmission` est `CONTENT_TYPE=application/x-www-form-urlencoded`. Les valeurs qui correspondent aux champs nommés `mortgageAmount`, `lastName` et `firstName` sont affichées. Une méthode définie par l&#39;utilisateur, `getNodeText`, est utilisée dans ce début rapide. Il accepte une instance `org.w3c.dom.Document` et une valeur de chaîne qui spécifie le nom du noeud. Cette méthode renvoie une valeur de chaîne qui représente la valeur du noeud. (Voir [Gestion du Forms envoyé](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 /*
     * This quick start handles data submitted as XML from a rendered HTML form
     */
 public class HandleSubmittedHTMLForm extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/x-www-form-urlencoded",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
 
                     //Get the form data
                     Document formOutput = formOut.getOutputContent();
                     InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                     //Create DocumentBuilderFactory and DocumentBuilder objects
                     DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                     DocumentBuilder builder = factory.newDocumentBuilder();
                     org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                     //Call for each field in the form
                     String Amount = getNodeText("mortgageAmount", myDOM);
                     String myLastName =  getNodeText("lastName", myDOM);
                     String myFirstName = getNodeText("firstName", myDOM);
 
                     //Write the form data to the web browser
                     pp.println("<p> The form data is :<br><br>" +
                             "<li> The mortgage amount is "+ Amount+"" +
                             "<li> Last name is "+ myLastName+"" +
                             "<li> First name is "+ myFirstName+"")    ;
                      }
                 }
             catch (Exception e) {
                  e.printStackTrace();
               }
         }
 
         //This method returns the value of the specified node
         private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
         {
           //Get the XML node by name
           NodeList oList = myDOM.getElementsByTagName(nodeName);
           Node myNode = oList.item(0);
           NodeList oChildNodes = myNode.getChildNodes();
 
          String sText = "";
          for (int i = 0; i < oChildNodes.getLength(); i++)
          {
              Node oItem = oChildNodes.item(i);
             if (oItem.getNodeType() == Node.TEXT_NODE)
              {
                sText = sText.concat(oItem.getNodeValue());
              }
          }
         return sText;
         }
     }
 
```

## Début rapide (mode SOAP) : Création de Documents PDF avec des données XML envoyées à l’aide de l’API Java {#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api}

L’exemple de code Java suivant traite les données de formulaire envoyées au format XML. Les données de formulaire sont récupérées à partir de l’envoi du formulaire à l’aide de l’API Forms et envoyées au service Output. Les données de formulaire et une conception de formulaire sont utilisées pour créer un document PDF non interactif. Le document PDF non interactif est stocké dans un noeud Content Services (obsolète) nommé `/Company Home/Test Directory`. Le nom du formulaire est créé de manière dynamique. En d’autres termes, le prénom et le nom de l’utilisateur sont utilisés pour nommer le fichier PDF. L’identifiant de ressource du nouveau contenu est écrit dans le navigateur Web client. (Voir [Création de Documents PDF avec des données XML envoyées](/help/forms/developing/rendering-forms.md#creating-pdf-documents-with-submitted-xml-data).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * 20. adobe-output-client.jar
     * 21. adobe-contentservices-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.contentservices.client.impl.UpdateVersionType;
 import com.adobe.livecycle.formsservice.client.*;
 import com.adobe.livecycle.output.client.OutputClient;
 import com.adobe.livecycle.output.client.OutputResult;
 import com.adobe.livecycle.output.client.PDFOutputOptionsSpec;
 import com.adobe.livecycle.output.client.TransformationFormat;
 
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleDataSendToOutput extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 //Create a non-interactive PDF document by invoking the Output service
                 Document myPDFform = GeneratePDFDocument(myFactory, formOutput);
 
                 //Create the name of the PDF file to store
                 String pdfName = "Loan_"+myLastName+"_"+myFirstName+".pdf" ;
                 String userName = myFirstName+" "+myLastName ;
 
                 //Store the PDF form into Content Services (deprecated)
                 String resourceID = StorePDFDocument(myFactory, myPDFform, pdfName,userName);
                 pp.println("<p> The pdf document was store in :<br><br>" +
                         "<li> /Company home "+
                         "<li> The identifier value of the new resource is "+ resourceID+"");
                   }
             }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 
     //Store the PDF document in /Company Home/Test Directory using the
     //AEM Forms Content Service API
     private String StorePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document pdfDoc, String formName, String userName)
     {
         try
         {
             //Create a DocumentManagementServiceClientImpl object
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
             //Specify the store and node name
             String storeName ="SpacesStore";
             String nodeName = "/Company Home/Test Directory";
 
             //Create a MAP instance to store attributes
             Map<String,Object> inputs = new HashMap<String,Object>();
 
             //Specify attributes that belong to the new content
             String creator = "{https://www.alfresco.org/model/content/1.0}creator";
             String description = "{https://www.alfresco.org/model/content/1.0}description";
 
             inputs.put(creator,userName);
             inputs.put(description,"A mortgage application form");
 
             //Store MortgageForm.pdf in /Company Home/Test Directory
             CRCResult result = docManager.storeContent(storeName,
                      nodeName,
                      formName,
                     "{https://www.alfresco.org/model/content/1.0}content",
                     pdfDoc,
                     "UTF-8",
                     UpdateVersionType.INCREMENT_MAJOR_VERSION,
                     null,
                     inputs);
             //Get the identifier value of the new resource
             String id = result.getNodeUuid();
             return id;
     }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null ;
     }
 
 
     //This method returns the value of the specified node
     private com.adobe.idp.Document GeneratePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document formData)
     {
         try
         {
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Set PDF run-time options
         com.adobe.livecycle.output.client.PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setLocale("en_US");
 
         //Set rendering run-time options
         com.adobe.livecycle.output.client.RenderOptionsSpec pdfOptions = new com.adobe.livecycle.output.client.RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             formData
         );
 
         //Get the Generated PDF file
         Document ouputDoc = outputDocument.getGeneratedDoc();
         return ouputDoc ;
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null;
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
```

## Début rapide (mode SOAP) : Préremplissage de Forms avec des mises en page souples à l’aide de l’API Java {#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api}

L’exemple de code suivant préremplit un formulaire avec une source de données dynamique. En d’autres termes, la source de données est créée au moment de l’exécution et n’est pas contenue dans un fichier XML ni créée au moment de la conception. Cet exemple de code contient trois méthodes définies par l&#39;utilisateur :

* `createDataSource`: Crée un  `org.w3c.dom.Document` objet qui représente la source de données utilisée pour préremplir le formulaire. Cette méthode définie par l&#39;utilisateur renvoie l&#39;objet `org.w3c.dom.Document`.
* `convertDataSource`: Convertit un  `org.w3c.dom.Document` objet en  `com.adobe.idp.Document` objet. Cette méthode accepte un objet `org.w3c.dom.Document` comme paramètre d&#39;entrée et renvoie un objet `com.adobe.idp.Document`.
* `renderPOForm`: Utilise l’API Java du service Forms pour générer un formulaire de bon de commande dynamique. L’objet `com.adobe.idp.Document` renvoyé par la méthode `convertDataSource` est utilisé pour préremplir le formulaire.

   Toutes ces méthodes sont appelées à partir de la méthode `doPost` de la servlet Java. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/rendering-forms.md#prepopulating-forms-with-flowable-layouts).)

```java
/*
* This Java Quick Start uses the following JAR files
* 1. adobe-forms-client.jar
* 2. adobe-livecycle-client.jar
* 3. adobe-usermanager-client.jar
* 4. activation.jar (required for SOAP mode)
* 5. axis.jar (required for SOAP mode)
* 6. commons-codec-1.3.jar (required for SOAP mode)
* 7. commons-collections-3.2.jar (required for SOAP mode)
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
* (Because Forms quick starts are implemented as Java servlets, it is
* not necessary to include J2EE specific JAR files - the Java project
* that contains this quick start is exported as a WAR file which
* is deployed to the J2EE application server)
*
* These JAR files are located in the following path:
* <install directory>/sdk/client-libs/common
*
* For complete details about the location of these JAR files,
* see "Including AEM Forms library files" in Programming with AEM forms
*/
import java.io.IOException;
import javax.servlet.Servlet;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.adobe.livecycle.formsservice.client. * ;
import java.util. * ;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import org.w3c.dom.Element;
import javax.xml.parsers. * ;
import javax.xml.transform. * ;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
public class RenderDynamicForm extends HttpServlet implements Servlet {
 public void doGet(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  doPost(req, resp);
 }
 public void doPost(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  //Render a dynamic purchase order form
  //Create an org.w3c.dom.Document object
  org.w3c.dom.Document myDom = createDataSource();
  //Convert the org.w3c.dom.Document object
  //to a com.adobe.idp.Document object
  com.adobe.idp.Document formData = convertDataSource(myDom);
  //Render the dynamic form using data located within the
  //com.adobe.idp.Document object
  renderPOForm(resp, formData);
 }
 //Creates an org.w3c.dom.Document object
 private org.w3c.dom.Document createDataSource() {
  org.w3c.dom.Document document = null;
  try {
   //Create DocumentBuilderFactory and DocumentBuilder objects
   DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
   DocumentBuilder builder = factory.newDocumentBuilder();
   //Create a new Document object
   document = builder.newDocument();
   //Create the root element and append it to the XML DOM
   Element root = (Element) document.createElement("transaction");
   document.appendChild(root);
   //Create the header element
   Element header = (Element) document.createElement("header");
   root.appendChild(header);
   //Create the txtPONum element and append it to the
   //header element
   Element txtPONum = (Element) document.createElement("txtPONum");
   txtPONum.appendChild(document.createTextNode("8745236985"));
   header.appendChild(txtPONum);
   //Create the dtmDate element and append it to the
   //header element
   Element dtmDate = (Element) document.createElement("dtmDate");
   dtmDate.appendChild(document.createTextNode("2007-02-08"));
   header.appendChild(dtmDate);
   //Create the orderedByAddress element and append
   //it to the header element
   Element orderedByAddress = (Element) document.createElement("orderedByAddress");
   orderedByAddress.appendChild(document.createTextNode("222, Any Blvd"));
   header.appendChild(orderedByAddress);
   //Create the txtOrderedByPhone element and append
   //it to the header element
   Element txtOrderedByPhone = (Element) document.createElement("txtOrderedByPhone");
   txtOrderedByPhone.appendChild(document.createTextNode("(555) 555-2334"));
   header.appendChild(txtOrderedByPhone);
   //Create the txtOrderedByFax element and append
   //it to the header element
   Element txtOrderedByFax = (Element) document.createElement("txtOrderedByFax");
   txtOrderedByFax.appendChild(document.createTextNode("(555) 555-9334"));
   header.appendChild(txtOrderedByFax);
   //Create the txtOrderedByContactName element and append
   //it to the header element
   Element txtOrderedByContactName = (Element) document.createElement("txtOrderedByContactName");
   txtOrderedByContactName.appendChild(document.createTextNode("Frank Jones"));
   header.appendChild(txtOrderedByContactName);
   //Create the deliverToAddress element and append
   //it to the header element
   Element deliverToAddress = (Element) document.createElement("deliverToAddress");
   deliverToAddress.appendChild(document.createTextNode("555, Any Blvd"));
   header.appendChild(deliverToAddress);
   //Create the txtDeliverToPhone element and append
   //it to the header element
   Element txtDeliverToPhone = (Element) document.createElement("txtDeliverToPhone");
   txtDeliverToPhone.appendChild(document.createTextNode("(555) 555-9098"));
   header.appendChild(txtDeliverToPhone);
   //Create the txtDeliverToFax element and append
   //it to the header element
   Element txtDeliverToFax = (Element) document.createElement("txtDeliverToFax");
   txtDeliverToFax.appendChild(document.createTextNode("(555) 555-9000"));
   header.appendChild(txtDeliverToFax);
   //Create the txtDeliverToContactName element and
   //append it to the header element
   Element txtDeliverToContactName = (Element) document.createElement("txtDeliverToContactName");
   txtDeliverToContactName.appendChild(document.createTextNode("Jerry Johnson"));
   header.appendChild(txtDeliverToContactName);
   //Create the detail element and append it to the root
   Element detail = (Element) document.createElement("detail");
   root.appendChild(detail);

   //Create the txtPartNum element and append it to the
   //detail element
   Element txtPartNum = (Element) document.createElement("txtPartNum");
   txtPartNum.appendChild(document.createTextNode("00010-100"));
   detail.appendChild(txtPartNum);
   //Create the txtDescription element and append it
   //to the detail element
   Element txtDescription = (Element) document.createElement("txtDescription");
   txtDescription.appendChild(document.createTextNode("Monitor"));
   detail.appendChild(txtDescription);
   //Create the numQty element and append it to
   //the detail element
   Element numQty = (Element) document.createElement("numQty");
   numQty.appendChild(document.createTextNode("1"));
   detail.appendChild(numQty);
   //Create the numUnitPrice element and append it
   //to the detail element
   Element numUnitPrice = (Element) document.createElement("numUnitPrice");
   numUnitPrice.appendChild(document.createTextNode("350.00"));
   detail.appendChild(numUnitPrice);
   //Create another detail element named detail2 and
   //append it to root
   Element detail2 = (Element) document.createElement("detail");
   root.appendChild(detail2);
   //Create the txtPartNum element and append it to the
   //detail2 element
   Element txtPartNum2 = (Element) document.createElement("txtPartNum");
   txtPartNum2.appendChild(document.createTextNode("00010-200"));
   detail2.appendChild(txtPartNum2);
   //Create the txtDescription element and append it
   //to the detail2 element
   Element txtDescription2 = (Element) document.createElement("txtDescription");
   txtDescription2.appendChild(document.createTextNode("Desk lamps"));
   detail2.appendChild(txtDescription2);
   //Create the numQty element and append it to the
   //detail2 element
   Element numQty2 = (Element) document.createElement("numQty");
   numQty2.appendChild(document.createTextNode("3"));
   detail2.appendChild(numQty2);
   //Create the NUMUNITPRICE element
   Element numUnitPrice2 = (Element) document.createElement("numUnitPrice");
   numUnitPrice2.appendChild(document.createTextNode("55.00"));
   detail2.appendChild(numUnitPrice2);
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  return document;

 }
 //Converts an org.w3c.dom.Document object to a
 //com.adobe.idp.Document object
 private Document convertDataSource(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
 //Render the purchase order form using the specified
 //com.adobe.idp.Document object
 private void renderPOForm(HttpServletResponse resp, Document formData) {
  try {
   //Set connection properties required to invoke AEM Forms
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceC
   lientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
   //Create a ServiceClientFactory object
   ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
   //Create a FormsServiceClient object
   FormsServiceClient formsClient = new FormsServiceClient(myFactory);
   //Set the parameter values for the renderPDFForm method
   String formName = "Applications/FormsApplication/1.0/FormsFolder/PO.xdp";
   //Cache the form
   PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
   pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
   //Specify URI values that are required to render a form
   URLSpec uriValues = new URLSpec();
   uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
   uriValues.setContentRootURI("repository:///");
   uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
   //Invoke the renderForm method
   FormsResult formOut = formsClient.renderPDFForm(
   formName, //formQuery
   formData, //inDataDoc
   pdfFormRenderSpec, //PDFFormRenderSpec
   uriValues, //urlSpec
   null //attachments
   );
   //Create a ServletOutputStream object
   ServletOutputStream oOutput = resp.getOutputStream();
   //Create a Document object that stores form data
   Document myData = formOut.getOutputContent();
   //Create an InputStream object
   InputStream inputStream = myData.getInputStream();
   //Write the data stream to the web browser
   byte[] data = new byte[4096];
   int bytesRead = 0;
   while ((bytesRead = inputStream.read(data)) > 0) {
    oOutput.write(data, 0, bytesRead);
   }
  } catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
 }
}
```

## Début rapide (mode SOAP) : Gestion d’un formulaire contenant un script de calcul à l’aide de l’API Java {#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api}

L’exemple de code suivant traite un formulaire qui contient un script de calcul et écrit les résultats dans le navigateur Web client. (Voir [Calcul des données de formulaire](/help/forms/developing/rendering-forms.md#calculating-form-data).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CalculateData extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
             RenderOptionsSpec processSpec = new RenderOptionsSpec();
             processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,"CONTENT_TYPE=application/pdf&CONTENT_TYPE=application/vnd.adobe.xdp+xml","",processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is calculated
             if (processState == 1)
             {
 
                 //Write the data back to to the client web browser
                 ServletOutputStream oOutput = resp.getOutputStream();
                 Document calData = formOut.getOutputContent();
 
                 //Create an InputStream object
                 InputStream inputStream = calData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
              }
             }
         catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
         }
     }
 }
```

## Début rapide (mode SOAP) : Optimisation des performances à l’aide de l’API Java {#quick-start-soap-mode-optimizing-performance-using-the-java-api}

L’exemple de code suivant optimise les performances en définissant les options de mise en cache, autonome et linéarisée. Un fichier linéarisé est optimisé pour la diffusion sur le Web. (Voir [Optimisation des performances du service Forms](/help/forms/developing/rendering-forms.md#optimizing-the-performance-of-the-forms-service).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsPerformance extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
     try{
 
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set the parameter values for the renderForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set performance run-time options
         PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
         renderSpec.setCacheEnabled(new Boolean(true));
         renderSpec.setLinearizedPDF(true);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms Repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method and write the
         //results to a client web browser
         FormsResult formOut = formsClient.renderPDFForm(
                     formName,       //formQuery
                     oInputData,     //inDataDoc
                     renderSpec,     //PDFFormRenderSpec
                     uriValues,        //urlSpec
                     null            //attachments
                     );
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

## Début rapide (mode SOAP) : Rendu par valeur à l’aide de l’API Java {#quick-start-soap-mode-rendering-by-value-using-the-java-api}

Le début rapide Java suivant génère un formulaire PDF interactif basé sur une conception de formulaire nommée *Loan.xdp* par valeur. Notez que la conception de formulaire est utilisée pour remplir un objet `com.adobe.idp.Document` nommé *inputXDP*. (Voir [Rendu Forms par valeur](/help/forms/developing/rendering-forms.md#rendering-forms-by-value).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
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
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderByValue extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Retrieve the form design
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");
             Document inputXDP = new Document(fileInputStream);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Invoke the renderPDFForm method and pass the
             //form design by value
             FormsResult formOut = formsClient.renderPDFForm(
                         "",                     //formQuery
                         inputXDP,                 //inDataDoc
                         new PDFFormRenderSpec(), //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 }
```

## Début rapide (mode SOAP) : Transmission de documents au service Forms à l’aide de l’API Java {#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api}

Le début rapide Java suivant récupère le fichier Loan.xdp de Content Services (obsolète). Ce fichier XDP se trouve dans l’espace `/Company Home/Form Designs`. Le fichier XDP est renvoyé dans une instance `com.adobe.idp.Document`. L&#39;instance `com.adobe.idp.Document` est transmise au service Forms. Le formulaire interactif est écrit dans un navigateur Web client. (Voir [Transmission de Documents au service Forms](/help/forms/developing/passing-documents-forms-service.md).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-contentservices-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsFromContentServices extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Create an empty Document that represents form data
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Get the form design from Content Services (deprecated)
             Document formDesign =  GetFormDesign(myFactory);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Invoke the renderPDFForm2 and pass to the
             //Document that contains the form design
             FormsResult formOut = formsClient.renderPDFForm2(
                     formDesign,
                     oInputData,
                     pdfFormRenderSpec,
                     null,
                     null
                     );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 
     //Retrieve the form design from Content Services (deprecated)
     private Document GetFormDesign(ServiceClientFactory myFactory)
     {
         try{
 
         //Create a DocumentManagementServiceClientImpl object
         DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
         //Specify the name of the store and the content to retrieve
            String storeName = "SpacesStore";
            String nodeName  = "/Company Home/Form Designs/Loan.xdp";
 
            //Retrieve /Company Home/Form Designs/Loan.xdp
            CRCResult content = docManager.retrieveContent(
                      storeName,
                      nodeName,
                      "");
 
            //Return the Document instance
             Document doc =content.getDocument();
             return  doc;
          }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
         return null;
     }
 
 }
 
```

