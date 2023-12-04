---
title: Utiliser de CAPTCHA dans les formulaires adaptifs
description: Découvrez comment configurer le service AEM CAPTCHA ou Google reCAPTCHA dans les formulaires adaptatifs.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 82%

---

# Utilisation de CAPTCHA dans les formulaires adaptifs{#using-captcha-in-adaptive-forms}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html?lang=fr) |
| AEM 6.5 | Cet article |


<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatisé ayant pour but de différencier les personnes humaines des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les personnes humaines des programmes automatisés ou des robots. Il présente un test et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le site. Il empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et contribue à sécuriser les transactions en ligne en empêchant les robots d’envoyer des spams ou des messages malveillants.

AEM Forms prend en charge CAPTCHA dans les formulaires adaptatifs. Vous pouvez utiliser le service reCAPTCHA de Google pour implémenter CAPTCHA.

>[!NOTE]
>
>* AEM Forms prend en charge reCAPTCHA v2 et Enterprise. Toute autre version n’est pas prise en charge.
>* Dans les formulaires adaptatifs, CAPTCHA n’est pas pris en charge dans le mode hors ligne sur l’application AEM Forms.

## Configuration du service reCAPTCHA par Google pour les formulaires adaptatifs {#google-reCAPTCHA}

Les utilisateurs et utilisatrices d’AEM Forms peuvent utiliser le service reCAPTCHA de Google pour mettre en place CAPTCHA dans les formulaires adaptatifs. Il offre des fonctionnalités CAPTCHA avancées pour protéger votre site. Pour plus d’informations sur le fonctionnement de reCAPTCHA, consultez [Google reCAPTCHA](https://developers.google.com/recaptcha/). Le service reCAPTCHA, y compris reCAPTCHA v2 et reCAPTCHA Enterprise, est intégré à AEM Forms. Selon vos besoins, vous pouvez configurer le service reCAPTCHA pour activer :

* [reCAPTCHA Enterprise dans AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 dans AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### Configuration de reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Créez un [projet reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) activé avec l’[API reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [Obtenez](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) l’identifiant du projet.
1. Créez une [clé API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) et une [clé de site pour les sites web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Créez un conteneur de configuration pour les services cloud.

   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**. Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
   1. Procédez comme suit pour activer le dossier global pour les configurations cloud ou ignorez cette étape pour créer et configurer un autre dossier pour les configurations de service cloud.
      1. Dans l’explorateur de configurations, sélectionnez la variable **[!UICONTROL global]** et sélectionnez **[!UICONTROL Propriétés]**.
      1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
      1. Sélectionner **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et quitter la boîte de dialogue.

   1. Dans l’explorateur de configurations, sélectionnez **[!UICONTROL Créer]**.
   1. Dans la boîte de dialogue Créer une configuration, indiquez un titre pour le dossier et activez **[!UICONTROL Configurations cloud]**.
   1. Sélectionner **[!UICONTROL Créer]** pour créer le dossier activé pour les configurations de service cloud.
1. Configurez le service cloud pour reCAPTCHA Enterprise.

   1. Sur votre instance d’auteur Experience Manager, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Sélectionner **[!UICONTROL reCAPTCHA]**. La page de configuration s’ouvre. Sélectionnez le conteneur de configuration créé à l’étape précédente et sélectionnez **[!UICONTROL Créer]**.
   1. Sélectionnez la version reCAPTCHA Enterprise et indiquez le nom, l’ID de projet, la clé du site et la clé API (obtenue aux étapes 2 et 3) pour le service reCAPTCHA Enterprise.
   1. Sélectionnez le type de clé. Le type de clé doit être identique à la clé de site configurée dans le projet google cloud, par exemple : **Clé de site de case à cocher** ou **Clé de site basée sur les scores**.
   1. Spécifiez un score de seuil compris entre 0 et 1 ([Cliquez pour en savoir plus sur le score](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)). Les scores supérieurs ou égaux aux scores de seuil indiquent une interaction humaine, sinon il s’agit d’une interaction avec un robot.

      > Remarque :
      >
      > * Les auteurs et autrices de formulaires peuvent spécifier un score dans la plage adaptée à l’envoi ininterrompu de formulaires.

   1. Sélectionner **[!UICONTROL Créer]** pour créer la configuration du service cloud.

   1. Dans la boîte de dialogue Modifier le composant, spécifiez le nom, l’ID de projet, la clé du site, la clé API (obtenue aux étapes 2 et 3), sélectionnez le type de clé et saisissez le score de seuil. Sélectionner **[!UICONTROL Paramètres d’enregistrement]** puis sélectionnez **[!UICONTROL OK]** pour terminer la configuration.

Une fois que le service reCAPTCHA Enterprise est activé, il peut être utilisé dans les formulaires adaptatifs. Voir [Utilisation du CAPTCHA dans les formulaires adaptifs](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Configurer Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obtenir la [paire de clés de l’API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Elle comprend une **clé de site** et une **clé secrète**.
1. Créez un conteneur de configuration pour les services cloud.
   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**. Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
   1. Procédez comme suit pour activer le dossier global pour les configurations cloud ou ignorez cette étape pour créer et configurer un autre dossier pour les configurations de service cloud.

      1. Dans l’explorateur de configurations, sélectionnez la variable **[!UICONTROL global]** et sélectionnez **[!UICONTROL Propriétés]**.

      1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
      1. Sélectionner **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et quitter la boîte de dialogue.

   1. Dans l’explorateur de configurations, sélectionnez **[!UICONTROL Créer]**.
   1. Dans la boîte de dialogue Créer une configuration, indiquez un titre pour le dossier et activez **[!UICONTROL Configurations cloud]**.
   1. Sélectionner **[!UICONTROL Créer]** pour créer le dossier activé pour les configurations de service cloud.

1. Configurez le service cloud pour reCAPTCHA v2.

   1. Sur votre instance d’auteur AEM, accédez à ![tools-1](assets/tools-1.png) > Déploiement > **Services cloud**.
   1. Sélectionner **[!UICONTROL reCAPTCHA]**. La page de configuration s’ouvre. Sélectionnez le conteneur de configuration créé à l’étape précédente et sélectionnez **[!UICONTROL Créer]**.
   1. Sélectionnez la version reCAPTCHA v2, spécifiez Nom, Clé du site et Clé secrète pour le service reCAPTCHA (Obtenue à l’étape 1), puis sélectionnez **[!UICONTROL Créer]** pour créer la configuration du service cloud.
   1. Dans cette boîte de dialogue, spécifiez le site et les clés de site et secrète obtenues à l’étape 1. Sélectionner **[!UICONTROL Paramètres d’enregistrement]** puis sélectionnez **OK** pour terminer la configuration.

   Une fois que le service reCAPTCHA est configuré, il peut être utilisé dans les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation du CAPTCHA dans les formulaires adaptatifs](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## Utiliser le reCAPTCHA dans les formulaires adaptatifs {#using-reCAPTCHA}

Pour utiliser le reCAPTCHA dans les formulaires adaptatifs :

1. Ouvrez un formulaire adaptatif en mode d’édition.

   >[!NOTE]
   >
   >Assurez-vous que le conteneur de configurations sélectionné lors de la création du formulaire adaptatif contient le service cloud reCAPTCHA. Vous pouvez également changer les propriétés du formulaire adaptatif pour modifier le conteneur de configuration associé au formulaire.

1. À partir du navigateur du composant, faites glisser et déposez le composant **Captcha** sur le formulaire adaptatif.

   >[!NOTE]
   >
   >L’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. En outre, il n’est pas recommandé d’utiliser le CAPTCHA dans un panneau marqué pour le chargement différé ou dans un fragment.

   >[!NOTE]
   >
   >Le Captcha est sensible au temps et expire au bout d’une minute environ. Par conséquent, il est recommandé de placer le composant Captcha juste avant le bouton Soumettre dans le formulaire adaptatif.

1. Sélectionnez le composant Captcha que vous avez ajouté et sélectionnez ![cmppr](assets/cmppr.png) pour modifier ses propriétés.
1. Indiquez un titre pour le widget CAPTCHA. La valeur par défaut est **Captcha**. Sélectionnez **Masquer le titre** si vous ne voulez pas que le titre apparaisse.
1. Dans le menu déroulant **Service Captcha**, sélectionnez **reCAPTCHA** pour activer le service reCAPTCHA si vous l’avez configuré comme décrit dans [Service reCAPTCHA de Google](#google-reCAPTCHA).
1. Sélectionnez une configuration dans la liste déroulante Paramètres.
1. **Si la configuration sélectionnée comporte la version reCAPTCHA Enterprise** :
   1. Vous pouvez sélectionner la configuration cloud reCAPTCHA avec le **type de clé** en tant que **case à cocher**. Dans le type de clé en tant que case à cocher, le message d’erreur personnalisé s’affiche sous forme de message en ligne si la validation du captcha échoue. Vous pouvez sélectionner la taille **[!UICONTROL normale]** et la taille **[!UICONTROL compacte]**.
   1. Vous pouvez sélectionner la configuration cloud reCAPTCHA avec le **type de clé** **basée sur un score**. Dans le type de clé basée sur un score, le message d’erreur personnalisé s’affiche sous forme de message pop-up si la validation du captcha échoue.
   1. Lorsque vous sélectionnez une **[!UICONTROL Référence de liaison]**, les données soumises sont liées, sinon il s’agit de données non liées. Vous trouverez ci-dessous des exemples XML de données non liées et de données liées (avec une référence de liaison telle que SSN), respectivement, lorsqu’un formulaire est soumis.

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **Si la configuration sélectionnée comporte la version reCAPTCHA v2** :
   1. Sélectionnez la taille **[!UICONTROL normale]** ou **[!UICONTROL compacte]** pour le widget reCAPTCHA. Vous pouvez également sélectionner la variable **[!UICONTROL Invisible]** option pour montrer le défi CAPTCHA uniquement en cas de soupçon. Le badge **protégé par reCAPTCHA**, affiché ci-dessous, s’affiche sur les formulaires protégés.

      ![Badge protégé par reCAPTCHA de Google](/help/forms/using/assets/google-recaptcha-v2.png)


   Le service reCAPTCHA est activé sur le formulaire adaptatif. Vous pouvez prévisualiser le formulaire et voir le fonctionnement de CAPTCHA.

1. Enregistrez les propriétés.

>[!NOTE]
> 
> Ne sélectionnez pas **[!UICONTROL Par défaut]** dans le menu déroulant Service Captcha puisque le service par défaut AEM CAPTCHA est obsolète.

### Affichage ou masquage du composant CAPTCHA en fonction de règles {#show-hide-captcha}

Vous pouvez choisir d’afficher ou de masquer le composant CAPTCHA en fonction des règles que vous appliquez à un composant d’un formulaire adaptatif. Sélectionnez le composant, puis sélectionnez ![modifier les règles](assets/edit-rules-icon.svg), puis sélectionnez **[!UICONTROL Créer]** pour créer une règle. Pour plus d’informations sur la création de règles, voir la section [Éditeur de règles](rule-editor.md).

Par exemple, le composant CAPTCHA ne doit s’afficher dans un formulaire adaptatif que si la valeur du champ Valeur monétaire du formulaire est supérieure à 25 000.

Sélectionnez la variable **[!UICONTROL Valeur de devise]** dans le formulaire et créez les règles suivantes :

![Afficher ou masquer des règles](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * Si vous sélectionnez la configuration reCAPTCHA v2 avec la taille comme **[!UICONTROL Invisible]** ou les clés basées sur un score reCAPTCHA Enterprise, l’option afficher/masquer n’est pas applicable.

### Valider le CAPTCHA {#validate-captcha}

Vous pouvez valider le CAPTCHA dans un formulaire adaptatif lorsque vous envoyez le formulaire ou que vous basez la validation CAPTCHA sur des actions et conditions des utilisateurs.

#### Valider le CAPTCHA lors de l’envoi du formulaire {#validation-form-submission}

Pour valider automatiquement un CAPTCHA lorsque vous envoyez un formulaire adaptatif :

1. Sélectionnez le composant CAPTCHA et sélectionnez ![cmppr](assets/configure-icon.svg) pour afficher les propriétés du composant.
1. Dans la section **[!UICONTROL Valider le CAPTCHA]**, sélectionnez **[!UICONTROL Valider le CAPTCHA lors de l’envoi du formulaire]**.
1. Sélectionner ![Terminé](assets/save_icon.svg) pour enregistrer les propriétés du composant.

#### Validation du CAPTCHA sur les actions et conditions des utilisateurs {#validate-captcha-user-action}

Pour valider un CAPTCHA en fonction des conditions et des actions des utilisateurs :

1. Sélectionnez le composant CAPTCHA et sélectionnez ![cmppr](assets/configure-icon.svg) pour afficher les propriétés du composant.
1. Dans la section **[!UICONTROL Valider le CAPTCHA]**, sélectionnez **[!UICONTROL Valider le CAPTCHA sur une action utilisateur]**.
1. Sélectionner ![Terminé](assets/save_icon.svg) pour enregistrer les propriétés du composant.

   >[!NOTE]
   >
   >
   > Si vous sélectionnez la configuration reCAPTCHA v2 avec la taille comme **[!UICONTROL Invisible]** ou les clés basées sur un score reCAPTCHA Enterprise, il n’est pas possible de valider un Captcha sur une action de l’utilisateur ou de l’utilisatrice.

[!DNL Experience Manager Forms] fournit une API `ValidateCAPTCHA` pour valider le CAPTCHA à l’aide de conditions prédéfinies. Vous pouvez appeler l’API à l’aide d’une action d’envoi personnalisée ou en définissant des règles sur les composants d’un formulaire adaptatif.

Voici un exemple d’API `ValidateCAPTCHA` permettant de valider le CAPTCHA à l’aide de conditions prédéfinies :

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
        GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

L’exemple signifie que l’API `ValidateCAPTCHA` valide le CAPTCHA dans le formulaire uniquement si le nombre de chiffres dans la zone numérique spécifiée par l’utilisateur lors du remplissage du formulaire est supérieur à 5.

**Option 1 : utiliser l’API [!DNL Experience Manager Forms] ValidateCAPTCHA pour valider le CAPTCHA à l’aide d’une action d’envoi personnalisée**

Effectuez les étapes suivantes pour utiliser l’API `ValidateCAPTCHA` pour valider le CAPTCHA à l’aide d’une action d’envoi personnalisée :

1. Ajoutez le script qui inclut l’API `ValidateCAPTCHA` à l’action d’envoi personnalisée. Pour plus d’informations sur les actions d’envoi personnalisées, voir [Création d’une action d’envoi personnalisée pour les formulaires adaptatifs](custom-submit-action-form.md).
1. Sélectionnez le nom de l’action d’envoi personnalisée dans la liste déroulante **[!UICONTROL Action d’envoi]** des propriétés **[!UICONTROL Envoi]** d’un formulaire adaptatif.
1. Sélectionner **[!UICONTROL Envoyer]**. Le CAPTCHA est validé en fonction des conditions définies dans l’API `ValidateCAPTCHA` de l’action d’envoi personnalisée.

**Option 2 : utiliser l’API [!DNL Experience Manager Forms] ValidateCAPTCHA pour valider le CAPTCHA sur une action de l’utilisateur avant d’envoyer le formulaire**

Vous pouvez également appeler l’API `ValidateCAPTCHA` en appliquant des règles à un composant d’un formulaire adaptatif.

Par exemple, vous ajoutez un bouton **[!UICONTROL Valider le CAPTCHA]** dans un formulaire adaptatif et créez une règle pour appeler un service lors d’un clic sur un bouton.

La figure suivante illustre comment vous pouvez appeler un service lors d’un clic sur le bouton **[!UICONTROL Valider le CAPTCHA]** :

![Valider le CAPTCHA](assets/captcha-validation1.gif)

Vous pouvez appeler la servlet personnalisée qui inclut l’API `ValidateCAPTCHA` à l’aide de l’éditeur de règles et activer ou désactiver le bouton d’envoi du formulaire adaptatif en fonction du résultat de la validation.

De même, vous pouvez utiliser l’éditeur de règles pour inclure une méthode personnalisée pour valider le CAPTCHA dans un formulaire adaptatif.

<!--
### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` Refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` Refers to the `g_reCAPTCHA_response` that gets generated after solving a CAPTCHA in a form. -->
