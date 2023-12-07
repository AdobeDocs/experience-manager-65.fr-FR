---
title: Activer AEM pour rechercher des documents PDF protégés par la sécurité des documents
description: Découvrez comment activer la recherche AEM native pour effectuer une recherche de texte intégral sur des documents de PDF protégés DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 59%

---

# Activez AEM pour rechercher des documents PDF protégés par la sécurité des documents.{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM recherche permet de rechercher et de localiser AEM ressources et d’effectuer une recherche de texte dans divers formats de document couramment utilisés tels que les fichiers texte brut, les documents Microsoft Office et les documents PDF. Vous pouvez également étendre la recherche native pour effectuer une recherche de texte intégral sur [Documents PDF protégés par AEM Document Security](../../forms/using/admin-help/document-security.md). Pour permettre à AEM d’effectuer une recherche de texte intégral sur ces documents, procédez comme suit :

1. Établissement d’une connexion sécurisée
1. Index d’un exemple de document de PDF protégé par une stratégie

## Prérequis {#prerequisites}

* Si vous utilisez AEM Forms sur OSGi :

   * Installez le [package de l’indexeur de Document Security AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) sur le serveur AEM Forms.

   * Vérifiez qu’un serveur AEM Forms on JEE est opérationnel et que la sécurité des documents est installée sur le serveur AEM Forms on JEE approprié. Le serveur AEM Forms on JEE est nécessaire pour indexer le document protégé.

* Si vous utilisez uniquement un serveur AEM Forms on JEE, le package de l’indexeur est déjà installé.
* Vérifiez que tous les lots sont en cours d’utilisation. Si tous les bundles ne sont pas actifs, attendez qu’ils soient tous opérationnels.

   * Pour AEM Forms sur OSGi, les lots sont répertoriés à l’adresse suivante https://&#39;[server]:[port]&#39;/system/console/bundles.
   * Pour AEM Forms sur JEE, les lots sont répertoriés à l’adresse suivante : https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Par exemple, https://localhost:8080/lc/system/console/bundles.

* Ajoutez le package *sun.util.calendar* à la liste autorisée. Pour ajouter le package à la liste autorisée, procédez comme suit :

   1. Ouvrez la console Web AEM. L’URL est la suivante : https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Recherchez et ouvrez **la configuration du pare-feu de désérialisation.**

   1. Ajoutez le package sun.util.calendar au champ de préfixes de package ou de classes de placement sur la liste autorisée, puis cliquez sur **Enregistrer**.

### Établir une connexion sécurisée entre les piles AEM Forms JEE et OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Vous pouvez utiliser l’une des méthodes suivantes pour établir la connexion sécurisée :

* Configuration du bundle de SDK client Adobe LiveCycle avec les informations d’identification d’administrateur d’AEM Forms on JEE
* Configurer le groupe de SDK client Adobe LiveCycle à l’aide de l’authentification mutuelle

#### Configuration du bundle de SDK client Adobe LiveCycle avec les informations d’identification d’administrateur d’AEM Forms on JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Ouvrez la console Web AEM. L’URL est la suivante : https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez le **bundle Adobe LiveCycle Client SDK**. Spécifiez la valeur des champs suivants :

   * **URL du serveur** : spécifiez l’URL HTTPS d’AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur avec le paramètre -Djavax.net.ssl.trustStore=&lt;chemin du fichier de stockage de clés AEM Forms on JEE>.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.
   * **Nom d’utilisateur :** indiquez le nom d’utilisateur du compte AEM Forms on JEE à utiliser pour lancer des appels à partir du serveur AEM. Le compte spécifié doit disposer des autorisations nécessaires pour démarrer Document Services sur le serveur AEM Forms on JEE.
   * **Password**: indiquez le mot de passe du compte AEM Forms on JEE mentionné dans le champ Nom d’utilisateur .

   Cliquez sur **Enregistrer**. AEM est activé pour rechercher des documents de PDF protégés par Document Security.

#### Configurer le groupe de SDK client Adobe LiveCycle à l’aide de l’authentification mutuelle {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Activez l’authentification mutuelle pour AEM Forms on JEE. Pour plus d’informations, voir [CAC et authentification mutuelle](https://helpx.adobe.com/fr/livecycle/kb/cac-mutual-authentication.html).
1. Ouvrez la console Web AEM. L’URL est la suivante : https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez le **bundle Adobe LiveCycle Client SDK**. Spécifiez la valeur des propriétés suivantes :

   * **URL du serveur** : indiquez l’URL HTTPS du serveur AEM Forms on JEE. Pour activer la communication via https, redémarrez le serveur AEM avec le répertoire -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> .
   * **Activer SSL bidirectionnel** : activez l’option Activer SSL bidirectionnel.
   * **URL du fichier KeyStore** : indiquez l’URL du fichier de stockage de clés.
   * **URL du fichier TrustStore** : indiquez l’URL du fichier de magasin approuvé.
   * **Mot de passe du KeyStore** : indiquez le mot de passe du fichier de stockage des clés.
   * **Mot de passe TrustStore** : indiquez le mot de passe du fichier de magasin approuvé.
   * **Nom du service** : ajoutez RightsManagementService à la liste des services spécifiés.

   Cliquez sur **Enregistrer**. AEM est activé pour la recherche de documents de PDF protégés par Document Security

### Index d’un exemple de document de PDF protégé par une stratégie {#index-a-sample-policy-protected-pdf-document}

1. Connectez-vous à AEM Assets en tant qu’administrateur.
1. Créez un dossier dans AEM Digital Asset Manager et téléchargez les documents de PDF protégés par une stratégie vers le dossier nouvellement créé.

   Vous pouvez désormais effectuer des recherches dans les documents protégés par une stratégie à l’aide de la recherche AEM.
