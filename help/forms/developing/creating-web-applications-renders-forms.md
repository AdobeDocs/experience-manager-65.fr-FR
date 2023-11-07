---
title: Créer des applications web qui génèrent des formulaires
seo-title: Creating Web Applications thatRenders Forms
description: Créez une application web qui utilise des servlets Java pour appeler le service Forms et générer des formulaires. Le servlet Java sert de lien entre le service Forms qui renvoie un formulaire et un navigateur web client.
seo-description: Create a web-based application that uses Java servlets to invoke the Forms service and render forms. The Java servlet serves as the link between the Forms service that returns a form and a client web browser.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: Developer
exl-id: 85e00003-8c8b-463a-b728-66af174be295
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 93%

---

# Créer des applications web qui génèrent des formulaires {#creating-web-applications-thatrenders-forms}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## Créer des applications web qui génèrent des formulaires {#creating-web-applications-that-renders-forms}

Vous pouvez créer une application web qui utilise des servlets Java pour appeler le service Forms et générer des formulaires. L’utilisation d’un servlet Java™ est avantageuse dans la mesure où elle permet d’écrire la valeur renvoyée par le processus dans un navigateur web client. En d’autres termes, un servlet Java peut être utilisé comme lien entre le service Forms qui renvoie un formulaire et un navigateur web client.

>[!NOTE]
>
>Cette section décrit comment créer une application web utilisant un servlet Java qui appelle le service Forms et effectue le rendu des formulaires basés sur des fragments. (Reportez-vous à la section [Rendu de formulaires reposant sur des fragments](/help/forms/developing/rendering-forms-based-fragments.md).)

À l’aide d’un servlet Java, vous pouvez écrire un formulaire dans un navigateur web client afin qu’un client puisse afficher et saisir des données dans le formulaire. Après avoir rempli le formulaire avec des données, l’utilisateur web clique sur un bouton d’envoi situé sur le formulaire pour renvoyer les informations au servlet Java, où les données peuvent être récupérées et traitées. Par exemple, les données peuvent être envoyées à un autre processus.

Cette section explique comment créer une application web qui permet à l’utilisateur de sélectionner soit des données de formulaire américaines, soit des données de formulaire canadiennes, comme illustré ci-dessous.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

Le formulaire rendu est un formulaire basé sur des fragments. En d’autres termes, si l’utilisateur sélectionne des données américaines, le formulaire renvoyé utilise des fragments basés sur des données américaines. Par exemple, le pied de page du formulaire contient une adresse américaine, comme illustré ci-dessous.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

De même, si l’utilisateur sélectionne des données canadiennes, le formulaire renvoyé contient une adresse canadienne, comme le montre l’illustration suivante.

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>Pour plus d’informations sur la création de conceptions de formulaires basés sur des fragments, consultez le document [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

**Exemples de fichiers**

Cette section utilise des fichiers d’exemple qui peuvent se trouver à l’emplacement suivant :

&lt;*Répertoire d’installation de Forms Designe*>/Exemples/Forms/Bon de commande/Fragments de formulaire

où &lt;*répertoire d’installation*> est le chemin d’installation. Pour les besoins de l’application cliente, le fichier Purchase Order Dynamic.xdp a été copié à partir de cet emplacement d’installation et déployé vers une application Forms nommée *Applications/FormsApplication*. Le fichier Purchase Order Dynamic.xdp est placé dans un dossier nommé FormsFolder. De même, les fragments sont placés dans un dossier nommé Fragments, comme illustré ci-dessous.

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Pour accéder à la conception de formulaire Purchase Order Dynamic.xdp, spécifiez `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` comme nom du formulaire (premier paramètre transmis à la méthode `renderPDFForm`) et `repository:///` comme valeur de l’URI racine du contenu.

Les fichiers de données XML utilisés par l’application web ont été déplacés du dossier Data vers `C:\Adobe` (système de fichiers appartenant au serveur d’applications J2EE qui héberge AEM Forms). Les noms de fichier sont Bon de commande *Canada.xml* et Bon de commande *US.xml*.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).

### Résumé des étapes {#summary-of-steps}

Pour créer des applications web qui génèrent des formulaires basés sur des fragments, procédez comme suit :

