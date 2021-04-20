---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guide de déploiement d’AEM 6.5
breadcrumb-title: Guide de déploiement
user-guide-description: En savoir plus sur l’installation, le déploiement et l’architecture d’Adobe Experience Manager 6.5, y compris sur le déploiement cloud d’Adobe Managed Services.
feature-set: Experience Manager Sites
feature: Deploying
role: Architect
translation-type: tm+mt
source-git-commit: d7b0803385aaa451a1ec7ec280ff51c3e96e36e7
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 93%

---


# AEM 6.5 Déploiement du Guide de l’utilisateur {#deploying}

+ [Guide de l’utilisateur du déploiement](home.md)
+ Présentation de la plateforme AEM {#introduction}
   + [Présentation de la plateforme AEM](platform.md)
   + [Exigences techniques](technical-requirements.md)
   + [Éléments de stockage dans AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM avec MongoDB](aem-with-mongodb.md)
+ Déploiement d’AEM {#deploying}
   + [Déploiement et maintenance](deploy.md)
   + [Déploiements recommandés](recommended-deploys.md)
   + [Installation du serveur d’applications](application-server-install.md)
   + [Installation autonome personnalisée](custom-standalone-install.md)
   + [Début et arrêt d’AEM à partir de la ligne de commande](command-line-start-and-stop.md)
   + [Configuration des magasins de nœuds et des entrepôts de données dans AEM 6](data-store-config.md)
   + [Nettoyage de révision](revision-cleanup.md)
   + [Requêtes et indexation Oak](queries-and-indexing.md)
   + [Exécution d’AEM avec TarMK Cold Standby](tarmk-cold-standby.md)
   + [Prise en charge RDBMS dans AEM 6.5](rdbms-support-in-aem.md)
   + [Indexation par l’intermédiaire du fichier Jar d’Oak-run](indexing-via-the-oak-run-jar.md)
   + [Indexation du fichier Oak-run.jar – Scénarios d’utilisation](oak-run-indexing-usecases.md)
   + [Dépannage des index Oak](troubleshooting-oak-indexes.md)
   + [Souscription à la collecte de statistiques d’utilisation agrégées](opt-in-aggregated-usage-statistics.md)
   + [Résolution des incidents](troubleshooting.md)
+ Configuration d’AEM {#configuring}
   + [Concepts de configuration de base](configuring.md)
   + [Journalisation](configure-logging.md)
   + [Configuration d’OSGi](configuring-osgi.md)
   + [Paramètres de configuration OSGi](osgi-configuration-settings.md)
   + [Modes d’exécution](configure-runmodes.md)
   + [Console web](web-console.md)
   + [Réplication](replication.md)
   + [Réplication à l’aide du SSL mutuel](mssl-replication.md)
   + [Réplication de dépannage](troubleshoot-rep.md)
   + [Expiration des objets statiques](expiration-static-objects.md)
   + [Purge de version](version-purging.md)
   + [Contrôle et maintien de votre instance AEM](monitoring-and-maintaining.md)
   + [Tâches de déchargement](offloading.md)
   + [Connexion unique](single-sign-on.md)
   + [Mappage de ressources](resource-mapping.md)
   + [Activation de HTTP via SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Vérifications transversales et contrôles de cohérence](consistency-check.md)
   + [Instructions de performance](performance-guidelines.md)
   + [Optimisation des performances](configuring-performance.md)
   + [Guide de performances des ressources](assets-performance-sizing.md)
   + [Articles sur la procédure de configuration](ht-deploy.md)
   + [Configuration de la console Web](configuring-web-console.md)
+ Mise à niveau vers AEM 6.5 {#upgrading}
   + [Mise à niveau vers AEM 6.5](upgrade.md)
   + [Planification de la mise à niveau](upgrade-planning.md)
   + [Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs](pattern-detector.md)
   + [Compatibilité descendante dans AEM 6.5](backward-compatibility.md)
   + [Processus de mise à niveau](upgrade-procedure.md)
   + [Réalisation d’une mise à niveau statique](in-place-upgrade.md)
   + [Utilisation de la réindexation hors connexion pour réduire les temps d’inactivité lors d’une mise à niveau](upgrade-offline-reindexing.md)
   + [Migration différée du contenu](lazy-content-migration.md)
   + [Utilisation de l’outil de migration CRX2OAK](using-crx2oak.md)
   + [Tâches de maintenance avant la mise à niveau](pre-upgrade-maintenance-tasks.md)
   + [Vérifications et dépannage après la mise à niveau](post-upgrade-checks-and-troubleshooting.md)
   + [Mise à niveau des formulaires de recherche personnalisée](upgrading-custom-search-forms.md)
   + [Mises à niveau possibles](sustainable-upgrades.md)
   + [Code et personnalisations de la mise à niveau](upgrading-code-and-customizations.md)
   + [Procédure de mise à niveau pour les installations de serveur d’applications](app-server-upgrade.md)
   + [Liste des lots obsolètes désinstallés après la mise à niveau ](obsolete-bundles.md)
+ Restructuration des référentiels {#restructuring}
   + [Restructuration des référentiels dans AEM 6.5](repository-restructuring.md)
   + [Restructuration des référentiels dans AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels dans AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels d’Assets dans AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels Dynamic Media dans AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels de Forms dans AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels e-Commerce dans AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Restructuration des référentiels pour AEM Communities dans la version 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [Aperçu du commerce électronique](ecommerce.md)
   + [SAP Commerce Cloud](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Bonnes pratiques {#practices}
   + [Meilleures pratiques de déploiement](best-practices.md)
   + [Arborescence de la performance](performance-tree.md)
   + [Meilleures pratiques pour le test de la performance](best-practices-for-performance-testing.md)
   + [Bonnes pratiques relatives aux requêtes et à l’indexation](best-practices-for-queries-and-indexing.md)
   + [Recommandations d’interfaces utilisateur aux clients](ui-recommendations.md)
   + [Performance et évolutivité](performance.md)
