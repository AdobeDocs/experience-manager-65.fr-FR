---
title: Rendu des formulaires au format HTML
seo-title: Rendu des formulaires au format HTML
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '4108'
ht-degree: 1%

---


# Rendu des formulaires au format HTML {#rendering-forms-as-html}

Le service Forms effectue le rendu des formulaires au format HTML en réponse à une requête HTTP provenant d’un navigateur Web. Le rendu d’un formulaire au format HTML présente l’avantage de ne pas nécessiter Adobe Reader, Acrobat ou Flash Player pour l’ordinateur sur lequel se trouve le navigateur Web client (pour les guides de formulaire (obsolète)).

Pour générer un formulaire au format HTML, la conception de formulaire doit être enregistrée dans un fichier XDP. Une conception de formulaire enregistrée au format PDF ne peut pas être générée au format HTML. Lorsque vous développez une conception de formulaire dans Designer qui sera rendue au format HTML, tenez compte des critères suivants :

* N’utilisez pas les propriétés de bordure d’un objet pour tracer des lignes, des zones ou des grilles dans un formulaire. Certains navigateurs n’alignent pas les bordures exactement comme elles sont présentées dans un aperçu de Les objets risquent de se chevaucher ou de déplacer d’autres objets de manière imprévue.
* Vous pouvez utiliser des lignes, des rectangles et des cercles pour définir l’arrière-plan.
* Tracez du texte légèrement plus grand que ce qui semble être nécessaire pour s’adapter au texte. Certains navigateurs Web n’affichent pas le texte de manière lisible.

>[!NOTE]
>
>Lors du rendu d’un formulaire contenant des images TIFF à l’aide des méthodes `FormServiceClient` et `(Deprecated) renderHTMLForm` `renderHTMLForm2` méthodes de l’objet, les images TIFF ne sont pas visibles dans le formulaire HTML rendu affiché dans les navigateurs Internet Explorer ou Mozilla Firefox. Ces navigateurs n’offrent pas de prise en charge native des images TIFF.

## Pages HTML {#html-pages}

Lorsqu’une conception de formulaire est générée sous la forme d’un formulaire HTML, chaque sous-formulaire de second niveau est généré sous la forme d’une page HTML (panneau). Vous pouvez vue la hiérarchie d’un sous-formulaire dans Designer. Les sous-formulaires enfants qui appartiennent au sous-formulaire racine (le nom par défaut d’un sous-formulaire racine est form1) sont les sous-formulaires de panneau. L’exemple suivant montre les sous-formulaires d’une conception de formulaire.

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

Lorsque les conceptions de formulaire sont générées sous forme de formulaires HTML, les panneaux ne sont pas limités à une taille de page particulière. Si vous disposez de sous-formulaires dynamiques, ils doivent être imbriqués dans le sous-formulaire de panneau. Les sous-formulaires dynamiques peuvent s’étendre à un nombre infini de pages HTML.

Lorsqu’un formulaire est rendu sous la forme d’un formulaire HTML, les formats de page (requis pour paginer les formulaires rendus au format PDF) n’ont aucune signification. Un formulaire avec une disposition souple pouvant atteindre un nombre infini de pages HTML, il est important d’éviter les pieds de page sur le gabarit. Un pied de page situé sous la zone de contenu d’un gabarit peut remplacer le contenu HTML qui déborde d’une limite de page.

Vous devez explicitement passer d’un panneau à l’autre à l’aide des méthodes `xfa.host.pageUp` et `xfa.host.pageDown` . Vous modifiez les pages en envoyant un formulaire au service Forms et en demandant au service Forms de le rendre à nouveau sur le périphérique client, généralement un navigateur Web.

>[!NOTE]
>
>Le processus d’envoi d’un formulaire au service Forms, puis de réacheminement du formulaire par le service Forms vers le périphérique client est appelé données d’extraction arrondies vers le serveur.

>[!NOTE]
>
>Si vous souhaitez personnaliser l’aspect du bouton Signature numérique HTML sur un formulaire HTML, vous devez modifier les propriétés suivantes dans le fichier fscdigsig.css (dans le fichier adobe-forms-ds.ear > adobe-forms-ds.war) :

**.fsc-ds-ssb**: Cette feuille de style est applicable en cas de champ de signe vide.

**.fsc-ds-ssv**: Cette feuille de style est applicable en cas de champ de signature valide.

**.fsc-ds-ssc**: Cette feuille de style s’applique dans le cas d’un champ de signature valide, mais les données ont changé.

