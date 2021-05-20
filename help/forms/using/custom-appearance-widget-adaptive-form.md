---
title: Création d’apparences personnalisées pour les champs de formulaire adaptatif
seo-title: Création d’apparences personnalisées pour les champs de formulaire adaptatif
description: Personnalisation de l’apparence des composants prêts à l’emploi dans les formulaires adaptatifs.
seo-description: Personnalisation de l’apparence des composants prêts à l’emploi dans les formulaires adaptatifs.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 73%

---

# Création d’apparences personnalisées pour les champs de formulaire adaptatif{#create-custom-appearances-for-adaptive-form-fields}

## Présentation {#introduction}

Les formulaires adaptatifs exploitent [le cadre de l’apparence](/help/forms/using/introduction-widgets.md) pour vous aider à créer des apparences personnalisées pour des champs de formulaire adaptatif et offrir une expérience différente à l’utilisateur. Par exemple, remplacez des boutons radio et des cases à cocher par les boutons de basculement ou utilisez des modules externes jQuery pour limiter les entrées d’utilisateurs dans les champs tels que les numéros de téléphone ou l’ID de courrier électronique. 

Ce document explique comment utiliser un module externe jQuery pour créer ces expériences différentes pour les champs de formulaire adaptatif. En outre, il présente un exemple pour créer une apparence personnalisée de façon à ce que le composant de champ numérique s’affiche sous forme d’exécution numérique pas à pas ou de curseur.

Tout d’abord, examinons les termes et concepts clés utilisés dans cet article.

**** AspectFait référence au style, à l’aspect et à l’organisation des différents éléments d’un champ de formulaire adaptatif. Il comprend généralement un intitulé, une zone interactive pour saisir des données, une icône d’aide et des descriptions longues et courtes du champ. La personnalisation de l’apparence abordée dans cet article s’applique à l’apparence de la zone de saisie du champ.

**jQuery** pluginFournit un mécanisme standard, basé sur la structure du widget jQuery, pour mettre en oeuvre une autre apparence.

**** ClientLibSystème de bibliothèques côté client dans AEM traitement côté client piloté par du code JavaScript et CSS complexe. Pour plus d’informations, voir Utilisation des bibliothèques côté client.

**** Kit d’outils de modèle de projet Maven archetypeA défini comme modèle ou modèle d’origine pour les projets Maven. Pour en savoir plus, voir Présentation des archétypes.

**User** Control Fait référence à l’élément principal d’un widget qui contient la valeur du champ. Il est utilisé par la structure d’aspect pour lier l’interface utilisateur du widget personnalisé au modèle de formulaire adaptatif.

## Procédure à suivre pour créer une apparence personnalisée {#steps-to-create-a-custom-appearance}

Les étapes, à un niveau élevé, pour créer une apparence personnalisée sont les suivantes :

1. **Créez un projet** : Créez un projet Maven qui génère un module de contenu à déployer sur AEM.
1. **Étendez une classe** de widget existante : Étendez une classe de widget existante et remplacez les classes requises.
1. **Créer une bibliothèque cliente** : créez une bibliothèque `clientLib: af.customwidget` et ajoutez les fichiers Javascript et CSS requis.

1. **Créez et installez le projet** : Créez le projet Maven et installez le module de contenu généré sur AEM.
1. **Mettre à jour le formulaire** adaptatif : Mettez à jour les propriétés du champ de formulaire adaptatif pour utiliser l’apparence personnalisée.

### Création d’un projet {#create-a-project}

Un archétype d’expert est un point de départ pour créer une apparence personnalisée. Les détails de l’archétype à utiliser sont les suivants :

* **Référentiel** : https://repo.adobe.com/nexus/content/groups/public/
* **Id De L’Artifact** : custom-apparence-archetype
* **ID de groupe** : com.adobe.aemforms
* **Version** : 1.0.4

Exécutez la commande suivante pour créer un projet local en fonction de l’archétype :

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

La commande télécharge les modules externes experts et des informations sur l’archétype du référentiel et génère un projet basé sur les informations suivantes :

* **groupid** : Id de groupe utilisée par le projet expert généré
* **artifactId** : Id de l’artefact utilisé par le projet expert généré.
* **version** : version du projet expert généré.
* **package** : package utilisé pour la structure des fichiers.
* **artifactName** : nom de l’artefact du package AEM généré.
* **packageGroup** : groupe de packages du package AEM généré.
* **widgetName** : nom de l’apparence utilisé comme référence.

Le projet généré présente la structure suivante : 

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### Étendre une classe de widget existante {#extend-an-existing-widget-class}

Une fois le modèle de projet créé, effectuez les modifications suivantes, selon vos besoins :

