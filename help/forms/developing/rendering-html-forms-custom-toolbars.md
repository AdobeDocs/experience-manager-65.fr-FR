---
title: Effectuer le rendu des formulaires HTML avec des barres d’outils personnalisées
description: Utilisez le service Forms pour personnaliser une barre d’outils qui est rendue avec un formulaire HTML. Vous pouvez effectuer le rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java et d’une API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '2328'
ht-degree: 100%

---

# Effectuer le rendu des formulaires HTML avec des barres d’outils personnalisées {#rendering-html-forms-with-customtoolbars}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## Effectuer le rendu des formulaires HTML avec des barres d’outils personnalisées {#rendering-html-forms-with-custom-toolbars}

Le service Forms vous permet de personnaliser une barre d’outils qui est rendue avec un formulaire HTML. Une barre d’outils peut être personnalisée pour modifier son apparence en remplaçant les styles CSS par défaut et pour ajouter un comportement dynamique en remplaçant les scripts Java. Une barre d’outils est personnalisée en utilisant un fichier XML appelé fscmenu.xml. Par défaut, le service Forms récupère ce fichier à partir d’un emplacement URI spécifié en interne.

>[!NOTE]
>
>Cet emplacement d’URI se trouve dans le fichier adobe-forms-core.jar, qui est situé dans le fichier adobe-forms-dsc.jar. Le fichier adobe-forms-dsc.jar se trouve dans le répertoire suivant : C:\Adobe\Adobe_Experience_Manager_forms\ (C:\ est le répertoire d’installation). Vous pouvez utiliser un outil d’extraction de fichiers, tel que Win RAR, pour ouvrir le fichier Adobe.

Vous pouvez copier le fichier fscmenu.xml à partir de cet emplacement, le modifier pour répondre à vos besoins, puis le placer dans un emplacement URI personnalisé. Ensuite, à l’aide de l’API du service Forms, définissez les options d’exécution pour que le service Forms utilise votre fichier fscmenu.xml à l’emplacement spécifié. Suite à ces actions, le service Forms effectue le rendu d’un formulaire HTML doté d’une barre d’outils personnalisée.

En plus du fichier fscmenu.xml, vous devez également obtenir les fichiers suivants :

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS est le script Java associé à chaque nœud. Il est nécessaire d’en fournir un pour le nœud `div#fscmenu` et éventuellement pour les nœuds `ul#fscmenuItem`. Les fichiers JS implémentent les fonctionnalités de base de la barre d’outils et le fonctionnement des fichiers par défaut.

fscCSS est une feuille de style associée à un nœud particulier. Les styles dans les fichiers CSS définissent l’apparence de la barre d’outils. *fscVCSS* est une feuille de style pour une barre d’outils verticale, qui s’affiche à gauche du formulaire HTML rendu. *fscIECSS* est une feuille de style utilisée pour les formulaires HTML rendus dans Internet Explorer.

Assurez-vous que tous les fichiers ci-dessus sont référencés dans le fichier fscmenu.xml. En d’autres termes, dans le fichier fscmenu.xml, spécifiez les emplacements URI pour pointer vers ces fichiers afin que le service Forms puisse les localiser. Par défaut, ces fichiers sont disponibles aux emplacements URI commençant par les mots-clés internes `FSWebRoot` ou `ApplicationWebRoot`.

Pour personnaliser la barre d’outils, remplacez ces mots-clés par le mot-clé externe `FSToolBarURI`. Ce mot-clé représente l’URI qui est transmis au service Forms au moment de l’exécution (cette approche est présentée plus loin dans cette section).

Vous pouvez également spécifier les emplacements absolus de ces fichiers JS et CSS, comme https://www.mycompany.com/scripts/misc/fscmenu.js. Dans ce cas, vous n’avez pas besoin d’utiliser le mot-clé `FSToolBarURI`.

>[!NOTE]
>
>Il n’est pas recommandé de mélanger les méthodes de référencement de ces fichiers. En d’autres termes, toutes les URI doivent être référencées en utilisant soit le mot-clé `FSToolBarURI`, soit un emplacement absolu.

Vous pouvez obtenir les fichiers JS et CSS en ouvrant le fichier adobe-forms-&lt;appserver>.ear. Dans ce fichier, ouvrez le fichier adobe-forms-res.war. Tous ces fichiers se trouvent dans le fichier WAR. Le fichier adobe-forms-&lt;appserver>.ear se trouve dans le dossier d’installation d’AEM Forms (C:\ est le répertoire d’installation). Vous pouvez ouvrir adobe-forms-&lt;appserver>.ear à l’aide d’un outil d’extraction de fichiers tel que WinRAR.

