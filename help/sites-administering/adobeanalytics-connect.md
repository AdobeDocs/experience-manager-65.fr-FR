---
title: Connexion à Adobe Analytics et création de frameworks
description: Découvrez comment connecter AEM à SiteCatalyst et créer des frameworks.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 100%

---

# Connexion à Adobe Analytics et création de frameworks {#connecting-to-adobe-analytics-and-creating-frameworks}

Pour effectuer le suivi des données web de vos pages AEM dans Adobe Analytics, créez une configuration de services Adobe Analytics Cloud et un framework Adobe Analytics :

* **Configuration Adobe Analytics :** informations sur votre compte Adobe Analytics. La configuration Adobe Analytics permet à AEM de se connecter à Adobe Analytics. Créez une configuration Adobe Analytics pour chaque compte que vous utilisez.
* **Framework Adobe Analytics :** ensemble de mappages entre les propriétés de suite de rapports Adobe Analytics et les variables CQ. Utilisez un framework pour configurer la façon dont les données de votre site Web renseignent vos rapports Adobe Analytics. Les frameworks sont associés à une configuration Adobe Analytics. Vous pouvez créer plusieurs frameworks pour chaque configuration.

Lorsque vous associez une page Web à un framework, celui-ci effectue le suivi pour cette page et ses descendants. Les vues de page peuvent ensuite être récupérées dans Adobe Analytics et affichées dans la console Sites.

## Conditions préalables {#prerequisites}

### Compte Adobe Analytics {#adobe-analytics-account}

Pour effectuer le suivi des données d’AEM dans Adobe Analytics, vous devez disposer d’un compte Adobe Analytics d’Adobe Experience Cloud valide.

Le compte Adobe Analytics doit :

* disposer d’autorisations **Administrateur** ;
* être affecté au groupe d’utilisateurs **Accès aux services Web.**

>[!CAUTION]
>
>Le fait de fournir des autorisations **Administrateur** (dans Adobe Analytics) ne suffit pas pour permettre à l’utilisateur de se connecter d’AEM à Adobe Analytics. Le compte doit également avoir des droits d’**accès aux services web**.

![chlimage_1-67](assets/chlimage_1-67.png)

Avant de commencer, assurez-vous que vos informations d’identification vous permettent de vous connecter à Adobe Analytics. Utilisez l’une des méthodes suivantes :

