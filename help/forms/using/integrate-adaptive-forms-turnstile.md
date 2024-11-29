---
title: Comment utiliser Turnstile dans un AEM formulaire adaptatif 6.5 ?
description: Améliorez la sécurité des formulaires grâce au service Turnstile sans effort. Guide détaillé inclus.
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: a4e155de8a4f60d3746cecea110466b1d5d44dbb
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 13%

---

# Connexion de votre environnement AEM Forms à Turnstile {#connect-your-forms-environment-with-turnstile-service}

<!--

<span class="preview"> This feature is under the Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>

-->

<span class="preview"> Cette fonctionnalité est fournie dans le cadre du programme d’adoption précoce. Si vous souhaitez participer à notre programme d&#39;accès anticipé pour cette fonctionnalité, envoyez un email depuis votre adresse officielle à aem-forms-ea@adobe.com pour demander l&#39;accès à </span>.

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatisé ayant pour but de différencier les personnes humaines des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les personnes humaines des programmes automatisés ou des robots. Il présente un test et évalue la réponse de l’utilisateur ou de l’utilisatrice pour déterminer s’il s’agit d’une personne humaine ou d’un robot qui interagit avec le site. Cela empêche l’utilisateur ou l’utilisatrice de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des éléments malveillants.

AEM Forms 6.5 prend en charge les solutions CAPTCHA suivantes :

