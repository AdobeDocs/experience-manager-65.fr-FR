---
title: Connexion à Adobe Analytics et création de frameworks
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: Découvrez comment connecter AEM à SiteCatalyst et créer des structures.
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 54%

---

# Connexion à Adobe Analytics et création de frameworks {#connecting-to-adobe-analytics-and-creating-frameworks}

Pour effectuer le suivi des données web de vos pages AEM dans Adobe Analytics, créez une configuration de services Adobe Analytics Cloud et une structure Adobe Analytics :

* **Configuration Adobe Analytics :** informations sur votre compte Adobe Analytics. La configuration Adobe Analytics permet à AEM de se connecter à Adobe Analytics. Créez une configuration Adobe Analytics pour chaque compte que vous utilisez.
* **Framework Adobe Analytics :** ensemble de mappages entre les propriétés de suite de rapports Adobe Analytics et les variables CQ. Utilisez un framework pour configurer la façon dont les données de votre site Web renseignent vos rapports Adobe Analytics. Les structures sont associées à une configuration Adobe Analytics. Vous pouvez créer plusieurs frameworks pour chaque configuration.

Lorsque vous associez une page Web à un framework, celui-ci effectue le suivi pour cette page et ses descendants. Les vues de page peuvent ensuite être récupérées dans Adobe Analytics et affichées dans la console Sites.

## Prérequis {#prerequisites}

### Compte Adobe Analytics {#adobe-analytics-account}

Pour effectuer le suivi AEM données dans Adobe Analytics, vous devez disposer d’un compte Adobe Experience Cloud Adobe Analytics valide.

Le compte Adobe Analytics doit :

* disposer d’autorisations **Administrateur** ;
* être affecté au groupe d’utilisateurs **Accès aux services Web.**

>[!CAUTION]
>
>Le fait de fournir des autorisations **Administrateur** (dans Adobe Analytics) ne suffit pas pour permettre à l’utilisateur de se connecter d’AEM à Adobe Analytics. Le compte doit également avoir **Accès aux services web** des privilèges.

![chlimage_1-67](assets/chlimage_1-67.png)

Avant de poursuivre, vérifiez que vos informations d’identification vous permettent de vous connecter à Adobe Analytics. Par l’une des méthodes suivantes :

