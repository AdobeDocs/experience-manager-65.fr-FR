---
title: Intégration à Silverpop Engage
seo-title: Intégration à Silverpop Engage
description: Découvrez comment intégrer AEM à Silverpop Engage.
seo-description: Découvrez comment intégrer AEM à Silverpop Engage.
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 75%

---


# Intégration à Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>L’intégration à Silverpop **n’est pas** disponible par défaut. Vous devez télécharger le [module d’intégration Silverpop](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) à partir de Package Share et l’installer sur votre instance. Après avoir installé le module, vous pouvez le configurer comme décrit dans ce document.

L&#39;intégration d&#39;AEM à Silverpop Engage vous permet de gérer et d&#39;envoyer des courriels créés dans AEM via Silverpop. Il vous permet également d&#39;utiliser les fonctions de gestion des pistes de Silverpop via AEM formulaires sur les pages AEM.

L’intégration offre les fonctionnalités suivantes :

* La possibilité de créer des courriers électroniques dans AEM et de les publier sur Silverpop pour distribution.
* La possibilité de définir une action d’un formulaire AEM pour créer un abonné Silverpop.

Une fois Engagement Silverpop configuré, vous pouvez publier des newsletters ou des courriers électroniques sur Engagement Silverpop.

## Création d’une configuration Silverpop {#creating-a-silverpop-configuration}

Les configurations Silverpop peuvent être ajoutées via **Services cloud**, **Outils** ou des **points de terminaison d’API**. Toutes les méthodes sont décrites dans cette section.

### Configuration de Silverpop via Services cloud {#configuring-silverpop-via-cloudservices}

Pour créer une configuration Silverpop dans Services cloud :

1. Dans AEM, appuyez ou cliquez sur **Outils** > **Déploiement** > **Services cloud**. (Or directly access at `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Under third-party services, click **Silverop Engage** and then **Configure**. La fenêtre de configuration de Silverpop s’ouvre.

   >[!NOTE]
   >
   >Engagement Silverpop n’est pas disponible sous les services tiers, sauf si vous avez téléchargé le module sur Package Share.

1. Ajoutez un titre et, éventuellement, un nom, puis cliquez sur **Créer**. La fenêtre de configuration Paramètres** Silverpop** s&#39;ouvre.
1. Saisissez le nom d’utilisateur et le mot de passe, puis sélectionnez un point de terminaison d’API dans la liste déroulante.
1. Cliquez sur **Connecter·à Silverpop.** Une fois la connexion établie, vous voyez une boîte de dialogue de confirmation. Cliquez sur **OK** pour fermer la fenêtre. You can go to Silverpop by clicking **Go to Silverpop Engage**.
1. Silverpop a été configuré. Si vous souhaitez modifier la configuration, cliquez sur **Modifier**.
1. En outre, la structure Silverpop Engage peut être configurée pour les actions personnalisées lorsque vous fournissez un titre et un nom (facultatif). Cliquez sur Créer afin de définir la structure de la connexion à Silverpop déjà configurée.

   Les colonnes d’extension de données importées peuvent ensuite être utilisées par le composant AEM **Texte et personnalisation**.

### Configuration de Silverpop via Outils {#configuring-silverpop-via-tools}

Pour créer une configuration Silverpop dans Outils :

1. Dans AEM, appuyez ou cliquez sur **Outils** > **Déploiement** > **Services cloud**. Ou naviguez là directement en allant à `https://<hostname>:<port>/misadmin#/etc`.
1. Sélectionnez **Outils**, puis **Configuration des services en cloud** et ensuite **Silverpop Engage**.
1. Cliquez sur **Nouveau** pour ouvrir la fenêtre **Créer une page**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. Saisissez le **titre** et éventuellement le **nom**, puis cliquez sur **Créer**.
1. Saisissez les informations de configuration conformément à l’étape 4 de la procédure précédente. Suivez cette procédure pour terminer la configuration de Silverpop.

### Ajout de plusieurs configurations {#adding-multiple-configurations}

Pour ajouter plusieurs configurations, procédez comme suit :

1. Sur la page de bienvenue, cliquez sur **Services cloud** et cliquez sur **Silverpop Engage**. Click on **Show Configurations** button which appears if one or more Silverpop configurations is available. Toutes les configurations disponibles sont répertoriées.
1. Cliquez sur le lien **+** en regard de Configurations disponibles. Cette action ouvre la fenêtre **Créer une configuration**. Pour créer une autre configuration, suivez la procédure de configuration précédente.

### Configuration des points de terminaison d’API pour se connecter à Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Actuellement, AEM comporte six points de terminaison non sécurisés (Engage 1 à 6). Silverpop fournit désormais deux nouveaux points de terminaison, de même que des points de terminaison de connexion modifiés pour les existants.

Pour configurer les points de terminaison d’API :

1. Atteindre `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` le `https://<hostname>:<port>/crxde.`
1. Cliquez avec le bouton droit et sélectionnez **Créer**, puis **Créer un nœud**.
1. Enter the **Name** as `sp-e0` and choose **Type** as `cq:Widget`.
1. Ajoutez deux propriétés au nœud que vous venez de créer :

   1. **Nom**: `text`, **Type**: `String`, **Valeur**: `Engage 0`
   1. **Nom**: `value`, **Type**: `String`, **Valeur**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Cliquez sur le bouton Enregistrer tout.

1. Create one more node with **Name** as `sp-e7` and **Type** as `cq:Widget`.

   Ajoutez deux propriétés au nœud que vous venez de créer :

   1. **Nom**: `text`, **Type**: `String`, **Valeur**: `Pilot`
   1. **Nom**: `value`, **Type**: `String`, **Valeur**: `https://apipilot.silverpop.com/XMLAPI`

1. Pour modifier les points de terminaison d’API existants (Engage 1 à 6), cliquez sur chacun d’entre eux un par un et remplacez les valeurs comme suit :

   | **Nom du nœud** | **Valeur du point de terminaison existant** | **Nouvelle valeur de point de fin** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Cliquez sur **Enregistrer tout**. AEM est maintenant prêt à se connecter à Silverpop via des points de terminaison sécurisés.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)

