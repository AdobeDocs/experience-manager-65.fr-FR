---
title: Intégration à Adobe Target à l’aide d’Adobe I/O
seo-title: Intégration à Adobe Target à l’aide d’Adobe I/O
description: En savoir plus sur l’intégration d’AEM à Adobe Target à l’aide d’Adobe I/O
seo-description: En savoir plus sur l’intégration d’AEM à Adobe Target à l’aide d’Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 18%

---

# Intégration à Adobe Target à l’aide d’Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

L’intégration d’AEM avec Adobe Target via l’API Target Standard nécessite la configuration d’Adobe IMS (système Identity Management) et d’Adobe I/O.

>[!NOTE]
>
>La prise en charge de l’API Adobe Target Standard est nouvelle dans AEM 6.5. L’API Target Standard utilise l’authentification IMS.
>
>L’utilisation de l’API Adobe Target Classic dans AEM est toujours prise en charge à des fins de rétrocompatibilité. L’API [Target Classic utilise l’authentification des informations d’identification de l’utilisateur](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La sélection de l’API repose sur la méthode d’authentification utilisée pour l’intégration AEM/Target.
>Voir aussi la section [ID de client et code client](#tenant-client) .

## Prérequis {#prerequisites}

Avant de commencer cette procédure :

* [L’](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) assistance Adobe doit configurer votre compte pour :

   * Adobe Console
   * Adobe I/O
   * Adobe Target et
   * Adobe IMS (système Identity Management)

* L’administrateur système de votre entreprise doit utiliser le Admin Console pour ajouter les développeurs requis de votre entreprise aux profils de produit appropriés.

   * Les développeurs spécifiques disposent ainsi des autorisations nécessaires pour activer les intégrations dans Adobe I/O.
   * Pour plus d’informations, voir [Gestion des développeurs](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuration d’une configuration IMS - Génération d’une clé publique {#configuring-an-ims-configuration-generating-a-public-key}

La première étape de la configuration consiste à créer une configuration IMS dans AEM et à générer la clé publique.

1. Dans AEM, ouvrez le menu **Outils** .
1. Dans la section **Sécurité**, sélectionnez **Adobe des configurations IMS**.
1. Sélectionnez **Créer** pour ouvrir la **Configuration du compte technique IMS d’Adobe**.
1. Dans la liste déroulante sous **Configuration du cloud**, sélectionnez **Adobe Target**.
1. Activez **Créer un certificat** et saisissez un nouvel alias.
1. Confirmez avec **Créer un certificat**.

   ![](assets/integrate-target-io-01.png)

1. Sélectionnez **Télécharger** (ou **Télécharger la clé publique**) pour télécharger le fichier sur votre lecteur local, de sorte qu’il soit prêt à être utilisé lors de la configuration de l’Adobe I/O pour l’intégration d’Adobe Target avec AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).[

   >[!CAUTION]
   >
   >Gardez cette configuration ouverte. Elle sera nécessaire à nouveau lorsque [la configuration IMS sera terminée dans AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuration de l’Adobe I/O pour l’intégration d’Adobe Target avec AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Vous devez créer le projet Adobe I/O (intégration) avec Adobe Target que AEM utilisera, puis attribuer les privilèges requis.

### Création du projet {#creating-the-project}

Ouvrez la console Adobe I/O pour créer un projet I/O avec Adobe Target qui AEM utiliser :

>[!NOTE]
>
>Voir aussi les [tutoriels sur l’Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Ouvrez la console Adobe I/O pour Projets :

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Tous les projets que vous avez s’affichent. Sélectionnez **Créer un projet**. L’emplacement et l’utilisation dépendent de :

   * Si vous n’avez pas encore de projet, **Créer un nouveau projet** sera centré, en bas.
      ![Créer un projet - Premier projet](assets/integration-target-io-02.png)
   * Si vous avez déjà des projets existants, ils sont répertoriés et **Créer un projet** s’affiche en haut à droite.
      ![Créer un projet - Projets multiples](assets/integration-target-io-03.png)


1. Sélectionnez **Ajouter au projet** suivi de **API** :

   ![](assets/integration-target-io-10.png)

1. Sélectionnez **Adobe Target**, puis **Suivant** :

   >[!NOTE]
   >
   >Si vous êtes abonné à Adobe Target, mais que vous ne le voyez pas répertorié, vous devez cocher les [Conditions préalables](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Téléchargez votre clé** publique et, une fois l’opération terminée, continuez avec  **Suivant** :

   ![](assets/integration-target-io-13.png)

1. Passez en revue les informations d’identification, puis continuez avec **Suivant** :

   ![](assets/integration-target-io-15.png)

1. Sélectionnez les profils de produit requis et continuez avec **Enregistrer l’API configurée** :

   >[!NOTE]
   >
   >Les profils de produits affichés avec dépendent si vous disposez des éléments suivants :
   >
   >* Adobe Target Standard - Seul **Workspace par défaut** est disponible
   >* Adobe Target Premium : tous les espaces de travail disponibles sont répertoriés, comme illustré ci-dessous.


   ![](assets/integration-target-io-16.png)

1. La création sera confirmée.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Attribution de privilèges à l’intégration {#assigning-privileges-to-the-integration}

Vous devez maintenant attribuer les privilèges requis à l’intégration :

1. Ouvrez l’Adobe **Admin Console** :

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Accédez à **Produits** (barre d’outils supérieure), puis sélectionnez **Adobe Target - &quot;a3/>your-tenant-id ***(dans le panneau de gauche).*
1. Sélectionnez **Profils de produit**, puis l’espace de travail requis dans la liste présentée. Par exemple, Espace de travail par défaut.
1. Sélectionnez **Intégrations**, puis la configuration d’intégration requise.
1. Sélectionnez **Éditeur** comme **Rôle du produit** ; au lieu de **Observer**.

## Détails stockés pour le projet d’intégration Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Dans la console Projets d’Adobe I/O , vous pouvez voir la liste de tous vos projets d’intégration :

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Sélectionnez **Afficher** (à droite d’une entrée de projet spécifique) pour afficher plus de détails sur la configuration. Celles-ci comprennent :

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

1. Revenez à la [Configuration IMS ouverte dans AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Sélectionnez **Suivant**.

1. Ici, vous pouvez utiliser les [détails de l’Adobe I/O](#details-stored-for-the-adobe-io-integration-project) :

   * **Titre** : Votre texte.
   * **Serveur d’autorisation** : Copiez/collez ceci à partir de la  `"aud"` ligne de la section  **** Payload ci-dessous, par exemple  `"https://ims-na1.adobelogin.com"` dans l’exemple ci-dessous.
   * **Clé** API : Copiez-le dans la section  [](#details-stored-for-the-adobe-io-integration-project) Présentation de l’intégration Adobe I/O pour Target
   * **Client Secret** : Générez-le dans la section  [](#details-stored-for-the-adobe-io-integration-project) Présentation de l’intégration Adobe I/O pour Target, puis copiez
   * **Charge utile** : Copiez ceci dans la section  [Générer ](#details-stored-for-the-adobe-io-integration-project) JWT de l’intégration Adobe I/O pour Target

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
1. Sélectionnez **Vérifier l’intégrité** dans la barre d’outils, puis **Vérifier**.

   ![](assets/integrate-target-io-12.png)

1. En cas de réussite, le message suivant s’affiche :

   ![](assets/integrate-target-io-13.png)

## Configuration du Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

La configuration peut désormais être référencée pour qu’un Cloud Service utilise l’API Target Standard :

1. Ouvrez le menu **Outils** . Ensuite, dans la section **Cloud Services**, sélectionnez **Cloud Services hérités**.
1. Faites défiler l’écran jusqu’à **Adobe Target** et sélectionnez **Configurer maintenant**.

   La boîte de dialogue **Créer une configuration** s’ouvre.

1. Saisissez un **Titre** et, si vous le souhaitez, un **Nom** (si rien n’est indiqué, cela sera généré à partir du titre).

   Vous pouvez également sélectionner le modèle requis (si plusieurs modèles sont disponibles).

1. Confirmez avec **Créer**.

   La boîte de dialogue **Modifier le composant** s’ouvre.

1. Saisissez les détails dans l’onglet **Paramètres Adobe Target** :

   * **Authentification** : IMS
   * **ID** du client : Identifiant du tenant IMS de l’Adobe. Voir aussi la section [ID de client et code client](#tenant-client) .

      >[!NOTE]
      >
      >Pour IMS, cette valeur doit être extraite de Target. Vous pouvez vous connecter à Target et extraire l’ID de tenant de l’URL.
      >
      >Par exemple, si l’URL est :
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Vous utiliserez ensuite `yourtenantid`.
   * **Code client** : Voir l’identifiant  [du client et la ](#tenant-client) description du client.
   * **Configuration IMS** : sélectionnez le nom de la configuration IMS.
   * **Type** d’API : REST
   * **Configuration d’A4T Analytics Cloud** : sélectionnez la configuration de cloud Analytics utilisée pour les objectifs et les mesures des activités de Target. Vous avez besoin de cette option si vous utilisez Adobe Analytics en tant que source de création de rapports lors du ciblage de contenu. Si vous ne voyez pas votre configuration de cloud, voir la note dans [Configuration de A4T Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Utilisez un ciblage** précis : Cette case est cochée par défaut. Si cette option est sélectionnée, la configuration du service cloud attend le chargement du contexte avant de charger le contenu. Voir la remarque qui suit.
   * **Synchroniser les segments à partir d’Adobe Target** : Sélectionnez cette option pour télécharger les segments définis dans Target afin de les utiliser dans AEM. Vous devez sélectionner cette option lorsque la propriété Type d’API est REST, car les segments incorporés ne sont pas pris en charge, et vous devez toujours utiliser les segments de Target. (Notez que le terme « segment » d’AEM équivaut à « audience » dans Target.)
   * **Bibliothèque** cliente : Indiquez si vous souhaitez utiliser la bibliothèque cliente AT.js ou mbox.js (obsolète).
   * **Utilisez Tag Management System pour diffuser la bibliothèque** cliente : Utilisez DTM (obsolète), Adobe Launch ou tout autre système de gestion des balises.
   * **Fichier AT.js personnalisé** : Laissez ce champ vide si vous avez coché la case Gestion des balises ou pour utiliser le fichier AT.js par défaut. Vous pouvez également télécharger votre fichier AT.js personnalisé.  S’affiche uniquement si vous avez sélectionné AT.js.

   >[!NOTE]
   >
   >[La configuration d’un Cloud Service pour utiliser l’](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API Target Classic a été abandonnée (à l’aide de l’onglet Paramètres d’Adobe Recommendations).
1. Cliquez sur **Se connecter à Target** pour initialiser la connexion à Adobe Target.

   Si la connexion est établie, le message **Connexion réussie** s’affiche.

1. Sélectionnez **OK** dans le message, puis **OK** dans la boîte de dialogue pour confirmer la configuration.
1. Vous pouvez maintenant passer à [Ajout d’une structure Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) pour configurer ContextHub ou des paramètres de ClientContext qui seront envoyés à Target. Notez que cela n’est peut-être pas nécessaire pour exporter AEM fragments d’expérience vers Target.

### Identifiant du client et code client {#tenant-client}

Avec [Adobe Experience Manager 6.5.8.0](/help/release-notes/sp-release-notes.md), le champ Code client a été ajouté à la fenêtre de configuration de Target.

Lors de la configuration des champs Identifiant du client et Code client, veuillez tenir compte des points suivants :

1. Pour la plupart des clients, l’ID de client et le code client sont identiques. Cela signifie que les deux champs contiennent les mêmes informations et sont identiques. Veillez à saisir l’identifiant du client dans les deux champs.
2. Pour des raisons d’héritage, vous pouvez également entrer différentes valeurs dans les champs d’ID client et de Code client.

Dans les deux cas, il faut savoir que :

* par défaut, le code client (s’il est ajouté en premier) sera également automatiquement copié dans le champ d’ID client ;
* vous avez la possibilité de modifier le jeu d’ID client par défaut.
* Par conséquent, les appels du serveur principal vers Target sont basés sur l’ID client et les appels vers Target côté client sont basés sur le Code client.

Comme indiqué précédemment, le premier cas est le plus courant pour AEM 6.5. Dans les deux cas, assurez-vous que les champs **deux** contiennent les informations correctes en fonction de vos besoins.

>[!NOTE]
>
> Si vous souhaitez modifier une configuration Target existante :
>
> 1. saisissez de nouveau l’ID client ;
> 2. reconnectez-vous à Target ;
> 3. enregistrez la configuration.

