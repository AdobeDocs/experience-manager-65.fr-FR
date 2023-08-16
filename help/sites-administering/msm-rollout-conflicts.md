---
title: Conflits de déploiement dans MSM
seo-title: MSM Rollout Conflicts
description: Découvrez comment gérer les conflits de déploiement de Multi Site Manager.
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 70%

---

# Conflits de déploiement dans MSM{#msm-rollout-conflicts}

Des conflits peuvent apparaître si de nouvelles pages portant le même nom de page sont créées dans la branche de plan directeur et dans une branche de Live Copy dépendante.

Ces conflits doivent être gérés et résolus lors du déploiement.

## Gestion des conflits {#conflict-handling}

Lorsqu’il existe des pages en conflit (dans les branches Plan directeur et Live Copy), MSM vous permet de définir comment (ou même si) elles doivent être gérées.

Pour vous assurer que le déploiement n’est pas bloqué, les définitions possibles peuvent inclure :

* la page (plan directeur ou Live Copy) qui aura la priorité lors du déploiement,
* Pages renommées (et comment)
* Impact sur le contenu publié

   Le comportement par défaut d’AEM (version commerciale) est que le contenu publié n’est pas affecté. Ainsi, si une page qui a été créée manuellement dans la branche Live Copy a été publiée, ce contenu sera toujours publié après la gestion et le déploiement du conflit.

Outre les fonctionnalités standard, des gestionnaires de conflit personnalisés peuvent être ajoutés pour mettre en œuvre différentes règles. Ils peuvent également permettre des actions de publication sous la forme d’un processus individuel.

### Exemple de scénario {#example-scenario}

Dans les sections suivantes, nous utilisons l’exemple d’une nouvelle page `b`, créée dans les branches Plan directeur et Live Copy (créée manuellement) pour illustrer les différentes méthodes de résolution des conflits :

* Plan directeur : `/b`

  Page principale avec 1 page enfant, bp-level-1.

* Live Copy : `/b`

  Page créée manuellement dans la branche Live Copy, avec 1 page enfant, `lc-level-1`.

   * Activé lors de la publication sous la forme `/b`, avec la page enfant.

**Avant le déploiement**

<table>
 <tbody>
  <tr>
   <td><strong>Plan directeur avant le déploiement</strong></td>
   <td><strong>Live Copy avant le déploiement</strong></td>
   <td><strong>Publication avant le déploiement</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (Création dans la branche du plan directeur, prête pour le déploiement)<br /> </td>
   <td><code>b</code><br /> <br /> (Création manuelle dans la branche Live Copy)<br /> </td>
   <td><code>b</code><br /> <br /> (Contient le contenu de la page b créée manuellement dans la branche Live Copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (Création manuelle dans la branche Live Copy)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (Contient le contenu de la page <br /> créée manuellement dans la branche Live Copy)</td>
  </tr>
 </tbody>
</table>

## Gestionnaire de déploiement et gestion des conflits {#rollout-manager-and-conflict-handling}

Le gestionnaire de déploiement vous permet d’activer ou de désactiver la gestion des conflits.

Vous pouvez le faire à l’aide de la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) du **gestionnaire de déploiement gestion du contenu web Day CQ** :

* **Gestion des conflits avec les pages créées manuellement** :

  (`rolloutmgr.conflicthandling.enabled`)

  Définissez sur true si le gestionnaire de déploiement doit gérer des conflits d’une page créée dans la Live Copy portant un nom existant déjà dans le plan directeur.

