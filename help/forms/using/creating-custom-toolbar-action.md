---
title: Création d’une action de barre d’outils personnalisée
description: Les développeurs de formulaires peuvent créer des actions de barre d’outils personnalisées pour les formulaires adaptatifs dans les AEM Forms. L’utilisation d’actions personnalisées permet aux auteurs de formulaires de fournir davantage de processus et d’options aux utilisateurs finaux.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 17f7f0e1-09d8-45cd-a4f6-0846bdb079b6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 68%

---

# Création d’une action de barre d’outils personnalisée{#creating-a-custom-toolbar-action}

## Prérequis {#prerequisite}

Avant de créer une action de barre d’outils personnalisée, reportez-vous aux [Utilisation des bibliothèques côté client](/help/sites-developing/clientlibs.md) et [Développement avec le CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Qu’est-ce qu’une action ?  {#what-is-an-action-br}

Un formulaire adaptatif fournit une barre d’outils qui permet à un auteur de formulaire de configurer un ensemble d’options. Ces options sont définies comme des actions pour le formulaire adaptatif. Cliquez sur le bouton Modifier de la barre d’outils pour que le panneau définisse les actions prises en charge par les formulaires adaptatifs.

![Actions de barre d’outils par défaut](assets/default_toolbar_actions.png)

Outre l’ensemble d’actions fourni par défaut, vous pouvez créer des actions personnalisées dans la barre d’outils. Par exemple, vous pouvez ajouter une action pour permettre à l’utilisateur de parcourir tous les champs du formulaire adaptatif avant d’envoyer le formulaire.

## Procédure de création dʼune action personnalisée dans un formulaire adaptatif {#steps}

La procédure ci-dessous illustre la création d’une action personnalisée dans la barre d’outils. Elle décrit la création d’un bouton permettant aux utilisateurs finaux de parcourir tous les champs d’un formulaire adaptatif avant d’envoyer un formulaire complété.

1. Toutes les actions par défaut prises en charge par les formulaires adaptatifs figurent dans le dossier `/libs/fd/af/components/actions`. Dans CRXDE, copiez le nœud `fileattachmentlisting` de `/libs/fd/af/components/actions/fileattachmentlisting` vers `/apps/customaction`.

1. Après avoir copié le nœud dans le dossier `apps/customaction`, renommez-le en `reviewbeforesubmit`. Modifiez également les propriétés `jcr:title` et `jcr:description` du nœud.

   La propriété `jcr:title` contient le nom de l’action qui s’affiche dans la boîte de dialogue de la barre d’outils. La propriété `jcr:description` contient davantage d’informations qui s’affichent lorsqu’un utilisateur place le pointeur de la souris sur l’action.

   ![Hiérarchie des nœuds pour la personnalisation de la barre d’outils](assets/action3.png)

1. Sélectionnez le nœud `cq:template` dans le nœud `reviewbeforesubmit`. Assurez-vous que la valeur de la propriété `guideNodeClass` est `guideButton` et modifiez la propriété `jcr:title` en conséquence.
1. Modifiez la propriété de type dans le nœud `cq:Template`. Pour l’exemple actuel, modifiez la propriété type en bouton .

   La valeur type est ajoutée en tant que classe CSS dans le HTML généré pour le composant. Les utilisateurs peuvent utiliser cette classe CSS pour appliquer un style à leurs actions. Le style par défaut pour les appareils mobiles et fixes (ordinateurs de bureau) est fourni pour les valeurs de type Bouton, Envoyer, Réinitialiser et Enregistrer.

1. Sélectionnez l’action personnalisée dans la boîte de dialogue de barre d’outils de modification du formulaire adaptatif. Un bouton Révision s’affiche dans la barre d’outils du panneau.

   ![Action personnalisée est disponible dans la barre d’outils](assets/custom_action_available_in_toolbar.png) ![Affichage de l’action de barre d’outils personnalisée](assets/action7.png)

1. Pour fournir des fonctionnalités au bouton Révision, ajoutez du code JavaScript et CSS, ainsi que du code côté serveur, dans le fichier init.jsp situé dans le nœud `reviewbeforesubmit`.

   Ajoutez le code suivant dans le fichier `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   Ajoutez le code suivant dans le fichier `ReviewBeforeSubmit.js`.

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   Ajoutez le code suivant dans le fichier `ReviewBeforeSubmit.css`.

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. Pour vérifier les fonctionnalités de l’action personnalisée, ouvrez le formulaire adaptatif en mode Aperçu et cliquez sur Révision dans la barre d’outils.

   >[!NOTE]
   >
   >La bibliothèque `GuideBridge` n’est pas chargée en mode de création. Cette action personnalisée ne fonctionne donc pas dans ce mode.

   ![Démonstration de l’action du bouton de révision personnalisée](assets/action9.png)

## Exemples {#samples}

L’archive suivante contient un module de contenu. Le package comprend un formulaire adaptatif associé à la démonstration ci-dessus de l’action de barre d’outils personnalisée.

[Obtenir le fichier](assets/customtoolbaractiondemo.zip)
