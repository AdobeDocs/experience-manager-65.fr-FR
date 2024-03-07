---
title: Résoudre les problèmes d’intégration
description: Découvrez comment résoudre les problèmes lors de l’intégration à Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 58%

---

# Résoudre les problèmes d’intégration{#troubleshooting-integration-issues}

## Conseils pratiques de dépannage {#general-troubleshooting-tips}

### S’assurer qu’il n’y a aucune erreur JavaScript {#ensure-there-are-no-javascript-errors}

Vérifiez si des erreurs s’affichent sur la console JavaScript du navigateur. Les erreurs non prises en charge peuvent empêcher le code suivant de s’exécuter correctement. S’il y a des erreurs, vérifiez le script à l’origine de chaque erreur et dans quelle zone celle-ci s’est produite. Le chemin d’accès au script peut indiquer à quelle fonctionnalité le script appartient.

### Connexion au niveau du composant {#logging-on-component-level}

Dans certains cas, il peut s’avérer utile d’ajouter des instructions au niveau du composant. Puisque le composant est rendu, vous pouvez ajouter un balisage temporaire pour afficher les valeurs de variable qui pourraient vous aider à identifier les problèmes potentiels. Par exemple :

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Pour plus d’informations sur la connexion, reportez-vous aux pages [Connexion](/help/sites-deploying/configure-logging.md) et [Utilisation d’enregistrements d’audit et de fichiers journaux](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Problèmes d’intégration Analytics {#analytics-integration-issues}

### L’importateur de rapports provoque une utilisation élevée du processeur/de la mémoire {#the-report-importer-causes-high-cpu-memory-usage}

L’importateur de rapports mobilise fortement le processeur ou la mémoire ou entraîne des exceptions de type `OutOfMemoryError`.

#### Solution {#solution}

Pour résoudre ce problème, essayez les méthodes suivantes :

* Assurez-vous qu’il n’y a pas un grand nombre d’importateurs d’interrogations enregistrés (voir la section &quot;L’arrêt prend beaucoup de temps en raison de l’importateur d’interrogations&quot; ci-dessous).
* Exécutez les importateurs de rapports à un moment précis de la journée à l’aide des expressions CRON pour les configurations `ManagedPollingImporter` dans la [console OSGi](/help/sites-deploying/configuring-osgi.md).

Pour plus d’informations sur la création de services d’importation de données personnalisés dans AEM, consultez l’article [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### L’arrêt prend beaucoup de temps en raison de PollingImporter. {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics a été conçu avec un mécanisme d’héritage. L’utilisateur active généralement Analytics pour un site en ajoutant une référence à une configuration Analytics dans l’onglet des propriétés de la page des [Services cloud](/help/sites-developing/extending-cloud-config.md). Toutes les sous-pages héritent alors automatiquement de la configuration sans qu’il soit nécessaire d’ajouter à nouveau la référence, sauf si une page nécessite une configuration différente. De plus, l’ajout d’une référence à un site crée automatiquement plusieurs nœuds (12 pour AEM 6.3 et les versions antérieures, 6 pour AEM 6.4 et les versions ultérieures) de type `cq;PollConfig`, qui instancient les importateurs d’interrogations utilisés pour importer les données d’Analytics vers AEM. Par conséquent :

* Le fait que de nombreuses pages fassent référence à Analytics génère un grand nombre d’importateurs d’interrogations.
* En outre, la copie et le collage de pages avec une référence à une configuration Analytics entraîne une duplication de ses importateurs d’interrogations.

#### Solution {#solution-1}

Tout d’abord, l’analyse du fichier [error.log](/help/sites-deploying/configure-logging.md) peut vous donner quelques informations sur la quantité d’importateurs d’interrogations actifs ou enregistrés. Par exemple :

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

Ensuite, assurez-vous que seules les pages principales (situées en haut de la hiérarchie) disposent d’une configuration Analytics référencée.

Pour plus d’informations sur la création de services d’importation de données personnalisés dans AEM, consultez l’article [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problèmes DTM (hérités) {#dtm-legacy-issues}

### La balise de script DTM n’est pas rendue dans la source de la page. {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

La variable [DTM](/help/sites-administering/dtm.md) La balise de script n’est pas correctement incluse dans la page même si la configuration a été référencée dans les propriétés de la page. [Cloud Service](/help/sites-developing/extending-cloud-config.md) .

#### Solution {#solution-2}

Pour résoudre ce problème, vous pouvez essayer les méthodes suivantes :

* Assurez-vous que les propriétés chiffrées peuvent être déchiffrées (notez que le chiffrement peut utiliser une clé générée automatiquement différente pour chaque instance AEM). Pour plus d’informations, également lire [Prise en charge du chiffrement des propriétés de configuration](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Republiez les configurations trouvées dans `/etc/cloudservices/dynamictagmanagement`.
* Vérifiez les listes de contrôle d’accès sur `/etc/cloudservices`. Les listes ACL doivent être :

   * allow; jcr:read; webservice-support-service-servicelibfinder
   * allow; jcr:read; everyone; `rep:glob:`&amp;ast;`/defaults/`&amp;ast;
   * allow; jcr:read; everyone; `rep:glob:`&amp;ast;`/defaults`
   * allow; jcr:read; everyone; `rep:glob:`&amp;ast;`/public/`&amp;ast;
   * allow; jcr:read; everyone; `rep:glob:`&amp;ast;`/public`

Pour plus d’informations sur la gestion des listes de contrôle d’accès, consultez la section [Administration et sécurité des utilisateurs](/help/sites-administering/security.md#permissions-in-aem) page.

## Problèmes d’intégration de Target {#target-integration-issues}

### Contenu ciblé non visible en mode Aperçu lors de l’utilisation de composants de page personnalisés {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Ce problème se produit car les composants de page personnalisés n’incluent pas le JSP correct ou les bibliothèques clientes qui gèrent les intégrations de la gestion dynamique des balises Target.

#### Solution {#solution-3}

Vous pouvez essayer les solutions suivantes :

* Assurez-vous que le fichier personnalisé `headlibs.jsp` (le cas échéant, `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) inclut les propriétés suivantes :

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Assurez-vous que le fichier personnalisé `head.html` (le cas échéant, `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) n’inclut **pas** de manière sélective des headlibs d’intégration spécifiques comme dans l’exemple ci-dessous :

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

Le fichier `servicelibs.jsp` ajoute les objets d’analyse JavaScript requis et charge les bibliothèques de service cloud associées au site web. Pour le service Target, les bibliothèques sont chargées via le fichier `/libs/cq/analytics/components/testandtarget/headlibs.jsp`.

Le jeu de bibliothèques chargé dépend du type de bibliothèque cliente cible (`mbox.js` ou `at.js`) utilisé dans la configuration de Target.

Lorsque vous utilisez la gestion dynamique des balises pour fournir `mbox.js` ou `at.js`, assurez-vous que les bibliothèques sont chargées avant que le contenu soit rendu. L’utilisation de systèmes Tag Management qui chargent ces bibliothèques de manière asynchrone peut entraîner des problèmes lors de l’exécution du code JavaScript spécifique à la cible.

Pour plus d’informations, reportez-vous au [Développement pour le contenu ciblé](/help/sites-developing/target.md#understanding-the-target-component) page.

### L’erreur &quot;Identifiant de suite de rapports manquant dans l’initialisation de l’AppMeasurement&quot; s’affiche dans la console du navigateur. {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Ce problème peut se produire lorsqu’Adobe Analytics est mis en œuvre sur le site web à l’aide de la gestion dynamique des balises et utilise le code personnalisé. Cette expression utilise `s = new AppMeasurement()` pour instancier l’objet `s`.

#### Solution {#solution-4}

Utilisez `s_gi` plutôt que la méthode d’instanciation `new AppMeasurement`. Par exemple :

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Une offre par défaut s’affiche de manière aléatoire au lieu de l’offre correcte. {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Ce problème peut avoir plusieurs causes :

* Le chargement asynchrone de bibliothèques clientes cibles (`mbox.js` ou `at.js`) à l’aide de systèmes de gestion des balises tiers peut rompre le ciblage de manière aléatoire. Les bibliothèques cibles doivent être chargées de manière synchrone dans l’en-tête de la page. C’est toujours le cas lorsque les bibliothèques sont diffusées à partir d’AEM.

* Le chargement simultané de deux bibliothèques clientes cibles (`at.js`), par exemple une utilisant la gestion dynamique des balises et l’autre utilisant la configuration cible dans AEM, peut entraîner des conflits pour la définition d’`adobe.target` si les versions d’`at.js` diffèrent.

#### Solution {#solution-5}

Vous pouvez essayer les solutions suivantes :

* Assurez-vous que le code client qui charge les bibliothèques de type DTM (qui à leur tour chargent les bibliothèques Target) est exécuté de manière synchrone dans la variable [page head](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* Si le site est configuré pour utiliser la gestion dynamique des balises pour fournir les bibliothèques cible, assurez-vous que la **bibliothèque cliente diffusée par l’option de gestion dynamique des balises** est cochée dans la [configuration cible](https://helpx.adobe.com/fr/experience-manager/6-3/sites/administering/using/target-configuring.html) de ce site.

### Une offre par défaut est toujours affichée à la place de l’offre correcte lors de l’utilisation d’AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

Les versions prêtes à l’emploi AEM 6.2 et 6.3 ne sont pas compatibles avec AT.js version 1.3.0+. Avec l’introduction par AT.js version 1.3.0 de la validation des paramètres pour ses API, `adobe.target.applyOffer()` a besoin d’un paramètre « mbox » qui n’est pas fourni par le code `atjs-itegration.js`.

#### Solution {#solution-6}

Pour résoudre ce problème, modifiez `atjs-itegration.js` et ajoutez le champ `"mbox": mboxName` dans l’objet de paramètre pour `adobe.target.applyOffer()` comme suit :

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### La page Objectifs et paramètres n’affiche pas la section Sources de création {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Ce problème est probablement lié à la mise en service de la [configuration A4T d’Analytics Cloud](/help/sites-administering/target-configuring.md).

#### Solution {#solution-7}

Vous devez vérifier que A4T est correctement activé pour votre compte Target en adressant la demande de vérification suivante à AEM :

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Si la réponse contient la ligne `a4tEnabled:false`, contactez l’[Assistance clientèle Adobe](https://helpx.adobe.com/fr/contact.html) pour que votre compte soit correctement configuré.

### API Target utiles {#helpful-target-apis}

Vous trouverez ci-dessous deux API Target pouvant être utiles pour résoudre les problèmes liés à Target :

* Récupération du point de terminaison Target pour un code client donné

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Récupération du profil d’un client

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
