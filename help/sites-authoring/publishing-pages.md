---
title: Publication de pages
seo-title: Publication de pages
description: Publication de pages
seo-description: 'null'
uuid: 57795e4a-e528-4e74-ad9c-e13f868daebb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1f5eb646-acc7-49d5-b839-e451e68ada9e
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 88%

---


# Publication de pages {#publishing-pages}

Une fois le contenu créé et révisé dans l’environnement de création, l’objectif est de le [rendre disponible sur votre site web public](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) (votre environnement de publication).

On parle alors de publication d’une page, ou d’annulation de publication lorsque vous souhaitez retirer une page de l’environnement de publication. En cas de publication et d’annulation de la publication, la page reste disponible pour d’autres modifications dans l’environnement de création jusqu’à ce que vous la supprimiez.

Vous pouvez également publier/annuler la publication d’une page immédiatement ou à une date/heure prédéfinies.

>[!NOTE]
>
>Certains termes relatifs à la publication peuvent prêter à confusion :
>
>* **Publier/Annuler la publication**
   >  Termes principalement utilisés pour évoquer les opérations qui rendent votre contenu publiquement accessible dans votre environnement de publication (ou non).
   >
   >
* **Activer/Désactiver**
   >  Ces termes sont synonymes de publication/annulation de la publication.
   >
   >
* **Répliquer/Réplication**
   >  Il s’agit des termes techniques décrivant le déplacement des données (par exemple, contenu de page, fichiers, code, commentaires d’utilisateur) d’un environnement à l’autre, comme lors de la publication ou de la réplication inverse des commentaires d’utilisateur.
>



>[!NOTE]
>
>Si vous ne possédez pas les privilèges requis pour publier une page spécifique :
>
>* Un workflow est déclenché afin d’aviser la personne concernée de votre demande de publication.
>* Ce [workflow a peut-être été personnalisé](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) par votre équipe de développement.
>* Un message s’affiche brièvement pour vous informer que le workflow a été déclenché.

>



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

      * Spécifier les ressources, balises et autres éléments à publier conjointement avec la page, puis cliquer sur **Publier** pour terminer l’opération.

      * Sélectionner **Annuler** pour abandonner l’opération.

   ![chlimage_1](assets/chlimage_1.png)

1. L’option **Publier** réplique la page dans l’environnement de publication. Une bannière d’informations est affichée dans l’éditeur de page pour confirmer l’opération de publication.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Lorsque vous affichez la même page dans la console, l’état de publication mis à jour est visible.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>Une publication à partir de l’éditeur est dite superficielle ; en d’autres termes, seules la ou les pages sélectionnées sont publiées (les éventuelles pages enfants ne le sont pas).

### Publication à partir de la console {#publishing-from-the-console}

La console Sites propose deux options de publication :

