---
title: Configuration de l’authentification étendue à partir d’un navigateur externe pour Document Security
description: Découvrez comment configurer l’authentification du navigateur externe afin que les utilisateurs puissent s’authentifier pour les documents PDF protégés par une politique dans Acrobat ou Reader à l’aide du navigateur web par défaut du système.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 89a07256cd5bb850aac19565ad86273322fa1f31
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 4%

---

# Configuration de l’authentification étendue à partir d’un navigateur externe pour Document Security {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> Assurez-vous de disposer des droits d’administrateur pour accéder à la console d’administration AEM Forms.

L’authentification étendue à partir d’un navigateur externe permet aux utilisateurs de s’authentifier pour les documents PDF protégés par une politique à l’aide du navigateur web par défaut du système (tel que Microsoft Edge ou Google Chrome) au lieu du contrôle de navigateur intégré dans Acrobat ou Reader. Cela permet d’utiliser des méthodes d’authentification modernes telles que PassKey, l’authentification biométrique et d’autres fonctionnalités de fournisseur d’identité (IDP) qui nécessitent un navigateur moderne.

Lorsque cette option est activée, l’ouverture d’un document protégé par une politique dans Acrobat ou Reader lance la page de connexion du fournisseur d’identité dans le navigateur par défaut de l’utilisateur. Après l’authentification, l’utilisateur est automatiquement redirigé vers Acrobat ou Reader et le document est déverrouillé.

## Conditions préalables {#prerequisites}

Avant de configurer l’authentification du navigateur externe, assurez-vous que les conditions suivantes sont remplies :

