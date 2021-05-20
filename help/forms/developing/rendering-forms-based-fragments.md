---
title: Rendu de Forms basé sur des fragments
seo-title: Rendu de Forms basé sur des fragments
description: Utilisez le service Forms pour effectuer le rendu de formulaires reposant sur des fragments créés à l’aide de Designer.
seo-description: Utilisez le service Forms pour effectuer le rendu de formulaires reposant sur des fragments créés à l’aide de Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2229'
ht-degree: 9%

---

# Rendu de Forms basé sur des fragments {#rendering-forms-based-on-fragments}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

## Rendu de Forms basé sur des fragments {#rendering-forms-based-on-fragments-inner}

Le service Forms peut générer des formulaires basés sur des fragments que vous créez à l’aide de Designer. Un *fragment* est une partie réutilisable d’un formulaire et est enregistré en tant que fichier XDP distinct qui peut être inséré dans plusieurs conceptions de formulaire. Un fragment peut très bien inclure un bloc d’adresse ou un paragraphe juridique, par exemple.

L’utilisation de fragments simplifie et accélère la création et la gestion d’un grand nombre de formulaires. Lors de la création d’un formulaire, vous insérez une référence au fragment requis qui s’affiche dans le formulaire. La référence au fragment contient un sous-formulaire pointant vers le fichier XDP physique. Pour plus d’informations sur la création de conceptions de formulaire à partir de fragments, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un fragment peut inclure plusieurs sous-formulaires qui sont placés dans un jeu de sous-formulaires de choix. Les jeux de sous-formulaires de choix contrôlent l’affichage des sous-formulaires en fonction du flux de données d’une connexion aux données. Vous vous servez d’instructions conditionnelles pour déterminer le sous-formulaire du jeu devant s’afficher dans le formulaire obtenu. Par exemple, chaque sous-formulaire d’un jeu peut inclure des informations sur un emplacement géographique particulier et le sous-formulaire affiché peut être déterminé en fonction de l’emplacement de l’utilisateur.

Un *fragment de script* contient des fonctions ou des valeurs JavaScript réutilisables qui sont stockées séparément de tout objet particulier, tel qu’un analyseur de dates ou un appel de service Web. Les fragments de ce type comprennent un seul objet de script figurant comme enfant de variables dans la palette Hiérarchie. Ils ne peuvent pas être créés à partir de scripts correspondant à des propriétés d’autres objets, tels que les scripts d’événements (validate, calculate ou initialize, par exemple).

L’utilisation de fragments présente les avantages suivants :

* **Réutilisation** du contenu : Vous pouvez utiliser des fragments pour réutiliser du contenu dans plusieurs conceptions de formulaire. Lorsque vous devez utiliser un même contenu dans plusieurs formulaires, il est plus rapide et plus simple d’utiliser un fragment que de copier ou recréer le contenu. L’emploi de fragments permet par ailleurs de garantir l’homogénéité du contenu et de l’aspect de parties de formulaire reprises dans les différents formulaires de référencement.
* **Mises à jour globales** : Vous ne pouvez utiliser des fragments pour apporter des modifications globales à plusieurs formulaires en une seule fois, dans un seul fichier. Vous pouvez modifier le contenu, les objets de script, les liaisons de données, la mise en page ou les styles d’un fragment, et tous les formulaires XDP qui font référence au fragment seront pris en compte dans les modifications.
* Par exemple, un élément courant dans de nombreux formulaires peut être un bloc d’adresse qui inclut un objet de liste déroulante pour le pays. Si vous devez mettre à jour les valeurs de l’objet de liste déroulante, vous devez ouvrir de nombreux formulaires pour effectuer les modifications. Si vous incluez le bloc d’adresse dans un fragment, il vous suffit d’ouvrir un fichier de fragment pour effectuer les modifications.
* Pour mettre à jour un fragment dans un formulaire PDF, vous devez réenregistrer le formulaire dans Designer.
* **Création** de formulaires partagés : Vous pouvez utiliser des fragments pour partager la création de formulaires entre plusieurs ressources. Les développeurs de formulaires familiarisés avec l’utilisation de scripts ou d’autres fonctions avancées de Designer peuvent développer et partager des fragments tirant avantage des fonctions de script et des propriétés dynamiques. Les concepteurs de formulaires peuvent ensuite se servir de ces fragments pour définir la disposition de leurs conceptions de formulaire et s’assurer que toutes les parties de formulaires créés par plusieurs personnes revêtent un aspect, une présentation et des fonctionnalités homogènes.

### Assemblage d’une conception de formulaire à l’aide de fragments {#assembling-a-form-design-assembled-using-fragments}

