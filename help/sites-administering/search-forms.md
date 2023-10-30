---
title: Configurer des formulaires de recherche
description: Découvrez comment utiliser Search Forms pour personnaliser la sélection des prédicats de recherche utilisés dans les panneaux de recherche disponibles dans AEM consoles et panneaux de l’environnement de création.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 74%

---


# Configuration des formulaires de recherche{#configuring-search-forms}

Utilisez des **formulaires de recherche** pour personnaliser la sélection des prédicats de recherche utilisés dans les panneaux de recherche disponibles dans différents panneaux ou consoles AEM de l’environnement de création. La personnalisation de ces panneaux rend la fonctionnalité de recherche polyvalente selon vos besoins spécifiques.

Une [plage de prédicats](#predicates-and-their-settings) prête à l’emploi est disponible. Vous pouvez ajouter plusieurs prédicats, y compris (entre autres) le prédicat Propriété, pour rechercher des ressources correspondant à une seule propriété que vous avez spécifiée. Ou, le prédicat Options permet de rechercher des ressources qui correspondent à une ou plusieurs valeurs que vous spécifiez pour une propriété spécifique.

Vous pouvez [configurer les formulaires de recherche](#configuring-your-search-forms) utilisés dans différentes consoles et l’explorateur des ressources (lors de la modification des pages). Les [boîtes de dialogue de configuration de ces formulaires](#configuring-your-search-forms) sont accessible via :

* **Outils**

   * **Général**

      * **Formulaires de recherche**

Lorsque vous accédez à cette console pour la première fois, vous pouvez constater que toutes les configurations comportent un symbole de cadenas. Cela signifie que la configuration appropriée est la configuration par défaut (prête à l’emploi) et qu’elle ne peut pas être supprimée. Une fois la configuration personnalisée, le verrou disparaît sauf si vous [supprimer votre configuration personnalisée](#deleting-a-configuration-to-reinstate-the-default). Dans ce cas, la valeur par défaut (et l’indicateur de cadenas) est rétablie.

![Fenêtre Formulaires de recherche](assets/chlimage_1-374.png)

## Configurations {#configurations}

Les configurations par défaut disponibles sont les suivantes :

* **Éditeur de page (recherche de documents) :**

  Cette configuration définit les options disponibles lors de la recherche de documents dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche d’images) :**

  Cette configuration définit les options disponibles lors de la recherche d’images dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de manuscrits) :**

  Cette configuration définit les options disponibles lors de la recherche de manuscrits dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de pages) :**

  Cette configuration définit les options disponibles lors de la recherche de pages dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de paragraphes) :**

  Cette configuration définit les options disponibles lors de la recherche de paragraphes dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de produits) :**

  Cette configuration définit les options disponibles lors de la recherche de produits dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche dans Dynamic Media Classic, [anciennement Scene7])** :

  Cette configuration définit les options disponibles lors de la recherche de ressources Scene7 dans l’explorateur de ressources (lors de la modification d’une page).

* **Rail de recherche d’administration de sites** :

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous utilisez le rail de recherche de la console Sites.

* **Éditeur de page (recherche de vidéos) :**

  Cette configuration définit les options disponibles lors de la recherche de vidéos dans l’explorateur de ressources (lors de la modification d’une page).

* **Rail de recherche d’administration de ressources :**

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous utilisez le rail de recherche de la console Assets.

* **Rail de recherche d’administration de catalogues :**

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous effectuez une recherche dans un catalogue de commerce.

* **Rail de recherche d’administration de commandes :**

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous recherchez des commandes de commerce.

* **Rail de recherche d’administration de collections de produits :**

  Cette configuration définit les options de recherche disponibles lors de la recherche de collections de produits de commerce.

* **Rail de recherche d’administration de produits :**

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous recherchez des produits de commerce.

* **Rail de recherche d’administration de projets :**

  Cette configuration définit les options de recherche que vous pouvez sélectionner lorsque vous effectuez une recherche de projets.

## Prédicats et paramètres associés {#predicates-and-their-settings}

### Prédicats {#predicates}

En fonction de la configuration, les prédicats disponibles sont les suivants :

