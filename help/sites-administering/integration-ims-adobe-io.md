---
title: Intégration à Adobe Target à l’aide d’Adobe I/O
seo-title: Intégration à Adobe Target à l’aide d’Adobe I/O
description: Découvrez comment intégrer des AEM à Adobe Target à l'aide des E/S d'Adobe
seo-description: Découvrez comment intégrer des AEM à Adobe Target à l'aide des E/S d'Adobe
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: d12ebf77d2af389e0a3aea5c7f311c828ecd7c17
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 11%

---


# Intégration à Adobe Target à l’aide d’Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

L’intégration de l’AEM avec Adobe Target via l’API Target Standard nécessite la configuration de l’Adobe IMS (Identity Management System) et des E/S Adobes.

>[!NOTE]
>
>La prise en charge de l’API Adobe Target Standard est une nouveauté dans AEM 6.5. L’API Target Standard utilise l’authentification IMS.
>
>L’utilisation de l’API Adobe Target Classic dans AEM est toujours prise en charge pour la compatibilité ascendante. L’API [Cible Classic utilise l’authentification](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)des informations d’identification de l’utilisateur.
>
>La sélection de l’API est pilotée par la méthode d’authentification utilisée pour l’intégration AEM/Cible.

## Conditions préalables {#prerequisites}

Avant de commencer cette procédure :

