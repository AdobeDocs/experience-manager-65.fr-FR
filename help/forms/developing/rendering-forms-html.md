---
title: Rendu de Forms au format HTML
seo-title: Rendu de Forms au format HTML
description: Utilisez le service Forms pour effectuer le rendu des formulaires au format HTML en réponse à une requête HTTP provenant d’un navigateur Web. Vous pouvez utiliser l’API Java et l’API Web Service pour générer des formulaires au format HTML.
seo-description: Utilisez le service Forms pour effectuer le rendu des formulaires au format HTML en réponse à une requête HTTP provenant d’un navigateur Web. Vous pouvez utiliser l’API Java et l’API Web Service pour générer des formulaires au format HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4188'
ht-degree: 1%

---

# Rendu de Forms au format HTML {#rendering-forms-as-html}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Le service Forms effectue le rendu des formulaires au format HTML en réponse à une requête HTTP provenant d’un navigateur Web. L’un des avantages du rendu d’un formulaire au format HTML réside dans le fait que l’ordinateur sur lequel se trouve le navigateur Web client ne nécessite pas Adobe Reader, Acrobat ou Flash Player (pour les guides de formulaire (obsolète)).

Pour générer un formulaire au format HTML, la conception de formulaire doit être enregistrée en tant que fichier XDP. Une conception de formulaire enregistrée en tant que fichier PDF ne peut pas être rendue au format HTML. Lors du développement d’une conception de formulaire dans Designer qui sera rendue au format HTML, tenez compte des critères suivants :

* N’utilisez pas les propriétés de bordure d’un objet pour tracer des lignes, des zones ou des grilles dans un formulaire. Certains navigateurs n’alignent pas les bordures exactement comme elles sont présentées dans un aperçu de Les objets risquent de se chevaucher ou de déplacer d’autres objets de manière imprévue.
* Vous pouvez utiliser des lignes, des rectangles et des cercles pour définir l’arrière-plan.
* Dessinez du texte légèrement plus grand que ce qui semble être nécessaire pour s’adapter au texte. Certains navigateurs Web n’affichent pas le texte de manière lisible.

>[!NOTE]
>
>Lors du rendu d’un formulaire contenant des images TIFF à l’aide des méthodes `(Deprecated) renderHTMLForm` et `renderHTMLForm2` de l’objet `FormServiceClient`, les images TIFF ne sont pas visibles dans le formulaire HTML rendu affiché dans les navigateurs Internet Explorer ou Mozilla Firefox. Ces navigateurs ne fournissent pas de prise en charge native des images TIFF.

## Pages HTML {#html-pages}

Lorsqu’une conception de formulaire est générée sous la forme d’un formulaire HTML, chaque sous-formulaire de second niveau est généré sous la forme d’une page HTML (panneau). Vous pouvez afficher la hiérarchie d’un sous-formulaire dans Designer. Les sous-formulaires enfants qui appartiennent au sous-formulaire racine (le nom par défaut d’un sous-formulaire racine est form1) sont les sous-formulaires de panneau. L’exemple suivant illustre les sous-formulaires d’une conception de formulaire.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

Lorsque les conceptions de formulaire sont rendues sous forme de formulaires HTML, les panneaux ne sont pas limités à une taille de page particulière. Si vous disposez de sous-formulaires dynamiques, ils doivent être imbriqués dans le sous-formulaire du panneau. Les sous-formulaires dynamiques peuvent s’étendre à un nombre infini de pages HTML.

Lorsqu’un formulaire est rendu au format HTML, les formats de page (requis pour paginer les formulaires rendus au format PDF) n’ont aucune signification. Comme un formulaire avec disposition souple peut atteindre un nombre infini de pages HTML, il est important d’éviter les pieds de page sur le gabarit. Un pied de page situé sous la zone de contenu d’un gabarit peut remplacer le contenu HTML qui s’étend au-delà d’une limite de page.

Vous devez explicitement passer d’un panneau à un autre à l’aide des méthodes `xfa.host.pageUp` et `xfa.host.pageDown`. Vous pouvez modifier les pages en envoyant un formulaire au service Forms et en demandant au service Forms de le rendre à nouveau sur le périphérique client, généralement un navigateur Web.

