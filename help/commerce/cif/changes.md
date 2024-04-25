---
title: Modifications notables apportées au module complémentaire CIF (Commerce Integration Framework)
description: Modifications notables du module complémentaire Commerce Integration Framework (CIF) par rapport aux anciennes versions du CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 100%

---

# Modifications notables apportées au module complémentaire CIF (Commerce Integration Framework){#notable-changes}

Ce document met en évidence les différences importantes entre le module complémentaire CIF (Commerce Integration Framework) et les anciennes versions de CIF, connues principalement sous le nom de CIF Classic (Quickstart) et CIF Open Source.

## Installation et mises à jour

Le package complémentaire AEM CIF peut être installé et mis à jour grâce au gestionnaire de packages AEM.

**Versions CIF précédentes**

* CIF Classic : aucune installation n’était nécessaire, CIF faisait partie de la version Quickstart. Les mises à jour CIF faisaient partie des mises à jour régulières d’AEM ou de service pack.
* CIF open-source : installation via GitHub. Les mises à jour faisaient partie des opérations de mise à jour manuelle/de maintenance.

## Configuration du point d’entrée

Le point d’entrée est configuré via la console OSGi.

**Versions CIF précédentes**

* CIF Classic : via la configuration OSGi dans AEM
* CIF Open Source : via l’explorateur de configurations CIF

## Déploiement du projet CIF Venia

Le projet disponible dans les [Guides AEM GitHub - Projet CIF Venia](https://github.com/adobe/aem-cif-guides-venia) et déploiement effectué via le gestionnaire de packages AEM.

**Versions CIF précédentes**

* CIF Classic : via l’installation du package AEM

## Données du catalogue de produits

Les données du catalogue de produits sont accessibles à la demande par le biais d’appels en temps réel vers un point d’entrée externe qui prend en charge les API GraphQL requises. Ces API autorisent l’accès aux données actives ou intermédiaires à n’importe quelle date. Aucune réplication n’est nécessaire.

**Versions CIF précédentes**

* CIF Classic : les données de produits actives et intermédiaires sont importées et conservées dans JCR sur AEM Author grâce à des importations de produits complètes ou par différence. Les données de produits actives sont répliquées vers le service de publication AEM.

## Expériences de catalogue de produits avec rendu dans AEM

AEM effectue le rendu à la volée des expériences de catalogue de produits à l’aide de modèles de catalogues AEM préalablement affectés aux produits et aux catégories. Aucune réplication n’est nécessaire.

**Versions CIF précédentes**

* CIF Classic : AEM Author crée une page AEM pour chaque catégorie/produit à l’aide de l’outil de plan directeur de catalogue. Ces pages sont répliquées vers le service de publication AEM

>[!NOTE]
>
>Pour obtenir de la documentation supplémentaire sur l’utilisation de CIF avec AEM Managed Service ou AEM On-Premise, voir [Framework d’intégration de Commerce (Commerce Integration Framework, CIF)](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