1. Créer un projet web.
1. Créez une logique d’application Java qui représente le servlet Java.
1. Créez la page web de l’application web.
1. Conditionnez l’application web dans un fichier WAR.
1. Déployez le fichier WAR sur le serveur d’applications J2EE.
1. Testez votre application web.

>[!NOTE]
>
>Certaines de ces étapes dépendent de l’application J2EE sur laquelle AEM Forms est déployé. Par exemple, la méthode que vous utilisez pour déployer un fichier WAR dépend du serveur d’applications J2EE que vous utilisez. Cette section suppose qu’AEM Forms est déployé sur JBoss®.

### Créer un projet web {#creating-a-web-project}

La première étape pour créer une application web contenant un servlet Java pouvant appeler le service Forms consiste à créer un projet web. L’IDE Java sur lequel repose ce document est Eclipse 3.3. À l’aide de l’IDE Eclipse, créez un projet web et ajoutez les fichiers JAR requis à votre projet. Enfin, ajoutez une page de HTML nommée *index.html* et une servlet Java à votre projet.

La liste suivante répertorie les fichiers JAR que vous devez ajouter à votre projet web :

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

Pour plus d’informations sur l’emplacement de ces fichiers JAR, consultez la section [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Pour créer un projet web :**

1. Démarrez Eclipse et sélectionnez **Fichier** > **Nouveau projet**.
1. Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Web** > **Projet web dynamique**.
1. Entrez `FragmentsWebApplication` comme nom de projet, puis cliquez sur **Terminer**.

**Pour ajouter les fichiers JAR requis à votre projet :**

1. Dans lʼexplorateur de projets, cliquez avec le bouton droit sur le projet `FragmentsWebApplication` et sélectionnez **Propriétés**.
1. Cliquez sur le **Chemin d’accès création Java**, puis sur l’onglet **Bibliothèques**.
1. Cliquez sur le bouton **Ajouter des fichiers JAR externes** et recherchez les fichiers JAR à inclure.

**Pour ajouter une servlet Java au projet :**

1. Dans lʼexplorateur de projets, cliquez avec le bouton droit sur le projet `FragmentsWebApplication` et sélectionnez **Nouveau** > **Autre**.
1. Développez le dossier **Web**, sélectionnez **Servlet**, puis cliquez sur **Suivant**.
1. Dans la boîte de dialogue Créer une servlet, saisissez `RenderFormFragment` comme nom de servlet, puis cliquez sur **Terminer**.

**Pour ajouter une page HTML à votre projet :**

1. Dans lʼexplorateur de projets, cliquez avec le bouton droit sur le projet `FragmentsWebApplication` et sélectionnez **Nouveau** > **Autre**.
1. Développez le dossier **Web** et sélectionnez **HTML**, puis cliquez sur **Suivant**.
1. Dans la boîte de dialogue Nouvelle page HTML, entrez `index.html` comme nom de fichier, puis cliquez sur **Terminer**.

>[!NOTE]
>
>Pour plus d’informations sur la création de la page HTML qui appelle la servlet Java `RenderFormFragment`, consultez la section [Création de la page web](/help/forms/developing/rendering-forms.md#creating-the-web-page).

### Création d’une logique d’application Java pour la servlet {#creating-java-application-logic-for-the-servlet}

Créez une logique d’application Java qui appelle le service Forms à partir de la servlet Java. Le code suivant affiche la syntaxe de la servlet Java `RenderFormFragment` :

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

En règle générale, vous ne devez pas placer de code client dans la méthode `doGet` ou `doPost` de la servlet Java. Une bonne pratique en matière de programmation plus efficace consiste à placer ce code dans une classe distincte, à appeler la classe à partir de la méthode `doPost` (ou `doGet` ), puis à appeler les méthodes appropriées. Toutefois, pour des raisons de concision du code, les exemples de code de cette section sont réduits au minimum et placés dans la méthode `doPost`.

Pour restituer un formulaire reposant sur les fragments à l’aide de l’API du service Forms, procédez comme suit :

1. Incluez les fichiers JAR du client, tels que adobe-forms-client.jar, dans le chemin d’accès aux classes de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Récupérez la valeur du bouton radio qui est envoyé à partir du formulaire HTML, qui spécifie sʼil faut utiliser les données américaines ou canadiennes. Si American est envoyé, créez une `com.adobe.idp.Document` qui stocke les données dans la variable *Purchase Order US.xml*. De même, si la variable `com.adobe.idp.Document` qui stocke les données dans la variable *Purchase Order Canada.xml* fichier .
1. Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
1. Créez un objet `URLSpec` qui stocke les valeurs URI en utilisant son constructeur.
1. Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur de chaîne qui représente la racine web de l’application.
1. Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de la racine du contenu URI. Assurez-vous que la conception de formulaire et les fragments se trouvent dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel AEM Forms, spécifiez `repository://`.
1. Appelez la méthode `setTargetURL` de lʼobjet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur URL cible vers laquelle les données du formulaire sont affichées. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer les calculs.
1. Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Un objet `com.adobe.idp.Document` qui contient les données à fusionner avec le formulaire (créé à l’étape 2).
   * Un objet `PDFFormRenderSpec` qui stocke les options d’exécution. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objet `URLSpec` qui contient les valeurs URI requises par le service Forms pour effectuer le rendu d’un formulaire basé sur des fragments.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` qui contient un flux de données de formulaire qui doit être écrit dans le navigateur web du client.

1. Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
1. Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
1. Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
1. Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
1. Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de lʼobjet `com.adobe.idp.Document`.
1. Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de lʼobjet `InputStream` et en transmettant le tableau d’octets comme argument.
1. Appelez la méthode `write` de lʼobjet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

L’exemple de code suivant représente le servlet Java qui appelle le service Forms et effectue le rendu d’un formulaire basé sur des fragments.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
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
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
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

### Créer la page web {#creating-the-web-page}

La page web index.html fournit un point d’entrée au servlet Java et appelle le service Forms. Cette page web est un formulaire HTML de base qui contient deux boutons radio et un bouton d’envoi. Le nom des boutons radio est radio. Lorsque l’utilisateur clique sur le bouton d’envoi, les données du formulaire sont envoyées au servlet Java `RenderFormFragment`.

Le servlet Java capture les données publiées à partir de la page HTML en utilisant le code Java suivant :

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

Le code de HTML suivant se trouve dans le fichier index.html qui a été créé lors de la configuration de l’environnement de développement. (Voir [Créer un projet web](/help/forms/developing/rendering-forms.md#creating-a-web-project).)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### Conditionner l’application web {#packaging-the-web-application}

Pour déployer le servlet Java qui appelle le service Forms, conditionnez votre application web dans un fichier WAR. Assurez-vous que les fichiers JAR externes dont dépend la logique commerciale du composant, tels que adobe-livecycle-client.jar et adobe-forms-client.jar, sont également inclus dans le fichier WAR.

**Pour conditionner une application web dans un fichier WAR :**

1. Dans la fenêtre de l’**explorateur de projets**, cliquez avec le bouton droit sur le projet `FragmentsWebApplication` et sélectionnez **Exporter** > **Fichier WAR**.
1. Dans la zone de texte **Module web**, saisissez `FragmentsWebApplication` comme nom du projet Java.
1. Dans la zone de texte **Destination**, saisissez `FragmentsWebApplication.war`**comme** nom du fichier, indiquez l’emplacement de votre fichier WAR, puis cliquez sur Terminer.

### Déployer le fichier WAR sur le serveur d’applications J2EE {#deploying-the-war-file-to-the-j2ee-application-server}

Vous pouvez déployer le fichier WAR sur le serveur d’applications J2EE sur lequel AEM Forms est déployé. Une fois le fichier WAR déployé, vous pouvez accéder à la page web HTML à l’aide d’un navigateur web.

**Pour déployer le fichier WAR sur le serveur d’applications J2EE :**

* Copiez le fichier WAR du chemin d’accès d’exportation vers `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### Tester votre application web {#testing-your-web-application}

Une fois l’application web déployée, vous pouvez la tester à l’aide d’un navigateur web. En supposant que vous utilisiez le même ordinateur que celui qui héberge AEM Forms, vous pouvez spécifier l’URL suivante :

* http://localhost:8080/FragmentsWebApplication/index.html

  Sélectionnez un bouton radio et cliquez sur le bouton Envoyer. Un formulaire basé sur des fragments apparaît dans le navigateur web. En cas de problème, consultez le fichier journal du serveur d’applications J2EE.
