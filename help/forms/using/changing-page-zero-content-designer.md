---
title: Modification du contenu de la page zéro avec Designer
description: Savez-vous comment modifier le message affiché sur la page zéro d’un PDF XFA lors de son affichage dans une visionneuse de PDF autre qu’Adobe ?
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Forms Designer
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '230'
ht-degree: 100%

---

# Modifier le contenu de la page zéro dans Designer {#changing-page-zero-content-in-designer}

Le contenu de la page zéro s’affiche par défaut lorsqu’un programme de visualisation PDF autre que celui d’Adobe, tel que la visionneuse de fichiers PDF par défaut dans [!DNL Chrome] ou [!DNL Firefox], ne peut pas lire le contenu d’un formulaire PDF/XFA. Le message par défaut de la page zéro est affiché ci-dessous.

![defaultpage0message](assets/defaultpage0message.png)

La version [!DNL AEM Forms] de Designer vous permet de modifier le message affiché sur la page zéro. Pour modifier le message de la page zéro, procédez comme suit :

1. Assurez-vous que la version [!DNL AEM Forms] de Designer est installée. Vous pouvez vérifier la version dans l’écran A propos de Designer.

1. Ouvrez le formulaire dont vous souhaitez modifier le contenu de la page zéro.

1. Cliquez sur **[!UICONTROL Fichier]** > **[!UICONTROL Propriétés du formulaire]**.

1. Dans la boîte de dialogue [!UICONTROL Propriétés du formulaire], cliquez sur le signe ![plus](assets/plus.png) (icône plus) pour ajouter une propriété personnalisée.

1. Spécifiez **_pagezerocontent** en tant que nom de propriété.
1. Ajoutez le nouveau message de la page zéro, au format de texte enrichi, en tant que valeur. Par exemple :


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Enregistrez le formulaire au format PDF.

1. Affichez le formulaire PDF dans le navigateur pour vous assurer que le message a été mis à jour. La valeur d’exemple évoquée ci-dessus apparaît comme suit :

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La propriété personnalisée que vous avez créée peut ne pas s’afficher correctement dans la boîte de dialogue Propriétés du formulaire lors de la réouverture du formulaire. Cependant, elle fonctionne correctement et le formulaire affiche le message mis à jour de la page zéro.
