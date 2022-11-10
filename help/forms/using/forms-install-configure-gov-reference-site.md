---
title: Installer et configurer le site de référence We.Gov et We.Finance
seo-title: Set up and configure We.Gov reference site
description: Installez, configurez et personnalisez un module de démonstration AEM Forms.
seo-description: Install, configure, and customize an AEM Forms demo package.
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
exl-id: 1fee474e-7da5-4ab2-881a-34b8e055aa29
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '4689'
ht-degree: 88%

---

# Installer et configurer le site de référence We.Gov et We.Finance {#set-up-and-configure-we-gov-reference-site}

## Détails du module de démonstration {#demo-package-details}

### Conditions préalables à l’installation {#installation-prerequisites}

Ce module a été créé pour l’**auteur OSGi AEM Forms 6.4**. Il a été testé et est donc pris en charge sur les versions de plateforme suivantes :

| VERSION D’AEM | VERSION DU MODULE AEM FORMS | ÉTAT |
|---|---|---|
| 6.4 | 5.0.86 | **Pris en charge** |
| 6.5 | 6.0.80 | **Pris en charge** |
| 6.5.3 | 6.0.122 | **Pris en charge** |

Ce module contient la configuration cloud qui prend en charge les versions de plateforme suivantes :

| FOURNISSEUR DE CLOUD | VERSION DU SERVICE | ÉTAT |
|---|---|---|
| Adobe Sign | API v5 | **Pris en charge** |
| Microsoft Dynamics 365 | 1710 (9.1.0.3020) | **Pris en charge** |
| Adobe Analytics | API REST v1.4 | **Pris en charge** |
**Considérations relatives à l’installation du module :**

* Le module doit être installé sur un serveur nettoyé, sans autres modules de démonstration ou anciennes versions de modules de démonstration.
* Le module doit être installé sur un serveur OSGi s’exécutant en mode création.

### Que comprend ce module ? {#what-does-this-package-include}

Le [module de démonstration AEM Forms We.Gov](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip) (**we-gov-forms.pkg.all-&lt;version>.zip**) est fourni sous la forme d’un module qui comprend plusieurs autres sous-modules et services. Le module inclut les modules suivants :

* **we-gov-forms.pkg.all-&lt;version>.zip** : *module de démonstration complet*.

   * **we-gov-forms.ui.apps-&lt;version>.zip** : *contient tous les composants, bibliothèques clientes, exemples d’utilisateurs, modèles de workflow, etc.*

      * **we-gov-forms.core-&lt;version>.jar** : *contient tous les services OSGi, l’implémentation par étapes de workflows personnalisés, etc.*

      * **we-gov-forms.derby&lt;version>.jar** : *contient tous les services OSGi, le schéma de base de données, etc.*

      * **core.wcm.components.all-2.0.4.zip** : *collection d’exemples de composants WCM.*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** : *module de disposition Grille AEM Sites pour le contrôle des colonnes des pages Sites.*
   * **we-gov-forms.ui.content-&lt;version>.zip** : *contient l’ensemble du contenu, des pages, des images, des formulaires, des ressources de communication interactive, etc.*

   * **we-gov-forms.ui.analytics-&lt;version>.zip** : *contient toutes les données d’analyse de formulaires We.Gov à stocker dans le référentiel.*

   * **we-gov-forms.config.public-&lt;version>.zip** : *contient tous les nœuds de configuration par défaut, y compris les configurations cloud d’espace réservé, pour éviter les problèmes de modèle de données de formulaire et de liaison de service.*


Les ressources incluses dans ce module sont les suivantes :

* Pages de site AEM avec modèles modifiables
* Formulaires adaptatifs AEM Forms
* Communications interactives AEM Forms (canal d’impression et web)
* Document d’enregistrement XDP AEM Forms
* Modèle de données de formulaire MS Dynamics AEM Forms
* Intégration d’Adobe Sign
* Modèle de workflow AEM
* Exemples d’images AEM Assets
* Exemple de base de données Apache Derby (en mémoire)
* Source de données Apache Derby (à utiliser avec le modèle de données de formulaire)

## Installation du module de démonstration {#demo-package-installation}

Cette section contient des informations sur l’installation du module de démonstration.

### À partir de la distribution logicielle {#from-software-distribution}

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Formulaires]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Appuyez sur le nom du module **we-gov-forms.pkg.all-&lt;version>.zip**, sélectionnez **[!UICONTROL Accepter les termes du contrat de licence utilisateur final]**, puis appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le module et cliquez sur **[!UICONTROL Installer]**.

   ![module de formulaires we gov](assets/wegov_forms_package.jpg)

1. Attendez la fin du processus d’installation.
1. Accédez à *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* pour vérifier que l’installation a réussi.

### À partir d’un fichier ZIP local {#from-a-local-zip-file}

1. Téléchargez et recherchez le fichier **we-gov-forms.pkg.all-&lt;version>.zip**.
1. Accédez à *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*.
1. Sélectionnez l’option &quot;Télécharger le package&quot;.

   ![Option de chargement de module](assets/upload_package.jpg)

1. Utilisez l’explorateur de fichiers pour accéder au fichier ZIP téléchargé et sélectionnez-le.
1. Cliquez sur &quot;Ouvrir&quot; pour charger.
1. Une fois le téléchargement effectué, sélectionnez l’option &quot;Installer&quot; pour installer le package.

   ![Installer le package Forms WeGov](assets/wegov_forms_package-1.jpg)

1. Attendez la fin du processus d’installation.
1. Accédez à *https://&lt;serveur_aem>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* pour vérifier que l’installation a réussi.

