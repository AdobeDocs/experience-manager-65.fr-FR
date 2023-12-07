---
title: Activer les pièces jointes pour un formulaire HTML5
description: Par défaut, la prise en charge des pièces jointes pour les formulaires HTML5 est désactivée.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 85%

---

# Activer les pièces jointes pour un formulaire HTML5 {#enabling-attachments-for-an-html-form}

Vous pouvez télécharger, prévisualiser, et envoyer des pièces jointes avec des formulaires HTML5. Par défaut, la prise en charge des pièces jointes est désactivée. Pour activer la prise en charge des pièces jointes :

1. Créez un [profil personnalisé](/help/forms/using/custom-profile.md) avec une propriété de chaîne MultiSelect `mfAttachmentOptions`. Chaque chaîne de la propriété `mfAttachmentOptions` doit être au format `property=value` pour configurer les options du widget de pièce jointe. `property` et `value` peuvent avoir l’une des valeurs suivantes :

   | Propriété | Valeur |
   |--- |---|
   | multiSelect | vrai ou faux (vrai par défaut) |
   | fileSizeLimit | Nombre en Mo (2 Mo par défaut). Par exemple, 5. |
   | buttonText | Texte des boutons de la fenêtre pop-up (« Joindre » par défaut). |
   | d’accepter ; | liste séparée par des virgules des types de fichiers à accepter (« audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf » par défaut). |

   Par exemple :

   ![configurer les options](assets/mfAttachmentOptions.png)

   Au besoin, vous pouvez également spécifier d’autres options personnalisées pour la propriété `mfAttachmentOptions`.

   >[!NOTE]
   >
   >Dans Microsoft Internet Explorer 9, les utilisateurs peuvent joindre des fichiers supérieurs à la limite spécifiée. C&#39;est un problème connu.

1. Utilisez [l’éditeur de métadonnées](/help/forms/using/manage-form-metadata.md) pour sélectionner le profil personnalisé que vous avez créé ci-dessus pour les formulaires HTML5.
1. Effectuez le rendu de votre modèle de formulaire avec un profil personnalisé et l’icône de pièces jointes apparaît dans la barre d’outils de formulaires.

   >[!NOTE]
   >
   >Hors zone, le portail de formulaires fournit un profil personnalisé avec la fonctionnalité de pièces jointes et de brouillons activée. Pour obtenir plus d’information sur le profil **Save as Draft**, consultez [Enregistrement des formulaires HTML5 en tant que brouillon](/help/forms/using/saving-html5-form-draft.md).

1. Cliquez sur l’icône de pièce jointe, une boîte de dialogue de sélection de pièce jointe apparaît. Recherchez et sélectionnez la pièce jointe et cliquez sur **Joindre**.

   >[!NOTE]
   >
   >Pour afficher l’aperçu d’une pièce jointe, cliquez sur le nom de la pièce jointe. 

   >[!NOTE]
   >
   >L’option Aperçu du fichier n’est pas disponible pour les utilisateurs anonymes.

## Format d’envoi de pièce jointe {#attachment-submission-format}

Lorsque les pièces jointes sont activées, le formulaire HTML5 envoie des données multipartie. Les données multipartie sont envoyées en deux parties : fichier **dataXML** et **pièces jointes**.

>[!NOTE]
>
>Pour une compatibilité ascendante, si l’option `mfAllowAttachments` est désactivée, les formulaires HTML5 n’envoient pas les données multipartie. Ils envoient seulement le fichier de données XML au format **application/xml**.

Si l’indicateur mfAllowAttachments est activé, le [service proxy du service d’envoi](/help/forms/using/service-proxy.md) traite également les données multipartie avec les données Xml et les pièces jointes.
