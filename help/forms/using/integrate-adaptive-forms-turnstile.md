---
title: Comment utiliser Turnstile dans un formulaire adaptatif AEM 6.5 ?
description: Améliorez sans effort la sécurité des formulaires grâce au service Turnstile. Guide détaillé inclus.
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: ht
source-wordcount: '851'
ht-degree: 100%

---

# Connecter votre environnement AEM Forms à Turnstile {#connect-your-forms-environment-with-turnstile-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">Cette fonctionnalité n’est pas activée par défaut. Vous pouvez écrire à partir de votre adresse officielle à aem-forms-ea@adobe.com pour demander l’accès à la fonctionnalité.</span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatisé ayant pour but de différencier les personnes humaines des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les personnes humaines des programmes automatisés ou des robots. Il présente un test et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le site. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des éléments malveillants.

AEM Forms 6.5 prend en charge les solutions CAPTCHA suivantes :

* [Captcha Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Intégrer le Captcha Turnstile à un environnement AEM Forms

Le Captcha Cloudflare Turnstile est une mesure de sécurité visant à protéger les formulaires et les sites contre les robots automatisés, les attaques malveillantes, les spams et le trafic automatisé indésirable. Il affiche une case à cocher lors de l’envoi de formulaires, ce qui permet de vérifier que l’action est effectuée par de vraies personnes, avant l’envoi effectif.

>[!VIDEO](https://video.tv.adobe.com/v/3440942?captions=fre_fr)

### Conditions préalables à l’intégration du Captcha Turnstile à un environnement AEM Forms {#prerequisite}

Pour configurer Turnstile pour AEM Forms, vous devez obtenir la [clé de site Turnstile et la clé secrète](https://developers.cloudflare.com/turnstile/get-started/) à partir du site web Turnstile.

### Configurer Turnstile {#steps-to-configure-hcaptcha}

Pour intégrer le service Turnstile à AEM Forms, procédez comme suit :

1. Créez un conteneur de configuration dans votre environnement AEM Forms. Un conteneur de configuration contient les configurations cloud utilisées pour connecter AEM Forms à des services externes. Pour créer un conteneur de configuration :
   1. Ouvrez votre environnement AEM Forms.
   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
   1. Dans l’explorateur de configuration, sélectionnez un dossier existant ou créez-en un :
      * Pour créer un **nouveau dossier** et activer les configurations cloud :
         1. Dans l’explorateur de configuration, sélectionnez **[!UICONTROL Créer]**.
         1. Dans la boîte de dialogue Créer une configuration, spécifiez un nom et un titre et cochez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Créer]**.
      * Pour activer la configuration cloud pour un **dossier existant** :
         1. Dans l’explorateur de configuration, sélectionnez le dossier et cliquez sur **[!UICONTROL Propriétés]**.
         1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** pour appliquer la configuration.

1. Configurer vos services cloud :
   1. Dans votre instance de création AEM, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Services cloud]**, puis cliquez sur **[!UICONTROL Turnstile]**.
      ![Turnstile dans Cloud Services](assets/turnstile-in-ui.png)
   1. Sélectionnez un conteneur de configuration, créé ou mis à jour, comme décrit dans la section précédente. Cliquez sur **[!UICONTROL Créer]**.
      ![Configuration de Turnstile](assets/config-hcaptcha.png)
   1. Spécifiez le **[!UICONTROL Type de widget]** comme managé, non interactif ou invisible.
   1. Fournissez d’autres détails tels que le **[!UICONTROL Titre]** et le **[!UICONTROL Nom]**.
   1. Spécifiez la **[!UICONTROL clé de site]** et la **[!UICONTROL clé secrète]** pour le service Turnstile [ obtenues précédemment](#prerequisite).
   1. Cliquez sur **[!UICONTROL Créer]**.

      ![Configurer le service cloud pour connecter votre environnement AEM Forms à Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Les utilisateurs et les utilisatrices n’ont pas besoin de modifier l’URL de validation JavaScript côté client et l’URL de validation côté serveur, car elles sont déjà préremplies pour la validation Turnstile.

   Une fois le service Turnstile configuré, vous pouvez l’utiliser dans vos formulaires adaptatifs.

## Utiliser Turnstile dans un formulaire adaptatif {#using-turnstile-aem-6.5}

1. Ouvrez votre environnement AEM Forms.
1. Accédez à **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Propriétés]**. Dans le **[!UICONTROL Conteneur de configuration]**, sélectionnez le conteneur de configuration contenant la configuration cloud qui connecte AEM Forms à Turnstile.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   Si vous ne disposez pas d’un conteneur de configuration pour Turnstile, consultez la section [Configurer Turnstile](#configure-turnstile-steps-to-configure-hcaptcha) pour savoir comment créer un conteneur de configuration.

   ![Sélectionner un conteneur de configuration](assets/captcha-properties.png)

1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Modifier]** pour ouvrir votre formulaire adaptatif dans l’éditeur.
1. À partir du navigateur de composant, faites glisser et déposez le composant **[!UICONTROL Captcha]** sur le formulaire adaptatif.
1. Sélectionnez le composant **[!UICONTROL Captcha]**, puis cliquez sur l’icône Propriétés ![icône Propriétés](assets/configure-icon.svg). Cette action ouvre la boîte de dialogue des propriétés. Spécifiez les propriétés requises :

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL Titre] :** indiquez le titre de votre composant Captcha. Vous pouvez identifier facilement un composant de formulaire à l’aide de son titre unique à la fois dans le formulaire et dans l’éditeur de règles.
   * **[!UICONTROL Paramètres de configuration] :** sélectionnez une configuration de cloud configurée pour Turnstile.
   * **[!UICONTROL Message de validation] :** fournissez un message pour la validation du Captcha lors de l’envoi du formulaire ou en cas d’action de la part de l’utilisateur ou de l’utilisatrice.
   * **[!UICONTROL Service Captcha] :** sélectionnez le service CAPTCHA pour l’envoi du formulaire, ici Turnstile®.
   * **[!UICONTROL Paramètres de configuration] :** sélectionnez votre configuration de cloud configurée pour Turnstile®.
     >[!NOTE]
     >Plusieurs configurations de cloud peuvent être définies dans votre environnement dans un but similaire. Par conséquent, faites attention lorsque vous choisissez le service. Si aucun service n’est répertorié, consultez [Connecter votre environnement AEM Forms à Turnstile](#connect-your-forms-environment-with-turnstile-service) pour savoir comment créer un service cloud qui connecte votre environnement AEM Forms au service Turnstile.

   * **[!UICONTROL Message d’erreur] :** spécifiez le message d’erreur à afficher à l’utilisateur ou à l’utilisatrice en cas d’échec de l’envoi du Captcha.
   * **Taille de Captcha :** vous pouvez sélectionner la taille d’affichage de la boîte de dialogue du test hCaptcha®. Utilisez l’option **[!UICONTROL Compact]** pour afficher une boîte de dialogue de test hCaptcha® de petite taille et l’option **[!UICONTROL Normal]** pour afficher un hCaptcha de taille relativement grande.

1. Sélectionnez **[!UICONTROL Terminé]**.


Désormais, seuls les formulaires légitimes, pour lesquels la personne qui remplit le formulaire résout avec succès le problème présenté par le service Turnstile, sont autorisés pour l’envoi de formulaires.

![Test Turnstile](assets/turnstile-challenge.png)


## Questions fréquentes

* **Q : puis-je utiliser plusieurs composants Captcha dans un formulaire adaptatif ?**
* **R :** l’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. De plus, il n’est pas recommandé d’utiliser un composant Captcha dans un fragment ou un panneau marqué pour le chargement différé.

## Voir également {#see-also}

* [Utiliser CAPTCHA dans des formulaires adaptifs](/help/forms/using/captcha-adaptive-forms.md)
* [Utilisation de hCaptcha dans les formulaires adaptatifs](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
