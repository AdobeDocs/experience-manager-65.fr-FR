---
title: Erreurs de service indisponible pour CRX/bundle et page de démarrage une fois le dernier pack de services 6.5.15.0 installé
description: Erreurs de service indisponible pour CRX/bundle et page de démarrage une fois le dernier pack de services 6.5.15.0 installé
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 100%

---

# Erreur de service indisponible après l’installation du pack de services AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problème {#issue}

Après l’installation du [pack de services d’AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’erreur se produit comme suit :
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Unable to resolve org.apache.sling.scripting.console

Après avoir installé le pack de services AEM 6.5.15.0 le CRX/bundle et la page de démarrage affichent les erreurs de service indisponible.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :
* AEM Forms sur tous les serveurs JEE, à l’exception de ceux qui s’exécutent sur JBoss EAP 7.4.0

## Solution {#solution}

>[!NOTE]
>
>Les étapes de résolution de problèmes s’appliquent à tous les serveurs d’applications, à l’exception de JBoss EAP 7.4.

Après l’installation du [pack de services AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si le CRX/bundle et la page de démarrage affichent des erreurs de service indisponible, effectuez les étapes suivantes :

1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Recherchez le fichier `bundle.info`.
1. Ouvrez le fichier `bundle.info` dans un éditeur de texte et recherchez le nom du bundle sous la forme `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Au cas où `bundle.info` sous `bundle52` ne contient pas le lot `org.apache.felix.http.bridge`, vérifiez le numéro du lot entre crochets en regard de `org.apache.felix.http.bridge`. Accédez ensuite à [racine aem-forms]\crx-repository\launchpad\felix\bundle[x] et effectuez les étapes suivantes à cet emplacement.

1. Accéder à l’URL : `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Recherchez `bundle.jar` et renommez le `bundle.jar` en `bundle.jar.bak`.
1. Copiez le `Bundle for AEM 6.5 Forms on JEE Service Pack 15` à cet emplacement à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Démarrez le serveur d’applications, attendez que les journaux se stabilisent et vérifiez l’état du lot.
1. Une fois que l’état de tous les bundles est actif, installez le [fragment pour le pack de services 15 AEM 6.5 Forms on JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) à partir de `system/console/bundles` et attendez que le serveur d’applications se stabilise.
1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` et supprimez le `bundle.jar`.
1. Renommez le `bundle.jar.bak` en `bundle.jar`.
1. Démarrez le serveur d’applications.
