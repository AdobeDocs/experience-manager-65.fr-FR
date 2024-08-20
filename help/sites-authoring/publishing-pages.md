---
title: Publication de pages de contenu
description: Découvrez comment publier des pages de contenu dans Adobe Experience Manager 6.5.
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 6f3c4f4aa4183552492c6ce5039816896bd67495
workflow-type: ht
source-wordcount: '1669'
ht-degree: 100%

---

# Publication de pages {#publishing-pages}

Une fois le contenu créé et révisé dans l’environnement de création, [vous devez le rendre disponible sur votre site web public](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) (votre environnement de publication).

On parle alors de publication d’une page. Lorsque vous souhaitez supprimer une page de l’environnement de publication, on parle de dépublication. Lorsque vous publiez et dépubliez, la page reste disponible dans l’environnement de création pour d’autres modifications jusqu’à ce que vous la supprimiez.

Vous pouvez publier/dépublier une page tout de suite ou à une date/heure postérieures prédéfinies.

>[!NOTE]
>
>Certains termes liés à la publication peuvent être déroutants :
>
>* **Publier/dépublier**
>  Termes principalement utilisés pour évoquer les opérations qui rendent votre contenu publiquement accessible dans votre environnement de publication (ou non).
>
>* **Activer/Désactiver**
>  Ces termes sont synonymes de publication/dépublication.
>
>* **Répliquer/Réplication**
>  Termes techniques indiquant le déplacement des données (contenu de la page, fichiers, code et commentaires de l’utilisateur, par exemple) d’un environnement à un autre ; lors de la publication ou de la réplication inverse des commentaires utilisateur, par exemple.

## Privilèges insuffisants {#insufficient-privileges}

Si vous ne disposez pas des privilèges requis pour publier une page spécifique :

* Un workflow sera déclenché pour informer la personne appropriée de votre demande de publication.
* Ce [workflow a peut-être été personnalisé](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) par votre équipe de développement.
* Un message s’affiche brièvement pour vous informer que le workflow a été déclenché.

## Publication de pages {#publishing-pages-1}

Selon votre emplacement, vous pouvez effectuer la publication :

