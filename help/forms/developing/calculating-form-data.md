---
title: Calcul de données de formulaire
description: Utilisez le service Forms pour calculer les valeurs qu’un utilisateur saisit dans un formulaire et afficher les résultats. Le service Forms calcule les valeurs à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 81%

---

# Calcul de données de formulaire {#calculating-form-data}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le service Forms peut calculer les valeurs qu’un utilisateur saisit dans un formulaire et afficher les résultats. Pour calculer les données d’un formulaire, deux tâches sont nécessaires. Commencez par créer un script de conception de formulaire qui calcule les données du formulaire. Une conception de formulaire prend en charge trois types de scripts. Un type de script s’exécute sur le client, un autre sur le serveur et le troisième à la fois sur le serveur et sur le client. Le type de script décrit ici s’exécute sur le serveur. Les calculs côté serveur sont pris en charge pour les transformations HTML, PDF et Form Guide (obsolète).

Dans le cadre du processus de conception de formulaire, vous pouvez utiliser des calculs et des scripts pour offrir une expérience utilisateur plus riche. Il est possible d’ajouter des calculs et des scripts à la plupart des champs et objets de formulaire. Vous devez créer un script de conception de formulaire pour effectuer des opérations de calcul sur les données qu’un utilisateur saisit dans un formulaire interactif.

L’utilisateur saisit des valeurs dans le formulaire et clique ensuite sur le bouton Calculer pour afficher les résultats. Le processus suivant décrit un exemple d’application qui permet à un utilisateur de calculer des données :

