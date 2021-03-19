---
title: Rendu de HTML Forms avec des barres d’outils personnalisées
seo-title: Rendu de HTML Forms avec des barres d’outils personnalisées
description: Utilisez le service Forms pour personnaliser une barre d’outils générée avec un formulaire HTML. Vous pouvez générer un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java et d’une API de service Web.
seo-description: Utilisez le service Forms pour personnaliser une barre d’outils générée avec un formulaire HTML. Vous pouvez générer un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java et d’une API de service Web.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2385'
ht-degree: 1%

---


# Rendu de HTML Forms avec des barres d’outils personnalisées {#rendering-html-forms-with-customtoolbars}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

## Rendu de HTML Forms avec des barres d’outils personnalisées {#rendering-html-forms-with-custom-toolbars}

Le service Forms vous permet de personnaliser une barre d’outils générée avec un formulaire HTML. Une barre d’outils peut être personnalisée pour modifier son apparence en remplaçant les styles CSS par défaut et pour ajouter un comportement dynamique en remplaçant les scripts Java. Une barre d’outils est personnalisée à l’aide d’un fichier XML nommé fscmenu.xml. Par défaut, le service Forms récupère ce fichier à partir d’un emplacement URI spécifié en interne.

>[!NOTE]
>
>Cet emplacement URI se trouve dans le fichier adobe-forms-core.jar, qui se trouve dans le fichier adobe-forms-dsc.jar. Le fichier adobe-forms-dsc.jar se trouve dans C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Vous pouvez utiliser un outil d’extraction de fichiers, tel que Win RAR, pour ouvrir adobe.

Vous pouvez copier le fichier fscmenu.xml à partir de cet emplacement, le modifier pour répondre à vos besoins, puis le placer dans un emplacement URI personnalisé. Ensuite, à l’aide de l’API Service Forms, définissez les options d’exécution qui génèrent le service Forms en utilisant votre fichier fscmenu.xml à partir de l’emplacement spécifié. Ces actions entraînent le rendu par le service Forms d’un formulaire HTML doté d’une barre d’outils personnalisée.

Outre le fichier fscmenu.xml, vous devez également obtenir les fichiers suivants :

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS est le script Java associé à chaque noeud. Il est nécessaire d’en fournir un pour le noeud `div#fscmenu` et éventuellement pour les noeuds `ul#fscmenuItem`. Les fichiers JS implémentent la fonctionnalité de base de la barre d’outils et les fichiers par défaut fonctionnent.

fscCSS est une feuille de style associée à un noeud particulier. Les styles des fichiers CSS définissent l’aspect de la barre d’outils. ** fscVCSS est une feuille de style pour une barre d’outils verticale qui s’affiche à gauche du formulaire HTML rendu. ** fscIECSS est une feuille de style utilisée pour les formulaires HTML générés dans Internet Explorer.

Assurez-vous que tous les fichiers ci-dessus sont référencés dans le fichier fscmenu.xml. En d’autres termes, dans le fichier fscmenu.xml, spécifiez des emplacements URI pour pointer vers ces fichiers afin que le service Forms puisse les localiser. Par défaut, ces fichiers sont disponibles aux emplacements URI commençant par les mots-clés internes `FSWebRoot` ou `ApplicationWebRoot`.

Pour personnaliser la barre d’outils, remplacez les mots-clés par le mot-clé externe `FSToolBarURI`. Ce mot-clé représente l’URI transmis au service Forms au moment de l’exécution (cette approche est présentée plus loin dans cette section).

Vous pouvez également spécifier les emplacements absolus de ces fichiers JS et CSS, tels que https://www.mycompany.com/scripts/misc/fscmenu.js. Dans ce cas, vous n’avez pas besoin d’utiliser le mot-clé `FSToolBarURI`.

>[!NOTE]
>
>Il n’est pas recommandé de mélanger les méthodes de référencement de ces fichiers. En d’autres termes, tous les URI doivent être référencés à l’aide du mot-clé `FSToolBarURI` ou d’un emplacement absolu.

