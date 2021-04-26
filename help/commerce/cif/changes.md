---
title: Modifications notables du module complémentaire CIF (Commerce Integration Framework)
description: Changements notables du module complémentaire CIF (Commerce Integration Framework) par rapport aux anciennes versions de CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 9%

---

# Modifications notables du module complémentaire CIF (Commerce Integration Framework){#notable-changes}

Ce document souligne les différences importantes entre le module complémentaire du Commerce Integration Framework (CIF) et les anciennes versions de CIF, principalement connues sous le nom de CIF Classic (Quickstart) et CIF Open Source.

## Installation et mises à jour

Le module complémentaire AEM CIF est installé et mis à jour avec AEM Package Manager.

**Versions CIF précédentes**

* CIF Classic : Aucune installation n&#39;était nécessaire, CIF faisait partie de Quickstart. Les mises à jour CIF faisaient partie des mises à jour régulières des AEM ou Service Pack.
* CIF Open source : Installation via GitHub. Les mises à jour faisaient partie du travail manuel de mise à jour/maintenance.

## Configuration du point de terminaison

Le point de terminaison est configuré via la console OSGi.

**Versions CIF précédentes**

* CIF Classic : Via la configuration OSGi dans AEM
* CIF Open source : Via le navigateur de configuration CIF

## Déploiement du projet CIF Venia

Projet disponible sur [Guides d&#39;AEM GitHub - Projet CIF Venia](https://github.com/adobe/aem-cif-guides-venia) et déploiement effectué par l&#39;intermédiaire du gestionnaire de modules

**Versions CIF précédentes**

* CIF Classic : Via l’installation AEM package

## Données du catalogue de produits

Les données du catalogue de produits sont demandées à la demande via des appels en temps réel vers un point de terminaison externe qui prend en charge les API GraphQL requises. Ces API prennent en charge l’accès aux données actives ou d’évaluation à une date donnée. Aucune réplication n&#39;est nécessaire.

**Versions CIF précédentes**

* CIF Classic : Les données des produits en direct et intermédiaires sont importées et conservées dans le JCR sur AEM Author par le biais d’une importation de produits complète ou delta. Les données des produits en direct sont répliquées dans AEM Publish.

## Expériences de catalogue de produits avec rendu AEM

AEM effectue le rendu des expériences de catalogue de produits à la volée à l’aide de modèles de catalogue AEM qui ont été affectés à des produits et des catégories. Aucune réplication n&#39;est nécessaire.

**Versions CIF précédentes**

* CIF Classic : AEM Author crée une page d’AEM pour chaque catégorie/produit à l’aide de l’outil de schéma directeur du catalogue. Ces pages sont répliquées dans AEM Publish.

>[!NOTE]
>
>Pour obtenir de la documentation supplémentaire sur l’utilisation de CIF avec AEM Managed Service ou AEM On-premise, voir [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html).
