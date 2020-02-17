---
title: Essentials des affectations
seo-title: Essentials des affectations
description: Présentation de la fonctionnalité Affectations pour les communautés d’activation
seo-description: Présentation de la fonctionnalité Affectations pour les communautés d’activation
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Essentials des affectations{#assignments-essentials}

Lisez ce qui suit pour en savoir plus sur les informations essentielles pour travailler avec les fonctions d&#39;affectation des sites de la communauté [d&#39;](/help/communities/overview.md#enablement-community) activation.

La fonction des affectations permet d’affecter des ressources d’activation et des chemins d’apprentissage aux membres des communautés d’activation.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activation/composants/hbs/myassign</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassign<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learnpath</td>
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
   <td>voir <a href="/help/communities/assignments.md">Fonction des affectations</a></td>
  </tr>
 </tbody>
</table>

### État d’achèvement et de réussite {#completion-and-success-status}

Les états d’achèvement et de réussite sont utilisés dans les rapports et les bannières d’état sur les affectations.

État d’achèvement :

* Non attribué
* Non démarré (nouveau)
* En cours
* Terminer

État de réussite:

* Inconnu
* Réussite
* Échec

Les seules combinaisons possibles d’achèvement et d’état de réussite sont :

| **Fin** | **Réussite** |
|---|---|
| Non démarré | Inconnu |
| En cours | Inconnu |
| Terminer | Réussite |
| Terminer | Échec |

## Essentials for Server-Side {#essentials-for-server-side}

### Fonction Affectations {#assignments-function}

Une structure de site de la communauté qui inclut la fonction [](/help/communities/functions.md#assignments-function)Affectations, inclut un ` [assignments](/help/communities/assignments.md)` composant configuré.

### API de référence {#reference-apis}

* [API d&#39;activation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de création de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API Analytics de création de rapports](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