* [À partir de l’éditeur de page](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [À partir de la console Sites](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### Publication à partir de l’éditeur {#publishing-from-the-editor}

Si vous modifiez une page, vous pouvez la publier directement à partir de l’éditeur.

1. Sélectionnez l’icône **Informations sur la page** pour ouvrir le menu, puis sélectionnez l’option **Publier la page**.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. Selon que la page comporte des références qui doivent être publiées :

   * La page sera publiée directement, s’il n’y a aucune référence à publier.
   * Si la page comporte des références à publier, celles-ci seront répertoriées dans l’assistant **Publier**, où vous pourrez accomplir ce qui suit :

      * Spécifiez les ressources ou les balises à publier conjointement avec la page, puis utilisez **Publier** pour terminer l’opération.

      * Sélectionnez **Annuler** pour abandonner l’opération.

   ![chlimage_1](assets/chlimage_1.png)

1. L’option **Publier** réplique la page dans l’environnement de publication. Une bannière d’informations est affichée dans l’éditeur de page pour confirmer l’opération de publication.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Lorsque vous affichez la même page dans la console, le statut de publication mis à jour est visible.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>Une publication à partir de l’éditeur est dite superficielle ; en d’autres termes, seules la ou les pages sélectionnées sont publiées (les éventuelles pages enfants ne le sont pas).

>[!NOTE]
>
>Les pages accessibles par [alias](/help/sites-authoring/editing-page-properties.md#advanced) dans l’éditeur ne peuvent pas être publiées. Les options de publication dans l’éditeur ne sont disponibles que pour les pages auxquelles vous pouvez accéder à partir de leur chemin d’accès réel.

### Publication à partir de la console {#publishing-from-the-console}

La console Sites propose deux options de publication :

* [Publication rapide](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gérer la publication](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Publication rapide {#quick-publish}

L’option **Publication rapide** concerne les cas simples. Elle publie immédiatement la ou les pages sélectionnées sans aucune autre interaction. Pour cette raison, toutes les références non publiées seront également publiées automatiquement.

Pour publier une page avec publication rapide :

1. Sélectionnez la ou les pages dans la console Sites et cliquez ensuite sur le bouton **Publication rapide**.

   ![pp-02](assets/pp-02.png)

1. Dans la boîte de dialogue Publication rapide, confirmez la publication en cliquant sur **Publier** ou annulez-la en cliquant sur **Annuler**. Pour rappel, toute référence dépubliée sera également publiée automatiquement.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Une fois la page publiée, une alerte s’affiche pour confirmer la publication.

>[!NOTE]
>
>La publication rapide est une publication superficielle, c’est-à-dire que seules la ou les pages sélectionnées sont publiées alors que les pages enfants ne le sont pas.

#### Gérer la publication {#manage-publication}

**Gérer la publication** propose plus d’options que Publication rapide, dont la possibilité d’inclure des pages enfants, de personnaliser les références ou encore de lancer n’importe quel workflow applicable. Elle offre également la possibilité de publier la page à une date ultérieure.

Pour publier ou dépublier une page à l’aide de l’option Gérer la publication :

1. Sélectionnez la ou les pages dans la console Sites, puis cliquez sur le bouton **Gérer la publication**.

   ![pp-02-1](assets/pp-02-1.png)

1. L’assistant **Gérer la publication** démarre. La première étape, **Options**, vous permet d’effectuer les opérations suivantes :

   * Publier ou dépublier des pages sélectionnées.
   * Vous pouvez choisir d’effectuer cette action maintenant ou ultérieurement.

   La publication différée lance un workflow pour publier la ou les pages sélectionnées à un moment précis. A l’inverse, la dépublication différée lance un workflow pour dépublier la ou les pages sélectionnées à un moment précis.

   Pour annuler une publication/dépublier ultérieurement, rendez-vous dans la [console Workflow](/help/sites-administering/workflows.md) pour mettre un terme au workflow correspondant.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Cliquez sur **Suivant** pour continuer.

1. Au cours de l’étape suivante de l’assistant Gérer la publication, **Portée**, vous pouvez définir la portée de la publication ou de l’annulation de la publication ; par exemple, inclure des pages enfants et des références.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   Vous pouvez sélectionner le bouton **Ajouter du contenu** pour ajouter des pages à la liste des pages à publier, au cas où vous auriez omis d’en sélectionner une avant de lancer l’assistant Gérer la publication.

   Le bouton Ajouter du contenu lance l’[explorateur de chemins d’accès](/help/sites-authoring/author-environment-tools.md#path-browser), qui vous permet de sélectionner du contenu.

   Sélectionnez les pages souhaitées, puis cliquez sur **Sélectionner** pour ajouter du contenu à l’assistant ou sur **Annuler** pour annuler la sélection et revenir à l’assistant.

   De retour dans l’assistant, vous pouvez sélectionner un élément de la liste pour configurer ses autres options, telles que :

   * Inclure ses enfants.
   * Le supprimer de la sélection.
   * Gérer ses références publiées.

   ![pp-03](assets/pp-03.png)

   La boîte de dialogue qui s’ouvre lorsque vous cliquez sur **Inclure les enfants** vous permet d’effectuer les opérations suivantes :

   * Inclure seulement les enfants immédiats
   * Inclure seulement les pages modifiées
   * Inclure seulement les pages déjà publiées

   Cliquez sur **Ajouter** pour ajouter les pages enfants à la liste des pages à publier ou dépublier sur la base des options sélectionnées. Cliquez sur **Annuler** pour annuler la sélection et revenir à l’assistant.

   ![chlimage_1-3](assets/chlimage_1-3.png)

   De retour dans l’assistant, les pages ajoutées sont affichées en fonction des options que vous avez sélectionnées dans la boîte de dialogue Inclure les enfants.

   Vous pouvez afficher et modifier les références à publier ou dépublier pour une page. Pour ce faire, sélectionnez la page, puis cliquez sur le bouton **Références publiées**.

   ![pp-04](assets/pp-04.png)

   La boîte de dialogue **Références publiées** affiche alors les références du contenu sélectionné. Par défaut, elles sont toutes sélectionnées. Dès lors, elles seront toutes publiées ou dépubliées. Vous pouvez toutefois les désélectionner pour qu’elles ne soient pas incluses dans l’opération.

   Cliquez sur **Terminé** pour enregistrer vos modifications ou sur **Annuler** pour annuler la sélection et revenir à l’assistant.

   De retour dans l’assistant, la colonne **Références** est mise à jour afin de tenir compte des références que vous avez choisi de publier ou de dépublier.

   ![pp-05](assets/pp-05.png)

1. Pour terminer, cliquez sur **Publier**.

   De retour dans la console Sites, un message de notification s’affiche pour confirmer la publication.

1. Si les pages publiées sont associées à des workflows, elles peuvent être affichées dans une dernière étape de l’assistant de publication intitulée **Workflows**.

   >[!NOTE]
   >
   >L’étape **Workflows** est affichée en fonction des droits dont dispose ou non votre utilisateur ou utilisatrice.
   >
   >Pour plus d’informations, reportez-vous aux sections [Privilèges insuffisants](/help/sites-authoring/publishing-pages.md#insufficient-privileges), [Gérer l’accès aux workflows](/help/sites-administering/workflows-managing.md) et [Appliquer des workflows aux pages](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd).

   Les ressources sont regroupées selon les workflows déclenchés et chaque option donnée pour :

   * Définissez le titre du workflow.
   * conserver le package de workflow, à condition que le workflow dispose d’une [prise en charge multi-ressource](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) ;
   * définir le titre du package de workflow, si l’option de conservation du package de workflow a été sélectionnée.

   Cliquez sur **Publier** ou **Publier ultérieurement** pour terminer la publication.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Dépublication de pages {#unpublishing-pages}

La dépublication d’une page supprime cette page de votre environnement de publication, de sorte que vos lecteurs ne puissent plus y accéder.

Vous pouvez dépublier une ou de plusieurs pages [en procédant de la même manière que pour leur publication](/help/sites-authoring/publishing-pages.md#publishing-pages) :

* [À partir de l’éditeur de page](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [À partir de la console Sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Dépublication à partir de l’éditeur {#unpublishing-from-the-editor}

Lors de la modification d’une page, si vous la dépubliez, sélectionnez **Dépublier la page** dans le menu **Informations sur la page**, comme vous le feriez pour [publier la page](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>Les pages accessibles par [alias](/help/sites-authoring/editing-page-properties.md#advanced) dans l’éditeur ne peuvent pas être publiées. Les options de publication dans l’éditeur ne sont disponibles que pour les pages auxquelles vous pouvez accéder à partir de leur chemin d’accès réel.

### Dépublication à partir de la console {#unpublishing-from-the-console}

De la même façon que vous [utilisez l’option Gérer la publication pour publier une page](/help/sites-authoring/publishing-pages.md#manage-publication), vous pouvez l’utiliser pour la dépublication.

1. Sélectionnez la ou les pages dans la console des sites et cliquez sur le bouton **Gérer la publication**.
1. L’assistant **Gérer la publication** démarre. Dans la première étape, **Options**, sélectionnez **Dépublier** au lieu de l’option par défaut, à savoir **Publier**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   À l’instar de l’option de publication différée, qui lance un workflow permettant de publier cette version de la page à l’heure indiquée, la désactivation différée lance un workflow pour dépublier la ou les pages sélectionnées à une heure spécifique.

   Pour annuler une publication/dépublier ultérieurement, rendez-vous dans la [console Workflow](/help/sites-administering/workflows.md) pour mettre un terme au workflow correspondant.

1. Pour finaliser la dépublication, complétez les différentes étapes de l’assistant, comme vous le feriez pour [publier la page](/help/sites-authoring/publishing-pages.md#manage-publication).

## Publication et dépublication d’une arborescence {#publishing-and-unpublishing-a-tree}

Lorsque vous avez saisi ou mis à jour un nombre considérable de pages de contenu (toutes résidant sous la même page racine), il peut s’avérer plus facile de publier l’arborescence entière en une seule action.

Vous pouvez utiliser l’option [Gérer la publication](/help/sites-authoring/publishing-pages.md#manage-publication) sur la console des sites.

1. Dans la console Sites, sélectionnez la page racine de l’arborescence que vous souhaitez publier ou dépublier, puis sélectionnez **Gérer la publication**.
1. L’assistant **Gérer la publication** démarre. Choisissez la publication ou la dépublication, puis sélectionnez **Suivant** pour continuer.
1. À l’étape **Portée**, sélectionnez la page racine et sélectionnez **Inclure les enfants**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Dans la boîte de dialogue **Inclure les enfants**, désélectionnez les options suivantes :

   * Inclure seulement les enfants immédiats
   * Inclure seulement les pages déjà publiées

   Ces options sont sélectionnées par défaut. Vous devez donc penser à les désélectionner. Cliquez sur **Ajouter** pour confirmer et ajouter le contenu à l’opération de publication ou de dépublication.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. L’assistant **Gérer la publication** répertorie le contenu de l’arborescence à réviser. Vous pouvez personnaliser davantage la sélection en ajoutant des pages supplémentaires ou en supprimant celles sélectionnées.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   N’oubliez pas que vous pouvez également passer en revue les références à publier au moyen de l’option **Références publiées**.

1. [Poursuivez normalement les étapes de l’assistant Gérer la publication](#manage-publication) pour terminer la publication ou l’annulation de la publication de l’arborescence.

## Définition du statut de publication {#determining-publication-status}

Vous pouvez déterminer le statut de publication d’une page :

* dans les [informations d’aperçu des ressources de la console Sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) ;

  ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

  L’état de publication est indiqué dans les modes d’affichage [Carte](/help/sites-authoring/basic-handling.md#card-view), [Colonnes](/help/sites-authoring/basic-handling.md#column-view) et [Liste](/help/sites-authoring/basic-handling.md#list-view) de la console Sites.

* Dans la [chronologie](/help/sites-authoring/basic-handling.md#timeline)

  ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* dans le menu [Informations sur la page](/help/sites-authoring/author-environment-tools.md#page-information) lors de la modification d’une page.

  ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
