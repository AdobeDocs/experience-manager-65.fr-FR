---
title: Configurer la sortie de formulaire
description: Découvrez comment configurer la sortie de formulaire. Pour configurer la sortie du formulaire et activer la fonction, utilisez les scripts personnalisés avant l’envoi du formulaire.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 38%

---

# Configurer la sortie de formulaire{#configuring-form-output}

## Spécifiez le type de sortie de HTML renvoyée au navigateur web. {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Sortie de formulaire, sélectionnez l’une des options suivantes dans la liste Type de sortie :

   **HTML complet :** Pour effectuer le rendu du formulaire dans des balises de HTML complet (une page de HTML complète). Cette valeur est la valeur par défaut.

   **Corps de formulaire :** pour effectuer le rendu du formulaire avec des balises `<BODY>` (page HTML incomplète).

1. Cliquez sur Enregistrer.

## Spécifiez l’emplacement de rendu du contenu du PDF. {#specify-the-location-where-pdf-content-is-rendered}

1. Sous Sortie de formulaire, sélectionnez l’une des options suivantes dans la liste Rendu au :

   **Client :** Pour effectuer le rendu des PDF forms dans Adobe Acrobat ou Adobe Reader. Le rendu côté client améliore les performances d’AEM forms et s’applique uniquement à la transformation PDFForm.

   **Serveur :** Pour effectuer le rendu des PDF forms sur le serveur d’applications.

   **Automatique :** pour effectuer le rendu du formulaire au format PDF à l’emplacement indiqué par la valeur de configuration `dynamicRender` du formulaire XDP. Cette valeur est la valeur par défaut.

1. Cliquez sur Enregistrer.

## Configuration de l’appel de scripts personnalisés avant envoi de formulaire {#configuring-invocation-of-custom-scripts-before-form-submit}

Pour activer cette fonction, effectuez les étapes suivantes :

1. Connectez-vous à Administration Console.
1. Accédez à **Services** > **formulaires**.
1. Définissez le type de sortie sur Corps de formulaire.
1. Enregistrez les paramètres.
1. Saisissez une variable JavaScript, (__CUSTOM_SCRIPTS_VERSION) dans l’en-tête du code HTML et donnez-lui la valeur 1.

   >[!NOTE]
   >
   >*pour désactiver cette fonction, vous pouvez soit supprimer la variable JavaScript, soit lui donner la valeur 0.*
