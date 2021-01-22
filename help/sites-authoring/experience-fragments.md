---
title: Fragments d’expérience
seo-title: Fragments d’expérience
description: 'null'
seo-description: 'null'
uuid: 9a1d12ef-5690-4a2e-8635-a710775efa39
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4c5b52c3-5e23-4125-9306-48bf2ded23cb
docset: aem65
translation-type: tm+mt
source-git-commit: 5c88d9cfdd6238961aa46d36ebc1206a5d0507e0
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 96%

---


# Fragments d’expérience{#experience-fragments}

Un fragment d’expérience est un groupe d’un ou plusieurs composants comprenant un contenu et une disposition pouvant être référencés dans les pages. Il peut contenir n’importe quel composant.

Un fragment d’expérience :

* fait partie d’une expérience (page) ;
* peut être utilisé sur plusieurs pages ;
* est basé sur un modèle (uniquement modifiable) qui définit la structure et les composants ;
* comprend un ou plusieurs composants, avec mise en page, dans un système de paragraphes ;
* peut contenir d’autres fragments d’expérience ;
* peut être combiné à d’autres composants (y compris d’autres fragments d’expérience) pour former une page entière (expérience) ;
* peut avoir différentes variations et partager du contenu et/ou des composants ;
* peut être scindé en blocs de création utilisables dans plusieurs variations du fragment.

Vous pouvez utiliser des fragments d’expérience :

* Si un auteur souhaite réutiliser des parties (un fragment d’une expérience) d’une page, il doit copier et coller ce fragment. La création et la gestion de ces expériences de copier/coller sont chronophages et sources d’erreurs pour l’utilisateur. Les fragments d’expérience rendent inutiles les opérations de copier/coller.
* Pour gérer le scénario d’utilisation CMS sans interface. Les auteurs souhaitent utiliser AEM uniquement dans une optique de création, mais pas pour diffuser du contenu au client. Un système/point de contact tiers utilise cette expérience, puis la diffuse à l’utilisateur final.

>[!NOTE]
>
>Dans le cas des fragments d’expérience, l’accès en écriture exige que le compte utilisateur soit enregistré dans le groupe :
>
>    `experience-fragments-editors`
Si vous rencontrez des problèmes, contactez votre administrateur système.

## Quand utiliser les fragments d’expérience ?    {#when-should-you-use-experience-fragments}

Les fragments d’expérience doivent être utilisés dans les cas suivants :

* Chaque fois que vous souhaitez réutiliser des expériences.

   * Expériences qui seront réutilisées avec un contenu identique ou similaire

* Lorsque vous utilisez AEM en tant que plate-forme de diffusion de contenu à des tiers.

   * Toute solution qui souhaite utiliser AEM comme plate-forme de diffusion de contenu
   * Intégration de contenu dans des points de contact tiers

* Si l’une de vos expériences se décline en plusieurs variations ou rendus.

   * Variations spécifiques à un canal ou contexte particulier
   * Expériences qu’il y a lieu de regrouper (par exemple, une campagne avec des expériences différentes en fonction des canaux)

