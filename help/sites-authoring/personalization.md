---
title: Personnalisation et ciblage de contenu
seo-title: Personnalisation et ciblage de contenu
description: Découvrez comment AEM peut créer du contenu personnalisé
seo-description: Découvrez comment AEM peut créer du contenu personnalisé
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 87%

---


# Personnalisation et ciblage de contenu {#personalization}

## Personnalisation et ciblage de contenu {#personalization-and-content-targeting}

AEM propose un ensemble d’outils permettant de créer du contenu ciblé et de présenter des expériences personnalisées.

## Mode Ciblage   {#targeting-mode}

[Créez du contenu ciblé à l’aide du mode Ciblage d’AEM. ](/help/sites-authoring/content-targeting-touch.md) Le mode Ciblage et le composant Cible fournissent des outils permettant de créer du contenu pour les expériences de vos activités de marketing.

## Activités    {#activities}

Les activités définissent et organisent vos efforts de marketing. Les activités englobent les audiences ciblées et la période pendant laquelle le ciblage est appliqué.

Par exemple, le catalogue de produits We.Retail comprend des teasers qui concentrent leur attention sur les produits saisonniers. L’activité de sports d’été définit les segments de marketing que les teasers ciblent pendant les mois d’été.

Les activités identifient également le [moteur de ciblage](/help/sites-authoring/personalization.md#targeting-engine) que vos pages utilisent.

Utilisez la [console Activités](/help/sites-authoring/activitylib.md) pour créer et gérer les activités de vos marques. Vous pouvez également créer des activités tout en [créant du contenu ciblé](/help/sites-authoring/content-targeting-touch.md).

## Expériences {#experiences}

Pour chaque activité, vous définissez une ou plusieurs expériences qui identifient les audiences que vous ciblez. AEM vous permet de contrôler le contenu qui constitue chaque expérience.

Les audiences sont basées sur les segments de marketing créés dans AEM ou Adobe Target. Lorsqu’un visiteur ouvre une page web, la logique de la page détermine l’audience à laquelle ce visiteur appartient et affiche le contenu que vous avez créé pour cette audience.

Par exemple, une activité définit les expériences destinées à deux audiences distinctes : les femmes âgées de moins de 30 ans et les femmes âgées de plus de 30 ans. La page Femmes du site Web We.Retail présente différents produits pour chaque expérience.

Vous définissez des expériences pour une activité. Vous pouvez utiliser la [console Activités](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) ou le [mode de ciblage](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) pour ajouter des expériences à une activité.

## Offres    {#offers}

Une offre constitue du contenu qui s’affiche à un endroit d’une page pour créer une expérience. Utilisez différentes offres pour différentes expériences afin d’optimiser l’efficacité du contenu destiné à vos audiences.

Par exemple, la page Femmes du site Web d’exemple We.Retail peut utiliser des offres comme image de bande-annonce qui s’affiche en haut de la page. L’offre utilisée en tant que teaser de l’expérience destinée aux femmes de plus de 30 ans n’est pas la même que celle utilisée pour les femmes de moins de 30 ans.

Utilisez la [console Offres](/help/sites-authoring/offerlib.md) pour créer des offres que vous pouvez utiliser dans plusieurs expériences. Créez des offres à utiliser une seule fois ou ajoutez des offres issues d’une bibliothèque d’offres lors de la [création de contenu ciblé](/help/sites-authoring/content-targeting-touch.md).

## Moteur de ciblage    {#targeting-engine}

Le moteur de ciblage est le mécanisme sous-jacent à la logique du contenu ciblé. Les [activités](/help/sites-authoring/activitylib.md) sont configurées pour utiliser l’un des deux moteurs de ciblage disponibles : AEM et Adobe Target.

### AEM {#aem}

AEM fournit un moteur de ciblage intégré qui traite les requêtes de page et détermine le contenu à afficher. Lorsque vous utilisez le moteur de ciblage AEM, vous êtes limité aux segments créés dans AEM pour définir les audiences de vos expériences.

### Adobe Target {#adobe-target}

Avec le moteur de ciblage Adobe Target, les informations recueillies suite aux visites de page font l’objet d’un suivi dans Adobe Target.

* Avec ce moteur de ciblage, vous utilisez les segments que vous importez à partir d’Adobe Target pour définir les audiences de vos expériences.
* Les activités qui utilisent le moteur Adobe Target sont [synchronisées sur Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Vous pouvez utiliser ce moteur lorsque [est intégré à Adobe Target](/help/sites-administering/opt-in.md).
