---
title: Utilisation des ressources connectées pour partager des ressources DAM dans  [!DNL Sites]
description: Utilisez des ressources disponibles pour un déploiement  [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites]  à distance.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d17749cb8e923848f8f81360c03b9afba7989ae2
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 73%

---


# Utilisation des ressources connectées pour partager des ressources DAM dans [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Dans les grandes entreprises, l’infrastructure requise pour créer des sites web peut être distribuée. Il arrive que les fonctionnalités et les ressources numériques de création de sites web permettant de créer ces sites web se trouvent dans différents déploiements. Cette situation peut être motivée par la répartition géographique des déploiements existants, nécessaire pour travailler en tandem. Elle peut être aussi due à l’acquisition d’infrastructures hétérogènes que la société mère souhaite utiliser conjointement.

Les utilisateurs peuvent créer des pages web dans [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] est le système de gestion des ressources numériques (DAM) qui fournit les ressources nécessaires pour les sites web. [!DNL Experience Manager] prend désormais en charge le cas d’utilisation ci-dessus en intégrant [!DNL Sites] et [!DNL Assets].

## Présentation de la fonction Ressources connectées {#overview-of-connected-assets}

Lors de la modification de pages dans [!UICONTROL l’éditeur de page] en tant que destination de la cible, les auteurs peuvent rechercher, parcourir et incorporer facilement des ressources à partir d’un déploiement [!DNL Assets] différent qui agit comme source de ressources. Les administrateurs créent une intégration unique d’un déploiement de [!DNL Experience Manager] avec la fonctionnalité [!DNL Sites] avec un autre déploiement de [!DNL Experience Manager] avec la fonctionnalité [!DNL Assets].

Pour les auteurs [!DNL Sites], les ressources distantes sont disponibles en tant que ressources locales, en lecture seule. Cette fonctionnalité permet de rechercher et d’utiliser aisément plusieurs ressources distantes à la fois. Envisagez de migrer en masse de nombreuses ressources distantes pour les rendre disponibles sur le déploiement local [!DNL Sites] en une seule fois. Voir [Guide de migration des ressources du Experience Manager](/help/assets/assets-migration-guide.md).

### Conditions préalables et déploiements pris en charge {#prerequisites}

Avant d’utiliser ou de configurer cette fonctionnalité, vérifiez les points suivants :

* Les utilisateurs font partie de groupes d’utilisateurs appropriés sur chaque déploiement.
* Pour les types de déploiements [!DNL Adobe Experience Manager], l’un des critères pris en charge est satisfait. [!DNL Experience Manager] 6.5  [!DNL Assets] fonctionne  [!DNL Experience Manager] en tant que Cloud Service. Pour plus d’informations sur le fonctionnement de cette fonctionnalité en tant que [!DNL Cloud Service] [!DNL Experience Manager], voir [Actifs connectés dans [!DNL Experience Manager] sous la forme  [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] sur AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] on-premise |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]comme[!DNL Cloud Service]** | Pris en charge | Pris en charge | Pris en charge |
   | **[!DNL Experience Manager] 6.5 [!DNL Assets] sur AMS** | Pris en charge | Pris en charge | Pris en charge |
   | **[!DNL Experience Manager] 6.5 [!DNL Assets] on-premise** | Pas de prise en charge | Pas de prise en charge | Pas de prise en charge |

### Formats de fichiers pris en charge {#mimetypes}

Les auteurs recherchent des images et les types de documents suivants dans l’outil de recherche de contenu et utiliser les ressources recherchées dans l’éditeur de page. Les documents sont ajoutés au composant `Download` et les images au composant `Image`. Les auteurs ajoutent également les ressources distantes d’un composant [!DNL Experience Manager] personnalisé qui étend les composants par défaut `Download` ou `Image`. Les formats pris en charge sont les suivants :

