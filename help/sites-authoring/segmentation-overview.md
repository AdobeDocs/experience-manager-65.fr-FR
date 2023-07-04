---
title: Comprendre la segmentation lors de la création d’une campagne
description: La segmentation est un élément clé de la création d’une campagne.
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---

# Compréhension de la segmentation{#understanding-segmentation}

La segmentation est un élément clé de la création d’une campagne. Dans la plupart des cas, les segments doivent être déjà définis avant le démarrage de votre campagne.

Les visiteurs et visiteuses de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. La compréhension des objectifs et la satisfaction des attentes des visiteurs et visiteuses est un important facteur de réussite en matière de marketing en ligne.

La segmentation permet d’y parvenir en analysant et en profilant :

* l’activité du visiteur ou de la visiteuse sur le site web
* son profil
* l’activité du visiteur ou de la visiteuse sur d’autres sites web

Le contenu peut alors cibler les besoins et centres d’intérêts spécifiques des visiteurs et visiteuses en fonction du ou des segments qui leur correspondent.

## Utilisation de la segmentation {#using-segmentation}

Les segments sont définis dans la section [Configuration de la segmentation](/help/sites-administering/campaign-segmentation.md). Ils sont utilisés afin d’orienter le contenu réel affiché pour une audience cible spécifique.

## Terminologie de la segmentation {#segmentation-terminology}

Lors de la discussion de la segmentation, la terminologie suivante est utilisée :

**Visiteur** : un visiteur est une personne qui visite un site web. La visite de cette personne commence généralement à partir d’une page de référence, puis passe à une ou plusieurs vues de pages sur votre propre site web. Un profil comportemental peut être créé à partir des détails de la visite de cette personne.

**Utilisateur** : un utilisateur est un visiteur qui s’inscrit auprès du site web pour recevoir un profil de compte. Pour générer leur profil, ils fournissent une identification supplémentaire, telle qu’une adresse e-mail et un genre, entre autres. Des informations supplémentaires peuvent également être collectées, notamment l’activité de la communauté et les modèles d’achat, entre autres. En fonction des informations fournies dans le profil, un profil démographique peut être créé.

**Caractéristique** : une caractéristique est une particularité ou une propriété d’un visiteur qui peut être utilisée pour déterminer son appartenance à un segment spécifique.

**Segment** : un segment est un groupe de visiteurs qui partagent certaines caractéristiques. Les segments doivent être distincts, avec un minimum de chevauchement avec les autres segments.

**Caractéristiques comportementales** : les caractéristiques comportementales sont liées au comportement d’un visiteur sur le site web. Ces informations comprennent les éléments suivants :

* L’intérêt au sein de votre site web ; notamment les pages visitées et les produits achetés.
* L’intérêt sur le site web de référence ; notamment les termes de recherche utilisés ou les publicités cliquées.
* L’intérêt sur d’autres sites, déterminé à l’aide d’outils tels que Spyjax.
* La fidélité du visiteur ou de la visiteuse ; la durée de la visite, la fréquence des visites.

**Caractéristiques démographiques** : il s’agit de caractéristiques de population choisies, notamment :

* Âge
* Revenu
* Taille de la famille
* Statut matrimonial
* Genre
* Emplacement

**Caractéristiques dérivées** : certaines caractéristiques démographiques sont difficiles à déterminer sans inscription, mais peuvent être extraites en combinant les caractéristiques comportementales et démographiques.

Par exemple, la combinaison de l’URL de référence (en tant que caractéristique comportementale) avec des données démographiques (acquises à partir d’outils tels que [Google Ad Planner](https://www.google.com/adplanner/)) permet aux propriétaires du site d’extraire les caractéristiques comportementales de leurs visiteurs.

**Sous-segment** : un segment peut être divisé en plusieurs sous-segments. Ceci s’effectue en définissant des caractéristiques supplémentaires.

**Page de teaser** : une page de teaser est conçue à l’intention d’une audience spécifique. Elle contient du contenu réutilisable qui peut être utilisé dans le paragraphe de teaser.

**Campagne** : une campagne est une collection de pages de teaser et de pages de marketing par e-mail, comme des newsletters ou des invitations. Typiquement, une campagne dure pendant une période limitée, puis elle est remplacée par une autre campagne.

**Paragraphe de teaser** : il s’agit d’un paragraphe qui extrait du contenu d’une autre page selon une stratégie de sélection. Cette stratégie de sélection peut tenir compte de segments et de campagnes.

**Liste** : une liste est extraite à partir d’un segment d’utilisateurs enregistrés. Par exemple, l’emplacement utilisé pour diriger le contenu du paragraphe de teaser.

>[!NOTE]
>
>Pour plus d’informations sur les segments dans AEM, consultez la section [Segmentation](/help/sites-administering/campaign-segmentation.md).
