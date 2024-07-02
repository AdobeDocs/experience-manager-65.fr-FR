---
title: Choisir un type de persistance pour l’installation d’AEM Forms
description: Choisissez judicieusement le type de persistance. Il vous aide à créer un environnement AEM Forms efficace et évolutif.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '372'
ht-degree: 100%

---

# Choisir un type de persistance pour l’installation d’AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Choisissez judicieusement le type de persistance. Il vous aide à créer un environnement AEM Forms efficace et évolutif.

La persistance est la méthode de stockage du contenu dans les stockages physiques. Elle définit la structure réelle des données et le mécanisme de stockage des données. Les MicroKernels agissent comme des gestionnaires de persistance dans AEM Forms. AEM Forms prend en charge la persistance (MicroKernals) de type TarMK, MongoMK et RDBMK. Vous pouvez choisir le type de persistance pour AEM Forms en fonction de l’objectif et du type de déploiement (serveur unique, batterie ou cluster) de l’instance AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utilise le format de persistance TarPM pour stocker du contenu.

Le tableau suivant répertorie tous les types de persistance pris en charge avec divers paramètres afin de vous aider à choisir un type de persistance pour votre environnement :

<table>
 <tbody>
  <tr>
   <th><strong>Type/coût d’installation</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMK</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuration autonome</strong></th>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <th><strong>Configuration du cluster</strong></th>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <th><strong>Coût de la licence</strong></th>
   <td>Inclus avec AEM </td>
   <td>Licence distincte requise</td>
   <td>Licence distincte requise</td>
  </tr>
 </tbody>
</table>

TarMK est conçu pour les performances, tandis que MongoMK et RDBMK sont conçus pour l’évolutivité. Adobe recommande vivement d’utiliser TarMK comme technologie de persistance par défaut pour tous les scénarios de déploiement AEM Forms, pour les instances de création et de publication, sauf dans les cas d’utilisation décrits dans la section [Choisir Mongo ou un micronoyau de base de données relationnelle plutôt que TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Pour obtenir la liste des micronoyaux pris en charge, consultez les articles [Exigences techniques d’AEM Forms sur OSGi](/help/sites-deploying/technical-requirements.md) et [Combinaisons de plateformes prises en charge par AEM Forms sur JEE](/help/forms/using/aem-forms-jee-supported-platforms.md).

## Choisir Mongo ou un micronoyau de base de données relationnelle plutôt que TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un environnement AEM Forms évolutif (organisé en clusters) est un ensemble de deux instances de création actives ou plus, configurées horizontalement. Vous pouvez choisir d’exécuter plusieurs instances de création si un seul serveur prenant en charge toutes les activités de création simultanées n’est plus durable.

Seuls les types de persistance MongoMK et RDBMK sont pris en charge pour un environnement AEM Forms sur JEE évolutif (organisé en clusters). Le nombre de serveurs ou la taille de l’environnement évolutif varie pour chaque installation. Pour obtenir une liste des considérations et des exemples, consultez les articles [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md) et [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). Vous pouvez également contacter l’assistance AEM Forms pour obtenir des informations détaillées sur la planification de la capacité d’AEM Forms avec RDBMK et TarMK.
