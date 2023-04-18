---
title: Déploiement d’eCommerce avec le Commerce Cloud SAP
description: Découvrez comment déployer eCommerce avec le Commerce Cloud SAP.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 58%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>Cette page contient des liens vers le site web d’Hybris. Pour certaines pages, vous aurez besoin d’un compte pour vous connecter.

## Déploiement d’eCommerce avec SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Les procédures ci-dessous utilisent le catalogue de démonstration suivant pour illustrer le déploiement :
>
>`Geometrixx Outdoors Site English (US)`

Le déploiement des [packages eCommerce nécessaires](#packages-needed-for-ecommerce-with-hybris) met à disposition la fonctionnalité complète de la structure eCommerce avec une implémentation de référence de la fonctionnalité eCommerce fournie avec une implémentation Hybris (dont un catalogue de démonstration).

Cette option est disponible dans la partie en anglais (US) (`/content/geometrixx-outdoors/en_US`) du site de Geometrixx Outdoors :

* [Informations sur le produit](#productinformationwithcolorvariants) (avec les variantes de couleur, le cas échéant)

* [Présentations du contenu du panier](#shoppingcartcontentoverview)
* [Inscription du client](#customersignup) et [Connexion du client](#customersignin)

* [Accès à la console de gestion Hybris](#accesstothehybrismanagementconsole)

### Exigences techniques – Serveur Hybris {#technical-requirements-hybris-server}

L’extension Hybris d’eCommerce Integration Framework a été mise à jour afin de prendre en charge Hybris 5 (par défaut), tout en conservant une rétrocompatibilité avec [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Prend en charge les versions 18.11 et ultérieures.
>* Pour exécuter le [serveur Hybris 5](https://www.hybris.com/en/architecture-technology), vous devez disposer de Java 7.
>* Le module complémentaire Hybris, la [Telco Accelerator](https://www.hybris.com/en/products/telecommunication), n’est pas pris en charge par l’extension AEM.
>


### Modules nécessaires au commerce électronique avec hybris {#packages-needed-for-ecommerce-with-hybris}

Pour installer la fonctionnalité eCommerce, vous avez besoin des éléments suivants :

* Votre serveur Hybris
* Le framework d’AEM eCommerce :

   * fait partie d’une installation d’AEM standard

* AEM package Geometrixx-all :

   * `cq-geometrixx-all-pkg`

* Packages de contenu AEM Hybris : 

   * `cq-hybris-content-6.3.2`
   * Implémentation de l’API spécifique à Hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * Implémentation de référence permettant d’illustrer l’utilisation d’Hybris (`geometrixx-outdoors/en_US`)

### Installation d’eCommerce avec Hybris {#installation-of-ecommerce-with-hybris}

Pour installer une configuration complète (à l’aide du catalogue de démonstration, les Geometrixx Outdoors), les étapes de base sont les suivantes :

1. [Installez AEM](/help/sites-deploying/deploy.md).
1. Installer le package Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Installez les packages de contenu de démonstration à l’aide du [gestionnaire de packages](/help/sites-administering/package-manager.md) :

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Téléchargez et créez votre serveur Hybris.](#download-and-build-your-hybris-server).
1. Créez votre catalogue dans votre moteur eCommerce :

   1. [Configuration de la boutique en ligne Geometrixx](#setup-the-geometrixx-outdoors-store).

1. [Auteur](/help/sites-authoring/qg-page-authoring.md) toutes les pages supplémentaires dont vous avez besoin dans AEM.

>[!CAUTION]
>
>L’utilisation du serveur Hybris nécessite une licence Hybris distincte.

>[!NOTE]
>
>Pour l’équipe de développement, la [documentation de l’API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) est également disponible pour téléchargement.

### Téléchargement et création de votre serveur Hybris {#download-and-build-your-hybris-server}

Les étapes de cette procédure téléchargent et créent le serveur Hybris. Il effectue également les configurations initiales requises pour les connexions entre hybris et cq. L’extension sera alors utilisable avec les paramètres par défaut.

>[!CAUTION]
>
>Les versions d’hybris antérieures à la version 5.5.1 ne sont pas prises en charge.

>[!NOTE]
>
>À cet effet, [Groovy](https://groovy-lang.org/) devra être installé sur votre système.

1. Téléchargez la distribution **Hybris Commerce Suite** sur le site de téléchargement Hybris.

   >[!CAUTION]
   >
   >Pour y accéder, vous aurez besoin d’un compte (Hybris).

1. Décompressez le fichier de distribution à l’emplacement requis (appelé &lt;hybris-root-directory>).
1. Sur la ligne de commande, exécutez les opérations suivantes :

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >Lors de l’exécution :
   >
   >`ant clean all`
   >
   >Appuyez sur `Return` si nécessaire.

1. Téléchargez les fichiers ci-dessous dans le dossier racine de la distribution Hybris extraite,

   ```
       <hybris-root-directory>
   ```


[Obtenir le fichier](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Pour Hybris 5.6.0 et version ultérieure, utilisez le fichier setup.groovy suivant.

   5.6.0 et versions ultérieures

[Obtenir le fichier](/help/sites-deploying/assets/setup-1.groovy)

1. Dans la ligne de commande, exécutez la commande ci-dessous pour :

   * mettre à jour la configuration du serveur Hybris (comme l’exige l’extension) ;
   * régénérer le serveur Hybris avec la configuration modifiée ;
   * Démarrez le serveur

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >En fonction de votre système, plusieurs de ces étapes peuvent prendre plusieurs minutes.

1. Dans votre navigateur, accédez au **console d’administration Hybris** at :

   [http://localhost:9002](http://localhost:9002)

1. Cliquez sur **Initialiser**, puis confirmez l’action d’initialisation (car elle va supprimer les données existantes).

   La progression s’affiche dans la console, et le message `FINISHED`indique la fin de l’opération.

   >[!NOTE]
   >
   >En fonction de votre système, cette opération peut prendre plusieurs minutes.

### Configuration de la boutique de Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Cette procédure permet de charger et de configurer le magasin de démonstration : Geometrixx Online.

1. Démarrez votre instance Hybris. Sur la ligne de commande, exécutez les opérations suivantes :

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Dans votre navigateur, accédez au **console de gestion Hybris** at :

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilisez les informations d’identification suivantes :
   * Nom d’utilisateur : admin
   * Mot de passe : nimda

1. À partir de la navigation de la barre latérale, développez **Système** et **Outils**. Sélectionnez **Importer** pour ouvrir le **Assistant : Importation CSV** fenêtre.
1. Dans le **Configuration** onglet, **Télécharger** les éléments suivants **Importer un fichier**:

[Obtenir le fichier](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Définissez le **paramètre régional** sur :

   `en_US - English (United States)`

1. Ouvrez le **Ressources** .
1. **Télécharger** les éléments suivants **Media-Zip**:

[Obtenir le fichier](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Pour importer les fichiers spécifiés, cliquez sur **Démarrer**. L’onglet **Résultat** affiche des entrées de journal.

1. Pour fermer la fenêtre d’importation, cliquez sur **Terminé**.

1. Dans la barre latérale, sélectionnez **Système**, **Outils**, puis **Importer**.

1. **Transférez** le **fichier d’importation** suivant :

[Obtenir le fichier](/help/sites-deploying/assets/base-store.csv)

   Pour Hybris 5.7, utilisez le fichier suivant :

[Obtenir le fichier](/help/sites-deploying/assets/base-store-5_7.csv)

1. Définissez le **paramètre régional** sur :

   `en_US - English (United States)`

1. Pour importer les fichiers spécifiés, cliquez sur **Démarrer**. L’onglet **Résultat** affiche des entrées de journal.

1. Pour fermer la fenêtre d’importation, cliquez sur **Terminé**.

1. À présent, vous pouvez utiliser le cockpit du produit pour afficher les catalogues et les produits importés :

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
