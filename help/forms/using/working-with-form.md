---
title: Utiliser un formulaire
seo-title: Working with a Form
description: Affichage et mise à jour d’un formulaire associé à une tâche ou à un point de départ dans l’application AEM Forms
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: eb71119474f03a969a721c792b6f1ac330f9dbf3
workflow-type: ht
source-wordcount: '414'
ht-degree: 100%

---

# Utiliser un formulaire {#working-with-a-form}

Les formulaires activés pour la synchronisation dans l’application sont téléchargés et peuvent être utilisés directement.

Les formulaires sont téléchargés sur votre application et sont disponibles hors ligne. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande sur votre site. L’application est un formulaire adaptatif qui accepte les informations de vos clients, puis les stocke en vue d’une révision. L’administrateur examine le formulaire et crée un formulaire de vérification dans l’instance d’auteur AEM. L’administrateur active la synchronisation du formulaire avec l’application AEM Forms. Si le formulaire de vérification est disponible dans l’application AEM Forms, votre agent de terrain peut utiliser un périphérique mobile pour vérifier les détails de votre client. Le périphérique mobile se synchronise avec le serveur et le formulaire de vérification est chargés dans l’application. Votre agent de terrain peut rendre visite à votre client, vérifier les détails, enregistrer les données en tant que brouillon ou envoyer le formulaire de vérification. Le formulaire est synchronisé avec le serveur chaque fois que votre application est en ligne.

Pour synchroniser votre formulaire dans l’application AEM Forms :

1. Dans l’instance d’auteur, sélectionnez un formulaire, puis cliquez sur **Afficher les propriétés**. 
1. Dans la page des propriétés, cliquez sur **Avancé.** 
1. Dans la section Avancé, activez l’option : **Synchroniser avec l’application AEM Forms** et appuyez sur **Enregistrer**.

Pour synchroniser plusieurs formulaires, dans l’instance d’auteur, sélectionnez plusieurs formulaires dans le gestionnaire de formulaires et appuyez sur **Synchroniser avec l’application AEM Forms**. Lorsque le formulaire est publié, l’application AEM Forms peut se connecter au serveur de publication et récupérer les formulaires.

Si la synchronisation de votre application AFA (application AEM Forms) échoue, procédez comme suit pour résoudre le problème de synchronisation :

1. Accédez à **https://[server]:[port]/system/console/configMgr**.
1. Recherchez le **[!UICONTROL Gestionnaire d’authentification des jetons Adobe Granite]** et cliquez sur **[!UICONTROL Modifier]**.
1. Sélectionnez l’option **[!UICONTROL Aucun]** dans le menu déroulant de l’attribut **[!UICONTROL Attribut SameSite pour le cookie du jeton de connexion]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

![Synchroniser l’image avec l’application Android AFA](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Formulaires pris en charge :
>
>* Formulaires adaptatifs (sans chargement différé)
>* Formulaires mobiles
>
>Les pièces jointes au niveau du formulaire ne sont pas prises en charge dans les formulaires adaptatifs extraits dans l’application AEM Forms synchronisée avec le serveur AEM Forms OSGi. Les utilisateurs peuvent ajouter des pièces jointes à un champ si l’auteur a activé les pièces jointes au niveau du formulaire au moment de sa création.


**Ouverture et mise à jour d’un formulaire**

1. Pour ouvrir un formulaire, appuyez sur le **[!UICONTROL formulaire]** sur l’écran d’accueil.
1. Vous pouvez mettre à jour les champs du formulaire, ajouter des pièces jointes, enregistrer en tant que brouillon et l’envoyer.
