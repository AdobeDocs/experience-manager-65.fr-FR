---
title: Connexion à Adobe Analytics et création de structures
seo-title: Connexion à Adobe Analytics et création de structures
description: Découvrez comment connecter AEM à SiteCatalyst et créer des structures.
seo-description: Découvrez comment connecter AEM à SiteCatalyst et créer des structures.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 63%

---


# Connexion à Adobe Analytics et création de structures  {#connecting-to-adobe-analytics-and-creating-frameworks}

Pour suivre les données Web de vos pages AEM dans Adobe Analytics, créez une configuration Adobe Analytics Cloud Services et une structure Adobe Analytics :

* **Configuration Adobe Analytics :** informations relatives à votre compte Adobe Analytics. La configuration Adobe Analytics permet à AEM de se connecter à Adobe Analytics. Créez une configuration Adobe Analytics pour chaque compte que vous utilisez.
* **Adobe Analytics Framework :** ensemble de mappages entre les propriétés de la suite de rapports Adobe Analytics et les variables CQ. Utilisez une structure pour configurer la façon dont les données de votre site web renseignent vos rapports Adobe Analytics. Les cadres sont associés à une configuration Adobe Analytics. Vous pouvez créer plusieurs structures pour chaque configuration.

Lorsque vous associez une page Web à une structure, celle-ci effectue le suivi pour cette page et ses descendants. Les vues de page peuvent ensuite être récupérées dans Adobe Analytics et affichées dans la console Sites.

## Conditions préalables {#prerequisites}

### Compte Adobe Analytics {#adobe-analytics-account}

Pour effectuer le suivi des données AEM dans Adobe Analytics, vous devez disposer d’un compte Adobe Marketing Cloud valide.

Le compte Adobe Analytics doit :

* Disposer d’autorisations **Administrateur**
* Être affecté au groupe d’utilisateurs **Accès aux services web.**

>[!CAUTION]
>
>Le fait de fournir des autorisations **Administrateur** (dans Adobe Analytics) ne suffit pas pour permettre à l’utilisateur de se connecter d’AEM à Adobe Analytics. Le compte doit également disposer d’autorisations **Accès aux services web**.

![chlimage_1-67](assets/chlimage_1-67.png)

Avant de commencer, assurez-vous que vos informations d’identification vous permettent de vous connecter à Adobe Analytics. Via :