### Installer une nouvelle version de package {#installing-new-package-versions}

Pour installer une nouvelle version de package, suivez les étapes définies aux points 4.1 et 4.2. Il est possible d’installer une version de package plus récente alors qu’un autre package plus ancien est installé. Il est toutefois recommandé de commencer par désinstaller l’ancienne version de package. Pour ce faire, procédez comme suit.

1. Accédez à *https://&lt;serveur_aem>:&lt;port>/crx/packmgr/index.jsp*.
1. Recherchez l’ancien fichier **we-gov-forms.pkg.all-&lt;version>.zip**.
1. Sélectionnez l’option &quot;Plus&quot;.
1. Dans la liste déroulante, sélectionnez l’option &quot;Désinstaller&quot;.

   ![Désinstaller le package WeGov](assets/uninstall_wegov_forms_package.jpg)

1. Sur confirmation, sélectionnez à nouveau &quot;Désinstaller&quot; et autorisez le processus de désinstallation à se terminer.

## Configuration du package de démonstration {#demo-package-configuration}

Cette section contient des informations détaillées et des instructions sur la configuration après le déploiement du package de démonstration avant présentation.

### Configuration de l’utilisateur fictif {#fictional-user-configuration}

1. Accédez à *https://&lt;serveur_aem>:&lt;port>/libs/granite/security/content/groupadmin.html*.
1. Connectez-vous en tant qu’administrateur pour effectuer les tâches ci-dessous.
1. Faites défiler la page jusqu’à la fin pour charger tous les groupes d’utilisateurs.
1. Recherchez &quot;**workflow**&quot;.
1. Sélectionnez le **workflow-users**&quot; et cliquez sur &quot;Propriétés&quot;.
1. Accédez à l’onglet &quot;Membres&quot;.
1. Saisissez **wegov** dans le champ &quot;Select User or Group&quot;.
1. Sélectionnez dans la liste déroulante &quot;**Utilisateurs de Forms We.Gov**&quot;.

   ![Modifier les paramètres de groupe pour les utilisateurs du workflow](assets/edit_group_settings.jpg)

1. Cliquez sur &quot;Enregistrer et fermer&quot; dans la barre de menus.
1. Répétez les étapes 2 à 7 en recherchant &quot;**analytics**&quot;, en sélectionnant le **Administrateurs d’Analytics**&quot;, puis en ajoutant le **Utilisateurs de Forms We.Gov**&quot; en tant que membre.
1. Répétez les étapes 2 à 7 en recherchant &quot;**utilisateurs de formulaires**&quot;, en sélectionnant le **forms-power-users**&quot;, puis en ajoutant le **Utilisateurs de Forms We.Gov**&quot; en tant que membre.
1. Répétez les étapes 2 à 7 en recherchant &quot;**forms-users**&quot;, en sélectionnant le **forms-users**&quot;, et cette fois, ajouter le &quot;**Utilisateurs de We.Gov**&quot; en tant que membre.

### Configuration du serveur d’e-mail {#email-server-configuration}

1. Consulter la documentation sur la configuration [Configurer la notification par e-mail](/help/sites-administering/notification.md)
1. Connectez-vous en tant qu’administrateur pour effectuer cette tâche.
1. Accédez à *https://&lt;serveur_aem>:&lt;port>/system/console/configMgr*.
1. Recherchez le service **Day CQ Mail Service**, puis cliquez dessus pour le configurer.

   ![Configuration du service de messagerie Day CQ](assets/day_cq_mail_service.jpg)

1. Configurez le service pour qu’il se connecte au serveur SMTP de votre choix :

   1. **Nom d’hôte du serveur SMTP** : par exemple (smtp.gmail.com)
   1. **Port du serveur** : par exemple (465) pour gmail utilisant SSL
   1. **Utilisateur SMTP** : demo@ &lt;nom_entreprise> .com
   1. **Adresse &quot;De&quot;**: aemformsdemo@adobe.com

   ![Configurer SMTP](assets/configure_smtp.jpg)

1. Cliquez sur &quot;Enregistrer&quot; pour enregistrer la configuration.

### (Facultatif) Configuration de SSL pour AEM {#aemsslconfig}

Cette section contient des informations détaillées sur la configuration du protocole SSL sur l’instance AEM afin de pouvoir définir la configuration d’Adobe Sign Cloud.

**Références:**

1. [SSL par défaut](/help/sites-administering/ssl-by-default.md)

**Remarques:**

1. Accédez à https://&lt;serveur_aem>:&lt;port>/aem/inbox pour terminer le processus expliqué via le lien de documentation de référence ci-dessus.
1. Le package `we-gov-forms.pkg.all-[version].zip` comprend un exemple de certificat et de clé SSL accessibles en extrayant le dossier `we-gov-forms.pkg.all-[version].zip/ssl` qui fait partie du package.

1. Détails du certificat et de la clé SSL :

   1. émis sur &quot;CN=localhost&quot;
   1. Validité 10 ans
   1. valeur de mot de passe de &quot;password&quot;
1. La clé privée est *localhostprivate.der*.
1. Le certificat est *localhost.crt*.
1. Cliquez sur Suivant.
1. Le nom d’hôte HTTPS doit être défini sur *localhost*.
1. Le port doit être défini sur un port exposé par le système.

### (Facultatif) Configuration cloud d’Adobe Sign {#adobe-sign-cloud-configuration}

Cette section contient des informations détaillées et des instructions sur la configuration cloud d’Adobe Sign.

**Références:**

