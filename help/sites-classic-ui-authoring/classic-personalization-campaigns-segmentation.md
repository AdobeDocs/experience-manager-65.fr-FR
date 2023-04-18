---
title: Compréhension de la segmentation
description: La segmentation est un élément clé de la création d’une campagne. Dans la plupart des cas, les segments doivent être déjà définis avant de démarrer votre campagne.
uuid: 609d83b3-df0e-44ad-8e27-90b676d2666b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bb75f4ab-d983-45f6-98a3-da8bd9b63751
exl-id: 9092977b-b558-42a3-8092-4615fbc0a08e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 61%

---

# Compréhension de la segmentation{#understanding-segmentation}

La segmentation est un élément clé de la création d’une campagne. Dans la plupart des cas, les segments doivent être déjà définis avant de démarrer votre campagne.

Les visiteurs du site ont des intérêts et des objectifs différents lorsqu’ils se rendent sur un site. Comprendre ces objectifs et répondre aux attentes est un facteur de réussite important pour le marketing en ligne.

La segmentation permet d’y parvenir en analysant et en caractérisant les éléments suivants d’un visiteur :

* activité sur le site web
* son profil
* activité sur d’autres sites web

Le contenu peut ensuite être spécifiquement ciblé sur les besoins et centres d’intérêt du visiteur, en fonction du ou des segments correspondants.

## Utilisation de la segmentation {#using-segmentation}

Les segments sont définis dans [Configuration de la segmentation](/help/sites-administering/campaign-segmentation.md). Ils sont utilisés afin d’orienter le contenu réel affiché pour une audience cible spécifique.

## Terminologie de la segmentation {#segmentation-terminology}

Lors de la discussion de la segmentation, la terminologie suivante est utilisée :

**Visiteur** : un visiteur est une personne qui visite un site web. La visite de cette personne commence généralement à partir d’une page de référence, puis passe à une ou plusieurs pages vues sur votre propre site web. Un profil comportemental peut être créé à partir des détails de la visite de cette personne.

**Utilisateur** : un utilisateur est un visiteur qui s’inscrit auprès du site web pour recevoir un profil de compte. Pour générer leur profil, ils fournissent une identification supplémentaire, telle qu’une adresse email et un genre, entre autres. Des informations supplémentaires peuvent également être collectées, notamment l’activité de la communauté et les modèles d’achat, entre autres. En fonction des informations fournies dans le profil, un profil démographique peut être créé.

**Caractéristique** : une caractéristique est une particularité ou une propriété d’un visiteur qui peut être utilisée pour déterminer son appartenance à un segment spécifique.

**Segment** : un segment est un groupe de visiteurs qui partagent certaines caractéristiques. Les segments doivent être distincts, avec un minimum de chevauchement avec les autres segments.

**Caractéristiques comportementales** : les caractéristiques comportementales sont liées au comportement d’un visiteur sur le site web. Ces informations comprennent les éléments suivants :

* L’intérêt au sein de votre site web ; notamment les pages visitées et les produits achetés.
* L’intérêt sur le site web de référence ; notamment les termes de recherche utilisés ou les publicités cliquées.
* L’intérêt sur d’autres sites, déterminé à l’aide d’outils tels que Spyjax.
* la fidélité des visiteurs ; durée de la visite, fréquence des visites.

**Caractéristiques démographiques** : il s’agit de caractéristiques de population choisies, notamment :

* Age
* Revenu
* Taille de la famille
* État civil
* Sexe
* Emplacement

**Caractéristiques dérivées**  

Certaines caractéristiques démographiques sont difficiles à déterminer sans inscription, mais peuvent être dérivées en combinant les caractéristiques comportementales et démographiques.

Par exemple, la combinaison de l’URL de référence (en tant que caractéristique comportementale) avec des données démographiques (acquises à partir d’outils tels que [Google Ad Planner](https://www.google.com/adplanner/)) permet aux propriétaires du site d’extraire les caractéristiques comportementales de leurs visiteurs.

**Sous-segment** : un segment peut être divisé en plusieurs sous-segments. Ceci s’effectue en définissant des caractéristiques supplémentaires.

**Page de teaser** : une page de teaser est conçue à l’intention d’une audience spécifique. Elle contient du contenu réutilisable qui peut être utilisé dans le paragraphe de teaser.

**Campagne** : une campagne est une collection de pages de teaser et de pages de marketing par e-mail, comme des newsletters ou des invitations. Typiquement, une campagne dure pendant une période limitée, puis elle est remplacée par une autre campagne.

**Paragraphe de teaser** : il s’agit d’un paragraphe qui extrait du contenu d’une autre page selon une stratégie de sélection. Cette stratégie de sélection peut tenir compte de segments et de campagnes.

**Liste** : une liste est extraite à partir d’un segment d’utilisateurs enregistrés. Par exemple, l’emplacement utilisé pour diriger le contenu du paragraphe de teaser.

>[!NOTE]
>
>Pour plus d’informations sur les segments dans AEM, consultez la section [Segmentation](/help/sites-administering/campaign-segmentation.md).
