---
title: Ajout d’une action personnalisée à la vue Liste des ressources
description: Cet article explique comment ajouter une action personnalisée à la vue liste des ressources.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: bf6d3edb-6bf7-4d3e-b042-d75cb8e39e3f
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1333'
ht-degree: 100%

---

# Ajout d’une action personnalisée à la vue Liste des ressources{#add-custom-action-to-the-asset-listing-view}

## Présentation {#overview}

La solution Gestion des correspondances vous permet d’ajouter des actions personnalisées à l’interface utilisateur Gérer les ressources.

Vous pouvez ajouter une action personnalisée à la vue liste des ressources pour :

* un ou plusieurs types de ressources ou lettres ;
* l’exécution (l’action/la commande devient active) lors de la sélection de plusieurs ressources/lettres uniques ou sans sélection.

Cette personnalisation est illustrée par le scénario qui ajoute une commande « Télécharger le PDF aplati » à la vue liste des ressources pour les lettres. Ce scénario de personnalisation permet à vos utilisateurs de télécharger le PDF aplati d’une lettre simple.

### Prérequis {#prerequisites}

Pour réaliser le scénario suivant ou un scénario similaire, vous devez connaître :

* CRX 
* JavaScript
* Java™

## Scénario : ajouter une commande à l’interface utilisateur Liste de lettres pour télécharger la version PDF aplatie d’une lettre. {#addcommandtoletters}

Les étapes ci-dessous ajoutent une commande « Télécharger le PDF aplati » à la vue liste des ressources pour les lettres et permettent à vos utilisateurs et utilisatrices de télécharger la version PDF aplatie de la lettre sélectionnée. En suivant ces étapes avec le code et les paramètres appropriés, vous pouvez ajouter d’autres fonctionnalités pour une ressource différente, comme des dictionnaires de données ou des textes.

Pour personnaliser Correspondence Management afin de permettre à vos utilisateurs et utilisatrices de télécharger une version PDF aplatie de lettres, procédez comme suit :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.

1. Dans le dossier d’applications, créez un dossier appelé éléments avec un chemin/une structure semblable au dossier d’éléments situé dans le dossier de sélection. Pour ce faire, procédez comme suit :

   1. Faites un clic droit sur le dossier des **éléments** à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >Ce chemin d’accès est spécifique à la création d’une action qui fonctionne avec la sélection d’une ou de plusieurs ressources/lettres. Si vous souhaitez créer une action qui fonctionne sans sélection, créez un nœud de recouvrement pour le chemin suivant et effectuez les étapes restantes en conséquence :
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![Créer un nœud](assets/1_itemscreatenode.png)

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** sélectionné

      ![Nœud de recouvrement](assets/2_createnodedownloadflatpdf.png)

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

      Cliquez sur **Enregistrer tout**.

