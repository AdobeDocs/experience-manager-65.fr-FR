---
title: Use Connected Assets to share DAM assets in [!DNL Adobe Experience Manager Sites] authoring workflow.
description: Utilisez les ressources disponibles lors d’un [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] déploiement à distance.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3d2f9bf9f8e83a088769507da8a46f1c9ef4e74e
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 54%

---


# Utilisation des ressources connectées pour partager des ressources DAM dans [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Dans les grandes entreprises, l’infrastructure requise pour créer des sites web peut être distribuée. Il arrive que les fonctionnalités et les ressources numériques de création de sites web permettant de créer ces sites web se trouvent dans différents déploiements. Une des raisons peut être la répartition géographique des déploiements existants qui sont nécessaires pour travailler en tandem. Une autre raison peut être l&#39;acquisition d&#39;infrastructures hétérogènes que la société mère souhaite utiliser ensemble.

Les utilisateurs peuvent créer des pages Web dans [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] est le système de gestion des actifs numériques (DAM) qui fournit les actifs requis pour les sites Web. [!DNL Experience Manager] prend désormais en charge le cas d’utilisation ci-dessus en intégrant [!DNL Sites] et [!DNL Assets].

## Présentation de la fonction Ressources connectées {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Les administrateurs créent une intégration unique d’un déploiement de [!DNL Sites] avec un déploiement différent (distant) de [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Cette fonctionnalité permet de rechercher et d’utiliser aisément plusieurs ressources distantes à la fois. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. Voir le guide [de migration des ressources](/help/assets/assets-migration-guide.md)Experience Manager.

### Conditions préalables et déploiements pris en charge {#prerequisites}

Avant d’utiliser ou de configurer cette fonctionnalité, vérifiez les points suivants :

* Les utilisateurs font partie de groupes d’utilisateurs appropriés sur chaque déploiement.
* Pour les types de déploiement d’Adobe Experience Manager, l’un des critères pris en charge est satisfait. [!DNL Experience Manager] La version 6.5 [!DNL Assets] fonctionne [!DNL Experience Manager] en tant que service Cloud. Pour plus d’informations, voir la fonctionnalité Ressources [connectées dans Experience Manager en tant que service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)Cloud.

   |  | [!DNL Sites]as a Cloud Service | [!DNL Experience Manager] 6.5 [!DNL Sites] sur AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] sur site |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a Cloud Service ** | Pris en charge | Pris en charge | Pris en charge |
   | **[!DNL Experience Manager]6.5[!DNL Assets]sur AMS ** | Pris en charge | Pris en charge | Pris en charge |
   | **[!DNL Experience Manager]6.5[!DNL Assets]sur site ** | pas de prise en charge | pas de prise en charge | pas de prise en charge |

### Formats de fichiers pris en charge {#mimetypes}

Les auteurs peuvent rechercher des images et les types de documents suivants dans l’outil de recherche de contenu et utiliser les ressources recherchées dans l’éditeur de page. Vous pouvez ajouter des documents au composant `Download` ou des images au composant `Image`. Authors can also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. Les formats pris en charge sont les suivants :

