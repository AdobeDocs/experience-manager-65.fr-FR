---
title: Structuration de la gestion multisite du contenu ciblé
seo-title: How Multisite Management for Targeted Content is Structured
description: Un diagramme indique comment la prise en charge multisite du contenu ciblé est structurée.
seo-description: A diagram shows how multisite support for targeted content is structured
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 100%

---

# Structuration de la gestion multisite du contenu ciblé{#how-multisite-management-for-targeted-content-is-structured}

Le diagramme suivant indique comment est structurée la prise en charge multisite du contenu ciblé.

Les zones apparaissent sous **/content/campaigns/&lt;marque>** et par défaut chaque marque comporte une zone maître, qui est créée automatiquement. Chaque zone contient son propre ensemble d’activités, d’expériences et d’offres.

![chlimage_1-268](assets/chlimage_1-268.png)

Pour consulter du contenu ciblé, les pages ou les sites peuvent être mappés à une zone. Si aucune zone n’est configurée, AEM utilise la zone maître de cette marque spécifique.

Le diagramme suivant illustre le fonctionnement de la logique pour trois sites, nommés site1, site2 et site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* Le site1 consulte mazone1 pour la marque1 et l’autrezone2 pour la marque2 en fonction du mappage de zone.
* Le site2 consulte mazone1 pour la marque1 et la zone maître pour la marque2, car seul le mappage de zone de la zone1 est défini.
* Le site3 consulte la zone maître de la marque1 et de la marque2, car aucun autre mappage de zone n’est défini pour ce site.
