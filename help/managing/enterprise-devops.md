---
title: Opérations de développement d’entreprise (DevOps)
seo-title: Opérations de développement d’entreprise (DevOps)
description: Découvrez les processus, les méthodes et les communications requis pour faciliter le déploiement et simplifier la collaboration.
seo-description: Découvrez les processus, les méthodes et les communications requis pour faciliter le déploiement et simplifier la collaboration.
uuid: ca4806d2-c845-4c18-9498-4b66f0980a5e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 934eda2a-bd3b-4018-86dc-dbb01d246386
exl-id: e67f848a-a8cd-4585-a734-e6b1de8a8d74
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 98%

---

# Opérations de développement d’entreprise (DevOps){#enterprise-devops}

Les opérations de développement couvrent les processus, les méthodes et les communications requis pour :

* simplifier le déploiement de votre logiciel sur les différents environnements ;
* simplifier la collaboration entre les équipes de développement, de test et de déploiement.

Les opérations de développement visent à éviter les problèmes tels que :

* les erreurs manuelles ;
* les éléments oubliés, par exemple, des fichiers ou des détails de configuration ;
* les incohérences, par exemple, entre l’environnement local d’un développeur et d’autres environnements.

## Environnements {#environments}

Un déploiement d’Adobe Experience Manager (AEM) implique généralement plusieurs environnements, utilisés à diverses fins à différents niveaux :

