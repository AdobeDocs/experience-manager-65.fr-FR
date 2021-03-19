---
title: Modification du contenu de la page zéro avec Designer
seo-title: Modification du contenu de la page zéro avec Designer
description: Savez-vous comment modifier le message affiché sur la page zéro d’un PDF XFA ouvert avec un programme de visualisation PDF non Adobe ?
seo-description: Savez-vous comment modifier le message affiché sur la page zéro d’un PDF XFA ouvert avec un programme de visualisation PDF non Adobe ?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Formulaires adaptatifs
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 72%

---


# Modification du contenu de la page zéro avec Designer {#changing-page-zero-content-in-designer}

Le contenu de la page zéro s’affiche par défaut lorsqu’un lecteur non Adobe PDF, tel que la visionneuse PDF par défaut dans [!DNL Chrome] ou [!DNL Firefox], ne peut pas lire le contenu du formulaire PDF/XFA. Le message par défaut de la page zéro est affiché ci-dessous.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] La version de Designer vous permet de modifier le message affiché sur la page zéro. Pour modifier le message de la page zéro, procédez comme suit :

1. Assurez-vous que la version [!DNL AEM Forms] de Designer est installée. Vous pouvez vérifier la version dans l’écran A propos de Designer.

1. Ouvrez le formulaire dont vous souhaitez modifier le contenu de la page zéro.

1. Cliquez sur **[!UICONTROL Fichier]** > **[!UICONTROL Propriétés du formulaire]**.

1. Dans la boîte de dialogue [!UICONTROL Propriétés du formulaire], cliquez sur ![plus](assets/plus.png) (icône Plus) pour ajouter une propriété personnalisée.

1. Spécifiez **_pagezerocontent** en tant que nom de propriété.
1. Ajoutez le nouveau message de la page zéro au format Rich Text, en tant que valeur. Par exemple :


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Enregistrez le formulaire au format PDF.

1. Affichez le formulaire PDF dans le navigateur pour vous assurer que le message a été mis à jour. La valeur d’exemple évoquée ci-dessus apparaît comme suit : 

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La propriété personnalisée créée peut ne pas s’afficher correctement dans la boîte de dialogue Propriétés du formulaire lors de la réouverture du formulaire. Toutefois, le formulaire fonctionne correctement et affiche le message mis à jour sur la page zéro.
