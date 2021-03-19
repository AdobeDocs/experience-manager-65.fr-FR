---
title: Activer AEM pour rechercher des documents PDF protégés par la sécurité documentaire
seo-title: Activer AEM pour rechercher des documents PDF protégés par la sécurité documentaire
description: 'Découvrez comment permettre à la recherche AEM native d’effectuer une recherche de texte intégral sur des documents PDF protégés par DRM.  '
seo-description: 'Découvrez comment permettre à la recherche AEM native d’effectuer une recherche de texte intégral sur des documents PDF protégés par DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 86%

---


# Activer AEM pour rechercher des documents PDF protégés par la sécurité documentaire{#enable-aem-to-search-document-security-protected-pdf-documents}

La recherche AEM peut rechercher et localiser des ressources AEM et effectuer une recherche de texte dans les formats de document couramment utilisés tels que les fichiers texte brut, les documents Microsoft Office et les fichiers PDF. Vous pouvez également étendre la recherche native pour effectuer une recherche en texte intégral sur les [documents PDF protégés par la sécurité documentaire AEM](../../forms/using/admin-help/document-security.md). Pour permettre à AEM d’effectuer une recherche en texte intégral sur ces documents, procédez comme suit :

1. Créez une connexion sécurisée
1. Indexer un document PDF protégé par un exemple de stratégie

## Conditions préalables {#prerequisites}

* Si vous utilisez AEM Forms sur OSGi :

   * Installez le [package de l’indexeur de Document Security AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) sur le serveur AEM Forms.

   * Vérifiez qu’un serveur AEM Forms on JEE est opérationnel et que la sécurité des documents est installée sur le serveur AEM Forms on JEE approprié. Le serveur AEM Forms on JEE est nécessaire pour indexer le document protégé.

* Si vous utilisez uniquement un serveur AEM Forms on JEE, le package de l’indexeur est déjà installé.
* Vérifiez que tous les lots sont en cours d’utilisation. Si tous les bundles ne sont pas actifs, attendez qu’ils soient tous opérationnels.

   * Pour AEM Forms sur OSGi, les lots sont répertoriés à l’adresse https://&#39;[server]:[port]&#39;/system/console/bundles.
   * Pour AEM Forms on JEE, les lots sont répertoriés à l’adresse https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Par exemple, https://localhost:8080/lc/system/console/bundles.

* Ajoutez le package *sun.util.calendar* à la liste autorisée. Pour ajouter le package à la liste autorisée, procédez comme suit :

   1. Ouvrez la console web AEM. L’URL est https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Recherchez et ouvrez **la configuration du pare-feu de désérialisation.**

   1. Ajoutez le package sun.util.calendar dans le champ des classes Placées sur la liste autorisée ou des préfixes de package et cliquez sur **Enregistrer**.

### Établir une connexion sécurisée entre les piles AEM Forms JEE et OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Vous pouvez utiliser l’une des méthodes suivantes pour créer une connexion sécurisée :

* Configurer le groupe de SDK client Adobe LiveCycle avec les informations d’identification d’administrateur d’AEM Forms on JEE
* Configurer le groupe de SDK client Adobe LiveCycle à l’aide de l’authentification mutuelle

#### Configurer le groupe de SDK client Adobe LiveCycle avec les informations d’identification d’administrateur d’AEM Forms on JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Ouvrez la console web AEM. L’URL est https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez le **bundle Adobe LiveCycle Client SDK**. Spécifiez la valeur des champs suivants :

   * **URL du serveur** : spécifiez l’URL HTTPS d’AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur avec le paramètre -Djavax.net.ssl.trustStore=&lt;chemin du fichier de stockage de clés AEM Forms on JEE>.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.
   * **Nom d’utilisateur :** indiquez le nom d’utilisateur du compte AEM Forms on JEE à utiliser pour lancer des appels à partir du serveur AEM. Le compte spécifié doit disposer des autorisations pour démarrer Document services sur le serveur AEM Forms on JEE.
   * **Mot de passe** : indiquez le mot de passe du compte AEM Forms on JEE mentionné dans le champ Nom d’utilisateur.

   Cliquez sur **Enregistrer**. AEM est activé pour effectuer une recherche de documents PDF protégés par la sécurité documentaire.

#### Configurer le groupe de SDK client Adobe LiveCycle à l’aide de l’authentification mutuelle {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Activez l’authentification mutuelle pour AEM Forms on JEE. Pour plus d’informations, voir [CAC et authentification mutuelle](https://helpx.adobe.com/fr/livecycle/kb/cac-mutual-authentication.html).
1. Ouvrez la console Web AEM. L’URL est https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez le **bundle Adobe LiveCycle Client SDK**. Spécifiez la valeur des propriétés suivantes :

   * **URL du serveur** : indiquez l’URL HTTPS du serveur AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur AEM avec le paramètre -Djavax.net.ssl.trustStore=&lt;chemin du fichier de stockage de clés AEM Forms on JEE>.
   * **Activer SSL bidirectionnel** : activez l’option Activer SSL bidirectionnel.
   * **URL du fichier KeyStore** : indiquez l’URL du fichier de stockage de clés.
   * **URL du fichier TrustStore** : indiquez l’URL du fichier de magasin approuvé.
   * **Mot de passe du KeyStore** : indiquez le mot de passe du fichier de stockage des clés.
   * **Mot de passe TrustStore** : indiquez le mot de passe du fichier de magasin approuvé.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.

   Cliquez sur **Enregistrer**. AEM est activé pour effectuer une recherche de documents PDF protégés par la sécurité documentaire.

### Indexer un document PDF protégé par un exemple de stratégie  {#index-a-sample-policy-protected-pdf-document}

1. Connectez-vous à AEM Assets en tant qu’administrateur.
1. Créez un dossier dans AEM Digital Asset Manager et téléchargez les documents PDF protégés par une stratégie vers le dossier que vous venez de créer.

   Désormais, vous pouvez effectuer une recherche portant sur les documents protégés par une stratégie à l’aide de la recherche AEM.

