---
title: Effectuer le rendu de formulaires en HTML
description: Utilisez le service Forms pour effectuer le rendu des formulaires en format HTML en réponse à une requête HTTP d’un navigateur web. Vous pouvez utiliser l’API Java™ et l’API de service web pour effectuer le rendu des formulaires au format HTML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '4099'
ht-degree: 100%

---

# Effectuer le rendu de formulaires en HTML {#rendering-forms-as-html}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le service Forms effectue le rendu des formulaires en format HTML en réponse à une requête HTTP d’un navigateur web. L’un des avantages du rendu d’un formulaire en format HTML réside dans le fait que l’ordinateur sur lequel se trouve le navigateur web client n’a pas besoin d’avoir Adobe Reader, Acrobat ou Flash Player (pour les guides de formulaire (obsolète)).

Pour générer un formulaire en format HTML, la conception de formulaire doit être enregistrée en tant que fichier XDP. Une conception de formulaire enregistrée en tant que fichier PDF ne peut pas être générée en tant que HTML. Lors du développement d’une conception de formulaire dans Designer qui sera rendue en format HTML, tenez compte des critères suivants :

* N’utilisez pas les propriétés de bordure d’un objet pour tracer des lignes, des zones ou des grilles dans un formulaire. Certains navigateurs n’alignent pas les bordures exactement comme elles sont présentées dans un aperçu de Les objets risquent de se chevaucher ou de déplacer d’autres objets de manière imprévue.
* Vous pouvez utiliser des lignes, des rectangles et des cercles pour définir l’arrière-plan.
* Créez des objets de texte un peu plus grands que nécessaire pour accueillir le texte. Certains navigateurs web n’affichent pas le texte de manière lisible.

>[!NOTE]
>
>Lors du rendu d’un formulaire contenant des images TIFF à l’aide des méthodes `(Deprecated) renderHTMLForm` et `renderHTMLForm2` de l’objet `FormServiceClient`, les images TIFF ne sont pas visibles dans le formulaire HTML rendu affiché dans les navigateurs Internet Explorer ou Mozilla Firefox. Ces navigateurs ne fournissent pas de prise en charge native des images TIFF.

## Pages HTML {#html-pages}

Lorsqu’une conception de formulaire est générée sous forme de formulaire HTML, chaque sous-formulaire de second niveau est généré sous forme de page HTML (panneau). Vous pouvez afficher la hiérarchie d’un sous-formulaire dans Designer. Les sous-formulaires enfants appartenant au sous-formulaire racine (le nom par défaut d’un sous-formulaire racine est form1) sont les sous-formulaires de panneau. L’exemple suivant illustre les sous-formulaires d’une conception de formulaire.

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

Lorsque les conceptions de formulaire sont générées sous forme de formulaires HTML, les panneaux ne sont pas limités à une taille de page particulière. Si vous disposez de sous-formulaires dynamiques, ils doivent être imbriqués dans le sous-formulaire de panneau. Les sous-formulaires dynamiques peuvent s’étendre sur un nombre infini de pages HTML.

Lorsqu’un formulaire est rendu en format HTML, les formats de page (requis pour paginer les formulaires rendus en PDF) n’ont aucune signification. Étant donné qu’un formulaire avec disposition fluide peut atteindre un nombre infini de pages HTML, il est important d’éviter les pieds de page sur le gabarit. Un pied de page situé sous la zone de contenu d’un gabarit peut remplacer le contenu HTML qui s’étend au-delà d’une limite de page.

Vous devez explicitement passer d’un panneau à l’autre à l’aide des méthodes `xfa.host.pageUp` et `xfa.host.pageDown`. Vous pouvez modifier les pages en envoyant un formulaire au service Forms et en demandant au service Forms de le rendre à nouveau sur l’appareil client, généralement un navigateur web.

>[!NOTE]
>
>Le processus d’envoi d’un formulaire au service Forms, puis de renvoi du formulaire par le service Forms vers l’appareil client est appelé données de basculement arrondies vers le serveur.

>[!NOTE]
>
>Si vous souhaitez personnaliser l’aspect du bouton Signature numérique HTML sur un formulaire HTML, vous devez modifier les propriétés suivantes dans le fichier fscdigsig.css (dans le fichier adobe-forms-ds.ear > adobe-forms-ds.war) :

**`.fsc-ds-ssb`** : cette feuille de style s’applique en cas de champ de signature vide.

**`.fsc-ds-ssv`** : cette feuille de style s’applique en cas de champ de signature valide.