* **Formats d’image** : les formats pris en charge par le composant [Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=fr). Les images [!DNL Dynamic Media] ne sont pas prises en charge.
* **Formats de document** : voir les [formats de document pris en charge](assets-formats.md#supported-document-formats).

### Utilisateurs et groupes concernés {#users-and-groups-involved}

Les différents rôles impliqués pour configurer et utiliser la fonctionnalité et leurs groupes d’utilisateurs correspondants sont décrits ci-dessous. La portée locale est utilisée dans le cas où un auteur crée une page web. La portée distante est utilisée pour le déploiement DAM qui héberge les ressources requises. L’auteur [!DNL Sites] récupère ces ressources distantes.

| Rôle | Portée | Groupe d’utilisateurs | Nom d’utilisateur de la présentation | Condition requise |
|---|---|---|---|---|
| Administrateur [!DNL Sites] | Local | [!DNL Experience Manager] `administrators` | `admin` | Configurez [!DNL Experience Manager], ainsi que l’intégration au déploiement [!DNL Assets] distant. |
| Utilisateur DAM | Local | `Authors` | `ksaner` | Utilisé pour afficher et dupliquer les ressources récupérées au niveau de `/content/DAM/connectedassets/`. |
| Auteur [!DNL Sites] | Local | <ul><li>`Authors` (avec les droits d’accès en lecture sur l’instance DAM distante et l’accès en tant qu’auteur sur l’instance [!DNL Sites] locale) </li> <li>`dam-users` sur local  [!DNL Sites]</li></ul> | `ksaner` | Les utilisateurs finaux sont des auteurs [!DNL Sites] qui utilisent cette intégration pour améliorer leur vélocité de contenu. Les auteurs recherchent et parcourent les ressources dans des fichiers DAM distants à l’aide de l’[!UICONTROL outil de recherche de contenu] et utilisent les images requises dans les pages web locales. Les identifiants de l’utilisateur DAM `ksaner` sont utilisés. |
| Administrateur [!DNL Assets] | Distant | [!DNL Experience Manager] `administrators` | `admin` sur [!DNL Experience Manager] distant | Configurez le partage des ressources cross-origin (CORS). |
| Utilisateur DAM | Distant | `Authors` | `ksaner` sur [!DNL Experience Manager] distant | Rôle d’auteur sur le déploiement [!DNL Experience Manager] distant. Recherchez et parcourez les ressources dans la fonction Ressources connectées à l’aide de l’[!UICONTROL outil de recherche de contenu]. |
| Distributeur DAM (utilisateur technique) | Distant | [!DNL Sites] `Authors` | `ksaner` sur [!DNL Experience Manager] distant | Cet utilisateur présent sur le déploiement distant est utilisé par le serveur local [!DNL Experience Manager] (et non le rôle d’auteur [!DNL Sites]) pour récupérer les ressources distantes, au nom de l’auteur [!DNL Sites]. Ce rôle n’est pas identique aux deux rôles `ksaner` ci-dessus et appartient à un groupe d’utilisateurs différent. |

## Configurez une connexion entre les déploiements [!DNL Sites] et [!DNL Assets] {#configure-a-connection-between-sites-and-assets-deployments}

Un administrateur [!DNL Experience Manager] peut créer cette intégration. Une fois créées, les autorisations requises pour l’utiliser sont établies par le biais de groupes d’utilisateurs. Les groupes d’utilisateurs sont définis sur les déploiements [!DNL Sites] et DAM.

Pour configurer les ressources connectées et la connectivité des [!DNL Sites] locaux, procédez comme suit :

1. Accédez à un déploiement [!DNL Sites] existant ou créez-en un à l’aide de la commande suivante :

   1. Dans le dossier du fichier JAR, exécutez la commande ci-dessous sur un terminal pour créer chaque serveur [!DNL Experience Manager].
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Au bout de quelques minutes, le serveur [!DNL Experience Manager] démarre. Considérez ce déploiement [!DNL Sites] comme l’ordinateur local pour la création de pages web, par exemple à l’adresse `https://[local_sites]:4502`.

1. Assurez-vous que les utilisateurs et les rôles avec la portée appropriée existent sur le déploiement [!DNL Sites] et sur le déploiement [!DNL Assets] sur AMS. Créez un utilisateur technique sur le déploiement [!DNL Assets] et ajoutez-le au groupe d’utilisateurs mentionné dans les [Utilisateurs et groupes concernés](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accédez au déploiement [!DNL Sites] local à l’adresse `https://[local_sites]:4502`. Cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration de ressources connectées]** et fournissez les valeurs suivantes :

   1. **[!UICONTROL Titre]** de la configuration.
   1. **[!UICONTROL L&#39;]** URL DAM distante est l&#39;URL de l&#39; [!DNL Assets] emplacement au format  `https://[assets_servername]:[port]`.
   1. Identifiants d’un distributeur DAM (utilisateur technique).
   1. Dans le champ **[!UICONTROL Point de montage]**, entrez le chemin local [!DNL Experience Manager] où [!DNL Experience Manager] récupère les ressources. Par exemple, le dossier `remoteassets`. Les ressources extraites de DAM sont stockées dans ce dossier sur le déploiement [!DNL Sites].
   1. **[!UICONTROL L’]** URL des sites locaux correspond à l’emplacement du  [!DNL Sites] déploiement. [!DNL Assets] déploiement utilise cette valeur pour conserver les références aux ressources numériques récupérées par ce  [!DNL Sites] déploiement.
   1. Informations d’identification de l’utilisateur technique [!DNL Sites].
   1. La valeur du champ **[!UICONTROL Seuil d&#39;optimisation du transfert binaire d&#39;origine]** indique si les ressources d&#39;origine (y compris les rendus) sont transférées de manière synchrone ou non. Il est possible de récupérer facilement les fichiers de taille inférieure, tandis que les fichiers de taille de fichier relativement importante sont mieux synchronisés de manière asynchrone. La valeur dépend de vos capacités réseau.
   1. Sélectionnez **[!UICONTROL Entrepôt de données partagé avec les ressources connectées]** si vous utilisez un entrepôt de données pour stocker vos ressources et qu’elle constitue le support de stockage commun aux deux déploiements. Dans ce cas, la limite de seuil n’a pas d’importance puisque des fichiers binaires réels sont disponibles sur la banque de données et ne sont pas transférés.

   ![Configuration standard de la fonctionnalité Ressources connectées](assets/connected-assets-typical-config.png)

   *Figure : Configuration standard de la fonctionnalité Ressources connectées.*

1. Les ressources numériques existantes sur le déploiement [!DNL Assets] sont déjà traitées et les rendus sont générés. Ces rendus sont récupérés à l’aide de cette fonctionnalité, de sorte qu’il n’est pas nécessaire de les régénérer. Désactivez les lanceurs de processus pour empêcher la régénération des rendus. Ajustez les configurations de lanceur sur le déploiement ([!DNL Sites]) pour exclure le dossier `connectedassets` (les ressources sont extraites dans ce dossier).

   1. Sur le déploiement [!DNL Sites], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Lanceurs]**.

   1. Recherchez les lanceurs avec les workflows comme **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** et **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**.

   1. Sélectionnez le lanceur de workflow puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’actions.

   1. Dans l’assistant [!UICONTROL Propriétés], modifiez les champs **[!UICONTROL Chemin]** en fonction des mappages suivants pour mettre à jour leurs expressions régulières afin d’exclure le point de montage **[!UICONTROL connectedassets]**.

   | Avant | Après |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Tous les rendus disponibles sur le déploiement distant sont récupérés lorsque les auteurs obtiennent une ressource. Si vous souhaitez créer d’autres rendus d’une ressource récupérée, ignorez cette étape de configuration. Le workflow [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] est déclenché et crée d’autres rendus. Ces rendus sont disponibles uniquement sur le déploiement [!DNL Sites] local, et non sur le déploiement DAM distant.

1. Ajoutez le déploiement [!DNL Sites] comme origine autorisée dans la configuration CORS du déploiement [!DNL Assets].

   1. Connectez-vous à l’aide des informations d’identification d’administrateur. Recherchez `Cross-Origin`. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.

   1. Pour créer une configuration CORS concernant le déploiement [!DNL Sites], cliquez sur l’option Ajouter ![icône Ajouter des ressources](assets/do-not-localize/assets_add_icon.png) en regard de **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. Dans le champ **[!UICONTROL Origines autorisées]**, entrez l’URL de l’instance locale [!DNL Sites], c’est-à-dire `https://[local_sites]:[port]`. Enregistrez la configuration.

Vous pouvez vérifier la connectivité entre les déploiements [!DNL Sites] configurés et le déploiement [!DNL Assets].

![Test de connexion des ressources connectées configurées  [!DNL Sites]](assets/connected-assets-multiple-config.png)

## Utilisation des ressources distantes {#use-remote-assets}

Les auteurs de site web utilisent l’outil de recherche de contenu pour se connecter au déploiement DAM. Les auteurs peuvent parcourir, rechercher et faire glisser les ressources distantes dans un composant. Pour vous authentifier sur le système DAM distant, conservez les identifiants de l’utilisateur DAM fournis par votre administrateur.

Les auteurs peuvent utiliser les ressources disponibles sur les déploiements DAM local et distant, dans une page web unique. Utilisez l’outil de recherche de contenu pour basculer entre la recherche sur l’instance DAM locale et sur l’instance DAM distante.

Seules sont récupérées les balises des ressources distantes présentant une balise qui correspond exactement (avec la même hiérarchie de taxonomie), disponible sur le déploiement [!DNL Sites] local. Toutes les autres balises sont ignorées. Les auteurs peuvent rechercher des ressources distantes à l’aide de toutes les balises présentes dans le déploiement [!DNL Experience Manager] distant, car AEM offre une fonctionnalité de recherche de texte intégral.

### Présentation de l’utilisation {#walk-through-of-usage}

Utilisez la configuration ci-dessus pour découvrir l’expérience de création et comprendre les principes de la fonctionnalité. Utilisez les documents ou les images de votre choix sur le déploiement DAM distant.

1. Accédez à l’interface [!DNL Assets] sur le déploiement distant via **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]** dans l’espace de travail [!DNL Experience Manager]. Vous pouvez également accéder à `https://[assets_servername_ams]:[port]/assets.html/content/dam` dans un navigateur. Chargez les ressources de votre choix.
1. Sur le déploiement [!DNL Sites], dans l’activateur de profil situé dans le coin supérieur droit, cliquez sur **[!UICONTROL Emprunter l’identité de]**. Indiquez `ksaner` comme nom d’utilisateur, sélectionnez l’option fournie, puis cliquez sur **[!UICONTROL OK]**.
1. Ouvrez une page du site web We.Retail via **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL fr]** > **[!UICONTROL fr]**. Modifiez la page. Vous pouvez également accéder à `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` dans un navigateur pour modifier une page.

   Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** dans le coin supérieur gauche de la page.