* Lorsque vous avez recours au commerce omnicanal.

   * Partage de contenu commercial sur les canaux des [réseaux sociaux](/help/sites-developing/experience-fragments.md#social-variations) à grande échelle
   * Conversion des points de contact en points de transaction

## Organisation des fragments d’expérience {#organizing-your-experience-fragments}

Nous vous encourageons à :
* utiliser des dossiers pour organiser vos fragments d’expérience ;

* [configurer les modèles autorisés sur ces dossiers](#configure-allowed-templates-folder).

La création de dossiers vous permet d’effectuer les opérations suivantes :

* Créer une structure significative pour vos fragments d’expérience ; en fonction de la classification, par exemple

   >[!NOTE]
   Il n’est pas nécessaire d’aligner la structure de vos fragments d’expérience sur la structure de page de votre site.

* [Allouer les modèles autorisés au niveau du dossier](#configure-allowed-templates-folder)

   >[!NOTE]
   Vous pouvez utiliser l’[éditeur de modèles](/help/sites-authoring/templates.md) pour créer votre propre modèle.

Le projet WKND structure certains fragments d’expérience en fonction de `Contributors`. La structure utilisée illustre également l’utilisation d’autres fonctionnalités, telles que la gestion multisite (y compris des copies de langue).

Voir :

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Dossiers des fragments d’expérience](/help/sites-authoring/assets/xf-folders.png)

## Création et configuration d’un dossier pour vos fragments d’expérience {#creating-and-configuring-a-folder-for-your-experience-fragments}

Pour créer et configurer un dossier pour vos fragments d’expérience, il est recommandé de :

1. [Créer un dossier](/help/sites-authoring/managing-pages.md#creating-a-new-folder)

1. [Configurer les modèles de fragments d’expérience autorisés pour ce dossier](#configure-allowed-templates-folder)

>[!NOTE]
Il est également possible de configurer les [modèles autorisés pour votre instance](#configure-allowed-templates-instance). Cependant, cette méthode n’est **pas** recommandée, car les valeurs peuvent être remplacées lors de la mise à niveau.

### Configuration des modèles autorisés pour votre dossier {#configure-allowed-templates-folder}

>[!NOTE]
Il s’agit de la méthode recommandée pour spécifier les **Modèles autorisés**, car les valeurs ne sont pas remplacées lors de la mise à niveau.

1. Accédez au dossier **Fragments d’expérience** concerné.

1. Sélectionnez le dossier, puis **Propriétés**.

1. Spécifiez l’expression régulière pour récupérer les modèles requis dans le champ **Modèles autorisés**.

   Par exemple :
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Voir :
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Propriétés des fragments d’expérience - Modèles autorisés](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   Pour plus d’informations, voir [Modèles de fragments d’expérience](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments).

1. Sélectionnez **Enregistrer et fermer**.

### Configuration des modèles autorisés pour votre instance {#configure-allowed-templates-instance}

>[!CAUTION]
Il est déconseillé de modifier les **Modèles autorisés** à l’aide de cette méthode, car les modèles spécifiés peuvent être remplacés lors de la mise à niveau.
Veuillez utiliser cette boîte de dialogue uniquement à titre d’information.

1. Accédez à la console **Fragments d’expérience** concernée.

1. Sélectionnez **Options de configuration** :

   ![Bouton Configuration](assets/ef-02.png)

1. Spécifiez les modèles requis dans la boîte de dialogue **Configurer des Fragments d’expérience** :

   ![Configurer des fragments d’expérience](assets/ef-01.png)

   >[!NOTE]
   Pour plus d’informations, voir [Modèles de fragments d’expérience](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments).

1. Sélectionnez **Enregistrer**.

## Création d’un fragment d’expérience {#creating-an-experience-fragment}

Pour créer un fragment d’expérience :

1. Sélectionnez Fragments d’expérience dans la navigation globale.

   ![xf-01](assets/xf-01.png)

1. Accédez au dossier requis et sélectionnez **Créer**.

   ![xf-02](assets/xf-02.png)

1. Sélectionnez **Fragment d’expérience** pour ouvrir l’assistant **Créer un fragment d’expérience**.

   Sélectionnez le **Modèle** requis, puis **Suivant** :

   ![xf-03](assets/xf-03.png)

1. Renseignez les **Propriétés** de votre **Fragment d’expérience**.

   Un **Titre** est obligatoire. Si le **Nom** n’est pas spécifié, il est dérivé du **Titre**.

   ![xf-04](assets/xf-04.png)

1. Cliquez sur **Créer**.

   Un message s’affiche. Sélectionnez :

   * **Terminé** pour revenir à la console

   * **Ouvrir** pour ouvrir l’éditeur de fragments

## Modification d’un fragment d’expérience {#editing-your-experience-fragment}

L’Éditeur de fragments d’expérience offre des fonctionnalités similaires à celles à l’Éditeur de page classique.

>[!NOTE]
Pour plus d’informations sur l’utilisation de l’Éditeur de page, voir [Modification du contenu de la page](/help/sites-authoring/editing-content.md).

La procédure suivante explique comment créer un teaser pour un produit :

1. Faites glisser et déposez un **Teaser** à partir de l’[Explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser).

   ![xf-05](assets/xf-05.png)

1. Sélectionnez **[Configurer](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)** dans la barre d’outils du composant.
1. Ajoutez la **ressource** et définissez les **propriétés** selon vos besoins.
1. Confirmez les définitions en cliquant sur **Terminé** (icône représentant une coche).
1. Ajoutez d’autres composants, en fonction de vos besoins.

## Création d’une variation de fragment d’expérience {#creating-an-experience-fragment-variation}

Vous pouvez créer des variations du fragment d’expérience, selon vos besoins :

1. Ouvrez le fragment à des fins de [modification](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment).
1. Ouvrez l’onglet **Variations**.

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. L’option **Créer** permet de créer les éléments suivants :

   * **Variation**
   * **Variation comme Live Copy**.

1. Définissez les propriétés requises :

   * **Template**
   * **Titre**
   * **Nom** ; si rien n’est indiqué dans ce champ, le nom est déduit du titre
   * **Description**
   * **Balises de variation**

   ![xf-06](assets/xf-06.png)

1. Confirmez en cliquant sur **Terminé** (icône représentant une coche). La nouvelle variation est alors affichée dans le panneau :

   ![xf-07](assets/xf-07.png)

## Utilisation du fragment d’expérience {#using-your-experience-fragment}

Vous pouvez désormais utiliser le fragment d’expérience lors de la création de vos pages :

1. Ouvrez une page à modifier.

   Par exemple : [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. Créez une instance du composant Fragment d’expérience. Pour ce faire, faites glisser le composant sur le système de paragraphes de la page depuis l’explorateur de composants :

   ![xf-08](assets/xf-08.png)

1. Ajoutez le fragment d’expérience proprement dit à l’instance de composant. Pour ce faire, vous pouvez effectuer l’une des opérations suivantes :

   * Faites glisser le fragment requis sur le composant depuis l’Explorateur de ressources
   * Sélectionnez **Configurer** dans la barre d’outils du composant et indiquez le fragment à utiliser. Confirmez en cliquant sur **Terminé** (icône représentant une coche).

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   L’option Modifier disponible dans la barre d’outils du composant sert de raccourci pour ouvrir le fragment dans l’éditeur de fragments.

## Blocs de création {#building-blocks}

Vous pouvez sélectionner un ou plusieurs composants pour créer un bloc de création à recycler dans votre fragment :

### Création d’un bloc {#creating-a-building-block}

Pour créer un bloc de ce type, procédez comme suit :

1. Dans l’éditeur de fragments d’expérience, sélectionnez les composants que vous souhaitez réutiliser :

   ![xf-10](assets/xf-10.png)

1. Dans la barre d’outils des composants, sélectionnez **Convertir en bloc de création** :

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. Saisissez le nom du **Bloc de création** et confirmez en cliquant sur **Convertir** :

   ![xf-11](assets/xf-11.png)

1. Le **bloc de création** s’affiche dans l’onglet et peut être sélectionné dans le système de paragraphe :

   ![xf-12](assets/xf-12.png)

#### Gestion d’un bloc de création {#managing-a-building-block}

Le bloc de création est visible dans l’onglet **Blocs de création**. Pour chaque bloc, les actions suivantes peuvent être effectuées :

* Atteindre l’élément principal : ouvre la variation principale dans un nouvel onglet
* Renommer
* Supprimer

![xf-13](assets/xf-13.png)

#### Utilisation d’un bloc de création {#using-a-building-block}

Vous pouvez faire glisser votre bloc de création vers le système de paragraphes de n’importe quel fragment, comme avec n’importe quel composant.

## Détails de votre Éditeur de fragments {#details-of-your-experience-fragment}

Les détails de votre fragment sont visibles :

1. Les détails sont affichés dans toutes les vues de la console **Éditeur de Fragments**, en **mode Liste**, notamment les détails d’une [exportation vers Target](/help/sites-administering/experience-fragments-target.md) :

   ![ef-03](assets/ef-03.png)

1. Lorsque vous ouvrez la section **Propriétés** du composant Fragment d’expérience :

   ![ef-04](assets/ef-04.png)

   Les propriétés sont disponibles dans plusieurs onglets :

   >[!CAUTION]
   Ces onglets s’affichent lorsque vous ouvrez les **propriétés** à partir de la console Fragments d’expérience.
   Si vous **ouvrez les propriétés** lors de la modification d’un fragment d’expérience, les [propriétés de page](/help/sites-authoring/editing-page-properties.md) appropriées s’affichent.

   ![ef-05](assets/ef-05.png)

   * **De base**

      * **Titre** - obligatoire

      * **Description**
      * **Balises**
      * **Nombre total de variations** - informations uniquement

      * **Nombre de variations web** - informations uniquement
      * **Nombre de variantes non-Web** - inf **ormations uniquement**

      * **Nombre de pages utilisant ce fragment** - informations uniquement
   * **Cloud Services**

      * **Configuration du cloud**
      * **Configuration de Cloud Services**
      * **Identifiant de page Facebook**
      * **Panorama Pinterest**
   * **Références**

      * Liste de références.
   * **État des réseaux sociaux**

      * Détails des variations des réseaux sociaux.




## Rendu HTML brut {#the-plain-html-rendition}

Utiliser le sélecteur `.plain.` de l’URL permet d’accéder au rendu HTML brut à partir du navigateur.

>[!NOTE]
Même s’il est directement disponible à partir du navigateur, [le principal objectif consiste à autoriser d’autres applications (des applications web tierces et des implémentations mobiles personnalisées, par exemple) à accéder directement au contenu du composant Fragment d’expérience en utilisant uniquement l’URL](/help/sites-developing/experience-fragments.md#the-plain-html-rendition).

## Exportation de fragments d’expérience    {#exporting-experience-fragments}

Par défaut, les fragments d’expérience sont fournis au format HTML. Ils peuvent être utilisés à la fois par AEM et les canaux tiers.

Pour l’exportation vers Adobe Target, JSON peut également être utilisé. Pour obtenir des informations complètes, voir [Intégration de Target aux ](/help/sites-administering/experience-fragments-target.md)Fragments d’expérience.
