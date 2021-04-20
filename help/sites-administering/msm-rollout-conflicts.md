---
title: Conflits de déploiement de MSM
seo-title: Conflits de déploiement de MSM
description: Découvrez comment gérer les conflits de déploiement avec le gestionnaire multisite.
seo-description: Découvrez comment gérer les conflits de déploiement avec le gestionnaire multisite.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 59%

---


# Conflits de déploiement dans MSM{#msm-rollout-conflicts}

Des conflits peuvent survenir si de nouvelles pages portant le même nom de page sont créées à la fois dans la branche du plan directeur et dans une branche de la copie dynamique dépendante.

Ces conflits doivent être gérés et résolus lors du déploiement.

## Gestion des conflits {#conflict-handling}

Lorsqu’il y a des pages en conflit (dans les branches Plan directeur et Live Copy), MSM permet de définir comment elles doivent être gérées (voire si elles doivent l’être).

Pour vous assurer que le déploiement n’est pas bloqué, les définitions possibles peuvent inclure :

* Page (Plan directeur et Live Copy) ayant la priorité lors du déploiement
* Pages renommées (et comment)
* Impact sur le contenu publié

    Le comportement par défaut d’AEM (version commerciale) est que le contenu publié n’est pas affecté. Ainsi, si une page créée manuellement dans la branche Live Copy a été publiée, ce contenu est toujours publié avec la gestion du conflit et le déploiement.

Outre les fonctionnalités standard, des gestionnaires de conflit personnalisés peuvent être ajoutés pour mettre en œuvre différentes règles. Elles peuvent également permettre des actions de publication sous forme de processus individuel.

### Exemple de scénario {#example-scenario}

Dans les sections suivantes, nous utilisons l’exemple d’une nouvelle page `b`, créée dans les branches Plan directeur et Live Copy (créée manuellement) pour illustrer les différentes méthodes de résolution des conflits :

* plan directeur : `/b`

   Un gabarit ; avec 1 page enfant, bp-level-1.

* copie en direct : `/b`

   Une page créée manuellement dans la branche de la copie dynamique ; avec une page enfant, `lc-level-1`.

   * Activé lors de la publication en tant que `/b`, avec la page enfant.

**Avant le déploiement**

<table>
 <tbody>
  <tr>
   <td><strong>avant le déploiement</strong></td>
   <td><strong>copie dynamique avant le déploiement</strong></td>
   <td><strong>publier avant le déploiement</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (créé dans la branche du plan directeur, prêt pour le déploiement)<br /> </td>
   <td><code>b</code> <br /> (créé manuellement dans une branche de copie dynamique)<br /> </td>
   <td><code>b</code> <br /> (contient le contenu de la page b créée manuellement dans la branche de la copie dynamique)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (créé manuellement dans une branche de copie dynamique)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contient le contenu de la page<br /> enfant-level-1 créée manuellement dans la branche de la copie dynamique)</td>
  </tr>
 </tbody>
</table>

## Gestionnaire de déploiement et gestion des conflits {#rollout-manager-and-conflict-handling}

Le gestionnaire de déploiement permet d’activer ou de désactiver la gestion des conflits.

À cet effet, à l’aide de la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) du **gestionnaire de déploiement WCM Day CQ** :

* **Gérer les conflits avec les pages** créées manuellement :

   ( `rolloutmgr.conflicthandling.enabled`)

   Définissez cette variable sur true si le gestionnaire de déploiement doit gérer les conflits provenant d&#39;une page créée dans la copie dynamique avec un nom présent dans le plan directeur.