* [Connexion Adobe Experience Cloud](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Connexion Adobe Analytics](https://sc.omniture.com/login/)

### Configuration d’AEM pour utiliser vos centres de données Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [datacenters](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) collecte, traite et stocke les données associées à votre suite de rapports Adobe Analytics. Vous devez configurer AEM pour utiliser le centre de données qui héberge votre suite de rapports Adobe Analytics. Le tableau suivant répertorie les centres de données disponibles et leur URL.

| Centre de données | URL |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| Dallas | https://api2.omniture.com/admin/1.4/rest/ |
| Londres | https://api3.omniture.com/admin/1.4/rest/ |
| Singapour | https://api4.omniture.com/admin/1.4/rest/ |
| Oregon | https://api5.omniture.com/admin/1.4/rest/ |

AEM utilise le centre de données de San Jose (https://api.omniture.com/admin/1.4/rest/) par défaut.

Utilisez la [console Web pour configurer le](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **client HTTP Adobe AEM Analytics du lot OSGi**. Ajoutez l&#39;**URL du centre de données** pour le centre de données qui héberge une suite de rapports pour laquelle vos pages AEM collectent des données.

![aa-07](assets/aa-07.png)

1. Ouvrez la console Web dans votre navigateur web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Entrez vos informations d’identification pour accéder à la console.

   >[!NOTE]
   >
   >Contactez l’administrateur de votre site web pour savoir si vous avez accès à cette console.

1. Sélectionnez l’élément de configuration nommé **Client HTTP Adobe AEM Analytics**.
1. Pour ajouter l’URL d’un centre de données, appuyez sur le bouton + en regard de la liste **URL des centres de données**, puis saisissez l’URL dans la zone.

1. Pour supprimer une URL de la liste, cliquez sur le bouton - situé en regard de l’URL.
1. Cliquez sur Enregistrer.

## Configuration de la connexion à Adobe Analytics  {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM.
>
>Le [module externe ActivityMap fourni par Adobe Analytics](https://docs.adobe.com/content/help/fr-FR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) doit maintenant être utilisé.

## Configuration pour Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM.
>
>Le [module externe ActivityMap fourni par Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) doit maintenant être utilisé.

## Création d’une structure Adobe Analytics {#creating-a-adobe-analytics-framework}

Pour l’identifiant de suite de rapports (RSID) que vous utilisez, vous pouvez contrôler quelles instances de serveur (création, publication ou les deux) contribuent aux données de la suite de rapports :

* **Tout** : les informations de l’instance de création et de publication renseignent la suite de rapports.
* **Création** : seules les informations de l’instance de création renseignent la suite de rapports.
* **Publication** : seules les informations de l’instance de publication renseignent la suite de rapports.

>[!NOTE]
>
>La sélection du type d’instance de serveur ne restreint pas les appels à Adobe Analytics, mais contrôle simplement quels appels incluent le RSID.
>
>Par exemple, une structure est configurée pour utiliser la suite de rapports *diiweretail* et l’instance de serveur sélectionnée est l’instance de création. Lorsque les pages sont publiées avec la structure, les appels sont toujours émis vers Adobe Analytics, mais ces appels ne contiennent pas le RSID. Seuls les appels effectués à partir de l’instance de création incluent le RSID.

1. Avec la **Navigation**, sélectionnez **Outils**, **Services cloud**, puis **Services cloud hérités**.
1. Accédez à **Adobe Analytics** et sélectionnez **Afficher les configurations**.
1. Cliquez sur le lien **[+]** en regard de votre configuration Adobe Analytics.

1. Dans la boîte de dialogue **Créer une structure** :

   * Spécifiez un **Titre**.
   * Vous pouvez éventuellement spécifier le **Nom**, pour le nœud qui stocke les détails de la structure dans le référentiel.
   * Sélectionnez **Adobe Analytics Framework**

   puis cliquez sur **Créer**.

   La structure s’ouvre en vue de la modification.

1. Dans la section **Suites de rapports** de la capsule latérale (côté droit du panneau principal), cliquez sur **Ajouter un élément**. Utilisez ensuite la liste déroulante pour sélectionner l’identifiant de suite de rapports (par exemple, `geometrixxauth`) avec lequel la structure interagira.

   >[!NOTE]
   >
   >L’outil de recherche de contenu situé à gauche est renseigné par des variables Adobe Analytics (variables de SiteCatalyst) lorsque vous sélectionnez un identifiant de suite de rapports.

1. Utilisez ensuite le menu déroulant **Mode d’exécution** (situé à côté de l’identifiant de suite de rapports) pour sélectionner les instances de serveur qui doivent envoyer des informations à la suite de rapports.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Pour rendre la structure disponible sur l’instance de publication de votre site, dans l’onglet **Page** du sidekick, cliquez sur **Activer la structure.**

### Configuration des paramètres de serveur pour Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Le système de structure vous permet de modifier les paramètres du serveur dans chaque structure Adobe Analytics.

>[!CAUTION]
>
>Ces paramètres déterminent l&#39;emplacement et le mode d&#39;envoi des données. Il est donc impératif que vous *ne modifiez pas ces paramètres* et que votre représentant Adobe Analytics les configurez à la place.

Commencez par ouvrir le panneau. Appuyez sur la flèche vers le bas située en regard de **Serveurs** :

![server_001](assets/server_001.png)

* **Serveur de suivi**

   * contient l’URL utilisée pour envoyer des appels Adobe Analytics

      * cname : nom de Société *du compte Adobe Analytics* par défaut.
      * d1 : correspond au centre de données auquel les informations seront envoyées (il peut s’agir de d1, d2 ou d3)
      * sc.omtrdc.net - nom de domaine

* **Serveur de suivi sécurisé**

   * Comporte les mêmes segments que le serveur de suivi
   * Ceci permet d’envoyer les données à partir des pages sécurisées (https://)

* **Espace de noms du visiteur**

   * L’espace de noms détermine la première partie de l’URL de suivi.
   * Par exemple, si vous modifiez l’espace de nommage en **CNAME**, les appels effectués à Adobe Analytics ressembleront à **CNAME.d1.omtrdc.net** au lieu de  par défaut.

## Association d’une page à une structure Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Lorsqu’une page est associée à une structure Adobe Analytics, la page envoie des données à Adobe Analytics au chargement de la page. Les variables que la page renseigne sont mappées et extraites des variables Adobe Analytics dans la structure. Par exemple, les pages vues sont extraites d’Adobe Analytics.

Les descendants de la page héritent de l’association avec la structure. Par exemple, lorsque vous associez la page racine de votre site à une structure, toutes les pages du site sont associées à cette structure.

1. Dans la console **Sites**, sélectionnez la page à configurer avec le suivi.
1. Ouvrez les **[Propriétés de la page](/help/sites-authoring/editing-page-properties.md)**, directement à partir de la console ou via l’éditeur de page.
1. Ouvrez l&#39;onglet** Cloud Services**.

1. Utilisez la liste déroulante **Ajouter la configuration** pour sélectionner **Adobe Analytics** dans les options disponibles. Si l’héritage est en place, vous devez le désactiver pour que le sélecteur devienne disponible.

1. Le sélecteur déroulant pour **Adobe Analytics** est ajouté aux options disponibles. Utilisez-le pour sélectionner la configuration de structure requise.

1. Sélectionnez **Enregistrer et fermer**.
1. **[Publiez](/help/sites-authoring/publishing-pages.md)** la page pour activer la page et tous les fichiers/configurations connecté(e)s.
1. La dernière étape consiste à visiter la page sur l’instance de publication et à rechercher un mot-clé (par exemple, aubergine) à l’aide du composant **Rechercher**.
1. Vous pouvez ensuite vérifier les appels à Adobe Analytics à l&#39;aide d&#39;un outil approprié ; par exemple, [Débogueur Adobe Experience Cloud](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).
1. Dans l’exemple fourni, l’appel doit contenir la valeur entrée (c’est-à-dire, aubergine) dans eVar7 et la liste des événements doit contenir event3.

### Pages vues {#page-views}

Lorsqu&#39;une page est associée à une structure Adobe Analytics, le nombre de vues de page peut être affiché dans la vue de Liste de la console Sites.

Voir [Affichage des données d’analyse de page](/help/sites-authoring/page-analytics-using.md) pour plus de détails.

### Configuration de l’intervalle d’importation  {#configuring-the-import-interval}

Configurez l’instance appropriée du service **Configurations d’interrogation personnalisées Adobe AEM** :

* **Intervalle d’interrogation** : intervalle, en secondes, auquel le service extrait les données de pages vues d’Adobe Analytics.
L’intervalle par défaut est de 43 200 000 ms (12 heures).

* **Activer** :  pour activer ou désactiver le service. Par défaut, le service est activé.

Pour configurer ce service OSGi, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou un noeud [osgiConfig dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (le PID de service est `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Modification de configurations et/ou de structures Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Comme pour la création d’une configuration ou d’une structure Adobe Analytics, accédez à l’écran **Services cloud** (hérité). Sélectionnez **Afficher les configurations**, puis cliquez sur le lien vers la configuration que vous souhaitez mettre à jour.

Lors de la modification d’une configuration Adobe Analytics, vous devez également appuyer sur le bouton **Modifier** dans la page de configuration afin d’ouvrir la boîte de dialogue **Modifier le composant**.

## Suppression de structures Adobe Analytics {#deleting-adobe-analytics-frameworks}

Pour supprimer une structure Adobe Analytics, [ouvrez-la d’abord pour la modifier](#editing-adobe-analytics-configurations-and-or-frameworks).

Sélectionnez ensuite **Supprimer l’infrastructure** dans l’onglet **Page** du sidekick.

