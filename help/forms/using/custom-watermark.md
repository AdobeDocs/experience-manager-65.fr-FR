---
title: Filigrane personnalisé dans l’aperçu de la lettre PDF
seo-title: Filigrane personnalisé dans l’aperçu de la lettre PDF
description: Découvrez comment créer un filigrane personnalisé dans l’aperçu de la lettre PDF.
seo-description: Découvrez comment créer un filigrane personnalisé dans l’aperçu de la lettre PDF.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Filigrane personnalisé dans l’aperçu de la lettre PDF{#custom-watermark-in-letter-pdf-preview}

## Présentation {#overview}

Dans l’interface utilisateur de création de correspondance, les utilisateurs d’agent prévisualisent la correspondance dans la forme finale dans laquelle elle est envoyée en post-traitement, comme pour l’envoi par courrier électronique ou l’impression.

Pour éviter l’utilisation non autorisée de ces données, les entreprises peuvent ajouter un filigrane à l’aperçu PDF. Le filigrane par défaut, « APERÇU », apparaît sur le PDF.

To enable the watermark in preview PDF, select the **[!UICONTROL Apply Watermark]** During Preview option in **[!UICONTROL Correspondence Management Configurations]** at https://&#39;[server]:[port]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

Vous pouvez utiliser les étapes suivantes pour personnaliser le texte et l’apparence du filigrane :

## Personnalisation du filigrane dans l’aperçu PDF dans l’interface utilisateur de création de correspondance {#customizewatermark-}

1. Go to `https://'[server]:[port]'/[ContextPath]/crx/de` and login as Administrator.
1. In the apps folder, create a folder named **[!UICONTROL previewwatermark]** with path/structure similar to the previewwatermark folder in the libs folder:

   1. Right-click the **previewwatermark** folder at the following path and select **Overlay Node**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/configFiles/previewwatermark

      **Emplacement de l’incrustation :** /apps/

      **Faire correspondre les types de noeud :** Coché

      >[!NOTE]
      >
      >N&#39;apportez pas de modifications dans la branche /libs. Toutes les modifications que vous apportez risquent d’être perdues, car cette branche est exposée aux modifications chaque fois que vous :
      >
      >    
      >    
      >    * Effectuez une mise à niveau sur votre instance
      >    * Appliquez un correctif
      >    * Configurez un feature pack


   1. Cliquez sur **OK**, puis sur **Enregistrer tout**. The **[!UICONTROL previewwatermark]** folder is created in the specified path.



1. Copy and paste the ddx file from &quot;/libs/fd/cm/configFiles/previewwatermark&quot; folder to &quot;/apps/fd/cm/configFiles/previewwatermark&quot; folder and click **[!UICONTROL Save All]**.
1. Apportez les modifications souhaitées dans le fichier ddx sous /apps/fd/cm/configFiles/previewwatermark/.

   ```
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   For information on customizing the watermark appearance, text, and alignment, see Adding and removing watermarks and backgrounds in the [Assembler Service and DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) document.

   >[!NOTE]
   >
   >Dans le fichier ddx, les références au résultat et à la source doivent rester identiques à output.pdf et input.pdf. Le nom du fichier ddx doit également rester identique.

1. Cliquez sur **Enregistrer tout**.

