---
title: Appel de processus pour des intervenants humains de longue durée
seo-title: Appel de processus pour des intervenants humains de longue durée
description: Appelez par programmation des processus de longue durée centrés sur l’homme créés dans Workbench à l’aide d’une application cliente Web Java qui utilise l’API Invocation, une application ASP.NET qui utilise les services Web et une application cliente créée avec Flex qui utilise Remoting.
seo-description: Appelez par programmation des processus de longue durée centrés sur l’homme créés dans Workbench à l’aide d’une application cliente Web Java qui utilise l’API Invocation, une application ASP.NET qui utilise les services Web et une application cliente créée avec Flex qui utilise Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3740'
ht-degree: 4%

---


# Appel de processus pour des intervenants humains de longue durée {#invoking-human-centric-long-lived-processes}

Vous pouvez appeler par programmation des processus de longue durée centrés sur l’être humain qui ont été créés dans Workbench à l’aide des applications clientes suivantes :

* Application cliente Web Java utilisant l’API d’appel. (Voir [Appeler AEM Forms à l’aide de l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)
* Application ASP.NET qui utilise des services Web. (Voir [Appel d’AEM Forms à l’aide de services Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Application cliente créée avec Flex qui utilise Remoting. (Voir [Appeler AEM Forms à l’aide de (obsolète pour les formulaires AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Le processus de longue durée appelé est nommé *FirstAppSolution/PreLoanProcess*. Vous pouvez créer ce processus en suivant le didacticiel spécifié dans [Création de votre première application AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

Un processus axé sur l’humain implique une tâche à laquelle un utilisateur peut répondre en utilisant Workspace. Par exemple, à l’aide de Workbench, vous pouvez créer un processus qui permet à un gestionnaire de banque d’approuver ou de refuser une demande de prêt. L&#39;illustration suivante montre le processus *FirstAppSolution/PreLoanProcess*.

Le processus *FirstAppSolution/PreLoanProcess* accepte un paramètre d’entrée nommé *formData* dont le type de données est XML. Les données XML sont fusionnées avec une conception de formulaire nommée *PreLoanForm.xdp*. L’illustration suivante présente un formulaire qui représente une tâche affectée à un utilisateur pour approuver ou refuser une demande de prêt. L’utilisateur approuve ou refuse l’application à l’aide de Workspace. L’utilisateur de Workspace peut approuver la demande de prêt en cliquant sur le bouton Approuver illustré dans l’illustration suivante. De même, l’utilisateur peut refuser la demande de prêt en cliquant sur le bouton de refus.

Un processus de longue durée est appelé de manière asynchrone et ne peut pas l’être de manière synchrone en raison des facteurs suivants :

* Un processus peut s’étendre sur une période considérable.
* Un processus peut dépasser les limites organisationnelles.
* Un processus a besoin d’une entrée externe pour se terminer. Prenons l’exemple d’un cas où un formulaire est envoyé à un responsable absent du bureau. Dans ce cas, le processus n’est pas terminé tant que le gestionnaire ne retourne pas et ne remplit pas le formulaire.

Lorsqu’un processus de longue durée est appelé, AEM Forms crée une valeur d’identificateur d’appel dans le cadre de la création d’un enregistrement. L’enregistrement suit l’état du processus de longue durée et est stocké dans la base de données AEM Forms. A l’aide de la valeur d’identifiant d’appel, vous pouvez suivre l’état du processus de longue durée. En outre, vous pouvez utiliser la valeur de l’identifiant d’appel de processus pour effectuer des opérations Process Manager telles que l’arrêt d’une instance de processus en cours d’exécution.

>[!NOTE]
>
>AEM Forms ne crée pas de valeur d’identifiant d’appel ni d’enregistrement lorsqu’un processus de courte durée est appelé.

Le processus `FirstAppSolution/PreLoanProcess` est appelé lorsqu’un demandeur soumet une demande, qui est représentée sous la forme de données XML. Le nom de la variable de processus d’entrée est `formData` et son type de données est XML. Aux fins de cette discussion, supposons que les données XML suivantes soient utilisées comme entrée au processus `FirstAppSolution/PreLoanProcess`.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

Les données XML transmises à un processus doivent correspondre aux champs situés dans le formulaire utilisé dans le processus. Sinon, les données ne s’affichent pas dans le formulaire. Toutes les applications qui appellent le processus `FirstAppSolution/PreLoanProcess` doivent transmettre cette source de données XML. Les applications créées dans *Appeler des processus à longue durée centrés sur l&#39;humain* créent dynamiquement la source de données XML à partir des valeurs qu&#39;un utilisateur a entrées dans un client Web.

A l’aide d’une application cliente, vous pouvez envoyer le *PremierAppSolution/PreLoanProcess* processus de traitement des données XML requises. Un processus de longue durée renvoie une valeur d’identifiant d’appel comme valeur de retour. L’illustration suivante montre les applications clientes qui invoquent le processus de longue durée*FirstAppSolution/PreLoanProcess. Les applications clientes envoient des données XML et récupèrent une valeur de chaîne qui représente la valeur de l’identifiant d’appel.

**Voir également**

[Création d’une application Web Java qui appelle un processus pour des intervenants humains de longue durée](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[Création d&#39;une application Web ASP.NET qui appelle un processus de longue durée axé sur l&#39;humain](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[Création d’une application cliente créée avec Flex qui appelle un processus de longue durée axé sur l’être humain](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## Création d’une application Web Java qui appelle un processus pour des intervenants humains de longue durée {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Vous pouvez créer une application Web qui utilise une servlet Java pour appeler le processus `FirstAppSolution/PreLoanProcess`. Pour appeler ce processus à partir d’une servlet Java, utilisez l’API d’appel dans la servlet Java. (Voir [Appel d’AEM Forms à l’aide de l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

L’illustration suivante présente une application cliente Web qui publie des valeurs de nom, de téléphone (ou de courrier électronique) et de montant. Ces valeurs sont envoyées à la servlet Java lorsque l’utilisateur clique sur le bouton Envoyer la demande.

La servlet Java exécute les tâches suivantes :

* Récupère les valeurs publiées de la page HTML vers la servlet Java.
* Crée de manière dynamique une source de données XML à transmettre au processus *FirstAppSolution/PreLoanProcess*. Les valeurs de nom, de téléphone (ou de courrier électronique) et de montant sont spécifiées dans la source de données XML.
* Appelle le processus *FirstAppSolution/PreLoanProcess* à l’aide de l’API d’appel AEM Forms.
* Renvoie la valeur de l’identifiant d’appel au navigateur Web client.

### Résumé des étapes {#summary-of-steps}

Pour créer une application Web Java qui appelle le processus `FirstAppSolution/PreLoanProcess`, procédez comme suit :

1. [Créez un projet](invoking-human-centric-long-lived.md#create-a-web-project) Web.
1. [Créez une logique d&#39;application Java pour la servlet](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [Création de la page Web pour l’application Web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Assemblez l&#39;application Web dans un fichier](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file) WAR.
1. [Déployez le fichier WAR sur le serveur d’applications J2EE hébergeant AEM Forms](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [Testez votre application](invoking-human-centric-long-lived.md#test-your-web-application) Web.

>[!NOTE]
>
>Certaines de ces étapes dépendent de l’application J2EE sur laquelle AEM Forms est déployé. Par exemple, la méthode que vous utilisez pour déployer un fichier WAR dépend du serveur d’applications J2EE que vous utilisez. AEM Forms est probablement déployé sur JBoss®.

### Créer un projet Web {#create-a-web-project}

La première étape de la création d’une application Web consiste à créer un projet Web. Eclipse 3.3 est l&#39;IDE Java sur lequel repose ce document. A l&#39;aide de l&#39;IDE Eclipse, créez un projet Web et ajoutez les fichiers JAR requis à votre projet. Ajoutez une page HTML nommée *index.html* et une servlet Java à votre projet.

La liste suivante spécifie les fichiers JAR à inclure dans votre projet Web :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

Pour connaître l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>Le fichier J2EE.jar définit les types de données utilisés par une servlet Java. Vous pouvez obtenir ce fichier JAR à partir du serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un projet Web**

1. Début Eclipse et cliquez sur **Fichier** > **Nouveau projet**.
1. Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Web** > **Projet Web dynamique**.
1. Tapez `InvokePreLoanProcess` pour le nom de votre projet, puis cliquez sur **Terminer**.

**Ajouter les fichiers JAR requis à votre projet**

1. Dans la fenêtre Explorateur de projets, cliquez avec le bouton droit sur le projet `InvokePreLoanProcess` et sélectionnez **Propriétés**.
1. Cliquez sur **Chemin de génération Java**, puis sur l&#39;onglet **Bibliothèques**.
1. Cliquez sur le bouton **Ajouter les fichiers JAR externes** et accédez aux fichiers JAR à inclure.

**Ajouter une servlet Java à votre projet**

1. Dans la fenêtre Explorateur de projets, cliquez avec le bouton droit sur le projet `InvokePreLoanProcess` et sélectionnez **Nouveau** > **Autre**.
1. Développez le dossier **Web**, sélectionnez **Servlet**, puis cliquez sur **Suivant**.
1. Dans la boîte de dialogue Créer un servlet, tapez `SubmitXML` pour le nom de la servlet, puis cliquez sur **Terminer**.

**Ajouter une page HTML à votre projet**

1. Dans la fenêtre Explorateur de projets, cliquez avec le bouton droit sur le projet `InvokePreLoanProcess` et sélectionnez **Nouveau** > **Autre**.
1. Développez le dossier **Web**, sélectionnez **HTML**, puis cliquez sur **Suivant**.
1. Dans la boîte de dialogue Nouveau code HTML, saisissez `index.html` pour le nom de fichier, puis cliquez sur **Terminer**.

>[!NOTE]
>
>Pour plus d’informations sur la création de contenu HTML qui appelle la servlet Java SubmitXML, voir [Création de la page Web pour l’application Web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### Créer une logique d&#39;application Java pour la servlet {#create-java-application-logic-for-the-servlet}

Créez une logique d’application Java qui appelle le processus `FirstAppSolution/PreLoanProcess` depuis la servlet Java. Le code suivant illustre la syntaxe de la servlet Java `SubmitXML` :

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

Normalement, vous ne placez pas de code client dans la méthode `doGet` ou `doPost` d&#39;une servlet Java. Une meilleure pratique de programmation consiste à placer ce code dans une classe distincte. Instanciez ensuite la classe à partir de la méthode `doPost` (ou de la méthode `doGet`), puis appelez les méthodes appropriées. Toutefois, pour la concision du code, les exemples de code sont conservés au minimum et sont placés dans la méthode `doPost`.

Pour appeler le processus `FirstAppSolution/PreLoanProcess` à l’aide de l’API d’appel, effectuez les tâches suivantes :

1. Incluez des fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Récupérez les valeurs de nom, de téléphone et de montant envoyées à partir de la page HTML. Utilisez ces valeurs pour créer de manière dynamique une source de données XML envoyée au processus `FirstAppSolution/PreLoanProcess`. Vous pouvez utiliser les classes `org.w3c.dom` pour créer la source de données XML (cette logique d&#39;application est illustrée dans l&#39;exemple de code suivant).
1. Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Créez un objet `ServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. Un objet `ServiceClient` vous permet d’appeler une opération de service. Il gère des tâches telles que la localisation, la répartition et le routage des demandes d’appel.
1. Créez un objet `java.util.HashMap` en utilisant son constructeur.
1. Appelez la méthode `java.util.HashMap` de l’objet `put` pour chaque paramètre d’entrée à transmettre au processus de longue durée. Veillez à spécifier le nom des paramètres d’entrée du processus. Comme le processus `FirstAppSolution/PreLoanProcess` requiert un paramètre d&#39;entrée de type `XML` (nommé `formData`), vous ne devez appeler la méthode `put` qu&#39;une seule fois.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Créez un objet `InvocationRequest` en appelant la méthode `ServiceClientFactory` de l&#39;objet `createInvocationRequest` et en transmettant les valeurs suivantes :

   * Valeur string qui spécifie le nom du processus de longue durée à appeler. Pour appeler le processus `FirstAppSolution/PreLoanProcess`, spécifiez `FirstAppSolution/PreLoanProcess`.
   * Une valeur string qui représente le nom de l’opération de processus. Le nom de l’opération de processus de longue durée est `invoke`.
   * L’objet `java.util.HashMap` qui contient les valeurs de paramètre requises par l’opération de service.
   * Valeur booléenne qui spécifie `false`, qui crée une requête asynchrone (cette valeur est applicable pour appeler un processus de longue durée).

   >[!NOTE]
   >
   >*Un processus de courte durée peut être appelé en transmettant la valeur true en tant que quatrième paramètre de la méthode createInvocationRequest. La transmission de la valeur true crée une requête synchrone.*

1. Envoyez la demande d’appel à AEM Forms en appelant la méthode `ServiceClient` de l’objet `invoke` et en transmettant l’objet `InvocationRequest`. La méthode `invoke` renvoie un objet `InvocationReponse`.
1. Un processus de longue durée renvoie une valeur de chaîne qui représente une valeur d’identification d’appel. Récupérez cette valeur en appelant la méthode `getInvocationId` de l’objet `InvocationReponse`.

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. Ecrivez la valeur d’identification d’appel au navigateur Web client. Vous pouvez utiliser une instance `java.io.PrintWriter` pour écrire cette valeur dans le navigateur Web client.

### Début rapide : Appel d’un processus de longue durée à l’aide de l’API d’appel {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

L&#39;exemple de code Java suivant représente la servlet Java qui appelle le processus `FirstAppSolution/PreLoanProcess`.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### Créez la page Web de l’application Web {#create-the-web-page-for-the-web-application}

La page Web *index.html* fournit un point d’entrée à la servlet Java qui appelle le processus `FirstAppSolution/PreLoanProcess`. Cette page Web est un formulaire HTML de base qui contient un formulaire HTML et un bouton d’envoi. Lorsque l’utilisateur clique sur le bouton d’envoi, les données de formulaire sont publiées sur la servlet Java `SubmitXML`.

La servlet Java capture les données publiées à partir de la page HTML à l’aide du code Java suivant :

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

Le code HTML suivant représente le fichier index.html créé lors de la configuration de l’environnement de développement. (Voir [Création d’un projet Web](invoking-human-centric-long-lived.md#create-a-web-project).)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### Compresser l&#39;application Web dans un fichier WAR {#package-the-web-application-to-a-war-file}

Pour déployer la servlet Java qui appelle le processus `FirstAppSolution/PreLoanProcess`, incluez votre application Web dans un fichier WAR. Assurez-vous que les fichiers JAR externes dont dépend la logique métier du composant, tels que adobe-livecycle-client.jar et adobe-usermanager-client.jar, sont également inclus dans le fichier WAR.

L’illustration suivante présente le contenu du projet Eclipse, qui est présenté dans un fichier WAR.

>[!NOTE]
>
>Dans l’illustration précédente, le fichier JPG peut être remplacé par n’importe quel fichier image JPG.

**Créez un package d&#39;application Web dans un fichier WAR :**

1. Dans la fenêtre **Explorateur de projets**, cliquez avec le bouton droit sur le projet `InvokePreLoanProcess` et sélectionnez **Exporter** > **Fichier WAR**.
1. Dans la zone de texte **Module Web**, saisissez `InvokePreLoanProcess` pour le nom du projet Java.
1. Dans la zone de texte **Destination**, saisissez `PreLoanProcess.war`**pour le nom du fichier**, indiquez l’emplacement de votre fichier WAR, puis cliquez sur Terminer.

### Déployez le fichier WAR sur le serveur d’applications J2EE hébergeant AEM Forms {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}.

Déployez le fichier WAR sur le serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour déployer le fichier WAR sur le serveur d’applications J2EE, copiez le fichier WAR du chemin d’exportation vers `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>si AEM Forms n’est pas déployé sur JBoss, vous devez déployer le fichier WAR en conformité avec le serveur d’applications J2EE hébergeant AEM Forms.

### Testez votre application Web {#test-your-web-application}

Après avoir déployé l’application Web, vous pouvez la tester à l’aide d’un navigateur Web. En supposant que vous utilisiez le même ordinateur qui héberge AEM Forms, vous pouvez spécifier l’URL suivante :

* http://localhost:8080/PreLoanProcess/index.html

   Saisissez des valeurs dans les champs de formulaire HTML, puis cliquez sur le bouton Envoyer la demande. Si des problèmes se produisent, consultez le fichier journal du serveur d’applications J2EE.

>[!NOTE]
>
>Pour confirmer que l’application Java a appelé le processus, début Workspace et accepté le prêt.

## Création d&#39;une application Web ASP.NET qui appelle un processus de longue durée axé sur l&#39;humain {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

Vous pouvez créer une application ASP.NET qui appelle le processus `FirstAppSolution/PreLoanProcess`. Pour appeler ce processus à partir d&#39;une application ASP.NET, utilisez les services Web. (Voir [Appel d’AEM Forms à l’aide des services Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

L&#39;illustration suivante montre une application cliente ASP.NET qui obtient des données d&#39;un utilisateur final. Les données sont placées dans une source de données XML et envoyées au processus `FirstAppSolution/PreLoanProcess` lorsque l’utilisateur clique sur le bouton Envoyer la demande.

Notez qu’une fois le processus appelé, une valeur d’identificateur d’appel s’affiche. Une valeur d’identifiant d’appel est créée dans le cadre d’un enregistrement qui effectue le suivi de l’état du processus de longue durée.

L&#39;application ASP.NET exécute les tâches suivantes :

* Récupère les valeurs saisies par l’utilisateur dans la page Web.
* Crée de manière dynamique une source de données XML transmise au * PremierAppSolution/PreLoanProcess *. Les trois valeurs sont spécifiées dans la source de données XML.
* Appelle le *processus* FirstAppSolution/PreLoanProcess en utilisant les services Web.
* Renvoie la valeur de l’identifiant d’appel et l’état de l’opération de longue durée au navigateur Web client.

### Résumé des étapes {#summary_of_steps-1}

Pour créer une application ASP.NET capable d&#39;appeler le processus FirstAppSolution/PreLoanProcess, effectuez les étapes suivantes :

1. [Créez une application](invoking-human-centric-long-lived.md#create-an-asp-net-web-application) Web ASP.NET.
1. [Créez une page ASP qui appelle FirstAppSolution/PreLoanProcess](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [Exécutez l&#39;application](invoking-human-centric-long-lived.md#run-the-asp-net-application) ASP.NET.

### Créer une application Web ASP.NET {#create-an-asp-net-web-application}

Créez une Application web Microsoft .NET C# ASP.NET. L&#39;illustration suivante montre le contenu du projet ASP.NET nommé *InvokePreLoanProcess*.

Avis sous Références du service, il y a deux éléments. Le premier élément est nommé* JobManager*. Cette référence permet à l&#39;application ASP.NET d&#39;appeler le service Job Manager. Ce service renvoie des informations sur l’état d’un processus de longue durée. Par exemple, si le processus est en cours d’exécution, ce service renvoie une valeur numérique qui indique que le processus est en cours d’exécution. La seconde référence est appelée *PreLoanProcess*. Cette référence de service représente la référence au *processus* FirstAppSolution/PreLoanProcess. Une fois que vous avez créé une référence de service, les types de données associés au service AEM Forms peuvent être utilisés dans votre projet .NET.

**Créez un projet ASP.NET :**

1. Début Microsoft Visual Studio 2008.
1. Dans le menu **Fichier**, sélectionnez **Nouveau**, **Site Web**.
1. Dans la liste **Modèles**, sélectionnez **Site Web ASP.NET**.
1. Dans la zone **Emplacement**, sélectionnez un emplacement pour votre projet. Nommez votre projet *InvokePreLoanProcess*.
1. Dans la zone **Langage**, sélectionnez Visual C#
1. Cliquez sur OK.

**Ajouter les références de service :**

1. Dans le menu Projet, sélectionnez **Ajouter le service de référence**.
1. Dans la boîte de dialogue **Adresse**, spécifiez le fichier WSDL au service Job Manager.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. Dans le champ Espace de nommage, saisissez `JobManager`.
1. Cliquez sur **Aller** puis sur **OK**.
1. Dans le menu **Projet**, sélectionnez **Ajouter le service de référence**.
1. Dans la boîte de dialogue **Adresse**, spécifiez le fichier WSDL dans le processus FirstAppSolution/PreLoanProcess.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. Dans le champ Espace de nommage, saisissez `PreLoanProcess`.
1. Cliquez sur **Aller** puis sur **OK**.

>[!NOTE]
>
>Remplacez `hiro-xp` par l’adresse IP du serveur d’applications J2EE hébergeant AEM Forms. L’option `lc_version` garantit que la fonctionnalité AEM Forms, telle que MTOM, est disponible. Sans spécifier l’option `lc_version`, vous ne pouvez pas appeler AEM Forms à l’aide de MTOM. (Voir [Appeler AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### Créer une page ASP qui appelle FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

Dans le projet ASP.NET, ajoutez un formulaire Web (un fichier ASPX) qui est responsable de l&#39;affichage d&#39;une page HTML au demandeur du prêt. Le formulaire Web est basé sur une classe dérivée de `System.Web.UI.Page`. La logique d&#39;application C# qui appelle `FirstAppSolution/PreLoanProcess` se trouve dans la méthode `Button1_Click` (ce bouton représente le bouton Envoyer l&#39;application).

L&#39;illustration suivante montre l&#39;application ASP.NET

Le tableau suivant liste les contrôles qui font partie de cette application ASP.NET.

<table>
 <thead>
  <tr>
   <th><p>Nom du contrôle</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>Indique le prénom et le nom du client. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>Indique le téléphone ou l’adresse électronique du client. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>Indique le montant du prêt.</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>Représente le bouton Envoyer la demande.</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>Contrôle Label qui spécifie la valeur de l’identifiant d’appel.</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>Contrôle Label qui spécifie la valeur de l’état de la tâche. Cette valeur est récupérée en appelant le service Job Manager. </p></td>
  </tr>
 </tbody>
</table>

La logique d&#39;application qui fait partie de l&#39;application ASP.NET doit créer dynamiquement une source de données XML à transmettre au processus `FirstAppSolution/PreLoanProcess`. Les valeurs que le demandeur a entrées dans la page HTML doivent être spécifiées dans la source de données XML. Ces valeurs de données sont fusionnées dans le formulaire lorsque le formulaire est affiché dans Workspace. Les classes situées dans l&#39;espace de nommage `System.Xml` sont utilisées pour créer la source de données XML.

Lors de l&#39;appel d&#39;un processus qui requiert des données XML d&#39;une application ASP.NET, vous pouvez utiliser un type de données XML. Autrement dit, vous ne pouvez pas transmettre une instance `System.Xml.XmlDocument` au processus. Le nom qualifié complet de cette instance XML à transmettre au processus est `InvokePreLoanProcess.PreLoanProcess.XML`. Convertissez l&#39;instance `System.Xml.XmlDocument` en `InvokePreLoanProcess.PreLoanProcess.XML`. Vous pouvez exécuter cette tâche en utilisant le code suivant.

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

Pour créer une page ASP qui appelle le processus `FirstAppSolution/PreLoanProcess`, effectuez les tâches suivantes dans la méthode `Button1_Click` :

1. Créez un objet `FirstAppSolution_PreLoanProcessClient` en utilisant son constructeur par défaut.
1. Créez un objet `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transférez une valeur de chaîne qui spécifie le WSDL au service AEM Forms et le type de codage :

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Veillez toutefois à spécifier `?blob=mtom`.

   >[!NOTE]
   >
   >Remplacez `hiro-xp`* par l’adresse IP du serveur d’applications J2EE hébergeant AEM Forms. *

1. Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du membre de données `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
1. Définissez le membre de données `System.ServiceModel.BasicHttpBinding` de l&#39;objet `MessageEncoding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
1. Activez l’authentification HTTP de base en exécutant les tâches suivantes :

   * Affectez le nom d’utilisateur AEM forms au membre de données `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * Affectez la valeur de mot de passe correspondante au membre de données `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * Affectez la valeur constante `HttpClientCredentialType.Basic` au membre de données `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au membre de données `BasicHttpBindingSecurity.Security.Mode`.

   L&#39;exemple de code suivant montre ces tâches.

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. Récupérez les valeurs de nom, de téléphone et de montant saisies par l’utilisateur dans la page Web. Utilisez ces valeurs pour créer de manière dynamique une source de données XML envoyée au processus `FirstAppSolution/PreLoanProcess`. Créez un `System.Xml.XmlDocument` qui représente la source de données XML à transmettre au processus (cette logique d&#39;application est illustrée dans l&#39;exemple de code suivant).
1. Convertissez l&#39;instance `System.Xml.XmlDocument` en `InvokePreLoanProcess.PreLoanProcess.XML` (cette logique d&#39;application est illustrée dans l&#39;exemple de code suivant).
1. Appelez le processus `FirstAppSolution/PreLoanProcess` en appelant la méthode `FirstAppSolution_PreLoanProcessClient` de l’objet `invoke_Async`. Cette méthode renvoie une valeur de chaîne qui représente la valeur de l’identifiant d’appel du processus de longue durée.
1. Créez un `JobManagerClient` en utilisant son constructeur. (Vérifiez que vous avez défini une référence de service au service Job Manager.)
1. Répétez les étapes 1 à 5. Spécifiez l’URL suivante pour l’étape 2 : `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. Créez un objet `JobId` en utilisant son constructeur.
1. Définissez le membre de données `id` de l&#39;objet `JobId` avec la valeur renvoyée de la méthode `FirstAppSolution_PreLoanProcessClient` de l&#39;objet `invoke_Async`.
1. Affectez la valeur `value` true au membre de données `persistent` de l’objet `JobId`.
1. Créez un objet `JobStatus` en appelant la méthode `JobManagerService` de l&#39;objet `getStatus` et en transmettant l&#39;objet `JobId`.
1. Obtenez la valeur d’état en récupérant la valeur du membre de données `statusCode` de l’objet `JobStatus`.
1. Affectez la valeur d’identificateur d’appel au champ `LabelJobID.Text`.
1. Affectez la valeur d’état au champ `LabelStatus.Text`.

### Début rapide : Appel d’un processus de longue durée à l’aide de l’API du service Web {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

L&#39;exemple de code C# suivant appelle le processus `FirstAppSolution/PreLoanProcess`.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>Les valeurs situées dans la méthode définie par l’utilisateur getJobDescription correspondent aux valeurs renvoyées par le service Job Manager.

### Exécution de l&#39;application ASP.NET {#run-the-asp-net-application}

Après avoir compilé et déployé votre application ASP.NET, vous pouvez l&#39;exécuter à l&#39;aide d&#39;un navigateur Web. En supposant que le nom du projet ASP.NET soit *InvokePreLoanProcess*, spécifiez l&#39;URL suivante dans un navigateur Web :

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

où localhost est le nom du serveur Web hébergeant le projet ASP.NET et 1629 est le numéro de port. Lorsque vous compilez et générez votre application ASP.NET, Microsoft Visual Studio la déploie automatiquement.

>[!NOTE]
>
>Pour confirmer que l&#39;application ASP.NET a appelé le processus, début Workspace et accepté le prêt.

## Création d’une application cliente créée avec Flex qui appelle un processus de longue durée axé sur l’être humain {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Vous pouvez créer une application cliente créée avec Flex pour appeler le processus *FirstAppSolution/PreLoanProcess*. Cette application utilise Remoting pour appeler le processus *FirstAppSolution/PreLoanProcess*. (Voir [Appeler AEM Forms à l’aide de (obsolète pour les formulaires AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

L’illustration suivante présente une application cliente créée avec Flex pour collecter des données auprès d’un utilisateur final. Les données sont placées dans une source de données XML et envoyées au processus.

Notez qu’une fois le processus appelé, une valeur d’identificateur d’appel s’affiche. Une valeur d’identifiant d’appel est créée dans le cadre d’un enregistrement qui effectue le suivi de l’état du processus de longue durée.

L’application cliente générée avec Flex effectue les tâches suivantes :

* Récupère les valeurs saisies par l’utilisateur dans la page Web.
* Créez de manière dynamique une source de données XML transmise au processus *FirstAppSolution/PreLoanProcess*. Les trois valeurs sont spécifiées dans la source de données XML.
* Appelle le processus *FirstAppSolution/PreLoanProcess* en utilisant Remoting.
* Renvoie la valeur de l’identifiant d’appel du processus de longue durée.

### Résumé des étapes {#summary_of_steps-2}

Pour créer une application cliente créée avec Flex qui peut appeler le processus FirstAppSolution/PreLoanProcess, effectuez les étapes suivantes :

1. Début d&#39;un nouveau projet Flex.
1. Incluez le fichier adobe-remoting-provider.swc dans le chemin de classe de votre projet. (Voir [Inclusion du fichier de bibliothèque Flex AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. Créez une instance `mx:RemoteObject` par ActionScript ou MXML. (Voir [Création d’une instance mx:RemoteObject](/help/forms/developing/invoking-aem-forms-using-remoting.md)).
1. Configurez une instance `ChannelSet` pour communiquer avec AEM Forms et associez-la à l&#39;instance `mx:RemoteObject`. (Voir [Création d’un Canal à AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. Appelez la méthode `login` de ChannelSet ou la méthode `setCredentials` du service pour spécifier la valeur d&#39;identifiant utilisateur et le mot de passe. (Voir [Utilisation de la connexion unique](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Créez la source de données XML à transmettre au processus `FirstAppSolution/PreLoanProcess` en créant une instance XML. (Cette logique d’application est illustrée dans l’exemple de code suivant.)
1. Créez un objet de type Objet à l’aide de son constructeur. Affectez le code XML à l’objet en spécifiant le nom du paramètre d’entrée du processus, comme indiqué dans le code suivant :

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. Appelez le processus `FirstAppSolution/PreLoanProcess` en appelant la méthode `mx:RemoteObject` de l’instance `invoke_Async`. Transmettez le `Object` qui contient le paramètre d&#39;entrée. (Voir [Transmission des valeurs d’entrée](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. Récupérez la valeur d’identification d’appel qui est renvoyée à partir d’un processus de longue durée, comme indiqué dans le code suivant :

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Appel d’un processus de longue durée à l’aide de Remoting {#invoking-a-long-lived-process-using-remoting}

L&#39;exemple de code Flex suivant appelle le processus `FirstAppSolution/PreLoanProcess`.

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```

