---
title: Éditeur universel
description: Découvrez la flexibilité de l’éditeur universel et comment il peut vous aider à optimiser vos expériences découplées à l’aide d’AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# Éditeur universel {#universal-editor}

Découvrez la flexibilité de l’éditeur universel et comment il peut vous aider à optimiser vos expériences découplées à l’aide d’AEM 6.5.

## Vue d’ensemble {#overview}

L’éditeur universel est un éditeur visuel polyvalent qui fait partie d’Adobe Experience Manager Sites. Il permet aux auteurs et aux autrices d’effectuer une modification WYSIWYG de n’importe quelle expérience découplée.

* Les auteurs et les autrices bénéficient de la flexibilité de l’éditeur universel, car il offre la même interface de modification visuelle pour toutes les formes de contenu découplé AEM.
* Les développeurs et les développeuses bénéficient de la polyvalence de l’éditeur universel, car il prend également en charge le véritable découplage de l’implémentation. Il permet aux développeurs et aux développeuses d’utiliser pratiquement tout framework ou toute architecture de leur choix, sans imposer la moindre contrainte de SDK ou de technologie.

Consultez la [documentation d’AEM as a Cloud Service sur l’éditeur universel](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) pour plus d’informations.

## Architecture {#architecture}

L’éditeur universel est un service qui fonctionne en tandem avec AEM pour créer du contenu découplé.

* L’éditeur universel est hébergé sur `https://experience.adobe.com/#/aem/editor/canvas` et peut modifier les pages créées par AEM 6.5.
* La page AEM est lue par l’éditeur universel via Dispatcher à partir de l’instance de création AEM.
* Le service de l’éditeur universel, qui s’exécute sur le même hôte que Dispatcher, écrit les modifications dans l’instance de création AEM.

![Flux de création à l’aide de l’éditeur universel](assets/author-flow.png)

## Conditions requises {#requirements}

L’éditeur universel est pris en charge par :

* AEM 6.5
   * Les hébergements locaux et AMS sont pris en charge.
