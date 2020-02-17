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
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# Définitions des véhicules de version d’AEM Update{#update-release-vehicle-definitions}

Ce document contient des informations à propos des différents types de versions d’Adobe Experience Manager, dont les versions intégrales, les packs de fonctionnalités et les Service Packs mis par Adobe à la disposition des clients.

>[!Nnote]
>
>Pour connaître le calendrier des versions des mises à jour d’AEM, reportez-vous à la feuille de route des versions des mises à jour [AEM.](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

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
     <li>Les numéros de version pour les versions majeures augmentent selon la formule X+1.Y.Z. </li>
     <li>Les numéros de version pour les versions mineures augmentent selon la formule X.Y+1.Z</li>
    </ul> <p>Où X est le numéro de version principal, Y est le numéro de version secondaire et Z le numéro de correctif.</p> </td>
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
     <li>Les notes de mise à jour sont disponibles sur le portail de documentation</li>
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
     <li>Distribué en tant que programme d’installation autonome du produit</li>
     <li>Disponible sur le site Web de gestion des licences et sur le site Web de gestion des licences</li>
     <li>Peut nécessiter une migration du référentiel de contenu</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Totalement validée par AQ</td>
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
     <li>Actuellement, il est impossible de revenir en arrière</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>
    <ul>
     <li>Le numéro de version du correctif est un nombre à un chiffre</li>
     <li>Après l'installation, augmentera le chiffre du correctif du numéro de version installé, en fonction de la formule X.Y.Z.SPx</li>
     <li>Où X est le numéro de version principal, Y est le numéro de version secondaire et Z le numéro de correctif. x est le numéro du Service Pack. </li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>
    <ul>
     <li>Nouvelles fonctionnalités</li>
     <li>Améliorations</li>
     <li>Correctifs</li>
     <li>Service Pack intérêt commun (le cas échéant)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>
    <ul>
     <li>Notes de mise à jour disponibles sur le portail de documentation</li>
     <li>Documentation sur les fonctionnalités, améliorations et correctifs du portail de documentation</li>
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
     <li>Tous les correctifs ont été validés</li>
     <li>Analyse générale des packages avec les exécutions d’automatisation</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pack de correctifs cumulés {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Modèle de remise unique des correctifs</li>
     <li>Package de contenu agrégateur contenant le package de contenu de composants individuels</li>
     <li>Les CFP sont un survol des correctifs et aucune amélioration n'en fait partie.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Où X est le numéro de version principal, Y est le numéro de version secondaire et Z le numéro de correctif. x est le numéro cumulé du Service Pack. </p> </td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td><p>Le CFP est un pack de correctifs cumulatif contenant des correctifs de tous les composants au cours de dates spécifiées. Par exemple, si un client applique CFP3, alors CFP3 = CFP1 + CFP2. </p> </td>
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
     <li>Selon le dernier Service Pack publié</li>
     <li>Le CFP est indépendant. Les clients n’ont pas à se soucier de trouver/résoudre des problèmes de dépendances. Le pack de correctifs cumulatif doit être installé sur le dernier Service Pack publié.</li>
     <li>Le CFP peut être installé sous la forme d’un package unique, ce qui améliore l’expérience client.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Contrôle qualité validé au niveau de l’intégration et test de régression</td>
  </tr>
 </tbody>
</table>

## Pack de correctifs cumulatif Oak {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td>
    <ul>
     <li>Semblable à un CFP standard, mais ne contient que des correctifs liés à Oak</li>
     <li>La COFP est autonome (sans dépendances). Les clients n’ont pas à se soucier de trouver/résoudre des problèmes de dépendances. [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>oak &lt;version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>COFP est un pack de correctifs cumulatif contenant les correctifs de tous les composants Oak pour une version 1.x spécifique. Par exemple, si le client applique le pack de correctifs cumulatif Oak (COHF) 1.x.3, alors COHF 1.x.3. = COHF + 1.x.1 COHF 1.x.2. </td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td><p>Si nécessaire</p> </td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Le processus d’installation COFP a été simplifié pour améliorer l’expérience client. (Les clients peuvent se contenter d’installer un module unique pour tous les composants). </li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td><p>Contrôle qualité validé</p> </td>
  </tr>
 </tbody>
</table>

## Correctif {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>Définition</strong></td>
   <td><p>Package comprenant un ou plusieurs fichiers créés pour résoudre un défaut de produit qui dégrade de manière significative les services essentiels ou affecte de manière significative les opérations commerciales. </p> </td>
  </tr>
  <tr>
   <td><strong>Dénomination</strong></td>
   <td>cq-&lt;Version de publication&gt;-hotfix-&lt;ID du correctif&gt;-&lt;version du correctif&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>Inclut des correctifs pour un problème spécifique</td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>Les notes de mise à jour des correctifs publics ne sont disponibles que sur la base de la demande du client via le portail d’assistance AEM.</td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Si nécessaire</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Livré sous la forme d’un module.</li>
     <li>Disponible sur Package Share</li>
     <li>Selon le dernier Service Pack publié</li>
     <li>La plupart des correctifs sont autonomes, sauf indication contraire. Peut être installé dans n’importe quel ordre. Peut être vérifié par le biais de l’onglet Détails Package Share de l’élément des dépendances.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>
    <ul>
     <li>Validée par le service à la clientèle</li>
     <li>Les correctifs AEM ne bénéficient pas du même niveau d’assurance qualité que les Service Packs ou les versions de produits. Par conséquent, ils doivent d’abord être validés sur un environnement intermédiaire dans le cadre des processus de déploiement de qualité. </li>
    </ul> </td>
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
   <td>overlay-&lt;ID du ticket&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusions</strong></td>
   <td>Correction de bogues pour un fichier JS ou JSP</td>
  </tr>
  <tr>
   <td><strong>Documentation</strong></td>
   <td>Aucun</td>
  </tr>
  <tr>
   <td><strong>Fréquence</strong></td>
   <td>Si nécessaire</td>
  </tr>
  <tr>
   <td><strong>Disponibilité et installation</strong></td>
   <td>
    <ul>
     <li>Fourni en tant que package par le service à la clientèle AEM</li>
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
     <li>Fourni via des Service Packs</li>
     <li>Disponible sur Package Share. Les clients acceptent les conditions générales d’Adobe par le biais du partage de packages.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Niveau de test</strong></td>
   <td>Les packs de fonctionnalités (feature packs) de disponibilité générale (GA) sont validés par le contrôle qualité.</td>
  </tr>
 </tbody>
</table>

* [1]: Les correctifs OAK ne sont pas fournis en tant que correctifs individuels. Toutefois, ils sont inclus dans le correctif cumulatif OAK. Si nécessaire, un diagnostic intégré avec le dernier pack de correctifs cumulatif Oak peut être mis à votre disposition. Condition préalable : le client possède le dernier pack de correctifs cumulatif Oak. Les diagnostics intégrés fournissent le même niveau d’assurance qualité qu’un correctif. Par conséquent, ils ne proposent pas le même niveau d’assurance qualité qu’un pack de correctifs cumulatif, un Service Pack ou une version de produit. Le correctif final est livré avec le prochain CFP.

