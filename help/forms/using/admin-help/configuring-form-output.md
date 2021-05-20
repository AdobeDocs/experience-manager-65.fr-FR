---
title: Configuration de la sortie de formulaire
seo-title: Configuration de la sortie de formulaire
description: Découvrez comment configurer la sortie de formulaire.
seo-description: Découvrez comment configurer la sortie de formulaire.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 94%

---

# Configuration de la sortie de formulaire{#configuring-form-output}

## Définition du type de sortie HTML renvoyée au navigateur Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Dans Administration Console, cliquez sur Services > Formulaires.
1. Sous Sortie de formulaire, dans la liste Type de sortie, sélectionnez l’une des options suivantes :

   **HTML complet :** pour effectuer le rendu du formulaire avec des balises HTML complètes (page HTML complète). Il s’agit de la valeur par défaut.

   **Corps du formulaire :** pour effectuer le rendu du formulaire dans  `<BODY>` des balises (page HTML non complète).

1. Cliquez sur Enregistrer.

## Définition de l’emplacement du rendu des contenus au format PDF {#specify-the-location-where-pdf-content-is-rendered}

1. Sous Sortie de formulaire, dans la liste Rendu vers, sélectionnez l’une des options suivantes :

   **Client :** pour effectuer le rendu des formulaires au format PDF dans Adobe Acrobat ou Adobe Reader. Le rendu côté client améliore les performances d’AEM forms et ne s’applique qu’à la transformation PDFForm.

   **Serveur :** pour rendre les formulaires au format PDF sur le serveur d’applications.

   **Automatique :** pour effectuer le rendu du formulaire au format PDF à l’emplacement indiqué par la valeur de configuration `dynamicRender` du formulaire XDP. Il s’agit de la valeur par défaut.

1. Cliquez sur Enregistrer.

## Configuration de l’appel de scripts personnalisés avant l’envoi de formulaire  {#configuring-invocation-of-custom-scripts-before-form-submit}

Pour activer cette fonction, effectuez les étapes suivantes :

1. Connectez-vous à Administration Console.
1. Accédez à **Services** > **Forms**.
1. Définissez le type de sortie sur Corps de formulaire.
1. Enregistrez les paramètres.
1. Saisissez une variable JavaScript, (__CUSTOM_SCRIPTS_VERSION) dans l’en-tête du code HTML et donnez-lui la valeur 1.

   >[!NOTE]
   >
   >*pour désactiver cette fonction, vous pouvez soit supprimer la variable JavaScript, soit lui donner la valeur 0.*
