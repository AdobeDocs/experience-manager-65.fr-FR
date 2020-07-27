---
title: Rendu des PDF forms interactifs
seo-title: Rendu des PDF forms interactifs
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 0%

---


# Rendu des PDF forms interactifs {#rendering-interactive-pdf-forms}

Le service Forms effectue le rendu de PDF forms interactifs sur les périphériques clients, généralement les navigateurs Web, afin de recueillir des informations auprès des utilisateurs. Une fois qu’un formulaire interactif est rendu, un utilisateur peut saisir des données dans les champs du formulaire et cliquer sur un bouton d’envoi situé sur le formulaire pour renvoyer les informations au service Forms. Adobe Reader ou Acrobat doit être installé sur l’ordinateur hébergeant le navigateur Web client pour qu’un formulaire PDF interactif soit visible.

>[!NOTE]
>
>Avant de pouvoir générer un formulaire à l’aide du service Forms, vous devez créer une conception de formulaire. En règle générale, une conception de formulaire est créée dans Designer et enregistrée dans un fichier XDP. Pour plus d’informations sur la création d’une conception de formulaire, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exemple de demande de prêt**

Un exemple de demande de prêt est présenté pour montrer comment le service Forms utilise des formulaires interactifs pour collecter des informations auprès des utilisateurs. Cette application permet à un utilisateur de remplir un formulaire avec les données nécessaires pour sécuriser un prêt, puis d’envoyer les données au service Forms. Le diagramme suivant présente le flux logique de la demande de prêt.

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
   <td><p>La servlet <code>GetLoanForm</code> Java est appelée à partir d’une page HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le servlet <code>GetLoanForm</code> Java utilise l’API Client du service Forms pour générer le formulaire de prêt au navigateur Web client. (voir <a href="#render-an-interactive-pdf-form-using-the-java-api">Rendu d’un formulaire PDF interactif à l’aide de l’API</a>Java).</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Une fois que l’utilisateur a rempli le formulaire de prêt et cliqué sur le bouton d’envoi, les données sont envoyées au servlet <code>HandleData</code> Java Servlet. (Voir <i>"Formulaire de prêt"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le servlet <code>HandleData</code> Java utilise l’API Client du service Forms pour traiter l’envoi du formulaire et récupérer les données du formulaire. Les données sont ensuite stockées dans une base de données d’entreprise. (Voir <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestion des formulaires</a>envoyés.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Un formulaire de confirmation est rendu au navigateur Web. Les données telles que le prénom et le nom de l’utilisateur sont fusionnées avec le formulaire avant d’être générées. (Voir <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Préremplissage de formulaires avec des dispositions</a>à disposition souple.)</p></td>
  </tr>
 </tbody>
</table>

**Formulaire de prêt**

Ce formulaire de prêt interactif est généré par le servlet `GetLoanForm` Java de la demande de prêt d’exemple.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulaire de confirmation**

Ce formulaire est généré par le servlet `HandleData` Java de la demande de prêt d’exemples.

![ri_ri_verify](assets/ri_ri_confirm.png)

Le servlet `HandleData` Java préremplit ce formulaire avec le prénom et le nom de l’utilisateur, ainsi que le montant. Une fois le formulaire prérempli, il est envoyé au navigateur Web client. (Voir [Préremplissage de formulaires avec des dispositions](/help/forms/developing/prepopulating-forms-flowable-layouts.md)souple).

**Servlets Java**

L’exemple de demande de prêt est un exemple d’application de service Forms qui existe en tant que servlet Java. Un servlet Java est un programme Java s’exécutant sur un serveur d’applications J2EE, tel que WebSphere, et contient le code API du client du service Forms.

Le code suivant montre la syntaxe d&#39;une servlet Java appelée GetLoanForm :

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalement, vous ne placez pas le code API du client du service Forms dans une méthode `doGet` ou une méthode Java Servlet `doPost` . Il est plus pratique de programmer de placer ce code dans une classe distincte, d&#39;instancier la classe à partir de la `doPost` méthode (ou `doGet` méthode) et d&#39;appeler les méthodes appropriées. Toutefois, pour la concision du code, les exemples de code de cette section sont maintenus au minimum et les exemples de code sont placés dans la `doPost` méthode.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Résumé des étapes**

Pour générer un formulaire PDF interactif, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API du client Forms.
1. Spécifiez des valeurs URI.
1. Joindre des fichiers au formulaire (facultatif).
1. Générer un formulaire PDF interactif
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API du client du service Forms, vous devez créer un objet d’API du client Forms. Si vous utilisez l’API Java, créez un `FormsServiceClient` objet. Si vous utilisez l’API du service Web de Forms, créez un `FormsService` objet.

**Spécification des valeurs URI**

Vous pouvez spécifier les valeurs URI requises par le service Forms pour générer un formulaire. Une conception de formulaire enregistrée dans le cadre d’une application Forms peut être référencée à l’aide de la valeur URI racine de contenu `repository:///`. Prenons l’exemple de la conception de formulaire suivante, appelée *Loan.xdp* , située dans une application Forms appelée *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Pour accéder à cette conception de formulaire, spécifiez `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` le nom du formulaire (le premier paramètre transmis à la `renderPDFForm` méthode) et `repository:///` la valeur URI racine du contenu.

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Forms à l’aide de Workbench, voir Aide [de](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.

Le chemin d’accès à une ressource située dans une application Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Les valeurs suivantes présentent quelques exemples de valeurs URI :

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Lorsque vous générez un formulaire interactif, vous pouvez définir des valeurs d’URI telles que l’URL de la cible vers laquelle les données du formulaire sont publiées. L’URL de la cible peut être définie de l’une des manières suivantes :

* Sur le bouton Envoyer lors de la conception de la conception de formulaire dans Designer
* En utilisant l’API du client du service Forms

Si l’URL de la cible est définie dans la conception de formulaire, ne la remplacez pas par l’API Client du service Forms. En d’autres termes, la définition de l’URL de cible à l’aide de l’API Forms réinitialise l’URL spécifiée dans la conception de formulaire à celle spécifiée à l’aide de l’API. Si vous souhaitez envoyer le formulaire PDF à l’URL de cible spécifiée dans la conception de formulaire, définissez par programmation l’URL de la cible sur une chaîne vide.

Si vous disposez d’un formulaire contenant un bouton d’envoi et un bouton de calcul (avec un script correspondant s’exécutant sur le serveur), vous pouvez définir par programmation l’URL vers laquelle le formulaire est envoyé pour exécuter le script. Utilisez le bouton d’envoi sur la conception de formulaire pour spécifier l’URL vers laquelle les données du formulaire sont publiées. (Voir [Calcul des données](/help/forms/developing/calculating-form-data.md)de formulaire.)

>[!NOTE]
>
>Au lieu de spécifier une valeur d’URL pour référencer un fichier XDP, vous pouvez également transmettre une `com.adobe.idp.Document` instance au service Forms. L’ `com.adobe.idp.Document` instance contient une conception de formulaire. (Voir [Transmission de Documents au service](/help/forms/developing/passing-documents-forms-service.md)Forms.)

**Joindre des fichiers au formulaire**

Vous pouvez joindre des fichiers à un formulaire. Lorsque vous générez un formulaire PDF contenant des pièces jointes, les utilisateurs peuvent récupérer les pièces jointes dans Acrobat à l’aide du volet de pièces jointes. Vous pouvez associer différents types de fichier à un formulaire, tel qu’un fichier texte, ou à un fichier binaire tel qu’un fichier JPG.

>[!NOTE]
>
>Le fait de joindre des pièces jointes à un formulaire est facultatif.

**Génération d’un formulaire PDF interactif**

Pour générer un formulaire, utilisez une conception de formulaire créée dans Designer et enregistrée dans un fichier XDP ou PDF. Vous pouvez également générer un formulaire créé à l’aide d’Acrobat et enregistré au format PDF. Pour générer un formulaire PDF interactif, appelez la `FormsServiceClient` méthode ou la `renderPDFForm` `renderPDFForm2` méthode de l’objet.

L’objet `renderPDFForm` utilise un `URLSpec` objet. La racine de contenu du fichier XDP est transmise au service Forms à l’aide de la `URLSpec` méthode de l’objet `setContentRootURI` . Le nom de la conception de formulaire ( `formQuery`) est transmis en tant que valeur de paramètre distincte. Les deux valeurs sont concaténées pour obtenir la référence absolue à la conception de formulaire.

La `renderPDFForm2` méthode accepte une `com.adobe.idp.Document` instance contenant le document XDP ou PDF à rendre.

>[!NOTE]
>
>L’option d’exécution PDF balisé ne peut pas être définie si le document d’entrée est un document PDF. Si le fichier d’entrée est un fichier XDP, l’option PDF balisé peut être définie.

## Générer un formulaire PDF interactif à l’aide de l’API Java {#render-an-interactive-pdf-form-using-the-java-api}

Générer un formulaire PDF interactif à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Spécification des valeurs URI

   * Créez un `URLSpec` objet qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `URLSpec` de l’objet `setApplicationWebRoot` et transmettez une valeur de chaîne qui représente la racine Web de l’application.
   * Appelez la méthode `URLSpec` de l’objet `setContentRootURI` et transmettez une valeur de chaîne qui spécifie la valeur URI racine du contenu. Assurez-vous que la conception de formulaire se trouve dans l’URI racine de contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository:///`.
   * Appelez la `URLSpec` méthode de l’ `setTargetURL` objet et transmettez une valeur de chaîne qui spécifie la valeur de l’URL de cible à l’endroit où les données du formulaire sont publiées. Si vous définissez l’URL de la cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer des calculs.

1. Joindre des fichiers au formulaire

   * Créez un `java.util.HashMap` objet pour stocker les pièces jointes en utilisant son constructeur.
   * Appelez la méthode `java.util.HashMap` de l’objet `put` pour chaque fichier à joindre au formulaire généré. Transmettez les valeurs suivantes à cette méthode :

      * Valeur de chaîne qui spécifie le nom du fichier joint, y compris l’extension du nom de fichier.
   * Objet `com.adobe.idp.Document` contenant la pièce jointe du fichier.

   >[!NOTE]
   >
   >Répétez cette étape pour chaque fichier à joindre au formulaire. Cette étape est facultative et vous pouvez la passer `null` si vous ne souhaitez pas envoyer de pièces jointes.

1. Génération d’un formulaire PDF interactif

   Appelez la méthode `FormsServiceClient` de l’ `renderPDFForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

## Générer un formulaire PDF interactif à l’aide de l’API du service Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Générer un formulaire PDF interactif à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Spécification des valeurs URI

   * Créez un `URLSpec` objet qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `URLSpec` de l’objet `setApplicationWebRoot` et transmettez une valeur de chaîne qui représente la racine Web de l’application.
   * Appelez la méthode `URLSpec` de l’objet `setContentRootURI` et transmettez une valeur de chaîne qui spécifie la valeur URI racine du contenu. Assurez-vous que la conception de formulaire se trouve dans l’URI racine de contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository:///`.
   * Appelez la `URLSpec` méthode de l’ `setTargetURL` objet et transmettez une valeur de chaîne qui spécifie la valeur de l’URL de cible à l’endroit où les données du formulaire sont publiées. Si vous définissez l’URL de la cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer des calculs.

1. Joindre des fichiers au formulaire

   * Créez un `java.util.HashMap` objet pour stocker les pièces jointes en utilisant son constructeur.
   * Appelez la méthode `java.util.HashMap` de l’objet `put` pour chaque fichier à joindre au formulaire généré. Transmettez les valeurs suivantes à cette méthode :

      * Valeur de chaîne spécifiant le nom du fichier joint, y compris l’extension du nom de fichier
   * Objet `BLOB` contenant la pièce jointe du fichier

   >[!NOTE]
   >
   >Répétez cette étape pour chaque fichier à joindre au formulaire.

1. Génération d’un formulaire PDF interactif

   Appelez la méthode `FormsService` de l’ `renderPDFForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` rempli par la méthode. Elle permet de stocker le formulaire PDF rendu.
   * Objet vide `javax.xml.rpc.holders.LongHolder` rempli par la méthode. (Cet argument stocke le nombre de pages dans le formulaire.)
   * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode. (Cet argument stocke la valeur du paramètre régional.)
   * Objet vide `com.adobe.idp.services.holders.FormsResultHolder` qui contiendra les résultats de cette opération.

   La `renderPDFForm` méthode remplit l’ `com.adobe.idp.services.holders.FormsResultHolder` objet transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `FormResult` objet en obtenant la valeur du membre `com.adobe.idp.services.holders.FormsResultHolder` de données de l’ `value` objet.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `BLOB` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `BLOB` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un tableau d’octets et remplissez-le en appelant la `BLOB` `getBinaryData` méthode de l’objet. Cette tâche affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible pour l’utilisateur.