1. Ouvrez l’onglet [!UICONTROL Ressources] et cliquez sur **[!UICONTROL Connexion aux ressources connectées]**.
1. Indiquez les identifiants : `ksaner` comme nom d’utilisateur et `password` comme mot de passe. Cet utilisateur dispose d’autorisations de création sur les deux déploiements [!DNL Experience Manager].
1. Recherchez la ressource que vous avez ajoutée dans DAM. Les ressources distantes s’affichent dans le panneau de gauche. Filtrez les images ou les documents, puis les types de documents pris en charge. Faites glisser les images sur un composant `Image` et les documents sur un composant `Download`.

   Les ressources récupérées sont en lecture seule sur le déploiement local [!DNL Sites]. Vous pouvez toujours utiliser les options des composants [!DNL Sites] pour modifier la ressource récupérée. La modification par composants est non destructive.

   ![Options de filtrage des types de documents et des images lors de la recherche de fichiers sur DAM distant](assets/filetypes_filter_connected_assets.png)

   *Figure : Options de filtrage des types de documents et des images lors de la recherche de fichiers sur DAM distant.*

1. Un auteur de site est informé de la récupération asynchrone d’une ressource et de l’échec d’une tâche de récupération. Lors de la création ou même après la création, les auteurs peuvent consulter des informations détaillées sur la récupération des tâches et des erreurs dans l’interface utilisateur [tâches asynchrones](/help/sites-administering/asynchronous-jobs.md).

   ![Notification concernant la récupération asynchrone en arrière-plan des ressources.](assets/assets_async_transfer_fails.png)

   *Figure : Notification concernant la récupération asynchrone en arrière-plan des ressources.*

