---
title: Comment utiliser hCaptcha® dans AEM Forms 6.5 ?
description: Améliorez sans effort la sécurité des formulaires grâce au service hCaptcha®. Guide détaillé inclus.
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 6aa7a0a5-bd45-4628-abd0-312a9e6cf6fe
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: ht
source-wordcount: '872'
ht-degree: 100%

---

# Connecter votre environnement AEM Forms à hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">Cette fonctionnalité n’est pas activée par défaut. Vous pouvez écrire à partir de votre adresse officielle à aem-forms-ea@adobe.com pour demander l’accès à la fonctionnalité.</span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatisé ayant pour but de différencier les personnes humaines des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les personnes humaines des programmes automatisés ou des robots. Il présente un test et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le site. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des éléments malveillants.

En plus de hCaptcha®, AEM Forms 6.5 prend en charge les solutions CAPTCHA suivantes :

* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## Intégrer hCaptcha® à un environnement AEM Forms

Le service hCaptcha® protège vos formulaires des robots, spams et violations automatisées. Il propose un test sous forme de widget de case à cocher et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le formulaire. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des activités malveillantes.

AEM 6.5 Adaptive Forms prend en charge hCaptcha®. Vous pouvez l’utiliser pour présenter un widget Captcha avec une case à cocher lors de l’envoi d’un formulaire.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Conditions préalables à l’intégration de hCaptcha® à un environnement AEM Forms {#prerequisite}

Pour configurer hCaptcha® avec AEM Forms, vous devez obtenir la clé de site [hCaptcha® et la clé secrète](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) à partir du site web hCaptcha®.

### Configurer hCaptcha® {#steps-to-configure-hcaptcha}

Pour intégrer le service hCaptcha® à AEM Forms, procédez comme suit :

1. Créez un conteneur de configuration dans votre environnement AEM Forms, qui contient les configurations cloud utilisées pour connecter AEM à des services externes. Pour créer un conteneur de configuration :
   1. Ouvrez votre environnement AEM Forms.
   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
   1. Dans l’explorateur de configuration, vous pouvez sélectionner un dossier existant ou en créer un nouveau :
      * Pour créer un dossier et activer les configurations cloud :
         1. Dans l’explorateur de configuration, sélectionnez **[!UICONTROL Créer]**.
         1. Dans la boîte de dialogue Créer une configuration, spécifiez un nom et un titre et cochez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Créer]**.
      * Pour activer la configuration cloud pour un dossier existant :
         1. Dans l’explorateur de configuration, sélectionnez le dossier et cliquez sur **[!UICONTROL Propriétés]**.
         1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et fermer la boîte de dialogue.

