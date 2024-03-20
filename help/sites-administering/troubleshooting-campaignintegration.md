---
title: Résolution des problèmes d’intégration d’Adobe Campaign Classic
description: Découvrez comment résoudre les problèmes liés à l’intégration d’Adobe Campaign Classic.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 98%

---


# Résolution des problèmes d’intégration d’Adobe Campaign Classic{#troubleshooting-your-adobe-campaign-classic-integration}

Découvrez comment résoudre les problèmes liés à l’intégration d’Adobe Campaign Classic (ACC).

Les conseils de dépannage suivants permettent de résoudre les problèmes les plus courants que vous pouvez rencontrer lorsque vous intégrez AEM à ACC :

## Conseils pratiques de dépannage {#general-troubleshooting-tips}

Vérifiez si les appels HTTP sont envoyés et reçus par les deux solutions (AEM > Adobe Campaign Classic, Adobe Campaign Classic > AEM). Cette astuce vous permet d’éviter les problèmes de pare-feu/SSL.

* Pour la fonctionnalité AEM, vous pouvez constater que les appels JSON sont demandés depuis l’interface de création d’AEM.
   * Ces appels ne doivent pas entraîner d’erreur HTTP-500.
   * Si vous voyez des erreurs HTTP 500, vérifiez le fichier `error.log` pour plus d’informations.
* L’augmentation du niveau de débogage pour les classes de campagne dans AEM peut également aider à résoudre les problèmes.

## Si la connexion échoue {#when-the-connection-fails}

Vérifiez que vous avez configuré l’opérateur **`aemserver`** dans Adobe Campaign Classic.

## Si les images n’apparaissent pas dans la console Adobe Campaign Classic {#if-images-do-not-appear-in-the-adobe-campaign-console}

Vérifiez la source HTML et confirmez que vous pouvez ouvrir l’URL à partir de l’ordinateur client. Si l’URL contient `localhost:4503`, modifiez la configuration de Day CQ Link Externalizer sur votre instance de création AEM. Faites pointer l’instance vers une instance de publication accessible à partir de la machine de la console Adobe Campaign Classic.

Consultez la section [Configuration de l’externaliseur.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Si vous ne pouvez pas vous connecter d’AEM à Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Recherchez le message d’erreur suivant dans Adobe Campaign Classic.

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Pour résoudre ce problème, modifiez ce qui suit dans `$CAMPAIGN_HOME/conf/config-<instance-name>.xml` :

* `<dataStore hosts="*" lang="en_GB">`

## Si aucune donnée ne s’affiche dans la boîte de dialogue Adobe Campaign Classic {#if-no-data-displays-in-the-adobe-campaign-dialog}

Dans Adobe Campaign Classic, assurez-vous qu’il n’y a aucune barre oblique (`/`) après le numéro de port.

![Adobe Campaign Classic : assurez-vous qu’aucune barre oblique ne se trouve après le numéro de port.](assets/chlimage_1-149.png)

## Si vous recevez un avertissement à propos de setlocale {#if-you-get-a-warning-about-your-setlocale}

Lors du démarrage du service Apache HTTPD pour Adobe Campaign Classic, l’erreur `Warning: setlocale: LC_CTYPE cannot change locale` peut s’afficher.

Assurez-vous que `en_CA.ISO-8859-15 locale` est installé sur votre serveur Adobe Campaign Classic.

* Vous pouvez vérifier l’installation à l’aide de `local -a`.
* Si l’installation n’a pas été effectuée, vous pouvez corriger le script `/usr/local/neolane/nl6/env.sh` et remplacer le paramètre régional par un paramètre installé.

## Si vous obtenez une erreur lors de la compilation du script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Si le message d’erreur suivant s’affiche dans le fichier journal d’AEM :

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Procédez comme suit sur le serveur Adobe Campaign Classic.

1. Ouvrez le fichier `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`.
1. Modifiez la ligne 467 de la méthode `amcGetSeedMetaData`.
1. Remplacez `label : [inclView.@label](mailto:inclView.@label)` par `label : String([inclView.@label](mailto:inclView.@label))`.
1. Enregistrez.
1. Relancez le serveur.

## Si Adobe Campaign Classic affiche une erreur lors du clic sur le bouton Synchroniser {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Lorsque vous cliquez sur le bouton **Synchroniser** dans Adobe Campaign Classic, l’erreur suivante peut s’afficher :

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Pour résoudre ce problème, assurez-vous que l’URL de connexion AEM configurée dans les **Comptes externes** dans Adobe Campaign Classic est accessible à partir de l’ordinateur.

Un changement de `localhost` à une adresse IP pour l’URL peut souvent résoudre ce problème.

## Si vous recevez une erreur « Cannot parse XTK Date+Time &#39;undefined » {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Après avoir cliqué sur **Synchroniser** dans AEM, vous pouvez recevoir une erreur indiquant qu’un script s’est produit sur les pages.

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

Cette erreur survient en présence d’informations obsolètes relatives à Adobe Campaign Classic sur l’instance AEM. Vous pouvez résoudre ce problème en procédant comme suit :

1. Supprimez toutes les configurations d’intégration Adobe Campaign Classic sur AEM.
1. Recréez l’intégration.
1. Créez un modèle.

## Si une connexion à SSL affiche une erreur lors de la configuration du service cloud {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Soumettez un ticket à l’équipe d’assistance Adobe Campaign si les éléments suivants sont affichés dans le `error.log` d’AEM.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## Si vous voyez HTTP au lieu des liens HTTPS prévus dans la boîte de dialogue de synchronisation {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Lorsque vous essayez de synchroniser le contenu dans la diffusion Adobe Campaign Classic, AEM renvoie une liste de newsletters. Toutefois, les URL des newsletters de la liste peuvent être des adresses HTTP au lieu de HTTPS. Lorsque vous sélectionnez l’un des éléments de la liste, une erreur se produit. Cette erreur peut se produire avec la configuration suivante.

* Adobe Campaign hébergé à l’aide de https pour les communications avec l’instance de création AEM
* Proxy inverse mettant fin à SSL
* Instance de création AEM On-Premise

Pour résoudre ce problème, procédez comme suit :

* Le Dispatcher AEM ou le proxy inverse doit être configuré pour transmettre le protocole d’origine en tant qu’en-tête.
* Le **Filtre SSL du service HTTP Apache Felix** dans la configuration OSGi d’AEM doit être configuré avec les paramètres d’en-tête requis.
   * `https://<host>:<port>/system/console/configMgr`
   * Voir [https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## Un modèle personnalisé ne peut pas être sélectionné dans les propriétés de la page. {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Lors de la création d’un modèle d’e-mail dans AEM pour Adobe Campaign Classic, vous devez inclure la propriété `acMapping` avec la valeur `mapRecipient` dans le nœud `jcr:content` du modèle. Si vous ne le faites pas, vous ne pouvez pas sélectionner le modèle Adobe Campaign Classic dans **Propriétés de la page** d’AEM. Le champ apparaît désactivé.

## Si vous voyez l’erreur « com.day.cq.mcm.campaign.servlets.util.ParameterMapper » dans les journaux d’AEM, {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

L’erreur `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` peut s’afficher dans les journaux d’AEM lors de l’utilisation d’un modèle personnalisé.

Cette erreur se produit si la propriété `acMapping` est définie sur une valeur autre que `recipient.firstName`, une valeur vide est créée dans Adobe Campaign Manager.

Si cette erreur se produit, installez le pack de fonctionnalités 6576 pour AEM depuis le [Partage de modules](/help/sites-administering/package-manager.md#package-share).
