---
title: Publication de pages
description: Une fois que vous avez créé et révisé votre contenu dans l’environnement de création, rendez-le disponible sur votre site web public.
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 43%

---

# Publication de pages{#publishing-pages}

Après avoir créé et révisé votre contenu dans l’environnement de création, rendez-le disponible sur votre site web public (votre environnement de publication).

On parle alors de publication d’une page. Lorsque vous souhaitez supprimer une page de l’environnement de publication, on parle d’annulation de publication. Lorsque vous publiez et annulez la publication, la page reste disponible dans l’environnement de création pour d’autres modifications jusqu’à ce que vous la supprimiez.

Vous pouvez également publier/annuler la publication d’une page immédiatement ou à une date/heure prédéfinies.

>[!NOTE]
>
>Certains termes liés à la publication peuvent être déroutés :
>
>* **Publier/dépublier**
   >  Termes principalement utilisés pour évoquer les opérations qui rendent votre contenu publiquement accessible dans votre environnement de publication (ou non).
>
>* **Activer/Désactiver**
   >  Ces termes sont synonymes de publication/dépublication.
>
>* **Répliquer/Réplication**
   >  Termes techniques indiquant le déplacement des données (contenu de la page, fichiers, code et commentaires de l’utilisateur, par exemple) d’un environnement à un autre ; lors de la publication ou de la réplication inverse des commentaires utilisateur, par exemple.
>


>[!NOTE]
>
>Si vous ne disposez pas des privilèges requis pour publier une page spécifique :
>
>* Un workflow sera déclenché pour informer la personne appropriée de votre demande de publication.
>* Un message vous en informera (pendant une courte période).
>


## Publication d’une page {#publishing-a-page}

Il existe deux méthodes pour activer une page :

