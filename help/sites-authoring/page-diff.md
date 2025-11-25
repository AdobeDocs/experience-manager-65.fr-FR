---
title: Outil de comparaison des pages
description: De fait, l’outil de comparaison des pages permet d’afficher côte à côte deux pages pour les comparer en mettant en évidence leurs différences.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 100%

---

# Outil de comparaison des pages{#page-diff}

## Présentation {#introduction}

La création de contenu est un processus itératif. Pour être efficace lorsque vous créez du contenu, vous devez pouvoir voir ce qui a changé d’une version à l’autre. L’affichage d’une version de page, puis de l’autre, est inefficace et source d’erreurs. Un créateur ou une créatrice doit pouvoir facilement comparer la page actuelle à côté d’une autre version.

De fait, l’outil de comparaison des pages permet d’afficher côte à côte deux pages pour les comparer en mettant en évidence leurs différences.

>[!TIP]
>
>Consultez la section consacrée à l’[outil de comparaison des pages](/help/sites-developing/pagediff.md#operation-details) pour plus d’informations sur cette fonction.

## Utilisez {#use}

L’outil de comparaison côte à côte permet de comparer les éléments suivants :

* [Versions](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) : la version actuelle d’une page et sa version antérieure.
* [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) : une Live Copy et son plan directeur
* [Lancements](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) : un lancement et sa source
* [Copies de langue](/help/sites-administering/tc-manage.md#comparing-language-copies) : une page avant et après (re)traduction

Reportez-vous aux rubriques correspondantes afin de connaître la procédure de comparaison pour ces différents éléments.

### Présentation des différences {#presentation-of-differences}

Quel que soit le contenu comparé, la présentation des différences reste la même.

* Le contenu sélectionné au démarrage de l’outil de comparaison s’affiche à gauche (le point d’entrée de l’outil de comparaison).
* Le contenu de la comparaison est affiché à droite (ce qui est comparé au contenu sélectionné).

Par exemple, si vous comparez des versions, la version actuelle est affichée à gauche et la version précédente à droite.

La source des deux pages s’affiche clairement dans la barre d’en-tête située en haut de la fenêtre du navigateur.

![Source affichée dans l&#39;en-tête](assets/chlimage_1-109.png)

L’outil de comparaison détecte les modifications effectuées sur les composants et le code HTML. Les éléments qui ont été modifiés sont mis en surbrillance avec des couleurs différentes.

**Modifications des composants**

* Vert clair : composant ajouté
* Rose : composant supprimé

**Modifications du code HTML**

* Vert foncé : HTML ajouté
* Rouge : HTML supprimé

>[!NOTE]
>
>Lorsque vous comparez des copies de langue, la mise en surbrillance est désactivée. En effet, dans la mesure où la traduction modifie tout le contenu, la mise en surbrillance ne présente aucun intérêt.

### Affichage en mode plein écran {#fullscreen-and-exiting}

Si vous souhaitez vous concentrer sur un contenu spécifique, vous pouvez cliquer sur l’icône du mode plein écran pour l’un ou l’autre des deux « côtés » de votre comparaison. Cela vous permet d’afficher la version en plein écran dans la fenêtre du navigateur.

![Icône du mode Plein écran](do-not-localize/chlimage_1-18.png)

Le côté sélectionné s’affiche dans la totalité de la fenêtre, mais la barre d’en-tête reste disponible en haut de la fenêtre pour vous permettre de basculer d’une page à l’autre si vous le souhaitez.

![La barre supérieure permet de basculer entre les pages.](assets/chlimage_1-110.png)

Vous pouvez également quitter le mode plein écran en cliquant sur l’icône de fermeture du mode plein écran.

![Fermer le mode Plein écran](do-not-localize/chlimage_1-19.png)

Vous pouvez quitter le mode de comparaison côte à côte à tout moment en cliquant sur le bouton Fermer dans l’en-tête.

## Restrictions {#limitations}

Dans certains cas, l’outil de comparaison des pages peut ne pas détecter toutes les différences.

* Lors de la comparaison des versions et des lancements, celle-ci ne prend pas en compte les composants dynamiques tels que les chemins de navigation, les menus, les listes de produits ou les logos (composants qui dépendent de la structure du site pour effectuer le rendu de leur contenu).
* Pour les versions, l’outil de comparaison ne recrée pas la politique de contrôle d’accès ni les relations Live Copy.
* Si une page a été déplacée, vous ne pouvez plus la comparer à des versions antérieures au déplacement.

   * Si vous rencontrez des problèmes liés à une comparaison, vérifiez la [Chronologie](/help/sites-authoring/basic-handling.md#timeline) de la page afin de voir si la page a été déplacée.

>[!NOTE]
>
>Les versions ne peuvent pas être comparées entre elles. Seule la version en cours peut être comparée aux autres versions de la page. La version dont les modifications sont mises en surbrillance est toujours la version en cours.

>[!NOTE]
>
>Pour plus d’informations sur le fonctionnement de l’outil de comparaison des pages et des limites pouvant affecter cette comparaison, consultez la [documentation de développement](/help/sites-developing/pagediff.md) liée à cette fonctionnalité.
