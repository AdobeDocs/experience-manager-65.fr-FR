---
title: Création d’une action Envoyer personnalisée pour les formulaires adaptatifs
seo-title: Création d’une action Envoyer personnalisée pour les formulaires adaptatifs
description: Les formulaires AEM permettent de créer une action Envoyer personnalisée pour les formulaires adaptatifs. Cet article décrit la procédure à suivre pour ajouter une action Envoyer personnalisée pour les formulaires adaptatifs.
seo-description: Les formulaires AEM permettent de créer une action Envoyer personnalisée pour les formulaires adaptatifs. Cet article décrit la procédure à suivre pour ajouter une action Envoyer personnalisée pour les formulaires adaptatifs.
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 71%

---

# Création d’une action Envoyer personnalisée pour les formulaires adaptatifs{#writing-custom-submit-action-for-adaptive-forms}

Les formulaires adaptatifs nécessitent des actions d’envoi pour traiter les données spécifiées par l’utilisateur. Une action Envoyer détermine la tâche effectuée sur les données que vous envoyez à l’aide d’un formulaire adaptatif. Adobe Experience Manager (AEM) comprend des [actions Envoyer prêtes à l’emploi](../../forms/using/configuring-submit-actions.md) qui montrent les tâches personnalisées que vous pouvez effectuer à l’aide des données envoyées par l’utilisateur. Vous pouvez par exemple effectuer des tâches comme envoyer un courrier électronique ou stocker les données.

## Processus d&#39;une action Envoyer {#workflow-for-a-submit-action}

L’organigramme illustre le processus d’une action Envoyer déclenchée lorsque vous cliquez sur le bouton **[!UICONTROL Envoyer]** dans un formulaire adaptatif. Les fichiers du composant Pièce jointe sont téléchargés sur le serveur, et les données de formulaire sont mises à jour avec les URL des fichiers téléchargés. Sur le client, les données sont stockées au format JSON. Le client envoie une requête Ajax à une servlet interne qui transforme les données spécifiées et les renvoie au format XML. Le client assemble ces données avec des champs d’action. Elle envoie les données au servlet final (servlet Guide Submit) par le biais d’une action d’envoi de formulaire. La servlet transfère ensuite le contrôle à l’action Envoyer. L’action Envoyer peut transférer la requête vers une ressource sling différente ou rediriger le navigateur vers une autre URL.

![Organigramme décrivant le flux de l’action Envoyer](assets/diagram1.png)

### Format des données XML {#xml-data-format}

