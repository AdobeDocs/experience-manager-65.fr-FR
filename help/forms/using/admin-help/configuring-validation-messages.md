---
title: Configuration des messages de validation
seo-title: Configuration des messages de validation
description: Découvrez comment spécifier l’affichage des messages de validation et leur emplacement par rapport au formulaire renvoyé dans le navigateur Web.
seo-description: Découvrez comment spécifier l’affichage des messages de validation et leur emplacement par rapport au formulaire renvoyé dans le navigateur Web.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 100%

---

# Configuration des messages de validation {#configuring-validation-messages}

Pour les formulaires rendus au format HTML, les erreurs de validation de formulaire qui surviennent s’affichent pour consultation par l’utilisateur. Vous pouvez personnaliser le type d’affichage des messages de validation. Selon l’endroit où les messages de validation sont affichés, vous pouvez également contrôler l’emplacement du message dans le formulaire et la taille du cadre.

## Définition du type d’affichage des messages de validation {#specify-how-validation-messages-are-displayed}

1. Dans Administration Console, cliquez sur Services > Formulaires.
1. Sous Sortie de validation, dans la liste Rapport, sélectionnez l’une des options suivantes :

   **Zone de message :** pour que les messages de validation s’affichent dans une boîte de dialogue distincte.

   **Cadre :** pour que les messages de validation s’affichent à l’intérieur d’un cadre dans la même fenêtre.

   **Aucun cadre :** pour que les messages de validation s’affichent dans la même fenêtre. Il s’agit de la valeur par défaut.

   **Via API (avec données) :** pour renvoyer les messages de validation via l’API (avec des données). Les messages de validation ne s’affichent pas à l’écran.

   **Via API (avec formulaire) :** pour renvoyer les messages de validation via l’API (avec le formulaire). Les messages de validation ne s’affichent pas à l’écran.

   **Aucun :** pour que les messages de validation ne s’affichent pas.

1. Cliquez sur Enregistrer.

## Définition de l’emplacement des messages de validation par rapport au formulaire renvoyé dans le navigateur Web  {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Lorsque l’option Rapport est définie sur Cadre ou Aucun cadre, vous pouvez indiquer l’emplacement des messages de validation.

1. Sous Sortie de validation, dans la liste Position, sélectionnez l’une des options suivantes :

   **A gauche :** pour que les messages de validation s’affichent dans la partie gauche du navigateur Web.

   **A droite :** pour que les messages de validation s’affichent dans la partie droite du navigateur Web.

   **En haut :** pour que les messages de validation s’affichent dans la partie supérieure du navigateur Web. Il s’agit de la valeur par défaut.

   **En bas :** pour que les messages de validation s’affichent dans la partie inférieure du navigateur Web.

1. Cliquez sur Enregistrer.

## Définition de la taille du cadre  {#specify-the-frame-border-size}

Lorsque l’option Rapport est définie sur Cadre, vous pouvez indiquer la taille du cadre.

1. Sous Sortie de validation, dans le champ Taille de la bordure, entrez la taille de la bordure du cadre, en pixels.

   La taille de la bordure doit être égale ou supérieure à 0. La valeur par défaut est 1.

1. Cliquez sur Enregistrer.