* [Se connecter à Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Se connecter à Adobe Analytics](https://sc.omniture.com/login/)

### Configuration d’AEM pour utiliser vos centres de données Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [centres de données](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) collecter, traiter et stocker les données associées à votre suite de rapports Adobe Analytics. Configurez AEM pour utiliser le centre de données qui héberge votre suite de rapports Adobe Analytics. Le centre de données est mentionné dans votre contrat. Pour obtenir ces informations, contactez un administrateur de votre entreprise.

Au besoin, utilisez les éléments suivants pour les router vers le centre de données approprié : `https://api.omniture.com/`.

Si votre entreprise a besoin d’une collecte ou d’une récupération de données à partir d’un centre de données spécifique, utilisez les méthodes suivantes :

| Centre de données | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Singapour | `https://api4.omniture.com/` |
| Oregon | `https://api5.omniture.com/` |

Utilisez la [console Web pour configurer le](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **client HTTP Adobe AEM Analytics du lot OSGi**. Ajoutez l’**URL du centre de données** du centre de données qui héberge une suite de rapports pour laquelle vos pages AEM collectent des données.

![aa-07](assets/aa-07.png)

1. Ouvrez la console Web dans votre navigateur Web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Pour accéder à la console, saisissez vos informations d’identification.

   >[!NOTE]
   >
   >Pour savoir si vous avez accès à cette console, contactez votre administrateur de site.

1. Sélectionnez l’élément Configuration nommé **Adobe AEM client HTTP Analytics**.
1. Pour ajouter l’URL d’un centre de données, appuyez sur le bouton + situé en regard de la liste **URL de centre de données**, puis saisissez l’URL dans la boîte de dialogue.

1. Pour supprimer une URL de la liste, cliquez sur le bouton - situé en regard de l’URL.
1. Cliquez sur Enregistrer.

## Configuration de la connexion à Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM.
>
>Le [plug-in Activity Map fourni par Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=fr) doit désormais être utilisé.

## Configuration pour Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM.
>
>Le [plug-in Activity Map fourni par Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=fr) doit désormais être utilisé.

## Création d’une structure Adobe Analytics {#creating-a-adobe-analytics-framework}

Pour l’identifiant de suite de rapports (RSID) que vous utilisez, vous pouvez contrôler quelles instances de serveur (création, publication ou les deux) contribuent aux données de la suite de rapports :

* **Tous**: Les informations de l’instance d’auteur et de publication renseignent la suite de rapports.
* **Auteur**: Seules les informations provenant de l’instance d’auteur renseignent la suite de rapports.
* **Publier**: Seules les informations provenant de l’instance de publication renseignent la suite de rapports.

>[!NOTE]
>
>La sélection du type d’instance de serveur ne limite pas les appels à Adobe Analytics, elle contrôle simplement les appels qui incluent le RSID.
>
>Par exemple, une structure est configurée pour utiliser la suite de rapports *diiweretail* et l’instance de serveur sélectionnée est l’instance de création. Lorsque les pages sont publiées avec la structure, les appels sont toujours émis vers Adobe Analytics, mais ces appels ne contiennent pas le RSID. Seuls les appels effectués à partir de l’instance de création incluent le RSID.

1. Avec la **Navigation**, sélectionnez **Outils**, **Services cloud**, puis **Services cloud hérités**.
1. Faites défiler jusqu’à **Adobe Analytics** et sélectionnez **Afficher les configurations**.
1. Cliquez sur le lien **[+]** situé en regard de votre configuration Adobe Analytics.

1. Dans le **Créer une structure** dialog :

   * Spécifiez un **Titre**.
   * Vous pouvez éventuellement spécifier la variable **Nom**, pour le noeud qui stocke les détails de la structure dans le référentiel.
   * Sélectionnez **Framework Adobe Analytics**,

   puis cliquez sur **Créer**.

   Le framework s’ouvre en vue de la modification.

1. Dans la section **Suites de rapports** de la capsule latérale (côté droit du panneau principal), cliquez sur **Ajouter un élément**. Utilisez ensuite la liste déroulante pour sélectionner l’identifiant de suite de rapports (par exemple, `geometrixxauth`) avec laquelle la structure interagit.

   >[!NOTE]
   >
   >L’outil de recherche de contenu situé à gauche est renseigné avec les variables Adobe Analytics (variables SiteCatalyst) lorsque vous sélectionnez un identifiant de suite de rapports.

1. Pour sélectionner les instances de serveur pour lesquelles vous souhaitez envoyer des informations à la suite de rapports, utilisez le **Mode d’exécution** Liste déroulante (en regard de l’identifiant de suite de rapports).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Pour que le framework soit disponible sur l’instance de publication de votre site, dans l’onglet **Page** du sidekick, cliquez sur **Activer le framework.**

### Configuration des paramètres de serveur pour Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Le système de framework vous permet de modifier les paramètres de serveur dans chaque framework Adobe Analytics.

>[!CAUTION]
>
>Ces paramètres déterminant où vos données sont envoyées et comment, il est impératif de *ne pas les modifier vous-même* et de laisser votre représentant Adobe Analytics les configurer.

Commencez par ouvrir le panneau. Appuyez sur la flèche vers le bas en regard de **Serveurs**:

![server_001](assets/server_001.png)

* **Serveur de suivi**

   * Contient l’URL utilisée pour envoyer les appels Adobe Analytics.

      * `cname` : prend par défaut le *nom d’entreprise* du compte Adobe Analytics
      * `d1` - correspond au centre de données auquel les informations sont envoyées (l’une ou l’autre des deux `d1`, `d2`ou `d3`)
      * `sc.omtrdc.net` - nom de domaine

* **Serveur de suivi sécurisé**

   * Comporte les mêmes segments que le serveur de suivi
   * Utilisé pour envoyer des données à partir de pages sécurisées (`https://`)

* **Espace de noms du visiteur**

   * L’espace de noms détermine la première partie de l’URL de suivi.
   * Par exemple, modifiez l’espace de noms en **CNAME** fait ressembler les appels effectués vers Adobe Analytics à **CNAME.d1.omtrdc.net** au lieu de la valeur par défaut.

## Association d’une page à une structure Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Lorsqu’une page est associée à un framework Adobe Analytics, elle envoie des données à Adobe Analytics lors de son chargement. Les variables que la page renseigne sont mappées et extraites des variables Adobe Analytics dans la structure. Par exemple, les pages vues sont récupérées à partir d’Adobe Analytics.

Les descendants de la page héritent de l’association avec la structure. Par exemple, lorsque vous associez la page racine de votre site à une structure, toutes les pages du site sont associées à la structure.

1. Dans la console **Sites**, sélectionnez la page dont vous souhaitez configurer le suivi.
1. Ouvrez les **[Propriétés de la page](/help/sites-authoring/editing-page-properties.md)**, directement à partir de la console ou via l’éditeur de page.
1. Ouvrez l’onglet **Services cloud**.

1. Utilisez le menu déroulant **Ajouter une configuration** pour sélectionner **Adobe Analytics** parmi les options disponibles. Si l’héritage est placé, désactivez-le avant que le sélecteur ne soit disponible.

1. Sélecteur de liste déroulante pour **Adobe Analytics** est ajouté aux options disponibles. Sélectionnez la configuration de structure requise.

1. Sélectionner **Enregistrer et fermer**.
1. Pour activer la page et les configurations/fichiers connectés, **[Publier](/help/sites-authoring/publishing-pages.md)** de la page.
1. La dernière étape consiste à accéder à la page sur l’instance de publication et à rechercher un mot-clé (par exemple, aubergine) à l’aide de la fonction **Rechercher** composant.
1. Vous pouvez ensuite vérifier les appels effectués à Adobe Analytics à l’aide d’un outil approprié, par exemple [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. A partir de l&#39;exemple fourni, l&#39;appel doit contenir la valeur renseignée (c&#39;est-à-dire aubergine) en eVar7 et la liste des événements doit contenir event3.

### Pages vues {#page-views}

Lorsqu’une page est associée à une structure Adobe Analytics, le nombre de pages vues peut être affiché dans la vue Liste de la console Sites.

Voir [Affichage des données d’analyse de page](/help/sites-authoring/page-analytics-using.md) pour plus de détails.

### Configuration de l’intervalle d’importation {#configuring-the-import-interval}

Configurez l’instance appropriée de la **Adobe AEM configuration des interrogations gérées** service :

* **Intervalle d’interrogation** : intervalle, en secondes, auquel le service extrait les données de pages vues d’Adobe Analytics.
L’intervalle par défaut est de 43 200 000 ms (12 heures).

* **Activer** :
pour activer ou désactiver le service. Par défaut, le service est activé.

Pour configurer ce service OSGi, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou un [nœud osgiConfig dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (le PID de service est `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Modification des configurations et/ou des structures Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Comme pour la création d’une configuration ou d’une structure Adobe Analytics, accédez à l’écran **Services cloud** (hérité). Sélectionner **Afficher les configurations**, puis cliquez sur le lien vers la configuration spécifique à mettre à jour.

Lors de la modification d’une configuration Adobe Analytics, appuyez sur **Modifier** lorsque sur la page de configuration elle-même pour ouvrir la variable **Modifier le composant** boîte de dialogue.

## Suppression des frameworks Adobe Analytics {#deleting-adobe-analytics-frameworks}

Pour supprimer une structure Adobe Analytics, commencez par [l’ouvrir pour modification](#editing-adobe-analytics-configurations-and-or-frameworks).

Sélectionnez ensuite **Supprimer le framework** dans l’onglet **Page** du sidekick.
