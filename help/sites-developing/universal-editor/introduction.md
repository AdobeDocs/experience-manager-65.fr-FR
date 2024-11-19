---
title: Éditeur universel
description: Découvrez la flexibilité de l’éditeur universel et comment il peut vous aider à optimiser vos expériences sans tête à l’aide d’AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: c3af0befce5534891d45c2507684a2017f9363f8
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 1%

---


# Éditeur universel {#universal-editor}

Découvrez la flexibilité de l’éditeur universel et comment il peut vous aider à optimiser vos expériences sans tête à l’aide d’AEM 6.5.

## Vue d’ensemble {#overview}

Universal Editor est un éditeur visuel polyvalent qui fait partie d’Adobe Experience Manager Sites. Il permet aux auteurs de faire la modification WYSIWYG de n’importe quelle expérience sans tête.

* Les auteurs bénéficient de la flexibilité de l’éditeur universel, car il prend en charge la même modification visuelle cohérente pour toutes les formes de contenu AEM sans interface.
* Les développeurs bénéficient de la polyvalence d’Universal Editor dans la mesure où il prend également en charge un véritable découplage de l’implémentation. Il permet aux développeurs d’utiliser pratiquement n’importe quelle structure ou architecture de leur choix, sans imposer de contraintes de SDK ou de technologie.

Pour plus d’informations, consultez la [documentation AEM as a Cloud Service sur Universal Editor](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) .

## Architecture {#architecture}

Universal Editor est un service qui fonctionne en tandem avec l’AEM de créer du contenu sans interface utilisateur.

* L’éditeur universel est hébergé à l’emplacement `https://experience.adobe.com/#/aem/editor/canvas` et peut modifier les pages rendues par AEM 6.5.
* La page AEM est lue par l’éditeur universel via le dispatcher de l’instance d’auteur AEM.
* Le service d’éditeur universel, qui s’exécute sur le même hôte que Dispatcher, écrit les modifications sur l’instance d’auteur AEM.

![Flux d’auteur à l’aide de l’éditeur universel](assets/author-flow.png)

## Configuration {#setup}

Pour tester l’éditeur universel, vous devez :