1. Dans le dossier dʼéléments que vous avez créé, ajoutez un nœud pour le bouton/l’action personnalisé(e) d’une ressources particulière (exemple : downloadFlatPDF) en procédant comme suit :

   1. Cliquez avec le bouton droit sur le dossier **éléments** et sélectionnez **Créer** > **Créer un nœud**.

   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** downloadFlatPDF (ou le nom que vous souhaitez donner à cette propriété).

      **Type :** nt:unstructured

   1. Cliquez sur le nœud que vous avez créé (ici downloadFlatPDF). CRX affiche les propriétés du nœud.

   1. Ajoutez les propriétés suivantes au nœud (ici downloadFlatPDF) et cliquez sur **Enregistrer tout** :

      <table>
        <tbody>
        <tr>
        <td><strong>Nom</strong></td>
        <td><strong>Type</strong></td>
        <td><strong>Valeur et description</strong></td>
        </tr>
        <tr>
        <td>class</td>
        <td>Chaîne</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>Chaîne</td>
        <td><p>{"target": ".cq-manageasset-admin-childpages", "activeSelectionCount": "single","type": "LETTER"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> peut être unique ou multiple pour autoriser les sélections de ressources uniques ou multiples sur lesquelles effectuer une action personnalisée.</p> <p><strong>type</strong> peut être unique ou multiple (entrées multiples séparées par des virgules) : LETTER,TEXT,LIST,CONDITION,DATADICTIONARY</p> </td>
        </tr>
        <tr>
        <td>icon</td>
        <td>Chaîne</td>
        <td>icône-téléchargement<br /> <br /> Icône affichée par Correspondence Management sur le côté gauche de la commande/du menu. Pour connaître les icônes et paramètres disponibles, voir la <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr" target="_blank">documentation relative aux icônes CoralUI</a>.<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>Nom</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>Chaîne</td>
        <td>download-plat-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>Chaîne</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>text</td>
        <td>Chaîne</td>
        <td>Télécharger le PDF aplati (ou toute autre libellé)<br /> <br /> La commande qui apparaît dans l’interface de la liste des ressources</td>
        </tr>
        <tr>
        <td>titre</td>
        <td>Chaîne</td>
        <td>Téléchargez un document PDF aplati de la lettre sélectionnée (ou de tout autre libellé/texte de remplacement)<br /> <br /> Le titre correspond au texte affiché par Correspondence Management lorsque l’utilisateur passe sa souris sur la commande personnalisée.</td>
        </tr>
        </tbody>
       </table>

1. Dans le dossier d’applications, créez un dossier appelé js avec un chemin/une structure semblable au dossier d’éléments dans le dossier admin. Pour cela, suivez les étapes ci-après :

   1. Cliquez avec le bouton droit sur le dossier **js** à l’emplacement suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications. Cliquez sur **Enregistrer tout**.

1. Dans le dossier js, procédez comme suit pour créer un fichier nommé formaction.js avec le code de traitement d’action du bouton :

   1. Faites un clic droit sur le dossier **js** et sélectionnez **Créer > Créer un fichier** :

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      Nommez le fichier formaction.js.

   1. Double-cliquez sur le fichier pour l’ouvrir dans CRX.
   1. Dans le fichier formaction.js (sous la branche /apps), copiez le code à partir du fichier formaction.js à l’emplacement suivant :

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      Apposez alors le code suivant à l’extrémité dans le fichier formaction.js (sous la branche /apps) et cliquez sur **Enregistrer tout** :

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      Le code que vous ajoutez à cette étape remplace le code sous le dossier libs. Par conséquent, copiez le code précédent dans le fichier formaction.js dans la branche /apps. La copie du code de la branche /libs vers la branche /apps garantit que la fonctionnalité précédente fonctionne également.

      Le code ci-dessus est destiné au traitement des actions spécifiques aux lettres de la commande créée dans cette procédure. Pour gérer les actions d’autres ressources, modifiez le code JavaScript.

1. Dans le dossier d’applications, créez un dossier appelé éléments avec un chemin/une structure semblable au dossier d’éléments dans le dossier actionhandlers. Pour ce faire, procédez comme suit :

   1. Faites un clic droit sur le dossier des **éléments** à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** : 

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

   1. Cliquez sur **Enregistrer tout**.

1. Dans le nœud d’éléments que vous avez créé, ajoutez un nœud pour le bouton/l’action personnalisé(e) d’une ressource particulière (exemple : letterpdfdownloader) en suivant les étapes ci-après :

   1. Cliquez avec le bouton droit sur le dossier éléments et sélectionnez **Créer > Créer un nœud**.

   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** letterpdfdownloader (ou le nom que vous souhaitez donner à cette propriété - doit être unique. Si vous utilisez ici un autre nom, spécifiez le même dans la variable ACTION_URL du fichier formaction.js).

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau nœud que vous avez créé (ici downloadFlatPDF). CRX affiche les propriétés du nœud.

   1. Ajoutez la propriété suivante au nœud (ici letterpdfdownloader) et cliquez sur **Enregistrer tout** :

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | sling:resourceType | Chaîne | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. Créez un fichier appelé POST.jsp avec le code de traitement d’action de la commande à l’emplacement suivant :

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. Faites un clic droit sur le dossier **admin** et sélectionnez **Créer > Créer un fichier** :

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      Nommez le fichier POST.jsp. (Le nom du fichier doit être POST.jsp uniquement.)

   1. Double-cliquez sur le fichier **POST.jsp** pour l’ouvrir dans CRX.
   1. Ajoutez le code suivant au fichier POST.jsp et cliquez sur **Enregistrer tout** :

      Ce code est spécifique au service de rendu de lettre. Pour toute autre ressource, ajoutez les bibliothèques Java™ de ladite ressource à ce code. Pour plus d’informations sur les API d’AEM Forms, reportez-vous à [API d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

      Pour plus d’informations sur les bibliothèques d’AEM, consultez la section relatives aux [Composants](/help/sites-developing/components.md) AEM.

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## Télécharger le PDF aplati à partir d’une lettre à l’aide de la fonction personnalisée {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

Après avoir ajouté la fonctionnalité personnalisée pour télécharger un fichier PDF aplati de vos lettres, vous pouvez suivre les étapes ci-après pour télécharger la version PDF aplatie de la lettre :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/projects.html` et connectez-vous.

1. Sélectionnez **Formulaires > Lettres**. Correspondence Management répertorie les lettres disponibles dans le système.
1. Cliquez sur **Sélectionner**, puis sur une lettre pour la sélectionner.
1. Sélectionnez **plus** > **&lt;Télécharger un PDF aplati>** (soit la fonctionnalité personnalisées créée à l’aide des instructions fournies dans cet article). La boîte de dialogue Télécharger la lettre en tant que PDF s’affiche.

   Le nom de l’élément de menu, la fonctionnalité et l’autre texte dépendent de la personnalisation créée dans le [Scénario : ajoutez une commande à l’interface utilisateur des listes Lettres pour télécharger la version PDF aplatie d’une lettre.](#addcommandtoletters)

   ![Fonctionnalité personnalisée : Télécharger le PDF aplati](assets/5_downloadflatpdf.png)

1. Dans la boîte de dialogue Télécharger la lettre en tant que PDF, sélectionnez le XML approprié à partir duquel vous souhaitez renseigner les données du PDF.

   >[!NOTE]
   >
   >Avant de télécharger la lettre en tant que PDF aplati, vous pouvez créer le fichier XML avec les données dans la lettre à l’aide de l’option **Créer un rapport**.

   ![Télécharger la lettre en tant que PDF](assets/6_downloadflatpdf.png)

   La lettre est téléchargée sur votre ordinateur au format PDF aplati.
