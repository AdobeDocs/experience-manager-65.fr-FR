---
title: Envoi d’un accusé de réception d’envoi de formulaire par e-mail
description: AEM Forms permet de configurer l’action d’e-mail Envoyer qui envoie un accusé de réception à l’utilisateur ou à l’utilisatrice lors de l’envoi du formulaire.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 100%

---

# Envoi d’un accusé de réception d’envoi de formulaire par e-mail {#sending-a-form-submission-acknowledgement-via-email}

## Envoi de données de formulaire adaptatif {#adaptive-form-data-submission}

Les formulaires adaptatifs fournissent plusieurs workflows d’[actions Envoyer](../../forms/using/configuring-submit-actions.md) prêts à l’emploi pour envoyer les données de formulaire à différents points d’entrée.

Par exemple, l’action **[!UICONTROL Envoyer un e-mail]** envoie un e-mail lorsque l’envoi d’un formulaire adaptatif a été réussi. Elle peut également être configurée pour envoyer les données de formulaire et le fichier PDF dans l’e-mail.

Cet article décrit la procédure pour activer l’action E-mail dans un formulaire adaptatif et les différentes configurations fournies.

>[!NOTE]
>
>Vous pouvez également utiliser l’option **[!UICONTROL Envoyer PDF par e-mail]** pour envoyer le formulaire rempli par e-mail en tant que pièce jointe. Les options de configuration disponibles pour cette action sont identiques à celles proposées pour l’action **[!UICONTROL Envoyer un e-mail]**. L’action PDF par courrier électronique est disponible uniquement pour les formulaires adaptatifs basés sur XFA.

## Action Envoyer un e-mail {#email-action}

L’action Envoyer un e-mail permet à un auteur d’envoyer automatiquement un e-mail à un ou plusieurs destinataires lors de l’envoi réussi d’un formulaire adaptatif.

>[!NOTE]
>
>Pour utiliser l’action Envoyer un e-mail, vous devez configurer le service de messagerie AEM, comme décrit dans la section [Configurer le service de messagerie](/help/sites-administering/notification.md#configuring-the-mail-service).

### Activer l’action Envoyer un e-mail dans un formulaire adaptatif {#enabling-email-action-on-an-adaptive-form}

1. Ouvrez un formulaire adaptatif en mode d’**[!UICONTROL édition]**.

1. Dans l’onglet **[!UICONTROL Contenu]**, sélectionnez **[!UICONTROL Conteneur de formulaires]**, puis ![configurer](assets/configure-icon.svg) pour afficher les propriétés du formulaire adaptatif.

1. Dans la section **[!UICONTROL Envoi]**, sélectionnez **[!UICONTROL Envoyer un e-mail]** dans la liste déroulante **[!UICONTROL Action Envoyer]**.

   ![Actions Envoyer](assets/submission-actions.png)

1. Spécifiez des identifiants d’e-mails valides dans les champs **[!UICONTROL De]**, **[!UICONTROL CC]** et **[!UICONTROL Cci]**.

   Indiquez l’objet et le corps du message dans les champs respectifs **[!UICONTROL Objet]** et **[!UICONTROL Modèle d’e-mail]**.

   Vous pouvez également spécifier des espaces réservés aux variables dans les champs. Dans ce cas, les valeurs des champs sont traitées lorsque le formulaire est envoyé par un utilisateur ou une utilisatrice finale. Pour plus d’informations, consultez [Utilisation des noms de champ de formulaire adaptatif pour créer dynamiquement le contenu d’un e-mail](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Cochez la case **[!UICONTROL Inclure les pièces jointes]** si le formulaire contient des pièces jointes que vous souhaitez joindre à l’e-mail.

   >[!NOTE]
   >
   >Si vous sélectionnez **[!UICONTROL Envoyer un PDF par e-mail]**, vous devez sélectionner l’option Inclure les pièces jointes.

1. Cliquez sur ![Enregistrer](assets/save_icon.svg) pour enregistrer les modifications.

### Utilisation des noms de champ de formulaire adaptatif pour créer dynamiquement le contenu d’un e-mail {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Dans un formulaire adaptatif, les noms de champ sont appelés espaces réservés. Ils sont remplacés par la valeur du champ après l’envoi du formulaire par un utilisateur ou une utilisatrice.

Sous l’action **[!UICONTROL Envoyer un e-mail]**, vous pouvez utiliser des espaces réservés qui sont traités lorsque l’action est effectuée. Cela implique que les en-têtes de l’e-mail (tels que **[!UICONTROL À]**, **[!UICONTROL Cc]**, **[!UICONTROL Cci]**, **[!UICONTROL Objet]**) sont générés lorsque l’utilisateur envoie le formulaire.

Pour définir un espace réservé, spécifiez `${<field name>}` dans un champ après avoir sélectionné **[!UICONTROL Envoyer un e-mail]** comme action Envoyer.

Par exemple, si le formulaire contient le champ **[!UICONTROL Adresse électronique]**, appelé `email_addr` pour capturer l’identifiant d’adresse électronique d’un utilisateur, vous pouvez spécifier les valeurs suivantes dans les champs **[!UICONTROL À]**, **[!UICONTROL Cc]**, ou **[!UICONTROL Cci]**.

`${email_addr}`

Lorsqu’un utilisateur envoie le formulaire, un e-mail est envoyé à l’identifiant d’adresse électronique entré dans le champ `email_addr` du formulaire.

>[!NOTE]
>
>Vous pouvez trouver le nom d’un champ dans la boîte de dialogue **[!UICONTROL Modifier]** de ce champ.

Les espaces réservés aux variables peuvent également être utilisés dans les champs **[!UICONTROL Objet]** et **[!UICONTROL Modèle d’e-mail]**.

Par exemple :

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Les champs des panneaux répétables ne peuvent pas être utilisés en tant qu’espaces réservés aux variables.
