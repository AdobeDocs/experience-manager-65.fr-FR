---
title: Modifications notables du module complémentaire CIF (Commerce Integration Framework)
description: Modifications notables du module complémentaire CIF (Commerce Integration Framework) par rapport aux anciennes versions de CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 3%

---

# Modifications notables apportées au module complémentaire CIF (Commerce Integration Framework){#notable-changes}

Ce document met en évidence les différences importantes entre le module complémentaire CIF (Commerce Integration Framework) et les anciennes versions de CIF, connues principalement sous le nom de CIF Classic (Quickstart) et CIF Open Source.

## Installation et mises à jour

Le module complémentaire AEM CIF est installé et mis à jour avec AEM Package Manager.

**Versions CIF précédentes**

* CIF Classic : Aucune installation n’était nécessaire, CIF faisait partie du Quickstart. Les mises à jour CIF faisaient partie des mises à jour régulières d’AEM ou de Service Pack.
* CIF Open Source : Installation via GitHub. Les mises à jour faisaient partie du travail manuel de mise à jour/maintenance.

## Configuration du point d’entrée

Le point de terminaison est configuré via la console OSGi.

**Versions CIF précédentes**

* CIF Classic : Via la configuration OSGi dans AEM
* CIF Open Source : Via le navigateur de configuration CIF

## Déploiement du projet CIF Venia

Projet disponible sur [GitHub AEM Guides - Projet CIF Venia](https://github.com/adobe/aem-cif-guides-venia) et déploiement effectué via AEM Package Manager.

**Versions CIF précédentes**

* CIF Classic : Via l’installation AEM package

## Données du catalogue de produits

Les données du catalogue de produits sont demandées à la demande via des appels en temps réel vers un point de terminaison externe qui prend en charge les API GraphQL requises. Ces API prennent en charge l’accès aux données actives ou intermédiaires à n’importe quelle date donnée. Aucune réplication n’est nécessaire.

**Versions CIF précédentes**

* CIF Classic : Les données des produits en direct et intermédiaires sont importées et conservées dans JCR sur l’auteur AEM via l’importation de produits complète ou delta. Les données de produit en direct sont répliquées vers AEM Publish.

## Expériences du catalogue de produits avec rendu AEM

AEM effectue le rendu à la volée des expériences de catalogue de produits à l’aide AEM modèles de catalogue qui ont été affectés aux produits et aux catégories. Aucune réplication n’est nécessaire.

**Versions CIF précédentes**

* CIF Classic : AEM Author crée une page d’AEM pour chaque catégorie/produit à l’aide de l’outil de plan directeur de catalogue. Ces pages sont répliquées vers AEM Publish.

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation de CIF avec AEM Managed Service ou AEM On-Premise, voir [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