1. Configurer vos services cloud :
   1. Dans votre instance de création AEM, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Services cloud]**, puis cliquez sur **[!UICONTROL hCaptcha®]**.
      ![hCaptcha® dans l’interface d’utilisation](assets/hcaptcha-in-ui.png)
   1. Sélectionnez un conteneur de configuration, créé ou mis à jour, comme décrit dans la section précédente. Sélectionnez **[!UICONTROL Créer]**.
      ![Configuration de hCaptcha®](assets/config-hcaptcha.png)
   1. Spécifiez le **[!UICONTROL titre]**, le <!--**[!UICONTROL Name]**-->, la **[!UICONTROL clé de site]** et la **[!UICONTROL clé secrète]** pour le service hCaptcha® [obtenues précédemment](#prerequisite).
   1. Cliquez sur **[!UICONTROL Créer]**.

      ![Configurer le service cloud pour connecter votre environnement AEM Forms à hCaptcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Les utilisateurs et les utilisatrices n’ont pas besoin de modifier l’[URL de validation JavaScript côté client](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) et l’[URL de validation côté serveur](https://docs.hcaptcha.com/#verify-the-user-response-server-side), car elles sont déjà préremplies pour la validation hCaptcha®.

   Une fois le service hCAPTCHA configuré, vous pouvez l’utiliser dans vos formulaires adaptatifs.

## Utiliser hCaptcha® dans un formulaire adaptatif {#using-hCaptcha-in-aem-6.5}

1. Ouvrez votre environnement AEM Forms.
1. Accédez à **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Propriétés]**.
1. Dans le **[!UICONTROL Conteneur de configuration]**, sélectionnez le conteneur de configuration contenant la configuration cloud qui connecte AEM Forms à hCaptcha.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   Si vous ne disposez pas d’un conteneur de configuration pour hCaptcha, consultez la section [Connecter votre environnement AEM Forms à hCaptcha®](#configure-hcaptcha-steps-to-configure-hcaptcha) pour savoir comment créer un conteneur de configuration.

   ![Sélectionner un conteneur de configuration](/help/forms/using/assets/captcha-properties.png)

1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Modifier]** pour ouvrir le formulaire dans l’éditeur.
1. À partir du navigateur de composant, faites glisser et déposez le composant **[!UICONTROL Captcha]** sur le formulaire adaptatif.
1. Sélectionnez le composant **[!UICONTROL Captcha]**, puis cliquez sur Propriétés ![icône Propriétés](assets/configure-icon.svg) pour ouvrir la boîte de dialogue des propriétés. Spécifiez les propriétés requises :

   ![hCaptcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL Titre] :** indiquez le titre de votre composant Captcha.
   * **[!UICONTROL Message de validation] :** fournissez un message de validation pour votre validation Captcha lors de l’envoi du formulaire ou d’une action de l’utilisateur ou de l’utilisatrice.
   * **[!UICONTROL Service Captcha] :** sélectionnez le service CAPTCHA pour l’envoi du formulaire, ici hCaptcha®.
   * **[!UICONTROL Paramètres de configuration] :** sélectionnez votre configuration de cloud configurée pour hCaptcha®.
     >[!NOTE]
     >Plusieurs configurations de cloud peuvent être définies dans votre environnement dans un but similaire. Par conséquent, faites attention lorsque vous choisissez le service. Si aucun service n’est répertorié, consultez [Connecter votre environnement AEM Forms à hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) pour savoir comment créer un service cloud qui connecte votre environnement AEM Forms au service hCaptcha®.

   * **[!UICONTROL Message d’erreur] :** spécifiez le message d’erreur à afficher à l’utilisateur ou à l’utilisatrice en cas d’échec de l’envoi du Captcha.
   * **[!UICONTROL Taille du Captcha] :** vous pouvez sélectionner la taille d’affichage de la boîte de dialogue du test hCaptcha®. Utilisez l’option **[!UICONTROL Compact]** pour afficher une boîte de dialogue de petite taille et l’option **[!UICONTROL Normal]** pour afficher une boîte de dialogue de test hCaptcha® de taille relativement grande. Vous pouvez utiliser l’option **[!UICONTROL Invisible]** pour valider le hCaptcha® sans afficher explicitement le widget avec une case à cocher dans l’interface d’utilisation.

1. Sélectionnez **[!UICONTROL Terminé]**.


Désormais, seuls les formulaires légitimes, pour lesquels la personne qui remplit le formulaire résout avec succès le problème présenté par le service hCaptcha®, sont autorisés pour l’envoi de formulaires.

**hCaptcha® est une marque déposée d’Intuition Machines, Inc.**


## Questions fréquentes

* **Q : puis-je utiliser plusieurs composants Captcha dans un formulaire adaptatif ?**
* **R :** l’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. De plus, il n’est pas recommandé d’utiliser un composant Captcha dans un fragment ou un panneau marqué pour le chargement différé.

## Voir également {#see-also}

* [Utiliser CAPTCHA dans des formulaires adaptifs](/help/forms/using/captcha-adaptive-forms.md)
* [Utilisation de Captcha Turnstile dans les formulaires adaptatifs](/help/forms/using/integrate-adaptive-forms-turnstile.md)
