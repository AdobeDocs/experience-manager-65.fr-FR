---
title: SAP Commerce Cloud
seo-title: Commerce Cloud SAP
description: Découvrez comment déployer l’eCommerce avec SAP Commerce Cloud.
seo-description: Découvrez comment déployer l’eCommerce avec SAP Commerce Cloud.
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 86%

---


# Commerce Cloud SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Cette page contient des liens vers le site web d’Hybris. Pour certaines pages, vous devrez disposer d’un compte pour vous connecter.

## Déploiement du commerce électronique avec le Commerce Cloud SAP {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Les procédures ci-dessous utilisent le catalogue de démonstration suivant pour illustrer le déploiement :
>
>`Geometrixx Outdoors Site English (US)`

Le déploiement des [modules eCommerce nécessaires](#packages-needed-for-ecommerce-with-hybris) met à disposition la fonctionnalité complète de la structure eCommerce avec une implémentation de référence de la fonctionnalité eCommerce fournie avec une implémentation Hybris (dont un catalogue de démonstration).

Il est disponible sous la branche Anglais (États-Unis) ( `/content/geometrixx-outdoors/en_US`) du site Geometrixx Outdoors :

* [Informations sur le produit](#productinformationwithcolorvariants) (avec des variantes de couleur, le cas échéant)

* [Présentations du contenu du panier](#shoppingcartcontentoverview)
* [Inscription du client](#customersignup) et [Connexion du client](#customersignin)

* [Accès à la console de gestion Hybris](#accesstothehybrismanagementconsole)

### Exigences techniques – Serveur Hybris {#technical-requirements-hybris-server}

L&#39;extension hybris du cadre d&#39;intégration du commerce électronique a été mise à jour pour prendre en charge Hybris 5 (par défaut), tout en maintenant une compatibilité ascendante avec [Hybris 4](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Prend en charge les versions 18.11 et ultérieures.
>* Pour exécuter le [serveur Hybris 5](https://www.hybris.com/en/architecture-technology), vous devez disposer de Java 7.
>* Le module complémentaire Hybris, [Telco Accelerator](https://www.hybris.com/en/products/telecommunication), n’est pas pris en charge par l’extension AEM.

>



### Modules nécessaires à eCommerce avec Hybris  {#packages-needed-for-ecommerce-with-hybris}

Pour installer la fonctionnalité eCommerce, vous devez disposer des éléments suivants :

* Votre serveur hybris
* Structure d’AEM eCommerce :

   * fait partie d’une installation AEM standard

* Module AEM Geometrixx-all :

   * `cq-geometrixx-all-pkg`

* Modules de contenu AEM Hybris : 

   * `cq-hybris-content-6.3.2`
   * Implémentation de l’API spécifique à Hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * une implémentation de référence pour illustrer l&#39;utilisation de l&#39;hybris ( `geometrixx-outdoors/en_US`)

### Installation d’eCommerce avec Hybris {#installation-of-ecommerce-with-hybris}

Pour installer une configuration réelle (à l’aide du catalogue de démonstration, Geometrixx Outdoors), la procédure est la suivante :

1. [Installez AEM](/help/sites-deploying/deploy.md).
1. Installez le module Geometrixx-all.

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installez les modules de contenu de démonstration à l’aide du [gestionnaire de modules](/help/sites-administering/package-manager.md) :

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Téléchargez et créez votre serveur Hybris](#download-and-build-your-hybris-server).
1. Créez votre catalogue dans le moteur eCommerce :

   1. [Configurez le magasin de Geometrixx Outdoors](#setup-the-geometrixx-outdoors-store).

1. [Créez](/help/sites-authoring/qg-page-authoring.md) les pages supplémentaires dont vous avez besoin dans AEM.

>[!CAUTION]
>
>L’utilisation du serveur Hybris nécessite une licence Hybris distincte.

>[!NOTE]
>
>Pour les développeurs, la [documentation de l’API](/help/sites-developing/ecommerce.md#api-documentation) est également disponible pour téléchargement.

### Téléchargement et création du serveur Hybris {#download-and-build-your-hybris-server}

Les étapes de cette procédure consistent à télécharger et à créer le serveur Hybris. Elle permet également de créer la configuration initiale nécessaire aux connexions entre Hybris et cq. L’extension pourra ensuite être utilisée avec les paramètres par défaut.

>[!CAUTION]
>
>Les versions d’Hybris antérieures à la version 5.5.1 ne sont pas prises en charge.

>[!NOTE]
>
>À cet effet, [Groovy](https://groovy-lang.org/) devra être installé sur votre système.

1. Téléchargez la distribution **Hybris Commerce Suite** sur le site de téléchargement Hybris.

   >[!CAUTION]
   >
   >Pour y accéder, vous devez disposer d’un compte (disponible auprès de Hybris).

1. Décompressez le fichier de distribution à l’emplacement souhaité (désigné par &lt;répertoire-racine-hybris>).
1. Dans la ligne de commande, exécutez la commande suivante :

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >Lors de l’exécution de :
   >
   >`ant clean all`
   >
   >Appuyez sur `Return` si nécessaire.

1. Téléchargez les fichiers suivants dans le dossier racine de votre distribution d&#39;hybris extraite,

   ```
       <hybris-root-directory>
   ```


   [Obtenir le fichier](assets/setup.groovy)

   >[!NOTE]
   >
   >Pour Hybris 5.6.0 et version ultérieure, utilisez le fichier setup.groovy suivant.

   5.6.0 et version ultérieure

   [Obtenir le fichier](assets/setup-1.groovy)

1. Dans la ligne de commande, exécutez la commande ci-dessous pour :

   * mettre à jour la configuration du serveur Hybris (comme l’exige l’extension) ;
   * régénérer le serveur Hybris avec la configuration modifiée ;
   * démarrer le serveur.

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >En fonction de votre système, plusieurs de ces étapes peuvent prendre plusieurs minutes.

1. Dans votre navigateur, accédez à la **console d’administration Hybris**, à l’adresse :

   [http://localhost:9002](http://localhost:9002)

1. Cliquez sur **Initialiser** (Initialize), puis confirmez l’action d’initialisation (car elle va supprimer les données existantes).

   La progression s’affiche dans la console, et le message `FINISHED`TERMINÉ () indique la fin de l’opération.

   >[!NOTE]
   >
   >En fonction de votre système, cette opération peut prendre plusieurs minutes.

### Configuration du magasin Geometrixx Outdoors  {#setup-the-geometrixx-outdoors-store}

Cette procédure permet de transférer et de configurer le magasin de démonstration : Geometrixx Online.

1. Démarrez l’instance Hybris. Dans la ligne de commande, exécutez la commande suivante :

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Dans le navigateur, accédez à la **console de gestion Hybris**, à l’adresse :

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilisez les informations d’identification suivantes :
   * username : admin
   * password: nimda

1. À partir de la navigation de la barre latérale, développez **Système** (System) et **Outils** (Tools). Ensuite, sélectionnez **Importer** (Import) pour ouvrir la fenêtre **Assistant : Importation d’un fichier CSV** (Wizard: CSV Import).
1. Dans l’onglet **Configuration**, **transférez** le **fichier d’importation** suivant :

   [Obtenir le fichier](assets/geometrixx-outdoors-export.csv)

1. Définissez le **paramètre régional** sur :

   `en_US - English (United States)`

1. Ouvrez l’onglet **Ressources**.
1. **Transférez** le fichier **Media-Zip** suivant :

   [Obtenir le fichier](assets/geometrixx-outdoors-images.zip)

1. Pour importer les fichiers spécifiés, cliquez sur **Démarrer**. L’onglet **Résultat** affiche des entrées de journal.

1. Pour fermer la fenêtre d’importation, cliquez sur **Terminé**.

1. Dans la barre latérale, sélectionnez **Système**, **Outils**, puis **Importer**.

1. **Transférez** le **fichier d’importation** suivant :

   [Obtenir le fichier](assets/base-store.csv)

   Pour Hybris 5.7, utilisez le fichier suivant :

   [Obtenir le fichier](assets/base-store-5_7.csv)

1. Définissez le **paramètre régional** sur :

   `en_US - English (United States)`

1. Pour importer les fichiers spécifiés, cliquez sur **Démarrer**. L’onglet **Résultat** affiche des entrées de journal.

1. Pour fermer la fenêtre d’importation, cliquez sur **Terminé**.

1. À présent, vous pouvez utiliser le cockpit du produit pour afficher les catalogues et les produits importés :

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

