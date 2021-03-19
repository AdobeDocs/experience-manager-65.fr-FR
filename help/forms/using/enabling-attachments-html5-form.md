---
title: Activation des pièces jointes à un formulaire HTML5
seo-title: Activation des pièces jointes à un formulaire HTML5
description: Par défaut, la prise en charge de pièces jointes des formulaires HTML5 est désactivée.
seo-description: Par défaut, la prise en charge de pièces jointes des formulaires HTML5 est désactivée.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 68%

---


# Activation des pièces jointes à un formulaire HTML5 {#enabling-attachments-for-an-html-form}

Vous pouvez télécharger, prévisualiser, et envoyer des pièces jointes avec des formulaires HTML5. Par défaut, la prise en charge des pièces jointes est désactivée. Pour activer la prise en charge des pièces jointes :

1. Créez un [profil personnalisé](/help/forms/using/custom-profile.md) avec la propriété de chaîne à choix multiple `mfAttachmentOptions`.
1. Dans le profil personnalisé, spécifiez les propriétés `fileSizeLimit`, `multiSelect` et `buttonTex`t pour configurer les options du widget de pièce jointe du fichier. Si nécessaire, vous pouvez également spécifier davantage de propriétés personnalisées.

1. Dans le profil personnalisé, utilisez les configurations suivantes :

   * **multiSelect**-> vrai ou faux (vrai par défaut)
   * **fileSizeLimit** -> value_in_mb (par exemple 5) (2 Mo par défaut)
   * **buttonText** -> Texte du bouton pour la fenêtre contextuelle (&quot;Joindre&quot; par défaut)
   * **accept** -> types de fichiers à accepter (&quot;audio/&amp;ast ;, video/&amp;ast ;, image/&amp;ast ;, text/&amp;ast ;, .pdf&quot; par défaut)

   >[!NOTE]
   >
   >Microsoft Internet Explorer 9 permet aux utilisateurs de joindre un fichier plus volumineux que la limite spécifiée. Il s’agit d’un problème connu.

1. Utilisez [l’éditeur de métadonnées](/help/forms/using/manage-form-metadata.md) pour sélectionner le profil personnalisé que vous avez créé ci-dessus pour les formulaires HTML5.
1. Générez votre modèle de formulaire avec un profil personnalisé et l’icône de pièces jointes apparaît sur la barre d’outils Formulaires.

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

Lorsque les pièces jointes sont activées, le formulaire HTML5 envoie des données multipartie. Les données d’envoi en plusieurs parties comportent deux parties **dataXml** et **pièces jointes**.

>[!NOTE]
>
>Pour une compatibilité ascendante, si l’option `mfAllowAttachments` est désactivée, les formulaires HTML5 n’envoient pas les données à parties multiples. Il envoie un fichier XML de données simples au format **application/xml**.

Si l’indicateur mfAllowAttachments est activé, le [service proxy du service d’envoi](/help/forms/using/service-proxy.md) traite également les données multipartie avec les données Xml et les pièces jointes.
