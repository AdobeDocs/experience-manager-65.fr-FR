---
title: Gestion des ressources Adobe Stock dans les ressources AEM
description: Recherchez, récupérez, autorisez et gérez des ressources Adobe Stock depuis AEM. Utilisez les ressources sous licence comme n’importe quelle autre ressource numérique.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 62e82b6da2a5f961acf8cbc30ad29b3c25b1ecef

---


# Utilisation de ressources Adobe Stock dans AEM Assets {#use-adobe-stock-assets-in-aem-assets}

Les entreprises peuvent intégrer leur formule d’abonnement Adobe Stock pour entreprise dans AEM Assets pour s’assurer que les ressources sous licence sont mises à la disposition de leurs projets de création et marketing, tout en bénéficiant des puissantes fonctionnalités de gestion de ressources d’AEM.

Le service Adobe Stock permet aux créateurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de haute qualité et libres de droit pour tous leurs projets de création. Les utilisateurs d’AEM peuvent, en un éclair, rechercher, prévisualiser et acquérir sous licence des ressources Adobe Stock qui sont enregistrées dans AEM, sans quitter l’espace de travail d’AEM.

## Conditions préalables {#prerequisites}

L’intégration requiert un [abonnement Adobe Stock entreprise](https://stockenterprise.adobe.com/) et AEM 6.5 ou une version ultérieure. Pour plus d’informations sur les Service Packs d’AEM 6.5, consultez ces [notes de mise à jour](/help/release-notes/sp-release-notes.md).

## Intégration d’AEM et d’Adobe Stock {#integrate-aem-and-adobe-stock}

Pour permettre à AEM et Adobe Stock de communiquer, créez une configuration IMS et une configuration Adobe Stock dans AEM.

>[!NOTE]
>
>Seuls les administrateurs d’AEM et les administrateurs d’Admin Console d’une entreprise peuvent procéder à l’intégration, dans la mesure où cette opération requiert des privilèges d’administrateur.

### Création d’une configuration d’IMS {#create-an-ims-configuration}

1. Cliquez sur le logo AEM. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations Adobe IMS]**. Cliquez sur **[!UICONTROL Créer]**, puis sélectionnez **[!UICONTROL Solution Cloud]** > **[!UICONTROL Adobe Stock]**.
1. Réutilisez un certificat existant ou sélectionnez **[!UICONTROL Créer un certificat]**.
1. Cliquez sur **[!UICONTROL Créer un certificat]**. Une fois le certificat créé, téléchargez la clé publique. Cliquez sur **[!UICONTROL Suivant]**.
1. Indiquez les valeurs appropriées dans les champs intitulés **[!UICONTROL Titre]**, **[!UICONTROL Serveur d’autorisation]**, **[!UICONTROL Clé API]**, **[!UICONTROL Secret client]** et **[!UICONTROL Charge]**. Voir [Démarrage rapide de l’authentification JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md) pour obtenir des informations détaillées sur la récupération de ces valeurs à partir des E/S Adobe.
1. Ajoutez la clé publique téléchargée à votre compte de service Adobe I/O.

### Création d’une configuration Adobe Stock dans AEM {#create-adobe-stock-configuration-in-aem}

1. Dans l’interface utilisateur d’AEM, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services Cloud]** > **[!UICONTROL Adobe Stock]**.
1. Cliquez sur **[!UICONTROL Créer]** pour créer une configuration et l’associer à votre configuration IMS existante. Sélectionnez `PROD` comme paramètre d’environnement.
1. Ne modifiez pas l’emplacement défini dans le champ **[!UICONTROL Chemin d’accès aux ressources sous licence]**. Ne modifiez pas l’emplacement où vous souhaitez stocker les ressources Adobe Stock.
1. Pour terminer la procédure de création, ajoutez toutes les propriétés requises. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.
1. Ajoutez les utilisateurs ou groupes AEM qui peuvent acquérir les ressources sous licence.

>[!NOTE]
>
>S’il existe plusieurs configurations Adobe Stock, sélectionnez la configuration souhaitée dans le panneau Préférences  utilisateur en cliquant sur le logo AEM dans l’interface utilisateur d’AEM.

## Utilisation et gestion de ressources Adobe Stock dans AEM {#usemanage}

Grâce à cette fonctionnalité, les entreprises peuvent permettre à leurs utilisateurs de travailler avec des ressources Adobe Stock dans AEM Assets. Dans l’interface utilisateur AEM, les utilisateurs peuvent rechercher des ressources Adobe Stock et obtenir des licences pour les ressources requises.

Une fois qu’une ressource Adobe Stock est sous licence dans AEM, elle peut être utilisée et gérée comme une ressource standard. Dans AEM, les utilisateurs peuvent rechercher et prévisualiser les ressources ; copier et publier les fichiers ; partager les ressources sur Brand Portal ; accéder aux ressources et les utiliser via l&#39;application de bureau AEM ; etc.

![Recherche de ressources Adobe Stock et filtrage des résultats à partir de l’espace de travail d’AEM](assets/adobe-stock-search-results-workspace.png)

*Figure : Rechercher des ressources Adobe Stock et filtrer les résultats de votre espace de travail AEM*