Vous pouvez obtenir les fichiers JS et CSS en ouvrant le fichier adobe-forms-&lt;serveur d’applications>.ear. Dans ce fichier, ouvrez le fichier adobe-forms-res.war. Tous ces fichiers se trouvent dans le fichier WAR. Le fichier adobe-forms-&lt;serveur d’applications>.ear se trouve dans le dossier d’installation AEM forms (C:\ is the installation directory). Vous pouvez ouvrir le fichier adobe-forms-&lt;serveur d’applications>.ear à l’aide d’un outil d’extraction de fichiers tel que WinRAR.

La syntaxe XML suivante illustre un exemple de fichier fscmenu.xml.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Le texte en gras représente les URI des fichiers CSS et JS qui doivent être référencés.

Les éléments suivants décrivent comment personnaliser une barre d’outils :

* Modifiez les valeurs des attributs `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (dans le fichier fscmenu.xml) afin de refléter les emplacements personnalisés des fichiers référencés à l’aide de l’une des méthodes décrites dans cette section (par exemple, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Tous les fichiers CSS et JS doivent être spécifiés. Si aucun des fichiers n’est modifié, indiquez le fichier par défaut à l’emplacement personnalisé. Vous pouvez obtenir les fichiers par défaut en ouvrant divers fichiers comme décrit dans cette section.
* Il est possible de fournir une référence absolue (par exemple, https://www.example.com/scripts/custom-vertical-fscmenu.css) à tout fichier.
* Les fichiers JS et CSS requis par le noeud `div#fscmenu` sont essentiels à la fonctionnalité de barre d’outils. Certains noeuds `ul#fscmenuItem` peuvent ou non avoir des fichiers JS ou CSS pris en charge.

**Modification de la valeur locale**

Dans le cadre de la personnalisation d’une barre d’outils, vous pouvez modifier la valeur des paramètres régionaux de la barre d’outils. Autrement dit, vous pouvez l&#39;afficher dans une autre langue. L’illustration suivante présente une barre d’outils personnalisée qui s’affiche en français.

>[!NOTE]
>
>Il n’est pas possible de créer une barre d’outils personnalisée dans plusieurs langues. Les barres d’outils ne peuvent pas utiliser des fichiers XML différents en fonction des paramètres régionaux.

Pour modifier la valeur des paramètres régionaux d’une barre d’outils, assurez-vous que le fichier fscmenu.xml contient la langue à afficher. La syntaxe XML suivante présente le fichier fscmenu.xml utilisé pour afficher une barre d’outils en français.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Les Débuts rapides associés à cette section utilisent ce fichier XML pour afficher une barre d’outils personnalisée en français, comme le montre l’illustration précédente.

Spécifiez également une valeur de paramètre régional valide en appelant la méthode `HTMLRenderSpec` de l’objet `setLocale` et en transmettant une valeur de chaîne qui spécifie la valeur de paramètre régional. Par exemple, transmettez `fr_FR` pour spécifier le français. Le service Forms est fourni avec des barres d’outils localisées.

>[!NOTE]
>
>Avant de générer un formulaire HTML qui utilise une barre d’outils personnalisée, vous devez connaître le mode de rendu des formulaires HTML. (Voir [Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md).)

Pour plus d’informations sur le service Forms, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML contenant une barre d’outils personnalisée, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un objet API Java Forms.
1. Référencez un fichier XML fscmenu personnalisé.
1. Générer un formulaire HTML.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un objet API Java Forms**

Avant de pouvoir exécuter par programmation une opération prise en charge par le service Forms, vous devez créer un objet client Forms.

**Référence à un fichier XML fscmenu personnalisé**

Pour générer un formulaire HTML contenant une barre d’outils personnalisée, référencez un fichier XML fscmenu qui décrit la barre d’outils. (Cette section fournit deux exemples d’un fichier XML fscmenu.) Assurez-vous également que le fichier fscmenu.xml spécifie correctement l’emplacement de tous les fichiers référencés. Comme mentionné plus haut dans cette section, veillez à ce que tous les fichiers soient référencés par le mot-clé `FSToolBarURI` ou par leur emplacement absolu.

