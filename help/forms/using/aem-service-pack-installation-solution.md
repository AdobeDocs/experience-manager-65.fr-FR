---
title: CRX/bundle et service de page de démarrage indisponibles une fois le dernier Service Pack 6.5.15.0 installé
description: CRX/bundle et service de page de démarrage indisponibles une fois le dernier Service Pack 6.5.15.0 installé
source-git-commit: 813d8ffc53dc1928674367c9568b6269642cecb7
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 16%

---


# Erreurs du service indisponibles après l’installation du Service Pack AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problème {#issue}

Après l’installation du [Service Pack d’AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), l’erreur se produit comme suit :
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException : Impossible de résoudre org.apache.sling.scripting.console

Après avoir installé AEM service pack 6.5.15.0, le lot CRX/et la page de démarrage affichent les erreurs non disponibles du service.

## Application {#applies-to}

Cette solution s’applique à :
* AEM Forms sur tous les serveurs JEE, à l’exception de ceux qui s’exécutent sur JBoss EAP 7.4.0

## Solution {#solution}

>[!NOTE]
>
>Les étapes de dépannage s’appliquent à tous les serveurs d’applications, à l’exception de JBoss EAP 7.4.

Après installation [Service Pack d’AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), si le lot CRX/et le service d’affichage de la page de début ne sont pas disponibles, effectuez les étapes suivantes :

1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Recherchez la variable `bundle.info` fichier .
1. Ouvrez le `bundle.info` dans l’éditeur de texte de fourmis et recherchez le nom du lot sous la forme `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Au cas où la variable `bundle.info` under `bundle52` ne contient pas le paramètre `org.apache.felix.http.bridge` du lot, vérifiez le numéro du lot entre crochets en regard de l’objet `org.apache.felix.http.bridge`. Accédez ensuite à [racine aem-forms]\crx-repository\launchpad\felix\bundle[x] et effectuez les étapes suivantes à cet emplacement.

1. Accéder à l’URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Rechercher `bundle.jar` et renommez `bundle.jar` to `bundle.jar.bak`.
1. Copier `bundle.jar` à cet emplacement à partir du [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Démarrez le serveur d’applications, attendez que les journaux se stabilisent et vérifiez l’état du lot.
1. Une fois que tous les lots sont à l’état activé, installez le `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` fragment de servlet à partir de `system/console/bundles` téléchargé depuis [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) et attendez que le serveur d’applications se stabilise.
1. Arrêtez le serveur d’applications.
1. Accédez à `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` et supprimez la variable `bundle.jar`.
1. Renommez la variable `bundle.jar.bak` au `bundle.jar`.
1. Démarrez le serveur d’applications.