**`.fsc-ds-ssc`** : cette feuille de style s’applique en cas de champ de signature valide, mais dont les données ont été modifiées.

**`.fsc-ds-ssi`** : cette feuille de style s’applique en cas de champ de signature non valide.

**`.fsc-ds-popup-bg`** : cette propriété de feuille de style n’est pas utilisée.

**.`fsc-ds-popup-btn`** : cette propriété de feuille de style n’est pas utilisée.

## Exécuter des scripts {#running-scripts}

Un auteur de formulaire indique si un script s’exécute sur le serveur ou sur le client. Le service Forms crée un environnement de traitement des événements distribué pour l’exécution des renseignements sur les formulaires qui peuvent être distribués entre le client et le serveur à l’aide de l’attribut `runAt`. Pour plus d’informations sur cet attribut ou la création de scripts dans les conceptions de formulaire, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr)

Le service Forms peut exécuter des scripts pendant la génération du formulaire. Par conséquent, vous pouvez préremplir un formulaire avec des données en vous connectant à une base de données ou à des services web qui pourraient ne pas être disponibles côté client. Vous pouvez également définir un événement `Click` de bouton à exécuter sur le serveur afin que le client puisse envoyer et reprendre des données au serveur. Cela permet au client d’exécuter des scripts qui peuvent nécessiter des ressources serveur, telles qu’une base de données d’entreprise, lorsqu’un utilisateur interagit avec un formulaire. Pour les formulaires HTML, les scripts formcalc ne peuvent être exécutés que sur le serveur. Par conséquent, vous devez marquer ces scripts pour qu’ils s’exécutent sur `server` ou `both`.

Vous pouvez concevoir des formulaires qui se déplacent entre les pages (panneaux) en appelant les méthodes `xfa.host.pageUp` et `xfa.host.pageDown`. Ce script est placé dans l’événement `Click` du bouton et l’attribut `runAt` est défini sur `Both`. Le motif de votre choix de `Both` permet à Adobe Reader ou Acrobat (pour les formulaires rendus en format PDF) de modifier les pages sans passer par le serveur et les formulaires HTML peuvent modifier les pages en envoyant et en reprenant les données au serveur. En d’autres termes, un formulaire est envoyé au service Forms et un formulaire est rendu en format HTML avec la nouvelle page affichée.

Il est recommandé de ne pas donner les mêmes noms aux variables de script et aux champs de formulaire, par exemple élément. Certains navigateurs web, tels qu’Internet Explorer, peuvent ne pas initialiser une variable portant le même nom qu’un champ de formulaire, ce qui entraîne une erreur de script. Une bonne pratique consiste à donner des noms différents aux champs de formulaire et aux variables de script.

Lors du rendu de formulaires HTML qui contiennent à la fois des fonctionnalités de navigation de page et des scripts de formulaire (supposons, par exemple, qu’un script récupère les données de champ d’une base de données chaque fois que le formulaire est rendu), assurez-vous que le script de formulaire se trouve dans l’événement form:calculate au lieu de form:readyevent.

Les scripts de formulaire situés dans l’événement form:ready ne sont exécutés qu’une seule fois lors du rendu initial du formulaire et ne sont pas exécutés pour les récupérations de page suivantes. En revanche, l’événement form:calculate est exécuté pour chaque navigation de page dans laquelle le formulaire est rendu.

>[!NOTE]
>
Dans un formulaire de plusieurs pages, les modifications apportées par JavaScript à une page ne sont pas conservées si vous passez à une autre page.

Vous pouvez appeler des scripts personnalisés avant d’envoyer un formulaire. Cette fonctionnalité fonctionne sur tous les navigateurs disponibles. Cependant, elle ne peut être utilisée que lorsque les utilisateurs effectuent le rendu du formulaire HTML dont la propriété `Output Type` est définie sur `Form Body`. Cela ne fonctionne pas lorsque la propriété `Output Type` est définie sur `Full HTML`. Pour connaître les étapes de configuration de cette fonctionnalité, consultez la section Configurer des formulaires dans l’aide d’administration.

Définissez d’abord une fonction de rappel appelée avant l’envoi du formulaire, où le nom de la fonction est `_user_onsubmit`. On suppose que la fonction ne renvoie aucune exception ou que, dans ce cas, l’exception est ignorée. Il est recommandé de placer la fonction JavaScript dans la section HEAD du fichier HTML. Vous pouvez toutefois la déclarer n’importe où avant la fin des balises de script qui incluent `xfasubset.js`.

