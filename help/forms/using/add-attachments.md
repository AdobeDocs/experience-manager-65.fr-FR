---
title: Ajouter des pièces jointes
description: Ajout de photos et de notes par saisie tactile à votre tâche dans l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 35%

---

# Ajouter des pièces jointes{#adding-attachments}

## Ajouter des pièces jointes dans les formulaires synchronisés avec le serveur AEM Forms Workflow (AEM Forms sur JEE) {#adding-annotations}

L’application AEM Forms vous permet de joindre des images, des annotations et des notes de texte à votre formulaire synchronisé avec le serveur AEM Forms JEE. Si votre formulaire est chargé à partir d’un serveur AEM Forms Workflow, vos pièces jointes sont ajoutées au formulaire. Vous pouvez sélectionner le bouton de pièce jointe ![attachments-app](assets/attachments-app.png) pour afficher toutes les pièces jointes d’un formulaire. La notification rouge indique le nombre de pièces jointes du formulaire. Si le formulaire ne compte aucune pièce jointe, le bouton rouge de notification n’est pas visible. Si le formulaire ne contient aucune pièce jointe, lorsque vous sélectionnez le bouton pièces jointes . ![attch](assets/attch.png), vous avez la possibilité de joindre des photos ou des annotations.

Vous avez le choix entre :

* **Galerie** : vous permet d’ajouter une image à partir des images enregistrées sur votre appareil.

* **Appareil photo** : vous permet de prendre une photo et de l’ajouter au formulaire. 

* **Notes** : vous permet d’ajouter une saisie tactile ou une note de texte. Utilisez ![Griffonnage](assets/scribble.png) pour ajouter une note griffonnée et ![Clavier](assets/keyboard.png) pour ajouter une note de texte.

>[!NOTE]
>
>Les pièces jointes ajoutées par un utilisateur sont visibles par les autres utilisateurs de l’application AEM Forms. Les autres utilisateurs ne peuvent pas supprimer les pièces jointes ajoutées par un utilisateur.
>

### L’écran Pièces jointes {#the-attachments-screen}

Pour afficher toutes les pièces jointes à un emplacement, sélectionnez ![attachments-app](assets/attachments-app.png). Vous pouvez ajouter, renommer ou supprimer des pièces jointes ici.

![Toutes les pièces jointes au même endroit](assets/attachments-screen.png)

Vous pouvez utiliser le bouton **+** sur l’écran Pièces jointes pour joindre une autre image, une autre saisie tactile ou un autre texte.

### Ajouter une photo {#adding-a-photograph}

Vous pouvez utiliser l’appareil photo de votre appareil mobile ou des images enregistrées de votre appareil pour joindre une image dans le formulaire.

1. Sélectionner le bouton de pièce jointe ![attch](assets/attch.png) au bas de la fenêtre.
1. Sélectionner **Galerie** ou **Appareil photo** dans la fenêtre contextuelle qui s’affiche.
1. Selon l’option que vous sélectionnez, effectuez les opérations suivantes :

   1. Si vous sélectionnez **Appareil photo**.

      Prenez une photo. Sélectionnez ensuite le **Utilisation** ![use-pic](assets/use-pic.png) bouton .

      Ou sélectionnez l’option **Retake** ![retake](assets/retake.png) pour reprendre la photo.

   1. Si vous sélectionnez **Galerie**.

      L’explorateur d’images de l’appareil s’affiche. Dans le navigateur d’images de votre appareil, sélectionnez l’image à joindre.

### Ajouter une note {#adding-a-note}

L’option **Notes** vous permet d’ajouter des annotations à main levée et du texte en pièces jointes dans votre formulaire.

1. Sélectionner le bouton de pièce jointe ![attch](assets/attch.png) au bas de la fenêtre.
1. Sélectionner **Remarques** dans la fenêtre contextuelle qui s’affiche.
1. Dans l’interface utilisateur de notes qui est lancée, capturez une saisie tactile à main levée.

   ![Interface de saisie tactile](assets/scribble-ui.png)

   Griffonnage

   Vous pouvez utiliser les options suivantes dans l’interface de saisie tactile :

   * **Effacer**: efface l’écran.
   * **Bouton Terminé**: joint la saisie tactile actuelle.
   * **Bouton Annuler**: ignore la saisie tactile actuelle et quitte l’interface utilisateur de saisie tactile.
   * ![Clavier](assets/keyboard.png) : efface la note griffonnée et vous permet d’ajouter une note de texte.

   ![Clavier de saisie tactile de l’application AEM Forms](assets/keyboard-inapp.png)

## Pièces jointes dans les formulaires synchronisés avec les serveurs AEM Forms sans AEM Forms Workflow (AEM Forms sur OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Les pièces jointes pour les formulaires mobiles synchronisés avec les serveurs AEM Forms OSGi fonctionnent de la même manière que les serveurs AEM Forms JEE.

Les pièces jointes au niveau du formulaire ne sont pas prises en charge pour les formulaires adaptatifs chargés dans l’application à partir d’un serveur AEM Forms OSGi. Pour joindre des images ou des notes de texte, activez les pièces jointes au niveau du champ dans le formulaire lorsque vous le créez. Faites glisser et déposez le composant de pièce jointe depuis l’explorateur de composants sur le champ.

S’il existe des formulaires adaptatifs, vous pouvez afficher les fichiers joints dans le document d’enregistrement (DE). Consultez [Générer un document d’enregistrement pour les formulaires adaptatifs non basés sur XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
