---
title: Ajout de pièces jointes
seo-title: Ajout de pièces jointes
description: Ajouter des photos et saisir des notes à main levée dans votre tâche dans l’application AEM Forms
seo-description: Ajouter des photos et saisir des notes à main levée dans votre tâche dans l’application AEM Forms
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Ajout de pièces jointes{#adding-attachments}

## Adding attachments in forms synced with AEM Forms Workflow server (AEM Forms on JEE) {#adding-annotations}

L’application AEM Forms vous permet de joindre des images, des annotations et des notes de texte à votre formulaire synchronisé avec le serveur AEM Forms JEE. Si votre formulaire est chargé depuis un serveur de flux de travail AEM Forms, vos pièces jointes sont ajoutées au formulaire. You can tap the attachment button ![attachments-app](assets/attachments-app.png) to see all the attachments in a form together. La notification rouge indique le nombre de pièces jointes du formulaire. S’il n’existe aucune pièce jointe dans le formulaire, le bouton rouge des notifications ne s’affiche pas. If there are no attachments in the form, when you tap the attachments button ![attch](assets/attch.png), you get options to attach photos or scribbles.

Vous avez le choix entre :

* **Galerie** : vous permet d’ajouter une image à partir des images enregistrées sur votre périphérique.

* **Appareil photo** : vous permet de prendre une photo et de l’ajouter au formulaire. 

* **Notes** : vous permet d’ajouter une saisie tactile ou une note de texte. Use ![scribble](assets/scribble.png) to add a scribble, and ![keyboard](assets/keyboard.png) to add a text note.

>[!NOTE]
>
>Les pièces jointes ajoutées par un utilisateur sont visibles par les autres utilisateurs de l’application AEM Forms. Les autres utilisateurs ne peuvent pas supprimer les pièces jointes ajoutées par un utilisateur.


### L’écran Pièces jointes {#the-attachments-screen}

To see all the attachments in a place, tap ![attachments-app](assets/attachments-app.png). Vous pouvez ajouter, renommer ou supprimer des pièces jointes ici.

![Toutes les pièces jointes au même endroit](assets/attachments-screen.png)

Vous pouvez utiliser le bouton **+** sur l’écran Pièces jointes pour joindre une autre image, une autre saisie tactile ou un autre texte.

### Ajouter une photo {#adding-a-photograph}

Vous pouvez utiliser l’appareil photo de votre périphérique mobile ou des images enregistrées dans votre périphérique pour joindre une photo dans le formulaire.

1. Tap the attachment button ![attch](assets/attch.png) at the bottom of the window.
1. Appuyez sur **Galerie** ou **Appareil photo** dans la fenêtre contextuelle qui s’affiche.
1. Selon l’option que vous sélectionnez, effectuez ce qui suit :

   1. Si vous sélectionnez **Appareil photo**.

      Prenez une photo. Then tap the **Use** ![use-pic](assets/use-pic.png) button.

      Or tap the **Retake** ![retake](assets/retake.png) button to retake the photograph.

   1. Si vous sélectionnez **Galerie**.

      L’explorateur d’images du périphérique s’affiche. Dans le navigateur d’images de votre périphérique, appuyez sur l’image que vous voulez joindre.

### Ajouter une note {#adding-a-note}

L’option **Notes** vous permet d’ajouter des annotations à main levée et du texte en pièces jointes dans votre formulaire.

1. Tap the attachment button ![attch](assets/attch.png) at the bottom of the window.
1. Appuyez sur **Notes** dans la fenêtre contextuelle qui s’affiche.
1. Dans l’interface utilisateur de Notes qui est lancée, saisissez des annotations à main levée.

   ![Interface de saisie tactile](assets/scribble-ui.png)

   Saisie tactile

   Vous pouvez utiliser les options suivantes dans l’interface de saisie tactile :

   * **Effacer** : efface l’écran.
   * **Bouton Terminé** : joint l’annotation en cours.
   * **Bouton Annuler** : supprime l’annotation en cours et quitte l’interface utilisateur de saisie tactile.
   * ![clavier](assets/keyboard.png): Efface la saisie tactile et vous permet d’ajouter une note de texte.
   ![Clavier de saisie tactile de l’application AEM Forms](assets/keyboard-inapp.png)

## Pièces jointes dans les formulaires synchronisés avec les serveurs AEM Forms sans flux de travaux AEM Forms (AEM Forms sur OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Les pièces jointes pour les formulaires mobiles synchronisés avec les serveurs AEM Forms OSGi fonctionnent comme des serveurs AEM Forms JEE.

Les pièces jointes au niveau du formulaire ne sont pas prises en charge pour les formulaires adaptatifs chargés dans l’application d’un serveur AEM Forms OSGi. Pour joindre des images ou des notes de texte, autorisez les pièces jointes au niveau des champs dans le formulaire au moment de sa création. Faites glisser et déposez le composant de pièce jointe du fichier depuis le navigateur des composants sur le champ.

Dans le cas de formulaires adaptatifs, vous pouvez afficher les fichiers joints dans le document d’enregistrement (DoR). Consultez [Générer un document d’enregistrement pour les formulaires adaptatifs non basés sur XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
