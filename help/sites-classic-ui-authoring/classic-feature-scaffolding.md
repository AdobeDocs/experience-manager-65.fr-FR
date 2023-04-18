---
title: Génération de modèles automatique
description: Il peut arriver que vous deviez créer un grand ensemble de pages partageant la même structure mais ayant un contenu différent. Avec la génération de modèles automatique, vous pouvez créer un formulaire (un modèle automatique) avec des champs qui reflètent la structure souhaitée pour vos pages, puis utiliser ce formulaire pour créer facilement des pages en fonction de cette structure.
uuid: 5904abc0-b256-4da4-a7d7-3c17ea299648
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a63e5732-b1a3-4639-9838-652af401e788
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 41%

---

# Génération de modèles automatique{#scaffolding}

Il peut arriver que vous deviez créer un grand ensemble de pages partageant la même structure mais ayant un contenu différent. Par le biais de l’interface d’AEM standard, vous devez créer chaque page, faire glisser les composants appropriés sur la page et remplir chacune d’elles individuellement.

Avec la génération de modèles automatique, vous pouvez créer un formulaire (un modèle automatique) avec des champs qui reflètent la structure souhaitée pour vos pages, puis utiliser ce formulaire pour créer facilement des pages en fonction de cette structure.

>[!NOTE]
>
>La génération de modèles automatique (IU classique) respecte [l’héritage du MSM](#scaffolding-with-msm-inheritance). 

## Fonctionnement de la génération de modèles automatique {#how-scaffolding-works}

Les modèles automatiques sont stockés dans la console **Outils** de l’administrateur du site.

* Ouvrez le **Outils** puis cliquez sur **Génération de modèles automatique de page par défaut**.
* Sous ce clic, **geometrixx**.
* Sous **geometrixx** vous trouverez un *page scaffold* appelé **News**. Double-cliquez pour ouvrir cette page.

![howscaffolds_work](assets/howscaffolds_work.png)

Le modèle automatique est constitué d’un formulaire avec un champ pour chaque élément de contenu qui compose la page à créer et de quatre paramètres importants accessibles par le biais des **propriétés de page** de la page du modèle automatique.

![pageprops](assets/pageprops.png)

Les propriétés de la page de génération de modèles automatique sont les suivantes :

* **Texte du titre**: Il s’agit du nom de cette page de génération de modèles automatique. Dans cet exemple, il s’appelle &quot;News&quot;.
* **Description**: Celui-ci s’affiche sous le titre de la page de génération de modèles automatique.
* **Modèle cible**: Il s’agit du modèle que ce modèle automatique utilisera lors de la création d’une page. Dans cet exemple, il s’agit d’une *Page de contenu Geometrixx* modèle.
* **Chemin cible**: Il s’agit du chemin d’accès de la page parente au-dessous de laquelle ce modèle automatique créera de nouvelles pages. Dans cet exemple, le chemin d’accès est */content/geometrixx/en/news*.

Le contenu du modèle automatique est le formulaire. Lorsqu’un utilisateur souhaite crée une page à l’aide du modèle automatique, il remplit le formulaire et clique sur *Créer*, au bas du formulaire. Dans l’exemple **Actualités** ci-dessus, le formulaire se compose des champs suivants :

* **Titre**: Il s’agit du nom de la page à créer. Ce champ est toujours présent sur chaque modèle automatique.
* **Texte**: Ce champ correspond à un composant Texte sur la page résultant du processus.
* **Image** : ce champ correspond à un composant Image sur la page qui en résulte.
* **Image/Avancé**: **Titre**: Titre de l’image.
* **Image/Avancé**: **Texte de remplacement**: Texte secondaire de l’image.
* **Image / Avancé** : **Description** : description de l’image.
* **Image/Avancé**: **Taille**: Taille de l’image.
* **Balises/Mots-clés**: Métadonnées à attribuer à cette page. Ce champ est toujours présent sur chaque modèle automatique.

### Création d’un modèle automatique {#creating-a-scaffold}

Pour créer un modèle automatique, accédez à la console **Outils**, puis cliquez sur **Génération de modèles automatique de page par défaut** et créez une page. Un seul type de modèle de page est disponible : *Modèle de génération de modèles automatique.*

Accédez aux **Propriétés de la page** de la nouvelle page et définissez le *texte du titre*, la *description*, le *modèle cible* et le *chemin cible*, comme décrit ci-dessus.

Vous devez ensuite définir la structure de la page qui sera créée par ce modèle automatique. Pour ce faire, accédez au **[mode Conception](/help/sites-authoring/page-authoring.md#sidekick)** dans la page de modèle automatique. Un lien s’affiche alors pour vous permettre de modifier le modèle automatique dans l’**éditeur de boîte de dialogue**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

À l’aide de l’éditeur de boîte de dialogue, spécifiez les propriétés qui seront créées chaque fois qu’une nouvelle page est créée à l’aide de ce modèle automatique.

La définition de boîte de dialogue d’un modèle automatique fonctionne de la même manière que celle d’un composant (voir [Composants](/help/sites-developing/components.md)). Toutefois, quelques différences importantes s’appliquent :

* Les définitions de boîte de dialogue de composant sont rendues comme des boîtes de dialogue normales (comme illustré dans le volet central de l’éditeur de boîte de dialogue, par exemple), tandis que les définitions de boîte de dialogue de modèle automatique, bien qu’elles apparaissent comme des boîtes de dialogue normales dans l’éditeur de boîte de dialogue, sont rendues sur la page de modèle automatique sous la forme d’un formulaire de modèle automatique (comme illustré dans la section **News** scaffold ci-dessus).
* Les boîtes de dialogue de composant ne contiennent que les champs nécessaires pour définir le contenu d’un seul composant spécifique. Une boîte de dialogue de modèle automatique doit fournir des champs pour chaque propriété de chaque paragraphe de la page à créer.
* Dans le cas des boîtes de dialogue de composant, le composant utilisé pour le rendu du contenu spécifié est implicite. Par conséquent, la propriété `sling:resourceType` du paragraphe est complétée automatiquement lors de la création du paragraphe. Avec un modèle automatique, toutes les informations définissant le contenu et le composant affecté pour un paragraphe donné doivent être fournies par la boîte de dialogue elle-même. Dans les boîtes de dialogue de modèle automatique, ces informations doivent être fournies en utilisant *Masqué* champs pour envoyer ces informations lors de la création de la page.

Un aperçu de l’exemple **News** la boîte de dialogue scaffold dans l’éditeur de boîte de dialogue permet d’expliquer comment cela fonctionne. Passez en mode de conception sur la page du modèle automatique, puis cliquez sur le lien de l’éditeur de boîte de dialogue.

Cliquez à présent sur le champ de dialogue **Dialogue > Volet Onglets > Texte > Texte**, comme illustré ci-dessous :

![textedit](assets/textedit.png)

La liste des propriétés de ce champ s’affiche sur le côté droit de l’éditeur de boîte de dialogue, comme ceci :

![list_of_properties](assets/list_of_properties.png)

Notez la propriété name de ce champ. Il a la valeur

`./jcr:content/par/text/text`

Il s’agit du nom de la propriété à laquelle le contenu de ce champ sera écrit lorsque le modèle automatique est utilisé pour créer une page. La propriété est indiquée comme chemin relatif à partir du noeud représentant la page à créer. Il spécifie le texte de propriété, sous le texte du noeud, qui se trouve sous le noeud par, qui est lui-même un enfant du noeud jcr:content sous le noeud de page.

Cela définit l’emplacement de stockage du contenu pour le texte qui sera saisi dans ce champ. Cependant, nous devons également spécifier deux caractéristiques supplémentaires pour ce contenu :

* Le fait que la chaîne en cours de stockage ici doit être interprétée comme *texte enrichi*, et
* le composant à utiliser pour effectuer le rendu de ce contenu sur la page résultant du processus.

Notez que dans une boîte de dialogue de composant normale, vous n’avez pas à spécifier ces informations, car elles sont implicites dans le fait que la boîte de dialogue est déjà liée à un composant spécifique.

Pour spécifier ces deux informations, vous utilisez des champs masqués. Cliquez sur le premier champ masqué **Dialogue > Volet Onglets > Texte > Masqué**, comme illustré ci-dessous :

![hidden](assets/hidden.png)

Les propriétés de ce champ masqué sont les suivantes :

![hidden_list_props](assets/hidden_list_props.png)

La propriété name de ce champ masqué est

`./jcr:content/par/text/textIsRich`

Il s’agit d’une propriété booléenne utilisée pour interpréter la chaîne de texte stockée à l’adresse `./jcr:content/par/text/text`.

Puisque nous savons que le texte doit être interprété comme texte enrichi, nous définissons la propriété `value` de ce champ sur `true`.

>[!CAUTION]
>
>L’éditeur de boîte de dialogue permet à l’utilisateur de modifier les valeurs des propriétés *existantes* dans la définition de la boîte de dialogue. Pour ajouter une nouvelle propriété, l’utilisateur doit utiliser [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Par exemple, lorsqu’un nouveau champ masqué est ajouté à une définition de boîte de dialogue à l’aide de l’éditeur de boîte de dialogue, il n’a pas de *value* (c’est-à-dire, une propriété nommée &quot;valeur&quot;). Si le champ masqué en question nécessite une valeur par défaut *value* pour être définie, cette propriété doit être ajoutée manuellement avec l’un des outils CRX. La valeur ne peut pas être ajoutée avec l’éditeur de boîte de dialogue lui-même. Cependant, une fois la propriété présente, sa valeur peut être modifiée à l’aide de l’éditeur de boîte de dialogue.

Le second champ masqué est visible en cliquant dessus comme suit :

![hidden2](assets/hidden2.png)

Les propriétés de ce champ masqué sont les suivantes :

![hidden_list_props2](assets/hidden_list_props2.png)

La propriété name de ce champ masqué est

`./jcr:content/par/text/sling:resourceType`

et la valeur fixe spécifiée pour cette propriété est

`foundation/components/textimage`

Cela indique que le composant à utiliser pour effectuer le rendu du contenu texte de ce paragraphe est le composant *Texte et Image*. La valeur booléenne `isRichText` spécifiée dans l’autre champ masqué permet au composant d’effectuer le rendu de la chaîne de texte réelle stockée dans `./jcr:content/par/text/text` de la manière choisie.

### Génération de modèles automatique avec l’héritage du MSM {#scaffolding-with-msm-inheritance}

Dans l’IU classique, la génération de modèles automatique est entièrement intégrée à l’héritage du MSM (le cas échéant). 

Lorsque vous ouvrez une page en mode **Génération de modèles automatique** (à l’aide de l’icône située dans la partie inférieure du sidekick), tous les composants soumis à l’héritage sont indiqués par :

* un cadenas (pour la plupart des composants, par exemple Texte et Titre) ;
* un masque avec le texte **Cliquez pour annuler l’héritage** (pour les composants Image).

Ces deux indications montrent que le composant ne peut pas être publié, tant que l’héritage n’a pas été annulé. 

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>Cela peut être comparé à [composants hérités lors de la modification du contenu de la page](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Cliquez sur le symbole de verrouillage ou sur l’icône d’image pour rompre l’héritage :

* Le symbole se transforme en cadenas ouvert. 
* Une fois déverrouillé, vous pouvez modifier le contenu.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Après le déverrouillage, vous pouvez restaurer l’héritage en cliquant sur le symbole de cadenas ouvert. Vous perdrez les modifications que vous avez apportées.

>[!NOTE]
>
>Si l’héritage est annulé au niveau de la page (dans l’onglet Livecopy des propriétés de la page), tous les composants sont modifiables en mode **Génération de modèles automatique** (ils s’affichent à l’état déverrouillé).
