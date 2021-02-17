---
title: Utilisation d’un formulaire
seo-title: Utilisation d’un formulaire
description: Affichage et mise à jour d’un formulaire associé à une tâche ou à un point de départ dans l’application AEM Forms
seo-description: Affichage et mise à jour d’un formulaire associé à une tâche ou à un point de départ dans l’application AEM Forms
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 96%

---


# Utilisation d’un formulaire {#working-with-a-form}

Les formulaires activés pour la synchronisation dans l’application sont téléchargés et peuvent être utilisés directement.

Les formulaires sont téléchargés sur votre application et sont disponibles hors ligne. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande sur votre site. L’application est un formulaire adaptatif qui accepte les informations de vos clients, puis les stocke en vue d’une révision. L’administrateur examine le formulaire et crée un formulaire de vérification dans l’instance d’auteur AEM. L’administrateur active la synchronisation du formulaire avec l’application AEM Forms. Si le formulaire de vérification est disponible dans l’application AEM Forms, votre agent de terrain peut utiliser un périphérique mobile pour vérifier les détails de votre client. Le périphérique mobile se synchronise avec le serveur et le formulaire de vérification est chargés dans l’application. Votre agent de terrain peut rendre visite à votre client, vérifier les détails, enregistrer les données en tant que brouillon ou envoyer le formulaire de vérification. Le formulaire est synchronisé avec le serveur chaque fois que votre application est en ligne.

Pour synchroniser votre formulaire dans l’application AEM Forms :

1. Dans l’instance d’auteur, sélectionnez un formulaire, puis cliquez sur **Afficher les propriétés**. 
1. Dans la page des propriétés, cliquez sur **Avancé.** 
1. Sous Avancé, activez l&#39;option : **Synchroniser avec l’application AEM Forms**, puis appuyez sur **Enregistrer**.

Pour synchroniser plusieurs formulaires, dans l’instance d’auteur, sélectionnez plusieurs formulaires dans le gestionnaire de formulaires et appuyez sur **Synchroniser avec l’application AEM Forms**. Lorsque le formulaire est publié, l’application AEM Forms peut se connecter au serveur de publication et récupérer les formulaires.

>[!NOTE]
>
>Formulaires pris en charge :
>
>* Formulaires adaptatifs (sans chargement différé)
>* Formulaires mobiles

>
>
Les pièces jointes au niveau du formulaire ne sont pas prises en charge dans les formulaires adaptatifs extraits dans l’application AEM Forms synchronisée avec le serveur AEM Forms OSGi. Les utilisateurs peuvent ajouter des pièces jointes à un champ si l’auteur a activé les pièces jointes au niveau du formulaire au moment de sa création.

**Ouverture et mise à jour d’un formulaire**

1. Pour ouvrir un formulaire, appuyez sur celui-ci dans l’écran d’accueil.
1. Vous pouvez mettre à jour les champs du formulaire, ajouter des pièces jointes, enregistrer en tant que brouillon et soumettre le formulaire.
