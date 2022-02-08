---
title: Intégration à Adobe Target à l’aide d’Adobe I/O
seo-title: Integration with Adobe Target using Adobe I/O
description: En savoir plus sur l’intégration d’AEM à Adobe Target à l’aide d’Adobe I/O
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: bf55553f48c1eddf5dec503fb105cf35ff26677d
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 18%

---

# Intégration à Adobe Target à l’aide d’Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

L’intégration d’AEM avec Adobe Target via l’API Target Standard nécessite la configuration d’Adobe IMS (système Identity Management) et d’Adobe I/O.

>[!NOTE]
>
>La prise en charge de l’API Adobe Target Standard est nouvelle dans AEM 6.5. L’API Target Standard utilise l’authentification IMS.
>
>L’utilisation de l’API Adobe Target Classic dans AEM est toujours prise en charge à des fins de rétrocompatibilité. Le [L’API Target Classic utilise l’authentification des informations d’identification d’utilisateur](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La sélection de l’API repose sur la méthode d’authentification utilisée pour l’intégration AEM/Target.
>Voir aussi [ID de client et code client](#tenant-client) .

## Prérequis {#prerequisites}

Avant de commencer cette procédure :

* [Prise en charge des Adobes](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) doit configurer votre compte pour :

   * Adobe Console
   * Adobe I/O
   * Adobe Target et
   * Adobe IMS (système Identity Management)

* L’administrateur système de votre entreprise doit utiliser le Admin Console pour ajouter les développeurs requis de votre entreprise aux profils de produit appropriés.

   * Les développeurs spécifiques disposent ainsi des autorisations nécessaires pour activer les intégrations dans Adobe I/O.
   * Pour plus d’informations, voir [Gestion des développeurs](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuration d’une configuration IMS - Génération d’une clé publique {#configuring-an-ims-configuration-generating-a-public-key}

La première étape de la configuration consiste à créer une configuration IMS dans AEM et à générer la clé publique.

1. Dans AEM, ouvrez le **Outils** .
1. Dans le **Sécurité** section select **Configurations d’Adobe IMS**.
1. Sélectionner **Créer** pour ouvrir le **Configuration du compte technique Adobe IMS**.
1. Utilisation de la liste déroulante sous **Configuration du cloud**, sélectionnez **Adobe Target**.
1. Activer **Création d’un certificat** et saisissez un nouvel alias.
1. Confirmer avec **Création d’un certificat**.

   ![](assets/integrate-target-io-01.png)

1. Sélectionner **Télécharger** (ou **Télécharger la clé publique**) pour télécharger le fichier sur votre lecteur local, afin qu’il soit prêt à être utilisé lors de la [configuration de l’Adobe I/O pour l’intégration d’Adobe Target avec AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Gardez cette configuration ouverte. Elle sera nécessaire à nouveau lorsque [Réalisation de la configuration IMS dans AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuration de l’Adobe I/O pour l’intégration d’Adobe Target avec AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Vous devez créer le projet Adobe I/O (intégration) avec Adobe Target que AEM utilisera, puis attribuer les privilèges requis.

### Création du projet {#creating-the-project}

Ouvrez la console Adobe I/O pour créer un projet I/O avec Adobe Target qui AEM utiliser :

>[!NOTE]
>
>Voir aussi [Tutoriels sur l’Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Ouvrez la console Adobe I/O pour Projets :

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Tous les projets que vous avez s’affichent. Sélectionner **Créer un projet** - l’emplacement et l’utilisation dépendent de :

   * Si vous n’avez pas encore de projet, **Créer un projet** sera au centre, en bas.
      ![Créer un projet - Premier projet](assets/integration-target-io-02.png)
   * Si vous disposez déjà de projets, ceux-ci sont répertoriés et **Créer un projet** sera en haut à droite.
      ![Créer un projet - Projets multiples](assets/integration-target-io-03.png)


1. Sélectionner **Ajouter au projet** suivie de **API**:

   ![](assets/integration-target-io-10.png)

1. Sélectionner **Adobe Target**, puis **Suivant**:

   >[!NOTE]
   >
   >Si vous êtes abonné à Adobe Target, mais que vous ne le voyez pas répertorié, cochez la case [Conditions préalables](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Chargement de votre clé publique**, puis, une fois l’opération terminée, passez à **Suivant**:

   ![](assets/integration-target-io-13.png)

1. Vérifiez les informations d’identification et continuez avec **Suivant**:

   ![](assets/integration-target-io-15.png)

1. Sélectionnez les profils de produit requis et continuez avec **Enregistrer l’API configurée**:

   >[!NOTE]
   >
   >Les profils de produits affichés avec dépendent si vous disposez des éléments suivants :
   >
   >* Adobe Target Standard - uniquement **Espace de travail par défaut** est disponible
   >* Adobe Target Premium : tous les espaces de travail disponibles sont répertoriés, comme illustré ci-dessous.


   ![](assets/integration-target-io-16.png)

1. La création sera confirmée.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Attribution de privilèges à l’intégration {#assigning-privileges-to-the-integration}

Vous devez maintenant attribuer les privilèges requis à l’intégration :

1. Ouvrir l’Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Accédez à **Produits** (barre d’outils supérieure), puis sélectionnez **Adobe Target - &lt;*your-tenant-id*>** (dans le panneau de gauche).
1. Sélectionner **Profils de produit**, puis l’espace de travail requis dans la liste présentée. Par exemple, Espace de travail par défaut.
1. Sélectionner **Informations d’identification de l’API**, puis la configuration d’intégration requise.
1. Sélectionner **Éditeur** comme la propriété **Rôle de produit**; au lieu de **Observateur**.

## Détails stockés pour le projet d’intégration Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Dans la console Projets d’Adobe I/O , vous pouvez voir la liste de tous vos projets d’intégration :

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Sélectionner **Affichage** (à droite d’une entrée de projet spécifique) pour afficher des détails supplémentaires sur la configuration. Celles-ci comprennent les éléments suivants :

* Présentation du projet
* Statistiques
* Informations d’identification
   * Compte de service (JWT)
      * Informations d’identification
      * Génération de JWT
* API
   * Par exemple, Adobe Target

Certains d’entre eux vous devrez terminer l’intégration Adobe I/O pour Target dans AEM.

## Réalisation de la configuration IMS dans AEM {#completing-the-ims-configuration-in-aem}

Pour revenir à AEM, vous pouvez terminer la configuration IMS en ajoutant les valeurs requises de l’intégration Adobe I/O pour Target :

1. Revenez au [Configuration IMS ouverte dans AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Sélectionnez **Suivant**.

1. Ici, vous pouvez utiliser la variable [détails de l’Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Titre**: Votre texte.
   * **Serveur d’autorisation**: Copiez/collez ceci à partir du `aud` de la ligne **Payload** ci-dessous, par exemple `https://ims-na1.adobelogin.com` dans l’exemple ci-dessous
   * **Clé API**: Copiez-le depuis le [Présentation](#details-stored-for-the-adobe-io-integration-project) section de l’intégration Adobe I/O pour Target
   * **Secret du client**: Générez-le dans le [Présentation](#details-stored-for-the-adobe-io-integration-project) section de l’intégration Adobe I/O pour Target et copie
   * **Payload**: Copiez-le depuis le [Génération de JWT](#details-stored-for-the-adobe-io-integration-project) section de l’intégration Adobe I/O pour Target

   ![](assets/integrate-target-io-10.png)

1. Confirmez avec **Créer**.

1. Votre configuration Adobe Target s’affichera dans la console AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmation de la configuration IMS {#confirming-the-ims-configuration}

Pour confirmer que la configuration fonctionne comme prévu :

1. Ouvrez :

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Par exemple :

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Sélectionnez votre configuration.
1. Sélectionner **Contrôle de l’intégrité** de la barre d’outils, suivie de **Vérifier**.

   ![](assets/integrate-target-io-12.png)

1. En cas de réussite, le message suivant s’affiche :

   ![](assets/integrate-target-io-13.png)

## Configuration du Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

La configuration peut désormais être référencée pour qu’un Cloud Service utilise l’API Target Standard :

1. Ouvrez le **Outils** . Ensuite, dans la variable **Cloud Services** , sélectionnez **Cloud Services hérités**.
1. Faites défiler jusqu’à **Adobe Target** et sélectionnez **Configurer maintenant**.

   Le **Créer une configuration** s’ouvre.

1. Saisissez un **Titre** et, si vous le souhaitez, un **Nom** (si rien n’est indiqué, cela sera généré à partir du titre).

   Vous pouvez également sélectionner le modèle requis (si plusieurs modèles sont disponibles).

1. Confirmez avec **Créer**.

   Le **Modifier le composant** s’ouvre.

1. Saisissez les détails dans le champ **Paramètres Adobe Target** tab :

   * **Authentification**: IMS

   * **Identifiant du client**: Identifiant du tenant Adobe IMS. Voir aussi [ID de client et code client](#tenant-client) .

      >[!NOTE]
      >
      >Pour IMS, cette valeur doit être extraite de Target. Vous pouvez vous connecter à Target et extraire l’ID de tenant de l’URL.
      >
      >Par exemple, si l’URL est :
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Vous pouvez alors utiliser `yourtenantid`.

   * **Code client**: Voir [ID de client et code client](#tenant-client) .

   * **Configuration IMS**: sélectionnez le nom de la configuration IMS.

   * **Type d’API**: REST

   * **Configuration d’A4T Analytics Cloud** : sélectionnez la configuration de cloud Analytics utilisée pour les objectifs et les mesures des activités de Target. Vous avez besoin de cette option si vous utilisez Adobe Analytics en tant que source de création de rapports lors du ciblage de contenu. Si vous ne voyez pas votre configuration cloud, reportez-vous à la remarque de la section [Configuration de la configuration d’Analytics Cloud A4T](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **Utiliser un ciblage précis**: Cette case est cochée par défaut. Si cette option est sélectionnée, la configuration du service cloud attend le chargement du contexte avant de charger le contenu. Voir la remarque qui suit.

   * **Synchronisation des segments à partir d’Adobe Target**: Sélectionnez cette option pour télécharger les segments définis dans Target afin de les utiliser dans AEM. Vous devez sélectionner cette option lorsque la propriété Type d’API est REST, car les segments incorporés ne sont pas pris en charge, et vous devez toujours utiliser les segments de Target. (Notez que le terme « segment » d’AEM équivaut à « audience » dans Target.)

   * **Bibliothèque cliente**: Indiquez si vous souhaitez utiliser la bibliothèque cliente AT.js ou mbox.js (obsolète).

   * **Utilisation du système de gestion des balises pour diffuser la bibliothèque cliente**: Utilisez DTM (obsolète), Adobe Launch ou tout autre système de gestion des balises.

   * **Fichier AT.js personnalisé**: Laissez ce champ vide si vous avez coché la case Gestion des balises ou pour utiliser le fichier AT.js par défaut. Vous pouvez également télécharger votre fichier AT.js personnalisé.  S’affiche uniquement si vous avez sélectionné AT.js.
   >[!NOTE]
   >
   >[Configuration d’un Cloud Service pour utiliser l’API Target Classic](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) est obsolète (utilise l’onglet Paramètres d’Adobe Recommendations ).

1. Cliquez sur **Connexion à Target** pour initialiser la connexion avec Adobe Target.

   Si la connexion est établie, le message **Connexion réussie** s’affiche.

1. Sélectionner **OK** sur le message, suivi de **OK** dans la boîte de dialogue pour confirmer la configuration.

1. Vous pouvez maintenant procéder à la [Ajout d’une structure Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) pour configurer les paramètres ContextHub ou de ClientContext qui seront envoyés à Target. Notez que cela n’est peut-être pas nécessaire pour exporter AEM fragments d’expérience vers Target.

### ID de client et code client {#tenant-client}

Avec [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md), le champ Code client a été ajouté à la fenêtre de configuration de Target.

Lors de la configuration des champs Identifiant du client et Code client, veuillez tenir compte des points suivants :

1. Pour la plupart des clients, l’ID de client et le code client sont identiques. Cela signifie que les deux champs contiennent les mêmes informations et sont identiques. Veillez à saisir l’identifiant du client dans les deux champs.
2. Pour des raisons d’héritage, vous pouvez également entrer différentes valeurs dans les champs d’ID client et de Code client.

Dans les deux cas, il faut savoir que :

* par défaut, le code client (s’il est ajouté en premier) sera également automatiquement copié dans le champ d’ID client ;
* vous avez la possibilité de modifier le jeu d’ID client par défaut.
* Par conséquent, les appels du serveur principal vers Target sont basés sur l’ID client et les appels vers Target côté client sont basés sur le Code client.

Comme indiqué précédemment, le premier cas est le plus courant pour AEM 6.5. Dans les deux cas, assurez-vous que **both** contiennent les informations correctes en fonction de vos besoins.

>[!NOTE]
>
> Si vous souhaitez modifier une configuration Target existante :
>
> 1. saisissez de nouveau l’ID client ;
> 2. reconnectez-vous à Target ;
> 3. enregistrez la configuration.