Vous pouvez assembler une conception de formulaire à transmettre au service Forms en fonction de plusieurs fragments. Pour assembler plusieurs fragments, utilisez le service Assembler. Pour voir un exemple d’utilisation du service Assemble pour créer une conception de formulaire utilisée par un autre service Forms (le service Output), voir [Création de documents PDF à l’aide de fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Au lieu d’utiliser le service Output, vous pouvez exécuter le même workflow à l’aide du service Forms.

Lors de l’utilisation du service Assembler, vous transmettez une conception de formulaire qui a été assemblée à l’aide de fragments. La conception de formulaire qui a été créée ne fait pas référence à d’autres fragments. En revanche, cette rubrique aborde la transmission d’une conception de formulaire qui référence d’autres fragments au service Forms. Toutefois, la conception de formulaire n’a pas été assemblée par Assembler. Il a été créé dans Designer.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application web qui effectue le rendu des formulaires à partir de fragments, voir [Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Résumé des étapes {#summary-of-steps}

Pour générer un formulaire à partir de fragments, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet API client Forms.
1. Spécifiez les valeurs URI.
1. Effectuez le rendu du formulaire.
1. Ecrivez le flux de données de formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API client Forms**

Avant d’effectuer par programmation une opération d’API client de service Forms, vous devez créer un client de service Forms.

**Spécification de valeurs URI**

Pour réussir le rendu d’un formulaire basé sur des fragments, vous devez vous assurer que le service Forms peut localiser le formulaire et les fragments (fichiers XDP) auxquels la conception de formulaire fait référence. Supposons, par exemple, que le formulaire soit nommé PO.xdp et que ce formulaire utilise deux fragments nommés FooterUS.xdp et FooterCanada.xdp. Dans ce cas, le service Forms doit pouvoir localiser les trois fichiers XDP.

Vous pouvez organiser un formulaire et ses fragments en plaçant le formulaire à un emplacement et les fragments à un autre emplacement, ou vous pouvez placer tous les fichiers XDP au même emplacement. Pour les besoins de cette section, supposons que tous les fichiers XDP se trouvent dans le référentiel AEM Forms. Pour plus d’informations sur le placement de fichiers XDP dans le référentiel AEM Forms, voir [Écriture de ressources](/help/forms/developing/aem-forms-repository.md#writing-resources).

Lors du rendu d’un formulaire basé sur des fragments, vous devez référencer uniquement le formulaire lui-même et non les fragments. Par exemple, vous devez référencer PO.xdp et non FooterUS.xdp ou FooterCanada.xdp. Veillez à placer les fragments à un emplacement où le service Forms peut les localiser.

**Rendu du formulaire**

Un formulaire basé sur des fragments peut être rendu de la même manière que les formulaires non fragmentés. En d’autres termes, vous pouvez effectuer le rendu du formulaire au format PDF, HTML ou Guides de formulaire (obsolète). L’exemple de cette section présente un formulaire basé sur des fragments sous la forme d’un formulaire PDF interactif. (Voir [Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Écrire le flux de données de formulaire dans le navigateur Web client**

Lorsque le service Forms effectue le rendu d’un formulaire, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire est visible par l’utilisateur.

**Voir également**

[Rendu de formulaires reposant sur des fragments à l’aide de l’API Java](#render-forms-based-on-fragments-using-the-java-api)

[Rendu de formulaires basés sur des fragments à l’aide de l’API de service Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendu des formulaires basés sur des fragments à l’aide de l’API Java {#render-forms-based-on-fragments-using-the-java-api}

Rendre un formulaire basé sur des fragments à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Spécification de valeurs URI

   * Créez un objet `URLSpec` qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur string qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur string qui spécifie la valeur de l’URI racine du contenu. Assurez-vous que la conception de formulaire et les fragments se trouvent dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appelez la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur string qui spécifie la valeur de l’URL cible à l’endroit où les données de formulaire sont publiées. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer les calculs.

1. Rendu du formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms pour générer un formulaire basé sur des fragments.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l’objet `getOutputContent`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets pour le remplir avec le flux de données de formulaire en appelant la méthode `InputStream` de l’objet `read`et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Rendu de Forms basé sur des fragments](#rendering-forms-based-on-fragments)

[Démarrage rapide (mode SOAP) : Rendu d’un formulaire basé sur des fragments à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendu de formulaires basés sur des fragments à l’aide de l’API de service Web {#render-forms-based-on-fragments-using-the-web-service-api}

Rendre un formulaire basé sur des fragments à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de classe.

1. Création d’un objet API client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Spécification de valeurs URI

   * Créez un objet `URLSpec` qui stocke les valeurs URI à l’aide de son constructeur.
   * Appelez la méthode `setApplicationWebRoot` de l’objet `URLSpec` et transmettez une valeur string qui représente la racine web de l’application.
   * Appelez la méthode `setContentRootURI` de l’objet `URLSpec` et transmettez une valeur string qui spécifie la valeur de l’URI racine du contenu. Assurez-vous que la conception de formulaire se trouve dans l’URI racine du contenu. Dans le cas contraire, le service Forms renvoie une exception. Pour référencer le référentiel, spécifiez `repository://`.
   * Appelez la méthode `setTargetURL` de l’objet `URLSpec` et transmettez une valeur string qui spécifie la valeur de l’URL cible à l’endroit où les données de formulaire sont publiées. Si vous définissez l’URL cible dans la conception de formulaire, vous pouvez transmettre une chaîne vide. Vous pouvez également spécifier l’URL vers laquelle un formulaire est envoyé pour effectuer les calculs.

1. Rendu du formulaire

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Notez que l’option PDF balisé ne peut pas être définie si le document d’entrée est un document PDF. Si le fichier d’entrée est un fichier XDP, l’option PDF balisé peut être définie.
   * Objet `URLSpec` contenant les valeurs URI requises par le service Forms.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode . Ce paramètre est utilisé pour stocker le formulaire rendu.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode . Cet argument stocke le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode . Cet argument stocke la valeur du paramètre régional.
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Rendu de Forms basé sur des fragments](#rendering-forms-based-on-fragments)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
