---
title: Activer AEM pour rechercher des documents PDF et Microsoft Office protégés par la sécurité des documents
description: Découvrez comment activer la recherche AEM native pour effectuer une recherche de texte intégral sur des documents PDF protégés par DRM.
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '673'
ht-degree: 100%

---

# Activer AEM pour rechercher des documents PDF protégés par la sécurité documentaire et des documents Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager fournit une interface utilisateur pour rechercher et localiser diverses ressources stockées dans AEM. La recherche native est capable de rechercher et de localiser des ressources AEM et d’effectuer une recherche de texte dans divers formats de document couramment utilisés tels que les fichiers en texte brut, les documents Microsoft Office et les documents PDF. Vous pouvez également étendre la recherche native de sorte à ce qu’elle effectue une recherche de texte intégral dans des documents PDF protégés DRM et des documents Microsoft Office.

Effectuez les étapes suivantes pour permettre à AEM d’effectuer des recherches dans des documents PDF et Microsoft Office protégés par Document Security :

## Avant de commencer {#before-you-start}

* Installez et configurez AEM Forms Document Security.
* Ajoutez le package sun.util.calendar à la liste blanche de la **Configuration du pare-feu de désérialisation.** La configuration est répertoriée à l’adresse `https://'[server]:[port]'/system/console/configMgr`.
* Vérifiez que tous les bundles AEM sont en cours d’utilisation. Les lots sont répertoriés à l’adresse `https://'[server]:[port]'/system/console/bundles`. Si tous les lots ne sont pas actifs, patientez, puis vérifiez leur statut après quelques minutes.

## Établir une connexion sécurisée dans le workflow AEM Forms (AEM Forms on JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Une connexion sécurisée permet un flux d’informations harmonieux entre AEM Forms on JEE et les services OSGi s’exécutant sur le même serveur. Utilisez l’une des méthodes suivantes pour établir une connexion sécurisée :

* Configurer le bundle de SDK client AEM Forms avec les informations d’identification d’administrateur d’AEM Forms on JEE
* Configurer le bundle de SDK client AEM Forms à l’aide de l’authentification mutuelle

### Configurer le bundle de SDK client AEM Forms avec les informations d’identification d’administrateur d’AEM Forms on JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Ouvrez le gestionnaire de configuration AEM et connectez-vous en tant qu’administrateur ou administratrice. L’URL par défaut est https://&lt;Nomserveur>:&lt;port>/lc/system/console/configMgr.
1. Recherchez et ouvrez le bundle SDK client AEM Forms. Spécifiez la valeur des propriétés suivantes :

   * **URL du serveur :** spécifiez l’URL HTTP d’AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur AEM Forms sur JEE avec le paramètre -Djavax.net.ssl.trustStore=&lt;chemin dʼaccès du fichier de stockage de clés AEM Forms sur JEE>.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.
   * **Nom d’utilisateur :** indiquez le nom d’utilisateur du compte AEM Forms on JEE à utiliser pour lancer des appels à partir du serveur AEM Forms on JEE. Le compte spécifié doit disposer des autorisations nécessaires pour appeler Document Services sur le serveur AEM Forms on JEE.
   * **Mot de passe** : indiquez le mot de passe du compte AEM Forms on JEE mentionné dans le champ Nom d’utilisateur.

   Cliquez sur **Enregistrer**. AEM est activé pour effectuer des recherches dans des documents PDF et Microsoft Office protégés par Document Security.

### Configurer le bundle de SDK client AEM Forms à l’aide de l’authentification mutuelle {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Activez l’authentification mutuelle pour AEM Forms on JEE. Pour plus d’informations, voir [CAC et authentification mutuelle](https://helpx.adobe.com/fr/livecycle/kb/cac-mutual-authentication.html).
1. Ouvrez le gestionnaire de configuration AEM et connectez-vous en tant qu’administrateur ou administratrice. L’URL par défaut est https://&lt;Nomserveur>:&lt;port>/lc/system/console/configMgr.
1. Recherchez et ouvrez le bundle SDK client AEM Forms. Spécifiez la valeur des propriétés suivantes :

   * **URL du serveur** : spécifiez l’URL HTTPS d’AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur AEM Forms sur JEE avec le paramètre -Djavax.net.ssl.trustStore=&lt;chemin dʼaccès du fichier de stockage de clés AEM Forms sur JEE>.
   * **Activer SSL bidirectionnel** : activez l’option Activer SSL bidirectionnel.
   * **URL du fichier KeyStore** : indiquez l’URL du fichier de stockage de clés.
   * **URL du fichier TrustStore** : indiquez l’URL du fichier de magasin approuvé.
   * **Mot de passe du KeyStore** : indiquez le mot de passe du fichier de stockage des clés.
   * **Mot de passe TrustStore** : indiquez le mot de passe du fichier de magasin approuvé.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.

   Cliquez sur **Enregistrer**. AEM est activé pour effectuer des recherches dans des documents PDF et Microsoft Office protégés par Document Security.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

## Indexer un exemple de document PDF ou Microsoft Office protégé par une politique {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Connectez-vous à AEM Assets en tant qu’administrateur.
1. Créez un dossier dans le gestionnaire de ressources numériques AEM et téléchargez un document PDF ou Microsoft Office protégé par une politique vers le dossier que vous venez de créer. Désormais, vous pouvez rechercher le contenu des documents protégés par une politique à l’aide de la recherche AEM. Il doit renvoyer le document contenant le texte recherché.
