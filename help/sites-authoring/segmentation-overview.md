---
title: Comprendre la segmentation lors de la création d’une campagne
description: La segmentation est un élément clé de la création d’une campagne.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 77%

---

# Compréhension de la segmentation{#understanding-segmentation}

La segmentation est un élément clé de la création d’une campagne. En règle générale, les segments doivent être déjà définis avant de démarrer votre campagne.

Les visiteurs et visiteuses de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. La compréhension des objectifs et la satisfaction des attentes des visiteurs et visiteuses est un important facteur de réussite en matière de marketing en ligne.

La segmentation permet d’y parvenir en analysant et en profilant :

* l’activité du visiteur ou de la visiteuse sur le site web
* son profil
* l’activité du visiteur ou de la visiteuse sur d’autres sites web

Le contenu peut ensuite être ciblé en fonction des besoins et des centres d’intérêt du visiteur, selon les segments correspondants.

## Utilisation de la segmentation {#using-segmentation}

Les segments sont définis dans la section [Configuration de la segmentation](/help/sites-administering/campaign-segmentation.md). Ils sont utilisés afin d’orienter le contenu réel affiché pour une audience cible spécifique.

## Terminologie de la segmentation {#segmentation-terminology}

Lors de la discussion de la segmentation, la terminologie suivante est utilisée :

**Visiteur** : un visiteur est une personne qui visite un site web. La visite de cette personne commence généralement à partir d’une page de référence, puis passe à une ou plusieurs vues de pages sur votre propre site web. Un profil comportemental peut être créé à partir des détails de la visite de cette personne.

**Utilisateur** : un utilisateur est un visiteur qui s’inscrit auprès du site web pour recevoir un profil de compte. Pour générer leur profil, ils fournissent une identification supplémentaire, telle qu’une adresse email et un genre, entre autres. Des informations supplémentaires peuvent également être collectées, notamment l’activité de la communauté et les modèles d’achat, entre autres. En fonction des informations fournies dans le profil, un profil démographique peut être créé.

**Caractéristique** : une caractéristique est une particularité ou une propriété d’un visiteur qui peut être utilisée pour déterminer son appartenance à un segment spécifique.

**Segment** : un segment est un groupe de visiteurs qui partagent certaines caractéristiques. Les segments doivent être distincts, avec un minimum de chevauchement avec les autres segments.

**Caractéristiques comportementales** : les caractéristiques comportementales sont liées au comportement d’un visiteur sur le site web. Ces informations comprennent les éléments suivants :

* L’intérêt au sein de votre site web ; notamment les pages visitées et les produits achetés.
* les intérêts sur le site web de référence ; y compris les termes de recherche utilisés ou les publicités sur lesquelles l’utilisateur a cliqué.
* L’intérêt sur d’autres sites, déterminé à l’aide d’outils tels que Spyjax.
* La fidélité du visiteur ; la durée de la visite, la fréquence des visites.

**Caractéristiques démographiques** : il s’agit de caractéristiques de population choisies, notamment :

* Âge
* Revenu
* Taille de la famille
* Statut matrimonial
* Genre
* Emplacement

**Caractéristiques dérivées** : certaines caractéristiques démographiques sont difficiles à déterminer sans inscription, mais peuvent être extraites en combinant les caractéristiques comportementales et démographiques.

Par exemple, la combinaison de l’URL de référence (en tant que caractéristique comportementale) avec des données démographiques (acquises à partir d’outils tels que [Google Ad Planner](https://www.google.com/adplanner/)) permettent aux propriétaires de site d’extraire les caractéristiques démographiques de leurs visiteurs.

**Sous-segment** : un segment peut être divisé en plusieurs sous-segments. Ceci s’effectue en définissant des caractéristiques supplémentaires.

**Page de teaser** : une page de teaser est conçue à l’intention d’une audience spécifique. Il contient du contenu réutilisable pouvant être utilisé dans le paragraphe de teaser.

**Campagne** : une campagne est une collection de pages de teaser et de pages de marketing par e-mail, comme des newsletters ou des invitations. Normalement, la campagne s’étend sur une période limitée, puis elle est remplacée par une autre campagne.

**Paragraphe de teaser** : il s’agit d’un paragraphe qui extrait du contenu d’une autre page selon une stratégie de sélection. Cette stratégie de sélection peut tenir compte de segments et de campagnes.

**Liste** : une liste est extraite à partir d’un segment d’utilisateurs enregistrés. Par exemple, l’emplacement utilisé pour diriger le contenu du paragraphe de teaser.

>[!NOTE]
>
>Voir [Segmentation](/help/sites-administering/campaign-segmentation.md) pour plus d’informations sur les segments dans Adobe Experience Manager.