* [AEM 6.5 LTS](https://experienceleague.adobe.com/fr/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Les hébergements locaux et AMS sont pris en charge.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

Ce document aborde la prise en charge de l’éditeur universel par AEM 6.5. Pour utiliser l’éditeur universel avec AEM 6.5, vous devez disposer des éléments suivants :

* AEM 6.5 avec le pack de services 23 ou version ultérieure
   * Les packs de service 21 et 22 sont également pris en charge avec [un pack de fonctionnalités](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip).
* Dispatcher configuré de manière appropriée

## Configuration {#setup}

Pour tester l’éditeur universel, vous devez effectuer les opérations suivantes :

1. [Configurer un service d’éditeur universel local.](#set-up-ue)
1. [Configurer votre Dispatcher pour qu’il autorise le service d’éditeur universel.](#update-dispatcher)

Une fois que vous avez terminé la configuration, vous pouvez [paramétrer vos applications pour qu’elles utilisent l’éditeur universel.](#instrumentation)

### Configurer les services {#configure-services}

L’éditeur universel exploite plusieurs packages pour lesquels une configuration supplémentaire est nécessaire.

#### Définissez l’attribut SameSite pour le cookie `login-token`. {#samesite-attribute}

1. Ouvrez le gestionnaire de configuration.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez le **Gestionnaire d’authentification de jeton Adobe Granite** dans la liste, puis cliquez sur **Modifier les valeurs de configuration**.
1. Dans la boîte de dialogue, remplacez la valeur de l’attribut **SameSite pour le cookie du jeton de connexion** (`token.samesite.cookie.attr`) par `Partitioned`.
1. Cliquez sur **Enregistrer**.

#### Supprimez l’option X-Frame des en-têtes `SAMEORIGIN`. {#sameorigin}

1. Ouvrez le gestionnaire de configuration.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez le **Servlet principal Apache Sling** dans la liste, puis cliquez sur **Modifier les valeurs de configuration**.
1. Supprimez la valeur `X-Frame-Options=SAMEORIGIN` de l’attribut **En-têtes de réponse supplémentaires** (`sling.additional.response.headers`) s’il existe.
1. Cliquez sur **Enregistrer**.

#### Configurez le gestionnaire d’authentification des paramètres de requête Adobe Granite. {#query-parameter}

1. Ouvrez le gestionnaire de configuration.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez le **Gestionnaire d’authentification des paramètres de requête Adobe Granite** dans la liste, puis cliquez sur **Modifier les valeurs de configuration**.
1. Dans le champ **Chemin d’accès** (`path`), ajoutez `/` pour activer le gestionnaire.
   * Une valeur vide désactive le gestionnaire d’authentification.
1. Cliquez sur **Enregistrer**.

#### Définissez pour quels chemins d’accès de contenu ou `sling:resourceTypes` l’éditeur universel doit s’ouvrir. {#paths}

1. Ouvrez le gestionnaire de configuration.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez le **Service d’URL de l’éditeur universel** dans la liste, puis cliquez sur **Modifier les valeurs de configuration**.
1. Définissez pour quels chemins d’accès de contenu ou `sling:resourceTypes` l’éditeur universel doit s’ouvrir.
   * Dans le champ **Mappage d’ouverture de l’éditeur universel** indiquez les chemins d’accès pour lesquels l’éditeur universel doit être ouvert.
   * Dans le champ **Sling:resourceTypes qui doit être ouvert par l’éditeur universel**, indiquez la liste des ressources qui sont ouvertes directement par l’éditeur universel.
1. Cliquez sur **Enregistrer**.
1. Vérifiez votre [configuration d’externaliseur](/help/sites-developing/externalizer.md) pour vous assurer que vous disposez au minimum des environnements local, de création et de publication définis comme dans l’exemple suivant.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Une fois ces étapes de configuration terminées, AEM ouvre l’éditeur universel pour les pages dans l’ordre suivant.

1. AEM vérifie ensuite les mappages via `Universal Editor Opening Mapping`, et si le contenu se trouve dans l’un des chemins définis, l’éditeur universel s’ouvre pour celui-ci.
1. Pour le contenu ne se trouvant pas dans les chemins définis dans le mappage `Universal Editor Opening Mapping`, AEM vérifie si les `resourceType` du contenu correspondent à ceux définis dans le **Sling:resourceTypes qui doit être ouvert par l’éditeur universel**. Si le contenu correspond à l’un de ces types, l’éditeur universel s’ouvre pour celui-ci à l’adresse `${author}${path}.html`.
1. Sinon, AEM ouvre l’éditeur de page.

Les variables suivantes sont disponibles pour définir vos mappages dans l’`Universal Editor Opening Mapping`.

* `path` : chemin d’accès du contenu de la ressource à ouvrir
* `localhost` : entrée de l’externaliseur pour un `localhost` sans schéma, par exemple `localhost:4502`
* `author` : entrée de l’externaliseur pour la création sans schéma, par exemple `localhost:4502`
* `publish` : entrée de l’externaliseur pour la publication sans schéma, par exemple `localhost:4503`
* `preview` : entrée de l’externaliseur pour la prévisualisation sans schéma, par exemple `localhost:4504`
* `env` : `prod`, `stage`, `dev` en fonction des modes d’exécution Sling définis
* `token` : jeton de requête requis pour le `QueryTokenAuthenticationHandler`

Exemples de mappages :

* Ouvrez toutes les pages présentes dans `/content/foo` dans l’instance de création AEM :
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Cela entraîne l’ouverture de `https://localhost:4502/content/foo/x.html?login-token=<token>`.
* Ouvrez toutes les pages présentes dans `/content/bar` sur un serveur NextJS distant, en fournissant toutes les variables comme informations.
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Cela entraîne l’ouverture de `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`.

### Configurer le service d’éditeur universel {#set-up-ue}

Une fois AEM mis à jour et configuré, vous pouvez configurer un service d’éditeur universel local pour votre propre développement et vos propres tests en local.

1. Installez Node.js 20 ou une version ultérieure.
1. Téléchargez et décompressez le dernier service d’éditeur universel à partir de la [Distribution logicielle](https://experienceleague.adobe.com/fr/docs/experience-cloud/software-distribution/home).
1. Configurez le service d’éditeur universel via des variables d’environnement ou un fichier `.env`.
   * [Consultez la documentation sur l’éditeur universel d’AEM as a Cloud Service pour plus d’informations.](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Notez que vous devrez peut-être utiliser l’option `UES_MAPPING` si une réécriture d’adresse IP interne est requise.
1. Exécuter `universal-editor-service.cjs`

### Mettre à jour Dispatcher {#update-dispatcher}

Une fois AEM configuré et un service d’éditeur universel local en cours d’exécution, vous devez autoriser un proxy inverse pour le nouveau service [dans Dispatcher.](https://experienceleague.adobe.com/fr/docs/experience-manager-dispatcher/using/dispatcher)

1. Paramétrez le fichier vhost de l’instance de création pour inclure un proxy inverse.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >Le port par défaut est 8080. Si vous avez modifié cette valeur à l’aide du paramètre `UES_PORT` dans [votre fichier `.env`,](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) vous devez paramétrer ici la valeur de port en conséquence.

1. Redémarrez Apache.

## Paramétrer votre application {#instrumentation}

Avec AEM mis à jour et un service d’éditeur universel local en cours d’exécution, vous pouvez commencer à modifier du contenu découplé à l’aide de l’éditeur universel.

Cependant, votre application doit être paramétrée pour tirer parti de l’éditeur universel. Cela implique d’inclure des balises meta pour indiquer à l’éditeur comment et où conserver le contenu. Les détails de ce paramétrage sont disponibles dans la [documentation sur l’éditeur universel d’AEM as a Cloud Service.](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page).

Notez que lorsque vous suivez les instructions de la documentation sur l’éditeur universel avec AEM as a Cloud Service, les modifications suivantes s’appliquent lorsque vous l’utilisez avec AEM 6.5.

* Le protocole dans la balise meta doit être `aem65` au lieu de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* Le point d’entrée du service de l’éditeur universel doit être spécifié à l’aide d’une balise meta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Dans la section `plugins` de la définition des composants, `aem65` doit être utilisé à la place de `aem`.

>[!TIP]
>
>Pour obtenir un guide complet destiné aux développeurs et aux développeuses qui commencent à utiliser l’éditeur universel, consultez le document [Présentation de l’éditeur universel pour les développeurs et les développeuses AEM](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) dans la documentation d’AEM as a Cloud Service, tout en gardant à l’esprit les modifications nécessaires pour la prise en charge d’AEM 6.5, comme mentionné dans cette section.

## Différences entre AEM 6.5 et AEM as a Cloud Service {#differences}

L’éditeur universel d’AEM 6.5 fonctionne globalement de la même manière que dans AEM as a Cloud Service, y compris pour l’interface d’utilisation et la majorité de la configuration. Il existe cependant des différences à noter.

* L’éditeur universel dans AEM 6.5 prend uniquement en charge le cas d’utilisation découplé.
* La configuration de l’éditeur universel varie légèrement pour AEM 6.5 ([comme décrit](#setup) dans le présent document).
* L’éditeur universel dans AEM 6.5 utilise un sélecteur de ressources et un sélecteur de fragments de contenu différents d’AEM as a Cloud Service.
