---
title: Mettre à jour les définitions de véhicule de version
seo-title: Mettre à jour les définitions de véhicule de version
description: Cet article décrit les différents types de publications AEM, y compris les versions, les Features Pack et les Service Packs.
seo-description: Cet article décrit les différents types de publications AEM, y compris les versions, les Features Pack et les Service Packs.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 50%

---


# aem mettre à jour les définitions des véhicules de version{#update-release-vehicle-definitions}

Ce document contient des informations à propos des différents types de versions d’Adobe Experience Manager, dont les versions intégrales, les packs de fonctionnalités et les Service Packs mis par Adobe à la disposition des clients.

>[!NOTE]
>
>Pour connaître le calendrier de publication des AEM mises à jour, reportez-vous à la feuille de route des mises à jour [AEM](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## Version intégrale {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Version planifiée</li>
     <li>Prend en charge les chemins de mise à niveau pour des versions spécifiques, définis dans les notes de mise à jour</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>
    <ul>
     <li>Les numéros de version pour les versions majeures augmentent en fonction de la formule X+1.Y.Z. </li>
     <li>Les numéros de version pour les versions mineures augmentent en fonction de la formule X.Y+1.Z</li>
    </ul> <p>Où X est le numéro de version Principal, Y est le numéro de version secondaire et Z le numéro de correctif.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>
    <ul>
     <li>Nouvelles fonctionnalités</li>
     <li>Améliorations</li>
     <li>Correctifs</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>
    <ul>
     <li>Les notes de mise à jour sont disponibles sur le portail de documentation.</li>
     <li>La documentation sur les fonctionnalités, les améliorations et les correctifs est disponible sur le portail de documentation.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Annuel</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré en tant que programme d’installation de produit autonome</li>
     <li>Disponible sur le site Web de gestion des licences et le site Web de gestion des licences Managed Services</li>
     <li>Peut nécessiter une migration du référentiel de contenu</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Entièrement validé par le contrôle qualité</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Version planifiée</li>
     <li>Actuellement, la restauration est impossible</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>
    <ul>
     <li>Le numéro de version du correctif est un numéro à un chiffre.</li>
     <li>Après l'installation, augmentera le chiffre de correctif du numéro de version installé, en fonction de la formule X.Y.Z.SPx</li>
     <li>Où X est le numéro de version Principal, Y est le numéro de version secondaire et Z le numéro de correctif. x est le numéro du Service Pack. </li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>
    <ul>
     <li>Nouvelles fonctionnalités</li>
     <li>Améliorations</li>
     <li>Correctifs</li>
     <li>Packs de fonctionnalités d’intérêt commun (le cas échéant)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>
    <ul>
     <li>Notes de mise à jour disponibles sur le portail de documentation</li>
     <li>Documentation sur les fonctionnalités, les améliorations et les correctifs de bogues sur le portail de documentation</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Trimestriel</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré sous la forme d’un module.</li>
     <li>Disponible sur Package Share</li>
     <li>Nécessite une installation fonctionnelle existante</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>
    <ul>
     <li>Tous les correctifs ont été validés par l’assurance qualité</li>
     <li>Fonctionnement général des packages avec les exécutions d’automatisation</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pack de correctifs cumulés {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Modèle diffusion unique de correctifs de publication</li>
     <li>Package de contenu agrégé contenant le package de contenu de composants individuels</li>
     <li>Les CFP remplacent les correctifs et aucune amélioration n’en fait partie.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Où X est le numéro de version Principal, Y est le numéro de version secondaire et Z le numéro de correctif. x est le numéro cumulé du Service Pack. </p> </td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td><p>CFP est un pack de correctifs cumulatif contenant des correctifs de tous les composants au cours de dates spécifiées. Par exemple, si un client applique CFP3, alors CFP3 = CFP1 + CFP2. </p> </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>Notes de mise à jour disponibles sur le portail de documentation</td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Quaterly</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré sous la forme d’un module.</li>
     <li>Disponible sur Package Share</li>
     <li>Dépendant du dernier Service Pack publié</li>
     <li>La PCP est indépendante. Les clients n’ont pas à se soucier de trouver/résoudre des problèmes de dépendances. Le pack de correctifs cumulatif doit être installé sur le dernier Service Pack publié.</li>
     <li>Le CFP peut être installé sous la forme d’un package unique, ce qui améliore l’expérience des clients.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Contrôle qualité validé au niveau de l’intégration et test de régression</td>
  </tr>
 </tbody>
</table>

## Incrustation {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>overlay-&lt;ID de ticket&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>Correction de bogues pour un fichier JS ou JSP</td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>Aucune</td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Si nécessaire</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré sous forme de package par AEM service à la clientèle</li>
     <li>Pas nécessairement inclus dans les Service Packs ou les versions complètes</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Validée par le service à la clientèle</td>
  </tr>
 </tbody>
</table>

## Feature Pack {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Les Feature Packs sont des fonctionnalités ajoutées et sont fournis par l’intermédiaire des Service Packs. Si une version AEM a publié son dernier Service Pack, Adobe ne fournira plus aucun Feature Pack pour elle à l’avenir.</li>
     <li>Les Feature Packs contiennent des améliorations de produit, prévues pour une version ultérieure du produit, mais diffusées rapidement en fonction de la décision des responsables des produits d’Adobe.</li>
     <li>Les fonctionnalités sont toujours fusionnées avec la prochaine publication majeure, puis rétroportées à la version d’AEM requise par le client.</li>
     <li>L’intérêt commun et les packs de fonctionnalités (feature packs) de disponibilité générale (GA) sont fusionnés dans le prochain Service Pack.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>cq-&lt;Version de publication&gt;-featurepack-&lt;ID du Feature Pack&gt;-&lt;Version du Feature Pack&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>
    <ul>
     <li>Nouvelles fonctionnalités</li>
     <li>Améliorations</li>
     <li>Correctifs de bogues (mises à niveau incrémentielles du produit)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>La documentation est disponible sur helpx.adobe.com.</td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Varie en fonction du domaine du produit.</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré par le biais de Service Packs</li>
     <li>Disponible sur Package Share. Les clients acceptent les termes et conditions de l’Adobe par le biais du partage de package.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Les packs de fonctionnalités (feature packs) de disponibilité générale (GA) sont validés par le contrôle qualité.</td>
  </tr>
 </tbody>
</table>

* [1]: Les correctifs OAK ne sont pas fournis en tant que correctifs logiciels. Toutefois, ils sont inclus dans le correctif cumulatif OAK. Si nécessaire, un diagnostic intégré avec le dernier pack de correctifs cumulatif Oak peut être mis à votre disposition. Condition préalable : le client possède le dernier pack de correctifs cumulatif Oak. Les diagnostics intégrés fournissent le même niveau d’assurance qualité qu’un correctif. Par conséquent, ils ne proposent pas le même niveau d’assurance qualité qu’un pack de correctifs cumulatif, un Service Pack ou une version de produit. Le correctif final est fourni avec le prochain CFP.

