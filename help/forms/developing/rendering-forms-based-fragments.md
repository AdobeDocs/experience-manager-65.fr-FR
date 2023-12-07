---
title: Générer des formulaires reposant sur des fragments
description: Utilisez le service Forms pour restituer des formulaires reposant sur des fragments créés à l’aide de Designer.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 90%

---

# Générer des formulaires reposant sur des fragments {#rendering-forms-based-on-fragments}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## Générer des formulaires reposant sur des fragments {#rendering-forms-based-on-fragments-inner}

Le service Forms peut restituer des formulaires reposant sur des fragments créés à l’aide de Designer. Un *fragment* est une partie réutilisable d’un formulaire et est enregistrée en tant que fichier XDP distinct pouvant être inséré dans plusieurs conceptions de formulaire. Un fragment peut très bien inclure un bloc d’adresse ou un paragraphe juridique, par exemple.

L’utilisation de fragments simplifie et accélère la création et la gestion d’un grand nombre de formulaires. Lors de la création d’un formulaire, vous insérez une référence au fragment requis qui s’affiche dans le formulaire. La référence au fragment contient un sous-formulaire pointant vers le fichier XDP physique. Pour plus d’informations sur la création de conceptions de formulaires reposant sur des fragments, consultez la section [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

Un fragment peut inclure plusieurs sous-formulaires qui sont placés dans un jeu de sous-formulaires de choix. Les jeux de sous-formulaires de choix contrôlent l’affichage des sous-formulaires en fonction du flux de données d’une connexion aux données. Vous vous servez d’instructions conditionnelles pour déterminer le sous-formulaire du jeu devant s’afficher dans le formulaire obtenu. Par exemple, chaque sous-formulaire faisant partie d’un jeu peut comprendre des informations relatives à un emplacement géographique particulier et le sous-formulaire affiché peut être déterminé d’après l’emplacement de lʼutilisateur.

Un *fragment de script* contient des valeurs ou des fonctions JavaScript réutilisables stockées séparément des objets, tels qu’un analyseur de dates ou un appel de services web. Ces fragments incluent un seul objet de script qui apparaît comme enfant de variables dans la palette Hiérarchie. Les fragments ne peuvent pas être créés à partir de scripts qui sont des propriétés d’autres objets, tels que des scripts d’événement tels que validate, calculate ou initialize.

L’utilisation de fragments présente les avantages suivants :

* **Réutilisation du contenu** : les fragments vous permettent de réutiliser un contenu dans plusieurs conceptions de formulaire. Lorsque vous devez utiliser le même contenu dans plusieurs formulaires, il est plus rapide et plus simple d’utiliser un fragment que de copier ou de recréer le contenu. L’emploi de fragments permet par ailleurs de garantir l’homogénéité du contenu et de l’aspect de parties de formulaire reprises dans les différents formulaires de référencement.
* **Mises à jour globales** : l’utilisation de fragments vous permet d’effectuer des changements globaux dans plusieurs formulaires en une opération et en modifiant un seul fichier. Vous pouvez modifier le contenu, les objets de script, les liaisons de données, la disposition ou les styles d’un fragment : tous les formulaires XDP référençant ce fragment reflèteront ces changements.
* Par exemple, vous pouvez retrouver dans de nombreux formulaires un élément commun tel qu’un bloc d’adresse comprenant un objet de liste déroulante de pays. Si vous mettez à jour les valeurs de cet objet de liste déroulante, vous devez ouvrir un grand nombre de formulaires afin d’y apporter les modifications voulues. En revanche, si vous placez le bloc d’adresse dans un fragment, il vous suffit d’ouvrir un fichier de fragment pour y apporter les modifications voulues.
* Pour mettre à jour un fragment dans un formulaire PDF, vous devez réenregistrer le formulaire dans Designer.
* **Création de formulaires partagée** : lʼutilisation de fragments permet de partager la création de formulaires entre plusieurs ressources. Les développeurs de formulaires maîtrisant les fonctions de script ou d’autres fonctions avancées de Designer peuvent développer et partager des fragments tirant parti des fonctions de script et des propriétés dynamiques. Les concepteurs de formulaires peuvent utiliser ces fragments pour mettre en page des conceptions de formulaire et s’assurer que toutes les parties d’un formulaire ont une apparence et une fonctionnalité cohérentes sur plusieurs formulaires conçus par plusieurs personnes.

### Assembler une conception de formulaire à l’aide de fragments {#assembling-a-form-design-assembled-using-fragments}

Vous pouvez assembler une conception de formulaire à transmettre au service Forms en fonction de plusieurs fragments. Pour assembler plusieurs fragments, utilisez le service Assembler. Pour découvrir un exemple d’utilisation du service Assembler consistant à créer une conception de formulaire utilisée par un autre service Forms (le service Output), consultez la section [Créez des documents PDF en utilisant des fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Au lieu d’utiliser le service Output, vous pouvez réaliser le même workflow à l’aide du service Forms.

Lors de l’utilisation du service Assembler, vous transmettez une conception de formulaire assemblée à l’aide de fragments. La conception de formulaire créée ne fait pas référence à d’autres fragments. En revanche, cette rubrique aborde la transmission d’une conception de formulaire qui fait référence à d’autres fragments au service Forms. Toutefois, la conception de formulaire n’a pas été assemblée par Assembler. Elle a été créée dans Designer.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application web qui restitue des formulaires reposant sur des fragments, consultez la section [Créer des applications web qui restituent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md).

### Résumé des étapes {#summary-of-steps}

Pour restituer un formulaire reposant sur des fragments, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Spécifier les valeurs URI
1. Restituer le formulaire
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet de lʼAPI client de Forms**

Avant d’effectuer par programmation une opération de l’API du client de service Forms, vous devez créer un client de service Forms.

**Spécifier les valeurs URI**

Pour restituer correctement un formulaire reposant sur des fragments, veillez à ce que le service Forms puisse localiser le formulaire et les fragments (les fichiers XDP) auxquels la conception de formulaire fait référence. Prenons lʼexemple suivant : le formulaire est nommé PO.xdp et utilise deux fragments nommés FooterUS.xdp et FooterCanada.xdp. Dans ce cas, le service Forms doit pouvoir localiser les trois fichiers XDP.

Vous pouvez organiser un formulaire et ses fragments en plaçant le formulaire à un emplacement et les fragments à un autre, ou vous pouvez placer tous les fichiers XDP au même emplacement. Pour les besoins de cette section, supposons que tous les fichiers XDP se trouvent dans le référentiel AEM Forms. Pour plus d’informations sur le placement des fichiers XDP dans le référentiel AEM Forms, consultez la section [Enregistrer les ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).

Lors de la restitution dʼun formulaire reposant sur des fragments, vous ne devez référencer que le formulaire lui-même et non les fragments. Par exemple, vous devez référencer PO.xdp et non FooterUS.xdp ou FooterCanada.xdp. Veillez à placer les fragments à un emplacement localisable par le service Forms.

**Restituer le formulaire**

Un formulaire reposant sur des fragments peut être restitué de la même manière que les formulaires non fragmentés. Cela signifie que vous pouvez restituer le formulaire au format PDF, HTML ou guides de formulaire (déprécié). L’exemple de cette section restitue un formulaire reposant sur des fragments sous forme de formulaire PDF interactif. (Consultez la section [Restituer des formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)).

**Enregistrer le flux de données de formulaire dans le navigateur web du client**

Lorsque le service Forms effectue la restitution d’un formulaire, il renvoie un flux de données de formulaire que vous devez enregistrer dans le navigateur web du client. Lorsqu’il est écrit dans le navigateur web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Restituer des formulaires reposant sur des fragments à l’aide de l’API Java](#render-forms-based-on-fragments-using-the-java-api)

[Restituer des formulaires reposant sur des fragments à l’aide de l’API de service web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Restituer des formulaires reposant sur des fragments à l’aide de l’API Java {#render-forms-based-on-fragments-using-the-java-api}

Restituer un formulaire reposant sur des fragments à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre projet Java Classpath.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Spécifier les valeurs URI

   * Créez un objet `URLSpec` stockant des valeurs URI en utilisant son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur de chaîne qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de la racine du contenu URI. Assurez-vous que la conception de formulaire et les fragments se trouvent dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appeler la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URL cible à l’endroit où les données de formulaire sont publiées. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer les calculs.

1. Restituer le formulaire

   Appelez la méthode `renderPDFForm` de lʼobjet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez un objet `com.adobe.idp.Document` vide.
   * Un objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Un objet `URLSpec` qui contient les valeurs URI requises par le service Forms pour restituer un formulaire reposant sur des fragments.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de lʼobjet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de lʼobjet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de lʼobjet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Générer des formulaires reposant sur des fragments](#rendering-forms-based-on-fragments)

[Démarrage rapide (mode SOAP) : générer un formulaire basé sur des fragments à l’aide de l’API Java.](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Restituer des formulaires reposant sur des fragments à l’aide de l’API de service web {#render-forms-based-on-fragments-using-the-web-service-api}

Générer un formulaire basé sur des fragments à l’aide de l’API Forms (Web Service) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Spécifier les valeurs URI

   * Créez un objet `URLSpec` stockant des valeurs URI en utilisant son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur de chaîne qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de la racine du contenu URI. Assurez-vous que la conception de formulaire se trouve dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appeler la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur de chaîne qui spécifie la valeur de l’URL cible à l’endroit où les données de formulaire sont publiées. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer les calculs.

1. Restituer le formulaire

   Appelez la méthode `renderPDFForm` de lʼobjet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin dʼaccès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`.
   * Un objet `PDFFormRenderSpec` stockant les options d’exécution. L’option de PDF balisé ne peut pas être définie si le document d’entrée est un document de PDF. Si le fichier d’entrée est un fichier XDP, l’option de PDF balisé peut être définie.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` stockant les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Ce paramètre est utilisé pour stocker le formulaire généré.
   * Objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. Cet argument stocke le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. Cet argument stocke la valeur des paramètres régionaux.
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide contenant les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` servant à écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Générer des formulaires reposant sur des fragments](#rendering-forms-based-on-fragments)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
