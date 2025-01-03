---
title: Configurer la sortie de formulaire
description: Découvrez comment configurer la sortie de formulaire. Pour configurer la sortie du formulaire et activer la fonctionnalité, utilisez les scripts personnalisés avant l’envoi du formulaire.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---

# Configurer la sortie de formulaire{#configuring-form-output}

## Définition du type de sortie HTML renvoyée au navigateur web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Dans la console d’administration, cliquez sur Services > Formulaires.
1. Sous Sortie de formulaire, dans la liste Type de sortie, sélectionnez l’une des options suivantes :

   **HTML complet :** pour effectuer le rendu du formulaire avec des balises HTML complètes (page HTML complète). Il s’agit de la valeur par défaut.

   **Corps de formulaire :** pour effectuer le rendu du formulaire avec des balises `<BODY>` (page HTML incomplète).

1. Cliquez sur Enregistrer.

## Définir l’emplacement du rendu du contenu PDF {#specify-the-location-where-pdf-content-is-rendered}

1. Dans Sortie de formulaire, dans la liste Rendu vers, sélectionnez l’une des options suivantes :

   **Client :** pour effectuer le rendu des PDF forms dans Adobe Acrobat ou Adobe Reader. Le rendu côté client améliore les performances d’AEM Forms et ne s’applique qu’à la transformation PDFForm.

   **Serveur :** pour effectuer le rendu des PDF forms sur le serveur d’applications.

   **Automatique :** pour effectuer le rendu du formulaire au format PDF à l’emplacement indiqué par la valeur de configuration `dynamicRender` du formulaire XDP. Il s’agit de la valeur par défaut.

1. Cliquez sur Enregistrer.

## Configuration de l’appel de scripts personnalisés avant l’envoi de formulaire {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Pour activer cette fonction, effectuez les étapes suivantes :

1. Connectez-vous à la console d’administration.
1. Accédez à **Services** > **Forms**.
1. Définissez le type de sortie sur Corps de formulaire.
1. Enregistrez les paramètres.
1. Saisissez une variable JavaScript, (__CUSTOM_SCRIPTS_VERSION) dans l’en-tête du code HTML et donnez-lui la valeur 1.

   >[!NOTE]
   >
   >*pour désactiver cette fonction, vous pouvez soit supprimer la variable JavaScript, soit lui donner la valeur 0.*
