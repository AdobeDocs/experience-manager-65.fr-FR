---
title: Comprendre la segmentation lors de la création d’une campagne
description: La segmentation est un élément clé de la création d’une campagne.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
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
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 100%
---
# Compréhension de la segmentation{#understanding-segmentation}

La segmentation est un élément clé de la création d’une campagne. En règle générale, les segments doivent être déjà définis avant le démarrage de votre campagne.

Les visiteurs et visiteuses de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. La compréhension des objectifs et la satisfaction des attentes des visiteurs et visiteuses est un important facteur de réussite en matière de marketing en ligne.

La segmentation permet d’y parvenir en analysant et en profilant :

* l’activité du visiteur ou de la visiteuse sur le site web
* son profil
* l’activité du visiteur ou de la visiteuse sur d’autres sites web

Le contenu peut alors cibler les besoins et centres d’intérêts des visiteurs et visiteuses en fonction des segments qui leur correspondent.

## Utilisation de la segmentation {#using-segmentation}

Les segments sont définis dans la section [Configuration de la segmentation](/help/sites-administering/campaign-segmentation.md). Ils sont utilisés afin d’orienter le contenu réel affiché pour une audience cible spécifique.

## Terminologie de la segmentation {#segmentation-terminology}

Lors de la discussion de la segmentation, la terminologie suivante est utilisée :

**Visiteur** : un visiteur est une personne qui visite un site web. La visite de cette personne commence généralement à partir d’une page de référence, puis passe à une ou plusieurs vues de pages sur votre propre site web. Un profil comportemental peut être créé à partir des détails de la visite de cette personne.

**Utilisateur** : un utilisateur est un visiteur qui s’inscrit auprès du site web pour recevoir un profil de compte. Pour générer leur profil, ils ou elles fournissent une identification supplémentaire, telle qu’une adresse e-mail et un genre, entre autres. Des informations supplémentaires peuvent également être collectées, notamment l’activité de la communauté et les modèles d’achat, entre autres. En fonction des informations fournies dans le profil, un profil démographique peut être créé.

**Caractéristique** : une caractéristique est une particularité ou une propriété d’un visiteur ou d’une visiteuse qui peut être utilisée pour déterminer son appartenance à un segment spécifique.

**Segment** : un segment est un groupe de visiteurs qui partagent certaines caractéristiques. Les segments doivent être distincts, avec un minimum de chevauchement avec les autres segments.

**Caractéristiques comportementales** : les caractéristiques comportementales sont liées au comportement d’un visiteur sur le site web. Ces informations comprennent les éléments suivants :

* L’intérêt au sein de votre site web ; notamment les pages visitées et les produits achetés.
* L’intérêt sur le site web de référence ; notamment les termes de recherche utilisés ou les publicités faisant l’objet d’un clic.
* L’intérêt sur d’autres sites ; déterminé à l’aide d’outils tels que Spyjax.
* La fidélité du visiteur ou de la visiteuse ; la durée de la visite, la fréquence des visites.

**Caractéristiques démographiques** : il s’agit de caractéristiques de population choisies, notamment :

* Âge
* Revenu
* Taille de la famille
* Statut matrimonial
* Genre
* Emplacement

**Caractéristiques dérivées** : certaines caractéristiques démographiques sont difficiles à déterminer sans inscription, mais peuvent être extraites en combinant les caractéristiques comportementales et démographiques.

Par exemple, la combinaison de l’URL de référence (en tant que caractéristique comportementale) avec des données démographiques (acquises à partir d’outils tels que [Google Ad Planner](https://www.google.com/adplanner/)) permet aux propriétaires du site d’extraire les caractéristiques comportementales de leurs visiteurs et visiteuses.

**Sous-segment** : un segment peut être divisé en plusieurs sous-segments. Ceci s’effectue en définissant des caractéristiques supplémentaires.

**Page de teaser** : une page de teaser est conçue à l’intention d’une audience spécifique. Elle contient du contenu réutilisable qui peut être utilisé dans le paragraphe de teaser.

**Campagne** : une campagne est une collection de pages de teaser et de pages de marketing par e-mail, comme des newsletters ou des invitations. Normalement, la campagne s’étend sur une période limitée, puis elle est remplacée par une autre campagne.

**Paragraphe de teaser** : il s’agit d’un paragraphe qui extrait du contenu d’une autre page selon une stratégie de sélection. Cette stratégie de sélection peut tenir compte de segments et de campagnes.

**Liste** : une liste est extraite à partir d’un segment d’utilisateurs enregistrés. Par exemple, l’emplacement utilisé pour diriger le contenu du paragraphe de teaser.

>[!NOTE]
>
>Voir [Segmentation](/help/sites-administering/campaign-segmentation.md) pour plus d’informations sur les segments dans Adobe Experience Manager.
