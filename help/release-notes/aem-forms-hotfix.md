---
title: Correctifs pour AEM Forms
description: Fournit des informations sur la manière de télécharger et d’installer un correctif pour AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 276b0122fb3d88c584dd6b2b4c2c6f6eda9d0537
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 14%

---

# Correctifs Adobe Experience Manager Forms{#aem-form-hotfix}

Cet article répertorie les correctifs critiques mis en oeuvre pour résoudre les problèmes connus, améliorer la stabilité du système et améliorer les performances globales d’AEM Forms.

## Correctifs pour les Forms adaptatives {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Date</strong></td>
    <td><strong>Lien de téléchargement de correctif (lien AEM de distribution logicielle)</strong></td>
    <td><strong>Problèmes résolus</strong></td>
   </tr>
   <tr>
    <td>mardi 20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Correctif pour AEM Service Pack 6.5.18.0 pour Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Correctif pour AEM Service Pack 6.5.18.0 pour Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Correctif pour AEM Service Pack 6.5.18.0 pour Mac OS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La signature en ligne cesse de fonctionner lorsqu’une URL de redirection est définie dans le conteneur de guide d’un formulaire adaptatif. (FORMS-10493)</li>
    <li>Les modèles de document d’enregistrement (DoR) ne parviennent pas à publier pour le Forms adaptatif localisé. (FORMS-10535)</li>
    <li>La communication interactive avec les images intégrées volumineuses ne s’ouvre pas en mode d’édition. (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## Télécharger et installer un correctif {#download-install-hotfix}

Effectuez les étapes suivantes pour télécharger et installer le correctif :

1. Télécharger [Correctif](#hotfix-for-adaptive-forms) à partir du lien Distribution logicielle .
1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de lot (.jar).
1. Téléchargez et installez le package (.zip) via le [Gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Ouverture des lots Configuration Manager `https://server:host/system/console/bundles`, téléchargez et installez le lot (.jar). Le correctif est installé.
