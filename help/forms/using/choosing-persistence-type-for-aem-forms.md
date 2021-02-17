---
title: Choix d’un type de persistance pour l’installation d’AEM Forms
seo-title: Choix d’un type de persistance pour l’installation d’AEM Forms
description: Choisissez un type de persistance avec soin. Il vous aide à créer un environnement AEM Forms efficace et évolutif.
seo-description: Choisissez un type de persistance avec soin. Il vous aide à créer un environnement AEM Forms efficace et évolutif.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 94%

---


# Choix d’un type de persistance pour l’installation d’AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Choisissez un type de persistance avec soin. Il vous aide à créer un environnement AEM Forms efficace et évolutif.

La persistance est la méthode de stockage du contenu sur les stockages physiques. Elle définit le mécanisme réel de structure et de stockage des données. Les MicroKernals agissent comme des gestionnaires de persistance dans AEM Forms. AEM Forms prend en charge la persistance (MicroKernals) de type TarMK, MongoMK et RDBMK. Vous pouvez sélectionner un type de persistance pour AEM Forms selon l’objectif et le type de déploiement (serveur unique, batterie ou grappe) d’une instance d’AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utilise le format de persistance TarPM pour stocker du contenu.

Le tableau suivant liste tous les types de persistance pris en charge avec divers paramètres afin de vous aider à choisir un type de persistance pour votre environnement :

<table>
 <tbody>
  <tr>
   <th><strong>Type/coût d’installation</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuration autonome</strong></th>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <th><strong>Configuration en grappe</strong></th>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <th><strong>Coût de la licence</strong></th>
   <td>Inclus avec AEM </td>
   <td>Licence distincte obligatoire</td>
   <td>Licence distincte obligatoire</td>
  </tr>
 </tbody>
</table>

TarMK est conçu pour les performances, tandis que MongoMK et RDBMK sont conçus pour l’évolutivité. Adobe recommande vivement TarMK en tant que technologie de persistance par défaut pour tous les scénarios de déploiement AEM Forms, pour les instances d’auteur et de publication, sauf dans les cas d’utilisation décrits dans la section [Mongo ou Microkernel de base de données relationnelle versus TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Pour obtenir la liste des Microkernels pris en charge, voir [Exigences techniques d’AEM Forms on OSGi](/help/sites-deploying/technical-requirements.md) ou [Combinaisons de plates-formes prises en charge AEM Forms on JEE](/help/forms/using/aem-forms-jee-supported-platforms.md).

## Mongo ou Microkernel de base de données relationnelle versus TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un environnement AEM Forms (en grappes) évolutif est un ensemble de deux instances d’auteur actives ou plus, configurées horizontalement. Vous pouvez choisir d’exécuter plus d’une instance d’auteur si un seul serveur prenant en charge toutes les activités de création simultanées n’est plus fiable.

Seuls les types de persistance MongoMK et RDBMK sont pris en charge pour AEM Forms (en grappe) évolutif sur un environnement JEE. Le nombre de serveurs ou la taille de l’environnement extensible varie pour chaque installation. Pour obtenir la liste des remarques et d’exemples, voir [Déploiement recommandés](/help/sites-deploying/recommended-deploys.md) et ou [Topologies d’architecture et de déploiement pour AEM Forms. ](/help/forms/using/aem-forms-architecture-deployment.md) Vous pouvez également contacter l’assistance AEM Forms pour plus d’informations sur la planification de capacité pour AEM Forms avec RDBMK et TarMK.
