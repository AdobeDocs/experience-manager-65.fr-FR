---
title: Notions fondamentales sur les affectations
seo-title: Assignments Essentials
description: Présentation de la fonction Affectations pour les communautés d’activation
seo-description: Assignments feature overview for enablement communities
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 13%

---

# Notions fondamentales sur les affectations {#assignments-essentials}

Lisez la suite pour en savoir plus sur les informations essentielles à l’utilisation de la fonction d’affectation de [communauté d&#39;activation](/help/communities/overview.md#enablement-community) sites.

La fonction Affectations permet d’affecter des ressources d’activation et des parcours d’apprentissage aux membres des communautés d’activation.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="/help/communities/assignments.md">Fonctionnalité Affectations</a></td>
  </tr>
 </tbody>
</table>

### État d’achèvement et de réussite {#completion-and-success-status}

Les états de fin et de réussite sont utilisés dans les rapports et les bannières d’état sur les affectations.

État d’achèvement :

* Non attribué
* Non démarré (nouveau)
* En cours
* Terminé

État de réussite:

* Inconnu
* Réussite
* Échec

Les seules combinaisons possibles d’achèvement et d’état de réussite sont les suivantes :

| **Fin** | **Réussite** |
|---|---|
| Non démarré | Inconnu |
| En cours | Inconnu |
| Terminé | Réussite |
| Terminé | Échec |

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

### Fonction Affectations {#assignments-function}

Une structure de site de communauté qui inclut [Fonction Affectations](/help/communities/functions.md#assignments-function), inclut une ` [assignments](/help/communities/assignments.md)` composant.

### API de référence {#reference-apis}

* [API d’activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de création de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