>[!NOTE]
>
>Le processus d’envoi d’un formulaire au service Forms, puis de renvoi du formulaire par le service Forms vers le périphérique client est appelé données de basculement arrondies vers le serveur.

>[!NOTE]
>
>Si vous souhaitez personnaliser l’aspect du bouton de signature numérique HTML sur un formulaire HTML, vous devez modifier les propriétés suivantes dans le fichier fscdigsig.css (dans le fichier adobe-forms-ds.ear > adobe-forms-ds.war) :

**.fsc-ds-ssb** : Cette feuille de style s’applique en cas de champ de signe vide.

**.fsc-ds-ssv** : Cette feuille de style s’applique dans le cas d’un champ de signe valide.

**.fsc-ds-ssc** : Cette feuille de style s’applique dans le cas d’un champ de signe valide, mais les données ont changé.

**.fsc-ds-ssi** : Cette feuille de style s’applique en cas de champ de signature non valide.

**.fsc-ds-popup-bg** : Cette propriété de feuille de style n’est pas utilisée.

**.fsc-ds-popup-btn** : Cette propriété de feuille de style n’est pas utilisée.

## Exécution de scripts {#running-scripts}

Un auteur de formulaire indique si un script s’exécute sur le serveur ou sur le client. Le service Forms crée un environnement de traitement des événements distribué pour l’exécution des renseignements sur les formulaires qui peuvent être distribués entre le client et le serveur à l’aide de l’attribut `runAt` . Pour plus d’informations sur cet attribut ou la création de scripts dans les conceptions de formulaire, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Le service Forms peut exécuter des scripts pendant la génération du formulaire. Par conséquent, vous pouvez préremplir un formulaire avec des données en vous connectant à une base de données ou à des services Web qui ne sont peut-être pas disponibles sur le client. Vous pouvez également définir l’événement `Click` d’un bouton pour qu’il s’exécute sur le serveur afin que le client puisse arrondir les données du déplacement au serveur. Cela permet au client d’exécuter des scripts qui peuvent nécessiter des ressources serveur, telles qu’une base de données d’entreprise, lorsqu’un utilisateur interagit avec un formulaire. Pour les formulaires HTML, les scripts formcalc ne peuvent être exécutés que sur le serveur. Par conséquent, vous devez marquer ces scripts pour qu’ils s’exécutent à `server` ou `both`.

Vous pouvez concevoir des formulaires qui se déplacent entre les pages (panneaux) en appelant les méthodes `xfa.host.pageUp` et `xfa.host.pageDown`. Ce script est placé dans l’événement `Click` d’un bouton et l’attribut `runAt` est défini sur `Both`. La raison pour laquelle vous choisissez `Both` est telle qu’Adobe Reader ou Acrobat (pour les formulaires rendus au format PDF) peut modifier les pages sans accéder au serveur et les formulaires HTML peuvent changer les pages en arrondissant les données au serveur. En d’autres termes, un formulaire est envoyé au service Forms et un formulaire est rendu au format HTML avec la nouvelle page affichée.

Il est recommandé de ne pas donner aux variables de script et aux champs de formulaire les mêmes noms que les éléments, par exemple. Certains navigateurs Web, tels qu’Internet Explorer, peuvent ne pas initialiser une variable portant le même nom qu’un champ de formulaire, ce qui entraîne une erreur de script. Il est recommandé de donner aux champs de formulaire et aux variables de script différents noms.

Lors du rendu de formulaires HTML qui contiennent à la fois la fonctionnalité de navigation de page et des scripts de formulaire (supposons, par exemple, qu’un script récupère les données de champ d’une base de données chaque fois que le formulaire est généré), assurez-vous que le script de formulaire se trouve dans l’événement form:calculate au lieu de form:readyevent.

Les scripts de formulaire situés dans l’événement form:ready ne sont exécutés qu’une seule fois lors du rendu initial du formulaire et ne sont pas exécutés pour les récupérations de page suivantes. En revanche, l’événement form:calculate est exécuté pour chaque navigation de page dans laquelle le formulaire est rendu.

>[!NOTE]
Dans un formulaire multipage, les modifications apportées par JavaScript à une page ne sont pas conservées si vous passez à une autre page.