AEM possède un [comportement prédéfini lorsque la gestion des conflits a été désactivée](#behavior-when-conflict-handling-deactivated).

## Gestionnaires de conflit {#conflict-handlers}

AEM utilise des gestionnaires de conflit pour résoudre des conflits de page qui émergent lors du déploiement du contenu du plan directeur vers la Live Copy. L’une des méthodes (habituelles) pour résoudre ce type de conflit est de renommer les pages. Plusieurs gestionnaires de conflit peuvent être opérationnels pour permettre une sélection de comportements différents.

AEM fournit :

* La variable [gestionnaire de conflit par défaut](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* La possibilité de mettre en œuvre un [gestionnaire personnalisé](#customized-handlers).
* Mécanisme de classement des services qui vous permet de définir la priorité de chaque gestionnaire individuel. Le service qui possède la valeur la plus élevée est utilisé.

### Gestionnaire de conflits par défaut {#default-conflict-handler}

Gestionnaire de conflits par défaut :

* est appelé `ResourceNameRolloutConflictHandler`.

* Avec ce gestionnaire, la page du plan directeur prévaut.
* Le classement des services pour ce gestionnaire est défini sur Bas, c’est-à-dire en dessous de la valeur par défaut pour la propriété `service.ranking`, car le postulat de base est que les gestionnaires personnalisés doivent posséder un classement supérieur. Cependant, le classement n’est pas le minimum absolu pour garantir de la flexibilité lorsque cela est nécessaire.

Ce gestionnaire de conflits donne la priorité au plan directeur. La page de la Live Copy `/b` est déplacée (dans la branche Live Copy) vers `/b_msm_moved`.

* Live Copy : `/b`

  Est déplacée (dans la Live Copy) vers `/b_msm_moved`. Cela fait office de sauvegarde et permet de s’assurer qu’aucun contenu n’est perdu.

   * `lc-level-1` n’est pas déplacé.

* Plan directeur : `/b`

  Est déployé dans la page Live Copy `/b`.

   * `bp-level-1` est déployé dans la Live Copy.

**Après le déploiement**

<table>
 <tbody>
  <tr>
   <td><strong>Plan directeur après le déploiement</strong></td>
   <td><strong>Live Copy après le déploiement</strong><br /> </td>
   <td></td>
   <td><strong>Live Copy après le déploiement</strong><br /> <br /> <br /> </td>
   <td><strong>Publication après le déploiement</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (Contient le contenu de la page b du plan directeur qui a été déployée)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (Contient le contenu de la page b créée manuellement dans la branche Live Copy)</td>
   <td><code>b</code><br /> <br /> (Aucune modification ; contient le contenu de la page b d’origine qui a été créée manuellement dans la branche Live Copy et qui est maintenant appelée b_msm_moved)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (Aucune modification)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (Aucune modification)</td>
  </tr>
 </tbody>
</table>

### Gestionnaires personnalisés {#customized-handlers}

Les gestionnaires de conflit personnalisés vous permettent de mettre en oeuvre vos propres règles. Grâce au mécanisme de classement des services, vous pouvez également définir la manière dont ils interagissent avec d’autres gestionnaires.

Les gestionnaires de conflit personnalisés peuvent :

* nommés selon vos besoins ;
* Vous pouvez développer/configurer en fonction de vos besoins ; par exemple, vous pouvez développer un gestionnaire pour que la page Live Copy soit prioritaire.
* Peut être conçu pour être configuré à l’aide de la variable [Configuration OSGi](/help/sites-deploying/configuring-osgi.md), en particulier :

   * **Classement de service** :

     Définit l’ordre associé aux autres gestionnaires de conflit (`service.ranking`).

     La valeur par défaut est 0.

### Comportement lorsque la gestion des conflits est désactivée {#behavior-when-conflict-handling-deactivated}

Si vous procédez manuellement [désactiver la gestion des conflits](#rollout-manager-and-conflict-handling) AEM n’effectue aucune action sur les pages en conflit (les pages non en conflit sont déployées comme prévu).

>[!CAUTION]
>
>AEM ne donne aucune indication que les conflits sont ignorés, car ce comportement doit être configuré explicitement. Il est donc supposé qu’il s’agit du comportement requis.

Dans ce cas, la Live Copy prévaut effectivement. La page du plan directeur `/b` n’est pas copiée, et la page de la Live Copy `/b` reste intacte.

* Plan directeur : `/b`

  N’est pas copié du tout et est ignoré.

* Live Copy : `/b`

  Reste la même.

<table>
 <caption>
   Après le déploiement
 </caption>
 <tbody>
  <tr>
   <td><strong>Plan directeur après le déploiement</strong></td>
   <td><strong>Live Copy après le déploiement</strong><br /> <br /> <br /> </td>
   <td><strong>Publication après le déploiement</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (Aucune modification ; contient le contenu de la page b créée manuellement dans la branche Live Copy)</td>
   <td><code>b</code><br /> <br /> (Aucune modification ; contient le contenu de la page b créée manuellement dans la branche Live Copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (Aucune modification)</td>
   <td><code> /lc-level-1</code><br /> <br /> (Aucune modification)</td>
  </tr>
 </tbody>
</table>

### Classements des services {#service-rankings}

Le classement des services [OSGi](https://www.osgi.org/) peut être utilisé pour définir la priorité des différents gestionnaires de conflit.