AEM possède un [comportement prédéfini lorsque la gestion des conflits a été désactivée](#behavior-when-conflict-handling-deactivated).

## Gestionnaires de conflit {#conflict-handlers}

AEM utilise des gestionnaires de conflit pour résoudre des conflits de page qui émergent lors du déploiement du contenu du plan directeur vers la Live Copy. L’une des méthodes (habituelles) pour résoudre ce type de conflit est de renommer les pages. Plusieurs gestionnaires de conflit peuvent être opérationnels pour permettre de sélectionner différents comportements.

AEM comporte les éléments suivants :

* [Gestionnaire de conflits par défaut](#default-conflict-handler) :

   * `ResourceNameRolloutConflictHandler`

* Possibilité de mettre en œuvre un [gestionnaire personnalisé](#customized-handlers).
* Le mécanisme de classement des services qui permet de définir la priorité de chaque gestionnaire individuel. Le service qui possède la valeur la plus élevée est utilisé.

### Gestionnaire de conflits par défaut {#default-conflict-handler}

Le gestionnaire de conflits par défaut :

* Est appelé `ResourceNameRolloutConflictHandler`

* Avec ce gestionnaire, la page du plan directeur prévaut.
* Le classement des services pour ce gestionnaire est défini sur faible ( &quot;i.e. sous la valeur par défaut de la propriété `service.ranking`), car l’hypothèse est que les gestionnaires personnalisés auront besoin d’un classement plus élevé. Cependant, le classement n’est pas le minimum absolu pour s’assurer de la flexibilité lorsque cela est nécessaire.

Ce gestionnaire de conflits donne la priorité au plan directeur. La page de la copie dynamique `/b` est déplacée (dans la branche de la copie dynamique) vers `/b_msm_moved`.

* copie en direct : `/b`

   Est déplacé (dans la copie dynamique) vers `/b_msm_moved`. Cela fait office de sauvegarde et permet de s’assurer qu’aucun contenu n’est perdu.

   * `lc-level-1` n’est pas déplacé.

* plan directeur : `/b`

   Est déployé sur la page de copie dynamique `/b`.

   * `bp-level-1` est déployé dans la Live Copy.

**Après le déploiement**

<table>
 <tbody>
  <tr>
   <td><strong>plan directeur après le déploiement</strong></td>
   <td><strong>copie dynamique après le déploiement</strong><br /> </td>
   <td></td>
   <td><strong>copie dynamique après le déploiement</strong><br /> <br /> <br /> </td>
   <td><strong>publier après le déploiement</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (a le contenu de la page du plan directeur b qui a été publiée)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (contient le contenu de la page b qui a été créée manuellement dans la branche de la copie dynamique)</td>
   <td><code>b</code> <br /> (aucun changement ; contient le contenu de la page d'origine b qui a été créée manuellement dans la branche de la copie dynamique et est maintenant appelée b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (aucune modification)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (aucune modification)</td>
  </tr>
 </tbody>
</table>

### Gestionnaires personnalisés {#customized-handlers}

Les gestionnaires de conflit personnalisés permettent de mettre en œuvre vos propres règles. À l’aide du mécanisme de classement des services, vous pouvez également définir leur mode d’interaction avec les autres gestionnaires.

Les gestionnaires de conflit personnalisés peuvent être :

* nommés selon vos besoins ;
* développés/configurés selon vos besoins, par exemple, vous pouvez développer un gestionnaire de sorte que la page de la Live Copy prévale ;
* conçus de manière à être configurés à l’aide de la [configuration OSGi](/help/sites-deploying/configuring-osgi.md), en particulier :

   * **Classement de service**:

      Définit l’ordre associé aux autres gestionnaires de conflit ( `service.ranking`).

      La valeur par défaut est 0.

### Comportement lorsque la gestion des conflits est désactivée {#behavior-when-conflict-handling-deactivated}

Si vous [désactivez manuellement la gestion des conflits](#rollout-manager-and-conflict-handling), AEM n’intervient pas sur les pages créant un conflit (les pages ne présentant pas de conflit sont déployées comme prévu).

>[!CAUTION]
>
>AEM ne fournit pas d’indication lorsque des conflits sont ignorés, car ce comportement doit être configuré explicitement. Il est donc considéré comme le comportement exigé.

Dans ce cas, la Live Copy prévaut effectivement. La page du plan directeur `/b` n&#39;est pas copiée et la page de la copie dynamique `/b` n&#39;est pas touchée.

* plan directeur : `/b`

   N’est pas copié du tout, mais est ignoré.

* copie en direct : `/b`

   Reste le même.

<table>
 <caption>
   Après le déploiement
 </caption>
 <tbody>
  <tr>
   <td><strong>plan directeur après le déploiement</strong></td>
   <td><strong>copie dynamique après le déploiement</strong><br /> <br /> <br /> </td>
   <td><strong>publier après le déploiement</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (aucun changement ; a le contenu de la page b créée manuellement dans la branche de la copie dynamique)</td>
   <td><code>b</code> <br /> (aucun changement ; contient le contenu de la page b créée manuellement dans la branche de la copie dynamique)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (aucune modification)</td>
   <td><code> /lc-level-1</code> <br /> (aucune modification)</td>
  </tr>
 </tbody>
</table>

### Classements des services {#service-rankings}

Le classement des services [OSGi](https://www.osgi.org/) peut être utilisé pour définir la priorité des différents gestionnaires de conflit.