* [Se connecter à Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Se connecter à Adobe Analytics](https://sc.omniture.com/login/)

### Configuration d’AEM pour utiliser vos centres de données Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Les [centres de données](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=fr) d’Adobe Analytics collectent, traitent et stockent les données associées à votre suite de rapports Adobe Analytics. Configurez AEM pour utiliser le centre de données qui héberge votre suite de rapports Adobe Analytics. Le centre de données est mentionné dans votre contrat. Pour obtenir ces informations, contactez un administrateur ou une administratrice de votre organisation.

Au besoin, utilisez l’élément suivant pour accéder au centre de données approprié : `https://api.omniture.com/`.

Si votre organisation a besoin de collecter ou de récupérer des données d’un centre de données spécifique, utilisez ce qui suit :

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
   >Pour savoir si vous avez accès à cette console, contactez l’administrateur ou l’administratrice de votre site.

1. Sélectionnez l’élément de configuration nommé **Client HTTP Adobe Analytics d’AEM**.
1. Pour ajouter l’URL d’un centre de données, appuyez sur le bouton + situé en regard de la liste **URL de centre de données**, puis saisissez l’URL dans la boîte de dialogue.

1. Pour supprimer une URL de la liste, cliquez sur le bouton - situé en regard de l’URL.
1. Cliquez sur Enregistrer.

## Configurer la connexion à Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

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

## Créer un framework Adobe Analytics {#creating-a-adobe-analytics-framework}

Pour l’identifiant de suite de rapports (RSID) que vous utilisez, vous pouvez contrôler quelles instances de serveur (création, publication ou les deux) contribuent aux données de la suite de rapports :

* **Tous** : les informations de l’instance de création et de publication renseignent la suite de rapports.
* **Création** : seules les informations provenant de l’instance de création renseignent la suite de rapports.
* **Publication** : seules les informations provenant de l’instance de publication renseignent la suite de rapports.

>[!NOTE]
>
>La sélection du type d’instance de serveur ne limite pas les appels à Adobe Analytics, elle contrôle simplement les appels qui incluent le RSID.
>
>Par exemple, une structure est configurée pour utiliser la suite de rapports *diiweretail* et l’instance de serveur sélectionnée est l’instance de création. Lorsque les pages sont publiées avec la structure, les appels sont toujours émis vers Adobe Analytics, mais ces appels ne contiennent pas le RSID. Seuls les appels effectués à partir de l’instance de création incluent le RSID.

1. Avec la **Navigation**, sélectionnez **Outils**, **Services cloud**, puis **Services cloud hérités**.
1. Faites défiler jusqu’à **Adobe Analytics** et sélectionnez **Afficher les configurations**.
1. Cliquez sur le lien **[+]** situé en regard de votre configuration Adobe Analytics.

1. Dans la boîte de dialogue **Créer un framework** :

   * Spécifiez un **Titre**.
   * Il est possible de spécifier le **Nom** pour le nœud qui stocke les détails du framework dans le référentiel.
   * Sélectionnez **Framework Adobe Analytics**,

   puis cliquez sur **Créer**.

   Le framework s’ouvre en vue de la modification.

1. Dans la section **Suites de rapports** de la capsule latérale (côté droit du panneau principal), cliquez sur **Ajouter un élément**. Utilisez ensuite le menu déroulant pour sélectionner l’identifiant de suite de rapports (par exemple, `geometrixxauth`) avec lequel le framework interagira.

   >[!NOTE]
   >
   >L’outil de recherche de contenu situé à gauche est renseigné avec les variables d’Adobe Analytics (variables de SiteCatalyst) lorsque vous sélectionnez un identifiant de suite de rapports.

1. Pour sélectionner les instances de serveur qui doivent envoyer des informations à la suite de rapports, utilisez la liste déroulante du **Mode d’exécution** (en regard de l’identifiant de suite de rapports).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Pour que le framework soit disponible sur l’instance de publication de votre site, dans l’onglet **Page** du sidekick, cliquez sur **Activer le framework.**

### Configuration des paramètres de serveur pour Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Le système de framework vous permet de modifier les paramètres de serveur dans chaque framework Adobe Analytics.

>[!CAUTION]
>
>Ces paramètres déterminant où vos données sont envoyées et comment, il est impératif de *ne pas les modifier vous-même* et de laisser votre représentant Adobe Analytics les configurer.

Commencez par ouvrir le panneau. Appuyez sur la flèche vers le bas en regard de **Serveurs** :

![server_001](assets/server_001.png)

* **Serveur de suivi**

   * Contient l’URL utilisée pour envoyer les appels Adobe Analytics.

      * `cname` : prend par défaut le *nom d’entreprise* du compte Adobe Analytics.
      * `d1` : correspond au centre de données auquel les informations sont envoyées (soit `d1`, `d2` ou `d3`).
      * `sc.omtrdc.net` : nom de domaine.

* **Serveur de suivi sécurisé**

   * Comporte les mêmes segments que le serveur de suivi.
   * Utilisé pour envoyer des données à partir de pages sécurisées (`https://`).

* **Espace de noms du visiteur ou de la visiteuse**

   * L’espace de noms détermine la première partie de l’URL de suivi.
   * Par exemple, si l’espace de noms est redéfini sur **CNAME**, les appels effectués vers Adobe Analytics ressembleront à **CNAME.d1.omtrdc.net** plutôt qu’à la valeur par défaut.

## Associer une page à un framework d’Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Lorsqu’une page est associée à un framework Adobe Analytics, elle envoie des données à Adobe Analytics lors de son chargement. Les variables que la page renseigne sont mappées et extraites des variables Adobe Analytics dans la structure. Par exemple, les pages vues sont récupérées à partir d’Adobe Analytics.

Les descendants de la page héritent de l’association avec la structure. Par exemple, lorsque vous associez la page racine de votre site à un framework, toutes les pages du site sont associées au framework.

1. Dans la console **Sites**, sélectionnez la page dont vous souhaitez configurer le suivi.
1. Ouvrez les **[Propriétés de la page](/help/sites-authoring/editing-page-properties.md)**, directement à partir de la console ou via l’éditeur de page.
1. Ouvrez l’onglet **Services cloud**.

1. Utilisez le menu déroulant **Ajouter une configuration** pour sélectionner **Adobe Analytics** parmi les options disponibles. Si l’héritage est en place, désactivez-le avant que le sélecteur ne soit disponible.

1. Le sélecteur de liste déroulante pour **Adobe Analytics** est ajouté aux options disponibles. Sélectionnez la configuration de framework requise.

1. Sélectionnez **Enregistrer et fermer**.
1. Pour activer la page et les configurations/fichiers connectés, **[publiez](/help/sites-authoring/publishing-pages.md)** la page.
1. La dernière étape consiste à accéder à la page sur l’instance de publication et à rechercher un mot-clé (par exemple, aubergine) à l’aide du composant **Recherche**.
1. Vous pouvez ensuite vérifier les appels effectués à Adobe Analytics à l’aide d’un outil approprié, par exemple le [débogueur d’Adobe Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=fr).
1. À partir de l’exemple fourni, l’appel doit contenir la valeur renseignée (c’est-à-dire aubergine) en eVar7 et la liste des événements doit contenir event3.

### Pages vues {#page-views}

Lorsqu’une page est associée à un framework d’Adobe Analytics, le nombre de pages vues peut être affiché dans la vue liste de la console Sites.

Voir [Affichage des données d’analyse de page](/help/sites-authoring/page-analytics-using.md) pour plus de détails.

### Configurer l’intervalle d’importation {#configuring-the-import-interval}

Configurez l’instance appropriée du service **Importateur Sling de rapports Adobe AEM Analytics** :

* **Tentatives de récupération** :
nombre de tentatives de récupération d’un rapport en file d’attente.
La valeur par défaut est `6`.

* **Délai de récupération** :
nombre de millisecondes entre les tentatives de récupération d’un rapport en file d’attente.
La valeur par défaut est de `10000`. Comme la valeur est en millisecondes, cela correspond à 10 secondes.

* **Fréquence de récupération** :
expression `cron` pour déterminer la fréquence de récupération du rapport Analytics.
La valeur par défaut est `0 0 0/12 * * ?` ; cela correspond à 12 récupérations par heure.

Pour configurer ce service OSGi, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou un [nœud osgiConfig dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (le PID de service est `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`).

## Modifier les configurations et/ou les frameworks d’Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Comme pour la création d’une configuration ou d’une structure Adobe Analytics, accédez à l’écran **Services cloud** (hérité). Sélectionnez **Afficher les configurations**, puis cliquez sur le lien vers la configuration que vous souhaitez mettre à jour.

Lors de la modification d’une configuration Adobe Analytics, appuyez sur **Modifier** sur la page de configuration pour ouvrir la boîte de dialogue **Modifier le composant**.

## Supprimer des frameworks d’Adobe Analytics {#deleting-adobe-analytics-frameworks}

Pour supprimer un framework d’Adobe Analytics, commencez par [l’ouvrir pour le modifier](#editing-adobe-analytics-configurations-and-or-frameworks).

Sélectionnez ensuite **Supprimer le framework** dans l’onglet **Page** du sidekick.