**.fsc-ds-ssi**: Cette feuille de style est applicable en cas de champ de signature non valide.

**.fsc-ds-popup-bg**: Cette propriété de feuille de style n’est pas utilisée.

**.fsc-ds-popup-btn**: Cette propriété de feuille de style n’est pas utilisée.

## Exécution de scripts {#running-scripts}

Un auteur de formulaire indique si un script s’exécute sur le serveur ou sur le client. Le service Forms crée un environnement de traitement de événement distribué pour l’exécution de l’intelligence des formulaires qui peut être distribué entre le client et le serveur à l’aide de l’ `runAt` attribut. Pour plus d’informations sur cet attribut ou la création de scripts dans les conceptions de formulaire, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Le service Forms peut exécuter des scripts pendant la génération du formulaire. Par conséquent, vous pouvez préremplir un formulaire avec des données en vous connectant à une base de données ou à des services Web qui ne sont peut-être pas disponibles sur le client. Vous pouvez également définir le `Click` événement d’un bouton pour qu’il s’exécute sur le serveur, de sorte que le client effectue un aller-retour des données vers le serveur. Cela permet au client d’exécuter des scripts qui peuvent nécessiter des ressources serveur, telles qu’une base de données d’entreprise, pendant qu’un utilisateur interagit avec un formulaire. Pour les formulaires HTML, les scripts formcalc peuvent être exécutés sur le serveur uniquement. Par conséquent, vous devez marquer ces scripts pour qu’ils s’exécutent sur `server` ou `both`.

Vous pouvez concevoir des formulaires qui se déplacent d’une page à l’autre (panneaux) en appelant `xfa.host.pageUp` et en `xfa.host.pageDown` appliquant les méthodes. Ce script est placé dans le `Click` événement d’un bouton et l’ `runAt` attribut est défini sur `Both`. La raison de votre choix `Both` est que Adobe Reader ou Acrobat (pour les formulaires rendus au format PDF) peut modifier les pages sans passer par le serveur et que les formulaires HTML peuvent modifier les pages en arrondissant les données de tri au serveur. En d’autres termes, un formulaire est envoyé au service Forms et un formulaire est rendu au format HTML avec la nouvelle page affichée.

Il est recommandé de ne pas donner aux variables de script et aux champs de formulaire les mêmes noms que les éléments, par exemple. Certains navigateurs Web, tels qu’Internet Explorer, peuvent ne pas initialiser une variable portant le même nom qu’un champ de formulaire, ce qui entraîne une erreur de script. Il est recommandé de donner différents noms aux champs de formulaire et aux variables de script.

Lors du rendu de formulaires HTML qui contiennent à la fois la fonctionnalité de navigation de page et les scripts de formulaire (par exemple, supposons qu’un script récupère les données de champ d’une base de données chaque fois que le formulaire est rendu), assurez-vous que le script de formulaire se trouve dans le événement form:calculate et non dans le formulaire:readyevent.

Les scripts de formulaire situés dans le événement form:ready ne sont exécutés qu’une seule fois lors du rendu initial du formulaire et ne sont pas exécutés pour les récupérations de page suivantes. En revanche, le événement form:calculate est exécuté pour chaque navigation de page dans laquelle le formulaire est généré.

>[!NOTE]
Dans un formulaire multipage, les modifications apportées par JavaScript à une page ne sont pas conservées si vous passez à une autre page.

Vous pouvez appeler des scripts personnalisés avant d’envoyer un formulaire. Cette fonction fonctionne sur tous les navigateurs disponibles. Cependant, il ne peut être utilisé que lorsque les utilisateurs effectuent le rendu du formulaire HTML dont la `Output Type` propriété est définie sur `Form Body`. Ça ne marchera pas quand le `Output Type` sera `Full HTML`. Reportez-vous à la rubrique Configuration de formulaires dans l’aide à l’administration pour connaître les étapes de configuration de cette fonctionnalité.

Vous devez d’abord définir une fonction de rappel appelée avant d’envoyer le formulaire, où se trouve le nom de la fonction `_user_onsubmit`. On suppose que la fonction ne va pas lancer d&#39;exception, ou si elle le fait, l&#39;exception sera ignorée. Il est recommandé de placer la fonction JavaScript dans la section head du fichier html ; toutefois, vous pouvez le déclarer n’importe où avant la fin des balises de script qui incluent `xfasubset.js`.

