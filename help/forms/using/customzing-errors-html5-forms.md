---
title: Personnaliser les messages d’erreur pour les formulaires HTML5
seo-title: Customizing error messages for HTML5 forms
description: Découvrez comment personnaliser l’affichage des messages d’erreur pour les formulaires HTML5 et notamment comment modifier leur position et leur aspect.
seo-description: Learn how to customize the display of error messages for HTML5 forms including how to change their position and appearance.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '515'
ht-degree: 100%

---

# Personnaliser les messages d’erreur pour les formulaires HTML5 {#customizing-error-messages-for-html-forms}

Dans les formulaires HTML5, hors de la zone, les messages d’erreur et les avertissements ont une position et un aspect fixes (police et couleur), l’erreur est affichée uniquement pour un champ sélectionné, et une seule erreur s’affiche.

L’article fournit les étapes pour personnaliser les messages d’erreur des formulaires HTML5 afin de

* changer l’aspect et la position des messages d’erreur. Vous pouvez faire qu’une erreur apparaisse en haut, en bas, et sur le côté droit de chaque champ.
* afficher les messages d’erreur pour plusieurs champs à tout moment spécifié. 
* afficher l’erreur, que le champ soit sélectionné ou non.

## Personnalisation des messages d’erreur  {#customizing-error-messages-nbsp}

Avant de personnaliser les messages d’erreur, téléchargez et extrayez le package ci-joint (CustomErrorManager-1.0-SNAPSHOT.zip). 

Après avoir extrait le package, ouvrez le dossier CustomErrorManager-1.0-SNAPSHOT. Il contient les dossiers jcr_root et META-INF. Ces dossiers contiennent les fichiers CSS et .JS requis pour personnaliser les messages d’erreur.

[Obtenir le fichier](assets/customerrormanager-1.0-snapshot.zip)

### Personnalisation de la position des messages d’erreur  {#customizing-the-position-of-error-messages-nbsp}

Pour personnaliser la position d’un message d’erreur, ajoutez une balise &lt;div> à chaque champ d’erreur et d’avertissement, positionnez la balise &lt;div> à gauche ou à droite, puis appliquez les styles CSS à la balise &lt;div>. Pour obtenir des instructions détaillées, consultez la procédure ci-dessous :

1. Accédez au dossier `CustomErrorManager-1.0-SNAPSHOT` et ouvrez le dossier `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`.
1. Ouvrez le fichier `customErrorManager.js` pour le modifier. La fonction `markError` du fichier accepte les paramètres suivants :

   |  |  |
   |---|---|
   | jqWidget | jqWidget est la poignée du widget. |
   | msg | contient le message d’erreur |
   | type | indique s’il s’agit d’une erreur ou d’un avertissement |

1. Sur l’implémentation hors de la zone, les messages d’erreur apparaissent à droite du champ. Pour que les messages d’erreur apparaissent au-dessus, utilisez le code suivant.

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
1. Utilisez le gestionnaire de packages pour télécharger et installer le package.

## Affichage des messages d’erreur pour plusieurs champs  {#display-error-messages-for-multiple-fields-nbsp}

Utilisez le package ci-joint pour afficher simultanément les messages d’erreur pour tous les champs. Pour afficher un seul message d’erreur, utilisez le profil par défaut.

### Personnalisation de l’aspect des messages d’erreur.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Accédez au dossier etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css.

1. Ouvrez le fichier sample.css en mode d’édition. Le fichier CSS contient 2 identifiants, #customError, #customWarning. Vous pouvez utiliser ces identifiants pour modifier diverses propriétés telles que la couleur, la taille de police, etc.

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
1. Utilisez le gestionnaire de packages pour télécharger et installer le package.

## Rendre le formulaire avec le nouveau profil.  {#render-the-form-with-the-new-profile-nbsp}

D’emblée, les formulaires HTML5 utilisent un profil par défaut : https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>.

Pour afficher un formulaire avec les messages d’erreur personnalisés, effectuez le rendu du formulaire avec le profil d’erreur : https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location>&amp;template=&lt;name of the xdp>.

>[!NOTE]
>
>Le package ci-joint installe le profil d’erreur.
