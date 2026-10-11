---
title: Erreurs de service indisponible pour CRX/bundle et page de démarrage une fois le dernier pack de services 6.5.15.0 installé
description: Erreurs de service indisponible pour CRX/bundle et page de démarrage une fois le dernier pack de services 6.5.15.0 installé
SEO Description: Trouble shooting steps to resolve the errors after installing latest 6.5.15.0 service pack
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 76%
---
# Erreur de service indisponible après l’installation du pack de services AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problème {#issue}

Après l’installation du pack de services [AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’erreur se produit comme suit :
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Unable to resolve org.apache.sling.scripting.console

Après l’installation du pack de services AEM 6.5.15.0, le CRX/bundle et la page de démarrage affichent les erreurs de service indisponible.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :
* AEM Forms sur tous les serveurs JEE, à l’exception de ceux qui s’exécutent sur JBoss EAP 7.4.0

## Solution {#solution}

>[!NOTE]
>
>Les étapes de résolution de problèmes s’appliquent à tous les serveurs d’applications, à l’exception de JBoss EAP 7.4.

Après l’installation du pack de services AEM 6.5.15.0 [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si le CRX/bundle et la page de démarrage affichent des erreurs de service indisponible, procédez comme suit :

1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Recherchez le fichier `bundle.info`.
1. Ouvrez le fichier `bundle.info` dans un éditeur de texte et recherchez le nom du bundle sous la forme `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Si `bundle.info` sous `bundle52` ne contient pas le bundle `org.apache.felix.http.bridge`, vérifiez le numéro du bundle entre crochets en regard de `org.apache.felix.http.bridge`. Accédez ensuite à [racine aem-forms]\crx-repository\launchpad\felix\bundle[x] et effectuez les étapes suivantes à cet emplacement.

1. Accéder à l’URL : `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Recherchez `bundle.jar` et renommez le `bundle.jar` en `bundle.jar.bak`.
1. Copiez le `Bundle for AEM 6.5 Forms on JEE Service Pack 15` à cet emplacement à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Démarrez le serveur d’applications, attendez que les journaux se stabilisent et vérifiez l’état du lot.
1. Une fois que l’état de tous les bundles est actif, installez le [fragment pour le pack de services 15 AEM 6.5 Forms on JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) à partir de `system/console/bundles` et attendez que le serveur d’applications se stabilise.
1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` et supprimez le `bundle.jar`.
1. Renommez le `bundle.jar.bak` en `bundle.jar`.
1. Démarrez le serveur d’applications.