<table>
 <tbody>
  <tr>
   <th>Prédicat</th>
   <th>Objectif</th>
   <th>Paramètres</th>
  </tr>
  <tr>
   <td>Analyses </td>
   <td>Fonctionnalités de recherche/filtrage dans le navigateur Sites lors de l’affichage de données optimisées par l’analyse. Les filtres de recherche Analyses sont chargés de façon à correspondre aux colonnes Analyses personnalisées mappées.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dernière modification de la ressource </td>
   <td>Date de dernière modification de la ressource.<br /> </td>
   <td>Prédicat personnalisé, en fonction du prédicat de date.</td>
  </tr>
  <tr>
   <td>Composants </td>
   <td>Permet à un auteur de rechercher/filtrer des pages comportant un composant spécifique. Par exemple, une galerie d’images.<br /> </td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Espace réservé</li>
     <li>Nom de la propriété*</li>
     <li>Détails de propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plage </td>
   <td>Recherche de ressources à l’aide d’un curseur en fonction d’une propriété de date.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plage de dates </td>
   <td>Recherche de ressources créées dans une plage spécifiée pour une propriété de date. Dans le panneau Rechercher, vous pouvez spécifier des dates de début et de fin.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Espace réservé</li>
     <li>Nom de la propriété*</li>
     <li>Texte de la plage (De)*</li>
     <li>Texte de la plage (À)*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>État d’expiration </td>
   <td>Recherche de ressources en fonction de leur statut d’expiration.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Taille de fichier </td>
   <td>Recherche de ressources en fonction de leur taille.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Masqué  Filtrer</td>
   <td>Filtrez selon la propriété et la valeur, invisible pour l’utilisateur.</td>
   <td>
    <ul>
     <li>Nom de la propriété</li>
     <li>Valeur de la propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Options </td>
   <td><p>Les options sont des nœuds de contenu créés par l’utilisateur.</p> <p>Pour plus d’informations, voir <a href="#addinganoptionspredicate">Ajout d’un prédicat Options</a>.</p> </td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Chemin d’accès JSON</li>
     <li>Nom de la propriété*</li>
     <li>Sélection simple</li>
     <li>Chemin d’accès aux options</li>
     <li>sa description ;</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriété des options </td>
   <td>Recherche d’une propriété de l’option.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès au nœud d’options<br /> </li>
     <li>Sélection simple</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>État de la page </td>
   <td>Filtre de pages en fonction de leur statut.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété de publication</li>
     <li>Nom de propriété LiveCopy</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Chemin  </td>
   <td>Recherche de ressources situées sous un chemin d’accès spécifique.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Ajout d’un chemin de recherche</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriété </td>
   <td>Effectuez une recherche sur une propriété spécifiée.</td>
   <td>aucune</td>
  </tr>
  <tr>
   <td>Statut de publication </td>
   <td>Recherche de ressources en fonction de leur statut de publication</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plage </td>
   <td>Recherchez des ressources figurant dans une plage spécifiée. Vous pouvez spécifier, dans le panneau Rechercher, les valeurs minimale et maximale de la plage concernée.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Options de plage </td>
   <td>Prédicat de recherche spécifique pour les ressources et identique au prédicat de curseur commun. est toujours disponible en raison de problèmes de rétrocompatibilité ;</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Évaluation </td>
   <td>Recherche de ressources en fonction de leur évaluation.<br /> </td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Date relative </td>
   <td>Filtre de ressources en fonction de la date relative de leur création<br /> </td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Date relative</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plage du curseur </td>
   <td>Prédicat de recherche courant qui étend le prédicat de plage avec la fonctionnalité de curseur. La valeur de la propriété recherchée doit être comprise entre les limites du curseur.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Balise </td>
   <td>Recherche de ressources en fonction de leurs balises. Vous pouvez configurer la propriété de chemin d’accès pour renseigner les différentes balises dans la liste de balises.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Balises </td>
   <td>Effectuez une recherche en fonction de balises.</td>
   <td>
    <ul>
     <li>Espace réservé</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Les prédicats de recherche courants sont définis dans :
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* Les prédicats de recherche liés uniquement à siteadmin (IU classique) se trouvent sous :
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * Ils sont obsolètes et disponibles uniquement à des fins de rétrocompatibilité.
>
>Ces informations sont proposées à titre de référence uniquement. Ne pas modifier `/libs`.

### Paramètres de prédicat {#predicate-settings}

En fonction du prédicat, une sélection de paramètres est disponible pour la configuration :

* **Libellé du champ**

  Libellé qui s’affiche sous la forme de l’en-tête réductible ou du libellé du champ du prédicat.

* **Description**

  Informations descriptives à l’intention de l’utilisateur.

* **Espace réservé**

  Texte non renseigné ou espace réservé du prédicat au cas où aucun texte de filtrage ne serait saisi.

* **Nom de la propriété**

  Propriété selon laquelle effectuer la recherche. Elle utilise un chemin relatif et les caractères génériques `*/*/*` pour spécifier la profondeur de la propriété par rapport au nœud `jcr:content` (chaque astérisque représente un niveau de nœud).

  Si vous souhaitez effectuer une recherche uniquement sur un noeud enfant de premier niveau de la ressource qui a la propriété `x` sur la propriété `jcr:content` node use `*/jcr:content/x`

