---
title: Effectuer le rendu de formulaires PDF interactifs
description: Utilisez le service Forms pour effectuer le rendu des formulaires PDF interactifs sur les appareils clients, généralement les navigateurs web, afin de collecter des informations auprès des utilisateurs. Vous pouvez utiliser le service Forms pour générer des formulaires interactifs à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '2455'
ht-degree: 100%

---

# Effectuer le rendu de formulaires PDF interactifs {#rendering-interactive-pdf-forms}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le service Forms effectue le rendu de formulaires PDF interactifs sur les appareils clients, généralement les navigateurs web, afin de collecter des informations auprès des utilisateurs. Une fois le formulaire interactif généré, l’utilisateur peut saisir des données dans les champs du formulaire et cliquer sur un bouton d’envoi situé sur le formulaire pour renvoyer les informations au service Forms. Adobe Reader ou Acrobat doit être installé sur l’ordinateur hébergeant le navigateur web client pour qu’un formulaire PDF interactif soit visible.

>[!NOTE]
>
>Avant de pouvoir générer un formulaire à l’aide du service Forms, vous devez créer une conception de formulaire. En règle générale, une conception de formulaire est créée dans Designer et enregistrée en tant que fichier XDP. Pour plus d’informations sur la création d’une conception de formulaire, consultez la section [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

**Exemple de demande de prêt**

Cet exemple de demande de prêt permet de démontrer comment le service Forms utilise des formulaires interactifs pour collecter des informations auprès des utilisateurs. Cette demande permet à un utilisateur de remplir un formulaire avec les données nécessaires pour sécuriser un prêt, puis d’envoyer les données au service Forms. Le diagramme suivant illustre le cheminement logique de la demande de prêt.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

Le tableau suivant décrit les étapes de ce diagramme.

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Le servlet Java <code>GetLoanForm</code> est appelé à partir d’une page HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le servlet Java <code>GetLoanForm</code> utilise l’API cliente du service Forms pour effectuer le rendu du formulaire de prêt vers le navigateur web client. (Consultez la section <a href="#render-an-interactive-pdf-form-using-the-java-api">Générer un formulaire PDF interactif à l’aide de l’API Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Une fois que l’utilisateur a rempli le formulaire de prêt et cliqué sur le bouton d’envoi, les données sont envoyées au servlet Java <code>HandleData</code>. (Reportez-vous à <i>« Formulaire de prêt »</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le servlet Java <code>HandleData</code> utilise l’API cliente du service Forms pour traiter l’envoi du formulaire et récupérer ses données. Les données sont ensuite stockées dans une base de données d’entreprise. (Consultez la section <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gérer les Forms envoyés</a>).</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Un formulaire de confirmation est renvoyé au navigateur web. Les données telles que le prénom et le nom de l’utilisateur ou l’utilisatrice sont fusionnées avec le formulaire avant son rendu. (Consultez la section <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Préremplir des formulaires avec des dispositions fluides</a>).</p></td>
  </tr>
 </tbody>
</table>

**Formulaire de prêt**

Ce formulaire interactif de prêt est rendu par le servlet Java `GetLoanForm` de lʼexemple de demande de prêt.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulaire de confirmation**

Ce formulaire est rendu par le servlet Java `HandleData` de l’exemple de demande de prêt.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Le servlet Java `HandleData` préremplit ce formulaire avec le prénom et le nom de l’utilisateur ou l’utilisatrice, ainsi qu’avec le montant. Une fois le formulaire prérempli, il est envoyé au navigateur web client. (Consultez la section [Préremplir des formulaires avec des dispositions fluides](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).

**Servlets Java**

L’exemple de demande de prêt est un exemple d’application de service Forms qui existe en tant que servlet Java. Un servlet Java est un programme Java exécuté sur un serveur d’applications J2EE, tel que WebSphere, qui contient le code de l’API cliente du service Forms.

Le code suivant affiche la syntaxe d’un servlet Java nommé GetLoanForm :

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

En règle générale, vous ne placez pas le code de l’API cliente du service Forms dans une méthode `doGet` ou `doPost` d’un servlet Java. Une bonne pratique en matière de programmation consiste à placer ce code dans une classe distincte. Instanciez la classe depuis la méthode `doPost` (ou `doGet`) et appelez les méthodes appropriées. Toutefois, pour des raisons de concision du code, les exemples de code de cette section sont réduits au minimum et les exemples de code sont placés dans la méthode `doPost`.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

**Résumé des étapes**

Pour effectuer le rendu d’un formulaire PDF interactif, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Spécifier les valeurs URI
1. Joignez des fichiers au formulaire (facultatif).
1. Générez un formulaire PDF interactif.
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créez un objet API client Forms**

Avant d’effectuer par programmation une opération de l’API cliente du service Forms, vous devez créer un objet API client Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API du service web Forms, créez un objet `FormsService`.

**Spécifier les valeurs URI**

Vous pouvez spécifier les valeurs URI requises par le service Forms pour générer un formulaire. Une conception de formulaire enregistrée dans le cadre d’une application Forms peut être référencée à l’aide de la valeur de lʼURI racine du contenu `repository:///`. Prenons l’exemple de conception de formulaire suivante nommée *Loan.xdp*, située dans une application Forms nommée *FormsApplication* :

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Pour accéder à cette conception de formulaire, spécifiez `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` comme nom du formulaire (premier paramètre transmis à la méthode `renderPDFForm`) et `repository:///` comme valeur de l’URI racine du contenu.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, consultez la section [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).

Le chemin d’accès à une ressource dans une application Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes présentent quelques exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Lorsque vous effectuez le rendu d’un formulaire interactif, vous pouvez définir des valeurs d’URI telles que l’URL cible vers laquelle les données de formulaire sont publiées. L’URL cible peut être définie de l’une des manières suivantes :

* Sur le bouton Envoyer lors de la conception de formulaire dans Designer
* En utilisant l’API cliente du service Forms

Si l’URL cible est définie dans la conception de formulaire, ne la remplacez pas par l’API cliente du service Forms. En d’autres termes, la définition de l’URL cible à l’aide de l’API Forms remplace l’URL spécifiée dans la conception de formulaire par celle spécifiée à l’aide de l’API. Si vous souhaitez envoyer le formulaire PDF à l’URL cible spécifiée dans la conception de formulaire, définissez l’URL cible par programmation sur une chaîne vide.

Si vous disposez d’un formulaire contenant un bouton d’envoi et un bouton de calcul (avec un script correspondant s’exécutant sur le serveur), vous pouvez définir par programmation l’URL vers laquelle le formulaire est envoyé pour exécuter le script. Utilisez le bouton d’envoi de la conception de formulaire pour spécifier l’URL vers laquelle les données de formulaire sont publiées. (Consultez la section [Calculer les données de formulaire](/help/forms/developing/calculating-form-data.md)).

>[!NOTE]
>
>Au lieu de spécifier une valeur d’URL pour référencer un fichier XDP, vous pouvez également transmettre une instance `com.adobe.idp.Document` au service Forms. L’instance `com.adobe.idp.Document` contient une conception de formulaire. (Consultez la section [Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)).

**Joindre des fichiers au formulaire**

Vous pouvez joindre des fichiers à un formulaire. Lorsque vous générez un formulaire PDF avec des pièces jointes, les utilisateurs peuvent récupérer ces pièces jointes dans Acrobat à l’aide du volet des pièces jointes. Vous pouvez joindre différents types de fichiers à un formulaire (un fichier texte, par exemple) ou à un fichier binaire (un fichier JPG, par exemple).

>[!NOTE]
>
>Il nʼest pas obligatoire d’attacher des pièces jointes à un formulaire.

**Générer un formulaire PDF interactif**

Pour générer un formulaire, utilisez une conception de formulaire créée dans Designer et enregistrée au format XDP ou PDF. Vous pouvez également générer un formulaire créé à l’aide d’Acrobat et enregistré en tant que fichier PDF. Pour effectuer le rendu d’un formulaire PDF interactif, appelez la méthode `renderPDFForm` ou `renderPDFForm2` de lʼobjet `FormsServiceClient`.

La méthode `renderPDFForm` utilise un objet `URLSpec`. La racine de contenu du fichier XDP est transmise au service Forms à l’aide de la méthode `setContentRootURI` de l’objet `URLSpec`. Le nom de la conception de formulaire (`formQuery`) est transmis en tant que valeur de paramètre distincte. Les deux valeurs sont concaténées afin d’obtenir la référence absolue de la conception de formulaire.

La méthode `renderPDFForm2` accepte une instance `com.adobe.idp.Document` contenant le document XDP ou PDF à rendre.

>[!NOTE]
>
>L’option d’exécution du PDF balisé ne peut pas être définie si le document d’entrée est au format PDF. Si le fichier d’entrée est un fichier XDP, l’option de PDF balisé peut être définie.

## Générer un formulaire PDF interactif à l’aide de l’API Java {#render-an-interactive-pdf-form-using-the-java-api}

Pour générer un formulaire PDF interactif à l’aide de l’API Forms (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre chemin de classe de projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Spécifier les valeurs URI

   * Créez un objet `URLSpec` stockant des valeurs URI en utilisant son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur de chaîne qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URI de la racine de contenu. Assurez-vous que l’URI de la racine de contenu contient la conception du formulaire. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository:///`.
   * Appelez la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URL cible où sont publiées les données de formulaire. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL où est envoyé un formulaire pour effectuer des calculs.

1. Joindre des fichiers au formulaire

   * Créez un objet `java.util.HashMap` afin de stocker les pièces jointes en utilisant son constructeur.
   * Appelez la méthode `put` de l’objet `java.util.HashMap` pour chaque fichier à joindre au formulaire rendu. Transmettez les valeurs suivantes à cette méthode :

      * Une valeur de chaîne qui spécifie le nom de la pièce jointe, y compris l’extension du nom de fichier.

   * Un objet `com.adobe.idp.Document` contenant la pièce jointe.

   >[!NOTE]
   >
   >Répétez cette étape pour chaque fichier à joindre au formulaire. Cette étape est facultative et vous pouvez transmettre `null` si vous ne souhaitez pas envoyer de pièces jointes.

1. Effectuer le rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document`.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution. Ce paramètre est facultatif et vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données du formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

## Générer un formulaire PDF interactif à l’aide de l’API de service web {#render-an-interactive-pdf-form-using-the-web-service-api}

Pour générer un formulaire PDF interactif à l’aide de l’API Forms (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Spécifier les valeurs URI

   * Créez un objet `URLSpec` stockant des valeurs URI en utilisant son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur de chaîne qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URI de la racine de contenu. Assurez-vous que l’URI de la racine de contenu contient la conception du formulaire. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository:///`.
   * Appelez la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URL cible où sont publiées les données de formulaire. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL où est envoyé un formulaire pour effectuer des calculs.

1. Joindre des fichiers au formulaire

   * Créez un objet `java.util.HashMap` afin de stocker les pièces jointes en utilisant son constructeur.
   * Appelez la méthode `put` de l’objet `java.util.HashMap` pour chaque fichier à joindre au formulaire rendu. Transmettez les valeurs suivantes à cette méthode :

      * Une valeur de chaîne qui spécifie le nom de la pièce jointe, y compris l’extension de nom de fichier.

   * Un objet `BLOB` contenant la pièce jointe.

   >[!NOTE]
   >
   >Répétez cette étape pour chaque fichier à joindre au formulaire.

1. Effectuer le rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution. Ce paramètre est facultatif et vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Il permet de stocker le formulaire PDF rendu.
   * Un objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. (Cet argument stocke le nombre de pages dans le formulaire).
   * Un objet `javax.xml.rpc.holders.StringHolder` qui est renseigné par la méthode. (Cet argument stocke la valeur du paramètre régional).
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` qui contient les données du formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données du formulaire vers le navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Écrire le flux de données de formulaire dans le navigateur web client**

Lorsque le service Forms effectue la restitution d’un formulaire, il renvoie un flux de données de formulaire que vous devez enregistrer dans le navigateur web du client. Lorsqu’il est écrit dans le navigateur web client, le formulaire est visible par l’utilisateur.
