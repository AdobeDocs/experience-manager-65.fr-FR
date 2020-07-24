---
title: ' [!DNL Adobe Stock] Gestion des ressources dans [!DNL Adobe Experience Manager Assets].'
description: Recherche, récupération, licence et [!DNL Adobe Stock] gestion de ressources internes [!DNL Adobe Experience Manager]. Utilisez les ressources sous licence comme toute autre ressource numérique.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 29%

---


# Utilisez [!DNL Adobe Stock] des ressources dans [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock]Le service permet aux créateurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de haute qualité et libres de droits pour tous leurs projets de création. [!DNL Experience Manager] les utilisateurs peuvent rapidement trouver, prévisualisation et accorder des licences [!DNL Adobe Stock] aux ressources enregistrées dans [!DNL Experience Manager], sans quitter l’ [!DNL Experience Manager] interface.

## Conditions préalables {#prerequisites}

L&#39;intégration requiert un plan [d&#39;](https://stockenterprise.adobe.com/)entreprise Adobe Stock.

## Intégrer [!DNL Experience Manager] et [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.

### Création d’une configuration d’IMS  {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Cliquez sur **[!UICONTROL Créer]**, puis sélectionnez **[!UICONTROL Solution Cloud]** > **[!UICONTROL Adobe Stock]**.
1. Réutilisez un certificat existant ou sélectionnez **[!UICONTROL Créer un certificat]**.
1. Cliquez sur **[!UICONTROL Créer un certificat]**. Une fois le certificat créé, téléchargez la clé publique. Cliquez sur **[!UICONTROL Suivant]**.
1. Add the downloaded public key to your [!DNL Adobe Developer Console] service account. Cliquez sur **[!UICONTROL Suivant]**. Laissez l’écran Configuration [!UICONTROL du compte technique] Adobe IMS ouvert pour fournir les valeurs sous peu.
1. Accédez à [Adobe Developer Console](https://console.adobe.io). Assurez-vous que votre compte dispose des autorisations d’administrateur pour l’organisation pour laquelle l’intégration est requise.
1. Cliquez sur **[!UICONTROL Créer un nouveau projet]** , puis sur **[!UICONTROL Ajouter l’API]**. Sélectionnez **[!UICONTROL Adobe Stock]** dans la liste des API [!UICONTROL disponibles pour vous]. Sélectionnez Web OAUTH 2.0. Configurez et copiez les différentes valeurs présentées.
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. Voir début [rapide de l’authentification](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)JWT pour obtenir des informations détaillées sur ces valeurs.

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Créer une [!DNL Adobe Stock] configuration dans [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Cliquez sur **[!UICONTROL Créer]** pour créer une configuration et l’associer à votre configuration IMS existante. Sélectionnez `PROD` comme paramètre d’environnement.
1. Ne modifiez pas l’emplacement défini dans le champ **[!UICONTROL Chemin d’accès aux ressources sous licence]**. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Pour terminer la procédure de création, ajoutez toutes les propriétés requises. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel (**[!UICONTROL AEM]** > **[!UICONTROL User Icon]** > **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**).

## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations can allow its users to work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.

![Recherchez des fichiers Adobe Stock et filtrez les résultats de votre espace de travail Adobe Experience Manager.](assets/adobe-stock-search-results-workspace.png)

*Figure : Recherchez[!DNL Adobe Stock]des ressources et filtrez les résultats de votre[!DNL Experience Manager]interface.*

**A.**[!DNL Adobe Stock] Rechercher les ressources semblables à celles dont l’ID est fourni. **B.** Rechercher les ressources correspondant à la forme ou à l’orientation que vous avez sélectionnée. **C.** Recherchez l&#39;un des types de ressources les plus pris en charge **D.** Ouvrez ou réduisez le volet filtres **E.** Obtenez la licence et enregistrez la ressource sélectionnée dans [!DNL Experience Manager] **F. Enregistrez la ressource en  avec un filigrane G.Vue Explorez les ressources du site Web  qui sont similaires à la ressource sélectionnée H. Nombre de ressources sélectionnées à partir des résultats de la recherche J. vue de carte et vue de Liste**[!DNL Experience Manager]****[!DNL Adobe Stock]****[!DNL Adobe Stock]********

### Recherche de ressources {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* Pour rechercher des ressources dans [!DNL Adobe Stock] et [!DNL Experience Manager Assets], cliquez sur Rechercher ![dans](assets/do-not-localize/search_icon.png).

Vous pouvez également commencer à saisir `Location: Adobe Stock` dans la barre de recherche pour sélectionner des ressources [!DNL Adobe Stock] [!DNL Experience Manager] propose des fonctionnalités de filtrage avancé sur les ressources recherchées, ce qui permet aux utilisateurs de cibler rapidement les ressources requises à l’aide de filtres tels que les types de ressources pris en charge, l’orientation d’image et l’état de licence.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] les actifs sont récupérés et stockés dans [!DNL Experience Manager] le référentiel uniquement après qu’un utilisateur [enregistre un actif](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [des licences et enregistre un actif](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![filtres de recherche dans les ressources de Experience Manager et de Adobe Stock surlignées dans les résultats de recherche](assets/aem-search-filters2.jpg)

*Figure : filtres de recherche dans[!DNL Experience Manager]les ressources en surbrillance[!DNL Adobe Stock]dans les résultats de recherche.*

### Enregistrement et affichage des ressources requises {#saveassets}

Sélectionnez une ressource que vous souhaitez enregistrer dans [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. Les ressources sans licence sont enregistrées en local avec un filigrane.

La prochaine fois que vous rechercherez des ressources, les ressources enregistrées seront mises en évidence avec un badge pour indiquer qu’elles sont disponibles dans [!DNL Experience Manager Assets].

>[!NOTE]
>
>Les ressources ajoutées récemment sont assorties d’un badge Nouveau au lieu du badge Sous licence.

### Acquisition de ressources sous licence {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. Lorsque vous acquérez une ressource sous licence, elle est enregistrée sans filigrane, et elle peut être recherchée et utilisée dans [!DNL Experience Manager Assets].

![Boîte de dialogue permettant d’activer la licence et d’enregistrer des actifs Adobe Stock dans des actifs Experience Manager](assets/aem-stock_licenseandsave.jpg)

*Figure : Boîte de dialogue permettant d’activer la licence et d’enregistrer[!DNL Adobe Stock]des fichiers dans[!DNL Experience Manager Assets].*

### Accès aux propriétés de ressources et de métadonnées {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Les utilisateurs peuvent afficher les propriétés de toutes les ressources, avec et sans licence.

![Affichage des métadonnées et des références de licence des ressources enregistrées, et accès à ces éléments](assets/metadata_properties.jpg)

*Figure : Vue et accès aux métadonnées et aux références de licence des ressources enregistrées.*

## Limitations connues {#known-limitations}

* **L’avertissement d’image éditoriale n’est pas affiché**: Lors de la licence d’une image, les utilisateurs ne peuvent pas vérifier si une image est à usage éditorial uniquement. Pour lutter contre une éventuelle utilisation abusive, les administrateurs peuvent désactiver l’accès aux ressources éditoriales à partir d’Admin Console.

* **Le type de licence incorrect s&#39;affiche**: Il est possible qu’un type de licence incorrect s’affiche dans [!DNL Experience Manager] pour un fichier. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Les champs de référence et les métadonnées ne sont pas synchronisés**: Lorsqu’un utilisateur met à jour un champ de référence de licence, les informations de référence de licence sont mises à jour dans [!DNL Experience Manager] mais pas sur le [!DNL Adobe Stock] site Web. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Didacticiel vidéo sur l’utilisation de ressources Adobe Stock avec des ressources Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Aide d’Adobe Stock pour entreprise](https://helpx.adobe.com/fr/enterprise/using/adobe-stock-enterprise.html)
>* [FAQ d’Adobe Stock](https://helpx.adobe.com/fr/stock/faq.html)