* [Publication rapide](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gérer la publication](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Publication rapide  {#quick-publish}

L’option **Publication rapide** concerne les cas simples. Elle publie immédiatement la ou les pages sélectionnées sans aucune autre interaction. De ce fait, toute autre référence non publiée l’est aussi automatiquement.

Pour publier une page avec l’option Publication rapide :

1. Sélectionnez la ou les pages dans la console Sites et cliquez ensuite sur le bouton **Publication rapide**.

   ![pp-02](assets/pp-02.png)

1. Dans la boîte de dialogue Publication rapide, confirmez la publication en cliquant sur **Publier** ou annulez en cliquant sur **Annuler**. Pour rappel, toute référence non publiée sera également publiée automatiquement.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Lorsque la page est publiée, une alerte est affichée pour confirmer la publication.

>[!NOTE]
>
>L’option de publication rapide est dite superficielle ; en d’autres termes, seules la ou les pages sélectionnées sont publiées (les éventuelles pages enfants ne le sont pas).

#### Gérer la publication   {#manage-publication}

La méthode **Gérer la publication** propose plus d’options que Publication rapide, dont la possibilité d’inclure des pages enfants, de personnaliser les références ou encore de lancer n’importe quel workflow applicable. Elle offre également la possibilité de publier la page à une date ultérieure.

Pour modifier ou annuler la publication d’une page à l’aide de l’option Gérer la publication :

1. Sélectionnez la ou les pages dans la console Sites et cliquez ensuite sur le bouton **Gérer la publication**.

   ![pp-02-1](assets/pp-02-1.png)

1. L’assistant **Gérer la publication** démarre. La première étape, **Options**, vous permet d’effectuer les opérations suivantes :

   * Publier ou annuler la publication des pages sélectionnées.
   * Effectuer une action maintenant ou ultérieurement.

   La publication différée lance un workflow pour modifier la ou les pages sélectionnées à l’heure indiquée. Si vous optez pour une annulation différée de la publication, un workflow est lancé pour annuler la publication de la ou des pages sélectionnées à une heure déterminée.

   Pour annuler une publication/annulation de publication ultérieure, rendez-vous dans la [console Processus](/help/sites-administering/workflows.md) pour mettre un terme au processus correspondant.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Cliquez sur **Suivant** pour continuer.

1. À l’étape suivante de l’assistant de gestion des publications, **Scope**, vous pouvez définir la portée de la publication/annulation de publication, par exemple inclure des pages enfants et/ou inclure des références.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   Vous pouvez sélectionner le bouton **Ajouter du contenu** pour ajouter des pages à la liste des pages à publier, au cas où vous auriez omis d’en sélectionner une avant de lancer l’assistant Gérer la publication.

   Le bouton Ajouter du contenu lance l’[explorateur de chemins d’accès](/help/sites-authoring/author-environment-tools.md#path-browser), qui vous permet de sélectionner du contenu.

   Sélectionnez les pages souhaitées, puis cliquez sur **Sélectionner** pour ajouter du contenu à l’assistant ou sur **Annuler** pour annuler la sélection et revenir à l’assistant.

   De retour dans l’assistant, vous pouvez sélectionner un élément dans la liste afin de configurer d’autres options :

   * Inclure ses enfants.
   * Le supprimer de la sélection.
   * Gérer ses références publiées.

   ![pp-03](assets/pp-03.png)

   La boîte de dialogue qui s’ouvre lorsque vous cliquez sur **Inclure les enfants** vous permet d’effectuer les opérations suivantes :

   * Inclure seulement les enfants immédiats.
   * Inclure seulement les pages modifiées.
   * Inclure seulement les pages déjà publiées.

   Cliquez sur **Ajouter** pour ajouter les pages enfants à la liste des pages à publier ou dont la publication doit être annulée sur la base des options sélectionnées. Cliquez sur **Annuler** pour annuler la sélection et revenir à l’assistant.

   ![chlimage_1-3](assets/chlimage_1-3.png)

   De retour dans l’assistant, les pages ajoutées sont affichées en fonction des options que vous avez sélectionnées dans la boîte de dialogue Inclure les enfants.

   Vous pouvez afficher et modifier les références à publier ou dont la publication doit être annulée pour une page. Pour ce faire, sélectionnez la page, puis cliquez sur le bouton **Références publiées**.

   ![pp-04](assets/pp-04.png)

   La boîte de dialogue **Références publiées** affiche les références du contenu sélectionné. Par défaut, elles sont toutes sélectionnées. Dès lors, elles seront toutes publiées ou leur publication sera annulée. Vous pouvez toutefois les désélectionner pour qu’elles ne soient pas incluses dans l’opération.

   Cliquez sur **Terminé** pour enregistrer vos modifications ou sur **Annuler** pour annuler la sélection et revenir à l&#39;Assistant.

   De retour dans l’assistant, la colonne **Références** est mise à jour afin de tenir compte des références que vous avez choisi de publier ou dont la publication doit être annulée.

   ![pp-05](assets/pp-05.png)

1. Pour terminer, cliquez sur **Publier**.

   De retour dans la console Sites, un message de notification s’affiche pour confirmer la publication.

1. Si les pages publiées sont associées à des workflows, elles peuvent être affichées dans une dernière étape de l’assistant de publication intitulée **Workflows**.

   >[!NOTE]
   >
   >L’étape **Workflows** est affichée en fonction des droits dont dispose ou non votre utilisateur. Pour plus d&#39;informations, consultez la [note précédente sur cette page](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) concernant les privilèges de publication ainsi que [Gestion de l&#39;accès aux Workflows](/help/sites-administering/workflows-managing.md) et [Application de Workflows aux pages](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd).

   Les ressources sont regroupées en fonction des workflows déclenchés et de chaque option proposée pour :

   * définir le titre du workflow ;
   * Conservez le package de flux de travaux, à condition que le flux de travaux prenne [en charge plusieurs ressources](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * définir le titre du module de workflow, si l’option de conservation du module de workflow a été sélectionnée.

   Cliquez sur **Publier** ou **Publier ultérieurement** pour terminer la publication.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Annulation de la publication des pages {#unpublishing-pages}

L’annulation de la publication d’une page supprime cette page de votre environnement de publication, de sorte que vos lecteurs ne puissent plus y accéder.

Vous pouvez annuler la publication d’une ou de plusieurs pages [en procédant de la même manière que pour leur publication](/help/sites-authoring/publishing-pages.md#publishing-pages) :

* [À partir de l’éditeur de page](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [À partir de la console Sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Annulation de la publication à partir de l’éditeur   {#unpublishing-from-the-editor}

Lors de la modification d’une page, si vous souhaitez annuler sa publication, sélectionnez **Annuler la publication de la page** dans le menu **Informations sur la page**, comme vous le feriez pour [publier la page](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

### Annulation de la publication à partir de la console   {#unpublishing-from-the-console}

De la même façon que vous [utilisez l’option Gérer la publication pour publier une page](/help/sites-authoring/publishing-pages.md#manage-publication), vous pouvez l’utiliser pour annuler la publication.

1. Sélectionnez la ou les pages dans la console Sites et cliquez ensuite sur le bouton **Gérer la publication**.
1. L’assistant **Gérer la publication** démarre. Dans la première étape, **Options**, sélectionnez **Annuler la publication** au lieu de l’option par défaut, à savoir **Publier**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   À l’instar de l’option de publication différée, qui lance un workflow permettant de publier cette version de la page à l’heure indiquée, la désactivation différée lance un workflow pour annuler la publication de la ou des pages sélectionnées à une heure spécifique.

   Pour annuler une publication/annulation de publication ultérieure, rendez-vous dans la [console Processus](/help/sites-administering/workflows.md) pour mettre un terme au processus correspondant.

1. Pour finaliser l’annulation de la publication, complétez les différentes étapes de l’assistant, comme vous le feriez pour [publier la page](/help/sites-authoring/publishing-pages.md#manage-publication).

## Publication et annulation de la publication d’une arborescence {#publishing-and-unpublishing-a-tree}

Après avoir saisi, ou mis à jour, un nombre élevé de pages de contenu (toutes résidant sous la même page racine), il peut s’avérer plus simple de publier toute l’arborescence en une seule opération.

Pour ce faire, vous pouvez utiliser l’option [Gérer la publication](/help/sites-authoring/publishing-pages.md#manage-publication) de la console Sites.

1. Dans la console Sites, sélectionnez la page racine de l’arborescence que vous souhaitez publier ou dont vous souhaitez annuler la publication, puis sélectionnez **Gérer la publication**.
1. L’assistant **Gérer la publication** démarre. Choisissez de publier ou d’annuler la publication, indiquez à quel moment cette opération doit être effectuée, puis sélectionnez **Suivant** pour continuer.
1. À l’étape **Portée**, sélectionnez la page racine, puis **Inclure les enfants**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Dans la boîte de dialogue **Inclure les enfants**, désélectionnez les options suivantes :

   * Inclure seulement les enfants immédiats
   * Inclure seulement les pages déjà publiées

   Ces options sont sélectionnées par défaut. Vous devez donc penser à les désélectionner. Cliquez sur **Ajouter** pour confirmer et ajouter le contenu à l’opération de publication ou d’annulation de la publication.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. L’assistant **Gérer la publication** répertorie le contenu de l’arborescence à des fins de révision. Vous pouvez personnaliser davantage la sélection en ajoutant d’autres pages ou en supprimant celles qui sont sélectionnées.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   N’oubliez pas que vous pouvez également passer en revue les références à publier au moyen de l’option **Références publiées**.

1. [Continuez l’assistant Gérer la publication comme ](#manage-publication) normal pour terminer la publication ou la déspublication de l’arborescence.

## Définition de l’état de publication {#determining-publication-status}

Vous pouvez déterminer l’état de publication d’une page :

* Dans les [informations d’aperçu des ressources de la console Sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

   L’état de publication est indiqué dans les modes d’affichage [Carte](/help/sites-authoring/basic-handling.md#card-view), [Colonnes](/help/sites-authoring/basic-handling.md#column-view) et [Liste](/help/sites-authoring/basic-handling.md#list-view) de la console Sites.

* Dans la [chronologie](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* Dans le menu [Informations sur la page](/help/sites-authoring/author-environment-tools.md#page-information) lors de la modification d’une page

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
