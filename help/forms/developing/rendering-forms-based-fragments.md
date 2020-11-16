---
title: Rendu de Forms en fonction de fragments
seo-title: Rendu de Forms en fonction de fragments
description: 'null'
seo-description: 'null'
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 9%

---


# Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments}

## Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments-inner}

Le service Forms peut générer des formulaires basés sur des fragments que vous créez à l’aide de Designer. Un *fragment* est une partie réutilisable d’un formulaire et est enregistré en tant que fichier XDP distinct qui peut être inséré dans plusieurs conceptions de formulaire. Un fragment peut très bien inclure un bloc d’adresse ou un paragraphe juridique, par exemple.

L’utilisation de fragments simplifie et accélère la création et la gestion d’un grand nombre de formulaires. Lors de la création d’un formulaire, vous insérez une référence au fragment requis et le fragment s’affiche dans le formulaire. La référence au fragment contient un sous-formulaire pointant vers le fichier XDP physique. Pour plus d’informations sur la création de conceptions de formulaire basées sur des fragments, voir [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

Un fragment peut inclure plusieurs sous-formulaires encapsulés dans un jeu de sous-formulaires de choix. Les jeux de sous-formulaires choisis contrôlent l’affichage des sous-formulaires en fonction du flux de données provenant d’une connexion aux données. Vous vous servez d’instructions conditionnelles pour déterminer le sous-formulaire du jeu devant s’afficher dans le formulaire obtenu. Par exemple, chaque sous-formulaire d’un jeu peut inclure des informations relatives à un emplacement géographique particulier et le sous-formulaire affiché peut être déterminé en fonction de l’emplacement de l’utilisateur.

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. Les fragments de ce type comprennent un seul objet de script figurant comme enfant de variables dans la palette Hiérarchie. Ils ne peuvent pas être créés à partir de scripts correspondant à des propriétés d’autres objets, tels que les scripts d’événements (validate, calculate ou initialize, par exemple).

L’utilisation de fragments présente les avantages suivants :

* **Réutilisation** du contenu : Vous pouvez utiliser des fragments pour réutiliser du contenu dans plusieurs conceptions de formulaire. Lorsque vous devez utiliser un même contenu dans plusieurs formulaires, il est plus rapide et plus simple d’utiliser un fragment que de copier ou de recréer le contenu. L’emploi de fragments permet par ailleurs de garantir l’homogénéité du contenu et de l’aspect de parties de formulaire reprises dans les différents formulaires de référencement.
* **Mises à jour** globales : Vous pouvez utiliser des fragments pour apporter des modifications globales à plusieurs formulaires une seule fois, dans un seul fichier. Vous pouvez modifier le contenu, les objets de script, les liaisons de données, la disposition ou les styles d’un fragment, et tous les formulaires XDP référençant le fragment reflètent les modifications.
* Par exemple, un élément commun à de nombreux formulaires peut être un bloc d’adresse qui inclut un objet de liste déroulant pour le pays. Si vous devez mettre à jour les valeurs de l’objet de liste déroulante, vous devez ouvrir de nombreux formulaires pour effectuer les modifications. Si vous incluez le bloc d’adresse dans un fragment, vous n’avez qu’à ouvrir un fichier de fragment pour effectuer les modifications.
* Pour mettre à jour un fragment dans un formulaire PDF, vous devez réenregistrer le formulaire dans Designer.
* **Création** de formulaire partagée : Vous pouvez utiliser des fragments pour partager la création de formulaires entre plusieurs ressources. Les développeurs de formulaires familiarisés avec l’utilisation de scripts ou d’autres fonctions avancées de Designer peuvent développer et partager des fragments tirant avantage des fonctions de script et des propriétés dynamiques. Les concepteurs de formulaires peuvent ensuite se servir de ces fragments pour définir la disposition de leurs conceptions de formulaire et s’assurer que toutes les parties de formulaires créés par plusieurs personnes revêtent un aspect, une présentation et des fonctionnalités homogènes.

### Assemblage d’une conception de formulaire assemblée à l’aide de fragments {#assembling-a-form-design-assembled-using-fragments}

Vous pouvez assembler une conception de formulaire à transmettre au service Forms en fonction de plusieurs fragments. Pour assembler plusieurs fragments, utilisez le service Assembler. Pour voir un exemple d’utilisation du service Assemble pour créer une conception de formulaire utilisée par un autre service Forms (le service Output), voir [Création de Documents PDF à l’aide de fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Au lieu d’utiliser le service Output, vous pouvez exécuter le même processus à l’aide du service Forms.

Lors de l’utilisation du service Assembler, vous transmettez une conception de formulaire qui a été assemblée à l’aide de fragments. La conception de formulaire créée ne fait pas référence à d’autres fragments. En revanche, cette rubrique traite de la transmission d’une conception de formulaire qui référence d’autres fragments au service Forms. Cependant, la conception de formulaire n’a pas été assemblée par Assembler. Il a été créé dans Designer.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Web qui effectue le rendu des formulaires à partir de fragments, voir [Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Résumé des étapes {#summary-of-steps}

Pour générer un formulaire à partir de fragments, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Client Forms.
1. Spécifiez des valeurs URI.
1. Générer le formulaire.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API Client Forms**

Avant de pouvoir exécuter par programmation une opération d’API Client de service Forms, vous devez créer un client de service Forms.

**Spécification des valeurs URI**

Pour générer un formulaire basé sur des fragments, vous devez vous assurer que le service Forms peut localiser le formulaire et les fragments (fichiers XDP) auxquels la conception de formulaire fait référence. Supposons, par exemple, que le formulaire soit nommé PO.xdp et que ce formulaire utilise deux fragments nommés FooterUS.xdp et FooterCanada.xdp. Dans ce cas, le service Forms doit être en mesure de localiser les trois fichiers XDP.

Vous pouvez organiser un formulaire et ses fragments en plaçant le formulaire à un emplacement et les fragments à un autre emplacement, ou vous pouvez placer tous les fichiers XDP au même emplacement. Aux fins de cette section, supposons que tous les fichiers XDP se trouvent dans le référentiel AEM Forms. Pour plus d’informations sur le placement de fichiers XDP dans le référentiel AEM Forms, voir [Ecriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).

Lors du rendu d’un formulaire basé sur des fragments, vous devez référencer uniquement le formulaire lui-même et non les fragments. Par exemple, vous devez référencer PO.xdp et non FooterUS.xdp ou FooterCanada.xdp. Assurez-vous de placer les fragments à l’emplacement où le service Forms peut les localiser.

**Rendu du formulaire**

Un formulaire basé sur des fragments peut être rendu de la même manière que les formulaires non fragmentés. En d’autres termes, vous pouvez générer le formulaire au format PDF, HTML ou Guides de formulaire (obsolète). L’exemple de cette section présente un formulaire basé sur des fragments sous la forme d’un formulaire PDF interactif. (Voir [Rendu de PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)interactifs.)

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms effectue le rendu d’un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible pour l’utilisateur.

**Voir également**

[Rendu de formulaires basés sur des fragments à l’aide de l’API Java](#render-forms-based-on-fragments-using-the-java-api)

[Rendu de formulaires basés sur des fragments à l’aide de l’API du service Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendu de formulaires basés sur des fragments à l’aide de l’API Java {#render-forms-based-on-fragments-using-the-java-api}

Générer un formulaire basé sur des fragments à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Spécification des valeurs URI

   * Créez un `URLSpec` objet qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `URLSpec` de l’objet `setApplicationWebRoot` et transmettez une valeur de chaîne qui représente la racine Web de l’application.
   * Appelez la méthode `URLSpec` de l’objet `setContentRootURI` et transmettez une valeur de chaîne qui spécifie la valeur URI racine du contenu. Assurez-vous que la conception de formulaire et les fragments se trouvent dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appelez la `URLSpec` méthode de l’ `setTargetURL` objet et transmettez une valeur de chaîne qui spécifie la valeur de l’URL de cible à l’endroit où les données du formulaire sont publiées. Si vous définissez l’URL de la cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer des calculs.

1. Rendu du formulaire

   Appelez la méthode `FormsServiceClient` de l’ `renderPDFForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI requises par le service Forms pour générer un formulaire basé sur des fragments.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets pour le remplir avec le flux de données du formulaire en appelant la `InputStream` `read`méthode de l’objet et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu de Forms en fonction de fragments](#rendering-forms-based-on-fragments)

[Début rapide (mode SOAP) : Rendu d’un formulaire basé sur des fragments à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendu de formulaires basés sur des fragments à l’aide de l’API du service Web {#render-forms-based-on-fragments-using-the-web-service-api}

Générer un formulaire à partir de fragments à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API Client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Spécification des valeurs URI

   * Créez un `URLSpec` objet qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `URLSpec` de l’objet `setApplicationWebRoot` et transmettez une valeur de chaîne qui représente la racine Web de l’application.
   * Appelez la méthode `URLSpec` de l’objet `setContentRootURI` et transmettez une valeur de chaîne qui spécifie la valeur URI racine du contenu. Assurez-vous que la conception de formulaire se trouve dans l’URI racine de contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appelez la `URLSpec` méthode de l’ `setTargetURL` objet et transmettez une valeur de chaîne qui spécifie la valeur de l’URL de cible à l’endroit où les données du formulaire sont publiées. Si vous définissez l’URL de la cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer des calculs.

1. Rendu du formulaire

   Appelez la méthode `FormsService` de l’ `renderPDFForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Notez que l’option PDF balisé ne peut pas être définie si le document d’entrée est un document PDF. Si le fichier d’entrée est un fichier XDP, l’option PDF balisé peut être définie.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` rempli par la méthode. Ce paramètre est utilisé pour stocker le formulaire rendu.
   * Objet vide `javax.xml.rpc.holders.LongHolder` rempli par la méthode. Cet argument stocke le nombre de pages dans le formulaire.
   * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode. Cet argument stocke la valeur du paramètre régional.
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

**Voir également**

[Rendu de Forms en fonction de fragments](#rendering-forms-based-on-fragments)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