1. [!DNL Experience Manager] affiche la liste complète des ressources utilisées sur une page lorsqu’elle est publiée. Veillez à bien récupérer les fichiers distants au moment de la publication. Pour vérifier l’état de chaque ressource récupérée, voir [interface utilisateur des tâches asynchrones](/help/sites-administering/asynchronous-jobs.md).

   >[!NOTE]
   >
   >Cette page est publiée même en cas de non-récupération d’une ou plusieurs ressources distantes. Le composant utilisant la ressource distante est publié vide. La zone de notification [!DNL Experience Manager] affiche une notification pour les erreurs qui s’affichent dans la page des tâches asynchrones.

>[!CAUTION]
>
>Une fois utilisées dans une page Web, les ressources distantes extraites peuvent être recherchées et utilisées par toute personne disposant des autorisations d’accès au dossier local. Les ressources extraites sont stockées dans le dossier local (`connectedassets` dans la procédure pas à pas ci-dessus). Les ressources sont également consultables et visibles dans le référentiel local via l’[!UICONTROL outil de recherche de contenu].

Les ressources récupérées peuvent être utilisées comme n’importe quelle autre ressource locale, à la différence que les métadonnées associées ne peuvent pas être modifiées.

### Vérifier l&#39;utilisation d&#39;un fichier sur plusieurs pages Web {#asset-usage-references}