1. [Incorporation d’Adobe Sign à AEM Forms](adobe-sign-integration-adaptive-forms.md)

#### Configuration cloud {#cloud-configuration}

1. Consultez les conditions préalables. Voir [Configuration de SSL AEM](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig) pour connaître la configuration SSL requise.
1. Accédez à :

   *https://&lt;aemserver>:&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >L’URL utilisée pour accéder au serveur AEM doit correspondre à celle configurée dans l’URI de redirection OAuth d’Adobe Sign afin d’éviter des problèmes de configuration (par exemple : *https://&lt;aemserver>:&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*).

1. Sélectionnez la configuration &quot;We.gov Adobe Sign&quot;.
1. Cliquez sur &quot;Propriétés&quot;.
1. Accédez à l’onglet &quot;Paramètres&quot;.
1. Saisissez l’URL oAuth, par exemple : [https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth).
1. Indiquez l’ID client et le secret client configurés à partir de l’instance Adobe Sign configurée.
1. Cliquez sur &quot;Se connecter à Adobe Sign&quot;.
1. Une fois la connexion établie, cliquez sur &quot;Enregistrer et fermer&quot; pour terminer l’intégration.

### (Facultatif) Configuration cloud de MS Dynamics {#ms-dynamics-cloud-configuration}

Cette section contient des détails et des instructions sur la configuration cloud de MS Dynamics.

**Références:**

