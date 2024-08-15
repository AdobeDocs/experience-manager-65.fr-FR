---
title: Résolution des problèmes et FAQ concernant MSM
description: Découvrez comment résoudre les problèmes les plus courants liés à MSM et comment obtenir des réponses aux questions les plus courantes à ce sujet.
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 98%

---

# Résolution des problèmes et FAQ concernant MSM {#troubleshooting-msm}

## Premières étapes de résolution des problèmes {#first-steps}

Si vous constatez ce que vous pensez être un comportement erroné ou une erreur dans MSM, avant de procéder à un dépannage en profondeur, assurez-vous de vérifier les points suivants :

* Consultez la [FAQ sur MSM](#faq) car vos problèmes ou questions peuvent y avoir déjà été abordés.
* Consultez l’[article sur les bonnes pratiques MSM](msm-best-practices.md), car plusieurs conseils y sont proposés, ainsi que des clarifications sur certaines idées fausses.

## Recherche d’informations avancées sur votre plan et le statut de Live Copy {#advanced-info}

MSM enregistre plusieurs servlets qui peuvent être sollicités par le biais de sélecteurs sur les URL des ressources. Ces dernières sont utilisées au travers de l’interface utilisateur mais peuvent également être appelées directement afin d’afficher directement des statuts MSM supplémentaires calculés de façon avancée pour vos pages :

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Utilisez cette adresse sur une page de plan directeur pour récupérer la liste de toutes les Live Copies qui lui sont liées, avec des informations supplémentaires sur le statut des Live Copies.
   * par exemple :
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Utilisez cette adresse sur les pages Live Copy pour récupérer des informations détaillées sur leurs relations à leurs pages de plan directeur. Si la page n’est pas une Live Copy, rien n’est renvoyé.
   * par exemple :
     `http://localhost:4502/content/wknd/ca/en.msm.json`

Ces servlets génèrent des messages du journal DEBUG via le journal `com.day.cq.wcm.msm` qui peuvent également être utiles.

## Vérification des informations spécifiques au module MSM dans le référentiel {#checking-repo}

Les versions précédentes des servlets renvoyaient des informations calculées basées sur les nœuds et mixins spécifiques au module MSM. Les informations sont stockées dans le référentiel de la manière suivante.

* Type de mixin `cq:LiveSync`
   * Il est défini sur les nœuds `jcr:content` et définit les pages racine Live Copy.
   * Ces pages présentent un nœud enfant `cq:LiveSyncConfig` de type `cq:LiveCopy` qui contiendra des informations de base et obligatoires sur la Live Copy dans les propriétés suivantes :
      * `cq:master` pointe vers la page de plan directeur de la Live Copy.
      * `cq:rolloutConfigs` indique les configurations de déploiement principal appliquées à la Live Copy.
      * `cq:isDeep` est « true » si les pages enfants de cette page racine de Live Copy sont incluses dans la Live Copy.
* Type de mixin `cq:LiveRelationship`
   * Toute page Live Copy dispose de ce type de mixin sur son nœud `jcr:content`.
   * Si tel n’est pas le cas, la page a dû à un moment donné être détachée ou créée manuellement par le biais de l’interface de création en dehors d’une action Live Copy (création ou déploiement).
* Type de mixin `cq:LiveSyncCancelled`
   * Ajouté aux nœuds `jcr:content` des pages Live Copy suspendues.
   * Si la suspension s’applique également aux pages enfants, une propriété `cq:isCancelledForChildren` est définie sur « true » sur le même nœud.

Les informations présentes dans ces propriétés doivent se refléter dans l’interface utilisateur. Toutefois, lors de la résolution des problèmes, il peut s’avérer utile d’observer directement le comportement de MSM dans le référentiel lorsque des actions MSM se produisent.

La connaissance de ces propriétés peut également s’avérer utile pour interroger votre référentiel et découvrir des jeux de pages qui se trouvent dans des états particuliers. Par exemple :

* `select * from cq:LiveSync` renvoie toutes les pages racine Live Copy.

## FAQ {#faq}

Vous trouverez ci-dessous quelques questions fréquentes concernant MSM et la Live Copy.

### Pourquoi certaines propriétés (par exemple le titre ou les annotations) ne sont-elles pas mises à jour lors d’un déploiement MSM ? {#missing-properties}

Les actions de synchronisation MSM sont hautement configurables. Les propriétés ou composants qui sont modifiés lors des déploiements dépendent directement des propriétés de ces configurations.

Pour plus d’informations sur cette rubrique, voir [Bonnes pratiques MSM](msm-best-practices.md) .

### Comment puis-je supprimer les autorisations de déploiement pour un groupe d’auteurs ?  {#remove-rollout-permissions}

Aucun privilège de **déploiement** ne peut être défini ou supprimé pour les principaux d’AEM (utilisateurs ou groupes).

Vous pouvez cependant :

* modifier l’interface utilisateur du produit pour masquer les actions de déploiement pour un principal de sécurité donné ;
* supprimer les privilèges d’écriture de l’arborescence Live Copy pour les auteurs et autrices qui n’ont pas l’autorisation de procéder à un déploiement.

### Pourquoi les pages Live Copy présentent-elles le suffixe « _msm_moved » ?  {#moved-pages}

Si une page de plan directeur est déployée, elle met à jour sa page Live Copy ou crée une nouvelle page Live Copy si celle-ci n’existe pas encore. Par exemple, lorsqu’elle a été déployée pour la première fois ou que la page Live Copy a été supprimée manuellement.

Dans ce dernier cas, cependant, si une page sans propriété `cq:LiveRelationship` porte le même nom, cette page sera renommée, avant la création de la page Live Copy.

Par défaut, le déploiement attend une page Live Copy liée, sur laquelle les mises à jour des plans directeurs sont déployées. Ou, il ne s’attend à aucune page lors de la création d’une page Live Copy.

Si une page « autonome » est trouvée, MSM choisit de la renommer et de créer une page Live Copy distincte et liée.

Une telle page autonome dans une sous-arborescence de Live Copy provient généralement d’une opération **Désolidariser**, ou l’ancienne page de Live Copy a pu avoir été supprimée manuellement par un auteur ou une autrice, puis recréée sous le même nom.

Pour éviter cela, utilisez la fonction Live Copy **Suspendre** au lieu de **Désolidariser**. Vous trouverez plus d’informations sur l’action **Désolidariser** dans [cet article](msm-livecopy.md).
