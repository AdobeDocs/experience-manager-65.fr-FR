---
title: Structuration de la gestion multisite du contenu ciblé
description: Le diagramme suivant indique comment est structurée la prise en charge multisite du contenu ciblé.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%
---
# Structuration de la gestion multisite du contenu ciblé{#how-multisite-management-for-targeted-content-is-structured}

Le diagramme suivant indique comment est structurée la prise en charge multisite du contenu ciblé.

Les zones apparaissent sous **/content/campaigns/&lt;marque>** et par défaut chaque marque comporte une zone maître, qui est créée automatiquement. Chaque zone contient son propre ensemble d’activités, d’expériences et d’offres.

![chlimage_1-268](assets/chlimage_1-268.png)

Pour rechercher du contenu ciblé, les pages ou les sites peuvent correspondre à une zone. Si aucune zone n’est configurée, AEM revient à la zone principale pour cette marque spécifique.

Le diagramme suivant illustre le fonctionnement de la logique pour trois sites, nommés site1, site2 et site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 recherche myarea1 pour brand1 et otherarea2 pour brand2 en fonction du mappage de la zone.
* site2 recherche myarea1 pour brand1 et la zone principale pour brand2 car seul le mappage de zone pour brand1 est défini.
* site3 recherche la zone principale pour brand1 et brand2 car aucun autre mappage de zone n’est défini pour ce site.
