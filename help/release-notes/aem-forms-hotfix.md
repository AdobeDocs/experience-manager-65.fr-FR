---
title: Correctif pour AEM Form Service Pack
description: Fournit des informations sur la manière de télécharger et d’installer le correctif pour AEM Forms Service Pack.
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 17%

---


# Correctifs Adobe Experience Manager{#aem-form-hotfix}

Installation de la dernière version [AEM Service Pack](/help/release-notes/release-notes.md) Il est recommandé d’inclure les correctifs et améliorations relatifs à la sécurité, aux performances, à la stabilité et aux clients clés publiés depuis la mise à disposition de Adobe Experience Manager 6.5.

## Correctifs pour les Forms adaptatives {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Date</strong></td>
    <td><strong>Noms des correctifs</strong></td>
    <td><strong>Correctifs</strong></td>
   </tr>
   <tr>
    <td>20 novembre 2023</td>
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

## Téléchargement et installation du correctif {#download-install-hotfix}

Effectuez les étapes suivantes pour télécharger et installer le correctif :

1. Télécharger [Correctif](#hotfix-for-adaptive-forms) à partir du lien du SDK.
1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de lot (.jar).
1. Chargez et installez le package (.zip) via le gestionnaire de packages.
1. Ouvrez les lots Configuration Manager `https://server:host/system/console/bundles`, chargez et installez le lot (.jar).
