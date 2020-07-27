---
title: Calcul des données de formulaire
seo-title: Calcul des données de formulaire
description: 'null'
seo-description: 'null'
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 2%

---


# Calcul des données de formulaire {#calculating-form-data}

Le service Forms peut calculer les valeurs qu’un utilisateur saisit dans un formulaire et afficher les résultats. Pour calculer les données de formulaire, vous devez effectuer deux tâches. Tout d’abord, vous créez un script de conception de formulaire qui calcule les données de formulaire. Une conception de formulaire prend en charge trois types de scripts. Un type de script est exécuté sur le client, un autre sur le serveur et le troisième sur le serveur et le client. Le type de script décrit dans cette rubrique s’exécute sur le serveur. Les calculs côté serveur sont pris en charge pour les transformations HTML, PDF et Form Guide (obsolète).

Dans le cadre du processus de conception de formulaire, vous pouvez utiliser des calculs et des scripts pour offrir une expérience utilisateur plus riche. Les calculs et les scripts peuvent être ajoutés à la plupart des champs et objets de formulaire. Vous devez créer un script de conception de formulaire pour effectuer des opérations de calcul sur les données saisies par un utilisateur dans un formulaire interactif.

L’utilisateur saisit des valeurs dans le formulaire et clique sur le bouton Calculer pour vue des résultats. Le processus suivant décrit un exemple d’application qui permet à un utilisateur de calculer des données :

