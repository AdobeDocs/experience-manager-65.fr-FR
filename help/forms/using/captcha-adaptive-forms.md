---
title: Utilisation de CAPTCHA dans les formulaires adaptifs
seo-title: Utilisation de CAPTCHA dans les formulaires adaptifs
description: Découvrez comment configurer le service AEM CAPTCHA ou Google reCAPTCHA dans les formulaires adaptatifs.
seo-description: Découvrez comment configurer le service AEM CAPTCHA ou Google reCAPTCHA dans les formulaires adaptatifs.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 82%

---


# Utilisation de CAPTCHA dans les formulaires adaptifs{#using-captcha-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart, Test public de Turing complètement automatique ayant pour but de différencier les humains des ordinateurs) est un programme couramment utilisé dans les transactions en ligne pour différencier les humains des programmes automatisés ou des robots. Cela pose un défi et évalue la réponse de l’utilisateur pour déterminer s’il s’agit d’un humain ou d’un robot interagissant avec le site. Cela empêche l’utilisateur de continuer si le test échoue et permet de sécuriser les transactions en ligne en empêchant les robots d’envoyer du spam ou des éléments malveillants.

AEM Forms prend en charge CAPTCHA dans les formulaires adaptatifs. Vous pouvez utiliser le service reCAPTCHA de Google pour implémenter CAPTCHA.

>[!NOTE]
>
>* AEM Forms prend en charge uniquement reCaptcha 2. Toute autre version n’est pas prise en charge.
>* CAPTCHA dans les formulaires adaptatifs n’est pas pris en charge dans le mode hors ligne sur l’application AEM Forms.

>



## Configurer le service ReCAPTCHA par Google  {#google-recaptcha}

Les auteurs du formulaire peuvent utiliser le service reCAPTCHA de Google pour mettre en place CAPTCHA dans les formulaires adaptatifs. Il offre des fonctionnalités CAPTCHA avancées pour protéger votre site. Pour plus d’informations sur le fonctionnement de reCAPTCHA, voir [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Pour mettre en place le service reCAPTCHA dans AEM Forms :

1. Obtenez la [paire de clés API reCAPTCHA](https://www.google.com/recaptcha/admin) auprès de Google. Elle comprend une clé de site et une clé secrète.
1. Créez un conteneur de configurations pour les services cloud.

   1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
      * Pour plus d’informations, consultez la documentation de [Navigateur de configuration](/help/sites-administering/configurations.md).
   1. Procédez comme suit pour activer le dossier global pour les configurations cloud ou ignorez cette étape pour créer et configurer un autre dossier pour les configurations de service cloud.

      1. Dans le navigateur de configuration, sélectionnez le dossier **[!UICONTROL global]** et appuyez sur **[!UICONTROL Propriétés]**.

      1. Dans la boîte de dialogue Propriétés de configuration, activez **[!UICONTROL Configurations cloud]**.
      1. Appuyez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et fermer la boîte de dialogue.
   1. Dans le navigateur de configuration, appuyez sur **[!UICONTROL Créer]**.
   1. Dans la boîte de dialogue Créer une configuration, indiquez un titre pour le dossier et activez **[!UICONTROL Configurations cloud]**.
   1. Appuyez sur **[!UICONTROL Créer]** pour créer le dossier activé pour les configurations de service cloud.


1. Configurez le service cloud pour reCAPTCHA.

   1. Sur votre instance d’auteur AEM, accédez à ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Appuyez sur **[!UICONTROL reCAPTCHA]**. La page Configurations s’ouvre. Sélectionnez le conteneur de configurations créé à l’étape précédente et appuyez sur **[!UICONTROL Créer]**.
   1. Spécifiez le nom, la clé du site et la clé secrète pour le service reCAPTCHA et appuyez sur **[!UICONTROL Créer]** pour créer la configuration du service cloud.
   1. Dans cette boîte, spécifiez le site et les clés de site et secrète obtenues à l’étape 1. Appuyez sur **Enregistrer les paramètres**, puis sur **OK** pour terminer la configuration.

   Une fois que le service reCAPTCHA est configuré, il peut être utilisé dans les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation de CAPTCHA dans les formulaires adaptatifs](#using-captcha).

## Utiliser CAPTCHA dans les formulaires adaptatifs  {#using-captcha}

Pour utiliser CAPTCHA dans les formulaires adaptatifs :

1. Ouvrez un formulaire adaptatif en mode d’édition.

   >[!NOTE]
   >
   >Assurez-vous que le conteneur de configurations sélectionné lors de la création d’un formulaire adaptatif contient le service cloud reCAPTCHA. Vous pouvez également modifier les propriétés de formulaire adaptatif pour modifier le conteneur de configurations associé au formulaire.

1. À partir du navigateur de composant, faites glisser et déposez le composant **Captcha** sur le formulaire adaptatif.

   >[!NOTE]
   >
   >L’utilisation de plusieurs composants Captcha dans un formulaire adaptatif n’est pas prise en charge. En outre, il n’est pas recommandé d’utiliser CAPTCHA dans un panneau marqué pour le chargement différé ou dans un fragment.

   >[!NOTE]
   >
   >Captcha est sensible au facteur temps et expire dans la minute. Par conséquent, il est recommandé de placer le composant Captcha juste avant le bouton Envoyer dans le formulaire adaptatif.

1. Sélectionnez le composant Captcha que vous avez ajouté et appuyez sur ![cmppr](assets/cmppr.png) pour modifier ses propriétés.
1. Indiquez un titre pour le widget CAPTCHA. La valeur par défaut est **Captcha**. Sélectionnez **Masquer le titre** si vous ne voulez pas que le titre apparaisse.
1. Dans la liste déroulante **Service Captcha**, sélectionnez **reCaptcha** pour activer le service reCAPTCHA si vous l&#39;avez configuré comme décrit dans le service [ReCAPTCHA de Google](#google-recaptcha). Sélectionnez une configuration dans la liste déroulante Paramètres. En outre, sélectionnez la taille **Normal** ou **Compact** pour le widget reCAPTCHA.

   >[!NOTE]
   >
   >Ne sélectionnez pas **[!UICONTROL Par défaut]** dans le menu déroulant Service Captcha puisque le service par défaut AEM CAPTCHA est obsolète.

1. Enregistrez les propriétés.

Le service reCAPTCHA est activé sur le formulaire adaptatif. Vous pouvez prévisualiser le formulaire et voir le fonctionnement de CAPTCHA.