* AEM Forms 6.5 on JEE avec le pack de services 6.5.25.0 déployé, ou le pack de services 6.5.24.0 avec le correctif de correctif JEE applicable installé sur un serveur d’applications pris en charge (JBoss, WebLogic ou WebSphere). Consultez la section [&#x200B; Liens de distribution logicielle pour le 6.5.24.0](#software-distribution-links) AEM Forms JEE Hotfix2 .
* L’authentification étendue (authentification tierce) est déjà activée et fonctionnelle avec un fournisseur d’identité. Voir [Paramètres de configuration du serveur](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings) et [Ajouter le fournisseur d’authentification étendu](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider).
* Adobe Acrobat Pro ou Adobe Acrobat Reader (64 bits) installé sur le PC client Windows avec la dernière mise à jour.

>[!NOTE]
>
> L’authentification du navigateur externe nécessite une version prise en charge d’Adobe Acrobat ou de Adobe Acrobat Reader sur le client. Voir les [notes de mise à jour d’Acrobat (suivi continu de mars 2026)](https://www.adobe.com/devnet-docs/acrobatetk/tools/ReleaseNotesDC/continuous/dccontinuousmarch2026.html#dccontinuousmarchtwentytwentysix) pour obtenir des informations sur les versions et les mises à jour.

### Liens de distribution logicielle pour AEM Forms JEE Hotfix2 6.5.24.0 {#software-distribution-links}

L’authentification du navigateur externe est disponible dans le pack de services AEM Forms on JEE 6.5.25.0 et versions ultérieures.

Si vous utilisez le pack de services 6.5.24.0 ou une version antérieure d’AEM Forms on JEE, effectuez l’une des opérations suivantes :

* Effectuez la mise à niveau vers le pack de services 6.5.25.0[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) d’AEM Forms on JEE.
* Installez le correctif 6.5.24.0 AEM Forms JEE Hotfix pour votre serveur d’applications et votre plateforme à l’aide des liens ci-dessous.

Téléchargez et installez le correctif 6.5.24.0 AEM Forms JEE Hotfix pour votre plateforme à partir de la [distribution logicielle d’Adobe &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) :

**JBoss**

* Windows : [correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur JBoss JEE](6.5.24.0-win-jboss.zip)
* Linux : [correctif pour AEM Service Pack 6.5.24.0 sur Linux pour le serveur JEE JBoss](6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows : [correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur WebSphere JEE](6.5.24.0-win-websphere.zip)
* Linux : [correctif pour AEM Service Pack 6.5.24.0 sur Linux pour le serveur WebSphere JEE](6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows : [correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur WebLogic JEE](6.5.24.0-win-weblogic.zip)
* Linux : [correctif pour AEM Service Pack 6.5.24.0 sur Linux pour le serveur WebLogic JEE](6.5.24.0-linux-weblogic.tar.gz)

Pour obtenir des instructions d’installation, voir [Installation d’un correctif JEE](/help/release-notes/jee-patch-installer-65.md).

## Activer l’authentification du navigateur externe {#enable-external-browser-authentication}

Cette vidéo montre comment activer l’authentification du navigateur externe sur le serveur Document Security d’AEM Forms.

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. Dans Administration Console, cliquez sur **Services** > **Document Security** > **Configuration** > **Configuration du serveur**.
1. Recherchez la section **Autoriser l’authentification étendue à partir d’un navigateur externe pour les applications clientes Adobe**.
1. Cochez la case correspondant à chaque plateforme cliente Adobe à activer :
   * **Adobe Acrobat et Reader (64 bits) - Bureau**
   * **Adobe Acrobat Reader (32 bits) - Bureau**
1. Cliquez sur **OK**.

Pour la description des paramètres du serveur, voir [Paramètres de configuration du serveur](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings).

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## Vérification {#verification}

Cette vidéo montre comment vérifier l’authentification du navigateur externe : ouvrez un PDF protégé par une politique dans Acrobat, connectez-vous via votre navigateur par défaut et confirmez que le document se déverrouille après l’authentification.

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Créez un document PDF protégé par une politique à l’aide du serveur Document Security.
1. Sur un ordinateur client Windows, ouvrez le PDF protégé dans Acrobat Pro ou Acrobat Reader.
1. Une boîte de dialogue de consentement s’affiche dans Acrobat. Cliquez sur **Se connecter**.
1. Vérifiez que le navigateur par défaut du système s’ouvre sur la page de connexion du fournisseur d’identité.
1. Authentification complète.
1. Vérifiez que le document protégé s’ouvre correctement.

## Résolution des problèmes {#troubleshooting}

### Le navigateur intégré s’ouvre à la place du navigateur système {#embedded-browser-opens-instead-of-system-browser}

* Vérifiez que l&#39;authentification du navigateur externe est activée sur le serveur. Voir [Activer l’authentification de navigateur externe](#enable-external-browser-authentication).
* Vérifiez que la version d’Acrobat ou de Reader prend en charge cette fonctionnalité. Voir [&#128279;](#acrobat).

### L’authentification réussit dans le navigateur, mais le document ne se déverrouille pas {#authentication-succeeds-but-document-does-not-unlock}

* Assurez-vous qu’Acrobat ou Reader est en cours d’exécution et n’est pas bloqué par un pare-feu ou un logiciel de sécurité.
* Si le problème persiste, réinstallez ou réparez l’installation d’Acrobat ou de Reader pour restaurer l’enregistrement du gestionnaire de protocole.

### Le message « Nous n’avons pas pu vous connecter » s’affiche dans Acrobat {#we-couldnt-sign-you-in-message}

* L&#39;utilisateur a peut-être mis trop de temps à s&#39;authentifier. Réessayez.
* Vérifiez la connectivité réseau entre le navigateur et le serveur AEM Forms.

### L’option Authentification n’apparaît pas sur la page de connexion {#authentication-option-does-not-appear}

* Les méthodes et options d’authentification sont configurées par le fournisseur d’identité, et non par AEM Forms ou Acrobat. Assurez-vous que le fournisseur d’identité prend en charge la méthode d’authentification que vous souhaitez utiliser.
* Vérifiez que la page de connexion se charge dans le navigateur système (et non dans le navigateur intégré).