* [depuis la console Sites web ;](#activating-a-page-from-the-websites-console)
* [depuis le sidekick sur la page elle-même.](#activating-a-page-from-sidekick)

>[!NOTE]
>
>Vous pouvez également activer une sous-arborescence de plusieurs pages à l’aide de l’option [Activer l’arborescence](#howtoactivateacompletesectiontreeofyourwebsite) sur la console Outils.

### Activation d’une page à partir de la console Sites web {#activating-a-page-from-the-websites-console}

Vous pouvez activer des pages dans la console Sites web . Après avoir ouvert une page et modifié son contenu, vous revenez à la console Sites web :

1. Dans la console Sites web , sélectionnez la page à activer.
1. Sélectionner **Activer**, dans le menu supérieur ou dans le menu déroulant de l’élément de page sélectionné.

   Pour activer le contenu de la page et toutes ses pages secondaires, utilisez la console [**Outils**](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >Si nécessaire, AEM demande d’activer ou de réactiver les ressources liées à la page. Vous pouvez cocher ou décocher les cases pour activer ces ressources.

1. Si nécessaire, AEM demande d’activer ou de réactiver les ressources liées à la page. Vous pouvez cocher ou décocher les cases pour activer ces ressources.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM active le contenu sélectionné. La ou les pages publiées s’affichent dans la [Console Sites web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) (en vert) avec des informations sur l’utilisateur qui a activé le contenu, ainsi que la date et l’heure d’activation.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Activation d’une page à partir du sidekick {#activating-a-page-from-sidekick}

Vous pouvez également activer une page lorsqu’elle est ouverte pour modification.

Après avoir ouvert la page et modifié son contenu, vous pouvez :

1. Sélectionnez la **Page** dans le sidekick.
1. Cliquez sur **Activer la page**.
Un message s’affiche dans le coin supérieur droit de la fenêtre pour confirmer l’activation de la page.

## Annulation de la publication d’une page {#unpublishing-a-page}

Pour supprimer une page de l’environnement de publication, désactivez le contenu.

Pour désactiver une page :

1. Dans la console Sites web , sélectionnez la page à désactiver.
1. Sélectionner **Désactiver**, dans le menu supérieur ou dans le menu déroulant de l’élément de page sélectionné. Vous êtes invité à confirmer la suppression.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. Actualisez la [console Sites web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) et le contenu est marqué en rouge, ce qui indique qu’il n’est plus publié.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## Activer/Désactiver ultérieurement {#activate-deactivate-later}

### Activer plus tard {#activate-later}

Pour planifier l’activation à une heure ultérieure :

1. Dans la console Sites web, accédez au menu **Activer** et sélectionnez ensuite **Activer plus tard**.
1. Dans la boîte de dialogue qui s’ouvre, indiquez la date et l’heure d’activation, puis cliquez sur **OK**. Ceci crée une version de la page qui sera activée à l’heure spécifiée.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

L’activation différée lance un workflow pour activer cette version de la page à l’heure indiquée. A l’inverse, la désactivation différée lance un workflow pour désactiver cette version de la page à un moment précis.

Pour annuler cette activation/désactivation, rendez-vous dans la [console Workflow](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) pour mettre un terme au workflow correspondant.

### Désactiver plus tard {#deactivate-later}

Pour planifier la désactivation à une heure ultérieure :

1. Dans la console Sites Web, accédez au menu **Désactiver** et sélectionnez **Désactiver plus tard**.

1. Dans la boîte de dialogue qui s’ouvre alors, indiquez la date et l’heure de désactivation, puis cliquez sur **OK**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**Désactivation tardive** ou lance un workflow pour désactiver cette version de la page à une heure spécifique.

Pour annuler cette désactivation, rendez-vous dans la [console Workflow](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) pour mettre un terme au workflow correspondant.

## Activation/désactivation planifiée (heure d’activation/de désactivation) {#scheduled-activation-deactivation-on-off-time}

Pour programmer les heures de publication/dépublication d’une page, utilisez les options **Heure d’activation** et **Heure de désactivation** dans les [Propriétés de la page](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### Définition du statut de publication de la page {#determining-page-publication-status-classic-ui}

L’état est visible à partir du [Console Sites web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). Les couleurs indiquent l’état de publication.

## Activation d’une section (arborescence) complète de votre site web {#activating-a-complete-section-tree-of-your-website}

Dans la **Sites web** vous pouvez activer les pages individuelles. Lorsque vous avez saisi ou mis à jour un nombre considérable de pages de contenu (toutes résidant sous la même page racine), il peut s’avérer plus facile d’activer l’arborescence entière en une seule action. Vous pouvez également exécuter une exécution d’essai pour émuler une activation et mettre en surbrillance les pages qui seront activées.

1. Ouvrez la console **Outils** en la sélectionnant sur la page **Bienvenue** et en double-cliquant ensuite sur **Réplication** pour ouvrir la console (`https://localhost:4502/etc/replication.html`).

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. Dans la console **Réplication**, cliquez sur **Activer l’arborescence**.

   La fenêtre suivante (`https://localhost:4502/etc/replication/treeactivation.html`) s’affiche.

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. Entrez le **Chemin de début**. Ceci permet de spécifier le chemin d’accès à la racine de la section à activer (publier). Cette page, et toutes les pages sous-jacentes, sont prises en compte pour l’activation (ou utilisées dans le cadre de l’émulation si une Exécution d’essai est sélectionnée).
1. Activez les critères de sélection suivant vos besoins :

   * **Modifié uniquement**: active uniquement les pages qui ont été modifiées.
   * **Activé uniquement**: active uniquement les pages qui ont (déjà) été activées. Cette option agit, en quelque sorte, comme une réactivation.
   * **Ignorer désactivé**: ignorer les pages qui ont été désactivées.

1. Sélectionnez l’action à effectuer :

   1. Sélectionnez **Exécution d’essai** pour vérifier quelles pages *devraient* être activées. Il s’agit seulement d’une émulation, aucune page ne sera activée.

   1. Sélectionnez **Activer** pour activer les pages.