1. Incluez la dépendance de module externe tiers au projet.

   1. Placez les modules externes jQuery tiers ou personnalisés dans le dossier `jqueryplugin/javascript` et les fichiers CSS associés dans le dossier `jqueryplugin/css`. Pour plus d’informations, voir les fichiers JS et CSS sous le dossier `jqueryplugin/javascript and jqueryplugin/css` .

   1. Modifiez les fichiers `js.txt` et `css.txt` pour inclure les fichiers Javascript et CSS supplémentaires du module externe jQuery.

1. Intégrez le module externe tiers au cadre pour permettre une interaction entre le cadre d’apparence personnalisée et le module externe jQuery. Le nouveau widget sera fonctionnel uniquement après avoir étendu ou remplacé les fonctions suivantes.

<table>
 <tbody>
  <tr>
   <td><strong>Fonction</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>La fonction de rendu renvoie l’objet jQuery à l’élément HTML par défaut du widget. L’élément HTML par défaut doit être d’un type pouvant être actif. Par exemple, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code> et <code>&lt;li&gt;</code>. L’élément renvoyé est utilisé comme <code>$userControl</code>. Si <code>$userControl</code> spécifie la contrainte ci-dessus, les fonctions de la classe <code>AbstractWidget</code> fonctionnent comme prévu, sinon certaines des API courantes (mise au point, clic) nécessitent des modifications. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Renvoie un mappage pour convertir les événements HTML en événements XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Cet exemple montre qu’ <code>blur</code> il s’agit d’un événement HTML et  <code>XFA_EXIT_EVENT</code> qu’il s’agit de l’événement XFA correspondant. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Renvoie un mappage qui fournit des détails sur l’action à exécuter lors de la modification d’une option. Les clés sont les options fournies au widget et les valeurs sont des fonctions qui sont appelées chaque fois qu’une modification de l’option est détectée. Le widget fournit des gestionnaires pour toutes les options courantes (à l’exception de <code>value</code> et <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>Le cadre de widget jQuery charge la fonction à chaque fois que la valeur du widget jQuery est enregistrée dans le modèle XFA (par exemple sur l’événement de sortie d’un champ de texte). L’implémentation doit renvoyer la valeur qui est enregistrée dans le widget. Le gestionnaire reçoit la nouvelle valeur de l’option.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Par défaut, lors de l’événement d’entrée dans XFA, la <code>rawValue</code> du champ s’affiche. Cette fonction est appelée pour afficher la <code>rawValue</code> à l’utilisateur. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Par défaut, sur l’événement de sortie dans XFA, la <code>formattedValue</code> du champ s’affiche. Cette fonction est appelée pour afficher la <code>formattedValue</code> à l’utilisateur. </td>
  </tr>
 </tbody>
</table>

1. Mettez le fichier Javascript à jour dans le dossier `integration/javascript` selon les besoins.

   * Remplacez le texte `__widgetName__` par le nom réel du widget.
   * Etendez le widget à partir d’une classe de widgets prêts à l’emploi convenable. Dans la plupart des cas, il s’agit de la classe de widget correspondant au widget existant à remplacer. Le nom de la classe parente est utilisé à plusieurs endroits, il est donc recommandé de rechercher toutes les instances de la chaîne `xfaWidget.textField` dans le fichier, et de les remplacer par la classe parente réelle utilisée.
   * Etendez la méthode `render` pour fournir une autre interface utilisateur. Il s’agit de l’emplacement d’où le module externe jQuery sera appelé pour mettre à jour l’interface utilisateur ou le comportement de l’interaction. La méthode `render` doit retourner un élément de contrôle de l’utilisateur.

   * Etendez la méthode `getOptionsMap` pour remplacer le paramètre d’option concerné suite à une modification du widget. La fonction renvoie un mappage qui fournit des détails sur l’action à effectuer lors de la modification d’une option. Les clés sont les options fournies au widget les valeurs sont les fonctions appelées chaque fois qu’un changement de l’option est détecté.
   * La méthode `getEventMap` mappe les événements déclenchés par le widget avec les événements requis par le modèle de formulaire adaptatif. La valeur par défaut mappe les événements HTML standard du widget par défaut et doit être mise à jour si un événement alternatif est déclenché.
   * La `showDisplayValue` et la `showValue` appliquent la clause d’affichage et de modification de l’image et peuvent être remplacées pour obtenir un autre comportement.

   * La méthode `getCommitValue` est appelée par le cadre des formulaires adaptatifs lorsque l’événement `commit` se produit. En règle générale, il s’agit de l’événement de sortie, à l’exception des éléments de liste déroulante, de bouton-radio et de case à cocher où il s’affiche en cas de modification. Pour en savoir plus, voir [Expressions des formulaires adaptatifs](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * Le fichier de modèle fournit des exemples d’implémentation pour différentes méthodes. Supprimez les méthodes qui ne doivent pas être étendues.

### Créer une bibliothèque cliente {#create-a-client-library}

L’exemple de projet généré par l’archétype d’expert crée automatiquement les bibliothèques clientes requises et les inclut dans une bibliothèque cliente avec une catégorie `af.customwidgets` . Les fichiers Javascript et CSS disponibles dans `af.customwidgets` sont automatiquement inclus au moment de l’exécution.

### Création et installation {#build-and-install}

Pour créer le projet, exécutez la commande suivante sur le shell pour générer un package CRX qui doit être installé sur le serveur AEM.

`mvn clean install`

>[!NOTE]
>
>Le projet d’expert fait référence à un référentiel distant à l’intérieur du fichier POM. Il est indiqué uniquement à titre de référence et conformément aux normes d’expert, les informations du référentiel sont capturées dans le fichier `settings.xml`.

### Mettre à jour le formulaire adaptatif {#update-the-adaptive-form}

Pour appliquer l’apparence personnalisée à un champ de formulaire adaptatif :

1. Ouvrez le formulaire adaptatif en mode d’édition.
1. Ouvrez la boîte de dialogue **Propriétés** pour trouver le champ auquel vous voulez appliquer l’apparence personnalisée.
1. Dans l’onglet **Style** , mettez à jour la propriété `CSS class` pour ajouter le nom de l’apparence au format `widget_<widgetName>` . Par exemple : **widget_numericstepper**

## Exemple : Créer une apparence personnalisée    {#sample-create-a-custom-appearance-nbsp}

Examinons à présent un exemple de création d’une apparence personnalisée pour qu’un champ numérique s’affiche sous forme d’exécution numérique pas à pas ou de curseur. Exécutez les étapes suivantes :

1. Exécutez la commande suivante pour créer un projet local en fonction de l’archétype expert :

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Il vous invite à spécifier des valeurs pour les paramètres suivants.
   *Les valeurs utilisées dans cet exemple sont mises en surbrillance en gras*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Accédez au répertoire `customWidgets` (valeur spécifiée pour la propriété `artifactID`) et exécutez la commande suivante afin de générer un projet Eclipse :

   `mvn eclipse:eclipse`

1. Ouvrez l’outil Eclipse et procédez comme suit pour importer le projet Eclipse :

   1. Sélectionnez **[!UICONTROL Fichier > Importer > Projets existants dans l’espace de travail]**.

   1. Recherchez et sélectionnez le dossier dans lequel vous avez exécuté la commande `archetype:generate`. 

   1. Cliquez sur **[!UICONTROL Finish]** (Terminer). 

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. Sélectionnez le widget à utiliser pour l’apparence personnalisée. Cet exemple utilise le widget d’exécution numérique pas à pas suivant :

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Dans le projet Eclipse, passez en revue le code du module externe dans le fichier `plugin.js` pour vous assurer qu’il correspond à la configuration requise pour l’apparence. Dans cet exemple, l’apparence satisfait aux exigences suivantes :

   * L’exécution numérique pas à pas doit s’étendre à partir de `- $.xfaWidget.numericInput`.
   * La méthode `set value` du widget définit la valeur une fois que le focus est sur le champ. Il s’agit d’un élément obligatoire pour un widget de formulaire adaptatif.
   * La méthode `render` doit être remplacée pour appeler la méthode `bootstrapNumber`.

   * Il n’y a aucune dépendance pour le module externe autre que le code source principal du module externe.
   * L’exemple n’effectue aucune mise en forme sur l’exécution automatique pas à pas ; aucun CSS supplémentaire n’est donc requis.
   * L’objet `$userControl` doit être disponible pour la méthode `render` . Il s’agit d’un champ de type `text` qui est cloné avec le code du module externe.

   * Les boutons **+** et **-** doivent être désactivés lorsque le champ est désactivé.

1. Remplacez le contenu de `bootstrap-number-input.js`(module externe jQuery) par le contenu du fichier `numericStepper-plugin.js` .
1. Dans le fichier `numericStepper-widget.js` , ajoutez le code suivant pour remplacer la méthode de rendu pour appeler le module externe et renvoyer l’objet `$userControl` :

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. Dans le fichier `numericStepper-widget.js` , remplacez la propriété `getOptionsMap` pour remplacer l’option d’accès, puis masquez les boutons + et - en mode désactivé.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. Enregistrez les modifications, accédez au dossier contenant le fichier `pom.xml` et exécutez la commande Maven suivante pour créer le projet :

   `mvn clean install`

1. Installez le package à l’aide d’AEM Package Manager. 

1. Ouvrez le formulaire adaptatif en mode d’édition auquel vous souhaitez appliquer l’apparence personnalisée et procédez comme suit :

   1. Cliquez avec le bouton droit de la souris sur le champ sur lequel vous souhaitez appliquer l’apparence et cliquez sur **[!UICONTROL Modifier]** pour ouvrir la boîte de dialogue Modifier le composant. 

   1. Dans l’onglet Style, mettez à jour la propriété **[!UICONTROL classe CSS]** pour ajouter `widget_numericStepper`.

La nouvelle apparence que vous venez de créer est désormais disponible.
