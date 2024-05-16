---
title: Correctifs pour AEM Forms
description: Fournit des informations sur la manière de télécharger et d’installer un correctif pour AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 5e2799505bc6d69cd5898445a9300ad162ef74fd
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 86%

---

# Correctifs Adobe Experience Manager Forms{#aem-form-hotfix}

Cet article répertorie les correctifs critiques mis en œuvre pour résoudre les problèmes connus, améliorer la stabilité du système et optimiser les performances globales d’AEM Forms.

>[!NOTE]
>
> Les correctifs sont conçus pour être cumulatifs, c’est-à-dire qu’ils englobent tous les correctifs précédents. Ainsi, lorsque vous appliquez le dernier correctif à une version, il résout non seulement le problème le plus récent, mais incorpore également tous les correctifs et améliorations antérieurs.

## Correctifs pour les formulaires adaptatifs {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Date</strong></td>
    <td><strong>Lien de téléchargement des correctifs (lien de distribution logicielle AEM)</strong></td>
    <td><strong>Problèmes résolus</strong></td>
  </tr>
  <tr>
    <td>vendredi 16 mai 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Correctif pour le pack de services 6.5.20.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Correctif pour AEM Service Pack 6.5.20.0 pour Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Correctif pour AEM Service Pack 6.5.20.0 pour Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Dans un formulaire adaptatif basé sur un XDP avec des scripts intégrés sur des cases à cocher, les scripts ne sont pas exécutés pour les éléments après ces cases à cocher. Un correctif est disponible pour ce problème. (FORMS-14244) </li>
     <li> Les lignes du widget du sélecteur de date sont tronquées lors du parcours de plusieurs mois dans le widget de pop-up pour les champs suivant le modèle d’édition/d’affichage. Un correctif est disponible pour ce problème. (FORMS-13620) </li>
     <li>Les envois de formulaire échouent lors de la tentative d’utilisation du service DOR (Document d’enregistrement) dans le serveur principal. Le message d’erreur rencontré est : « L’action Envoyer n’a pas pu se terminer, car la ressource de formulaire n’a pas été correctement affectée. » (FORMS-13798) </li>
     <li>Lorsqu’un formulaire adaptatif est envoyé d’une instance de publication Adobe Experience Manager à un processus Adobe Experience Manager, le processus ne parvient pas à enregistrer les pièces jointes.  (FORMS-14209) </li>
     <li> Lors de l’installation du package Forms Service Pack 20 d’AEM 6.5 (package de module complémentaire AEM Forms pour SP20), l’interface utilisateur d’AEM Sites présente une dégradation significative des performances.  (FORMS-13791) </li>
     <li>Le service de préremplissage échoue avec une exception de pointeur nulle dans les communications interactives. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 janvier 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Correctif pour le pack de services 6.5.19.0 d’AEM pour le serveur Windows on JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Dans AEM Forms sur le serveur JEE, le rendu des formulaires HTML5 qui utilisent le chemin d’accès au contexte échoue. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 janvier 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Le rendu du composant Signature tactile prêt à l’emploi échoue pour un aperçu dans un formulaire adaptatif. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>mardi 20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Lorsqu’une URL de redirection est définie dans le conteneur de guide d’un formulaire adaptatif, la signature intégrée cesse de fonctionner. (FORMS-10493)</li>
    <li>Les modèles de document d’enregistrement (DoR) ne se publient pas pour les formulaires adaptatifs localisés. (FORMS-10535)</li>
    <li>La communication interactive avec les images intégrées volumineuses ne s’ouvre pas en mode d’édition. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Télécharger et installer un correctif {#download-install-hotfix}

Effectuez les étapes suivantes pour télécharger et installer le correctif :

1. Téléchargez le [correctif](#hotfix-for-adaptive-forms) à partir du lien Distribution logicielle.
1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de lot (.jar).
1. Chargez et installez le package (.zip) via le [gestionnaire de packages](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=fr#accessing).
1. Ouvrez les lots Configuration Manager `https://server:host/system/console/bundles`, chargez et installez le lot (.jar). Le correctif est installé.
