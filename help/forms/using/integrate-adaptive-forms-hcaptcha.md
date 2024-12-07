---
title: Comment utiliser Captcha&reg; dans un Forms AEM 6.5 ?
description: Améliorez sans effort la sécurité des formulaires grâce au service hCaptcha®. Guide détaillé inclus.
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 6aa7a0a5-bd45-4628-abd0-312a9e6cf6fe
source-git-commit: 25dfe85048184e34cc3afb5e7b08cc0e2f054a01
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 23%

---

# Connexion de votre environnement AEM Forms avec Captcha® {#connect-your-forms-environment-with-hcaptcha-service}

<!--
<span class="preview"> This feature is under the early adopter program. If you’re interested in joining our early access program for this feature, send an email from your official address to aem-forms-ea@adobe.com to request access </span>
-->

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatisé ayant pour but de différencier les personnes humaines des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les personnes humaines des programmes automatisés ou des robots. Il présente un test et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le site. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des éléments malveillants.

Outre le Captcha®, AEM Forms 6.5 prend en charge les solutions CAPTCHA suivantes :

* [reCAPTCHA de Google](/help/forms/using/captcha-adaptive-forms.md)
* [Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## Intégration de l’environnement AEM Forms à®

Le service hCaptcha® protège vos formulaires des robots, spams et violations automatisées. Il propose un test sous forme de widget de case à cocher et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le formulaire. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des activités malveillantes.

AEM 6.5 Adaptive Forms prend en charge Captcha&amp;reg. Vous pouvez l’utiliser pour présenter un défi de widget de case à cocher lors de l’envoi du formulaire.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Conditions préalables pour intégrer l’environnement AEM Forms avec Captcha® {#prerequisite}

Pour configurer Captcha® avec AEM Forms, vous devez obtenir la clé de site [Captcha® et la clé secrète](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) à partir du site web Captcha®.

### Configuration de Captcha® {#steps-to-configure-hcaptcha}

Pour intégrer AEM Forms avec le service Captcha®, procédez comme suit :

1. Créez un conteneur de configuration sur votre environnement AEM Forms, qui contient les configurations cloud utilisées pour se connecter AEM aux services externes. Pour créer un conteneur de configuration :
   1. Ouvrez votre environnement AEM Forms.
   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
   1. Dans l’explorateur de configurations, vous pouvez sélectionner un dossier existant ou créer un dossier :
      * Pour créer un dossier et activer les configurations cloud, procédez comme suit :
         1. Dans l’explorateur de configurations, cliquez sur **[!UICONTROL Créer]**.
         1. Dans la boîte de dialogue Créer une configuration, indiquez un nom, un titre et cochez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Créer]**.
      * Pour activer la configuration du cloud pour un dossier existant :
         1. Dans l’explorateur de configurations, sélectionnez le dossier, puis **[!UICONTROL Propriétés]**.
         1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et quitter la boîte de dialogue.

1. Configurez vos Cloud Service :
   1. Sur votre instance d’auteur AEM, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** et cliquez sur **[!UICONTROL Captcha®]**.
      ![Captcha® dans ui](assets/hcaptcha-in-ui.png)
   1. Sélectionnez un conteneur de configuration, créé ou mis à jour, comme décrit dans la section précédente. Sélectionnez **[!UICONTROL Créer]**.
      ![Captcha de configuration®](assets/config-hcaptcha.png)
   1. Spécifiez **[!UICONTROL Title]**, <!--**[!UICONTROL Name]**--> **[!UICONTROL Clé du site]** et **[!UICONTROL Clé secrète]** pour le service Captcha® [obtenu en prérequis](#prerequisite).
   1. Cliquez sur **[!UICONTROL Créer]**.

      ![Configurez le Cloud Service pour connecter votre environnement AEM Forms à®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Les utilisateurs n’ont pas besoin de modifier [l’URL de validation JavaScript côté client](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) et [l’URL de validation côté serveur](https://docs.hcaptcha.com/#verify-the-user-response-server-side), car ils sont déjà préremplis pour la validation®.

   Une fois le service hCAPTCHA configuré, il peut être utilisé dans votre formulaire adaptatif.

## Utilisation de Captcha® dans un Forms adaptatif {#using-hCaptcha-in-aem-6.5}

1. Ouvrez votre environnement AEM Forms.
1. Accédez à **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Propriétés]**.
1. Dans le **[!UICONTROL Conteneur de configuration]**, sélectionnez votre configuration cloud pour Captcha®.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   Si vous ne disposez pas d’un conteneur de configuration de ce type, reportez-vous à la section [Connexion de votre environnement AEM Forms à avec le Captcha®](#connect-your-forms-environment-with-hcaptcha-service) pour comprendre comment créer un conteneur de configuration.

   ![Sélectionner Conteneur de configuration](/help/forms/using/assets/captcha-properties.png)

1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Modifier]** pour ouvrir le formulaire dans l’éditeur.
1. A partir de l’explorateur de composants, faites glisser et ajoutez le composant **[!UICONTROL Captcha de formulaire adaptatif®]** sur le formulaire adaptatif.
1. Sélectionnez le composant **[!UICONTROL Captcha de formulaire adaptatif®]** et cliquez sur Propriétés ![Icône Propriétés](assets/configure-icon.svg) pour ouvrir la boîte de dialogue Propriétés. Spécifiez les propriétés suivantes :

   ![Captcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL Titre] :** Spécifiez le titre de votre composant Captcha.
   * **[!UICONTROL Message de validation] :** fournissez un message de validation pour votre validation Captcha lors de l’envoi du formulaire ou lors d’une action de l’utilisateur.
   * **[!UICONTROL Service Captcha] :** Sélectionnez le service CAPTCHA pour l’envoi de votre formulaire, ici vous sélectionnez Captcha®.
   * **[!UICONTROL Paramètres de configuration] :** Sélectionnez la configuration de cloud configurée pour Captcha®.
     >[!NOTE]
     >Vous pouvez avoir plusieurs configurations de cloud dans votre environnement à des fins similaires. Choisissez donc le service avec soin. Si aucun service n’est répertorié, reportez-vous à la section [Connexion de votre environnement AEM Forms à avec le Captcha®](#connect-your-forms-environment-with-hcaptcha-service) pour savoir comment créer un Cloud Service qui connecte votre environnement AEM Forms au service Captcha®.
   * **Message d’erreur :** indiquez le message d’erreur à afficher à l’utilisateur lorsque l’envoi du Captcha échoue.
   * **Taille du captcha :** Vous pouvez sélectionner la taille d’affichage de la boîte de dialogue de défi Captcha®. Utilisez l’option **[!UICONTROL Compact]** pour afficher une petite taille et la **[!UICONTROL Normale]** pour afficher une boîte de dialogue de défi Captcha® de taille relativement importante ou **[!UICONTROL Invisible]** pour valider Captcha® sans afficher explicitement le widget de case à cocher dans l’interface utilisateur.

1. Sélectionnez **[!UICONTROL Terminé]**.


Désormais, seuls les formulaires légitimes dans lesquels l’utilisateur réussit à résoudre le problème posé par le service Captcha® sont autorisés pour l’envoi du formulaire. hCaptcha®

**hCaptcha® est une marque déposée d’Intuition Machines, Inc.**


## Questions fréquentes

* **Q : Puis-je utiliser plusieurs composants Captcha dans un formulaire adaptatif ?**
* **Réponse :** L’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. En outre, il n’est pas recommandé d’utiliser un composant Captcha dans un fragment ou un panneau marqué pour le chargement différé.

## Voir également {#see-also}

* [Utiliser de CAPTCHA dans les formulaires adaptifs](/help/forms/using/captcha-adaptive-forms.md)
* [Utilisation de Captcha Turnstile dans les formulaires adaptatifs](/help/forms/using/integrate-adaptive-forms-turnstile.md)