* [L&#39;assistance](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) Adobe doit prévoir votre compte pour :

   * Adobe Console
   * E/S Adobe
   * Adobe Target et
   * Adobe IMS (système Identity Management)

* L’administrateur système de votre entreprise doit utiliser le Admin Console pour ajouter les développeurs requis de votre entreprise aux profils de produits appropriés.

   * Cela permet aux développeurs spécifiques d&#39;activer les intégrations dans les E/S d&#39;Adobe.
   * Pour plus d’informations, voir [Gérer les développeurs](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuration d&#39;une configuration IMS - Génération d&#39;une clé publique {#configuring-an-ims-configuration-generating-a-public-key}

La première étape de la configuration consiste à créer une configuration IMS dans AEM et à générer la clé publique.

1. Dans AEM, ouvrez le menu **Outils** .
1. Dans la section **Sécurité** , sélectionnez Configurations **IMS** Adobe.
1. Sélectionnez **Créer** pour ouvrir l&#39; **Adobe Configuration** du compte technique IMS.
1. Dans la liste déroulante sous Configuration **** Cloud, sélectionnez **Adobe Target**.
1. Activer **Créez un nouveau certificat** et saisissez un nouvel alias.
1. Confirmez avec **Créer un certificat**.

   ![](assets/integrate-target-io-01.png)

1. Sélectionnez **Télécharger** (ou **Télécharger la clé** publique) pour télécharger le fichier sur votre lecteur local, de sorte qu&#39;il soit prêt à être utilisé lors de la [configuration des E/S d&#39;Adobe pour l&#39;intégration Adobe Target avec AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Gardez cette configuration ouverte, elle sera nécessaire à nouveau lors de l&#39; [achèvement de la configuration IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuration des E/S d&#39;Adobe pour l&#39;intégration Adobe Target avec AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Vous devez créer le projet d&#39;E/S d&#39;Adobe (intégration) avec Adobe Target que AEM utilisera, puis attribuer les privilèges requis.

### Création du projet {#creating-the-project}

Ouvrez la console d&#39;E/S Adobe pour créer un projet d&#39;E/S avec Adobe Target que l&#39;AEM utilisera :

>[!NOTE]
>
>Consultez également les didacticiels [d&#39;E/S](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)Adobe.

1. Ouvrez la console d&#39;E/S Adobe pour les projets :

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Tous les projets que vous avez seront affichés. Sélectionnez **Créer un nouveau projet** - l&#39;emplacement et l&#39;utilisation dépendent :

   * Si vous n&#39;avez pas encore de projet, **Créer un nouveau projet** sera au centre, en bas.
      ![Créer un nouveau projet - Premier projet](assets/integration-target-io-02.png)
   * Si vous avez déjà des projets existants, ceux-ci seront répertoriés et **Créer un nouveau projet** sera en haut à droite.
      ![Créer un projet - Plusieurs projets](assets/integration-target-io-03.png)


1. Sélectionnez **Ajouter au projet** , puis **API**:

   ![](assets/integration-target-io-10.png)

1. Sélectionnez **Adobe Target**, puis **Suivant**:

   >[!NOTE]
   >
   >Si vous êtes abonné à Adobe Target, mais que vous ne le voyez pas dans la liste, vous devez vérifier les [conditions préalables](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Téléchargez votre clé** publique et, une fois l’opération terminée, poursuivez avec **Suivant**:

   ![](assets/integration-target-io-13.png)

1. Vérifiez les informations d’identification et continuez avec **Suivant**:

   ![](assets/integration-target-io-15.png)

1. Sélectionnez les profils de produit requis et continuez avec l’API **configurée** Enregistrer :

   >[!NOTE]
   >
   >Les profils de produit affichés dépendent si vous avez :
   >
   >* Adobe Target Standard - Seul l’espace de travail **** par défaut est disponible
   >* Adobe Target Premium - tous les espaces de travail disponibles sont répertoriés, comme illustré ci-dessous.


   ![](assets/integration-target-io-16.png)

1. La création sera confirmée.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Attribution de privilèges à l’intégration {#assigning-privileges-to-the-integration}

Vous devez maintenant attribuer les privilèges requis à l’intégration :

1. Ouvrez l’Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Accédez à **Produits** (barre d’outils supérieure), puis sélectionnez **Adobe Target - &lt;*votre-locataire-id*>** (dans le panneau de gauche).
1. Sélectionnez Profils **** de produits, puis l’espace de travail requis dans la liste présentée. Par exemple, Espace de travail par défaut.
1. Sélectionnez **Intégrations**, puis la configuration d’intégration requise.
1. Sélectionnez **Editeur** comme rôle **de** produit ; plutôt que **Observer**.

## Détails stockés pour le projet d&#39;intégration E/S d&#39;Adobe {#details-stored-for-the-adobe-io-integration-project}

Dans la console Projets d&#39;E/S d&#39;Adobe, vous pouvez voir une liste de tous vos projets d&#39;intégration :

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Sélectionnez **Vue** (à droite d&#39;une entrée de projet spécifique) pour afficher d&#39;autres détails sur la configuration. Celles-ci comprennent :

* Présentation du projet
* Statistiques
* Informations d’identification
   * Compte de service (JWT)
      * Informations d’identification
      * Générer JWT
* APIS
   * Par exemple, Adobe Target

Certains d&#39;entre eux devront compléter l&#39;intégration E/S Adobe pour la Cible en AEM.

## Fin de la configuration IMS en AEM {#completing-the-ims-configuration-in-aem}

Pour revenir à AEM, vous pouvez terminer la configuration IMS en ajoutant les valeurs requises de l&#39;intégration E/S Adobe pour la Cible :

1. Revenez à la configuration [IMS ouverte dans AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Sélectionnez **Suivant**.

1. Vous pouvez utiliser ici les [détails des E/S](#details-stored-for-the-adobe-io-integration-project)Adobe :

   * **Titre**: Votre texte.
   * **Serveur** d&#39;autorisation : Copiez/collez ceci à partir de la `"aud"` ligne de la section **Charge** ci-dessous, par exemple `"https://ims-na1.adobelogin.com"` dans l’exemple ci-dessous.
   * **Clé** API : Copiez ceci de la section [Aperçu](#details-stored-for-the-adobe-io-integration-project) de l&#39;intégration E/S Adobe pour la Cible
   * **Secret** client : Générez-la dans la section [Aperçu](#details-stored-for-the-adobe-io-integration-project) de l&#39;intégration E/S Adobe pour la Cible, puis copiez-la
   * **Charge utile**: Copiez ceci de la section [Générer JWT](#details-stored-for-the-adobe-io-integration-project) de l&#39;intégration E/S Adobe pour la Cible

   ![](assets/integrate-target-io-10.png)

1. Confirmez avec **Créer**.

1. Votre configuration Adobe Target s&#39;affichera dans la console AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmation de la configuration IMS {#confirming-the-ims-configuration}

Pour confirmer que la configuration fonctionne comme prévu :

1. Ouvrez :

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Par exemple :

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Sélectionnez votre configuration.
1. Sélectionnez **Vérifier l’intégrité** dans la barre d’outils, puis **Vérifier**.

   ![](assets/integrate-target-io-12.png)

1. En cas de réussite, le message suivant s’affiche :

   ![](assets/integrate-target-io-13.png)

## Configuration de l’Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

La configuration peut désormais être référencée pour qu’un Cloud Service utilise l’API Target Standard :

1. Open the **Tools** menu. Puis, dans la section **Cloud Services** , sélectionnez Cloud Services **** hérités.
1. Faites défiler l&#39;écran jusqu&#39;à **Adobe Target** et sélectionnez **Configurer maintenant**.

   La boîte de dialogue **Créer une configuration** s’ouvre.

1. Saisissez un **Titre** et, si vous le souhaitez, un **Nom** (si rien n’est indiqué, ce champ sera généré à partir du titre).

   Vous pouvez également sélectionner le modèle requis (si plusieurs modèles sont disponibles).

1. Confirmez avec **Créer**.

   La boîte de dialogue **Modifier le composant** s&#39;ouvre.

1. Saisissez les détails dans l’onglet Paramètres **** Adobe Target :

   * **Authentification**: IMS
   * **ID** du client : l&#39;Adobe IMS - ID de client
   * **Configuration** IMS : sélectionner le nom de la configuration IMS
   * **Type** d&#39;API : REPOSE
   * **Configuration d’A4T Analytics Cloud** : sélectionnez la configuration de cloud Analytics utilisée pour les objectifs et les mesures des activités de Target. Vous avez besoin de cette option si vous utilisez Adobe Analytics en tant que source de création de rapports lors du ciblage de contenu. If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Utiliser un ciblage** précis : Cette case à cocher est activée par défaut. Si cette option est sélectionnée, la configuration du service cloud attend le chargement du contexte avant de charger le contenu. Voir la remarque qui suit.
   * **Synchroniser les segments à partir d’Adobe Target**: Sélectionnez cette option pour télécharger les segments définis dans la Cible afin de les utiliser dans AEM. Vous devez sélectionner cette option lorsque la propriété Type d’API est REST, car les segments incorporés ne sont pas pris en charge, et vous devez toujours utiliser les segments de Target. (Notez que le terme « segment » d’AEM équivaut à « audience » dans Target.)
   * **Bibliothèque** client : Indiquez si vous souhaitez utiliser la bibliothèque cliente AT.js ou mbox.js (obsolète).
   * **Utilisez le système de gestion des balises pour fournir la bibliothèque** cliente : Utilisez la gestion dynamique des balises (obsolète), le lancement d’Adobe ou tout autre système de gestion des balises.
   * **Personnaliser AT.js**: Laissez ce champ vide si vous avez coché la case Gestion des balises ou pour utiliser AT.js par défaut. Vous pouvez également télécharger votre fichier AT.js personnalisé.  S’affiche uniquement si vous avez sélectionné AT.js.

   >[!NOTE]
   >
   >[La configuration d’un Cloud Service pour l’utilisation de l’API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) Cible Classic a été abandonnée (utilise l’onglet Paramètres Adobe Recommendations).

   Par exemple :

   ![](assets/integrate-target-io-14.png)

1. Click **Connect to Target** to initialize the connection with Adobe Target.

   If the connection is successful, the message **Connection successful** is displayed.

1. Sélectionnez **OK** dans le message, puis **OK** dans la boîte de dialogue pour confirmer la configuration.
1. Vous pouvez maintenant [Ajouter une structure](/help/sites-administering/target-configuring.md#adding-a-target-framework) de Cible pour configurer ContextHub ou les paramètres de ClientContext qui seront envoyés à Cible. Notez que cela peut ne pas être nécessaire pour exporter des fragments d’expérience AEM vers la Cible.

