---
title: Création de contenu ciblé en mode Ciblage
seo-title: Création de contenu ciblé en mode Ciblage
description: Le mode Ciblage et le composant cible fournissent des outils permettant de créer du contenu pour les expériences.
seo-description: Le mode Ciblage et le composant cible fournissent des outils permettant de créer du contenu pour les expériences.
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '5374'
ht-degree: 95%

---


# Création de contenu ciblé en mode Ciblage{#authoring-targeted-content-using-targeting-mode}

Créez du contenu ciblé à l’aide du mode Ciblage d’AEM. Le mode Ciblage et le composant cible fournissent des outils pour créer du contenu pour les expériences :

* Identifiez facilement le contenu ciblé figurant dans la page. Une ligne pointillée forme une bordure autour de tout le contenu ciblé.
* Sélectionnez une marque et une activité pour afficher les expériences.
* Ajoutez des expériences à une activité ou supprimez des expériences.
* Effectuez des tests A/B et convertissez les gagnants (Adobe Target uniquement).
* Ajoutez des offres à une expérience en créant des offres ou en utilisant les offres d’une bibliothèque.
* Configurez les objectifs et les performances du moniteur.
* Simulez l’expérience utilisateur.
* Pour une personnalisation plus importante, configurez le composant cible.

Vous pouvez utiliser AEM ou Adobe Target comme moteur de ciblage (pour utiliser Adobe Target, vous devez disposer d’un compte Adobe Target valide). Si vous utilisez Adobe Target, vous devez commencer par configurer l’intégration. Voir [instructions d&#39;intégration à Adobe Target](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

Les activités et les expériences qui s’affichent en mode Cible se répercutent dans la [console Activités](/help/sites-authoring/activitylib.md) :

* Les modifications apportées aux activités et aux expériences en mode Ciblage se répercutent dans la console Activités.
* Les modifications apportées dans la console Activités se répercutent dans le mode Ciblage.

>[!NOTE]
>
>Lorsque vous créez une campagne dans Adobe Target, elle affecte la propriété `thirdPartyId` à chaque campagne. Lorsque vous supprimez la campagne dans Adobe Target, la propriété thirdPartyId n’est pas supprimée. Vous ne pouvez pas réutiliser la propriété `thirdPartyId` pour des campagnes de différents types (AB, XT) et elle ne peut pas être supprimée manuellement. Pour éviter ce problème, attribuez un nom unique à chaque campagne. Ainsi, les noms de campagne ne peuvent pas être réutilisés dans différents types de campagnes.
>
>Si vous utilisez le même nom dans le même type de campagne, vous remplacerez la campagne existante.
>
>Lors de la synchronisation, si le message d’erreur « Échec de la demande. `thirdPartyId` existe déjà. » s’affiche, modifiez le nom de la campagne et resynchronisez-la.

>[!NOTE]
>
>Lors du ciblage, la combinaison de la marque et de l’activité est conservée au niveau de l’utilisateur, et non au niveau du canal.

## Passage en mode Ciblage {#switching-to-targeting-mode}

Passez en mode Cible pour accéder aux outils de création de contenu ciblé.

Pour passer en mode Cible :

1. Ouvrez la page pour laquelle vous souhaitez créer du contenu ciblé.
1. Dans la barre d’outils au niveau de la partie supérieure de la page, cliquez ou appuyez sur le menu déroulant de mode pour afficher les types de modes disponibles.

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Cliquez ou appuyez sur **Ciblage**. Les options de ciblage s’affichent dans la partie supérieure de la page.

   ![chlimage_1-10](assets/chlimage_1-10.png)

## Ajout d’une activité à l’aide du mode Ciblage {#adding-an-activity-using-targeting-mode}

Utilisez le mode Ciblage pour ajouter une activité à une marque. Lorsque vous ajoutez une activité, elle contient l’expérience par défaut. Une fois que vous avez ajouté l’activité, vous commencez la procédure de ciblage de contenu de l’activité.

Vous pouvez également créer et gérer des activités Adobe Target à partir d’AEM avec l’option de sélection du moteur cible (AEM ou Adobe Target) et de sélection du type d’activité (ciblage de l’expérience ou test A/B).

De plus, vous pouvez gérer les objectifs et les mesures pour toutes les activités Adobe Target et gérer vos audiences Adobe Target. La création de rapports d’activité Adobe Target, y compris la conversion des gagnants, pour les tests A/B est également fournie.

Lorsque vous ajoutez une activité, elle s’affiche également dans la [console Activités](/help/sites-authoring/activitylib.md).

Pour ajouter une activité :

1. Utilisez le menu déroulant **Marque** pour sélectionner la marque pour laquelle vous souhaitez créer l’activité.

   >[!NOTE]
   >
   >Il est recommandé de [créer des marques via la console d’activités](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Si vous créez une marque en utilisant un autre procédé, assurez-vous que le nœud `/campaigns/<brand>/master` existe pour éviter qu’une erreur ne se produise lorsque vous tenterez de créer une activité.

1. Cliquez ou appuyez sur « + » en regard du menu déroulant **Activité**.
1. Tapez le nom de l’activité.

   >[!NOTE]
   >
   >Lorsque vous créez une activité et qu’une configuration de cloud Adobe Target est associée à la page ou à une page parente, AEM considère automatiquement Adobe Target comme le moteur.

1. Dans le menu déroulant du moteur **Ciblage**, sélectionnez votre moteur de ciblage.

   * Si vous sélectionnez **ContextHub AEM**, les champs restants sont grisés et ne sont pas disponibles. Cliquez ou appuyez sur **Créer**.

   * Si vous sélectionnez **Adobe Target**, vous pouvez choisir une configuration (par défaut, il s’agit de celle définie lorsque vous avez [configuré le compte](/help/sites-administering/opt-in.md)) et un type d’activité.

   * Si vous utilisez l’intégration AEM/Adobe Campaign et que vous envoyez du contenu ciblé (newsletters), sélectionnez **Adobe Campaign**. Pour plus d’informations, reportez-vous à la section [Intégration à Adobe Campaign](/help/sites-administering/campaign.md).

1. Dans le menu Activité, sélectionnez **Ciblage de l’expérience** ou **Test A/B**.

   * Ciblage de l’expérience : gérez les activités Adobe Target à partir d’AEM.
   * Test A/B : créez/gérez les activités de test A/B dans Adobe Target à partir d’AEM.

## Procédure de ciblage : création, ciblage et objectifs et paramètres  {#the-targeting-process-create-target-and-goals-settings}

Le mode Ciblage permet de configurer plusieurs aspects d’une activité. Pour créer du contenu ciblé pour une activité de marque, utilisez la procédure en trois étapes ci-dessous :

1. [Créer](#create-authoring-the-experiences) : ajoutez ou supprimez des expériences et ajoutez des offres pour chaque expérience.
1. [Cible](#diagramtargetconfiguringtheaudiences) : spécifiez l’audience ciblée par les différentes expériences. Vous pouvez cibler une audience spécifique et, si vous utilisez un test A/B, déterminer le pourcentage de trafic dirigé vers une expérience.
1. [Objectifs et paramètres](#settingsgoalssettingsconfiguringtheactivityandsettinggoals) : planifiez l’activité et définissez la priorité. Vous pouvez également définir des objectifs de mesures de succès.

Utilisez la procédure ci-dessous pour commencer la procédure de ciblage du contenu pour une activité.

>[!NOTE]
>
>Pour utiliser la procédure de ciblage, vous devez être membre du groupe d’utilisateurs créateurs d’activités ciblées.

Pour ajouter une activité :

1. Dans le menu déroulant **Marque**, sélectionnez la marque qui contient l’activité sur laquelle vous travaillez.
1. Dans le menu déroulant **Activité**, sélectionnez l’activité pour laquelle vous créez du contenu ciblé.
1. Pour afficher les options qui vous guident lors de la procédure de ciblage, cliquez ou appuyez sur **Commencer le ciblage**.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >Pour modifier l’activité que vous utilisez, cliquez ou appuyez sur **Précédent**.

## Créer : création d’expériences  {#create-authoring-the-experiences}

L’étape Créer du ciblage de contenu consiste à créer des expériences. Au cours de cette étape, vous pouvez créer ou supprimer les expériences de l’activité et ajouter des offres à chaque expérience.

### Affichage des offres d’expérience en mode Ciblage  {#seeing-experience-offers-in-targeting-mode}

Après avoir [commencé la procédure de ciblage](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), sélectionnez une expérience pour afficher les offres disponibles pour cette expérience. Lorsque vous sélectionnez une expérience, les composants ciblés dans la page changent de manière à afficher l’offre concernant cette expérience.

>[!CAUTION]
>
>Soyez prudent lorsque vous désactivez le ciblage d’un composant déjà ciblé dans l’instance d’auteur. L’activité correspondante sera automatiquement supprimée de l’instance de publication.

>[!NOTE]
>
>Une offre est le contenu d’un composant ciblé.

Les expériences s’affichent dans le volet Audiences. Dans l’exemple ci-dessous, les expériences sont **Par défaut**, **Femme**, **Femme âgée de plus de 30 ans** et **Femme âgée de moins de 30 ans**. Cet exemple affiche l’offre Par défaut d’un composant **Image** ciblé.

![chlimage_1-12](assets/chlimage_1-12.png)

Lorsqu’une autre expérience est sélectionnée, le composant Image affiche l’offre concernant cette expérience.

![chlimage_1-13](assets/chlimage_1-13.png)

Lorsqu’une expérience est sélectionnée et que le composant ciblé n’inclut pas d’offre pour cette expérience, le composant affiche l’option **Ajouter une offre** superposée à l’offre par défaut semi-transparente. Lorsqu’aucune offre n’a été créée pour une expérience, l’offre **Par défaut** s’affiche pour le segment mappé à l’expérience.

![chlimage_1-14](assets/chlimage_1-14.png)

L’expérience par défaut s’affiche également si les propriétés du visiteur ne correspondent à aucun segment mappé sur les expériences. Voir [Ajout d’expériences à l’aide du mode Ciblage](#adding-and-removing-experiences-using-targeting-mode).

### Offres personnalisées et offres de bibliothèque {#custom-offers-and-library-offers}

Les offres qui sont [créées dans la page](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) et utilisées pour une seule expérience sont des « offres personnalisées ». L’image ci-dessous est superposée sur le contenu d’une offre personnalisée :

![chlimage_1-15](assets/chlimage_1-15.png)

Les offres [ajoutées à partir d’une bibliothèque d’offres](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) sont superposées sur l’image suivante :

![chlimage_1-16](assets/chlimage_1-16.png)

Vous pouvez enregistrer des offres personnalisées à une bibliothèque d’offres si vous estimez que vous êtes susceptible de les réutiliser. Vous pouvez également convertir une offre de bibliothèque en offre personnalisée si vous souhaitez modifier le contenu d’une expérience. Après la modification, vous pouvez réenregistrer l’offre dans la bibliothèque.

### Ajout et suppression d’expériences à l’aide du mode Ciblage {#adding-and-removing-experiences-using-targeting-mode}

À l’aide de l’étape Créer de la [procédure de ciblage](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), vous pouvez ajouter et supprimer des expériences. Vous pouvez également dupliquer une expérience et la renommer.

#### Ajout d’expériences à l’aide du mode Ciblage  {#adding-experiences-using-targeting-mode}

Pour ajouter une expérience :

1. Pour ajouter une expérience, cliquez ou appuyez sur **+** **Ajouter le ciblage d’expérience**, qui s’affiche en dessous des expériences existantes dans le volet **Audiences**.
1. Sélectionnez une audience. Par défaut, ce nom est le nom de l’expérience. Vous pouvez entrer un autre nom, si vous le souhaitez. Cliquez ou appuyez sur **OK**.

#### Suppression d’expériences à l’aide du mode Ciblage  {#removing-experiences-using-targeting-mode}

Pour supprimer une expérience :

1. Cliquez ou appuyez sur la flèche en regard du nom de l’expérience.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Cliquez sur **Supprimer**.

#### Attribution d’un nouveau nom à des expériences à l’aide du mode Ciblage  {#renaming-experiences-using-targeting-mode}

Pour renommer des expériences à l’aide du mode Ciblage :

1. Cliquez ou appuyez sur la flèche en regard du nom de l’expérience.
1. Cliquez sur **Renommer l’expérience** et entrez le nouveau nom.
1. Cliquez ou appuyez ailleurs dans l’écran pour enregistrer les modifications.

#### Modification des audiences à l’aide du mode Ciblage {#editing-audiences-using-targeting-mode}

Pour modifier les audiences à l’aide du mode Ciblage :

1. Cliquez ou appuyez sur la flèche en regard du nom de l’expérience.
1. Cliquez sur **Modifier l’audience** et sélectionnez une nouvelle audience.
1. Cliquez sur **OK**.

#### Duplication d’expériences à l’aide du mode Ciblage  {#duplicating-experiences-using-targeting-mode}

Pour copier des expériences à l’aide du mode Ciblage :

1. Cliquez ou appuyez sur la flèche en regard du nom de l’expérience.
1. Cliquez sur **Dupliquer** et sélectionnez l’audience.
1. Renommez l’expérience, si vous le souhaitez, puis cliquez sur **OK**.

### Création d’offres à l’aide du mode Ciblage  {#creating-offers-using-targeting-mode}

Ciblez un composant pour créer des offres pour les expériences. Les composants ciblés fournissent le contenu utilisé comme offres pour les expériences.

* [Ciblez un composant existant](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). Le contenu devient l’offre de l’expérience par défaut.
* [Ajoutez un composant cible](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component), puis ajoutez du contenu au composant.

Une fois qu’un composant est ciblé, vous pouvez ajouter des offres pour chaque expérience :

* [Ajoutez des offres personnalisées](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [Ajoutez des offres d’une bibliothèque](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

Les outils ci-dessous sont disponibles pour l’utilisation d’offres :

* [Ajoutez une offre personnalisée à une bibliothèque d’offres](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [Convertissez une offre de bibliothèque en offre personnalisée](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [Ouvrez une offre de bibliothèque et modifiez son contenu](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### Création d’une offre par défaut à l’aide d’un composant Ciblage existant  {#creating-a-default-offer-by-targeting-an-existing-component}

Ciblez un composant dans la page pour l’utiliser comme offre pour l’expérience par défaut de l’activité. Lorsque vous ciblez un composant, il est enveloppé dans un composant cible et son contenu devient l’offre de l’expérience par défaut.

Si vous ciblez un composant, seul ce composant peut être utilisé dans l’offre. Vous ne pouvez pas supprimer le composant de l’offre ou ajouter d’autres composants à l’offre.

Suivez la procédure ci-dessous après [avoir commencé la procédure de ciblage](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings).

1. Cliquez ou appuyez sur le composant à cibler. La barre d’outils du composant s’affiche, comme indiqué sur l’exemple suivant.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Cliquez ou appuyez sur l’icône Cible.

   ![](do-not-localize/chlimage_1.png)

   Le contenu du composant est l’offre de l’expérience par défaut. Lorsqu’un composant est ciblé, son nœud par défaut sera répliqué pour chaque expérience. Cela est nécessaire afin de modifier le nœud de contenu adéquat lors d’une création spécifique à une expérience. Pour ces expériences autres que l’expérience par défaut, [ajoutez une offre personnalisée](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) ou [une offre de bibliothèque](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Création d’une offre en ajoutant un composant cible {#creating-an-offer-by-adding-a-target-component}

Ajoutez un composant cible afin de créer l’offre pour l’expérience par défaut. Le composant cible est un conteneur pour d’autres composants, et les composants insérés dans ce conteneur sont ciblés. Lorsque vous utilisez le composant cible, vous pouvez ajouter plusieurs composants pour créer une offre. De plus, vous pouvez utiliser différents composants dans chaque expérience pour créer des offres différentes.

Pour plus d’informations sur la personnalisation de ce composant, voir [Configuration des options de composant cible](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options).

>[!NOTE]
>
>Les offres que vous créez à l’aide de la [console Offres](/help/sites-authoring/offerlib.md) peuvent également contenir plusieurs composants. Ces offres appartiennent à une bibliothèque d’offres et peuvent être utilisées pour différentes expériences.

Comme le composant cible est un conteneur, il s’affiche sous forme de zone cible pour d’autres composants.

En mode Cible, le composant cible possède une bordure bleue, et le message de cible de dépôt indique la nature ciblée.

![chlimage_1-19](assets/chlimage_1-19.png)

En mode d’édition, le composant cible comporte une icône Cible.

![](do-not-localize/chlimage_1-1.png)

Lorsque vous faites glisser des composants dans le composant cible, ils sont des composants ciblés.

![chlimage_1-20](assets/chlimage_1-20.png)

Lorsque vous ajoutez un composant au composant cible, il fournit du contenu pour une expérience spécifique. Pour spécifier l’expérience, vous sélectionnez l’expérience avant d’ajouter des composants.

Vous pouvez ajouter un composant cible à la page en mode d’édition ou en mode Cible. Vous ne pouvez ajouter des composants au composant cible qu’en mode Cible. Le composant cible appartient au groupe Composants de personnalisation.

Si vous modifiez le contenu ciblé, vous devez cliquer ou appuyer sur **Commencer le ciblage** avant d’en avoir la possibilité.

1. Faites glisser le composant cible vers la page dans laquelle vous souhaitez afficher l’offre.
1. Par défaut, aucun ID d’emplacement n’est défini. Cliquez ou appuyez sur Configurer (icône d’engrenage) pour définir l’emplacement.

   >[!NOTE]
   >
   >S’il est défini par l’administrateur, vous pouvez avoir besoin de définir explicitement l’emplacement.
   >
   >
   >Les administrateurs peuvent déterminer si la définition de cette configuration est nécessaire en consultant **https://&lt;hôte>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   Pour demander aux utilisateurs de saisir un emplacement, cochez la case **Forcer l’emplacement **case.

1. Sélectionnez l’expérience pour laquelle vous souhaitez créer l’offre.
1. Création de l’offre :

   * Pour l’expérience par défaut, faites glisser les composants vers la zone ciblée et modifiez les propriétés du composant comme vous le faites habituellement pour créer le contenu de l’offre.
   * Pour les expériences autres que l’expérience par défaut, [ajoutez une offre personnalisée](#adding-a-custom-offer) ou [ajoutez une offre de bibliothèque](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Ajout d’une offre personnalisée  {#adding-a-custom-offer}

Créez une offre en créant le contenu d’un composant ciblé en mode Ciblage. Lorsque vous créez une offre personnalisée, elle est utilisée comme offre pour une seule expérience.

Si vous décidez que l’offre peut être utilisée pour d’autres expériences, vous pouvez créer une offre personnalisée et l’[ajouter à la bibliothèque](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library). Pour plus d’informations sur l’utilisation de la console Offres pour créer une offre réutilisable, reportez-vous à la section [Ajout d’une offre à une bibliothèque d’offres](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Sélectionnez l’expérience à laquelle vous ajoutez l’offre.
1. Pour afficher le menu Composant, cliquez ou appuyez sur le composant ciblé auquel vous ajoutez l’offre.

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Cliquez ou appuyez sur l’icône « + ».

   Le contenu de l’offre Par défaut est utilisé comme offre pour l’expérience actuelle.

1. Cliquez ou appuyez sur l’offre pour afficher le menu Offre, puis cliquez ou appuyez sur l’icône Modifier.

   ![](do-not-localize/chlimage_1-2.png)

1. Modifiez le contenu du composant.

#### Ajout d’une offre à partir d’une bibliothèque d’offres  {#adding-an-offer-from-an-offer-library}

Ajoutez une offre de la [bibliothèque d’offres](/help/sites-authoring/offerlib.md) à une expérience. Vous pouvez ajouter une offre de la bibliothèque de la marque que vous ciblez actuellement.

Vous ne pouvez pas ajouter d’offres de bibliothèque à l’expérience par défaut.

1. Sélectionnez l’expérience à laquelle vous ajoutez l’offre.
1. Pour afficher le menu Composant, cliquez ou appuyez sur le composant ciblé auquel vous ajoutez l’offre.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Cliquez ou appuyez sur l’icône Dossier.

   ![](do-not-localize/chlimage_1-3.png)

1. Sélectionnez l’offre dans la bibliothèque, puis cliquez ou appuyez sur l’icône en forme de coche.

   ![chlimage_1-23](assets/chlimage_1-23.png)

   Le sélecteur d’offres permet de chercher ou de filtrer les offres. Lors de la recherche ou du filtrage, vous pouvez également trier les offres et modifier le mode d’affichage. Le nombre dans la partie supérieure droite indique le nombre d’offres disponibles dans la bibliothèque actuelle.

   * Cliquez ou appuyez sur **Parcourir** pour accéder à un autre dossier. Le volet de navigation s’affiche. Cliquez sur la flèche pour accéder aux dossiers. Cliquez ou appuyez sur **Parcourir** pour fermer le volet de navigation.

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * Cliquez ou appuyez sur **Filtrer** pour filtrer les offres selon les mots-clés et les balises. Vous saisissez des mots-clés et sélectionnez des balises dans le menu déroulant. Cliquez ou appuyez de nouveau sur **Filtrer** pour fermer le volet de filtrage.

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * Modifiez la façon dont vous triez les offres en cliquant ou en appuyant sur la flèche en regard de **Du plus récent au plus ancien**. Les offres peuvent être triées de la plus récente à la plus ancienne et inversement.

   ![chlimage_1-26](assets/chlimage_1-26.png)

   Cliquez ou appuyez sur l’icône en regard de **Afficher sous** pour afficher les offres sous forme de mosaïque ou de liste.

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### Ajout d’une offre personnalisée à une bibliothèque {#adding-a-custom-offer-to-a-library}

Ajoutez une offre personnalisée à la [bibliothèque d’offres](/help/sites-authoring/offerlib.md) lorsque vous souhaitez la réutiliser comme offre pour différentes expériences. Vous pouvez ajouter des offres à la bibliothèque de la marque actuelle que vous ciblez.

Pour plus d’informations sur l’utilisation de la console Offres pour créer une offre réutilisable, reportez-vous à la section [Ajout d’une offre à une bibliothèque d’offres](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Sélectionnez l’expérience pour afficher l’offre personnalisée.
1. Cliquez ou appuyez sur l’offre personnalisée pour afficher le menu Offre, puis cliquez ou appuyez sur l’icône **Enregistrer l’offre dans la bibliothèque d’offre**.

   ![](do-not-localize/chlimage_1-4.png)

1. Saisissez le nom de l’offre et sélectionnez la bibliothèque à laquelle vous ajoutez l’offre, puis cliquez ou appuyez sur l’icône en forme de coche.

#### Conversion d’une offre de bibliothèque en bibliothèque personnalisée  {#converting-a-library-offer-to-a-custom-library}

Convertissez une offre de bibliothèque en offre personnalisée pour modifier l’offre pour l’expérience actuelle, sans modifier l’offre dans d’autres expériences.

1. Sélectionnez l’expérience pour afficher l’offre de bibliothèque.
1. Cliquez ou appuyez sur l’offre de bibliothèque pour afficher le menu Offre, puis cliquez ou appuyez sur l’icône Convertir en offre intégrée.

   ![](do-not-localize/chlimage_1-5.png)

#### Modification d’une offre de bibliothèque {#editing-a-library-offer}

Ouvrez une offre de bibliothèque à partir d’une expérience en mode ciblé pour modifier l’offre. Les modifications que vous apportez s’affichent dans toutes les expériences qui utilisent l’offre.

1. Sélectionnez l’expérience pour afficher l’offre de bibliothèque.
1. Convertissez l’offre de bibliothèque en offre locale/personnalisée. Reportez-vous à la section [Conversion d’une offre de bibliothèque en bibliothèque personnalisée](#converting-a-library-offer-to-a-custom-library).
1. Modifiez le contenu de l’offre.

1. Réenregistrez-la dans la bibliothèque. Reportez-vous à la section [Ajout d’une offre personnalisée à une bibliothèque](#adding-a-custom-offer-to-a-library).

## Cible : configuration des audiences {#target-configuring-the-audiences}

L’étape Cibler de la [procédure de ciblage](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) implique de mapper les audiences sur les expériences utilisées lors de l’étape Créer. La page Cible affiche les audiences ciblées par chaque expérience. Vous pouvez spécifier ou modifier l’audience de chaque expérience. Si vous utilisez Adobe Target, vous pouvez également créer des tests A/B qui permettent de cibler le pourcentage de trafic d’une audience pour une expérience spécifique.

### Si vous utilisez le ciblage d’AEM ou d’Adobe Target (ciblage d’expériences) ... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Les audiences s’affichent dans la partie gauche du diagramme de mappage, tandis que les expériences s’affichent dans la partie droite.

![chlimage_1-28](assets/chlimage_1-28.png)

Définissez une audience à l’aide d’un segment. La configuration du cloud de la page détermine les segments à votre disposition. Lorsque la page n’est pas associée à une configuration de cloud d’Adobe Target, les segments AEM sont disponibles pour définir les audiences. Lorsque la page est associée à une configuration de cloud d’Adobe Target, vous utilisez les segments cibles.

Pour plus d’informations sur les moteurs de ciblage, reportez-vous à la section [Moteur de ciblage](/help/sites-authoring/personalization.md#targeting-engine).

Une audience ne doit pas être utilisée par plusieurs expériences. Un symbole d’avertissement s’affiche en regard d’une expérience lorsqu’elle est associée à une audience mappée à une autre expérience.

![](do-not-localize/chlimage_1-6.png)

### Association d’expériences à des audiences (AEM ou Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Suivez la procédure ci-dessous pour associer une expérience à une audience lorsque vous utilisez le ciblage d’AEM (ou le ciblage d’expériences d’Adobe Target) :

1. Cliquez ou appuyez sur la flèche de liste déroulante en regard de la zone de l’audience sur l’expérience.
1. (Facultatif) Cliquez ou appuyez sur **Modifier**, puis saisissez un mot-clé pour chercher le segment souhaité.
1. Dans la liste d’audiences, sélectionnez l’audience et cliquez ou appuyez sur **OK**.

### Si vous utilisez des tests A/B (Adobe Target)…   {#if-you-are-using-a-b-testing-adobe-target}

Si vous avez une activité de test A/B, les audiences se trouvent dans la partie gauche, le pourcentage de chaque expérience s’affiche au centre et les expériences se trouvent à droite.

Vous pouvez modifier les pourcentages, à condition que leur somme reste égale à 100 %. Une audience peut être utilisée par plusieurs expériences dans un test A/B.

![chlimage_1-29](assets/chlimage_1-29.png)

### Association d’audiences et de pourcentages de trafic avec un test A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Cliquez ou appuyez sur la zone de liste déroulante en regard de l’audience mappée sur l’expérience.
1. (Facultatif) Cliquez sur **Modifier**, puis saisissez un mot-clé pour chercher le segment de votre choix.
1. Cliquez ou appuyez sur **OK.**
1. Saisissez les pourcentages pour configurer le mode d’acheminement du trafic vers les différentes expériences. Le total doit être égal à 100.
1. (Facultatif) Modifiez le nom de l’expérience en cliquant sur le menu déroulant en regard du nom de l’expérience.

## Objectifs et paramètres : configuration de l’activité et définition des objectifs  {#goals-settings-configuring-the-activity-and-setting-goals}

L’étape Objectifs et paramètres de la [procédure de ciblage](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) implique de configurer le comportement de l’activité de marque. Spécifiez le moment auquel l’activité commence et se termine, ainsi que le niveau de priorité de l’activité. Vous pouvez également suivre les objectifs. En particulier, vous pouvez déterminer ce que vous souhaitez mesurer avec vos activités.

Les mesures d’objectif ne sont disponibles que si vous utilisez Adobe Target pour votre moteur de ciblage. Vous devez définir au moins une mesure d’objectif. Si Adobe Analytics est configuré et que vous disposez d’une configuration de cloud A4T Analytics, vous pouvez choisir si la source de création de rapports est Adobe Target ou Adobe Analytics.

Les mesures d’objectif ne sont mesurées que pour la campagne publiée.

Si vous utilisez AEM comme moteur de ciblage :

![chlimage_1-30](assets/chlimage_1-30.png)

Si vous utilisez Adobe Target comme moteur de ciblage :

![chlimage_1-31](assets/chlimage_1-31.png)

Si vous utilisez Adobe Target comme moteur de ciblage et que A4T Analytics est configuré pour le compte, un menu déroulant supplémentaire, **Source de création de rapports**, s’affiche :

![chlimage_1-32](assets/chlimage_1-32.png)

Les mesures de succès ci-dessous sont disponibles (pour la publication uniquement) :

<table>
 <tbody>
  <tr>
   <td><strong>Conversion</strong></td>
   <td><p>Pourcentage de visiteurs ayant cliqué sur n’importe quelle partie de l’expérience testée. Une conversion peut être comptabilisée une fois par visiteur ou chaque fois qu’un visiteur effectue une conversion. La mesure de conversion est définie sur l’une des options suivantes : :</p>
    <ul>
     <li><strong>Affichage d'une page</strong>  - Vous pouvez définir la page que l'audience a consultée en sélectionnant l' <strong>URL </strong> qui vous intéresse, puis en définissant l'URL ou plusieurs URL, ou en sélectionnant  <strong>l'URL </strong> contenue, puis en ajoutant un chemin ou un mot-clé.</li>
     <li><strong>A affiché une mbox</strong> : vous pouvez définir la mbox que l’audience a consultée en saisissant le nom de la mbox. Vous pouvez saisir plusieurs mbox en cliquant sur <strong>Ajouter une mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Recettes</strong></td>
   <td><p>Recettes générées par la visite. Vous pouvez choisir parmi les mesures de recettes suivantes :</p>
    <ul>
     <li>Recettes par Visiteur (RPV)</li>
     <li>Valeur de commande moyenne (AOV)</li>
     <li>Total ventes </li>
     <li>Commandes</li>
    </ul> <p>Pour ces options, la consultation d’une mbox indique que l’objectif a été atteint. Vous pouvez définir la mbox ou plusieurs mbox.</p> </td>
  </tr>
  <tr>
   <td><strong>Engagement</strong></td>
   <td><p>Vous pouvez mesurer trois types d’engagements : :</p>
    <ul>
     <li>Pages vues</li>
     <li>Score personnalisé</li>
     <li>Temps passé sur le site</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

De plus, il existe des paramètres avancés qui permettent de déterminer comment compter les mesures de succès. Les options incluent la comptabilisation de la mesure par impression ou une fois par visiteur et la possibilité de conserver l’utilisateur dans l’activité ou de l’en retirer.

Utilisez les options avancées pour déterminer ce qui se passe **après** qu’un utilisateur a rencontré la mesure de l’objectif. Le tableau suivant présente les options disponibles.

<table>
 <tbody>
  <tr>
   <td><strong>Une fois qu’un utilisateur a rencontré cette mesure de l’objectif...</strong></td>
   <td><strong>Vous sélectionnez l’événement suivant…</strong></td>
  </tr>
  <tr>
   <td><strong>Incrémenter le décompte et laisser l’utilisateur dans l’activité</strong></td>
   <td>Spécifiez comment le nombre est incrémenté :
    <ul>
     <li>Une fois par participant</li>
     <li>À chaque impression (actualisations de page exclues)</li>
     <li>À chaque impression</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Incrémenter le décompte, libérer l’utilisateur et autoriser le retour</strong></td>
   <td>Sélectionnez l’expérience que voit le visiteur s’il entre de nouveau dans l’activité :
    <ul>
     <li>Même expérience</li>
     <li>Expérience aléatoire</li>
     <li>Expérience inconnue</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Incrémenter la comptabilisation, libérer l’utilisateur et bloquer le retour</strong></td>
   <td>Déterminez ce que l’utilisateur voit au lieu du contenu de l’activité :
    <ul>
     <li>Même expérience, sans suivi</li>
     <li>Contenu par défaut ou contenu d’une autre activité</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Pour plus d’informations sur les mesures de succès, voir [Documentation d’Adobe Target](https://docs.adobe.com/content/help/fr-FR/target/using/activities/success-metrics/success-metrics.html).

### Paramètres de configuration (ciblage d’AEM)  {#configuring-settings-aem-targeting}

Pour configurer les paramètres si vous utilisez le ciblage d’AEM :

1. Pour indiquer le moment où l’activité commence, utilisez le menu déroulant **Démarrer** pour sélectionner l’une des valeurs suivantes :

   * **Après activation** : l’activité commence lorsque la page contenant le contenu ciblé est activée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, cliquez ou appuyez sur l’icône du calendrier, sélectionnez une date et indiquez l’heure de début de l’activité.

1. Pour spécifier le moment où l’activité se termine, utilisez le menu déroulant **Fin** pour sélectionner l’une des valeurs suivantes :

   * **Si désactivés** : l’activité s’arrête lorsque la page contenant le contenu ciblé est désactivée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, appuyez ou cliquez sur l’icône de calendrier, sélectionnez une date, puis spécifiez l’heure de fin de l’activité.

1. Pour spécifier la priorité de l’activité, utilisez le curseur pour choisir **Faible**, **Normale** ou **Élevée**.

### Configuration des objectifs et des paramètres (Adobe Target)  {#configuring-goals-settings-adobe-target}

Pour configurer les objectifs et les paramètres si vous utilisez Adobe Target :

1. Pour indiquer le moment où l’activité commence, utilisez le menu déroulant **Démarrer** pour sélectionner l’une des valeurs suivantes :

   * **Après activation** : l’activité commence lorsque la page contenant le contenu ciblé est activée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, cliquez ou appuyez sur l’icône du calendrier, sélectionnez une date et indiquez l’heure de début de l’activité.

1. Pour spécifier le moment où l’activité se termine, utilisez le menu déroulant **Fin** pour sélectionner l’une des valeurs suivantes :

   * **Si désactivés** : l’activité s’arrête lorsque la page contenant le contenu ciblé est désactivée.
   * **Date et heure spécifiées :** heure spécifique. Lorsque vous sélectionnez cette option, appuyez ou cliquez sur l’icône de calendrier, sélectionnez une date, puis spécifiez l’heure de fin de l’activité.

1. Pour spécifier la priorité de l’activité, utilisez le curseur pour choisir **Faible**, **Normale** ou **Élevée**.
1. Si vous avez configuré Adobe Analytics avec votre compte Adobe Target, le menu déroulant de la **source de création de rapports** s’affiche. Sélectionnez **Adobe Target** ou **Adobe Analytics** en tant que source.

   Si vous avez sélectionné **Adobe Analytics**, sélectionnez la société et une suite de rapports. Si vous sélectionnez **Adobe Target**, aucune action n’est nécessaire.

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. Dans la zone **Mesure d’objectif**, sous **Mon objectif principal**, sélectionnez la mesure de succès dont vous souhaitez effectuer le suivi (Conversion, Chiffre d’affaires, Engagement) et saisissez la manière dont cette mesure est évaluée (ou l’action entreprise par l’audience pour indiquer qu’un objectif a été atteint). Consultez la définition des mesures d’objectif dans le tableau précédent et la [documentation d’Adobe Target](https://docs.adobe.com/content/help/en/target/using/activities/success-metrics/success-metrics.html) sur les mesures de succès.

   Vous pouvez renommer l’objectif en cliquant sur le bouton de sélection dans le coin supérieur droit et en sélectionnant **Renommer**.

   Si vous devez supprimer tous les champs, cliquez sur le bouton de sélection dans le coin supérieur droit et sélectionnez **Effacer tous les champs**.

   Toutes les mesures comportent également des paramètres avancés que vous pouvez définir. Sélectionnez **Paramètres avancés** pour y accéder. Reportez-vous à la définition de la comptabilisation des mesures de succès dans le tableau précédent et à la [Documentation d’Adobe Target](https://docs.adobe.com/content/help/en/target/using/activities/success-metrics/success-metrics.html).

   >[!NOTE]
   Un objectif au moins doit être défini.

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   S’il manque des informations dans votre mesure, la mesure est entourée d’une ligne rouge.

1. Cliquez sur **Ajouter une nouvelle mesure** pour configurer d’autres mesures de succès.

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   Vous pouvez supprimer d’autres objectifs en cliquant ou en appuyant sur le bouton de sélection et cliquant ou en appuyant sur **Supprimer**. AEM exige qu’au moins un objectif soit défini.

1. Si vous souhaitez mieux contrôler la méthode de comptabilisation des mesures de succès, cliquez ou appuyez sur **Paramètres avancés** pour y accéder.
1. Cliquez sur **Enregistrer**.

Après la configuration, vous pouvez [afficher les performances de vos activités](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test), qui utilisent Adobe Target (ciblage d’expériences ou des tests A/B). De plus, avec le ciblage des tests A/B, vous pouvez [convertir les gagnants](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test).

## Simulation d’une expérience  {#simulating-an-experience}

Simulez l’expérience d’un visiteur pour vérifier que le contenu de la page s’affiche de la façon escomptée en fonction de la conception du contenu ciblé. Lors de la simulation, chargez différents profils utilisateur et découvrez le contenu ciblé pour l’utilisateur en question.

Les critères ci-dessous déterminent le contenu qui s’affiche lors de la simulation des interactions d’un visiteur :

* Les données contenues dans le magasin de la session de l’utilisateur (par le biais de ContextHub).
* [Activités qui sont activées](/help/sites-authoring/activitylib.md).
* [Règles qui définissent les segments](/help/sites-administering/campaign-segmentation.md).
* Contenu des expériences dans les composants Cible.
* [Configuration du moteur de ciblage](/help/sites-authoring/activitylib.md).

Si un contenu inattendu s’affiche dans la page lorsque vous chargez un profil, vérifiez la configuration de chaque élément de cette liste.

>[!NOTE]
Si vous utilisez des tests A/B, lors de la simulation, les expériences s’affichent en fonction du pourcentage de trafic. Cette action est gérée par Adobe Target, ce qui peut entraîner des résultats inattendus pour les créateurs. (L’activité _créateur est synchronisée avec les paramètres spécifiques qui permettent une réévaluation lors de la simulation.) Les créateurs peuvent avoir besoin d’actualiser pour afficher les autres expériences en fonction des paramètres de trafic.

Pour simuler l’expérience du visiteur, utilisez les outils suivants :

* Activité de simulation en mode Ciblage : la page affiche les offres pour l’utilisateur sélectionné dans ContextHub. Vous pouvez modifier les offres qui ciblent l’utilisateur.
* Mode Aperçu : utilisez ContextHub pour sélectionner les utilisateurs et les emplacements répondant aux critères des segments sur lesquels vos expériences sont fondées. En cas de modification de vos sélections ContextHub, le contenu ciblé change en conséquence.

1. Pour passer en mode Aperçu, dans la barre d’outils, cliquez ou appuyez sur **Aperçu**.
1. Dans la barre d’outils, cliquez ou appuyez sur l’icône ContextHub.

   ![](do-not-localize/chlimage_1-7.png)

1. Utilisez ContextHub pour modifier les propriétés de contexte. Par exemple, cliquez ou appuyez sur la propriété Persona pour sélectionner un autre utilisateur.

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La page change pour afficher le contenu ciblé pour le contexte actuel.

1. Pour apporter des modifications aux offres affichées, passez en mode Ciblage. L’activité de simulation étant sélectionnée, modifiez les offres pour le contexte configuré en mode Aperçu.

## Configuration des options du composant cible  {#configuring-target-component-options}

Vous pouvez personnaliser le composant cible en accédant aux options du composant de l’une des deux façons suivantes :

1. Une fois que vous avez ciblé le composant, dans le composant cible, cliquez ou appuyez sur le composant, puis sur l’icône Paramètres (engrenage).

   ![](do-not-localize/chlimage_1-8.png)

   AEM affiche la fenêtre Options du composant cible.

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. Autrement, pour accéder à ces paramètres en mode Plein écran, dans la fenêtre Options du composant cible, cliquez ou appuyez sur l’icône Plein écran.

   ![](do-not-localize/chlimage_1-9.png)

   AEM affiche la fenêtre Options du composant cible en plein écran.

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Configurez les paramètres du composant cible, comme indiqué dans les tableaux suivants.

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><strong>Emplacement</strong></td>
   <td><p>L’emplacement est une chaîne qui attribue un nom à l’emplacement du contenu ciblé et connecte les offres aux lieux (ou aux emplacements ou composants) dans la page où ces offres doivent être positionnées.</p> <p>Ce champ est une valeur générique.</p> <p>Si vous insérez une offre dans un composant, l’offre mémorise l’ID d’emplacement. Lorsque la page est exécutée, le moteur évalue les segments de l’utilisateur et, à partir de là, résout les expériences des campagnes actives qui doivent s’afficher. Ensuite, il cherche les ID d’emplacement dans la page et tente de faire correspondre les offres aux ID d’emplacement.</p> </td>
  </tr>
  <tr>
   <td><strong>Moteur</strong></td>
   <td>Sélectionnez <strong>Règles côté client (sans suivi), Adobe Target, ContextHub, </strong>et <strong> Adobe Campaign </strong>selon le moteur à utiliser.</td>
  </tr>
 </tbody>
</table>

Si vous sélectionnez Adobe Target comme moteur :

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><strong>Ciblage précis</strong></td>
   <td><p>L’activation du ciblage précis indique au composant d’attendre les données de contexte du client ou les données ContextHub pour être disponible avant l’envoi de la demande à Adobe Target. Cela peut accroître le temps de chargement. Pour la création, le ciblage précis est toujours activé.</p> <p>Si vous cochez la case <strong>Ciblage précis</strong>, la mbox commence par effectuer une opération <code>mboxDefine</code>, puis une opération <code>mboxUpdate</code> dans une demande Ajax une fois que les données sont disponibles.</p> <p>Si vous ne cochez pas la case <strong>Ciblage précis</strong>, la mbox exécute immédiatement une <code>mboxCreate</code> requête synchrone (dans ce cas, toutes les données contextuelles ne sont pas encore disponibles).</p> <p><strong>Remarque :</strong> L’activation ou la désactivation du ciblage précis sur un composant spécifique n’a aucune incidence sur les paramètres définis globalement. Vous pouvez toujours remplacer les paramètres globaux en sélectionnant Ciblage précis dans le composant.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclure les segments résolus</strong></td>
   <td><p>Si vous cochez cette case, tous les segments résolus dans l’appel de mbox et les paramètres configurés dans la page et dans l’infrastructure sont inclus.</p> <p>Cela ne fonctionne avec l’API XML que lorsque vous synchronisez des segments AEM. Si des segments dans AEM ne sont pas gérés par Adobe Target (comme les segments de script), cette option permet de résoudre le segment dans AEM et d’envoyer à Adobe Target des informations indiquant que le segment est actif.</p> </td>
  </tr>
  <tr>
   <td><strong>Paramètres contextuels hérités</strong></td>
   <td>Répertorie les paramètres de contexte hérités de l’infrastructure Adobe Target, le cas échéant, associés à la page sélectionnée.</td>
  </tr>
  <tr>
   <td><strong>Paramètres de contexte</strong></td>
   <td>Cliquez ou appuyez sur <strong>Ajouter le champ</strong> pour configurer des paramètres contextuels supplémentaires (comme dans le cadre de Cible). Les paramètres de contexte ajoutés au composant ne concernent <i>que</i> le composant et non un autre composant, comme ce serait le cas si vous ajoutiez des paramètres de contexte directement dans l’infrastructure.</td>
  </tr>
  <tr>
   <td><strong>Paramètres statiques</strong></td>
   <td>Cliquez ou appuyez sur <strong>Ajouter le champ</strong> pour configurer d'autres paramètres statiques (comme dans le cadre de Cible). Les paramètres statiques ajoutés au composant s'appliquent <i>uniquement</i> au composant et non à d'autres composants, comme ce serait le cas si vous ajoutez des paramètres statiques directement à la structure. Les paramètres statiques ne proviennent pas du contexte (contexte du client de ContextHub).</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Lorsque vous sélectionnez un composant et que vous définissez son ciblage, AEM remplace également le composant et y insère un composant Adobe Target. (Le composant Adobe Target est utilisé non seulement lorsque vous l’ajoutez manuellement à la page, mais également lorsque vous ciblez un composant existant.)

Si vous sélectionnez ClientContext (côté client) comme moteur :

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><strong>Options côté client – Stratégie</strong></td>
   <td><p>Sélectionnez l’une des options suivantes :</p>
    <ul>
     <li><strong>Première</strong> : expérience la plus élevée dans la liste organisée dans la campagne.</li>
     <li><strong>Aléatoire</strong> : n’importe quelle expérience est utilisée.</li>
     <li><strong>Score</strong> du parcours de navigation : Les balises et les accès aux balises connexes qui sont suivis dans le contexte client sont utilisés. Les taux de fréquence d’accès aux balises définis sur la page de teaser sont comparés.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Vous sélectionnez **Adobe Campaign** comme moteur si vous intégrez AEM à Adobe Campaign. Pour plus d’informations, reportez-vous à la section [Intégration d’AEM à Adobe Campaign](/help/sites-administering/campaign.md).

Sélectionnez **ContextHub** comme moteur si vous utilisez le ciblage ContextHub. Reportez-vous à la section [Configuration de ContextHub.](/help/sites-developing/ch-configuring.md)
