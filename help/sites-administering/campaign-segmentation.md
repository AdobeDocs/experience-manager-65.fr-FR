---
title: Configurer la segmentation
description: Découvrir comment configurer la segmentation pour AEM Campaign.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 100%

---


# Configurer la segmentation {#configuring-segmentation}

>[!NOTE]
>
>Ce document traite de la configuration de la segmentation telle qu’utilisée avec ClientContext. Pour configurer des segments avec ContextHub à l’aide de l’interface utilisateur tactile, consultez [Configuration de la segmentation avec ContextHub](/help/sites-administering/segmentation.md).

La segmentation est un élément clé de la création d’une campagne. Voir [Glossaire de la segmentation](/help/sites-authoring/segmentation-overview.md) pour plus d’informations sur le fonctionnement de la segmentation et les mots clés.

En fonction des informations que vous avez déjà collectées sur les visiteurs et visiteuses de votre site et des objectifs que vous souhaitez atteindre, vous devez définir les segments et les stratégies requis pour votre contenu ciblé.

Ces segments sont ensuite utilisés pour fournir aux visiteurs et aux visiteuses du contenu spécifiquement ciblé. Ce contenu est conservé dans la section [Campagnes](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) du site web. Les pages Teaser définies ici peuvent être ajoutées en tant que paragraphe teaser sur n’importe quelle page et définissent à quel segment de visiteurs le contenu spécialisé s’applique.

AEM vous permet de facilement créer et mettre à jour des segments, des teasers et des campagnes. Il vous permet également de vérifier les résultats de vos définitions.

**L&#39;éditeur de segment** vous permet de définir facilement un segment :

![Fenêtre de l’éditeur de segments](assets/segmenteditor.png)

Vous pouvez **Modifier** chaque segment pour spécifier un facteur **Titre**, **Description** et **Amplifier**. À l’aide du sidekick, vous pouvez ajouter des conteneurs **ET** et **OU** pour définir la **Logique de segment**, puis ajouter les **Caractéristiques de segment** pour définir les critères de sélection.

## Facteur d’amplification {#boost-factor}

Chaque segment comporte un paramètre **Amplifier** utilisé comme un facteur de pondération : une valeur plus élevée indique que le segment sera sélectionné de préférence à un segment présentant une valeur plus faible.

* Valeur minimale : `0`
* Valeur maximale : `1000000`

## Logique de segment {#segment-logic}

Les conteneurs logiques suivants sont disponibles clé en main et vous permettent de créer la logique de votre sélection de segments. Ils peuvent être déplacés du sidekick vers l’éditeur :

<table>
 <tbody>
  <tr>
   <td> Conteneur ET<br /> </td>
   <td> Opérateur ET booléen.<br /> </td>
  </tr>
  <tr>
   <td> Conteneur OU<br /> </td>
   <td> Opérateur OU booléen.</td>
  </tr>
 </tbody>
</table>

## Caractéristiques de segment {#segment-traits}

Les caractéristiques de segment suivantes sont disponibles et prêtes à l’emploi ; elles peuvent être glissées du sidekick vers l’éditeur :

<table>
 <tbody>
  <tr>
   <td> Plage d’adresses IP<br /> </td>
   <td>Définit une plage d’adresses IP que le visiteur peut avoir.<br /> </td>
  </tr>
  <tr>
   <td> Accès à la page<br /> </td>
   <td>Fréquence à laquelle la page a été demandée. <br /> </td>
  </tr>
  <tr>
   <td> Propriété de page<br /> </td>
   <td>Toute propriété de la page visitée.<br /> </td>
  </tr>
  <tr>
   <td> Mots-clés de référence<br /> </td>
   <td>Mots-clés à associer aux informations du site web de référence. <br /> </td>
  </tr>
  <tr>
   <td> Script</td>
   <td>Expression JavaScript à évaluer.<br /> </td>
  </tr>
  <tr>
   <td> Référence de segment <br /> </td>
   <td>Référence à une autre définition de segment.<br /> </td>
  </tr>
  <tr>
   <td> Nuage de balises<br /> </td>
   <td>Balises à associer à celles des pages visitées.<br /> </td>
  </tr>
  <tr>
   <td> Âge de l’utilisateur<br /> </td>
   <td>Extrait du profil utilisateur.<br /> </td>
  </tr>
  <tr>
   <td> Propriété de l’utilisateur<br /> </td>
   <td>Toute autre information disponible dans le profil utilisateur. </td>
  </tr>
 </tbody>
</table>