Lorsque le serveur de formulaires effectue le rendu d’un fichier XDP contenant une liste déroulante, il crée deux champs de texte masqués en plus de créer la liste déroulante. Ces champs de texte stockent les données de la liste déroulante (l’un stocke le nom d’affichage des options et l’autre stocke la valeur des options). Par conséquent, chaque fois qu’un utilisateur ou une utilisatrice envoie le formulaire, toutes les données de la liste déroulante sont envoyées. Supposons que vous ne souhaitiez pas envoyer autant de données à chaque fois. Vous pouvez alors écrire un script personnalisé permettant de désactiver cela. Par exemple : le nom de la liste déroulante est `drpOrderedByStateProv`. Il est encapsulé dans l’en-tête de sous-formulaire. Le nom de l’élément d’entrée HTML est `header[0].drpOrderedByStateProv[0]`. Les noms des champs masqués qui stockent et envoient les données de la liste déroulante sont les suivants : `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`.

Vous pouvez suivre la procédure suivante pour désactiver ces éléments d’entrée si vous ne souhaitez pas publier les données. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

Lors de la création de conceptions de formulaire pour le rendu HTML, vous devez limiter votre script au sous-ensemble XFA pour les scripts en langage JavaScript.

Les scripts qui s’exécutent sur le client ou à la fois sur le client et le serveur doivent être écrits dans le sous-ensemble XFA. Les scripts qui s’exécutent sur le serveur peuvent utiliser le modèle de script XFA complet ainsi que FormCalc. Pour plus d’informations sur l’utilisation de JavaScript, voir [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

Lors de l’exécution de scripts côté client, seul le panneau actuellement affiché peut utiliser le script. Par exemple, vous ne pouvez pas utiliser de script pour les champs situés dans le panneau A lorsque le panneau B est affiché. Lors de l’exécution de scripts sur le serveur, tous les panneaux sont accessibles.

Faites attention lorsque vous utilisez des expressions de modèle d’objet de script (SOM) dans des scripts exécutés côté client. Seul un sous-ensemble simplifié d’expressions SOM est pris en charge par les scripts qui s’exécutent sur le client.

## Durée d’événement {#event-timing}

Le sous-ensemble XFA définit les événements XFA mappés aux événements HTML. Il existe une légère différence de comportement dans la durée des événements de calcul et de validation. Dans un navigateur web, un événement de calcul complet est exécuté lorsque vous quittez un champ. Les événements de calcul ne s’exécutent pas automatiquement lorsque vous modifiez une valeur de champ. Vous pouvez forcer un événement de calcul en appelant la méthode `xfa.form.execCalculate`.

Dans un navigateur web, les événements de validation ne s’exécutent que lors de la sortie d’un champ ou de l’envoi d’un formulaire. Vous pouvez forcer un événement de validation à l’aide de la méthode `xfa.form.execValidate`.

Les formulaires affichés dans un navigateur web (par opposition à Adobe Reader ou Acrobat) sont conformes au test Null XFA (erreurs ou avertissements) pour les champs obligatoires.

* Si le test Null génère une erreur et que vous quittez un champ sans spécifier de valeur, une zone de message s’affiche et vous êtes repositionné dans le champ après avoir cliqué sur OK.
* Si un test Null génère un avertissement et que vous quittez un champ sans spécifier de valeur, vous êtes invité à cliquer sur OK ou Annuler, ce qui vous donne la possibilité de continuer sans spécifier de valeur ou de revenir au champ pour saisir une valeur.

Pour plus d’informations sur le test Null, consultez la section [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

## Boutons de formulaire {#form-buttons}

Cliquer sur un bouton Envoyer envoie les données de formulaire au service Forms et représente la fin du traitement du formulaire. L’événement `preSubmit` peut être configuré pour s’exécuter sur le client ou le serveur. L’événement `preSubmit` s’exécute avant l’envoi du formulaire s’il est configuré pour s’exécuter sur le client. Dans le cas contraire, l’événement `preSubmit` s’exécute sur le serveur pendant l’envoi du formulaire. Pour plus d’informations sur l’événement `preSubmit`, consultez la section [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).

Si aucun script côté client n’est associé à un bouton, les données sont envoyées au serveur, les calculs sont effectués sur le serveur et le formulaire HTML est généré de nouveau. Si un bouton contient un script côté client, les données ne sont pas envoyées au serveur et le script côté client est exécuté dans le navigateur web.

## Navigateur web HTML 4.0 {#html-4-0-web-browser}

Un navigateur web qui ne prend en charge que le HTML 4.0 ne peut pas prendre en charge le modèle de script du sous-ensemble XFA côté client. Lors de la création d’une conception de formulaire devant fonctionner en HTML 4.0 et MSDHTML ou CSS2HTML, un script marqué comme devant s’exécuter sur un client s’exécute sur le serveur. Supposons, par exemple, qu’un utilisateur clique sur un bouton situé sur un formulaire affiché dans un navigateur web HTML 4.0. Dans ce cas, les données de formulaire sont envoyées au serveur sur lequel le script côté client est exécuté.

Il est recommandé de placer votre logique de formulaire dans les événements de calcul, qui s’exécutent sur le serveur en HTML 4.0 et sur le client pour HTML MSDHTML ou CSS2HTML.

## Conserver les modifications de présentation {#maintaining-presentation-changes}

Lorsque vous passez d’une page HTML à l’autre (panneaux), seul l’état des données est conservé. Les paramètres tels que la couleur d’arrière-plan ou les paramètres de champ obligatoires ne sont pas conservés (s’ils sont différents des paramètres initiaux). Pour conserver l’état de présentation, vous devez créer des champs (généralement masqués) qui représentent l’état de présentation des champs. Si vous ajoutez un script à l’événement `Calculate` d’un champ qui modifie la présentation en fonction des valeurs de champ masquées, vous pouvez conserver l’état de présentation lorsque vous passez d’une page HTML à l’autre (panneaux).

Le script suivant conserve la fonction `fillColor` d’un champ en fonction de la valeur de `hiddenField`. Supposons que ce script se trouve dans l’événement `Calculate` d’un champ.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
>
Les objets statiques ne s’affichent pas dans un formulaire HTML généré lorsqu’ils sont imbriqués dans la cellule d’un tableau. Par exemple, un cercle et un rectangle imbriqués dans une cellule de tableau ne s’affichent pas dans un formulaire HTML de rendu. Toutefois, ces mêmes objets statiques s’affichent correctement lorsqu’ils sont situés en dehors du tableau.

## Signature numérique de formulaires HTML {#digitally-signing-html-forms}

Vous ne pouvez pas signer un formulaire HTML contenant un champ de signature numérique si le formulaire est généré comme l’une des transformations HTML suivantes :

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

Pour plus d’informations à propos de la signature numérique d’un document, voir [Signature numérique et certification de documents](/help/forms/developing/digitally-signing-certifying-documents.md)

## Rendre un formulaire XHTML conforme aux directives d’accessibilité {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Vous pouvez générer un formulaire HTML complet conforme aux directives d’accessibilité. En d’autres termes, le formulaire est généré avec des balises HTML complètes, contrairement au formulaire HTML généré avec des balises body (page HTML incomplète).

## Valider des données de formulaire {#validating-form-data}

Il est recommandé de limiter l’utilisation des règles de validation pour les champs de formulaire lors du rendu du formulaire en tant que formulaire HTML. Certaines règles de validation peuvent ne pas être prises en charge pour les formulaires HTML. Par exemple, lorsqu’un modèle de validation MM-JJ-AAAA est appliqué à un champ `Date/Time` qui se trouve dans une conception de formulaire générée sous la forme HTML, il ne fonctionne pas correctement, même si la date est saisie correctement. Cependant, ce modèle de validation fonctionne correctement pour les formulaires générés en tant que PDF.

>[!NOTE]
>
Pour plus d’informations à propos du service Forms, voir [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour générer un formulaire HTML, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Forms.
1. Définissez les options d’exécution HTML.
1. Effectuez le rendu d’un formulaire HTML.
1. Écrivez le flux de données du formulaire dans le navigateur web du client.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un objet API client Forms**

Avant de pouvoir importer des données par programmation dans une API formClient PDF, vous devez créer un client de service Form Data Integration. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service.

**Définir les options d’exécution HTML**

Vous définissez les options d’exécution HTML lors de la génération d’un formulaire HTML. Par exemple, vous pouvez ajouter une barre d’outils à un formulaire HTML pour permettre aux utilisateurs de sélectionner les pièces jointes situées sur l’ordinateur client ou de récupérer les pièces jointes générées avec le formulaire HTML. Par défaut, une barre d’outils HTML est désactivée. Pour ajouter une barre d’outils à un formulaire HTML, vous devez définir par programmation les options d’exécution. Par défaut, une barre d’outils HTML se compose des boutons suivants :

* `Home` : fournit un lien vers la racine web de l’application.
* `Upload` : fournit une interface utilisateur pour sélectionner les fichiers à joindre au formulaire actif.
* `Download` : fournit une interface utilisateur pour afficher les fichiers joints.

Lorsqu’une barre d’outils HTML s’affiche sur un formulaire HTML, l’utilisateur ou l’utilisatrice peut sélectionner un maximum de dix fichiers à envoyer avec les données de formulaire. Une fois les fichiers envoyés, le service Forms peut les récupérer.

Lors du rendu d’un formulaire en tant que HTML, vous pouvez spécifier une valeur agent-utilisateur. Une valeur agent-utilisateur fournit des informations sur le navigateur et le système. Il s’agit d’une valeur facultative que vous pouvez transmettre à une valeur de chaîne vide. Le rendu d’un formulaire au format HTML à l’aide du démarrage rapide de l’API Java indique comment obtenir une valeur d’agent utilisateur et s’en servir pour générer un formulaire au format HTML.

Les URL HTTP où les données du formulaire sont envoyées peuvent être spécifiées en définissant l’URL cible à l’aide de l’API client du service Forms ou peuvent être spécifiées dans le bouton Envoyer contenu dans la conception de formulaire XDP. Si l’URL cible est spécifiée dans la conception de formulaire, ne définissez pas de valeur à l’aide de l’API client du service Forms.

>[!NOTE]
>
Le rendu d’un formulaire de HTML avec une barre d’outils est facultatif.

>[!NOTE]
>
Si vous générez un formulaire AHTML, il est recommandé de ne pas ajouter de barre d’outils au formulaire.

**Rendre un formulaire au format HTML**

Pour effectuer le rendu d’un formulaire HTML, spécifiez une conception de formulaire qui a été créée dans Designer et enregistrée en tant que fichier XDP. Sélectionnez un type de transformation HTML. Par exemple, vous pouvez spécifier le type de transformation HTML qui effectue le rendu d’un HTML dynamique pour Internet Explorer 5.0 ou version ultérieure.

Le rendu d’un formulaire HTML nécessite également des valeurs, telles que des valeurs URI requises pour effectuer le rendu d’autres types de formulaire.

**Écrire le flux de données de formulaire dans le navigateur web client**

Lorsque le service Forms génère un formulaire HTML, il renvoie un flux de données de formulaire que vous devez écrire dans le navigateur web client. Lorsqu’il est écrit dans le navigateur web client, le formulaire HTML est visible par l’utilisateur.

**Voir également**

[Rendre un formulaire au format HTML à l’aide de l’API Java](#render-a-form-as-html-using-the-java-api)

[Rendre un formulaire au format HTML à l’aide de l’API Web Service](#render-a-form-as-html-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Effectuer le rendu des formulaires HTML avec des barres d’outils personnalisées](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

## Rendre un formulaire au format HTML à l’aide de l’API Java {#render-a-form-as-html-using-the-java-api}

Renvoyez un formulaire au format HTML à l’aide de l’API Forms (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre chemin de classe de projet Java.

1. Créer un objet API Forms client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Définir les options d’exécution HTML

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir les paramètres régionaux HTML, appelez la méthode `setLocale` de l’objet `HTMLRenderSpec` et transmettez une valeur de chaîne qui spécifie les paramètres régionaux. (Ce paramétrage est facultatif.)
   * Pour effectuer le rendu du formulaire HTML dans des balises HTML complètes, appelez la méthode `setOutputType` de l’objet `HTMLRenderSpec` et transmettez `OutputType.FullHTMLTags`. (Ce paramétrage est facultatif.)

   >[!NOTE]
   >
   Les formulaires ne s’affichent pas correctement au format HTML lorsque l’option `StandAlone` est `true` et le `ApplicationWebRoot` référence un serveur autre que le serveur d’applications J2EE hébergeant les formulaires AEM (la valeur `ApplicationWebRoot` est spécifiée à l’aide de l’objet `URLSpec` qui est transmis à la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient`). Lorsque `ApplicationWebRoot` est un serveur autre que celui qui héberge AEM Forms, la valeur de l’URI racine web dans la console d’administration doit être définie comme valeur de l’URI de l’application web du formulaire. Pour ce faire, connectez-vous à la console d’administration, cliquez sur Services > Forms, puis définissez l’URI racine web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Effectuer le rendu d’un formulaire HTML

   Appelez la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document`.
   * L’objet `HTMLRenderSpec` qui stocke les options d’exécution HTML.
   * Une valeur string qui spécifie la valeur d’en-tête `HTTP_USER_AGENT`, par exemple `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Objet `URLSpec` stockant les valeurs URI requises pour générer un formulaire au format HTML.
   * Objet `java.util.HashMap` stockant les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `(Deprecated) renderHTMLForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire pouvant être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données du formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Effectuer le rendu de formulaires en HTML](#rendering-forms-as-html)

[Démarrage rapide (mode SOAP) : générer un formulaire HTML à l’aide de l’API Java.](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendu d’un formulaire en tant que HTML à l’aide de l’API Web Service {#render-a-form-as-html-using-the-web-service-api}

Générez un formulaire HTML à l’aide de l’API Forms (Web Service) :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le service WSDL de Forms.
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer un objet API Forms client

   Créez un objet `FormsService` et définissez les valeurs d’authentification.

1. Définir les options d’exécution HTML

   * Créez un objet `HTMLRenderSpec` en utilisant son constructeur.
   * Pour générer un formulaire HTML avec une barre d’outils, appelez la méthode `setHTMLToolbar` de l’objet `HTMLRenderSpec` et transmettez une valeur d’énumération `HTMLToolbar`. Par exemple, pour afficher une barre d’outils HTML verticale, transmettez `HTMLToolbar.Vertical`.
   * Pour définir les paramètres régionaux HTML, appelez la méthode `setLocale` de l’objet `HTMLRenderSpec` et transmettez une valeur de chaîne qui spécifie les paramètres régionaux. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Pour générer le formulaire HTML avec des balises HTML complètes, appelez la méthode `setOutputType` de l’objet `HTMLRenderSpec` et transmettez `OutputType.FullHTMLTags`.

   >[!NOTE]
   >
   Les formulaires ne sont générés correctement en HTML lorsque l’option `StandAlone` est `true` et que `ApplicationWebRoot` référence un serveur autre que le serveur d’applications J2EE hébergeant AEM Forms (la valeur `ApplicationWebRoot` est spécifiée à l’aide de l’objet `URLSpec` qui est transmis à la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsServiceClient`). Lorsque `ApplicationWebRoot` est un serveur autre que celui qui héberge AEM Forms, la valeur de l’URI racine web dans la console d’administration doit être définie comme valeur de l’URI de l’application web du formulaire. Pour ce faire, connectez-vous à la console d’administration, cliquez sur Services > Forms, puis définissez l’URI racine web sur https://server-name:port/FormServer. Enregistrez ensuite vos paramètres.

1. Effectuer le rendu d’un formulaire HTML

   Appelez la méthode `(Deprecated) renderHTMLForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Valeur string spécifiant le nom du modèle de formulaire, y compris l’extension du nom du fichier. Si vous référencez une conception de formulaire faisant partie d’une application Forms, veillez à spécifier le chemin complet, tel que `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Une valeur d’énumération `TransformTo` spécifiant le type de préférence HTML. Par exemple, pour effectuer le rendu d’un formulaire HTML compatible avec le HTML dynamique pour Internet Explorer 5.0 ou version ultérieure, spécifiez `TransformTo.MSDHTML`.
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez `null`. (Voir [Préremplir des formulaires avec des mises en page modulables](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * Objet `HTMLRenderSpec` stockant les options d’exécution HTML.
   * Valeur de chaîne spécifiant la valeur d’en-tête `HTTP_USER_AGENT`, par exemple `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Vous pouvez transmettre une chaîne vide si vous ne souhaitez pas définir cette valeur.
   * Objet `URLSpec` stockant les valeurs URI requises pour générer un formulaire HTML. (Voir [Spécifier des valeurs URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objet `java.util.HashMap` stockant les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire. (Voir [Joindre des fichiers au formulaire](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. La valeur de ce paramètre enregistre le formulaire rendu.
   * Objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Ce paramètre stocke les données XML de sortie.
   * Objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. Cet argument stocke le nombre de pages dans le formulaire.
   * Objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. Cet argument stocke la valeur des paramètres régionaux.
   * Objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. Cet argument stocke la valeur de rendu HTML utilisée.
   * Objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contient les résultats de cette opération.

   La méthode `(Deprecated) renderHTMLForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

1. Écrire le flux de données de formulaire dans le navigateur web client

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` qui contient les données du formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données du formulaire vers le navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Effectuer le rendu de formulaires en HTML](#rendering-forms-as-html)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
