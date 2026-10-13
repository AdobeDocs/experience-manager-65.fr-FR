---
title: Sélecteur de ressources
description: Découvrez comment utiliser le sélecteur de ressources pour rechercher, filtrer, parcourir et récupérer les métadonnées des ressources dans Adobe Experience Manager Assets. Découvrez également comment personnaliser l’interface du sélecteur de ressources.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: 74ec00bc-0862-520e-86dc-e377aeccc141
    internal-label: Search
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 100%
---
# Sélecteur de ressources {#asset-selector}

>[!NOTE]
>
>Le [sélecteur de ressources](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=fr) s’appelait [Asset picker](https://helpx.adobe.com/fr/experience-manager/6-2/assets/using/asset-picker.html) en anglais dans les versions antérieures d’[!DNL Experience Manager].

Le sélecteur de ressources vous permet de parcourir, rechercher et filtrer des ressources dans [!DNL Adobe Experience Manager] Assets. Vous pouvez également récupérer les métadonnées des ressources sélectionnées à l’aide du sélecteur de ressources. Pour personnaliser l’interface du sélecteur de ressources, vous pouvez l’ouvrir avec les paramètres de requête pris en charge. Ces paramètres définissent le contexte du sélecteur de ressources pour un scénario particulier.

Actuellement, vous pouvez transmettre les paramètres de requête `assettype` (*Image/Vidéo/Texte*) et sélectionner `mode` (*Mono/Multiple*) comme informations contextuelles pour le sélecteur de ressources, qui reste intact tout au long de la sélection.

Le sélecteur de ressources utilise le message **HTML5 Window.postMessage** pour envoyer au ou à la destinataire les données correspondant à la ressource sélectionnée.

Le sélecteur de ressources utilise le vocabulaire d’interface Foundation Picker de Granite. Par défaut, le sélecteur de ressources fonctionne en mode de navigation. Cependant, vous pouvez appliquer des filtres à l’aide de l’expérience OmniSearch pour affiner votre recherche de ressources spécifiques.

Vous pouvez intégrer n’importe quelle page web (qu’elle fasse partie ou non du conteneur CQ) au sélecteur de ressources (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Paramètres contextuels {#contextual-parameters}

Vous pouvez transmettre les paramètres de requête suivants dans une URL pour démarrer le sélecteur de ressources dans un contexte spécifique :

| Nom | Valeurs | Exemple | Objectif |
|---|---|---|---|
| suffixe de la ressource (B) | Chemin d’accès au dossier indiqué comme suffixe de la ressource dans l’URL :`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Pour démarrer le sélecteur de ressources avec un dossier particulier sélectionné, par exemple, le dossier `/content/dam/we-retail/en/activities`, l’URL doit se présentée comme suit : `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Si vous avez besoin de sélectionner un dossier en particulier au démarrage du sélecteur de ressources, vous pouvez l’indiquer comme suffixe de ressource. |
| mode | single, multiple | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | En mode multiple, vous pouvez sélectionner plusieurs ressources simultanément à l’aide du sélecteur de ressources. |
| boîte de dialogue | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Utilisez ces paramètres pour ouvrir le sélecteur de ressources en tant que boîte de dialogue Granite. Cette option ne peut être appliquée qu’au démarrage du sélecteur de ressources via le champ Chemin de Granite, en la configurant comme URL pickerSrc. |
| root | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Utilisez cette option pour spécifier le dossier racine du sélecteur de ressources. Dans ce cas, le sélecteur de ressources vous permet de sélectionner uniquement les ressources enfants (directes/indirectes) sous le dossier racine. |
| viewmode | search |  | Pour ouvrir le sélecteur de ressources en mode recherche, avec les paramètres assettype et mimetype. |
| assettype (S) | images, documents, multimedia, archives | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Utilisez cette option pour filtrer les types de ressources en fonction de la valeur transmise. |
| mimetype | Type(s) MIME (`/jcr:content/metadata/dc:format`) d’une ressource (le caractère générique est également pris en charge) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Utilisez-le pour filtrer les ressources en fonction du ou des types MIME |

## Utiliser le sélecteur de ressources {#using-the-asset-selector}

1. Pour accéder à l’interface du sélecteur de ressources, accédez à `https://[AEM_server]:[port]/aem/assetpicker`.
1. Accédez au dossier souhaité, puis sélectionnez une ou plusieurs ressources.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   Vous pouvez également rechercher la ressource souhaitée dans la zone OmniSearch, puis la sélectionner.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Si vous recherchez des ressources à l’aide de la zone OmniSearch, vous pouvez sélectionner différents filtres dans le volet **[!UICONTROL Filtres]** pour affiner votre recherche.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Cliquez sur **[!UICONTROL Sélectionner]** dans la barre d’outils.

>[!MORELIKETHIS]
>
>* [Sélecteur de ressources micro-frontend dans AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=fr)