1. [Mettez à jour et configurez votre instance de création AEM.](#update-configure-aem)
1. [Configurez un service Universal Editor local.](#set-up-ue)
1. [Ajustez votre Dispatcher pour autoriser le service Universal Editor.](#update-dispatcher)

Une fois la configuration terminée, vous pouvez [instrumenter vos applications pour utiliser l’éditeur universel.](#instrumentation)

### Mettre à jour les AEM {#update-aem}

Le Service Pack 21 ou 22 et un Feature Pack pour AEM sont nécessaires pour utiliser l’éditeur universel avec AEM 6.5.

#### Appliquer le dernier Service Pack {#latest}

Assurez-vous que vous exécutez au moins le Service Pack 21 ou 22 pour AEM 6.5. Vous pouvez télécharger le dernier Service Pack à partir de [Distribution logicielle.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=fr)

#### Installation du Feature Pack de l’éditeur universel {#feature-pack}

Installez le **package de fonctionnalités Universal Editor pour AEM 6.5** [ disponible sur Distribution logicielle.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)

Si vous exécutez déjà le Service Pack 23 ou supérieur, le Feature Pack n’est pas nécessaire.

### Configuration des services {#configure-services}

Le Feature Pack installe un certain nombre de nouveaux packages pour lesquels une configuration supplémentaire est nécessaire.

#### Définissez l’attribut SameSite pour le cookie `login-token`. {#samesite-attribute}

1. Ouvrez Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez **Adobe Granite Token Authentication Handler** dans la liste et cliquez sur **Changer les valeurs de configuration**.
1. Dans la boîte de dialogue, remplacez l’attribut **SameSite pour le cookie de jeton de connexion** (`token.samesite.cookie.attr`) par `Partitioned`.
1. Cliquez sur **Enregistrer**.

#### Supprimez l’option X-Frame des en-têtes `SAMEORIGIN`. {#sameorigin}

1. Ouvrez Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez **Apache Sling Main Servlet** dans la liste et cliquez sur **Modifier les valeurs de configuration**.
1. Supprimez la valeur `X-Frame-Options=SAMEORIGIN` de l’attribut **En-têtes de réponse supplémentaires** (`sling.additional.response.headers`) s’il existe.
1. Cliquez sur **Enregistrer**.

#### Configurez le gestionnaire d’authentification des paramètres de requête Granite Adobe. {#query-parameter}

1. Ouvrez Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Localisez **Adobe Granite Query Parameter Authentication Handler** dans la liste et cliquez sur **Modifier les valeurs de configuration**.
1. Dans le champ **Path** (`path`), ajoutez `/` pour activer.
   * Une valeur vide désactive le gestionnaire d’authentification.
1. Cliquez sur **Enregistrer**.

#### Définissez pour quels chemins de contenu ou `sling:resourceTypes` l’éditeur universel doit être ouvert. {#paths}

1. Ouvrez Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Recherchez **Universal Editor URL Service** dans la liste et cliquez sur **Modifier les valeurs de configuration**.
1. Définissez pour quels chemins de contenu ou `sling:resourceTypes` l’éditeur universel doit être ouvert.
   * Dans le champ **Universal Editor Opening Mapping** , indiquez les chemins d’accès pour lesquels Universal Editor est ouvert.
   * Dans le champ **Sling:resourceTypes qui doit être ouvert par Universal Editor**, fournissez une liste des ressources qui sont ouvertes directement par Universal Editor.
1. Cliquez sur **Enregistrer**.

AEM ouvrira l’éditeur universel pour les pages basées sur cette configuration.

1. AEM vérifiera les mappages sous `Universal Editor Opening Mapping` et si le contenu se trouve sous les chemins d’accès qui y sont définis, l’éditeur universel est ouvert pour celui-ci.
1. Pour le contenu qui ne se trouve pas sous les chemins définis dans `Universal Editor Opening Mapping`, AEM vérifie si le `resourceType` du contenu correspond à ceux définis dans **Sling:resourceTypes qui doit être ouvert par Universal Editor** et si le contenu correspond à l’un de ces types, l’éditeur universel est ouvert pour le contenu à l’emplacement `${author}${path}.html`.
1. Sinon, AEM ouvre l’éditeur de page.

Les variables suivantes sont disponibles pour définir vos mappages sous `Universal Editor Opening Mapping`.

* `path` : chemin d’accès à la ressource à ouvrir
* `localhost` : entrée de l’externaliseur pour `localhost` sans schéma, par exemple `localhost:4502`
* `author` : entrée de l’externaliseur pour l’auteur sans schéma, par exemple `localhost:4502`
* `publish` : entrée Externalizer pour publication sans schéma, par exemple `localhost:4503`
* `preview` : entrée de l’externaliseur pour la prévisualisation sans schéma, par exemple `localhost:4504`
* `env` : `prod`, `stage`, `dev` en fonction des modes d’exécution Sling définis
* `token` : jeton de requête requis pour le `QueryTokenAuthenticationHandler`

Exemples de mappages :

* Ouvrez toutes les pages sous `/content/foo` sur l’auteur AEM :
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Cela entraîne l’ouverture de `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Ouvrez toutes les pages sous `/content/bar` sur un serveur NextJS distant, en fournissant toutes les variables comme informations.
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Cela entraîne l’ouverture de `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configuration du service d’éditeur universel {#set-up-ue}

Une fois AEM mis à jour et configuré, vous pouvez configurer un service d’éditeur universel local pour votre propre développement et test local.

1. Installez la version de Node.js >=20.
1. Téléchargez et décompressez le dernier service Universal Editor à partir de [Distribution logicielle](https://experienceleague.adobe.com/r/docs/experience-cloud/software-distribution/home).
1. Configurez le service d’éditeur universel via des variables d’environnement ou un fichier `.env`.
   * [Pour plus d’informations, consultez la documentation d’AEM as a Cloud Service Universal Editor.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Notez que vous devrez peut-être utiliser l’option `UES_MAPPING` si une réécriture IP interne est requise.
1. Exécutez `universal-editor-service.cjs`.

### Mise à jour de Dispatcher {#update-dispatcher}

Une fois AEM configuré et qu’un service Universal Editor local est en cours d’exécution, vous devez autoriser un proxy inverse pour le nouveau service [ dans le Dispatcher.](https://experienceleague.adobe.com/fr/docs/experience-manager-dispatcher/using/dispatcher)

1. Ajustez le fichier vhost de l’instance d’auteur pour inclure un proxy inverse.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 est le port par défaut. Si vous l&#39;avez modifié à l&#39;aide du paramètre `UES_PORT` de [ votre fichier `.env`, ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) vous devez ajuster la valeur du port ici en conséquence.

1. Redémarrez Apache.

## Instrument de votre application {#instrumentation}

Une fois AEM mise à jour et qu’un service d’éditeur universel local est en cours d’exécution, vous pouvez commencer à modifier du contenu sans affichage à l’aide d’Universal Editor.

Toutefois, votre application doit être instrumentée pour tirer parti de l’éditeur universel. Cela implique d’inclure des balises META pour indiquer à l’éditeur comment et où conserver le contenu. Vous trouverez des détails sur cette instrumentation dans la [documentation Universal Editor pour AEM as a Cloud Service.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Notez que lorsque vous suivez la documentation d’Universal Editor avec AEM as a Cloud Service, les modifications suivantes s’appliquent lorsque vous l’utilisez avec AEM 6.5.

* Le protocole de la balise meta doit être `aem65` au lieu de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* Le point de terminaison du service d’éditeur universel doit être annoncé via une balise meta .

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Dans la section `plugins` de la définition des composants, `aem65` doit être utilisé à la place de `aem`.

>[!TIP]
>
>Pour obtenir un guide complet à l’intention des développeurs pour leur prise en main d’Universal Editor, consultez le document [Présentation d’Universal Editor pour AEM Developers](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) dans la documentation d’AEM as a Cloud Service, tout en gardant à l’esprit les modifications nécessaires à la prise en charge d’AEM 6.5, comme indiqué dans cette section.
