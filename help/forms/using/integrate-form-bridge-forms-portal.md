---
title: Intégration d’un objet Form Bridge à un portail personnalisé pour les formulaires HTML5
description: Vous pouvez utiliser l’API FormBridge pour obtenir ou définir des valeurs de champs de formulaire à partir de la page HTML et envoyer le formulaire.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 100%

---

# Intégration d’un objet Form Bridge à un portail personnalisé pour les formulaires HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge est une API Forms Bridge d&#39;HTML5 qui vous permet d’interagir avec un formulaire. Pour plus d’informations sur la référence à l’API FormBridge, reportez-vous à [Référence à l’API FormBridge](/help/forms/using/form-bridge-apis.md).

Vous pouvez utiliser l’API FormBridge pour obtenir ou définir des valeurs de champs de formulaire à partir de la page HTML et envoyer le formulaire. Par exemple, vous pouvez utiliser l’API pour créer une expérience semblable à un assistant.

Une application HTML existante peut utiliser l’API FormBridge pour interagir avec un formulaire et l’intégrer à la page HTML. Vous pouvez utiliser les étapes suivantes pour définir la valeur d’un champ à l’aide de l’API Form Bridge.

## Intégration de formulaires HTML5 à une page web {#integrating-html-forms-to-a-web-page}

1. **Choix ou création d’un profil**

   1. Dans l’interface CRX DE, accédez à : `https://'[server]:[port]'/crx/de`.
   1. Connectez-vous à l’aide des informations d’identification de l’administrateur ou de l’administratrice.
   1. Créez un profil ou choisissez un profil existant.

      Pour plus d’informations sur la façon de créer un profil, voir [Création d’un profil](/help/forms/using/custom-profile.md).

1. **Modifier un profil HTML**

   Ajoutez l’exécution de XFA, la bibliothèque XFA locale et l’extrait de formulaire XFA en HTML dans le rendu du profil, concevez votre page Web et placez le formulaire dans la page Web.

   Par exemple, utilisez l’extrait de code suivant, pour créer une application avec deux champs de saisie et un formulaire pour démontrer l’interaction entre le formulaire et une application externe.

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >La **ligne 9** contient la référence JSP supplémentaire pour permettre aux fichiers CSS et Javascript de concevoir la page.
   >
   >
   >La balise &lt;div id=&quot;rightdiv&quot;> à la **ligne 18** contient le snippet HTML du formulaire XFA.
   >
   >
   >La page comprend deux conteneurs : **gauche** et **droit**. Le conteneur de droite contient le formulaire. Le conteneur de gauche possède deux champs de saisie et une partie de la page HTML externe.
   >
   >
   >La capture d’écran suivante montre comment le formulaire s’affiche dans un navigateur.

   ![Portail](assets/portal.jpg)

   La partie gauche fait partie de la **page HTML**. La partie droite contenant les champs est le **formulaire xfa**.

1. **Accéder aux champs du formulaire à partir de la page**

   Voici un exemple de script que vous pouvez ajouter pour définir les valeurs dans un champ de formulaire.

   Par exemple, si vous souhaitez définir la valeur **EmployeeName** à l’aide des valeurs des champs **Prénom** et **Nom**, appelez la fonction **window.formBridge.setFieldValue**.

   De même, vous pouvez lire la valeur en appelant l’API **window.formBridge.getFieldValue**.

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