* L’utilisateur accède à une page de HTML nommée StartLoan.html qui fait office de page de démarrage de l’application web. Cette page appelle une servlet Java nommée `GetLoanForm`.
* La servlet `GetLoanForm` renvoie un formulaire de prêt. Ce formulaire contient un script, des champs interactifs, un bouton de calcul et un bouton d’envoi.
* L’utilisateur saisit des valeurs dans les champs du formulaire et clique sur le bouton Calculer . Le formulaire est envoyé à la servlet Java `CalculateData` où le script est exécuté. Le formulaire est renvoyé à l’utilisateur avec les résultats du calcul affichés dans le formulaire.
* Lʼutilisateur continue à saisir et calculer des valeurs jusquʼà lʼobtention du résulat désiré. Une fois satisfait, il clique sur le bouton Envoyer pour traiter le formulaire. Le formulaire est envoyé à une autre servlet Java nommée `ProcessForm`, qui est chargée de la récupération des données envoyées. (Consultez la section [Gestion des formulaires envoyés](/help/forms/developing/rendering-forms.md#handling-submitted-forms)).


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
   <td><p>La servlet Java <code>GetLoanForm</code> est appelée à partir de la page de démarrage HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>La servlet Java <code>GetLoanForm</code> utilise lʼAPI Client du service Forms pour restituer le formulaire de prêt au navigateur web du client. La différence entre le rendu dʼun formulaire contenant un script configuré pour être exécuté sur le serveur et le rendu dʼun formulaire ne contenant pas de script est la suivante : vous devez spécifier lʼemplacement cible utilisé pour exécuter le script. Si aucun emplacement cible n’est spécifié, un script configuré pour être exécuté sur le serveur n’est pas exécuté. Prenons l’exemple de l’application présentée dans cette section. La servlet Java <code>CalculateData</code> est l’emplacement cible où le script est exécuté.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utilisateur saisit des données dans des champs interactifs et clique sur le bouton Calculer. Le formulaire est envoyé à la servlet Java <code>CalculateData</code>, où le script est exécuté. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le formulaire est rendu au navigateur web avec les résultats du calcul affichés dans le formulaire. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Lʼutilisateur clique sur le bouton Envoyer lorsque les valeurs lui conviennent. Le formulaire est envoyé à une autre servlet Java nommée <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

En général, un formulaire envoyé en tant que contenu PDF contient des scripts qui sont exécutés sur le client. Toutefois, les calculs côté serveur peuvent également être exécutés. Il n’est pas possible d’utiliser un bouton Envoyer pour calculer les scripts. Dans ce cas, les calculs ne sont pas exécutés car le service Forms considère que l’interaction est terminée.

Pour illustrer l’utilisation d’un script de conception de formulaire, cette section examine un formulaire interactif simple contenant un script configuré pour s’exécuter sur le serveur. Le diagramme suivant illustre une conception de formulaire contenant un script qui ajoute les valeurs saisies par un utilisateur dans les deux premiers champs et affiche le résultat dans le troisième champ.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Un champ nommé NumericField1 **B.** Un champ nommé NumericField2 **C.** Un champ nommé NumericField3

La syntaxe du script dans cette conception de formulaire est la suivante :

```javascript
     NumericField3 = NumericField2 + NumericField1
```

Dans cette conception de formulaire, le bouton Calculer est un bouton de commande et le script se trouve dans le de `Click` . Lorsqu’un utilisateur saisit des valeurs dans les deux premiers champs (NumericField1 et NumericField2) et clique sur le bouton Calculer, le formulaire est envoyé au service Forms, où le script est exécuté. Le service Forms restitue le formulaire à l’appareil client avec les résultats du calcul affichés dans le champ NumericField3.

>[!NOTE]
>
>Pour plus d’informations sur la création d’un script de conception de formulaire, réportez-vous à [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour calculer les données d’un formulaire, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Récupérez un formulaire contenant un script de calcul.
1. Réécrivez le flux de données de formulaire dans le navigateur web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms. Si vous utilisez l’API Java, créez un objet `FormsServiceClient`. Si vous utilisez l’API du service Web Forms, créez un objet `FormsServiceService`.

**Récupération d’un formulaire contenant un script de calcul**

Vous utilisez l’API client du service Forms pour créer une logique d’application qui gère un formulaire contenant un script configuré pour s’exécuter sur le serveur. Le processus est similaire à la gestion d’un formulaire envoyé. (Voir [Gestion des formulaires envoyés](/help/forms/developing/handling-submitted-forms.md).)

Vérifiez que l’état de traitement associé au formulaire envoyé est `1` `(Calculate)`, ce qui signifie que le service Forms effectue une opération de calcul sur les données de formulaire et que les résultats doivent être renvoyés à l’utilisateur. Dans ce cas, un script configuré pour s’exécuter sur le serveur est automatiquement exécuté.

**Réécrivez le flux de données de formulaire dans le navigateur web client.**

Après avoir vérifié que l’état de traitement associé à un formulaire envoyé est `1`, vous devez réécrire les résultats dans le navigateur web client. Lorsque le formulaire est affiché, la valeur calculée apparaît dans le(s) champ(s) approprié(s).

**Voir également**

[Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcul des données de formulaire à l’aide de l’API Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcul des données de formulaire à l’aide de l’API de service Web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcul des données de formulaire à l’aide de l’API Java {#calculate-form-data-using-the-java-api}

Calculer les données de formulaire à l’aide de l’API Forms (Java) :

1. Inclure des fichiers du projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupération d’un formulaire contenant un script de calcul

   * Pour récupérer des données de formulaire contenant un script de calcul, créez une `com.adobe.idp.Document` en utilisant son constructeur et en appelant la propriété `javax.servlet.http.HttpServletResponse` de `getInputStream` à partir du constructeur.
   * Appeler la variable `FormsServiceClient` de `processFormSubmission` et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant les données de formulaire.
      * Une valeur de chaîne qui indique les variables d’environnement, y compris tous les en-têtes HTTP pertinents. Indiquez le type de contenu à gérer en spécifiant une ou plusieurs valeurs pour la variable d’environnement `CONTENT_TYPE`. Par exemple, pour gérer les données XML et PDF, spécifiez la valeur de chaîne suivante pour ce paramètre : `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Une valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` stockant les options d’exécution.

     La méthode `processFormSubmission` renvoie un objet `FormsResult` contenant les résultats de l’envoi du formulaire.

   * Vérifiez que l’état de traitement associé à un formulaire envoyé est `1` en appelant le `FormsResult` de `getAction` . Si cette méthode renvoie la valeur `1`, le calcul a été effectué et les données peuvent être réécrites dans le navigateur web du client.

1. Réécrivez le flux de données de formulaire dans le navigateur web client.

   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données du formulaire au navigateur web du client.
   * Créez un `com.adobe.idp.Document` en appelant la méthode `FormsResult` object’s `getOutputContent` .
   * Créez un `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de `getInputStream` .
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la fonction `InputStream` de `read` et transmission du tableau d’octets en tant qu’argument.
   * Appeler la variable `javax.servlet.ServletOutputStream` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**


[Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calculer les données du formulaire en utilisant l’API Web Service {#calculate-form-data-using-the-web-service-api}

Calculez les données du formulaire en utilisant l’API Forms (Web Service) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Récupérer un formulaire contenant un script de calcul

   * Pour récupérer les données du formulaire qui ont été publiées dans une servlet Java, créez un objet `BLOB` en utilisant son constructeur.
   * Créez un `java.io.InputStream` en utilisant l’objet `javax.servlet.http.HttpServletResponse` de `getInputStream` .
   * Créez un objet `java.io.ByteArrayOutputStream` en utilisant son constructeur et en transmettant la longueur de l’objet `java.io.InputStream`.
   * Copiez le contenu de l’objet `java.io.InputStream` dans l’objet `java.io.ByteArrayOutputStream`.
   * Créez un tableau d’octets en appelant la méthode `java.io.ByteArrayOutputStream` de `toByteArray` .
   * Renseignez l’objet `BLOB` en appelant sa méthode `setBinaryData` et en transmettant le tableau d’octets comme argument.
   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur. Définissez la valeur du paramètre régional en appelant la variable `RenderOptionsSpec` de `setLocale` et transmission d’une valeur string qui spécifie la valeur locale.
   * Appeler la variable `FormsServiceClient` de `processFormSubmission` et transmettez les valeurs suivantes :

      * Objet `BLOB` contenant les données du formulaire.
      * Valeur de chaîne spécifiant les variables d’environnement, y compris tous les en-têtes HTTP pertinents. Par exemple, vous pouvez spécifier la valeur de chaîne suivante : `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`.
      * Valeur de chaîne spécifiant la valeur de l’en-tête `HTTP_USER_AGENT`, par exemple `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objet `RenderOptionsSpec` stockant les options d’exécution. Pour plus d’informations, .
      * Objet `BLOBHolder` vide qui est rempli par la méthode.
      * Un objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode.
      * Un objet `BLOBHolder` vide qui est renseigné par la méthode.
      * Un objet `BLOBHolder` vide qui est renseigné par la méthode.
      * Un objet `javax.xml.rpc.holders.ShortHolder` vide qui est renseigné par la méthode.
      * Un objet `MyArrayOf_xsd_anyTypeHolder` vide qui est renseigné par la méthode. Ce paramètre est utilisé pour stocker les pièces jointes envoyées avec le formulaire.
      * Objet `FormsResultHolder` vide qui est rempli par la méthode avec le formulaire envoyé.

     La méthode `processFormSubmission` remplit le paramètre `FormsResultHolder` avec les résultats de l’envoi du formulaire. La méthode `processFormSubmission` renvoie un objet `FormsResult` contenant les résultats de l’envoi du formulaire.

   * Vérifiez que l’état de traitement associé à un formulaire envoyé est `1` en appelant le `FormsResult` de `getAction` . Si cette méthode renvoie la valeur `1`, le calcul a été effectué et les données peuvent être réécrites dans le navigateur web du client.

1. Réécrivez le flux de données de formulaire dans le navigateur web client.

   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données du formulaire au navigateur web du client.
   * Créez un `BLOB` qui contient des données de formulaire en appelant la méthode `FormsResult` de `getOutputContent` .
   * Créez un tableau d’octets et renseignez-le en appelant la variable `BLOB` de `getBinaryData` . Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appeler la variable `javax.servlet.http.HttpServletResponse` de `write` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Consultez également la section**
[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
