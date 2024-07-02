---
title: Ajouter des pièces jointes
description: Ajouter des photos et saisir des notes à main levée dans votre tâche dans l'application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '562'
ht-degree: 100%

---

# Ajouter des pièces jointes{#adding-attachments}

## Ajouter des pièces jointes dans les formulaires synchronisés avec le serveur AEM Forms Workflow (AEM Forms sur JEE) {#adding-annotations}

L’application AEM Forms vous permet de joindre des images, des annotations et des notes de texte à votre formulaire synchronisé avec le serveur AEM Forms JEE. Si votre formulaire est chargé à partir d’un serveur AEM Forms Workflow, vos pièces jointes sont ajoutées au formulaire. Vous pouvez sélectionner le bouton de pièce jointe ![attachments-app](assets/attachments-app.png) pour afficher toutes les pièces jointes dans un formulaire. La notification rouge indique le nombre de pièces jointes du formulaire. Si le formulaire ne compte aucune pièce jointe, le bouton rouge de notification n’est pas visible. Si le formulaire ne compte aucune pièce jointe, lorsque vous sélectionnez le bouton des pièces jointes ![attch](assets/attch.png), vous avez la possibilité de joindre des photos ou des annotations.

Vous avez le choix entre :

* **Galerie** : vous permet d’ajouter une image à partir des images enregistrées sur votre appareil.

* **Appareil photo** : vous permet de prendre une photo et de l’ajouter au formulaire. 

* **Notes** : vous permet d’ajouter une saisie tactile ou une note de texte. Utilisez ![Griffonnage](assets/scribble.png) pour ajouter une note griffonnée et ![Clavier](assets/keyboard.png) pour ajouter une note de texte.

>[!NOTE]
>
>Les pièces jointes ajoutées par un utilisateur sont visibles par les autres utilisateurs de l’application AEM Forms. Les autres utilisateurs ne peuvent pas supprimer les pièces jointes ajoutées par un utilisateur.
>

### L’écran Pièces jointes {#the-attachments-screen}

Pour afficher toutes les pièces jointes au même endroit, sélectionnez ![attachments-app](assets/attachments-app.png). Vous pouvez ajouter, renommer ou supprimer des pièces jointes ici.

![Toutes les pièces jointes au même endroit](assets/attachments-screen.png)

Vous pouvez utiliser le bouton **+** sur l’écran Pièces jointes pour joindre une autre image, une autre saisie tactile ou un autre texte.

### Ajouter une photographie {#adding-a-photograph}

Vous pouvez utiliser l’appareil photo de votre appareil mobile ou des images enregistrées de votre appareil pour joindre une image dans le formulaire.

1. Sélectionnez le bouton des pièces jointes ![attch](assets/attch.png) au bas de la fenêtre.
1. Sélectionnez **Galerie** ou **Appareil photo** dans la fenêtre contextuelle qui s’affiche.
1. Selon l’option que vous sélectionnez, effectuez les opérations suivantes :

   1. Si vous sélectionnez **Appareil photo**.

      Prenez une photo. Sélectionnez ensuite le bouton **Utiliser** ![use-pic](assets/use-pic.png).

      Alternativement, sélectionnez le bouton **Reprendre** ![retake](assets/retake.png) pour reprendre la photo.

   1. Si vous sélectionnez **Galerie**.

      L’explorateur d’images de l’appareil s’affiche. Dans l’explorateur d’images de votre appareil, sélectionnez l’image que vous voulez joindre.

### Ajouter une note {#adding-a-note}

L’option **Notes** vous permet d’ajouter des annotations à main levée et du texte en pièces jointes dans votre formulaire.

1. Sélectionnez le bouton des pièces jointes ![attch](assets/attch.png) au bas de la fenêtre.
1. Sélectionnez **Notes** dans la fenêtre contextuelle qui s’affiche.
1. Dans l’interface utilisateur de Notes qui est lancée, saisissez des annotations à main levée.

   ![Interface de saisie tactile](assets/scribble-ui.png)

   Griffonnage

   Vous pouvez utiliser les options suivantes dans l’interface de griffonnage :

   * **Effacer** : efface l’écran.
   * **Bouton Terminé** : joint le griffonnage actuel.
   * **Bouton Annuler** : ignore le griffonnage actuel et quitte l’interface utilisateur de griffonnage.
   * ![Clavier](assets/keyboard.png) : efface la note griffonnée et vous permet d’ajouter une note de texte.

   ![Clavier de saisie tactile de l’application AEM Forms](assets/keyboard-inapp.png)

## Pièces jointes dans les formulaires synchronisés avec les serveurs AEM Forms sans AEM Forms Workflow (AEM Forms sur OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Les pièces jointes pour les formulaires mobiles synchronisés avec les serveurs AEM Forms OSGi fonctionnent de la même manière que les serveurs AEM Forms JEE.

Les pièces jointes au niveau du formulaire ne sont pas prises en charge pour les formulaires adaptatifs chargés dans l’application à partir d’un serveur AEM Forms OSGi. Pour joindre des images ou des notes de texte, activez les pièces jointes au niveau du champ dans le formulaire lorsque vous le créez. Faites glisser et déposez le composant de pièce jointe depuis l’explorateur de composants sur le champ.

Pour les formulaires adaptatifs, vous pouvez afficher les fichiers joints dans le document d’enregistrement (DoR). Consultez [Générer un document d’enregistrement pour les formulaires adaptatifs non basés sur XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