[!DNL Experience Manager] permet aux utilisateurs DAM de vérifier toutes les références à une ressource. Il permet de comprendre et de gérer l’utilisation d’un fichier dans des ressources distantes [!DNL Sites] et dans des ressources composées. De nombreux auteurs de pages Web sur le déploiement de [!DNL Experience Manager Sites] peuvent utiliser une ressource sur une [!DNL Assets] distante dans différentes pages Web. Pour simplifier la gestion des ressources et ne pas générer de références rompues, il est important que les utilisateurs DAM vérifient l’utilisation d’une ressource sur les pages Web locales et distantes. L&#39;onglet [!UICONTROL Références] de la page [!UICONTROL Propriétés] d&#39;une ressource liste les références locales et distantes de la ressource.

Pour vue et gérer les références sur le déploiement [!DNL Assets], procédez comme suit :

1. Sélectionnez un fichier dans la console [!DNL Assets] et cliquez sur **[!UICONTROL Propriétés]** dans la barre d&#39;outils.
1. Cliquez sur **[!UICONTROL Références]** onglet. Voir **[!UICONTROL Références locales]** pour l’utilisation de la ressource sur le déploiement [!DNL Assets]. Voir **[!UICONTROL Références distantes] pour l’utilisation de la ressource dans le déploiement [!DNL Sites] où la ressource a été récupérée à l’aide de la fonctionnalité Ressources connectées.

   ![références distantes dans les propriétés de ressources](assets/connected-assets-remote-reference.png)

1. Les références des pages [!DNL Sites] indiquent le nombre total de références pour chaque [!DNL Sites] local. Il peut s&#39;écouler un certain temps avant de trouver toutes les références et d&#39;afficher le nombre total de références.
1. La liste des références est interactive et les utilisateurs DAM peuvent cliquer sur une référence pour ouvrir la page de référence. Si les références distantes ne peuvent pas être extraites pour une raison quelconque, une notification s’affiche pour informer l’utilisateur de l’échec.
1. Les utilisateurs peuvent déplacer ou supprimer le fichier. Lors du déplacement ou de la suppression d’un fichier, le nombre total de références de tous les fichiers/dossiers sélectionnés s’affiche dans une boîte de dialogue d’avertissement. Lors de la suppression d’un fichier pour lequel les références ne sont pas encore affichées, une boîte de dialogue d’avertissement s’affiche.

   ![avertissement de suppression de force](assets/delete-referenced-asset.png)

## Restrictions et bonnes pratiques {#tip-and-limitations}

* Pour obtenir des informations sur l’utilisation des ressources, configurez la fonctionnalité [Asset Insight](/help/assets/asset-insights.md) sur l’instance [!DNL Sites].

### Autorisations et gestion des ressources {#permissions-and-managing-assets}

* Les ressources locales ne sont pas synchronisées avec les ressources d’origine sur le déploiement distant. Tout retrait, modification ou suppression d’autorisation sur le déploiement DAM n’est pas propagé en aval.
* Les ressources locales sont des copies en lecture seule. Les composants [!DNL Experience Manager] effectuent des modifications non destructives des ressources. Aucune autre modification n’est autorisée.
* Les ressources récupérées localement sont disponibles à des fins d’écriture uniquement. Les workflows de mise à jour de ressources ne peuvent pas être appliqués et les métadonnées ne peuvent pas être modifiées.
* Seules les images et les formats de document répertoriés sont pris en charge. Les ressources [!DNL Dynamic Media], ainsi que les fragments de contenu et d’expérience, ne sont pas pris en charge.
* [!DNL Experience Manager] ne récupère pas les schémas de métadonnées. Il n’est donc pas possible d’afficher toutes les métadonnées extraites. Si le schéma est mis à jour séparément, toutes les propriétés sont affichées.
* Tous les auteurs [!DNL Sites] disposent de droits d’accès en lecture sur les copies récupérées, même s’ils n’en ont pas sur le déploiement DAM distant.
* Il n’existe aucune prise en charge API pour personnaliser l’intégration.
* Cette fonctionnalité permet de rechercher et d’utiliser aisément des ressources distantes. Pour rendre de nombreuses ressources distantes disponibles sur le déploiement local en une fois, envisagez de migrer les ressources. Voir le [guide de migration des ressources](assets-migration-guide.md).
* Il n’est pas possible d’utiliser une ressource distante comme miniature de page dans l’interface utilisateur [!UICONTROL Propriétés de la page]. Vous pouvez définir une miniature d’une page web dans l’interface utilisateur [!UICONTROL Propriétés de la page] à partir de la [!UICONTROL miniature] en cliquant sur [!UICONTROL Sélectionner l’image].

