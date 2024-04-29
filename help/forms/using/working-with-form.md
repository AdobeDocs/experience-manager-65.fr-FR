---
title: Utiliser un formulaire
description: Affichage et mise à jour d’un formulaire associé à une tâche ou à un point de départ dans l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '414'
ht-degree: 100%

---

# Utiliser un formulaire {#working-with-a-form}

Les formulaires activés pour la synchronisation dans l’application sont téléchargés et peuvent être utilisés directement.

Les formulaires sont téléchargés sur votre application et sont disponibles hors ligne. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande sur votre site. La demande est un formulaire adaptatif qui accepte les informations de vos clientes et clients et les stocke pour révision. L’administrateur ou l’administratrice examine le formulaire et crée un formulaire de vérification dans une instance de création AEM. L’administrateur ou l’administratrice active la synchronisation du formulaire avec l’application AEM Forms. Si le formulaire de vérification est disponible dans l’application AEM Forms, votre agent ou agente de terrain peut utiliser un appareil mobile pour vérifier les détails de votre client ou cliente. L’appareil mobile se synchronise avec le serveur et le formulaire de vérification est chargé dans l’application. Votre agent ou agente de terrain peut rendre visite à votre client ou votre cliente, vérifier les détails, enregistrer les données en tant que brouillon ou envoyer le formulaire de vérification. Le formulaire est synchronisé avec le serveur chaque fois que votre application est en ligne.

Pour synchroniser votre formulaire dans l’application AEM Forms :

1. Dans l’instance d’auteur, sélectionnez un formulaire, puis cliquez sur **Afficher les propriétés**. 
1. Dans la page des propriétés, cliquez sur **Avancé.** 
1. Dans la section Avancé, activez l’option : **Synchroniser avec l’application AEM Forms** et sélectionnez **Enregistrer**.

Pour synchroniser plusieurs formulaires, dans l’instance de création, sélectionnez plusieurs formulaires dans le gestionnaire de formulaires et sélectionnez **Synchroniser avec l’application AEM Forms**. Lorsque le formulaire est publié, l’application AEM Forms peut se connecter au serveur de publication et récupérer les formulaires.

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
>Les pièces jointes au niveau du formulaire ne sont pas prises en charge dans les formulaires adaptatifs extraits dans l’application AEM Forms synchronisée avec le serveur AEM Forms OSGi. Les utilisateurs et les utilisatrices peuvent ajouter des pièces jointes à un champ si l’auteur ou l’autrice a activé les pièces jointes au niveau du formulaire au moment de sa création.


**Ouvrir et mettre à jour un formulaire**

1. Pour ouvrir un formulaire, sélectionnez le **[!UICONTROL formulaire]** sur l’écran d’accueil.
1. Vous pouvez mettre à jour les champs du formulaire, ajouter des pièces jointes, l’enregistrer en tant que brouillon et l’envoyer.