**A.** Recherchez des fichiers similaires aux fichiers dont l’ID Adobe Stock est fourni. **B.** Recherchez les fichiers correspondant à votre sélection de forme ou d’orientation. **C.** Recherchez l’un des types de ressource pris en charge. **D.** Ouvrez ou réduisez le volet Filtres. **E.** Mettez sous licence et enregistrez la ressource sélectionnée dans AEM. **F.** Enregistrez le fichier dans AEM avec le filigrane. **G.** Explorez sur le site web d’Adobe Stock des fichiers similaires à la ressource sélectionnée. **H.** Affichez les fichiers sélectionnés sur le site web Adobe Stock. **I.** Nombre de fichiers sélectionnés à partir des résultats de la recherche. **J.** Basculez entre le mode Carte et le mode Liste.

### Recherche de ressources {#find-assets}

Vos utilisateurs AEM peuvent rechercher des ressources dans AEM et dans Adobe Stock. Lorsque l’emplacement de recherche n’est pas limité à Adobe Stock, les résultats de la recherche d’AEM et d’Adobe Stock s’affichent.

* Pour rechercher des ressources Adobe Stock, cliquez sur **[!UICONTROL Navigation]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rechercher sur Adobe Stock]**.

* To search for assets across Adobe Stock and AEM Assets, click the search icon ![search_icon](assets/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select Adobe Stock assets.  AEM offre des fonctionnalités de filtrage avancées sur les ressources recherchées, ce qui permet aux utilisateurs de se déconnecter rapidement des ressources requises à l’aide de filtres, tels que les types de ressources prises en charge, l’orientation de l’image et l’état sous licence.

>[!NOTE]
>
>Les ressources recherchées à partir d’Adobe Stock s’affichent simplement dans AEM. Les ressources Adobe Stock sont récupérées et stockées dans le référentiel AEM uniquement après qu’un utilisateur [enregistre une ressource](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [accorde une licence à un fichier](/help/assets/aem-assets-adobe-stock.md#licenseassets). Les ressources déjà stockées dans AEM sont affichées et mises en surbrillance pour simplifier leur référencement et leur accès. Ces fichiers sont également enregistrés avec des métadonnées supplémentaires pour indiquer la source en tant qu’Adobe Stock.

![Filtres de recherche dans AEM et ressources Adobe Stock mises en évidence dans les résultats de recherche](assets/aem-search-filters2.jpg)

*Figure : Filtres de recherche dans AEM et ressources Adobe Stock mises en surbrillance dans les résultats de recherche*

### Enregistrement et affichage des ressources requises {#saveassets}

Sélectionnez une ressource que vous souhaitez enregistrer dans AEM. Cliquez sur Enregistrer dans la barre d’outils supérieure, et indiquez le nom et l’emplacement de la ressource. Les ressources sans licence sont enregistrées en local avec un filigrane.

La prochaine fois que vous rechercherez des ressources, les ressources enregistrées seront mises en évidence avec un badge pour indiquer qu’elles sont disponibles dans AEM Assets.

>[!NOTE]
>
>Les ressources ajoutées récemment sont assorties d’un badge Nouveau au lieu du badge Sous licence.

### Acquisition de ressources sous licence {#licenseassets}

Les utilisateurs peuvent acquérir des ressources Adobe Stock sous licence en utilisant le quota de leur abonnement Adobe Stock pour entreprise. Lorsque vous acquérez une ressource sous licence, elle est enregistrée sans filigrane, et elle peut être recherchée et utilisée dans AEM Assets.

![Boîte de dialogue permettant d’acquérir sous licence et d’enregistrer des ressources Adobe Stock dans AEM Assets](assets/aem-stock_licenseandsave.jpg)

*Figure : Boîte de dialogue permettant d’activer la licence et d’enregistrer des ressources Adobe Stock dans les ressources AEM*

### Accès aux propriétés de ressources et de métadonnées {#access-metadata-and-asset-properties}

Les utilisateurs peuvent accéder aux métadonnées et les prévisualiser, ce qui inclut les propriétés de métadonnées Adobe Stock des ressources enregistrées dans AEM, et ajouter des **[!UICONTROL Références de licence]** pour une ressource. Cependant, les mises à jour apportées à une référence de licence ne sont pas synchronisées entre AEM et le site web d’Adobe Stock.

Les utilisateurs peuvent afficher les propriétés de toutes les ressources, avec et sans licence.

![Affichage des métadonnées et des références de licence des ressources enregistrées, et accès à ces éléments](assets/metadata_properties.jpg)

*Figure : Affichage et accès aux métadonnées et aux références de licence des fichiers enregistrés*

## Limitations connues {#known-limitations}

### L’avertissement d’image éditoriale ne s’affiche pas

Lors de l’acquisition d’une image sous licence, les utilisateurs ne peuvent pas vérifier si elle est destinée uniquement à un usage éditorial. Pour lutter contre une éventuelle utilisation abusive, les administrateurs peuvent désactiver l’accès aux ressources éditoriales à partir d’Admin Console.

### Le type de licence affiché est incorrect

Il est possible qu’un type de licence incorrect soit affiché pour une ressource dans AEM. Les utilisateurs peuvent se connecter au site web d’Adobe Stock pour afficher le type de licence.

### Les métadonnées et les champs de référence ne sont pas synchronisés

Lorsqu’un utilisateur met à jour un champ de référence de licence, les informations sur la référence de licence sont mises à jour dans AEM, mais pas sur le site web d’Adobe Stock. De même, si l’utilisateur met à jour les champs de référence sur le site web d’Adobe Stock, les mises à jour ne sont pas synchronisées dans AEM.

## Ressources connexes {#related-resources}

[Tutoriel visuel sur l’utilisation de ressources Adobe Stock avec AEM Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Aide d’Adobe Stock pour entreprise](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)

[FAQ d’Adobe Stock](https://helpx.adobe.com/stock/faq.html)