* **Détails de propriété**

  Détails maximum selon lesquels rechercher cette propriété dans les ressources. Une recherche sur cette propriété peut donc être exécutée sur une ressource et des enfants récursifs jusqu’au niveau auquel les enfants sont égaux à la profondeur spécifiée.

* **Valeur de la propriété**

  Valeur de la propriété sous forme de chaîne absolue ou de langage utilisant des expressions ; par exemple, `cq:Page` ou

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texte de la plage**

  Libellé du champ de plage dans le prédicat **Plage de dates**.

* **Chemin d’accès aux options**

  L’utilisateur peut sélectionner le chemin d’accès à l’aide de l’Explorateur de chemins d’accès dans l’onglet Paramètres de prédicat, Après avoir sélectionné **+**, l’icône permet d’ajouter la sélection à la liste des options valides (puis la fonction **-** pour la supprimer, le cas échéant).

  Les options sont des nœuds de contenu créés par l’utilisateur, qui possèdent la structure suivante :

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Chemin d’accès au nœud d’options**
Globalement identique à **Chemin d’accès aux options**, à la différence qu’il se trouve dans le champ de prédicat commun, tandis que l’autre est spécifique aux ressources.

* **Sélection simple**
Si cette case est cochée, les options sont présentées sous forme de cases à cocher qui ne permettent qu’une sélection simple. Si cette option est sélectionnée par erreur, vous pouvez désélectionner la case à cocher correspondante.

* **Noms des propriétés de publication et de Live Copy**
Étiquettes des cases à cocher Publication et Live Copy pour le prédicat spécifique aux sites.

* L’astérisque (&amp;ast;) figurant dans les libellés de champ de la variable **Paramètres** signifient que les champs sont obligatoires et qu’un message d’erreur s’affiche si rien n’est indiqué.

## Configuration des formulaires de recherche {#configuring-your-search-forms}

### Création et ouverture d’une configuration personnalisée {#creating-opening-a-customized-configuration}

1. Accédez à **Outils** &quot;  **Général** &quot; **Rechercher dans Forms**.