1. [Configuration du service OData de Microsoft Dynamics](https://experienceleague.adobe.com/docs/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [Configurer Microsoft Dynamics pour AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/using-ms-dynamics-with-aem-forms.html?lang=fr)

#### Service cloud OData de MS Dynamics {#ms-dynamics-odata-cloud-service}

1. Accédez à :

   https://&lt;aemserver>:&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. Assurez-vous d’accéder au serveur à l’aide de la même URL de redirection que celle configurée dans l’enregistrement de l’application MS Dynamics.

1. Sélectionnez la configuration &quot;Microsoft Dynamics OData Cloud Service&quot;.
1. Cliquez sur &quot;Propriétés&quot;.

   ![Propriétés du service cloud OData de Microsoft](assets/properties_odata_cloud_service.jpg)

1. Accédez à l’onglet &quot;Paramètres d’authentification&quot;.
1. Saisissez les informations suivantes :

   1. **Racine du service :** par exemple `https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`
   1. **Type d’authentification :** OAuth 2.0
   1. **Paramètres d’authentification** (voir [Paramètres de configuration cloud de MS Dynamics](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) pour collecter ces informations) :

      1. ID client (également appelé ID d’application)
      1. Secret client
      1. URL OAuth (par exemple [https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize))
      1. Actualiser l’URL du jeton (par exemple [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token))
      1. URL du jeton d’accès (par exemple, [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token))
      1. Portée de l’autorisation (**openid**)
      1. En-tête d’authentification (**porteur d’autorisation**)
      1. Ressource (par exemple `https://msdynamicsserver.api.crm3.dynamics.com`)
   1. Cliquez sur &quot;Se connecter à OAuth&quot;.


1. Après une authentification réussie, cliquez sur &quot;Enregistrer et fermer&quot; pour terminer l’intégration.

#### Paramètres de configuration de MS Dynamics Cloud {#dynamicsconfig}

Les étapes détaillées dans cette section vous permettent de localiser l’ID client, le secret client et les détails de votre instance MS Dynamics Cloud.

1. Accédez à [https://portal.azure.com/](https://portal.azure.com/) et connectez-vous.
1. Dans le menu de gauche, sélectionnez &quot;Tous les services&quot;.
1. Recherchez ou accédez à &quot;Enregistrement de l’application&quot;.
1. Créez ou sélectionnez un enregistrement d’application existant.
1. Copiez l’**ID de l’application** à utiliser comme **ID client** OAuth dans la configuration cloud d’AEM.
1. Cliquez sur &quot;Paramètres&quot; ou &quot;manifeste&quot; pour configurer la variable **URL de réponse.**

   1. Cette URL doit correspondre à l’URL utilisée pour accéder à votre serveur AEM lors de la configuration du service OData.

1. Dans la vue Paramètre, cliquez sur &quot;Clés&quot; pour afficher la création d’une clé (celle-ci est utilisée comme secret client dans AEM ).

   1. Veillez à conserver une copie de la clé, car vous ne pourrez pas la visualiser ultérieurement dans Azure ou AEM.

1. Pour localiser l’URL de ressource/l’URL racine du service, accédez au tableau de bord de l’instance MS Dynamics.
1. Dans la barre de navigation supérieure, cliquez sur &quot;Ventes&quot; ou sur votre propre type d’instance et &quot;Sélectionner les paramètres&quot;.
1. Cliquez sur &quot;Personnalisations&quot; et &quot;Ressources pour les développeurs&quot; en bas à droite.
1. Vous y trouverez l’URL racine du service : e.g

   *`https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`

1. Vous trouverez des informations détaillées sur l’URL du jeton d’accès et d’actualisation à l’adresse suivante :

   *[https://docs.microsoft.com/fr-fr/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/fr-fr/rest/api/datacatalog/authenticate-a-client-app)*

#### Tester le modèle de données de formulaire (Dynamics) {#testing-the-form-data-model}

Une fois la configuration du cloud terminée, vous pouvez tester le modèle de données de formulaire.

1. Accédez à

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. Sélectionnez &quot;We.gov Microsoft Dynamics CRM FDM&quot; et sélectionnez &quot;Propriétés&quot;.

   ![Propriétés de Dynamics CRM FDM](assets/properties_dynamics_crm.jpg)

1. Accédez à l’onglet &quot;Mettre à jour la source&quot;.
1. Assurez-vous que la &quot;configuration contextuelle&quot; est définie sur &quot;/conf/we-gov&quot; et que la source de données configurée est &quot;ms-dynamics-odata-cloud-service&quot;.

   ![Source de données configurée](assets/configured_data_source.jpg)

1. Modifiez le modèle de données de formulaire.

1. Testez les services pour vérifier qu’ils se connectent à la source de données configurée.

   >[!NOTE]
   Une fois les services testés, cliquez sur **Annuler** pour vous assurer que les modifications involontaires ne sont pas propagées au modèle de données de formulaire.

   >[!NOTE]
   Un redémarrage du serveur AEM est nécessaire pour que la source de données soit correctement liée à FDM.

#### Tester le modèle de données de formulaire (Derby) {#test-fdm-derby}

Une fois la configuration du cloud terminée, vous pouvez tester le modèle de données de formulaire.

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. Sélectionnez **Demande d’inscription We.Gov FDM**, puis cliquez sur **Propriétés**.

   ![Propriétés de Dynamics CRM FDM](assets/aftia-enrollment-fdm.jpg)

1. Accédez à l’onglet **Mettre à jour la source**.

1. Assurez-vous que la **Configuration basée sur le contexte** est définie sur `/conf/we-gov` et que la source de données configurée est **We.Gov Derby DS**.

   ![Propriétés de Dynamics CRM FDM](assets/aftia-update-data-source.jpg)

1. Cliquez sur **Enregistrer et fermer**.

1. [Tester les services](work-with-form-data-model.md#test-data-model-objects-and-services) pour vérifier qu’ils se connectent bien à la source de données configurée

   * Pour tester la connexion, sélectionnez l’option **Compte prêt hypothécaire** et appliquez-lui un service « get ». Testez le service afin que les administrateurs système puissent voir les données récupérées.

### Configurer Adobe Analytics (facultatif) {#adobe-analytics-configuration}

Cette section contient des informations détaillées et des instructions sur la configuration dʼAdobe Analytics Cloud.

**Références:**

* [Intégration à Adobe Analytics](../../sites-administering/adobeanalytics.md)

* [Connexion à Adobe Analytics et création de structures](../../sites-administering/adobeanalytics-connect.md)

* [Affichage des données d’analyse de page](../../sites-authoring/pa-using.md)

* [Configuration des analyses et des rapports](configure-analytics-forms-documents.md)

* [Consultation et compréhension des rapports d’analyse d’AEM Forms](view-understand-aem-forms-analytics-reports.md)

### Configuration du service cloud Adobe Analytics {#adobe-analytics-cloud-service-configuration}

Ce package est préconfiguré pour se connecter à Adobe Analytics. Les étapes ci-dessous sont fournies pour permettre la mise à jour de cette configuration.

1. Accédez à *https://&lt;aemserver>:&lt;port>/libs/cq/core/content/tools/cloudservices.html*
1. Recherchez la section Adobe Analytics et cliquez sur le lien &quot;Afficher les configurations&quot;.
1. Sélectionnez la configuration &quot;We.Gov Adobe Analytics (configuration Analytics)&quot;.

   ![Configuration du service cloud Analytics](assets/analytics_config.jpg)

1. Cliquez sur le bouton &quot;Modifier&quot; pour mettre à jour la configuration Adobe Analytics (vous devrez fournir le secret partagé). Cliquez sur &quot;Se connecter à Analytics&quot; pour vous connecter et sur &quot;OK&quot; pour terminer.

   ![We.Gov Adobe Analytics](assets/wegov_adobe_analytics.jpg)

1. Sur la même page, cliquez sur &quot;We.Gov Adobe Analytics Framework (Analytics Framework)&quot; si vous souhaitez mettre à jour les configurations de structure (voir [Activation de la création AEM](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) pour activer la création).

#### Localisation d’informations d’identification utilisateur Adobe Analytics {#analytics-locating-user-credentials}

Pour localiser les informations d’identification utilisateur d’un compte Adobe Analytics, l’administrateur de compte doit effectuer les tâches suivantes.

1. Accédez au portail Adobe Experience Cloud.
   * Se connecter avec des informations d’identification d’administrateur
1. Sélectionnez l’icône Adobe Analytics dans le tableau de bord principal.
   ![Accès rapide](assets/aftia-quick-access.jpg)
1. Accédez à l’onglet Admin et sélectionnez l’élément Gestion des utilisateurs (hérité).
   ![Rapports](assets/aftia-reports.jpg)
1. Sélectionnez l’onglet **Utilisateurs**.
   ![Gestion des utilisateurs](assets/aftia-user-management.jpg)
1. Sélectionnez un utilisateur dans la liste des utilisateurs.
1. Faites défiler jusqu’au bas de la page pour afficher les informations d’authentification des utilisateurs.
   ![Gérer l’accès](assets/aftia-admin-user-access.jpg)
1. Le nom d’utilisateur et les informations secrètes partagées s’affichent sur le côté droit de la zone des autorisations.
1. Notez que le nom d’utilisateur aura le signe des deux points dans le nom. Toutes les informations se trouvant à la gauche des deux points constituent le nom d’utilisateur et celles se trouvant à la droite constituent le nom de la société.
   * Voici un exemple : *nom d’utilisateur : nom de la société*

#### Configurer l’authentification des utilisateurs dans Adobe Analytics {#setup-user-authentication}

Les administrateurs peuvent accorder aux utilisateurs des autorisations AEM Analytics en procédant comme suit.

1. Accédez à Adobe Admin Console.

1. Cliquez sur l’instance Analytics exposée à la console d’administration.

   * Elle se trouve sur la page principale de la page d’administration.

1. Sélectionnez Accès administrateur complet dans Analytics.

1. Ajoutez un utilisateur au profil.

   ![Accès administrateur complet dans Analytics](assets/aftia-full-admin-access.jpg)

1. Cliquez sur l’onglet Autorisations une fois que l’ID utilisateur a été mappé dans le profil.

1. Assurez-vous que toutes les autorisations sont mises en correspondance avec le profil.

   ![Modifier les autorisations](assets/aftia-admin-access-edit.jpg)

1. Notez qu’une fois les autorisations mappées, la possibilité pour un utilisateur de se connecter peut prendre quelques heures.

### Rapports Adobe Analytics {#adobe-analytics-reporting}

#### Afficher les rapports sur les sites Adobe Analytics {#view-adobe-analytics-sites-reporting}

>[!NOTE]
Les données AEM Forms Analytics sont disponibles hors ligne ou sans configuration d’Adobe Analytics Cloud si le package `we-gov-forms.ui.analytics-<version>.zip` est installé, mais les données AEM Sites nécessitent une configuration cloud principale.

1. Accédez à *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Sélectionnez &quot;AEM Forms We.Gov Site&quot; pour afficher les pages du site.
1. Sélectionnez l’une des pages du site (par exemple Accueil), puis &quot;Analytics et Recommendations&quot;.

   ![Analysis et Recommendations](assets/analytics_recommendations.jpg)

1. Sur cette page, vous verrez les informations récupérées d’Adobe Analytics qui se rapportent à la page AEM Sites (remarque : par conception, ces informations sont périodiquement actualisées à partir d’Adobe Analytics et ne s’affichent pas en temps réel).

   ![Analyse AEM Sites](assets/sites_analysis.jpg)

1. De retour sur la page vue (accessible à l’étape 3.), vous pouvez également afficher les informations de page vue en modifiant le paramètre d’affichage afin d’afficher les éléments en &quot;mode Liste&quot;.
1. Recherchez le menu déroulant &quot;Affichage&quot; et sélectionnez &quot;Mode Liste&quot;.

   ![Mode Liste](assets/list_view.jpg)

1. Dans le même menu, sélectionnez &quot;Paramètre d’affichage&quot; et sélectionnez les colonnes que vous souhaitez afficher dans la section &quot;Analytics&quot;.

   ![Configurer les colonnes](assets/configure_columns.jpg)

1. Cliquez sur &quot;Mettre à jour&quot; pour rendre les nouvelles colonnes disponibles.

   ![Afficher les nouvelles colonnes](assets/new_columns_display.jpg)

#### Afficher les rapports de formulaires Adobe Analytics {#view-adobe-analytics-forms-reporting}

>[!NOTE]
Les données AEM Forms Analytics sont disponibles hors ligne ou sans configuration Adobe Analytics Cloud si le package `we-gov-forms.ui.analytics-<version>.zip` est installé, mais les données AEM Sites nécessitent une configuration cloud active.

1. Accédez à

   *https://&lt;serveur_AEM>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Sélectionnez le formulaire adaptatif &quot;Demande d’inscription pour les prestations de santé&quot; et sélectionnez l’option &quot;Rapport Analytics&quot;.

   ![Rapport Analytics](assets/analytics_report.jpg)

1. Patientez jusqu’au chargement de la page, puis affichez les données du rapport Analytics.

   ![Afficher les données du rapport Analytics](assets/analytics_report_data.jpg)

### Activation de la configuration des formulaires automatisés Adobe {#automated-forms-enablement}

Pour installer et configurer AEM Forms avec Adobe Forms, les utilisateurs de l’outil de conversion doivent disposer des éléments suivants.

1. Accès à Adobe I/O.

1. Autorisation de créer une intégration avec le service de conversion Adobe Forms.

1. Service Pack le plus récent pour Adobe AEM 6.5 exécuté en tant qu’auteur.

Avant de lire la suite des instructions, consultez le lien suivant :

* [Configurer le service de conversion automatisée de formulaires](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html)

#### Créer une configuration IMS - Partie 1 {#creating-ims-config}

Pour configurer le service afin qu’il communique correctement avec l’outil de conversion de formulaires, les utilisateurs doivent configurer le service Identity Management System (IMS) pour pouvoir s’enregistrer auprès d’Adobe I/O.

1. Accédez à https://&lt;serveur_AEM>:&lt;port> > Cliquez sur Adobe Experience 
Manager en haut à gauche > Outils > Sécurité > Configuration Adobe IMS.

1. Cliquez sur Créer.

1. Exécutez les actions dans l’image ci-dessous.

   ![Configurer le compte technique IMS](assets/aftia-technical-account-configuration.jpg)

1. Veillez à télécharger le certificat.

1. Ne procédez pas à la suite de la configuration. Consultez la section [Créer une intégration dans Adobe I/O](#create-integration-adobeio).

>[!NOTE]
Le certificat créé dans cette section va être servir à créer le service d’intégration dans Adobe I/O. Une fois ceci fait, les utilisateurs peuvent utiliser ces informations depuis Adobe I/O pour terminer la configuration.

#### Créer une intégration dans Adobe I/O {#create-integration-adobeio}

Assurez-vous que vous avez la possibilité de créer une intégration dans votre domaine Adobe sans avoir à contacter votre administrateur système.

1. Accédez à la [console Adobe I/O](https://console.adobe.io/).

1. Cliquez sur Créer une intégration.

1. Sélectionnez Accéder à une API.

1. Assurez-vous que vous vous trouvez dans le bon groupe (liste déroulante en haut à droite).

1. Dans la section Experience Cloud, sélectionnez l’outil de conversion de formulaires.

1. Cliquez sur Continuer.

1. Saisissez le nom et la description de votre intégration.

1. À l’aide de la clé publique de la section 2.1, placez-la dans l’intégration de la clé.

1. Sélectionnez un profil pour votre conversion automatisée de formulaires.

   ![Créer une intégration](assets/aftia-create-new-integration.jpg)

#### Créer la configuration IMS - Partie 2 {#create-ims-config-part-next}

Maintenant que vous avez créé une intégration, vous allez terminer l’installation de la configuration IMS.

1. Cliquez sur votre intégration dans Adobe I/O afin d’exposer les détails de connexion.

1. Accédez à votre configuration IMS dans AEM (Outils > Sécurité > IMS).

1. Cliquez sur Suivant dans l’écran Configuration IMS.

1. Saisissez le serveur d’autorisation (valeur affichée dans la capture d’écran).

1. Saisissez la clé API.

1. Saisissez le secret client (vous devez cliquer sur Exposer dans l’intégration dans Adobe I/O pour qu’il s’affiche).

1. Cliquez sur l’onglet JWT dans Adobe I/O afin d’obtenir la payload JWT et de la coller dans la payload de la configuration IMS.

   ![Configuration IMS de la payload](assets/aftia-payload-ims-config.jpg)

1. Une fois la configuration créée, cliquez sur la configuration IMS et sélectionnez Contrôle de l’intégrité. Les utilisateurs doivent voir le résultat suivant.

   ![Confirmation d’intégrité](assets/aftia-health-confirmation.jpg)

#### Définir la configuration cloud (We.Gov AFC Production) {#configure-cloud-configuration}

Une fois la configuration IMS terminée, nous pouvons passer en revue la configuration cloud dans AEM. Si la configuration n’existe pas, procédez comme suit pour créer la configuration cloud dans AEM :

1. Ouvrez votre navigateur et accédez à l’URL système https://&lt;nom_domaine>:&lt;port_système>.

1. Cliquez sur Adobe Experience Manager dans le coin supérieur gauche de l’écran > Outils > Services cloud > Configuration de la conversion automatisée des formulaires.

1. Sélectionnez le dossier de configuration dans lequel vous souhaitez placer la configuration.

1. Cliquez sur Créer.

1. Saisissez les informations figurant dans la capture d’écran ci-dessous.

   ![Exploitation AFC](assets/aftia-afc-production.jpg)

1. Fournissez un titre et un nom à la configuration.

1. L’URL du service pour le système est définie sur https://aemformsconversion.adobe.io/.

1. URL du modèle */conf-gov/settings/wcm/templates/we-gov-flamingo-template*.

1. URL du thème : */content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. Cliquez sur Suivant.

1. Pour cette configuration, nous avons laissé les deux valeurs de case à cocher vides.

   * Pour en savoir plus à propos de ces options, voir [Configurer le service cloud](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### Configurer le cloud (exploitation AFC We.Finance) {#configure-cloud-configuration-wefinance}

Une fois la configuration IMS terminée, nous pouvons procéder à la création de la configuration cloud dans AEM.

1. Ouvrez votre navigateur et accédez à l’URL système https://&lt;nom_domaine>:&lt;port_système>.

1. Cliquez sur Adobe Experience Manager dans le coin supérieur gauche de l’écran > Outils > Services cloud > Configuration de la conversion automatisée des formulaires.

1. Sélectionnez le dossier de configuration dans lequel vous souhaitez placer la configuration.

1. Cliquez sur Créer.

1. Saisissez les informations figurant dans la capture d’écran ci-dessous.

   ![Exploitation AFC We.Finance](assets/aftia-wefinance-afc-prod.jpg)

1. Fournissez un titre et un nom à la configuration.

1. L’URL du service pour le système est définie sur https://aemformsconversion.adobe.io/

1. URL du modèle : */conf/we-finance/settings/wcm/templates/we-finance-adaptive-form*

1. URL du thème : */content/dam/formsanddocuments-themes/adobe-finance-forms-themes/we-finance-theme*

1. Cliquez sur Suivant.

1. Pour cette configuration, nous avons laissé les deux valeurs de case à cocher vides.

   * Pour en savoir plus à propos de ces options, voir [Configurer le service cloud](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### Tester la conversion de formulaires (demande d’inscription We.Gov) {#test-forms-conversion}

Une fois la configuration définie, les utilisateurs peuvent la tester en chargeant un document PDF.

1. Accédez au système AEM https://&lt;domain_name>:&lt;system_port>.

1. Cliquez sur Forms > Forms > Documents > AEM Forms We.gov Forms > AFC.

1. Sélectionnez le PDF de demande d’inscription We.Gov.

1. Cliquez sur le bouton **Démarrer la conversion automatisée** dans le coin supérieur droit.

1. Les utilisateurs doivent pouvoir voir l’option telle qu’illustrée ci-dessous.

   ![Formulaire adaptatif converti](assets/aftia-converted-adaptive-form.jpg)

1. Une fois le bouton sélectionné, les options suivantes sont présentées aux utilisateurs :

   * Veillez à ce que les utilisateurs sélectionnent la configuration *Exploitation AFC We.Gov*.

   ![Paramètres de conversion](assets/aftia-conversion-settings.jpg)

   ![Paramètres de conversion avancés](assets/aftia-conversion-settings-2.jpg)

1. Sélectionnez Démarrer la conversion une fois que vous avez configuré toutes les options que vous souhaitez utiliser.

1. Au début du processus de conversion, les utilisateurs doivent voir l’écran suivant :

   ![Paramètres de conversion](assets/aftia-conversion-in-progress.jpg)

1. Une fois la conversion terminée, l’écran suivant s’affiche pour les utilisateurs :

   ![Formulaire adaptatif converti](assets/aftia-converted-adaptive-form-2.jpg)

   Cliquez sur le bouton **Sortie** pour afficher le formulaire adaptatif généré.

#### Problèmes connus et remarques {#known-issues-notes}

Le service Automated Forms Conversion comprend quelques [bonnes pratiques, modèles complexes connus](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html) et [problèmes connus](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/known-issues.html). Consultez-les avant de commencer à utiliser le service AEM Forms Automated Forms Conversion.

1. Générez le formulaire avec Générer le ou les formulaires adaptatifs sans liaison de données activée si vous souhaitez lier le formulaire à un FDM après la conversion.

1. Assurez-vous que jcr:read est activé pour toutes les autorisations du dossier de modèles. Autrement, l’utilisateur du service ne pourra pas lire le modèle à partir du référentiel et la conversion échouera.

## Personnalisations des packages de démonstration {#demo-package-customizations}

Cette section comprend des instructions sur la personnalisation de la démonstration.

### Personnalisation des modèles {#templates-customization}

Les modèles modifiables se trouvent à l’emplacement suivant :

*https://&lt;aemserver>:&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

Ces modèles incluent les modèles Site AEM, Formulaire adaptatif et Communications interactives, créés et assemblés avec des composants qui se trouvent à l’adresse :

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### Système de style {#customizetemplates}

Ce site comprend également des bibliothèques clientes, dont l’une importe le Bootstrap 4 ([https://getbootstrap.com/](https://getbootstrap.com/)). Cette bibliothèque cliente est disponible à l’adresse suivante.

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

Les modèles modifiables inclus dans ce package sont également préconfigurés avec des stratégies de modèle/page qui utilisent les classes CSS Bootstrap 4 pour la pagination, le style, etc. Toutes les classes n’ont pas été ajoutées aux stratégies de modèle, mais toute classe prise en charge par le Bootstrap 4 peut être ajoutée aux stratégies. Consultez la page de prise en main pour obtenir la liste des classes disponibles :

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

Les modèles inclus dans ce module prennent également en charge le système de style :

[Système de style](../../sites-authoring/style-system.md)

#### Modèles de logos {#template-logos}

Les ressources DAM du projet incluent également des images et logos We.Gov. Ces ressources sont disponibles à l’adresse suivante :

*https://&lt;aemserver>:&lt;port>/assets.html/content/dam/we-gov*

Lors de la modification des modèles de page et de formulaire, vous pouvez choisir de mettre à jour les logos de la marque en modifiant les composants Navigation et Pied de page. Ces composants offrent une boîte de dialogue de marque et de logo configurable qui peut être utilisée pour mettre à jour les logos :

![Logos des modèles](assets/template_logos.jpg)

Voir Modifier le contenu d’un formulaire pour plus d’informations :

[Modification du contenu de la page](../../sites-authoring/editing-content.md)

### Personnaliser des pages de sites {#sites-pages-customization}

Toutes les pages du site sont disponibles à l’adresse : *https://&lt;aemserver>:&lt;port>/sites.html/content/we-gov*.

Ces pages de site utilisent également le module AEM Grid pour contrôler la mise en page de quelques composants.

#### Système de style {#style-system}

Les pages incluses dans ce module prennent également en charge le système de style :

[Système de style](../../sites-authoring/style-system.md)

Vous pouvez également consulter [Système de style de personnalisation des modèles](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates) pour en savoir plus sur les styles pris en charge.

### Personnaliser les formulaires adaptatifs {#adaptive-forms-customization}

Tous les formulaires adaptatifs sont disponibles à l’adresse suivante :

*https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

Ces formulaires peuvent être personnalisés pour répondre à certains types d’utilisation. Notez que certains champs et la logique d’envoi ne doivent pas être modifiés afin de garantir le bon fonctionnement du formulaire. Cela inclut :

**Demande d’inscription pour les avantages santé :**

* contact_id : champ masqué utilisé pour recevoir l’ID de contact MS Dynamics lors de l’envoi.
* Envoyer : la logique du bouton Envoyer nécessite une personnalisation pour prendre en charge les rappels. La personnalisation est documentée, mais un script volumineux était nécessaire pour envoyer le formulaire lors de l’exécution d’une opération POST et GET à MS Dynamics via le modèle de données Forms.
* Panneau racine : l’événement Initialize permet d’ajouter un bouton MS Dynamics à la boîte de réception AEM de la manière la moins intrusive possible, car tous les composants de l’interface utilisateur Granite de la boîte de réception AEM ne peuvent pas être modifiés.

#### Mise en forme du formulaire adaptatif {#adaptive-form-styling}

Les formulaires adaptatifs peuvent également être stylisés à l’aide de l’éditeur de style ou de l’éditeur de thème :

* [Styles intégrés des composants de formulaire adaptatif](inline-style-adaptive-forms.md)
* [Création et utilisation des thèmes](themes.md)

### Personnalisation des workflows {#workflow-customization}

Le formulaire adaptatif d’inscription est envoyé à un workflow OSGI pour traitement. Ce workflow se trouve à l’adresse *https://&lt;aemserver>:&lt;port>/conf/we-gov/settings/models/we-gov-process.html*.

En raison de certaines limitations, ce workflow contient plusieurs scripts et étapes de processus OSGI personnalisées. Ces étapes de workflow ont été créées sous la forme d’étapes génériques et n’ont pas été créées avec des boîtes de dialogue de configuration. Actuellement, la configuration des étapes du workflow repose sur des arguments de processus.

Tout le code Java de l’étape du workflow est contenu dans le lot **we-gov-forms.core-&lt;version>.jar**.

## Considérations relatives aux démonstrations et problèmes connus {#demo-considerations-and-known-issues}

Cette section contient des informations sur les fonctionnalités de démonstration et les décisions de conception qui peuvent nécessiter des considérations spéciales pendant le processus de démonstration.

### Considérations relatives aux démonstrations {#demo-considerations}

* Conformément à l’AGRS-159, assurez-vous que le nom (prénom, deuxième prénom et nom de famille) du contact utilisé dans le formulaire adaptatif d’inscription est unique.
* Le formulaire adaptatif d’inscription enverra le courrier électronique Adobe Sign à l’adresse électronique spécifiée dans le champ de courrier électronique du formulaire. Cette adresse électronique ne peut pas être la même que celle utilisée pour la configuration cloud d’Adobe Sign.

### Problèmes connus {#known-issues}

* (AGRS-120) Le composant Navigation du site ne prend actuellement pas en charge les pages enfants imbriquées de plus de 2 niveaux.
* (AGRS-159) Le FDM MS Dynamics actuel doit effectuer 2 opérations pour commencer, PUBLIER les données du formulaire adaptatif d’inscription à Dynamics, puis rechercher l’enregistrement de l’utilisateur afin de récupérer l’ID de contact. Dans son état actuel, la récupération de l’ID de contact échoue si plus de deux utilisateurs portant le même nom sont présents dans Dynamics, ce qui n’autorise pas l’envoi du formulaire adaptatif d’inscription.

## Configurer des tests d’accessibilité {#configure-accessibility-testing}

### Activer le module complémentaire Chrome Test d’accessibilité {#enable-chrome-add-on}

Pour effectuer des tests d’accessibilité, vous devez d’abord installer le plug-in Chrome que vous pouvez trouver [ici](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=fr).

Une fois installé, chargez la page que vous souhaitez tester dans le navigateur Chrome. (Remarque : étant donné que l’ouverture de plusieurs onglets peut avoir une incidence sur votre score, il est préférable de n’ouvrir qu’un seul onglet.) Une fois la page chargée
**faites un clic droit** sur la page et sélectionnez l’onglet **Contrôles**. Les développeurs peuvent sélectionner le type de contrôle à effectuer par le plug-in Accessibilité. Une fois toutes les options sélectionnées, l’utilisateur peut cliquer sur le bouton Générer le rapport. Cela génère un document PDF qui indique la note globale d’accessibilité ainsi que ce qui peut être fait pour augmenter la note globale d’accessibilité.

Une fois le rapport exécuté, les utilisateurs peuvent s’attendre à voir les éléments suivants :

![Rapport d’accessibilité](assets/aftia-accessibility.jpg)

Le nombre affiché devant les utilisateurs est la note globale d’accessibilité qu’ils ont acquise. Il existe également une description de la façon dont ce calcul a été effectué en fonction du score.

Si les utilisateurs souhaitent l’exporter, ils peuvent cliquer sur les trois boutons situés à droite de l’écran et choisir parmi les autres options proposées par le plug-in.

![Rapport d’accessibilité](assets/aftia-accessibility-report.jpg)

### Thème Ultramarine {#ultramarine-theme}

Le thème Ultramarine, accessible au public et géré par Adobe, est intégré au
`we-gov-forms.pkg.all-<version>.zip` fichier ZIP installable. Une fois ce package installé à l’aide de CRX.

Gestionnaire de modules, les utilisateurs peuvent accéder au thème Ultramarine dans AEM Forms en accédant à **Forms** > **Thèmes** > **Thèmes de référence** > **accessible à Ultramarine**.

![Thème Ultramarine](assets/aftia-ultramarine-theme.jpg)

## Options de configuration {#configuration-options}

Les utilisateurs peuvent configurer différentes options de service de workflow, notamment :

1. Entrée Microsoft Dynamics
1. Adobe Sign
1. Gestion des communications personnalisées AEM
1. Adobe Analytics

Pour les configurer afin qu’ils soient activés dans le workflow, les utilisateurs doivent effectuer les tâches suivantes.

1. Accédez à https://&#39;[serveur]:[port]&#39;/system/console/configMgr.

1. Recherchez les *configurations WeGov*.

1. Ouvrez la définition de service et activez les services sélectionnés à appeler dans le workflow.

   >[!NOTE]
   Un utilisateur active le service dans la page Configuration Manager. Par conséquent, les utilisateurs doivent toujours configurer un service pour communiquer avec les services externes demandés.

   ![Package WeGov Forms](assets/aftia-configuration-options.jpg)

1. Une fois l’opération terminée, cliquez sur le bouton Enregistrer pour enregistrer les paramètres.

## Étapes suivantes {#next-steps}

Vous êtes maintenant prêt à explorer le site de référence We.Gov. Pour plus d’informations sur les étapes et le workflow du site de référence We.Gov, consultez la section [Présentation du site de référence We.Gov](../../forms/using/forms-gov-reference-site-user-demo.md).
