---
title: Personnaliser les messages d’erreur pour les formulaires HTML5
description: Découvrez comment personnaliser l’affichage des messages d’erreur pour les formulaires HTML5, y compris comment modifier leur position et leur apparence.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '497'
ht-degree: 100%

---

# Personnaliser les messages d’erreur pour les formulaires HTML5 {#customizing-error-messages-for-html-forms}

Dans les formulaires HTML5, hors de la zone, les messages d’erreur et les avertissements ont une position et un aspect fixes (police et couleur), l’erreur est affichée uniquement pour un champ sélectionné, et une seule erreur s’affiche.

Cet article décrit les étapes de personnalisation des messages d’erreur des formulaires HTML5 afin que vous puissiez effectuer les opérations suivantes :

* changer l’aspect et la position des messages d’erreur. Vous pouvez faire qu’une erreur apparaisse en haut, en bas, et sur le côté droit de chaque champ.
* afficher les messages d’erreur pour plusieurs champs à tout moment spécifié. 
* afficher l’erreur, que le champ soit sélectionné ou non.

## Personnalisation des messages d’erreur  {#customizing-error-messages-nbsp}

Avant de personnaliser les messages d’erreur, téléchargez et extrayez le package ci-joint (CustomErrorManager-1.0-SNAPSHOT.zip). 

Une fois que vous avez extrait le package, ouvrez le dossier CustomErrorManager-1.0-SNAPSHOT. Il contient les dossiers jcr_root et META-INF. Ces dossiers contiennent les fichiers CSS et .JS requis pour personnaliser le message d’erreur.

[Obtenir le fichier](assets/customerrormanager-1.0-snapshot.zip)

### Personnaliser la position des messages d’erreur {#customizing-the-position-of-error-messages-nbsp}

Pour personnaliser la position du message d’erreur, ajoutez une balise &lt;div> pour chaque champ d’erreur et d’avertissement, puis positionnez la balise &lt;div> sur la gauche ou la droite et appliquez des styles CSS à la balise &lt;div>. Pour obtenir des instructions détaillées, suivez la procédure ci-dessous :

1. Accédez au dossier `CustomErrorManager-1.0-SNAPSHOT` et ouvrez le dossier `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`.
1. Ouvrez le fichier `customErrorManager.js` pour le modifier. La fonction `markError` du fichier accepte les paramètres suivants :

   |   |  |
   |---|---|
   | jqWidget | jqWidget est la poignée d’un widget. |
   | msg | contient le message d’erreur |
   | type | indique s’il s’agit d’une erreur ou d’un avertissement |

1. Sur l’implémentation prête à l’emploi, les messages d’erreur s’affichent à droite du champ. Pour que les messages d’erreur apparaissent au-dessus, utilisez le code suivant.

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. Enregistrez et fermez le fichier.
1. Accédez au dossier `CustomErrorManager-1.0-SNAPSHOT` et créez une archive des dossiers jcr_root et META-INF. Renommez l’archive en CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilisez le gestionnaire de modules pour charger et installer le package.

## Afficher les messages d’erreur pour plusieurs champs {#display-error-messages-for-multiple-fields-nbsp}

Utilisez le package joint pour afficher simultanément les messages d’erreur pour tous les champs. Pour afficher un seul message d’erreur, utilisez le profil par défaut.

### Personnalisez l’apparence des messages d’erreur.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Accédez au dossier etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css.

1. Ouvrez le fichier sample.css en mode d’édition. Le fichier CSS contient 2 id : #customError et #customWarning. Vous pouvez utiliser ces identifiants pour modifier diverses propriétés, telles que la couleur et la taille de police.

   Utilisez le code suivant pour modifier la taille de police et la couleur des messages d’erreur ou d’avertissement.

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. Enregistrez et fermez le fichier.
1. Accédez au dossier CustomErrorManager-1.0-SNAPSHOT et créez une archive des dossiers jcr_root et META-INF. Renommez l’archive en CustomErrorManager-1.0-SNAPSHOT.zip.
1. Utilisez le gestionnaire de modules pour charger et installer le package.

## Rendre le formulaire avec le nouveau profil.  {#render-the-form-with-the-new-profile-nbsp}

Les formulaires HTML5 prêts à l’emploi utilisent un profil par défaut : `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

Pour afficher un formulaire avec les messages d’erreur personnalisés, effectuez le rendu du formulaire avec le profil d’erreur : `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>Le package ci-joint installe le profil d’erreur.