Les données XML sont envoyées à la servlet à l’aide du paramètre de requête **`jcr:data`**. Les actions Envoyer peuvent accéder au paramètre pour traiter les données. Le code ci-après décrit le format des données XML. Les champs liés au modèle de formulaire apparaissent dans la section **`afBoundData`**. Les champs non liés apparaissent dans la `afUnoundData`section. Pour plus d’informations sur le format du fichier `data.xml`, voir [Présentation du préremplissage des champs de formulaire adaptatif](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Champs d’action {#action-fields}

Une action Envoyer peut ajouter des champs d’entrée masqués (à l’aide de la balise HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input)) au code HTML du formulaire rendu. Ces champs masqués peuvent contenir les valeurs dont elle a besoin lors du traitement de l’envoi du formulaire. Lors de l’envoi du formulaire, ces valeurs de champ sont republiées en tant que paramètres de requête que l’action Envoyer peut utiliser lors de la gestion de l’envoi. Les champs d’entrée sont appelés champs d’action.

Par exemple, une action Envoyer qui capture également le temps nécessaire au remplissage d’un formulaire peut ajouter les champs de saisie masqués `startTime` et `endTime`.

Un script peut fournir les valeurs des champs `startTime` et `endTime` lors du rendu du formulaire et avant l’envoi du formulaire. Le script de l’action Envoyer `post.jsp` peut ensuite accéder à ces champs à l’aide des paramètres de requête et calculer le temps total nécessaire au remplissage du formulaire.

### Pièces jointes {#file-attachments}

Les actions Envoyer peuvent également utiliser les pièces jointes que vous téléchargez à l’aide du composant Pièce jointe. Les scripts des actions Envoyer peuvent accéder à ces fichiers à l’aide de la chaîne [RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). La méthode [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) de l’API permet de déterminer si le paramètre de requête correspond à un fichier ou à un champ de formulaire. Vous pouvez effectuer une itération sur les paramètres de requête dans une action Envoyer pour identifier les paramètres de pièce jointe.

L’exemple de code ci-après identifie les pièces jointes de la requête. Il lit ensuite les données du fichier à l’aide de [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Il crée enfin un objet Document à l’aide des données et l’ajoute à la liste.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Chemin de transfert et URL de redirection {#forward-path-and-redirect-url}

Après avoir exécuté l’action requise, la servlet Submit transfère la requête vers le chemin de transfert. Une action utilise l’API setForwardPath pour définir le chemin de transfert dans la servlet Guide Submit.

Si l’action ne fournit pas de chemin de transfert, la servlet Submit redirige le navigateur à l’aide de l’URL de redirection. L’auteur configure l’URL de redirection à l’aide de la configuration de la page Merci dans la boîte de dialogue Modifier le formulaire adaptatif. Vous pouvez également configurer l’URL de redirection par le biais de l’action Envoyer ou de l’API setRedirectUrl dans la servlet Guide Submit. Les paramètres de requête envoyés à l’URL de redirection peuvent aussi être configurés à l’aide de l’API setRedirectParameters de la servlet Guide Submit.

>[!NOTE]
>
>Un auteur fournit l’URL de redirection (à l’aide de la configuration de la page Merci). Les [actions Envoyer prêtes à l’emploi](../../forms/using/configuring-submit-actions.md) utilisent l’URL de redirection pour rediriger le navigateur à partir de la ressource référencée par le chemin de transfert.
>
>Vous pouvez écrire une action Envoyer personnalisée qui transfère une requête vers une ressource ou une servlet. Adobe recommande que le script qui effectue la gestion des ressources pour le chemin de transfert redirige la requête vers l’URL de redirection au terme du traitement.

## Action Envoyer {#submit-action}

Une action Envoyer est un sling:Folder qui comprend les éléments suivants :

* **addfields.jsp** : ce script fournit les champs d’action qui sont ajoutés au fichier HTML lors du rendu. Utilisez ce script pour ajouter les paramètres d’entrée masqués requis lors de l’envoi au script post.POST.jsp.
* **dialog.xml** : ce script est similaire à la boîte de dialogue Composant CQ. Il fournit des informations de configuration que l’auteur personnalise. Les champs s’affichent dans l’onglet Actions Envoyer de la boîte de dialogue Modifier le formulaire adaptatif lorsque vous sélectionnez l’action Envoyer.
* **post.POST.jsp** : la servlet Submit appelle ce script avec les données envoyées et les autres données des sections précédentes. Toute mention relative à l’exécution d’une action dans cette page implique l’exécution du script post.POST.jsp. Pour enregistrer l’action Envoyer avec les formulaires adaptatifs à afficher dans la boîte de dialogue Modifier le formulaire adaptatif, ajoutez les propriétés suivantes au sling:Folder :

   * **guideComponentType** de type chaîne et valeur **fd/af/components/guidesubmittype**
   * **** guideDataModelof type Chaîne qui spécifie le type de formulaire adaptatif pour lequel l’action Envoyer est applicable. **** xéchoue pris en charge pour les formulaires adaptatifs basés sur XFA, tandis que  **** xsdis pris en charge pour les formulaires adaptatifs basés sur XSD. **** les bases sont prises en charge pour les formulaires adaptatifs qui n’utilisent pas XDP ou XSD. Pour afficher l’action sur plusieurs types de formulaire adaptatif, ajoutez les chaînes correspondantes. Séparez chaque chaîne par une virgule. Par exemple, pour rendre une action visible sur des formulaires adaptatifs XFA et XSD, spécifiez respectivement les valeurs **xfa** et **xsd**.

   * **jcr:description** de type chaîne. La valeur de cette propriété s’affiche dans la liste des actions Envoyer sous l’onglet Actions Envoyer de la boîte de dialogue Modifier le formulaire adaptatif. Les actions prêtes à l’emploi figurent dans le référentiel CRX, à l’emplacement **/libs/fd/af/components/guidesubmittype**.

## Création d&#39;une action Envoyer personnalisée {#creating-a-custom-submit-action}

Pour créer une action Envoyer personnalisée qui enregistre les données dans le référentiel CRX et envoie ensuite un courrier électronique, suivez la procédure ci-après. Le formulaire adaptatif contient l’action Envoyer Stocker le contenu (obsolète) prête à l’emploi qui enregistre les données dans le référentiel CRX. En outre, CQ fournit une API de [messagerie](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=en#previous-updates) qui peut être utilisée pour envoyer des e-mails. Avant d’utiliser l’API de messagerie, [configurez](https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring le service de messagerie) le service de messagerie Day CQ via la console système. Vous pouvez réutiliser l’action Stocker le contenu (obsolète) pour stocker les données dans le référentiel. L’action Stocker le contenu (obsolète) se trouve à l’emplacement /libs/fd/af/components/guidesubmittype/store dans le référentiel CRX.

1. Connectez-vous à CRXDE Lite en accédant à https://&lt;server>:&lt;port>/crx/de/index.jsp. Créez un nœud avec la propriété sling:Folder et le nom store_and_mail dans le dossier /apps/custom_submit_action. Créez le dossier custom_submit_action, le cas échéant.

   ![Capture d’écran décrivant la création d’un nœud avec la propriété sling:Folder](assets/step1.png)

1. **Fournissez les champs de configuration obligatoires.**

   Ajoutez la configuration nécessaire à l’action Stocker. Copiez le nœud **cq:dialog** de l’action Stocker à l’emplacement /libs/fd/af/components/guidesubmittype/store dans le dossier d’action à l’emplacement /apps/custom_submit_action/store_and_email.

   ![Capture d’écran affichant la copie du nœud de boîte de dialogue au dossier d’action](assets/step2.png)

1. **Fournissez des champs de configuration pour demander à l’auteur la configuration des e-mails.**

   Le formulaire adaptatif contient également une action Courrier électronique qui permet d’envoyer des messages électroniques aux utilisateurs. Personnalisez cette action selon vos besoins. Accédez à /libs/fd/af/components/guidesubmittype/email/dialog. Copiez les noeuds du noeud cq:dialog dans le noeud cq:dialog de votre action Envoyer (/apps/custom_submit_action/store_and_email/dialog).

   ![Personnalisation de l’action d’e-mail](assets/step3.png)

1. **Rendez l’action accessible dans la boîte de dialogue Modifier le formulaire adaptatif.**

   Ajoutez les propriétés suivantes au nœud store_and_email :

   * **guideComponentType** de type **String** et valeur **fd/af/components/guidesubmittype**

   * **** guideDataModelof type  **** Chaîne et valeur  **xfa, xsd, basic**

   * **jcr:description** de type **chaîne** et de valeur **Store and Email Action**

1. Ouvrez un formulaire adaptatif. Cliquez sur le bouton **Modifier** en regard de **Démarrer** pour ouvrir la boîte de dialogue **Modifier** du conteneur de formulaires adaptatifs. La nouvelle action s’affiche sous l’onglet **Actions Envoyer**. La sélection de l’action **Store and Email** affiche la configuration ajoutée au nœud dialog.

   ![Boîte de dialogue de configuration de l’action Envoyer](assets/store_and_email_submit_action_dialog.jpg)

1. **Utilisez l’action pour effectuer une tâche.**

   Ajoutez le script post.POST.jsp à votre action. (/apps/custom_submit_action/store_and_mail/).

   Exécutez l&#39;action Stocker prête à l&#39;emploi (script post.POST.jsp). Utilisez l’API [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) fournie par CQ dans votre code. exécutez l’action Stocker . Ajoutez le code suivant à votre fichier JSP :

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Pour envoyer l’e-mail, le code lit l’adresse électronique du destinataire à partir de la configuration. Pour récupérer la valeur de configuration dans le script de l’action, lisez les propriétés de la ressource actuelle à l’aide du code ci-après. Vous pouvez également lire les autres fichiers de configuration.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Utilisez enfin l’API de messagerie CQ pour envoyer l’e-mail. Utilisez la classe [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) pour créer l’objet Email comme illustré ci-dessous :

   >[!NOTE]
   >
   >Vérifiez que le fichier JSP porte le nom post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Sélectionnez l’action dans le formulaire adaptatif. L’action envoie un e-mail et stocke les données.