1. Sélectionnez la configuration à personnaliser.
1. Cliquez sur l’icône **Modifier** pour ouvrir la configuration à mettre à jour.
1. Si vous souhaitez effectuer une nouvelle personnalisation, vous souhaiterez probablement [ajouter de nouveaux champs de prédicat et définir les paramètres](#add-edit-a-predicate-field-and-define-field-settings) selon les besoins. Si une personnalisation existante existe, vous pouvez sélectionner un champ existant et [mettre à jour les paramètres](#add-edit-a-predicate-field-and-define-field-settings).
1. Sélectionnez **Terminé** pour enregistrer la configuration.

   >[!NOTE]
   >
   >Les configurations personnalisées sont enregistrées (de façon appropriée) sous :
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Ajout et modification d’un champ de prédicat et définition des paramètres de champ {#add-edit-a-predicate-field-and-define-field-settings}

Vous pouvez ajouter ou modifier des champs et définir/mettre à jour leurs paramètres :

1. [Ouvrez la configuration personnalisée](#creating-opening-a-customized-configuration) pour la mise à jour.
1. Si vous souhaitez ajouter un champ, ouvrez le **Sélectionner un prédicat** et faites glisser le prédicat requis vers l’emplacement requis. Par exemple, le **prédicat de période** :

   ![Modification d’un formulaire de recherche](assets/chlimage_1-375.png)

1. Selon que :

   * Vous ajoutez un champ :

     Après avoir ajouté le prédicat, la variable **Paramètres** s’ouvre et affiche les propriétés qui peuvent être définies.

   * Vous souhaitiez ou non mettre à jour un prédicat existant :

     Sélectionnez le champ de prédicat (à droite), puis ouvrez l’onglet **Paramètres**.

   Par exemple, les paramètres du **prédicat de période** :

   ![Propriétés du prédicat de plage de dates](assets/chlimage_1-376.png)

1. Apportez les modifications nécessaires et confirmez-les en cliquant sur **Terminé**.

### Aperçu de la configuration de recherche {#previewing-the-search-configuration}

1. Sélectionnez l’icône Aperçu :

   ![Aperçu des formulaires de recherche](do-not-localize/chlimage_1-31.png)

1. Les formulaires de recherche s’affichent tels qu’ils sont affichés (entièrement développés) dans la colonne Rechercher de la console appropriée.

   ![Aperçu du formulaire de recherche](assets/chlimage_1-377.png)

1. **Fermer** l’aperçu afin que vous puissiez renvoyer et terminer la configuration.

### Suppression d’un champ de prédicat {#deleting-a-predicate-field}

1. [Ouvrez la configuration personnalisée](#creating-opening-a-customized-configuration) pour la mise à jour.
1. Sélectionnez le champ de prédicat (à droite), ouvrez l’onglet **Paramètres**, puis sélectionnez l’icône **Supprimer** (en bas à gauche).

   ![Icône Supprimer](do-not-localize/chlimage_1-32.png)

1. Une boîte de dialogue demande la confirmation de l’action de suppression.

1. Confirmez la suppression et les autres modifications en cliquant sur **Terminé**.

### Suppression d’une configuration (pour rétablir la valeur par défaut) {#deleting-a-configuration-to-reinstate-the-default}

Une fois que vous avez personnalisé une configuration, celle-ci remplace les valeurs par défaut. Vous pouvez rétablir la configuration par défaut en supprimant votre configuration personnalisée.

>[!NOTE]
>
>Vous ne pouvez supprimer aucune des configurations par défaut.

Les configurations personnalisées doivent être supprimées à partir de la console :

1. Sélectionnez une configuration (par exemple, **Éditeur de page (Recherche de paragraphes)**), puis cliquez sur l’icône **Supprimer** de la barre d’outils :

   ![Suppression d’un formulaire](assets/chlimage_1-378.png)

1. La configuration personnalisée est supprimée et la valeur par défaut est rétablie (le symbole de cadenas réapparaît dans la console).

### Ajouter des prédicats d’options {#adding-options-predicates}

Les prédicats d’options (options, propriété d’options) vous permettent de configurer un élément à rechercher. Ils sont utilisés pour rechercher quelque chose directement sous la page ; par exemple, une propriété sur le noeud de page.

L’exemple ci-dessous (pour effectuer une recherche en fonction du modèle utilisé pour créer une page) illustre la procédure :

1. Créez le nœud définissant la propriété à rechercher.

   Vous avez besoin d’un noeud racine contenant les définitions des différentes options disponibles pour l’utilisateur.

   Les nœuds pour les différentes options ont besoin de propriétés :

   * `jcr:title` : libellé de champ à afficher dans le champ de recherche
   * `value` : valeur de la propriété à rechercher

   ![Ajout d’options dans CRXDE](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >Do ***not*** modifiez les éléments du `/libs` chemin.
   >
   >En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
   >
   >La méthode recommandée pour la configuration et d’autres modifications est la suivante :
   >
   >1. Recréez l’élément nécessaire, tel qu’il existe dans `/libs`, sous `/apps`. Dans ce cas dans :
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Apportez les modifications désirées dans `/apps.`

1. Ouvrez la console **Formulaires de recherche** et sélectionnez la configuration à mettre à jour. Par exemple, le **rail de recherche d’administration de sites**.

   Ensuite, cliquez/appuyez sur le bouton **Modifier les formulaires de recherche** Icône

1. Selon la configuration, ajoutez une **Options** ou **Propriété Options** à la configuration.
1. Mettez à jour les champs, notamment :

   * **Nom de la propriété**

     Spécifique à la propriété du nœud à rechercher sur les nœuds cibles. Par exemple :

     `jcr:content/cq:template`

   * **Chemin d’accès du nœud d’option**

     Sélectionnez le chemin d’accès vers lequel vos options sont conservées. Par exemple :

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Ajout d’un chemin de propriété](assets/chlimage_1-380.png)

1. Sélectionnez **Terminé** pour enregistrer la configuration.
1. Accédez à la console appropriée (dans cet exemple, **Sites**) et ouvrez le rail **Rechercher**. Les formulaires de recherche qui viennent d’être définis, ainsi que les différentes options, sont visibles. Sélectionnez l’option requise pour afficher les résultats de la recherche :

   ![Les résultats finaux](assets/chlimage_1-381.png)

## Autorisations d’utilisateur {#user-permissions}

Le tableau ci-dessous répertorie les autorisations nécessaires à la modification, à la suppression et à l’aperçu dans des formulaires de recherche.

<table>
 <tbody>
  <tr>
   <td><strong>Action</strong></td>
   <td><strong>Autorisations</strong></td>
  </tr>
  <tr>
   <td>Modifier </td>
   <td>Autorisations de lecture et d’écriture sur le nœud <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Supprimer</td>
   <td>Autorisations de lecture, d’écriture et de suppression sur le nœud <code>/apps</code>.</td>
  </tr>
  <tr>
   <td>Aperçu</td>
   <td>Autorisations de lecture, d’écriture et de suppression sur le nœud <code>/var/dam/content</code>.<br /> Autorisations de lecture et d’écriture sur le nœud <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