**Génération d’un formulaire HTML**

Pour générer un formulaire HTML, spécifiez une conception de formulaire qui a été créée dans Designer et enregistrée dans un fichier XDP. Sélectionnez également un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un fichier HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML requiert également des valeurs, telles que des valeurs URI pour le rendu d’autres types de formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client pour rendre le formulaire HTML visible aux utilisateurs.

**Voir également**

[Générer un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API du service Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md)

[Création d’Applications web renvoyant Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Générer un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Générer un formulaire HTML contenant une barre d’outils personnalisée à l’aide de l’API Forms Service (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Java Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un fichier XML fscmenu personnalisé

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `HTMLRenderSpec` de l’objet `setHTMLToolbar` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Spécifiez l’emplacement du fichier XML fscmenu en appelant la méthode `HTMLRenderSpec` de l’objet `setToolbarURI` et en transmettant une valeur de chaîne qui spécifie l’emplacement URI du fichier XML.
   * Le cas échéant, définissez la valeur du paramètre régional en appelant la méthode `HTMLRenderSpec` de l’objet `setLocale` et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional. La valeur par défaut est Anglais.

   >[!NOTE]
   >
   >Les Débuts rapides associés à cette section définissent cette valeur sur `fr_FR`*.*

1. Génération d’un formulaire HTML

   Appelez la méthode `renderHTMLForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur d’énumération `TransformTo` qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou une version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderHTMLForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l&#39;objet &quot;s `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `com.adobe.idp.Document` de l&#39;objet `getInputStream`.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la méthode `InputStream` de l’objet `read` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Début rapide (mode SOAP) : Rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API de service Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Générer un formulaire HTML contenant une barre d’outils personnalisée à l’aide de l’API Service Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de classe.

1. Création d’un objet API Java Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Référence à un fichier XML fscmenu personnalisé

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `HTMLRenderSpec` de l’objet `setHTMLToolbar` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Spécifiez l’emplacement du fichier XML fscmenu en appelant la méthode `HTMLRenderSpec` de l’objet `setToolbarURI` et en transmettant une valeur de chaîne qui spécifie l’emplacement URI du fichier XML.
   * Le cas échéant, définissez la valeur du paramètre régional en appelant la méthode `HTMLRenderSpec` de l’objet `setLocale` et en transmettant une valeur de chaîne qui spécifie la valeur du paramètre régional. La valeur par défaut est Anglais.

   >[!NOTE]
   >
   >Les Débuts rapides associés à cette section définissent cette valeur sur `fr_FR`*.*

1. Génération d’un formulaire HTML

   Appelez la méthode `renderHTMLForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur d’énumération `TransformTo` qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou une version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` qui stocke les valeurs URI requises pour générer un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous n’avez pas l’intention de joindre des fichiers au formulaire.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode `renderHTMLForm`. Cette valeur de paramètre stocke le formulaire rendu.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode `renderHTMLForm`. Ce paramètre stocke les données XML de sortie.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode `renderHTMLForm`. Cet argument enregistre le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode `renderHTMLForm`. Cet argument stocke la valeur du paramètre régional.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode `renderHTMLForm`. Cet argument stocke la valeur de rendu HTML utilisée.
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderHTMLForm` remplit l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `com.adobe.idp.services.holders.FormsResultHolder` de l&#39;objet `value`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `FormsResult` de l&#39;objet `getOutputContent`.
   * Obtenez le type de contenu de l&#39;objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l&#39;objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l&#39;objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la méthode `javax.servlet.http.HttpServletResponse` de l’objet `getOutputStream`.
   * Créez un tableau d’octets et remplissez-le en appelant la méthode `BLOB` de l’objet `getBinaryData`. Cette tâche affecte le contenu de l&#39;objet `FormsResult` au tableau d&#39;octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données de formulaire au navigateur Web client. Transférez le tableau d’octets à la méthode `write`.

**Voir également**

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
