---
title: Intégration à Adobe Target à l’aide des E/S Adobe
seo-title: Intégration à Adobe Target à l’aide des E/S Adobe
description: Découvrez comment intégrer AEM à Adobe Target à l’aide des E/S Adobe
seo-description: Découvrez comment intégrer AEM à Adobe Target à l’aide des E/S Adobe
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: f476091236018c826ae303b4b0fc32c691318f79

---


# Intégration à Adobe Target à l’aide des E/S Adobe{#integration-with-adobe-target-using-adobe-i-o}

L’intégration d’AEM à Adobe Target via l’API Target Standard requiert la configuration d’Adobe IMS (Identity Management System) et des E/S Adobe.

>[!NOTE]
>
>La prise en charge de l’API Adobe Target Standard est une nouveauté dans AEM 6.5. L’API Target Standard utilise l’authentification IMS.
>
>L’utilisation de l’API Adobe Target Classic dans AEM est toujours prise en charge pour la compatibilité ascendante. L’API [Target Classic utilise l’authentification](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)des informations d’identification de l’utilisateur.
>
>La sélection de l’API dépend de la méthode d’authentification utilisée pour l’intégration d’AEM/Target.

## Conditions préalables {#prerequisites}

Avant de démarrer cette procédure, [Adobe Support](https://helpx.adobe.com/contact/enterprise-support.ec.html) doit configurer votre compte pour :

* Adobe Console
* E/S Adobe
* Adobe Target et
* Adobe IMS (Identity Management System)

## Configuration d’une configuration IMS - Génération d’une clé publique {#configuring-an-ims-configuration-generating-a-public-key}

La première étape de la configuration consiste à créer une configuration IMS dans AEM et à générer la clé publique.

1. Dans AEM, ouvrez le menu **Outils** .
1. Dans la section **Sécurité** , sélectionnez Configurations **Adobe IMS**.
1. Sélectionnez **Créer** pour ouvrir la configuration **du compte technique** Adobe IMS.
1. Dans la liste déroulante sous Configuration **** Cloud, sélectionnez **Adobe Target**.
1. Activer **Créez un certificat** et saisissez un nouvel alias.
1. Confirmez avec **Créer un certificat**.

   ![](assets/integrate-target-io-01.png)

1. Sélectionnez **Télécharger** (ou **Télécharger la clé** publique) pour télécharger le fichier sur votre lecteur local afin qu’il soit prêt à être utilisé lors de la [configuration de l’intégration Adobe E/S pour Adobe Target avec AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Gardez cette configuration ouverte, elle sera nécessaire à nouveau lors de l’ [achèvement de la configuration IMS dans AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuration des E/S Adobe pour l’intégration d’Adobe Target avec AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Vous devez créer l’intégration des E/S Adobe avec Adobe Target qu’AEM utilisera, puis attribuer les privilèges requis.

### Création de l’intégration {#creating-the-integration}

Ouvrez la console d’E/S Adobe pour créer une intégration E/S avec Adobe Target qu’AEM utilisera :

>[!NOTE]
>
>Voir aussi les didacticiels [Adobe E/S](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Ouvrez la console d’E/S Adobe pour les intégrations :

   * [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

1. Sélectionnez **Nouvelle intégration**:

   >[!NOTE]
   >
   >Si vous avez déjà des intégrations existantes, elles seront répertoriées et le bouton **Nouvelle intégration** sera en haut à droite.

   ![](assets/integrate-target-io-03.png)

1. Sélectionnez **Accéder à une API** , puis **Continuer**:

   ![](assets/integrate-target-io-04.png)

1. Sélectionnez **Adobe Target**, puis **Continuer**:

   ![](assets/integrate-target-io-05.png)

1. Ajoutez les détails requis pour la configuration de l’intégration :

   * **Nom**

      Entrez le nom.

   * **Description**

      Une description est facultative.

   * **Certificat de clé publique**

      Téléchargez le fichier de clé publique ; comme généré sous [Configuration d’une configuration IMS - Génération d’une clé](#configuring-an-ims-configuration-generating-a-public-key)publique.

      Une fois chargé, le certificat est répertorié sous **Certificats**.

   * **Profils de produit**

      Les profils de produit sont associés aux espaces de travail dans Target qu’AEM peut utiliser pour l’exportation de contenu et la création d’offres. Par défaut, l’espace de travail par défaut de Target est sélectionné. Sélectionnez d’autres profils/espaces de travail qui doivent être exposés dans AEM en tant que destinations d’exportation.
   Par exemple :

   ![](assets/integrate-target-io-06.png)

1. Confirmez avec l’intégration **Créer**.
1. La création sera confirmée, vous pouvez maintenant **continuer les détails** d’intégration ; elles sont nécessaires pour [terminer la configuration IMS dans AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)

### Attribution de privilèges à l’intégration {#assigning-privileges-to-the-integration}

Vous devez maintenant attribuer les privilèges requis à l’intégration :

1. Ouvrez la console **d’administration Adobe**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Accédez à **Produits** (barre d’outils supérieure), puis sélectionnez **Adobe Target - &lt;*votre-locataire-id*>** (dans le panneau de gauche).
1. Sélectionnez Profils **de** produit, puis l’espace de travail requis dans la liste présentée. Par exemple, Espace de travail par défaut.
1. Sélectionnez **Intégrations**, puis la configuration d’intégration requise.
1. Sélectionnez **Editeur** comme rôle **de** produit ; au lieu de **Observer**.

## Informations stockées pour l’intégration d’E/S Adobe {#details-stored-for-the-adobe-i-o-integration}

La console d’intégration d’E/S d’Adobe affiche la liste de toutes vos intégrations :

* [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

Sélectionnez **Affichage** (à droite d’une entrée d’intégration spécifique) pour afficher d’autres détails sur la configuration. Celles-ci comprennent :

* Présentation
* Statistiques
* Services
* Événements
* JWT (JSON Web Token)

Certaines d’entre elles nécessitent l’intégration des E/S Adobe pour Target dans AEM.

1. **Présentation**:

   ![](assets/integrate-target-io-08.png)

1. **Applications JWT**:

   ![](assets/integrate-target-io-09.png)

## Fin de la configuration IMS dans AEM {#completing-the-ims-configuration-in-aem}

Pour revenir à AEM, vous pouvez terminer la configuration IMS en ajoutant les valeurs requises de l’intégration d’E/S Adobe pour Target :

1. Revenez à la configuration [IMS ouverte dans AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Sélectionnez **Suivant**.

1. Vous pouvez utiliser ici les [détails des E/S](#details-stored-for-the-adobe-i-o-integration)Adobe :

   * **Titre**: Votre texte.
   * **Serveur** d’autorisations : Copiez/collez ceci à partir de la `"aud"` ligne de la section **Charge** ci-dessous, par exemple `"https://ims-na1.adobelogin.com"` dans l’exemple ci-dessous.
   * **Clé** API : Copiez ceci de la section [Aperçu](#details-stored-for-the-adobe-i-o-integration) de l’intégration des E/S Adobe pour Target.
   * **Secret** client : Générez-le dans la section [Aperçu](#details-stored-for-the-adobe-i-o-integration) de l’intégration des E/S Adobe pour Target, puis copiez
   * **Charge utile**: Copiez ceci de la section [JWT](#details-stored-for-the-adobe-i-o-integration) de l’intégration des E/S Adobe pour Target.
   ![](assets/integrate-target-io-10.png)

1. Confirmez avec **Create**.

1. Votre configuration Adobe Target s’affichera dans la console AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmation de la configuration IMS {#confirming-the-ims-configuration}

Pour confirmer que la configuration fonctionne comme prévu :

1. Ouvrez:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`
   Par exemple :

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Sélectionnez votre configuration.
1. Sélectionnez **Vérifier l’intégrité** dans la barre d’outils, puis **Vérifier**.

   ![](assets/integrate-target-io-12.png)

1. En cas de réussite, le message suivant s’affiche :

   ![](assets/integrate-target-io-13.png)

## Configuration du service Adobe Target Cloud {#configuring-the-adobe-target-cloud-service}

La configuration peut désormais être référencée pour un service Cloud afin d’utiliser l’API Target Standard :

1. Open the **Tools** menu. Ensuite, dans la section Services **** Cloud, sélectionnez Services **Cloud** hérités.
1. Faites défiler l’écran jusqu’à **Adobe Target** et sélectionnez **Configurer maintenant**.

   La boîte de dialogue **Créer une configuration** s’ouvre.

1. Entrez un **Titre** et, si vous le souhaitez, un **Nom** (si rien n’est fait, ce sera généré à partir du titre).

   Vous pouvez également sélectionner le modèle requis (si plusieurs modèles sont disponibles).

1. Confirmez avec **Create**.

   La boîte de dialogue **Modifier le composant** s’ouvre.

1. Entrez les détails dans l’onglet Paramètres **d’** Adobe Target :

   * **Code** client : l’ID de client Adobe IMS

      >[!CAUTION]
      >
      >L’ID de client Adobe IMS doit être saisi dans le champ Code client.

   * **Authentification**: IMS
   * **Configuration** IMS : sélectionnez le nom de la configuration IMS
   * **Type** d’API : REPOSE
   * **Configuration d’A4T Analytics Cloud** : sélectionnez la configuration de cloud Analytics utilisée pour les objectifs et les mesures des activités de Target. Vous avez besoin de cette option si vous utilisez Adobe Analytics en tant que source de création de rapports lors du ciblage de contenu. If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Utilisez un ciblage** précis : Cette case à cocher est activée par défaut. Si cette option est sélectionnée, la configuration du service cloud attend le chargement du contexte avant de charger le contenu. Voir la remarque qui suit.
   * **Synchroniser les segments à partir d’Adobe Target**: Sélectionnez cette option pour télécharger les segments définis dans Target afin de les utiliser dans AEM. Vous devez sélectionner cette option lorsque la propriété Type d’API est REST, car les segments incorporés ne sont pas pris en charge, et vous devez toujours utiliser les segments de Target. (Notez que le terme « segment » d’AEM équivaut à « audience » dans Target.)
   * **Bibliothèque** client : Indiquez si vous souhaitez utiliser la bibliothèque cliente AT.js ou mbox.js (obsolète).
   * **Utilisez le système de gestion des balises pour fournir la bibliothèque** client : Utilisez la gestion dynamique des balises (obsolète), Adobe Launch ou tout autre système de gestion des balises.
   * **Personnaliser AT.js**: Laissez ce champ vide si vous avez coché la case Gestion des balises ou pour utiliser le fichier AT.js par défaut. Vous pouvez également télécharger votre fichier AT.js personnalisé.  S’affiche uniquement si vous avez sélectionné AT.js.
   >[!NOTE]
   >
   >[La configuration d’un service Cloud pour utiliser l’API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) Target Classic a été abandonnée (utilise l’onglet Paramètres des recommandations Adobe).

   Par exemple :

   ![](assets/integrate-target-io-14.png)

1. Click **Connect to Target** to initialize the connection with Adobe Target.

   If the connection is successful, the message **Connection successful** is displayed.

1. Sélectionnez **OK** sur le message, puis **OK** dans la boîte de dialogue pour confirmer la configuration.
1. Vous pouvez maintenant [ajouter une structure](/help/sites-administering/target-configuring.md#adding-a-target-framework) Target pour configurer les paramètres ContextHub ou ClientContext qui seront envoyés à Target. Notez que cela n’est peut-être pas nécessaire pour exporter des fragments d’expérience AEM vers Target.