* **Formats** d’image : Formats pris en charge par le composant [](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/components/image.html) Image. [!DNL Dynamic Media] les images ne sont pas prises en charge.
* **Formats de document** : Voir [Formats de document de ressources connectées pris en charge](assets-formats.md#supported-document-formats).

### Utilisateurs et groupes concernés {#users-and-groups-involved}

Les différents rôles impliqués pour configurer et utiliser la fonctionnalité et leurs groupes d’utilisateurs correspondants sont décrits ci-dessous. La portée locale est utilisée pour le cas d’utilisation où un auteur crée une page Web. La portée distante est utilisée pour le déploiement DAM qui héberge les ressources requises. The [!DNL Sites] author fetches these remote assets.

| Rôle | Portée | Groupe d’utilisateurs | Nom d’utilisateur de la présentation | Condition requise |
|---|---|---|---|---|
| [!DNL Sites] administrator | Local | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| Utilisateur DAM | Local | `Authors` | `ksaner` | Utilisé pour afficher et dupliquer les ressources récupérées au niveau de `/content/DAM/connectedassets/`. |
| [!DNL Sites] création | Local | `Authors` (avec accès en lecture sur le DAM distant et accès auteur sur le site local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. Les identifiants d’utilisateur DAM `ksaner` sont utilisés. |
| [!DNL Assets] administrator | distant | [!DNL Experience Manager] `administrators` | `admin` sur distant [!DNL Experience Manager] | Configurez le partage des ressources cross-origin (CORS). |
| Utilisateur DAM | distant | `Authors` | `ksaner` sur distant [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| Distributeur DAM (utilisateur technique) | Distant | [!DNL Sites] `Authors` | `ksaner` sur distant [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Ce rôle n’est pas identique aux deux rôles `ksaner` ci-dessus et appartient à un groupe d’utilisateurs différent.  |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. Cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration de ressources connectées]** et fournissez les valeurs suivantes :

   1. [!DNL Assets] l&#39;emplacement est `https://[assets_servername_ams]:[port]`.
   1. Identifiants d’un distributeur DAM (utilisateur technique).
   1. Dans le champ **[!UICONTROL Point de montage]**, entrez le chemin local où récupère les ressources. [!DNL Experience Manager][!DNL Experience Manager] Par exemple, le dossier `remoteassets`.
   1. Ajustez les valeurs du **[!UICONTROL Seuil d’optimisation du transfert du binaire d’origine]** en fonction de votre réseau. Un rendu de ressource dont la taille est supérieure à ce seuil est transféré de façon asynchrone. 
   1. Sélectionnez **[!UICONTROL Banque de données partagée avec les ressources connectées]** si vous utilisez une banque de données pour stocker vos ressources et qu’elle constitue le support de stockage commun aux deux déploiements Dans ce cas, la limite de seuil n’a pas d’importance, car les fichiers binaires de ressources se trouvent dans le magasin de données et ne sont pas transférés.
      ![Exemple de configuration standard pour les ressources connectées](assets/connected-assets-typical-config.png)
   *Figure : Exemple de configuration standard pour les ressources connectées.*

1. Lorsque les ressources sont déjà traitées et que les rendus sont récupérés, désactivez les lanceurs de workflow. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Recherchez les lanceurs avec les workflows comme **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** et **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**.

   1. Sélectionnez le lanceur de workflow puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’actions.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | Avant | Après |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Tous les rendus disponibles sur le déploiement distant sont récupérés lorsque les auteurs récupèrent une ressource. Si vous souhaitez créer d’autres rendus d’une ressource récupérée, ignorez cette étape de configuration. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. Connectez-vous à l’aide des informations d’identification de l’administrateur. Rechercher `Cross-Origin`. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.

   1. To create a CORS configuration for [!DNL Sites] instance, click ![aem_assets_add_icon](assets/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Enregistrez la configuration.

## Utilisation des ressources distantes  {#use-remote-assets}

Les auteurs de site web utilisent l’outil de recherche de contenu pour se connecter à l’instance DAM. Les auteurs peuvent parcourir, rechercher et faire glisser les ressources distantes dans un composant. Pour vous authentifier sur le système DAM distant, conservez les identifiants de l’utilisateur DAM fournis par votre administrateur.

Les auteurs peuvent utiliser les ressources disponibles sur le DAM local et les instances DAM distantes, dans une seule page Web. Utilisez l’outil de recherche de contenu pour basculer entre la recherche sur l’instance DAM locale et sur l’instance DAM distante.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. Toutes les autres balises sont ignorées. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Présentation de l’utilisation {#walk-through-of-usage}

Utilisez la configuration ci-dessus pour découvrir l’expérience de création et comprendre les principes de la fonctionnalité. Utilisez les documents ou les images de votre choix sur le déploiement DAM distant.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. Vous pouvez également accéder à `https://[assets_servername_ams]:[port]/assets.html/content/dam` dans un navigateur. Téléchargez les ressources de votre choix.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Indiquez `ksaner` comme nom d’utilisateur, sélectionnez l’option fournie, puis cliquez sur **[!UICONTROL OK]**.
1. Ouvrez une page du site web We.Retail via **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL fr]** > **[!UICONTROL fr]**. Modifiez la page. Vous pouvez également accéder à `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` dans un navigateur pour modifier une page.

   Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** dans le coin supérieur gauche de la page.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Fournissez les identifiants : `ksaner` comme nom d’utilisateur et `password` comme mot de passe. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Recherchez la ressource que vous avez ajoutée dans DAM. Les ressources distantes s’affichent dans le panneau de gauche. Filtrez les images ou les documents, puis les types de documents pris en charge. Faites glisser les images sur un composant `Image` et les documents sur un composant `Download`.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. La modification par composants est non destructive.

   ![Options de filtrage des types de documents et des images lors de la recherche de fichiers sur DAM distant](assets/filetypes_filter_connected_assets.png)

   *Figure : Options de filtrage des types de documents et des images lors de la recherche de fichiers sur DAM distant.*

1. Un auteur de site est informé de la récupération asynchrone d’une ressource et de l’échec d’une tâche de récupération. Les auteurs peuvent consulter les informations détaillées sur la récupération des tâches et des erreurs dans l’[interface utilisateur](/help/assets/asynchronous-jobs.md) des tâches asynchrones pendant, voire après la création.

   ![Notification concernant la récupération asynchrone en arrière-plan des ressources.](assets/assets_async_transfer_fails.png)

   *Figure : Notification concernant la récupération asynchrone en arrière-plan des ressources.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. Veillez à bien récupérer les fichiers distants au moment de la publication. Pour vérifier l’état de chaque ressource récupérée, reportez-vous à l’interface utilisateur des [tâches asynchrones](/help/assets/asynchronous-jobs.md).

   >[!NOTE]
   >
   >Cette page est publiée même en cas de non-récupération d’une ou plusieurs ressources distantes. Le composant utilisant la ressource distante est publié vide. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Une fois utilisées dans n’importe quelle page web, les ressources distantes récupérées sont consultables et exploitables par toute personne disposant des droits d’accès au dossier local où les ressources récupérées sont stockées (`connectedassets` dans la présentation ci-dessus). Les ressources sont également consultables et visibles dans le référentiel local via l’[!UICONTROL outil de recherche de contenu].

Les ressources récupérées peuvent être utilisées comme n’importe quelle autre ressource locale, à la différence que les métadonnées associées ne peuvent pas être modifiées.

## Restrictions {#limitations}

### Autorisations et gestions des ressources {#permissions-and-managing-assets}

* Les ressources locales ne sont pas synchronisées avec les ressources d’origine sur le déploiement distant. Tout retrait, modification ou suppression d’autorisation sur le déploiement DAM n’est pas propagé en aval.
* Les ressources locales sont des copies en lecture seule. [!DNL Experience Manager]Les composants effectuent des modifications non destructives des ressources. Aucune autre modification n’est autorisée.
* Les ressources récupérées localement sont disponibles à des fins d’écriture uniquement. Les workflows de mise à jour de ressources ne peuvent pas être appliqués et les métadonnées ne peuvent pas être modifiées.
* Seules les images et les formats de document répertoriés sont pris en charge. [!DNL Dynamic Media]Les ressources , ainsi que les fragments de contenu et d’expérience ne sont pas pris en charge.
* Les schémas de métadonnées ne sont pas récupérés.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if authors do not have access to the remote DAM deployment.
* Il n’existe aucune prise en charge API pour personnaliser l’intégration.
* Cette fonctionnalité permet de rechercher et d’utiliser aisément des ressources distantes. Pour rendre de nombreuses ressources distantes disponibles sur le déploiement local en une fois, envisagez de migrer les ressources. Voir le [guide de migration des ressources](assets-migration-guide.md).
* Il n’est pas possible d’utiliser une ressource distante comme miniature de page dans l’interface utilisateur Propriétés [!UICONTROL de] la page. Vous pouvez définir une miniature d’une page Web dans l’interface utilisateur Propriétés [!UICONTROL de la] page à partir de la [!UICONTROL miniature] en cliquant sur [!UICONTROL Sélectionner l’image].

### Configuration et licences {#setup-licensing}

* [!DNL Assets] le déploiement sur [!DNL Adobe Managed Services] est pris en charge.
* [!DNL Sites] peut se connecter à un seul [!DNL Assets] référentiel à la fois.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Utilisation {#usage}

* La seule fonctionnalité prise en charge est la recherche de ressources distantes et le fait de les faire glisser sur la page locale pour créer du contenu.
* L’opération de récupération échoue après 5 secondes. Les auteurs peuvent rencontrer des problèmes lors de la récupération des ressources, par exemple en cas de problèmes de réseau. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Les modifications simples non destructives et les modifications prises en charge par le composant `Image` peuvent être effectuées sur les ressources récupérées. Les ressources sont en lecture seule.

## Résolution des problèmes   {#troubleshoot}

Pour résoudre les problèmes liés aux scénarios d’erreur courants, procédez comme suit :

* If you cannot search for remote assets from the [!UICONTROL Content Finder], recheck and ensure that the required roles and permissions are in place.
* Une ressource récupérée sur un DAM distant risque de ne pas être publiée sur une page web pour les raisons suivantes : il n’existe pas à distance, au même titre que les autorisations appropriées pour la récupérer ; une erreur réseau s’est produite. Assurez-vous que le fichier n&#39;est pas supprimé du DAM distant ou que les autorisations ne sont pas modifiées. Veiller à ce que les conditions préalables appropriées soient remplies. Essayez de rajouter le fichier à la page et de republier. Recherchez dans la [liste des tâches asynchrones](/help/assets/asynchronous-jobs.md) les erreurs de récupération de ressources.