La syntaxe XML suivante présente un exemple de fichier fscmenu.xml.

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
>Le texte en gras représente les URI des fichiers CSS et JS qui doivent être référencées.

Les éléments suivants décrivent comment personnaliser une barre d’outils :

* Modifiez les valeurs des attributs `fscJS`, `fscCSS`, `fscVCSS` et `fscIECSS` (dans le fichier fscmenu.xml) pour refléter les emplacements personnalisés des fichiers référencés en utilisant l’une des méthodes décrites dans cette section (par exemple, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Tous les fichiers CSS et JS doivent être spécifiés. Si aucun des fichiers n’est modifié, indiquez celui par défaut à l’emplacement personnalisé. Vous pouvez obtenir les fichiers par défaut en ouvrant divers fichiers comme décrit dans cette section.
* La fourniture dʼune référence absolue (par exemple, https://www.example.com/scripts/custom-vertical-fscmenu.css) pour tout fichier est autorisée.
* Les fichiers JS et CSS requis par le nœud `div#fscmenu` sont essentiels au fonctionnement de la barre d’outils. Les nœuds `ul#fscmenuItem` individuels avoir ou non des fichiers JS ou CSS.

**Modifier la valeur des paramètres régionaux**

Lors de la personnalisation d’une barre d’outils, vous pouvez modifier la valeur des paramètres régionaux de celle-ci. En d’autres termes, vous pouvez l’afficher dans une autre langue. L’illustration suivante montre une barre d’outils personnalisée en langue française.

>[!NOTE]
>
>Il n’est pas possible de créer une barre d’outils personnalisée dans plusieurs langues. Les barres d’outils ne peuvent pas utiliser différents fichiers XML en fonction des paramètres régionaux.

Pour modifier la valeur des paramètres régionaux d’une barre d’outils, assurez-vous que le fichier fscmenu.xml contient la langue que vous souhaitez utiliser. La syntaxe XML suivante montre le fichier fscmenu.xml permettant dʼafficher une barre d’outils en français.

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
>Les démarrages rapides associés à cette section utilisent ce fichier XML pour afficher une barre d’outils personnalisée en français (cf illustration précédente).

Spécifiez également une valeur de paramètres régionaux valide en appelant la méthode `setLocale` de l’objet `HTMLRenderSpec` et en transmettant une valeur de chaîne qui spécifie la valeur des paramètres régionaux. Par exemple, transmettez `fr_FR` pour spécifier le français. Le service Forms est fourni avec des barres d’outils localisées.

>[!NOTE]
>
>Avant d’effectuer le rendu d’un formulaire HTML qui utilise une barre d’outils personnalisée, vous devez comprendre comment les formulaires HTML sont rendus. (Consultez la section [Rendre des formulaires en HTML](/help/forms/developing/rendering-forms-html.md)).

Pour plus d’informations sur le service Forms, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour effectuer le rendu d’un formulaire HTML qui contient une barre d’outils personnalisée, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API Java Forms.
1. Référencez un fichier XML fscmenu personnalisé.
1. Effectuez le rendu d’un formulaire HTML.
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer un objet API Java Forms**

Avant de pouvoir effectuer par programmation une opération prise en charge par le service Forms, vous devez créer un objet client Forms.

**Référencer un fichier XML fscmenu personnalisé**

Pour effectuer le rendu d’un formulaire HTML qui contient une barre d’outils personnalisée, référencez un fichier XML fscmenu qui décrit la barre d’outils. (Cette section fournit deux exemples de fichier XML fscmenu). Assurez-vous également que le fichier fscmenu.xml spécifie correctement les emplacements de tous les fichiers référencés. Comme mentionné précédemment dans cette section, veillez à ce que tous les fichiers soient référencés par le mot-clé `FSToolBarURI` ou par leur emplacement absolu.

**Effectuer le rendu d’un formulaire HTML**

Pour effectuer le rendu d’un formulaire HTML, spécifiez une conception de formulaire qui a été créée dans Designer et enregistrée en tant que fichier XDP. Sélectionnez également un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML nécessite également des valeurs, telles que des valeurs URI pour le rendu d’autres types de formulaires.

**Écrire le flux de données de formulaire dans le navigateur web du client**

Lorsque le service Forms effectue le rendu d’un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web du client pour que le formulaire HTML soit visible par les utilisateurs.

**Voir également**

[Effectuer le rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Effectuer le rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API de service web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Effectuer le rendu de formulaires en HTML](/help/forms/developing/rendering-forms-html.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Effectuer le rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Effectuez le rendu d’un formulaire HTML contenant une barre d’outils personnalisée à l’aide de l’API du service Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre projet Java Classpath.

1. Créer un objet API Java Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencer un fichier XML fscmenu personnalisé

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Indiquez l’emplacement du fichier XML fscmenu en appelant la méthode `setToolbarURI` de l’objet `HTMLRenderSpec` et en transmettant une valeur de chaîne qui spécifie l’emplacement URI du fichier XML.
   * Le cas échéant, définissez la valeur des paramètres régionaux en appelant la méthode `setLocale` de l’objet `HTMLRenderSpec` et en transmettant une valeur de chaîne qui spécifie la valeur des paramètres régionaux. La valeur par défaut est l’anglais.

   >[!NOTE]
   >
   >Les démarrages rapides se rapportant à cette section définissent cette valeur sur `fr_FR`*.*

1. Effectuer le rendu d’un formulaire HTML

   Appelez la méthode `renderHTMLForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document`.
   * L’objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur de chaîne qui spécifie la valeur de l’en-tête `HTTP_USER_AGENT`, telle que `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objet `URLSpec` qui stocke les valeurs URI nécessaires pour effectuer le rendu d’un formulaire HTML.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif, si vous ne souhaitez pas joindre de fichier au formulaire, indiquez `null`.

   La méthode `renderHTMLForm` renvoie un objet `FormsResult` qui contient un flux de données de formulaire qui doit être écrit dans le navigateur web du client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données du formulaire dans le navigateur web du client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : rendre un formulaire HTML avec une barre d’outils personnalisée à lʼaide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Effectuer le rendu d’un formulaire HTML avec une barre d’outils personnalisée à l’aide de l’API de service web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Effectuez le rendu d’un formulaire HTML contenant une barre d’outils personnalisée à lʼaide de l’API du service Forms (service web) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Créer un objet API Java Forms

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Référencer un fichier XML fscmenu personnalisé

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Indiquez l’emplacement du fichier XML fscmenu en appelant la méthode `setToolbarURI` de l’objet `HTMLRenderSpec` et en transmettant une valeur de chaîne qui spécifie l’emplacement URI du fichier XML.
   * Le cas échéant, définissez la valeur des paramètres régionaux en appelant la méthode `setLocale` de l’objet `HTMLRenderSpec` et en transmettant une valeur de chaîne qui spécifie la valeur des paramètres régionaux. La valeur par défaut est l’anglais.

   >[!NOTE]
   >
   >Les démarrages rapides se rapportant à cette section définissent cette valeur sur `fr_FR`*.*

1. Effectuer le rendu d’un formulaire HTML

   Appelez la méthode `renderHTMLForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Un objet `BLOB` qui contient les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`.
   * Lʼobjet `HTMLRenderSpec` qui stocke les options d’exécution du formulaire HTML.
   * Une valeur de chaîne qui spécifie la valeur de lʼen-tête `HTTP_USER_AGENT`, comme `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Un objet `URLSpec` qui stocke les valeurs URI nécessaires au rendu dʼun formulaire HTML.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide, renseigné par la méthode `renderHTMLForm`. La valeur de ce paramètre enregistre le formulaire rendu.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide, renseigné par la méthode `renderHTMLForm`. Ce paramètre stocke les données XML de sortie.
   * Un objet `javax.xml.rpc.holders.LongHolder` vide, renseigné par la méthode `renderHTMLForm`. Cet argument stocke le nombre de pages du formulaire.
   * Un objet `javax.xml.rpc.holders.StringHolder` vide, renseigné par la méthode `renderHTMLForm`. Cet argument stocke la valeur du paramètre régional.
   * Un objet `javax.xml.rpc.holders.StringHolder` vide, renseigné par la méthode `renderHTMLForm`. Cet argument stocke la valeur de rendu HTML utilisée.
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderHTMLForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream`, utilisé pour enregistrer le flux de données de formulaire dans le navigateur web du client, en appelant la méthode `getOutputStream` de lʼobjet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de lʼobjet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur web client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