* [Développement](#development)
* [Assurance qualité](#quality-assurance)
* [Évaluation ](#staging)
* [Production](#production-author-and-publish)

>[!NOTE]
>
>L’environnement de production doit avoir au moins un environnement de création et un environnement de publication.
>
>Il est recommandé que tous les autres environnements se composent également d’un environnement de création et de publication afin de refléter l’environnement de production et de permettre des tests lors de phases précoces du projet.

### Développement {#development}

Les développeurs sont chargés de développer et de personnaliser le projet proposé (qu’il s’agisse d’un site web, d’applications mobiles, d’une mise en œuvre de gestion des actifs numériques, etc.) avec toutes les fonctionnalités nécessaires. Ils :

* développent et personnalisent les éléments nécessaires, par exemple, les modèles, les composants, les workflows et les applications ;
* réalisent la conception ;
* développent les services et les scripts nécessaires pour mettre en œuvre les fonctionnalités requises.

La configuration de l’environnement de [développement](/help/sites-developing/best-practices.md) peut dépendre de nombreux facteurs, bien qu’elle soit généralement composée des éléments suivants :

* Un système de développement intégré avec contrôle de version pour fournir une base de code intégrée. Il est utilisé pour fusionner et consolider le code des différents environnements de développement utilisés par chaque développeur.
* Un environnement personnel pour chaque développeur, résidant habituellement sur son ordinateur local. Le code est synchronisé avec le système de contrôle de version à des intervalles appropriés.

Selon l’échelle de votre système, l’environnement de développement peut comprendre une instance de création et une instance de publication.

### Assurance qualité {#quality-assurance}

Cet environnement est utilisé par l’équipe d’assurance qualité pour tester entièrement [votre nouveau système. conception et fonction. ](/help/sites-developing/test-plan.md) Il devrait comprendre des environnements de création et de publication, avec le contenu approprié, et fournir tous les services nécessaires pour réaliser une suite complète de tests.

### Évaluation  {#staging}

L’environnement intermédiaire doit être un miroir de l’environnement de production, en matière de configuration, de code et de contenu :

* Il permet de tester les scripts utilisés pour mettre en œuvre le déploiement.
* Il peut servir pour les tests finaux (de conception, des fonctionnalités et des interfaces) avant le déploiement sur les environnements de production.
* L’environnement intermédiaire ne peut pas toujours être identique à l’environnement de production ; toutefois, il doit s’en rapprocher le plus possible afin de permettre les tests de performance et de charge.

### Production : création et publication  {#production-author-and-publish}

L’environnement de production est constitué des environnements requis pour [créer et publier](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) votre mise en œuvre.

Un environnement de production comprend au moins une instance de création et une instance de publication :

* Une instance de [création](#author) pour la saisie du contenu.
* Une instance de [publication](#publish) pour le contenu mis à la disposition de vos visiteurs/utilisateurs.

En fonction de l’échelle du projet, il se compose bien souvent de plusieurs instances de création et/ou de publication. À un niveau inférieur, le référentiel peut également être mis en grappe sur plusieurs instances.

#### Création {#author}

Les instances de création sont généralement situées derrière le pare-feu interne. Il s’agit de l’environnement dans lequel vos collègues et vous-même effectuez les tâches de création, telles que :

* Administration du système
* Saisie du contenu
* Configuration de la mise en page et conception du contenu
* Activation du contenu dans l’environnement de publication

Le contenu qui a été activé est regroupé en module et placé dans la file d’attente de réplication de l’environnement de création. Le processus de réplication transporte alors ce contenu vers l’environnement de publication.

De façon à répliquer à l’inverse les données dans un environnement de publication vers l’environnement de création, un écouteur de réplication dans l’environnement de création interroge l’environnement de publication et récupère le contenu dans la boîte d’envoi de la réplication inverse de l’environnement de publication.

#### Publication  {#publish}

L’environnement de publication est généralement situé dans la zone démilitarisée (DMZ). Il s’agit de l’environnement dans lequel les visiteurs accèdent à votre contenu (par exemple, par le biais d’un site web ou sous forme d’application mobile) et interagissent avec lui, qu’il soit public ou se trouve sur votre réseau intranet. Un environnement de publication :

* présente du contenu répliqué à partir de l’environnement de création ;
* met ce contenu à la disposition des visiteurs ;
* stocke les données utilisateur générées par vos visiteurs, telles que les commentaires ou les autres soumissions de formulaires ;
* peut être configuré pour ajouter ces données utilisateur à une boîte d’envoi pour la réplication inverse vers l’environnement de création.

L’environnement de publication génère du contenu de manière dynamique et en temps réel, et le contenu peut être personnalisé pour chaque utilisateur.

## Mouvement de code   {#code-movement}

Le code doit toujours être propagé du bas vers le haut :

* Le code est développé initialement dans l’environnement de développement local puis dans les environnements de développement intégrés.
* Par la suite, il fait l’objet d’un test complet dans le ou les environnements d’assurance qualité.
* Il est ensuite testé dans les environnements intermédiaires.
* À ce stade seulement, le code doit être déployé dans les environnements de production.

Le code (par exemple, les fonctionnalités d’applications web et les modèles de conception personnalisés) est généralement transféré en exportant et en important des modules entre les différents référentiels de contenu. Le cas échéant, cette réplication peut être configurée en tant que processus automatique.

Les projets AEM déclenchent souvent le déploiement du code :

* Automatiquement : pour le transfert vers les environnements de développement et d’assurance qualité.
* Manuellement : les déploiements sur les environnements d’évaluation et de production sont effectués de manière plus contrôlée, souvent manuelle ; l’automatisation reste toutefois possible, si nécessaire.

![chlimage_1](assets/chlimage_1.png)

## Déplacement de contenu {#content-movement}

Le contenu conçu pour la production doit **toujours** être créé sur l’instance de création de production.

Le contenu ne doit pas suivre le déplacement du code des environnements inférieurs vers les plus élevés. Il n’est en effet pas recommandé de créer du contenu sur des ordinateurs locaux ou des environnements inférieurs, puis de le déplacer vers l’environnement de production, car cela peut introduire des erreurs et des incohérences.

Le contenu de production doit être déplacé à partir de l’environnement de production vers l’environnement d’évaluation pour assurer que ce dernier fournit un environnement de test efficace et précis.

>[!NOTE]
>
>Cela ne signifie pas que le contenu intermédiaire doit être continuellement synchronisé avec la production, les mises à jour régulières étant suffisantes, sauf avant de tester une nouvelle itération de code. Il n’est pas nécessaire de mettre à jour le contenu des environnements d’assurance qualité et de développement aussi fréquemment ; il doit simplement bien représenter le contenu de production.

Le contenu peut être transféré :

* entre les différents environnements, en exportant et en important des modules ;
* entre différentes instances, en répliquant directement (par [réplication AEM](/help/sites-deploying/replication.md)) le contenu (à l’aide d’une connexion HTTP ou HTTPS).

![chlimage_1-1](assets/chlimage_1-1.png)