* L’utilisateur accède à une page HTML nommée StartLoan.html qui fait office de page de début de l’application Web. Cette page appelle une servlet Java nommée `GetLoanForm`.
* La `GetLoanForm` servlet génère un formulaire de prêt. Ce formulaire contient un script, des champs interactifs, un bouton Calculer et un bouton Envoyer.
* L’utilisateur saisit des valeurs dans les champs du formulaire et clique sur le bouton Calculer. Le formulaire est envoyé au servlet `CalculateData` Java où le script est exécuté. Le formulaire est renvoyé à l’utilisateur avec les résultats de calcul affichés dans le formulaire.
* L’utilisateur continue à saisir et à calculer les valeurs jusqu’à ce qu’un résultat satisfaisant s’affiche. Lorsque l’utilisateur est satisfait, il clique sur le bouton Envoyer pour traiter le formulaire. Le formulaire est envoyé à un autre servlet Java nommé `ProcessForm` qui est chargé de récupérer les données envoyées. (Voir [Gestion des formulaires](/help/forms/developing/rendering-forms.md#handling-submitted-forms)envoyés.)


Le diagramme suivant illustre le flux logique de l’application.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

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
   <td><p>La servlet <code>GetLoanForm</code> Java est appelée à partir de la page début HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Le servlet <code>GetLoanForm</code> Java utilise l’API Client du service Forms pour générer le formulaire de prêt au navigateur Web client. La différence entre le rendu d’un formulaire qui contient un script configuré pour s’exécuter sur le serveur et le rendu d’un formulaire qui ne contient pas de script est que vous devez spécifier l’emplacement de cible utilisé pour exécuter le script. Si aucun emplacement de cible n’est spécifié, un script configuré pour s’exécuter sur le serveur n’est pas exécuté. Prenons l’exemple de l’application présentée dans cette section. Le servlet <code>CalculateData</code> Java est l’emplacement de cible où le script est exécuté.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utilisateur saisit des données dans des champs interactifs et clique sur le bouton Calculer. Le formulaire est envoyé à la servlet <code>CalculateData</code> Java, où le script est exécuté. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le formulaire est rendu au navigateur Web avec les résultats de calcul affichés dans le formulaire. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>L’utilisateur clique sur le bouton Envoyer lorsque les valeurs sont satisfaisantes. Le formulaire est envoyé à une autre servlet Java nommée <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

En règle générale, un formulaire envoyé en tant que contenu PDF contient des scripts exécutés sur le client. Cependant, les calculs côté serveur peuvent également être exécutés. Impossible d’utiliser un bouton Envoyer pour calculer les scripts. Dans ce cas, les calculs ne sont pas exécutés car le service Forms considère que l’interaction est terminée.

Pour illustrer l’utilisation d’un script de conception de formulaire, cette section examine un formulaire interactif simple qui contient un script configuré pour s’exécuter sur le serveur. Le diagramme suivant présente une conception de formulaire contenant un script qui ajoute des valeurs saisies par un utilisateur dans les deux premiers champs et affiche le résultat dans le troisième champ.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Champ nommé NumericField1 **B.** Champ nommé NumericField2 **C.** Champ nommé NumericField3

La syntaxe du script se trouvant dans cette conception de formulaire est la suivante :

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Dans cette conception de formulaire, le bouton Calculer est un bouton de commande et le script se trouve dans le `Click` événement de ce bouton. Lorsqu’un utilisateur saisit des valeurs dans les deux premiers champs (NumericField1 et NumericField2) et clique sur le bouton Calculer, le formulaire est envoyé au service Forms, où le script est exécuté. Le service Forms restitue le formulaire au périphérique client avec les résultats du calcul affichés dans le champ NumericField3.

>[!NOTE]
>
>Pour plus d’informations sur la création d’un script de conception de formulaire, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour calculer les données de formulaire, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API du client Forms.
1. Récupérez un formulaire contenant un script de calcul.
1. Réécriture du flux de données de formulaire dans le navigateur Web client

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un `FormsServiceClient` objet. Si vous utilisez l’API du service Web de Forms, créez un `FormsServiceService` objet.

**Récupération d’un formulaire contenant un script de calcul**

Utilisez l’API Client du service Forms pour créer une logique d’application qui gère un formulaire contenant un script configuré pour s’exécuter sur le serveur. Le processus est similaire à la gestion d’un formulaire envoyé. (Voir [Gestion des formulaires](/help/forms/developing/handling-submitted-forms.md)envoyés.)

Vérifiez que l’état de traitement associé au formulaire envoyé est `1``(Calculate)`le cas, ce qui signifie que le service Forms effectue une opération de calcul sur les données du formulaire et que les résultats doivent être consignés à l’utilisateur. Dans ce cas, un script configuré pour s’exécuter sur le serveur est exécuté automatiquement.

**Réécriture du flux de données de formulaire dans le navigateur Web client**

Une fois que vous avez vérifié l’état de traitement associé à un formulaire envoyé `1`, vous devez réécrire les résultats dans le navigateur Web client. Lorsque le formulaire est affiché, la valeur calculée s’affiche dans le ou les champs appropriés.

**Voir aussi**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calculer les données de formulaire à l’aide de l’API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)[Java Calculer les données de formulaire à l’aide de l’API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)[du service Web Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)[API du service Forms Débuts](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)Rendu de PDF forms interactifsCréation d’Applications web renvoyant des formulaires[](/help/forms/developing/rendering-interactive-pdf-forms.md)[](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcul des données de formulaire à l’aide de l’API Java {#calculate-form-data-using-the-java-api}

Calculez les données de formulaire à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Récupération d’un formulaire contenant un script de calcul

   * Pour récupérer des données de formulaire contenant un script de calcul, créez un `com.adobe.idp.Document` objet à l’aide de son constructeur et appelez la méthode de l’ `javax.servlet.http.HttpServletResponse` objet `getInputStream` depuis le constructeur.
   * Appelez la méthode `FormsServiceClient` de l’ `processFormSubmission` objet et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant les données du formulaire.
      * Valeur de chaîne qui spécifie les variables d’environnement, y compris tous les en-têtes HTTP appropriés. Vous devez spécifier le type de contenu à gérer en spécifiant une ou plusieurs valeurs pour la variable `CONTENT_TYPE` environnement. Par exemple, pour gérer les données XML et PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` qui stocke les options d’exécution.

      La `processFormSubmission` méthode renvoie un `FormsResult` objet contenant les résultats de l’envoi du formulaire.

   * Vérifiez que l’état de traitement associé à un formulaire envoyé est `1` en appelant la `FormsResult` méthode de l’ `getAction` objet. Si cette méthode renvoie la valeur `1`, le calcul a été effectué et les données peuvent être renvoyées au navigateur Web client.


1. Réécriture du flux de données de formulaire dans le navigateur Web client

   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir aussi**


[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcul des données de formulaire à l’aide de l’API de service Web {#calculate-form-data-using-the-web-service-api}

Calculez les données de formulaire à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Récupération d’un formulaire contenant un script de calcul

   * Pour récupérer les données de formulaire publiées sur un servlet Java, créez un `BLOB` objet à l’aide de son constructeur.
   * Créez un `java.io.InputStream` objet à l’aide de la `javax.servlet.http.HttpServletResponse` méthode de l’ `getInputStream` objet.
   * Create a `java.io.ByteArrayOutputStream` object by using its constructor and passing the length of the `java.io.InputStream` object.
   * Copiez le contenu de l’ `java.io.InputStream` objet dans l’ `java.io.ByteArrayOutputStream` objet.
   * Créez un tableau d’octets en appelant la `java.io.ByteArrayOutputStream` méthode de l’ `toByteArray` objet.
   * Renseignez l’ `BLOB` objet en appelant sa `setBinaryData` méthode et en transmettant le tableau d’octets comme argument.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la `RenderOptionsSpec` `setLocale` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional.
   * Appelez la méthode `FormsServiceClient` de l’ `processFormSubmission` objet et transmettez les valeurs suivantes :

      * Objet `BLOB` contenant les données du formulaire.
      * Une valeur de chaîne qui spécifie des variables d’environnement inclut tous les en-têtes HTTP appropriés. Par exemple, vous pouvez spécifier la valeur de chaîne suivante : `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` qui stocke les options d’exécution. Pour plus d’informations, .
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode.
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `BLOBHolder` rempli par la méthode.
      * Objet vide `javax.xml.rpc.holders.ShortHolder` rempli par la méthode.
      * Objet vide `MyArrayOf_xsd_anyTypeHolder` rempli par la méthode. Ce paramètre permet de stocker les pièces jointes envoyées avec le formulaire.
      * Objet vide `FormsResultHolder` rempli par la méthode avec le formulaire envoyé.

      La `processFormSubmission` méthode renseigne le `FormsResultHolder` paramètre avec les résultats de l’envoi du formulaire. La `processFormSubmission` méthode renvoie un `FormsResult` objet contenant les résultats de l’envoi du formulaire.

   * Vérifiez que l’état de traitement associé à un formulaire envoyé est `1` en appelant la `FormsResult` méthode de l’ `getAction` objet. Si cette méthode renvoie la valeur `1`, le calcul a été effectué et les données peuvent être renvoyées au navigateur Web client.


1. Réécriture du flux de données de formulaire dans le navigateur Web client

   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour envoyer un flux de données de formulaire au navigateur Web client.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Créez un tableau d’octets et remplissez-le en appelant la `BLOB` `getBinaryData` méthode de l’objet. Cette tâche affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir aussi**[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