* [Captcha Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [reCAPTCHA de Google](/help/forms/using/captcha-adaptive-forms.md)
* [Captcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Intégration de l’environnement AEM Forms à Turnstile Captcha

Le captcha de Cloudflare est une mesure de sécurité visant à protéger les formulaires et les sites contre les robots automatisés, les attaques malveillantes, les spams et le trafic automatisé indésirable. Il affiche une case à cocher lors de l’envoi du formulaire pour vérifier qu’il est humain, avant de lui permettre d’envoyer le formulaire.

### Conditions préalables pour intégrer l’environnement AEM Forms avec Turnstile Captcha {#prerequisite}

Pour configurer Turnstile pour AEM Forms, vous devez obtenir la [clé de site Turnstile et la clé secrète](https://developers.cloudflare.com/turnstile/get-started/) à partir du site Web Turnstile.

### Configuration de Turnstile {#steps-to-configure-hcaptcha}

Pour intégrer AEM Forms au service Turnstile, procédez comme suit :

1. Créez un conteneur de configuration sur votre environnement AEM Forms. Un conteneur de configuration contient les configurations cloud utilisées pour connecter AEM Forms à des services externes. Pour créer un conteneur de configuration :
   1. Ouvrez votre environnement AEM Forms.
   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
   1. Dans l’explorateur de configurations, vous sélectionnez un dossier existant ou créez un dossier :
      * Pour créer un **nouveau dossier** et activer les configurations cloud :
         1. Dans l’explorateur de configurations, cliquez sur **[!UICONTROL Créer]**.
         1. Dans la boîte de dialogue Créer une configuration, indiquez un nom, un titre et cochez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Créer]**.
      * Pour activer la configuration du cloud pour un **dossier existant** :
         1. Dans le navigateur de configuration, sélectionnez le dossier et cliquez sur **[!UICONTROL Propriétés]**.
         1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
         1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration.

1. Configurez vos Cloud Service :
   1. Sur votre instance d’auteur AEM, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** et cliquez sur **[!UICONTROL Turnstile]**.
      ![Turnstile en Cloud Service](assets/turnstile-in-ui.png)
   1. Sélectionnez un conteneur de configuration, créé ou mis à jour, comme décrit dans la section précédente. Cliquez sur **[!UICONTROL Créer]**.
      ![Turnstile de configuration](assets/config-hcaptcha.png)
   1. Spécifiez le **[!UICONTROL type de widget]** en tant que type géré, non interactif ou invisible.
   1. Fournissez d’autres détails tels que **[!UICONTROL Titre]**, **[!UICONTROL Nom]**.
   1. Spécifiez la **[!UICONTROL clé du site]** et la **[!UICONTROL clé secrète]** pour le service de Turnstile [obtenue dans la condition préalable](#prerequisite).
   1. Cliquez sur **[!UICONTROL Créer]**.

      ![Configurez le Cloud Service pour connecter votre environnement AEM Forms à Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Les utilisateurs ne doivent pas modifier l’URL de validation JavaScript côté client et l’URL de validation côté serveur, car ils sont déjà préremplis pour la validation de Turnstile.

   Une fois le service de capture de Turnstile configuré, il peut être utilisé dans votre formulaire adaptatif.

## Utiliser le tuteur dans un formulaire adaptatif {#using-turnstile-aem-6.5}

1. Ouvrez votre environnement AEM Forms.
1. Accédez à **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Sélectionnez un formulaire adaptatif, puis cliquez sur **[!UICONTROL Propriétés]**. Dans **[!UICONTROL Conteneur de configuration]**, sélectionnez votre configuration cloud pour Turnstile®.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   Si vous ne disposez pas d’un tel conteneur de configuration, reportez-vous à la section [Connexion de votre environnement AEM Forms à Turnstile](#connect-your-forms-environment-with-turnstile-service) pour savoir comment créer un conteneur de configuration.

   ![Sélectionner Conteneur de configuration](assets/captcha-properties.png)

1. Sélectionnez un formulaire adaptatif et cliquez sur **[!UICONTROL Modifier]** pour ouvrir le formulaire adaptatif dans l’éditeur.
1. A partir de l’explorateur de composants, faites glisser et ajoutez le composant **[!UICONTROL Turnstile de formulaire adaptatif]** sur le formulaire adaptatif.
1. Sélectionnez le composant **[!UICONTROL Turnstile de formulaire adaptatif]** et cliquez sur l’icône ![Icône Propriétés](assets/configure-icon.svg) . Elle ouvre la boîte de dialogue des propriétés. Spécifiez les propriétés suivantes :

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL Titre] :** Spécifiez le titre de votre composant Captcha. vous pouvez identifier facilement un composant de formulaire avec son titre unique dans le formulaire et dans l’éditeur de règles.
   * **[!UICONTROL Paramètres de configuration] :** sélectionnez une configuration cloud configurée pour Turnstile.
   * **[!UICONTROL Message de validation] :** fournissez un message de validation pour valider Captcha lors de l’envoi du formulaire ou lors d’une action de l’utilisateur.
   * **[!UICONTROL Service Captcha] :** Sélectionnez le service CAPTCHA pour l’envoi de votre formulaire, puis sélectionnez Turnstile®.
   * **[!UICONTROL Paramètres de configuration] :** Sélectionnez la configuration de cloud configurée pour Turnstile®.
     >[!NOTE]
     >Vous pouvez avoir plusieurs configurations de cloud dans votre environnement à des fins similaires. Choisissez donc le service avec soin. Si aucun service n’est répertorié, voir [Connexion de votre environnement AEM Forms à Turnstile](#connect-your-forms-environment-with-turnstile-service) pour savoir comment créer un Cloud Service qui connecte votre environnement AEM Forms au service Turnstile.
   * **Message d’erreur :** indiquez le message d’erreur à afficher à l’utilisateur lorsque l’envoi du Captcha échoue.
   * **Taille du captcha :** Vous pouvez sélectionner la taille d’affichage de la boîte de dialogue de défi Captcha®. Utilisez l’option **[!UICONTROL Compact]** pour afficher une petite taille et la **[!UICONTROL Normale]** pour afficher une boîte de dialogue de défi Captcha® de taille relativement importante.

1. Sélectionnez **[!UICONTROL Terminé]**.


Désormais, seuls les formulaires légitimes dans lesquels l’utilisateur parvient à résoudre le problème posé par le service Turnstile sont autorisés pour l’envoi du formulaire.

![Défi Turnstile](assets/turnstile-challenge.png)


## Questions fréquentes

* **Q : Puis-je utiliser plusieurs composants Captcha dans un formulaire adaptatif ?**
* **Réponse :** L’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. En outre, il n’est pas recommandé d’utiliser un composant Captcha dans un fragment ou un panneau marqué pour le chargement différé.

## Voir également {#see-also}

* [Utiliser de CAPTCHA dans les formulaires adaptifs](/help/forms/using/captcha-adaptive-forms.md)
* [Utilisation du captcha dans les formulaires adaptatifs](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)