Vous pouvez appeler des scripts personnalisés avant d’envoyer un formulaire. Cette fonctionnalité fonctionne sur tous les navigateurs disponibles. Cependant, il ne peut être utilisé que lorsque les utilisateurs affichent le formulaire HTML dont la propriété `Output Type` est définie sur `Form Body`. Cela ne fonctionnera pas lorsque la valeur `Output Type` est `Full HTML`. Pour connaître les étapes de configuration de cette fonctionnalité, voir Configuration des formulaires dans l’aide à l’administration .

Vous devez d’abord définir une fonction de rappel appelée avant d’envoyer le formulaire, où le nom de la fonction est `_user_onsubmit`. On suppose que la fonction ne renvoie aucune exception ou que, dans ce cas, l’exception est ignorée. Il est recommandé de placer la fonction JavaScript dans la section head du fichier html ; cependant, vous pouvez le déclarer n’importe où avant la fin des balises de script qui incluent `xfasubset.js`.

Lorsque le serveur de formulaires effectue le rendu d’un fichier XDP contenant une liste déroulante, en plus de créer la liste déroulante, il crée également deux champs de texte masqués. Ces champs de texte stockent les données de la liste déroulante (l’un stocke le nom d’affichage des options et l’autre stocke la valeur des options). Par conséquent, chaque fois qu’un utilisateur envoie le formulaire, toutes les données de la liste déroulante sont envoyées. En supposant que vous ne souhaitiez pas envoyer autant de données à chaque fois, vous pouvez écrire un script personnalisé pour le désactiver. Par exemple : Le nom de la liste déroulante est `drpOrderedByStateProv` et est placé sous l’en-tête du sous-formulaire. Le nom de l’élément d’entrée HTML sera `header[0].drpOrderedByStateProv[0]`. Le nom des champs masqués qui stockent et envoient les données de la liste déroulante porte les noms suivants : `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Vous pouvez désactiver ces éléments d’entrée de la manière suivante si vous ne souhaitez pas publier les données. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## Sous-ensembles XFA {#xfa-subsets}

Lors de la création de conceptions de formulaire pour un rendu au format HTML, vous devez limiter votre script au sous-ensemble XFA pour les scripts en langage JavaScript.

Les scripts qui s’exécutent sur le client ou s’exécutent sur le client et le serveur doivent être écrits dans le sous-ensemble XFA. Les scripts qui s’exécutent sur le serveur peuvent utiliser le modèle de script XFA complet et également FormCalc. Pour plus d’informations sur l’utilisation de JavaScript, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Lors de l’exécution de scripts sur le client, seul le panneau actuel affiché peut utiliser le script ; par exemple, vous ne pouvez pas créer de script pour les champs situés dans le panneau A lorsque le panneau B est affiché. Lors de l’exécution de scripts sur le serveur, tous les panneaux sont accessibles.

Vous devez également faire attention lorsque vous utilisez des expressions SOM (Scripting Object Model) dans des scripts exécutés sur le client. Seuls un sous-ensemble simplifié d’expressions SOM est pris en charge par les scripts qui s’exécutent sur le client.

## Timing de l’événement {#event-timing}

Le sous-ensemble XFA définit les événements XFA associés aux événements HTML. Il existe une légère différence de comportement dans le minutage des événements de calcul et de validation. Dans un navigateur web, un événement calculate complet est exécuté lorsque vous quittez un champ. Les événements de calcul ne sont pas automatiquement exécutés lorsque vous modifiez une valeur de champ. Vous pouvez forcer un événement calculate en appelant la méthode `xfa.form.execCalculate` .

Dans un navigateur web, les événements de validation ne sont exécutés que lors de la sortie d’un champ ou de l’envoi d’un formulaire. Vous pouvez forcer un événement validate à l’aide de la méthode `xfa.form.execValidate`.

Forms affiché dans un navigateur web (par opposition à Adobe Reader ou Acrobat) est conforme au test null XFA (erreurs ou avertissements) pour les champs obligatoires.

* Si le test null génère une erreur et que vous quittez un champ sans spécifier de valeur, une zone de message s’affiche et vous êtes repositionné dans le champ après avoir cliqué sur OK.
* Si un test null génère un avertissement et que vous quittez un champ sans spécifier de valeur, vous êtes invité à cliquer sur OK ou Annuler, ce qui vous donne la possibilité de continuer sans spécifier de valeur ou de revenir au champ pour saisir une valeur.

Pour plus d’informations sur un test null, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Boutons de formulaire {#form-buttons}

Cliquer sur un bouton Envoyer envoie les données de formulaire au service Forms et représente la fin du traitement du formulaire. L’événement `preSubmit` peut être défini pour s’exécuter sur le client ou le serveur. L’événement `preSubmit` s’exécute avant l’envoi du formulaire s’il est configuré pour s’exécuter sur le client. Dans le cas contraire, l’événement `preSubmit` s’exécute sur le serveur lors de l’envoi du formulaire. Pour plus d’informations sur l’événement `preSubmit`, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Si aucun script côté client n’est associé à un bouton, les données sont envoyées au serveur, les calculs sont effectués sur le serveur et le formulaire HTML est régénéré. Si un bouton contient un script côté client, les données ne sont pas envoyées au serveur et le script côté client est exécuté dans le navigateur web.

## Navigateur web HTML 4.0 {#html-4-0-web-browser}

Un navigateur web qui ne prend en charge que HTML 4.0 ne peut pas prendre en charge le modèle de script du sous-ensemble XFA côté client. Lors de la création d’une conception de formulaire pour fonctionner à la fois dans HTML 4.0 et MSDHTML ou CSS2HTML, un script marqué pour s’exécuter au niveau du client s’exécute sur le serveur. Supposons, par exemple, qu’un utilisateur clique sur un bouton situé sur un formulaire affiché dans un navigateur Web HTML 4.0. Dans ce cas, les données de formulaire sont envoyées au serveur sur lequel le script client est exécuté.

Il est recommandé de placer la logique de formulaire dans les événements calculate, qui s’exécutent sur le serveur en HTML 4.0 et sur le client pour MSDHTML ou CSS2HTML.

## Maintenance des modifications de présentation {#maintaining-presentation-changes}

Lorsque vous vous déplacez entre des pages HTML (panneaux), seul l’état des données est conservé. Les paramètres tels que la couleur d’arrière-plan ou les paramètres de champ obligatoires ne sont pas conservés (s’ils sont différents des paramètres initiaux). Pour conserver l’état de présentation, vous devez créer des champs (généralement masqués) qui représentent l’état de présentation des champs. Si vous ajoutez un script à l’événement `Calculate` d’un champ qui modifie la présentation en fonction des valeurs de champ masqué, vous pouvez conserver l’état de la présentation lorsque vous passez d’une page HTML à l’autre (panneaux).

Le script suivant conserve la valeur `fillColor` d’un champ en fonction de la valeur de `hiddenField`. Supposons que ce script se trouve dans l’événement `Calculate` d’un champ.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Les objets statiques ne sont pas affichés dans un formulaire HTML rendu lorsqu’ils sont imbriqués dans une cellule de tableau. Par exemple, un cercle et un rectangle imbriqués dans une cellule de tableau ne s’affichent pas dans un formulaire HTML de rendu. Toutefois, ces mêmes objets statiques s’affichent correctement lorsqu’ils sont situés en dehors du tableau.

## Signature numérique de formulaires HTML {#digitally-signing-html-forms}

Vous ne pouvez pas signer un formulaire HTML contenant un champ de signature numérique si le formulaire est rendu comme l’une des transformations HTML suivantes :

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Pour plus d’informations sur la signature numérique d’un document, voir [Signature numérique et certification de documents](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendu d’un formulaire XHTML conforme aux consignes d’accessibilité {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Vous pouvez générer un formulaire HTML complet conforme aux directives d’accessibilité. En d’autres termes, le formulaire est rendu dans des balises HTML complètes, contrairement au formulaire HTML généré dans des balises de contenu (et non dans une page HTML complète).

## Validation des données de formulaire {#validating-form-data}

Il est recommandé de limiter l’utilisation des règles de validation pour les champs de formulaire lors du rendu du formulaire au format HTML. Certaines règles de validation peuvent ne pas être prises en charge pour les formulaires HTML. Par exemple, lorsqu’un modèle de validation MM-JJ-AAAA est appliqué à un champ `Date/Time` situé dans une conception de formulaire rendue sous forme de formulaire HTML, il ne fonctionne pas correctement, même si la date est correctement saisie. Cependant, ce modèle de validation fonctionne correctement pour les formulaires rendus au format PDF.

>[!NOTE]
Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet API client Forms.
1. Définissez les options d’exécution HTML.
1. Générer un formulaire HTML.
1. Ecrivez le flux de données de formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API client Forms**

Avant de pouvoir importer des données par programmation dans une API PDF formClient, vous devez créer un client de service Form Data Integration . Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Définition des options d’exécution HTML**

Vous définissez les options d’exécution HTML lors du rendu d’un formulaire HTML. Par exemple, vous pouvez ajouter une barre d’outils à un formulaire HTML pour permettre aux utilisateurs de sélectionner les pièces jointes situées sur l’ordinateur client ou de récupérer les pièces jointes générées avec le formulaire HTML. Par défaut, une barre d’outils HTML est désactivée. Pour ajouter une barre d’outils à un formulaire HTML, vous devez définir par programmation les options d’exécution. Par défaut, une barre d’outils HTML se compose des boutons suivants :

* `Home`: Fournit un lien vers la racine Web de l’application.
* `Upload`: Fournit une interface utilisateur pour sélectionner les fichiers à joindre au formulaire actif.
* `Download`: Fournit une interface utilisateur pour afficher les fichiers joints.

Lorsqu’une barre d’outils HTML apparaît sur un formulaire HTML, l’utilisateur peut sélectionner un maximum de dix fichiers à envoyer avec les données de formulaire. Une fois les fichiers envoyés, le service Forms peut les récupérer.

Lors du rendu d’un formulaire au format HTML, vous pouvez spécifier une valeur agent-utilisateur. Une valeur agent-utilisateur fournit des informations sur le navigateur et le système. Il s’agit d’une valeur facultative que vous pouvez transmettre à une valeur de chaîne vide. Le guide de démarrage rapide Rendu d’un formulaire HTML à l’aide de l’API Java indique comment obtenir une valeur d’agent utilisateur et l’utiliser pour générer un formulaire au format HTML.

Les URL HTTP vers l’emplacement où les données de formulaire sont publiées peuvent être spécifiées en définissant l’URL cible à l’aide de l’API client du service Forms ou peuvent être spécifiées dans le bouton Envoyer contenu dans la conception de formulaire XDP. Si l’URL cible est spécifiée dans la conception de formulaire, ne définissez pas de valeur à l’aide de l’API client du service Forms.

>[!NOTE]
Le rendu d’un formulaire HTML avec une barre d’outils est facultatif.

>[!NOTE]
Si vous générez un formulaire AHTML, il est recommandé de ne pas ajouter de barre d’outils au formulaire.

**Rendu d’un formulaire HTML**

Pour générer un formulaire HTML, vous devez spécifier une conception de formulaire créée dans Designer et enregistrée en tant que fichier XDP. Vous devez également sélectionner un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML nécessite également des valeurs, telles que des valeurs URI requises pour effectuer le rendu d’autres types de formulaire.

**Écrire le flux de données de formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire HTML est visible par l’utilisateur.

**Voir également**

[Rendu d’un formulaire au format HTML à l’aide de l’API Java](#render-a-form-as-html-using-the-java-api)

[Rendu d’un formulaire au format HTML à l’aide de l’API du service Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu de HTML Forms avec des barres d’outils personnalisées](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Rendu d’un formulaire au format HTML à l’aide de l’API Java {#render-a-form-as-html-using-the-java-api}

Rendre un formulaire HTML à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définition des options d’exécution HTML

   * Créez un objet `HTMLRenderSpec` à l’aide de son constructeur.
   * Pour effectuer le rendu d’un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir la valeur locale du formulaire HTML, appelez la méthode `setLocale` de l’objet `HTMLRenderSpec` et transmettez une valeur string qui spécifie la valeur locale. (Il s’agit d’un paramètre facultatif.)
   * Pour effectuer le rendu du formulaire HTML dans des balises HTML complètes, appelez la méthode `setOutputType` de l’objet `HTMLRenderSpec` et transmettez `OutputType.FullHTMLTags`. (Il s’agit d’un paramètre facultatif.)

   >[!NOTE]
   Le rendu de Forms ne s’effectue pas correctement en HTML lorsque l’option `StandAlone` est `true` et que `ApplicationWebRoot` référence un serveur autre que le serveur d’applications J2EE hébergeant AEM Forms (la valeur `ApplicationWebRoot` est spécifiée à l’aide de l’objet `URLSpec` transmis à la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient`). Lorsque `ApplicationWebRoot` est un autre serveur de celui qui héberge AEM Forms, la valeur de l’URI racine Web dans la console d’administration doit être définie comme valeur de l’URI de l’application Web du formulaire. Pour ce faire, connectez-vous à la console d’administration, cliquez sur Services > Forms, puis définissez l’URI racine Web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Rendu d’un formulaire HTML

   Appelez la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` enum qui spécifie le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur string qui spécifie la valeur d’en-tête `HTTP_USER_AGENT` ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` qui stocke les valeurs URI nécessaires au rendu d’un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `(Deprecated) renderHTMLForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire pouvant être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l’objet `getOutputContent`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `InputStream` de l’objet `read` et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Rendu de Forms au format HTML](#rendering-forms-as-html)

[Démarrage rapide (mode SOAP) : Rendu d’un formulaire HTML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendu d’un formulaire au format HTML à l’aide de l’API de service Web {#render-a-form-as-html-using-the-web-service-api}

Rendre un formulaire HTML à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans le chemin de classe.

1. Création d’un objet API client Forms

   Créez un objet `FormsService` et définissez des valeurs d’authentification.

1. Définition des options d’exécution HTML

   * Créez un objet `HTMLRenderSpec` à l’aide de son constructeur.
   * Pour effectuer le rendu d’un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir la valeur locale du formulaire HTML, appelez la méthode `setLocale` de l’objet `HTMLRenderSpec` et transmettez une valeur string qui spécifie la valeur locale. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Pour effectuer le rendu du formulaire HTML dans des balises HTML complètes, appelez la méthode `setOutputType` de l’objet `HTMLRenderSpec` et transmettez `OutputType.FullHTMLTags`.

   >[!NOTE]
   Le rendu de Forms ne s’effectue pas correctement en HTML lorsque l’option `StandAlone` est `true` et que `ApplicationWebRoot` référence un serveur autre que le serveur d’applications J2EE hébergeant AEM Forms (la valeur `ApplicationWebRoot` est spécifiée à l’aide de l’objet `URLSpec` transmis à la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient`). Lorsque `ApplicationWebRoot` est un autre serveur de celui qui héberge AEM Forms, la valeur de l’URI racine Web dans la console d’administration doit être définie comme valeur de l’URI de l’application Web du formulaire. Pour ce faire, connectez-vous à la console d’administration, cliquez sur Services > Forms, puis définissez l’URI racine Web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Rendu d’un formulaire HTML

   Appelez la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire qui fait partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` enum qui spécifie le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner les données, transmettez `null`. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur string qui spécifie la valeur d’en-tête `HTTP_USER_AGENT` ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` qui stocke les valeurs URI nécessaires au rendu d’un formulaire HTML. (Voir [Spécification des valeurs URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif qui vous permet de spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire. (Voir [Joindre des fichiers au formulaire](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode . Cette valeur de paramètre stocke le formulaire rendu.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide renseigné par la méthode . Ce paramètre stocke les données XML de sortie.
   * Objet `javax.xml.rpc.holders.LongHolder` vide renseigné par la méthode . Cet argument stocke le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode . Cet argument stocke la valeur du paramètre régional.
   * Objet `javax.xml.rpc.holders.StringHolder` vide renseigné par la méthode . Cet argument stocke la valeur de rendu HTML utilisée.
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `(Deprecated) renderHTMLForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Écrire le flux de données de formulaire dans le navigateur Web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` contenant des données de formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Rendu de Forms au format HTML](#rendering-forms-as-html)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
