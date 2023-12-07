---
title: Configurer les messages de validation
description: Découvrez comment spécifier le mode d’affichage des messages de validation et leur emplacement par rapport au formulaire renvoyé dans le navigateur web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 4%

---

# Configurer les messages de validation {#configuring-validation-messages}

Pour les formulaires rendus en HTML, les erreurs de validation de formulaire qui se produisent s’affichent pour l’utilisateur. Vous pouvez personnaliser l’affichage des messages de validation. Selon l’emplacement d’affichage des messages de validation, vous pouvez également contrôler l’emplacement du message dans le formulaire et la taille de la bordure du cadre.

## Définition du mode d’affichage des messages de validation {#specify-how-validation-messages-are-displayed}

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Sortie de validation, dans la liste Création de rapports, sélectionnez l’une des options suivantes :

   **Zone de message :** Pour afficher les messages de validation dans une boîte de dialogue distincte.

   **Image :** Pour afficher les messages de validation dans un cadre de la même fenêtre.

   **Aucun cadre :** Pour afficher les messages de validation dans la même fenêtre. Cette valeur est la valeur par défaut.

   **Via API (avec données) :** Pour renvoyer les messages de validation via l’API (avec des données). Les messages de validation ne s’affichent pas à l’écran.

   **Via API (avec formulaire) :** Pour renvoyer les messages de validation via l’API (avec le formulaire). Les messages de validation ne s’affichent pas à l’écran.

   **Aucun :** Pour ne pas afficher de messages de validation.

1. Cliquez sur Enregistrer.

## Spécifier l’emplacement des messages de validation par rapport au formulaire renvoyé dans le navigateur web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Lorsque la création de rapports est définie sur Cadre ou Aucun cadre, vous pouvez spécifier l’emplacement des messages de validation.

1. Sous Sortie de validation, sélectionnez l’une des options suivantes dans la liste Position :

   **Left :** Pour afficher les messages de validation sur le côté gauche du navigateur web.

   **Droite :** Pour afficher les messages de validation sur le côté droit du navigateur web.

   **Haut**: pour afficher les messages de validation en haut du navigateur web. Cette valeur est la valeur par défaut.

   **Bas**: pour afficher les messages de validation au bas du navigateur web.

1. Cliquez sur Enregistrer.

## Définition de la taille de bordure du cadre {#specify-the-frame-border-size}

Lorsque l’option Rapport est définie sur Cadre, vous pouvez spécifier la taille de la bordure du cadre.

1. Sous Sortie de validation, dans la zone Taille de bordure, saisissez la taille de la bordure du cadre, en pixels.

   La taille de la bordure doit être supérieure ou égale à 0. La valeur par défaut est 1.

1. Cliquez sur Enregistrer.
