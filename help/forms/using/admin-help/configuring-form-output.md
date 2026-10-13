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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%
---
# Configurer la sortie de formulaire{#configuring-form-output}

## Définir le type de sortie HTML renvoyée au navigateur web {#specify-the-type-of-html-output-returned-to-the-web-browser}

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
1. Déclarez une variable JavaScript, __CUSTOM_SCRIPTS_VERSION, dans l’en-tête du code HTML et définissez sa valeur sur 1.

   >[!NOTE]
   >
   >*pour désactiver cette fonction, vous pouvez soit supprimer la variable JavaScript, soit lui donner la valeur 0.*