Vous pouvez combiner ces caractéristiques avec les opérateurs booléens OU et ET (voir la rubrique [Création d’un nouveau segment](#creating-a-new-segment)) afin de définir le scénario exact pour sélectionner ce segment.

Lorsque l’intégralité de l’instruction est vraie, alors ce segment a été résolu. S’il existe plusieurs segments applicables, le facteur **[Boost](/help/sites-administering/campaign-segmentation.md#boost-factor)** est également utilisé. 

>[!CAUTION]
>
>L’éditeur de segment ne vérifie aucune référence circulaire. Par exemple, le segment A fait référence à un autre segment B, qui à son tour fait référence au segment A. Vous devez vous assurer que vos segments ne contiennent aucune référence circulaire.

>[!NOTE]
>
>Les propriétés comportant le suffixe **_i18n** sont définies par un script faisant partie de la bibliothèque cliente d’interface utilisateur des personnalisations. Toutes les bibliothèques clientes liées à l’interface utilisateur sont chargées à la création uniquement, car l’interface utilisateur n’est pas nécessaire lors de la publication.
>
>Par conséquent, lors de la création d’un segment avec ces propriétés, il est normalement nécessaire de faire appel à **browserFamily**, par exemple, au lieu de **browserFamily_i18n**.

### Création d’un segment {#creating-a-new-segment}

Pour définir votre nouveau segment :

1. Dans le rail, choisissez **Outils > Opérations > Configuration**.
1. Cliquez sur le bouton **Segmentation** dans le volet de gauche, puis accédez à l’emplacement requis.
1. Créez [une nouvelle page](/help/sites-authoring/editing-content.md#creatinganewpage) à l’aide du modèle de **Segment**.
1. Ouvrez la nouvelle page pour afficher l’éditeur de segments :

   ![Première étape de la création d’un segment dans l’éditeur de segment](assets/screen_shot_2012-02-02at101726am.png)

1. Utilisez le sidekick ou le menu contextuel (en général, cliquez avec le bouton droit de la souris, puis sélectionnez **Nouveau** pour ouvrir la fenêtre Insérer un nouveau composant) et recherchez la caractéristique de segment dont vous avez besoin. Puis faites-le glisser sur **l&#39;éditeur de segment** il apparaît dans le conteneur **ET** par défaut.
1. Double-cliquez sur la nouvelle caractéristique pour modifier les paramètres spécifiques, par exemple la position de la souris :

   ![Modification d’un composant dans l’éditeur de segment](assets/screen_shot_2012-02-02at103135am.png)

1. Cliquez sur **OK** pour enregistrer vos modifications :
1. Vous pouvez **Modifier** le segment afin de lui donner un facteur **Titre**, **Description** et **[Amplification](#boost-factor)** :

   ![Modification des paramètres de segment dans l’éditeur de segment](assets/screen_shot_2012-02-02at103547am.png)

1. Ajoutez des caractéristiques si nécessaire. Vous pouvez formuler des expressions booléennes à l’aide des composants **Conteneur ET** et **Conteneur OU** figurant dans **Logique de segment**. Avec l’éditeur de segment, vous pouvez supprimer les caractéristiques ou les conteneurs qui ne sont plus nécessaires ou les faire glisser vers de nouveaux emplacements dans l’instruction.

### Utilisation des conteneurs ET et OU {#using-and-and-or-containers}

Vous pouvez créer des segments complexes dans AEM. Il est utile de tenir compte de quelques points de base :

* Le niveau supérieur de la définition est toujours le conteneur AND qui est initialement créé ; cela n’est pas modifiable, mais n’a pas d’effet sur le reste de votre définition de segment.
* Assurez-vous que l’imbrication de votre conteneur a un sens. Les conteneurs peuvent être considérés comme des crochets de votre expression booléenne.

L’exemple suivant permet de sélectionner les visiteurs et les visiteuses qui sont soit :

Des hommes et qui ont entre 16 et 65 ans

OU

Des femmes et qui ont entre 16 et 62 ans

Puisque l’opérateur principal est OU, vous devez commencer par le **Conteneur OU**. Vous y trouverez 2 instructions ET, pour chacune d’elles, vous avez besoin d’un **Conteneur ET**, dans lequel vous pouvez ajouter les caractéristiques individuelles.

![Exemple d’opérateurs ET et OU dans l’éditeur de segments](assets/screen_shot_2012-02-02at105145am.png)

## Test de l’application d’un segment {#testing-the-application-of-a-segment}

Une fois le segment défini, les résultats potentiels peuvent être testés avec le **[Contexte client](/help/sites-administering/client-context.md)** :

1. Sélectionnez le segment à tester.
1. Appuyez sur les touches **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** pour ouvrir le **[ClientContext](/help/sites-administering/client-context.md)**, qui affiche les données collectées. À des fins de test, vous pouvez **Modifier** certaines valeurs ou **Charger** un autre profil pour y voir l’impact.

1. En fonction des caractéristiques définies, les données disponibles pour la page en cours peuvent ou non correspondre à la définition de segment. Le statut de la correspondance s’affiche sous la définition.

Par exemple, une seule définition de segment peut être fonction de l’âge et du sexe de l’utilisateur. Le chargement d’un profil spécifique indique que le segment a été résolu avec succès :

![Utilisation de la fenêtre Contexte client pour tester une opération de segmentation ET](assets/screen_shot_2012-02-02at105926am.png)

Ou non :

![Utilisation de la fenêtre Contexte client pour tester une opération de segmentation NON](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Toutes les caractéristiques sont résolues immédiatement, bien que la plupart ne soient modifiées qu’au rechargement de la page. Les modifications apportées à la position de la souris sont immédiatement visibles, ce qui s’avère utile à des fins de test.

Ces tests peuvent également s’effectuer sur les pages de contenu et en combinaison avec des composants **Teaser**.

Pointez sur un paragraphe de teaser pour voir si les segments appliqués sont actuellement résolus et, par conséquent, pourquoi l’instance de teaser actuelle a été sélectionnée :

![Exemple de pointeur de souris sur un segment](assets/chlimage_1-47.png)

### Utilisation de votre segment {#using-your-segment}

Les segments sont actuellement utilisés dans les [campagnes](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Ils sont utilisés afin d’orienter le contenu réel affiché pour des audiences cible spécifiques. Voir [Présentation des segments](/help/sites-authoring/segmentation-overview.md) pour plus d’informations.
