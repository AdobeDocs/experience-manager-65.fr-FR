---
title: Administration des balises
seo-title: Administration des balises
description: Découvrez comment administrer les balises dans AEM.
seo-description: Découvrez comment administrer les balises dans AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 61%

---


# Administration des balises {#administering-tags}

Les balises constituent un moyen simple et rapide de classer le contenu de votre site web. Elles peuvent être considérées comme des mots-clés ou des étiquettes (métadonnées) qui permettent de trouver plus rapidement du contenu dans le résultat d’une recherche.

Dans Adobe Experience Manager (AEM), une balise peut être une propriété de

* Nœud de contenu d’une page (voir [Utilisation des balises](/help/sites-authoring/tags.md))

* Nœud de métadonnées pour une ressource (voir [Gestions des métadonnées des ressources numériques](/help/assets/metadata.md))

Outre les pages et les ressources, les balises sont utilisées pour les fonctionnalités d’AEM Communities :

* Contenu créé par l’utilisateur (voir [Balisage du contenu créé par l’utilisateur)](/help/communities/tag-ugc.md)

* Ressources d’activation (voir [Balisage des ressources d’activation](/help/communities/functions.md#catalog-function))

## Fonctionnalités des balises {#tag-features}

Voici quelques-unes des fonctionnalités des balises dans AEM :

* Les balises peuvent être regroupées dans différents espaces de noms. De telles hiérarchies autorisent la création de taxonomies. Ces taxonomies sont générales dans AEM.
* Pour les balises nouvellement créées, la principale restriction réside dans le fait qu’elles doivent être uniques dans un espace de noms spécifié.
* Le titre d’une balise ne doit pas comporter de caractères de séparation de chemin d’accès aux balises (s’il y en a, ils ne s’afficheront pas).

   * colon `:` - delimits the namespace tag
   * forward slash `/` - delimits sub-tags

* Des balises peuvent être appliquées par les créateurs et les visiteurs du site. Indépendamment de leur auteur, toutes les formes de balises peuvent être sélectionnées, tant lors de l’affectation d’une page que lors d’une recherche.
* Tags can be created and their taxonomy modified by members of the &quot;tag-administrators&quot; group and members who have modification rights to `/content/cq:tags`.

   * Une balise qui contient des balises enfants est appelée « balise conteneur ».
   * Une balise qui n’est pas une balise conteneur est appelée « balise terminale ».
   * Un espace de noms de balises est une balise terminale ou conteneur.

* Tags are used by the [Search component](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) to facilitate finding content.
* Tags are used by the [Teaser component](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), which monitors a user&#39;s tag cloud to provide targeted content.
* Si les balises constituent un aspect important de votre contenu :

   * Veillez à les regrouper avec les pages qui les utilisent.
   * Assurez-vous que les [autorisations des balises](#setting-tag-permissions) permettent l’accès en lecture.

## Console Balisage {#tagging-console}

La console Balisage permet de créer et de gérer des balises et leur taxonomie. Elle vise entre autres à éviter d’avoir de nombreuses balises similaires, qui renvoient essentiellement aux mêmes aspects : par exemple, page et pages ou chaussures et souliers.

Les balises sont gérées en les regroupant dans des espaces de noms, en vérifiant l’utilisation des balises existantes avant d’en créer d’autres et en les réorganisant sans déconnecter la balise du contenu actuellement référencé.

Pour accéder à la console Balisage, procédez comme suit :

* Sur l’instance de création.
* Connectez-vous avec des droits d’administrateur.
* Dans la navigation générale

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_using_thetagasAdministration Console](assets/managing_tags_usingthetagasministrationconsolea.png)

### Création d’un espace de noms {#creating-a-namespace}

To create a new namespace, select the **`Create Namespace`** icon.

L’espace de noms est lui-même une balise et ne comporte pas forcément de balise secondaire. Cependant, pour poursuivre la création d’une taxonomie, [créez des balises secondaires](#creating-tags), qui peuvent être des balises terminales ou conteneurs.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Titre**

   *(obligatoire)* Titre d’affichage de l’espace de nommage.

* **Nom**
   *(facultatif)* Nom de l’espace de nommage. Si aucun nom n’est spécifié, un nom de nœud valide est créé à partir du titre. See [TagID](/help/sites-developing/framework.md#tagid).

* **Description**

   *(facultatif)* Description de l’espace de nommage.

Une fois que les informations nécessaires ont été saisies :

* Sélectionnez **Créer**.

### Opérations sur les balises {#operations-on-tags}

La sélection d’un espace de noms ou d’une autre balise rend les opérations ci-dessous disponibles :

* [Afficher les propriétés](#viewing-tag-properties)
* [Références](#showing-tag-references)
* [Créer une balise](#creating-tags)
* [Modifier](#editing-tags)
* [Déplacer](#moving-tags)
* [Fusionner](#merging-tags)
* [Publication](#publishing-tags)
* [Annuler la publication](#unpublishing-tags)
* [Supprimer](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

When the browser window is not wide enough to display all icons, then the right-most icons are grouped together under a **`... More`** icon, which will display a drop-down list of the hidden operation icons when selected.

![chlimage_1-185](assets/chlimage_1-185.png)

### Sélection d’une balise d’espace de noms {#selecting-a-namespace-tag}

Lorsqu’un espace de noms est sélectionné pour la première fois, s’il ne contient aucune balise, les propriétés sont affichées à droite. Sinon, ce sont les balises enfants qui s’affichent. Chaque balise sélectionnée affiche les balises qu’elle contient ou ses propriétés si elle ne comporte pas de balises enfants.

Pour sélectionner une ou plusieurs balises pour des opérations, cliquez une seule fois sur l’icône en regard du titre. Cela a pour effet d’afficher les propriétés ou d’ouvrir la balise pour en afficher le contenu.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Affichage des propriétés de balise {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

When a namespace or other tag is selected, selecting the **`View Properties`** icon results in the display of information as to the `name`, time of last edit, and number of references. En cas de publication, l’heure de dernière publication et l’identifiant de la personne à l’origine de la publication s’affichent. Ces informations s’affichent dans une colonne à gauche des colonnes de balises.

![chlimage_1-189](assets/chlimage_1-189.png)

### Affichage des références des balises {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Lorsqu’un espace de noms ou une autre balise est sélectionné, si vous cliquez sur l’icône **Références**, le contenu auquel la balise fait référence est identifié.

L’affichage initial correspond au nombre de balises appliquées.

![chlimage_1-191](assets/chlimage_1-191.png)

Sélectionnez la flèche à droite du nombre pour connaître le nom des références.

Le chemin d’accès à la référence s’affiche sous la forme d’infobulle lorsque vous passez le curseur de la souris sur une référence.

![chlimage_1-192](assets/chlimage_1-192.png)

### Création de balises {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

When a namespace or other tag is selected (by selecting the icon next to the title), a child tag may be created for the current tag by selecting the **`Create Tag`** icon.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Titre*** (obligatoire) *Titre d’affichage de la balise.

* **Nom***(facultatif) *Nom de la balise. Si aucun nom n’est spécifié, un nom de nœud valide est créé à partir du titre. See [TagID](/help/sites-developing/framework.md#tagid).

* **Description***(facultatif) *Description de la balise.

Une fois que les informations nécessaires ont été saisies :

* Sélectionnez **Créer**.

### Modification de balises {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

When a namespace or other tag is selected, it is possible to alter the Title, Description, and provide localizations of the Title by selecting the **`Edit`**icon.

Une fois les modifications apportées, sélectionnez **Enregistrer**.

For details about adding language translations, see the section on [Managing Tags in Different Languages](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Déplacement des balises {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

When a namespace or other tag is selected, selecting the **`Move`** icon will allow Tags Administrators and Developers to clean up the taxonomy by moving the tag to a new location or renaming it. Si la balise sélectionnée est une balise conteneur, le fait de la déplacer déplace également toutes les balises enfants.

>[!NOTE]
>
>It is recommended that Authors only be allowed to [edit](#editing-tags) the tag&#39;s `title`, not to move or rename tags.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Chemin**

   *(lecture seule)* Chemin d’accès actuel à la balise sélectionnée.

* **Déplacer vers** Accédez au nouveau chemin d’accès où déplacer la balise.

* **Renommer sur** Initialement affiche le 
`name`de la balise . A new `name`may be entered.

* Sélectionnez **Enregistrer**.

### Fusion des balises {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

Il est également possible de recourir à la fusion de balises lorsqu’une taxonomie comporte des doublons. Si la balise A est fusionnée dans la balise B, toutes les pages balisées avec la balise A sont balisées avec la balise B, et la balise A n’est plus disponible pour les auteurs.

When a namespace or other tag is selected, selecting the **Merge** icon will open a panel where the path to merge into may be selected.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Chemin**

   *(lecture seule)* Chemin d’accès de la balise sélectionnée pour être fusionnée dans une autre balise.

* **Fusionner dans** Accédez au chemin d’accès de la balise où effectuer la fusion.

>[!NOTE]
>
>Après la fusion, le **Chemin d’accès** qui avait été initialement sélectionné n’existe (pratiquement) plus.
>
>Si une balise référencée est déplacée ou fusionnée, elle n’est pas physiquement supprimée, de sorte qu’il est possible de conserver les références.

### Publication de balises {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

When a namespace or other tag is selected, selecting the **Publish** icon to activate the tag in the publish environment. De même que pour le contenu d’une page, seule la balise sélectionnée est publiée, qu’il s’agisse d’une balise conteneur ou non.

Pour publier une taxonomie (un espace de noms et des balises secondaires), il est recommandé de créer un [module](/help/sites-administering/package-manager.md) de l’espace de noms (voir [Nœud racine de taxonomie](/help/sites-developing/framework.md#taxonomy-root-node)). Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.

### Annulation de la publication de balises {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

When a namespace or other tag is selected, selecting the **Unpublish** icon will deactivate the tag in the author environment and remove it from the publish environment. Similar to the `Delete`operation, if the selected tag is a container tag, all of its child tags will be deactivated in the author environment and removed from the publish environment.

### Suppression des balises {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

When a namespace or other tag is selected, selecting the **Delete** icon will permanently remove the tag from the author environment. Si la balise a été publiée, elle est également supprimée de l’environnement de publication. Si la balise sélectionnée est une balise conteneur, toutes ses balises enfants sont elles aussi supprimées.

## Définition des autorisations de balises {#setting-tag-permissions}

Tag permissions are [&#39;secure (by default)&#39;](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Pour ce faire, il suffit grosso modo de créer un module d’espace de noms de balises une fois que les autorisations ont été définies dans l’instance de création, puis d’installer le module sur toutes les instances de publication.

* Sur l’instance de création

   * Connectez-vous avec des droits d’administrateur.
   * Accédez à la [console Sécurité](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console).

      * Par exemple, http://localhost:4502/useradmin.
   * Dans le volet de gauche, sélectionnez le groupe (ou l’utilisateur) auquel accorder une [autorisation de lecture](/help/sites-administering/security.md#permissions).
   * dans le volet de droite, recherchez le **Path **to the Tag Espace de nommage.

      * par exemple, `/content/cq:tags/mycommunity`
   * select the `checkbox`in the **Read** column
   * sélectionnez **Enregistrer**



![chlimage_1-204](assets/chlimage_1-204.png)

* Assurez-vous que toutes les instances de publication disposent des mêmes autorisations.

   * Une méthode consiste à [créer un module](/help/sites-administering/package-manager.md#package-manager) de l’espace de noms sur l’instance de création.

      * sur `Advanced` l’onglet, pour `AC Handling` sélectionner `Overwrite`
   * Répliquez le module.

      * choose `Replicate` from package manager


## Gestion des balises dans différentes langues {#managing-tags-in-different-languages}

The `title`property of a tag may be translated into multiple languages. Once translated, the appropriate tag `title`may be displayed according to the user language or to the page language.

### Définition de titres de balises dans plusieurs langues {#defining-tag-titles-in-multiple-languages}

The following describes how to translate the `title`of the tag **Animals** from English into German and French.

Start by selecting the tag under the **Stock Photography** namespace and selecting the **`Edit`**icon (see [Editing Tags](#editing-tags) section).

Dans le panneau Modifier la balise, choisissez les langues dans lesquelles localiser le titre de la balise.

À mesure que chaque langue est sélectionnée, une zone de saisie de texte s’affiche, dans laquelle vous pouvez saisir le titre traduit.

Une fois toutes les traductions saisies, sélectionnez **Enregistrer** pour quitter le mode de modification.

![chlimage_1-205](assets/chlimage_1-205.png)

En général, la langue sélectionnée pour la balise dépend de la langue de la page, le cas échéant. Si le widget [`tag` est utilisé dans d’autres cas (dans des formulaires ou des boîtes de dialogue, par exemple), la langue du tag dépend du contexte.](/help/sites-developing/building.md#tagging-on-the-client-side)

Plutôt que d’utiliser le paramètre de langue de la page, la console Balisage utilise le paramètre de langue de l’utilisateur. Dans la console Balisage, pour la balise « Animals », « Animaux » s’affiche pour un utilisateur qui a défini la langue française dans ses propriétés d’utilisateur.

To add a new language to the dialog, see [Adding a New Language to the Edit Tag Dialog](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>The tag cloud and the meta keywords in the standard page component use the localized tag `titles`based on the page language, if available.

## Ressources {#resources}

* [Balisage pour les développeurs](/help/sites-developing/tags.md)

   Informations sur la structure de balisage, ainsi que sur l’extension et l’inclusion de balises dans les applications personnalisées.

* [Console Balisage de l’interface utilisateur classique](/help/sites-administering/classic-console.md)