### Configuration et licences {#setup-licensing}

* Le déploiement de [!DNL Assets] sur [!DNL Adobe Managed Services] est pris en charge.
* [!DNL Sites] peut se connecter à un seul référentiel [!DNL Assets] à la fois.
* Une licence [!DNL Assets] s’exécutant en tant que référentiel distant.
* Une ou plusieurs licences [!DNL Sites] s’exécutant comme un déploiement de création local.

### Utilisation {#usage}

* Les utilisateurs peuvent rechercher des ressources distantes et les faire glisser sur la page locale lors de la création. Aucune autre fonctionnalité n’est prise en charge.
* L’opération de récupération échoue après 5 secondes. Les auteurs peuvent rencontrer des problèmes lors de la récupération des ressources, par exemple en cas de problèmes de réseau. Les auteurs peuvent effectuer une nouvelle tentative et faire glisser la ressource distante de l’[!UICONTROL outil de recherche de contenu] vers l’[!UICONTROL éditeur de page].
* Les modifications simples non destructives et les modifications prises en charge par le composant `Image` peuvent être effectuées sur les ressources récupérées. Les ressources sont en lecture seule.
* La seule méthode pour récupérer à nouveau la ressource consiste à la faire glisser sur une page. Il n’existe aucune prise en charge d’API ni aucune autre méthode pour récupérer à nouveau une ressource afin de la mettre à jour.
* Si des ressources sont désaffectées de la gestion des ressources numériques, elles continuent d’être utilisées sur les pages [!DNL Sites].
* Les entrées de référence distantes d’une ressource sont extraites de manière asynchrone. Les références et le nombre total ne sont pas en temps réel et il peut y avoir une différence si un auteur de sites utilise la ressource alors qu&#39;un utilisateur de gestion des actifs numériques consulte la référence. Les utilisateurs DAM peuvent actualiser la page et réessayer dans quelques minutes pour obtenir le nombre total.

## Résolution des problèmes  {#troubleshoot}

Pour résoudre les erreurs courantes, procédez comme suit :

* Si vous ne pouvez pas rechercher des ressources distantes à partir de l’[!UICONTROL outil de recherche de contenu], vérifiez que les rôles et autorisations requis sont bien appliqués.
* Une ressource récupérée à partir du DAM distant peut ne pas être publiée sur une page web pour une ou plusieurs raisons, notamment son absence sur le serveur distant, l’absence d’autorisations appropriées pour la récupérer ou une défaillance du réseau. Assurez-vous que la ressource n’est pas supprimée du DAM distant. Assurez-vous que les autorisations appropriées sont en place et que les conditions préalables sont remplies. Essayez de rajouter la ressource à la page et de la republier. Recherchez dans la [liste des tâches asynchrones](/help/sites-administering/asynchronous-jobs.md) les erreurs de récupération de ressources.
* Si vous ne pouvez pas accéder au déploiement de la gestion des actifs numériques distant à partir du déploiement [!DNL Sites] local, assurez-vous que les cookies intersites sont autorisés. Si les cookies intersites sont bloqués, les deux déploiements de [!DNL Experience Manager] peuvent ne pas s’authentifier. Par exemple, [!DNL Google Chrome] en mode Incognito peut bloquer les cookies tiers. Pour autoriser les cookies dans le navigateur [!DNL Chrome], cliquez sur l’icône « oeil » dans la barre d’adresse, accédez à Le site ne fonctionne pas > Bloqué, sélectionnez l’URL de la gestion des actifs numériques distante et autorisez le cookie de jeton de connexion. Vous pouvez également consulter l’aide [sur la façon d’activer les cookies tiers](https://support.google.com/chrome/answer/95647).

   ![Erreur de cookie dans Chrome en mode incognito](assets/chrome-cookies-incognito-dialog.png)

* Si les références distantes ne sont pas récupérées et génèrent un message d’erreur, vérifiez si le déploiement des sites est disponible et recherchez les problèmes de connectivité réseau. Réessayez ultérieurement pour vérifier. [!DNL Assets] le déploiement tente à deux reprises d’établir une connexion avec le  [!DNL Sites] déploiement, puis signale un échec.

![échec de la nouvelle tentative de références distantes de ressources](assets/reference-report-failure.png)
