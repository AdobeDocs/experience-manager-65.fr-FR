---
title: Envoi d’un accusé de réception d’envoi de formulaire par courrier électronique
seo-title: Envoi d’un accusé de réception d’envoi de formulaire par courrier électronique
description: AEM Forms permet de configurer l’action Envoyer de courrier électronique qui envoie un accusé de réception à un utilisateur lors de l’envoi du formulaire.
seo-description: AEM Forms permet de configurer l’action Envoyer de courrier électronique qui envoie un accusé de réception à un utilisateur lors de l’envoi du formulaire.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 44%

---


# Envoi d’un accusé de réception d’envoi de formulaire par courrier électronique {#sending-a-form-submission-acknowledgement-via-email}

## Envoi de données de formulaire adaptatif {#adaptive-form-data-submission}

Les formulaires adaptatifs fournissent plusieurs flux de travaux [d’actions Envoyer](../../forms/using/configuring-submit-actions.md) prêts à l’emploi pour envoyer les données de formulaire à différents points de terminaison.

Par exemple, l’action d’envoi **[!UICONTROL Envoyer un courrier électronique]** envoie un courrier électronique lors de l’envoi réussi d’un formulaire adaptatif. Elle peut également être configurée pour envoyer les données de formulaire et le fichier PDF dans le courrier électronique.

Cet article décrit la procédure pour activer l’action Courrier électronique dans un formulaire adaptatif et les différentes configurations fournies.

>[!NOTE]
>
>Vous pouvez également utiliser l’option **[!UICONTROL Envoyer un PDF par courrier électronique]** pour envoyer le formulaire rempli par courrier électronique en tant que pièce jointe PDF. Les options de configuration disponibles pour cette action sont identiques à celles disponibles pour l&#39;action **[!UICONTROL Envoyer un courrier électronique]**. L’action PDF par courrier électronique est disponible uniquement pour les formulaires adaptatifs basés sur XFA.

## Envoyer une action de courrier électronique {#email-action}

L’action Envoyer un courrier électronique permet à un auteur d’envoyer automatiquement un courrier électronique à un ou plusieurs destinataires lors de l’envoi réussi d’un formulaire adaptatif.

>[!NOTE]
>
>Pour utiliser l&#39;action Envoyer un courrier électronique, vous devez configurer le service de messagerie AEM comme décrit dans [Configuration du service de messagerie](/help/sites-administering/notification.md#configuring-the-mail-service).

### Activation de l’action Envoyer un courrier électronique sur un formulaire adaptatif {#enabling-email-action-on-an-adaptive-form}

1. Ouvrez un formulaire adaptatif en mode **[!UICONTROL modifier]**.

1. Dans l’onglet **[!UICONTROL Contenu]**, appuyez sur **[!UICONTROL Conteneur de formulaire]** et appuyez sur ![configurer](assets/configure-icon.svg) pour vue les propriétés du formulaire adaptatif.

1. Dans la section **[!UICONTROL Envoi]**, sélectionnez **[!UICONTROL Envoyer un courriel]** dans la liste déroulante **[!UICONTROL Action d’envoi]**.

   ![Actions Envoyer](assets/submission-actions.png)

1. Indiquez des ID de courrier électronique valides dans les champs **[!UICONTROL À]**, **[!UICONTROL CC]** et **[!UICONTROL BCC]**.

   Indiquez l’objet et le corps du courrier électronique dans les champs **[!UICONTROL Objet]** et **[!UICONTROL Modèle de courriel]**, respectivement.

   Vous pouvez également spécifier des espaces réservés aux variables dans les champs. Dans ce cas, les valeurs des champs sont traitées lorsque le formulaire est envoyé par un utilisateur final. Pour plus d’informations, voir [Utilisation des noms de champ de formulaire adaptatif pour créer dynamiquement le contenu d’un courrier électronique](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Sélectionnez **[!UICONTROL Inclure les pièces jointes]** si le formulaire contient des pièces jointes et que vous souhaitez joindre ces fichiers au courrier électronique.

   >[!NOTE]
   >
   >Si vous choisissez l’option **[!UICONTROL Envoyer le PDF par courrier électronique]**, vous devez sélectionner l’option Inclure les pièces jointes.

1. Cliquez sur ![enregistrer](assets/save_icon.svg) pour enregistrer les modifications.

### Utilisation des noms de champ de formulaire adaptatif pour créer dynamiquement le contenu d’un courrier électronique {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Dans un formulaire adaptatif, les noms de champ sont appelés espaces réservés. Ils sont remplacés par la valeur du champ après l’envoi du formulaire par un utilisateur.

Dans l&#39;action **[!UICONTROL Envoyer un courrier électronique]**, vous pouvez utiliser des espaces réservés qui sont traités lorsque l&#39;action est exécutée. Cela signifie que les en-têtes du courrier électronique (tels que **[!UICONTROL À]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Objet]**) sont générés lorsque l’utilisateur envoie le formulaire.

Pour définir un espace réservé, spécifiez `${<field name>}` dans un champ après avoir sélectionné **[!UICONTROL Envoyer un courrier électronique]** comme action d’envoi.

Par exemple, si le formulaire contient le champ **[!UICONTROL Adresse électronique]**, nommé `email_addr`, pour capturer l’ID d’adresse électronique d’un utilisateur, vous pouvez spécifier les éléments suivants dans les champs **[!UICONTROL À]**, **[!UICONTROL CC]** ou **[!UICONTROL BCC]**.

`${email_addr}`

Lorsqu’un utilisateur envoie le formulaire, un courrier électronique est envoyé à l’identifiant d’adresse électronique entré dans le champ `email_addr` du formulaire.

>[!NOTE]
>
>Vous pouvez trouver le nom d’un champ dans la boîte de dialogue **[!UICONTROL Modifier]** de ce champ.

Les espaces réservés aux variables peuvent également être utilisés dans les champs **[!UICONTROL Objet]** et **[!UICONTROL Modèle de courriel]**.

Par exemple :

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Les champs des panneaux répétables ne peuvent pas être utilisés en tant qu’espaces réservés aux variables.

