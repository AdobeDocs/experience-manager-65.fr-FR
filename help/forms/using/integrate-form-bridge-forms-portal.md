---
title: Intégration d’un objet Form Bridge à un portail personnalisé pour les formulaires HTML5
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: Vous pouvez utiliser l’API FormBridge pour obtenir ou définir les valeurs des champs de formulaire à partir de la page de HTML et envoyer le formulaire.
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 26%

---

# Intégration d’un objet Form Bridge à un portail personnalisé pour les formulaires HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge est une API de passerelle de formulaires HTML5 qui vous permet d’interagir avec un formulaire. Pour plus d’informations sur la référence à l’API FormBridge, reportez-vous à [Référence à l’API FormBridge](/help/forms/using/form-bridge-apis.md).

Vous pouvez utiliser l’API FormBridge pour obtenir ou définir les valeurs des champs de formulaire à partir de la page de HTML et envoyer le formulaire. Par exemple, vous pouvez utiliser l’API pour créer une expérience de type assistant.

Une application de HTML existante peut tirer parti de l’API FormBridge pour interagir avec un formulaire et l’incorporer dans la page de HTML. Vous pouvez utiliser les étapes suivantes pour définir la valeur d’un champ à l’aide de l’API Form Bridge.

## Intégration de formulaires HTML5 à une page web {#integrating-html-forms-to-a-web-page}

1. **Choix ou création d’un profil**

   1. Dans l’interface CRX DE, accédez à : `https://'[server]:[port]'/crx/de`.
   1. Connectez-vous à l’aide des informations d’identification de l’administrateur.
   1. Créez un profil ou choisissez un profil existant.

      Pour plus d’informations sur la façon de créer un profil, voir[ Création d’un nouveau profil](/help/forms/using/custom-profile.md).

1. **Modification du profil de HTML**

   Incluez l’exécution XFA, la bibliothèque XFA locale et le fragment de HTML de formulaire XFA dans le rendu du profil, concevez votre page web et placez le formulaire dans la page web.

   Par exemple, utilisez le fragment de code suivant pour créer une application avec deux champs de saisie et un formulaire pour démontrer l’interaction entre le formulaire et une application externe.

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
   >La variable &lt;div id=&quot;rightdiv&quot;> balise **ligne 18** contient le fragment de HTML du formulaire XFA.
   >
   >
   La page est mise en forme en deux conteneurs : **left** et **right**. Le conteneur de droite comporte le formulaire . Le conteneur de gauche comporte deux champs de saisie et une partie de la page de HTML externe.
   >
   >
   La capture d’écran suivante montre comment le formulaire s’affiche dans un navigateur.

   ![Portail](assets/portal.jpg)

   Le côté gauche fait partie de la **HTML page**. Le côté droit contenant les champs est le **formulaire xfa**.

1. **Accès aux champs du formulaire depuis la page**

   Voici un exemple de script que vous pouvez ajouter pour définir des valeurs dans un champ de formulaire.

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