Lorsque le serveur de formulaires effectue le rendu d’un fichier XDP contenant une liste déroulante, en plus de créer la liste déroulante, il crée également deux champs de texte masqués. Ces champs de texte stockent les données de la liste déroulante (l’un stocke le nom d’affichage des options et l’autre stocke la valeur des options). Par conséquent, chaque fois qu’un utilisateur envoie le formulaire, toutes les données de la liste déroulante sont envoyées. En supposant que vous ne souhaitiez pas envoyer autant de données à chaque fois, vous pouvez écrire un script personnalisé pour désactiver cette fonction. Par exemple : Le nom de la liste déroulante est `drpOrderedByStateProv` placé sous l’en-tête de sous-formulaire. Le nom de l’élément d’entrée HTML sera `header[0].drpOrderedByStateProv[0]`indiqué. Le nom des champs masqués qui stockent et envoient les données de la liste déroulante porte les noms suivants : `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

Lors de la création de conceptions de formulaire à générer au format HTML, vous devez limiter votre script au sous-ensemble XFA pour les scripts en langage JavaScript.

Les scripts qui s’exécutent sur le client ou sur le client et le serveur doivent être écrits dans le sous-ensemble XFA. Les scripts qui s’exécutent sur le serveur peuvent utiliser le modèle de script XFA complet et également FormCalc. Pour plus d’informations sur l’utilisation de JavaScript, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Lors de l’exécution de scripts sur le client, seul le panneau actif affiché peut utiliser un script ; par exemple, vous ne pouvez pas effectuer de script sur les champs situés dans le panneau A lorsque le panneau B est affiché. Lors de l’exécution de scripts sur le serveur, tous les panneaux sont accessibles.

Vous devez également être prudent lors de l’utilisation d’expressions de modèle d’objet de script (SOM) dans des scripts exécutés sur le client. Seuls les scripts exécutés sur le client prennent en charge un sous-ensemble simplifié d’expressions SOM.

## Horodatage du Événement {#event-timing}

Le sous-ensemble XFA définit les événements XFA qui sont associés à des événements HTML. Il y a une légère différence de comportement dans le timing des événements de calcul et de validation. Dans un navigateur Web, un événement de calcul complet est exécuté lorsque vous quittez un champ. Les événements de calcul ne sont pas automatiquement exécutés lorsque vous modifiez la valeur d’un champ. Vous pouvez forcer un événement de calcul en appelant la `xfa.form.execCalculate` méthode.

Dans un navigateur Web, les événements de validation ne sont exécutés que lorsque vous quittez un champ ou envoyez un formulaire. Vous pouvez forcer un événement de validation à l’aide de la `xfa.form.execValidate` méthode.

Les formulaires affichés dans un navigateur Web (par opposition à Adobe Reader ou Acrobat) sont conformes au test null XFA (erreurs ou avertissements) pour les champs obligatoires.

* Si le test null génère une erreur et que vous quittez un champ sans spécifier de valeur, une boîte de message s’affiche et vous êtes repositionné dans le champ après avoir cliqué sur OK.
* Si un test null génère un avertissement et que vous quittez un champ sans spécifier de valeur, vous êtes invité à cliquer sur OK ou sur Annuler, ce qui vous permet de continuer sans spécifier de valeur ou de revenir au champ pour entrer une valeur.

Pour plus d’informations sur un test null, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Boutons de formulaire {#form-buttons}

Le fait de cliquer sur un bouton d’envoi envoie des données de formulaire au service Forms et représente la fin du traitement du formulaire. Le `preSubmit` événement peut être configuré pour s’exécuter sur le client ou le serveur. Le `preSubmit` événement s’exécute avant l’envoi du formulaire s’il est configuré pour s’exécuter sur le client. Sinon, le `preSubmit` événement s’exécute sur le serveur pendant l’envoi du formulaire. Pour plus d’informations sur le `preSubmit` événement, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Si aucun script client n’est associé à un bouton, les données sont envoyées au serveur, les calculs sont effectués sur le serveur et le formulaire HTML est régénéré. Si un bouton contient un script client, les données ne sont pas envoyées au serveur et le script client est exécuté dans le navigateur Web.

## Navigateur Web HTML 4.0 {#html-4-0-web-browser}

Un navigateur Web qui ne prend en charge que HTML 4.0 ne peut pas prendre en charge le modèle de script côté client du sous-ensemble XFA. Lors de la création d’une conception de formulaire compatible avec HTML 4.0 et MSDHTML ou CSS2HTML, un script marqué pour s’exécuter sur le client s’exécute sur le serveur. Supposons, par exemple, qu’un utilisateur clique sur un bouton situé sur un formulaire affiché dans un navigateur Web HTML 4.0. Dans ce cas, les données de formulaire sont envoyées au serveur sur lequel le script client est exécuté.

Il est recommandé de placer la logique de formulaire dans les événements de calcul, qui s’exécutent sur le serveur dans HTML 4.0 et sur le client pour MSDHTML ou CSS2HTML.

## Maintenance des modifications de présentation {#maintaining-presentation-changes}

Lorsque vous vous déplacez entre des pages HTML (panneaux), seul l’état des données est conservé. Les paramètres tels que la couleur d’arrière-plan ou les paramètres de champ obligatoire ne sont pas conservés (s’ils diffèrent des paramètres initiaux). Pour conserver l’état de présentation, vous devez créer des champs (généralement masqués) qui représentent l’état de présentation des champs. Si vous ajoutez un script au `Calculate` événement d’un champ qui modifie la présentation en fonction des valeurs de champ masqué, vous pouvez conserver l’état de la présentation lorsque vous passez d’une page HTML à l’autre (panneaux).

Le script suivant conserve la valeur `fillColor` d’un champ en fonction de la valeur de `hiddenField`. Supposons que ce script se trouve dans le `Calculate` événement d’un champ.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Les objets statiques ne s’affichent pas dans un formulaire HTML rendu lorsqu’ils sont imbriqués dans une cellule de tableau. Par exemple, un cercle et un rectangle imbriqués dans une cellule de tableau ne s’affichent pas dans un formulaire HTML de rendu. Cependant, ces mêmes objets statiques s’affichent correctement lorsqu’ils sont situés en dehors du tableau.

## Signature numérique de formulaires HTML {#digitally-signing-html-forms}

Vous ne pouvez pas signer un formulaire HTML qui contient un champ de signature numérique si le formulaire est généré comme l’une des transformations HTML suivantes :

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Pour plus d’informations sur la signature numérique d’un document, voir Signature [numérique et certification de Documents.](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendu d’un formulaire XHTML compatible avec les consignes d’accessibilité {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Vous pouvez générer un formulaire HTML complet conforme aux directives d’accessibilité. En d’autres termes, le formulaire est généré dans des balises HTML complètes, contrairement au formulaire HTML généré dans des balises body (et non dans une page HTML complète).

## Validation des données de formulaire {#validating-form-data}

Il est recommandé de limiter l’utilisation des règles de validation pour les champs de formulaire lors du rendu du formulaire au format HTML. Certaines règles de validation peuvent ne pas être prises en charge pour les formulaires HTML. Par exemple, lorsqu’un modèle de validation MM-JJ-AAAA est appliqué à un `Date/Time` champ situé dans une conception de formulaire rendue en tant que formulaire HTML, il ne fonctionne pas correctement, même si la date est correctement saisie. Cependant, ce modèle de validation fonctionne correctement pour les formulaires rendus au format PDF.

>[!NOTE]
For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API du client Forms.
1. Définissez les options d’exécution HTML.
1. Générer un formulaire HTML.
1. Ecrivez le flux de données du formulaire dans le navigateur Web client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet API du client Forms**

Avant de pouvoir importer des données par programmation dans une API FormsClient PDF, vous devez créer un client du service d’intégration des données de formulaire. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Définition des options d’exécution HTML**

Vous définissez les options d’exécution HTML lors du rendu d’un formulaire HTML. Par exemple, vous pouvez ajouter une barre d’outils à un formulaire HTML pour permettre aux utilisateurs de sélectionner des pièces jointes situées sur l’ordinateur client ou de récupérer les pièces jointes générées avec le formulaire HTML. Par défaut, une barre d’outils HTML est désactivée. Pour ajouter une barre d’outils à un formulaire HTML, vous devez configurer par programmation les options d’exécution. Par défaut, une barre d’outils HTML se compose des boutons suivants :

* `Home`: Fournit un lien vers la racine Web de l’application.
* `Upload`: Fournit une interface utilisateur permettant de sélectionner les fichiers à joindre au formulaire actif.
* `Download`: Fournit une interface utilisateur pour afficher les fichiers joints.

Lorsqu’une barre d’outils HTML s’affiche sur un formulaire HTML, un utilisateur peut sélectionner un maximum de dix fichiers à envoyer avec les données de formulaire. Une fois les fichiers envoyés, le service Forms peut récupérer les fichiers.

Lors du rendu d’un formulaire au format HTML, vous pouvez spécifier une valeur d’agent utilisateur. Une valeur user-agent fournit des informations sur le navigateur et le système. Il s’agit d’une valeur facultative et vous pouvez transmettre une valeur de chaîne vide. Le début rapide Rendu d’un formulaire HTML à l’aide de l’API Java montre comment obtenir une valeur d’agent utilisateur et l’utiliser pour générer un formulaire au format HTML.

Les URL HTTP vers l’emplacement de publication des données du formulaire peuvent être spécifiées en définissant l’URL de cible à l’aide de l’API du client Forms Service ou peuvent être spécifiées dans le bouton Envoyer contenu dans la conception de formulaire XDP. Si l’URL de la cible est spécifiée dans la conception de formulaire, ne définissez pas de valeur à l’aide de l’API du client Forms Service.

>[!NOTE]
Le rendu d’un formulaire HTML avec une barre d’outils est facultatif.

>[!NOTE]
Si vous générez un formulaire AHTML, il est recommandé de ne pas ajouter de barre d’outils au formulaire.

**Génération d’un formulaire HTML**

Pour générer un formulaire HTML, vous devez spécifier une conception de formulaire créée dans Designer et enregistrée dans un fichier XDP. Vous devez également sélectionner un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un fichier HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML requiert également des valeurs, telles que des valeurs URI, requises pour effectuer le rendu d’autres types de formulaire.

**Ecrire le flux de données du formulaire dans le navigateur Web client**

Lorsque le service Forms génère un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur Web client. Lorsqu’il est écrit dans le navigateur Web client, le formulaire HTML est visible pour l’utilisateur.

**Voir également**

[Générer un formulaire au format HTML à l’aide de l’API Java](#render-a-form-as-html-using-the-java-api)

[Générer un formulaire au format HTML à l’aide de l’API du service Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendu de formulaires HTML avec des barres d’outils personnalisées](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Création d’Applications web renvoyant des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Générer un formulaire au format HTML à l’aide de l’API Java {#render-a-form-as-html-using-the-java-api}

Générer un formulaire HTML à l’aide de l’API Forms (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API du client Forms

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Définition des options d’exécution HTML

   * Create an `HTMLRenderSpec` object by using its constructor.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la `HTMLRenderSpec` méthode de l’objet et transmettez une valeur `setHTMLToolbar` `HTMLToolbar` d’énumération. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir la valeur des paramètres régionaux du formulaire HTML, appelez la `HTMLRenderSpec` `setLocale` méthode de l’objet et transmettez une valeur de chaîne qui spécifie la valeur des paramètres régionaux. (Ce paramètre est facultatif.)
   * Pour effectuer le rendu du formulaire HTML au sein de balises HTML complètes, appelez la `HTMLRenderSpec` méthode de l’objet et transmettez `setOutputType` `OutputType.FullHTMLTags`. (Ce paramètre est facultatif.)

   >[!NOTE]
   Les formulaires ne sont pas rendus correctement dans le code HTML lorsque l’ `StandAlone` option est `true` sélectionnée et que le `ApplicationWebRoot` serveur fait référence à un serveur autre que le serveur d’applications J2EE hébergeant des AEM Forms (la `ApplicationWebRoot` valeur est spécifiée à l’aide de l’ `URLSpec` objet transmis à la `FormsServiceClient` méthode de l’ `(Deprecated) renderHTMLForm` objet). Lorsqu’il `ApplicationWebRoot` s’agit d’un autre serveur provenant d’un AEM Forms hôte, la valeur de l’URI racine Web dans Administration Console doit être définie en tant que valeur de l’URI de l’application Web du formulaire. Pour ce faire, connectez-vous à Administration Console, cliquez sur Services > Forms et définissez l’URI racine Web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Génération d’un formulaire HTML

   Appelez la méthode `FormsServiceClient` de l’ `(Deprecated) renderHTMLForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` d’énumération qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` qui stocke les valeurs URI nécessaires au rendu d’un formulaire HTML.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La `(Deprecated) renderHTMLForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire pouvant être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la `InputStream` `read` méthode de l’objet et en transmettant le tableau d’octets en tant qu’argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu des formulaires au format HTML](#rendering-forms-as-html)

[Début rapide (mode SOAP) : Rendu d’un formulaire HTML à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Générer un formulaire au format HTML à l’aide de l’API du service Web {#render-a-form-as-html-using-the-web-service-api}

Générer un formulaire HTML à l’aide de l’API Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez des classes de proxy Java qui utilisent le WSDL du service Forms.
   * Incluez les classes proxy Java dans votre chemin de classe.

1. Création d’un objet API du client Forms

   Créez un `FormsService` objet et définissez des valeurs d’authentification.

1. Définition des options d’exécution HTML

   * Create an `HTMLRenderSpec` object by using its constructor.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la `HTMLRenderSpec` méthode de l’objet et transmettez une valeur `setHTMLToolbar` `HTMLToolbar` d’énumération. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir la valeur des paramètres régionaux du formulaire HTML, appelez la `HTMLRenderSpec` `setLocale` méthode de l’objet et transmettez une valeur de chaîne qui spécifie la valeur des paramètres régionaux. For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Pour effectuer le rendu du formulaire HTML au sein de balises HTML complètes, appelez la `HTMLRenderSpec` méthode de l’objet et transmettez `setOutputType` `OutputType.FullHTMLTags`.

   >[!NOTE]
   Les formulaires ne sont pas rendus correctement dans le code HTML lorsque l’ `StandAlone` option est `true` sélectionnée et que le `ApplicationWebRoot` serveur fait référence à un serveur autre que le serveur d’applications J2EE hébergeant des AEM Forms (la `ApplicationWebRoot` valeur est spécifiée à l’aide de l’ `URLSpec` objet transmis à la `FormsServiceClient` méthode de l’ `(Deprecated) renderHTMLForm` objet). Lorsqu’il `ApplicationWebRoot` s’agit d’un autre serveur provenant d’un AEM Forms hôte, la valeur de l’URI racine Web dans Administration Console doit être définie en tant que valeur de l’URI de l’application Web du formulaire. Pour ce faire, connectez-vous à Administration Console, cliquez sur Services > Forms et définissez l’URI racine Web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Génération d’un formulaire HTML

   Appelez la méthode `FormsService` de l’ `(Deprecated) renderHTMLForm` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin d’accès complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valeur `TransformTo` d’énumération qui spécifie le type de préférence HTML. Par exemple, pour générer un formulaire HTML compatible avec le code HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`. (Voir [Préremplissage de formulaires avec des dispositions](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)à disposition souple.)
   * Objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Valeur de chaîne qui spécifie la valeur d’ `HTTP_USER_AGENT` en-tête ; par exemple, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` qui stocke les valeurs URI nécessaires au rendu d’un formulaire HTML. (voir [Spécification des valeurs](/help/forms/developing/rendering-interactive-pdf-forms.md)URI).
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire. (Voir [Joindre des fichiers au formulaire](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` rempli par la méthode. Cette valeur de paramètre stocke le formulaire rendu.
   * Objet vide `com.adobe.idp.services.holders.BLOBHolder` rempli par la méthode. Ce paramètre stocke les données XML de sortie.
   * Objet vide `javax.xml.rpc.holders.LongHolder` rempli par la méthode. Cet argument stocke le nombre de pages dans le formulaire.
   * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode. Cet argument stocke la valeur du paramètre régional.
   * Objet vide `javax.xml.rpc.holders.StringHolder` rempli par la méthode. Cet argument stocke la valeur de rendu HTML utilisée.
   * Objet vide `com.adobe.idp.services.holders.FormsResultHolder` qui contiendra les résultats de cette opération.

   La `(Deprecated) renderHTMLForm` méthode remplit l’ `com.adobe.idp.services.holders.FormsResultHolder` objet transmis en tant que valeur du dernier argument avec un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Ecrire le flux de données du formulaire dans le navigateur Web client

   * Créez un `FormResult` objet en obtenant la valeur du membre `com.adobe.idp.services.holders.FormsResultHolder` de données de l’ `value` objet.
   * Créez un `BLOB` objet contenant des données de formulaire en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `BLOB` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `BLOB` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un tableau d’octets et remplissez-le en appelant la `BLOB` `getBinaryData` méthode de l’objet. Cette tâche affecte le contenu de l’ `FormsResult` objet au tableau d’octets.
   * Appelez la méthode `javax.servlet.http.HttpServletResponse` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir également**

[Rendu des formulaires au format HTML](#rendering-forms-as-html)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

