---
title: Configuration des formulaires de recherche
seo-title: Configuration des formulaires de recherche
description: Découvrez comment configurer des formulaires de recherche.
seo-description: Découvrez comment configurer des formulaires de recherche.
uuid: 0d30921c-0d4d-4ab6-b796-7833cd321e5d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: abc27987-960e-48da-9580-1008a2bdc94c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration des formulaires de recherche{#configuring-search-forms}

Utilisez des **formulaires de recherche** pour personnaliser la sélection des prédicats de recherche utilisés dans les panneaux de recherche disponibles dans différents panneaux ou consoles AEM de l’environnement de création. La personnalisation de ces panneaux permet d’adapter la fonctionnalité de recherche à vos besoins.

Une [plage de prédicats](#predicates-and-their-settings) prête à l’emploi est disponible. Vous pouvez ajouter plusieurs prédicats, dont (entre autres) le prédicat Texte intégral pour les recherches en texte intégral, le prédicat Propriété pour rechercher des ressources correspondant à une propriété unique que vous avez spécifiée ou le prédicat Options pour rechercher des ressources correspondant à une ou plusieurs valeurs que vous spécifiez pour une propriété donnée.

Vous pouvez [configurer les formulaires de recherche](#configuring-your-search-forms) utilisés dans différentes consoles et l’explorateur des ressources (lors de la modification des pages). Les [boîtes de dialogue de configuration de ces formulaires](#configuring-your-search-forms) sont accessibles en sélectionnant :

* **Outils**

   * **Général**

      * **Formulaires de recherche**

Lorsque vous accédez à cette console pour la première fois, vous pouvez constater que toutes les configurations comportent un symbole de cadenas. Cela signifie que la configuration appropriée est la configuration par défaut (prête à l’emploi) et qu’elle ne peut pas être supprimée. Une fois que vous avez personnalisé la configuration, le cadenas disparaît sauf si vous [supprimez la configuration personnalisée](#deleting-a-configuration-to-reinstate-the-default), auquel cas la valeur par défaut (et le symbole de cadenas) est rétablie.

![chlimage_1-374](assets/chlimage_1-374.png)

## Configurations {#configurations}

Les configurations par défaut disponibles sont les suivantes :

* **Éditeur de page (recherche de documents):**

   Cette configuration définit les options disponibles lors de la recherche de documents dans l’explorateur d’actifs (lors de la modification d’une page).

* **Éditeur de page (recherche d’images):**

   Cette configuration définit les options disponibles lors de la recherche d’images dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de manuscrits):**

   Cette configuration définit les options disponibles lors de la recherche de manuscrits dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche de pages):**

   Cette configuration définit les options disponibles lors de la recherche de pages dans l’explorateur d’actifs (lors de la modification d’une page).

* **Éditeur de page (recherche de paragraphes):**

   Cette configuration définit les options disponibles lors de la recherche de paragraphes dans l’explorateur d’actifs (lors de la modification d’une page).

* **Éditeur de page (recherche de produits):**

   Cette configuration définit les options disponibles lors de la recherche de produits dans l’explorateur de ressources (lors de la modification d’une page).

* **Éditeur de page (recherche Scene7)**:

   Cette configuration définit les options disponibles lors de la recherche de ressources Scene7 dans l’explorateur de ressources (lors de la modification d’une page).

* **Rail de recherche d’administration de site**:

   Cette configuration définit les options de recherche disponibles pour l&#39;utilisateur lors de l&#39;utilisation du rail de recherche de la console Sites.

* **Éditeur de page (recherche de vidéos):**

   Cette configuration définit les options disponibles lors de la recherche de vidéos dans le navigateur de ressources (lors de la modification d’une page).

* **Rail de recherche d’administrateurs de ressources:**

   Cette configuration définit les options de recherche disponibles pour l’utilisateur lors de l’utilisation de la console Ressources.

* **Rail de recherche d’administrateurs de catalogues:**

   Cette configuration définit les options de recherche disponibles pour l’utilisateur lors de la recherche dans un catalogue de commerce.

* **Rail de recherche d’administrateurs de commandes:**

   Cette configuration définit les options de recherche disponibles pour l&#39;utilisateur lors de la recherche de commandes commerciales.

* **Rail de recherche d’administrateurs de collections de produits:**

   Cette configuration définit les options de recherche disponibles pour l’utilisateur lors de la recherche de collections de produits commerciaux.

* **Rail de recherche d’administrateurs de produits:**

   Cette configuration définit les options de recherche disponibles pour l’utilisateur lors de la recherche de produits commerciaux.

* **Rail de recherche d’administrateurs de projets:**

   Cette configuration définit les options de recherche disponibles pour l’utilisateur lors de la recherche de projets.

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
   <td>Analyse </td>
   <td>Fonctionnalités de recherche/filtrage dans le navigateur Sites lors de l’affichage des données optimisées par Analytics. Les filtres de recherche Analytics se chargent jusqu’à correspondre aux colonnes d’analyses personnalisées mappées.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dernière modification de la ressource </td>
   <td>Date de la dernière modification du fichier.<br /> </td>
   <td>Prédicat personnalisé, basé sur l’attribut de date.</td>
  </tr>
  <tr>
   <td>Composants </td>
   <td>Permet à un auteur de rechercher/filtrer les pages comportant un composant spécifique. Par exemple, une galerie d’images.<br /> </td>
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
   <td>Date </td>
   <td>Recherche de fichiers selon un curseur en fonction d’une propriété de date.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Date Plage </td>
   <td>Recherchez les ressources créées dans une plage spécifiée pour une propriété de date. Dans le panneau Rechercher, vous pouvez spécifier des dates de début et de fin.</td>
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
   <td>Recherche de fichiers en fonction de l’état d’expiration.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Taille de fichier </td>
   <td>Recherchez des fichiers en fonction de leur taille.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Texte intégral </td>
   <td>Prédicat de recherche pour les recherches en texte intégral..</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Espace réservé</li>
     <li>Nom de la propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtre masqué</td>
   <td>Filtre sur la propriété et la valeur, invisible pour l’utilisateur.</td>
   <td>
    <ul>
     <li>Nom de la propriété</li>
     <li>Valeur de la propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Options </td>
   <td><p>Les options sont des noeuds de contenu créés par l’utilisateur.</p> <p>See <a href="#addinganoptionspredicate">Adding an Options Predicate</a> for more information.</p> </td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Chemin d'accès JSON</li>
     <li>Nom de la propriété*</li>
     <li>Sélection simple</li>
     <li>Chemin d’accès aux options</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Options, propriété </td>
   <td>Recherchez une propriété de l’option.</td>
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
   <td>Page État </td>
   <td>Rechercher des pages en fonction de leur état.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété de publication</li>
     <li>Nom de propriété LiveCopy</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Chemin </td>
   <td>Rechercher des fichiers situés sous un chemin spécifique.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Ajouter un chemin de recherche</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriétés </td>
   <td>Recherche sur une propriété spécifiée.</td>
   <td>none</td>
  </tr>
  <tr>
   <td>État de publication </td>
   <td>Recherche de fichiers en fonction de leur état de publication</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Plage </td>
   <td>Rechercher des ressources qui se trouvent dans une plage spécifiée. Vous pouvez spécifier, dans le panneau Rechercher, les valeurs minimale et maximale de la période concernée.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Options d’étendue </td>
   <td>Un prédicat de recherche spécifique pour les ressources et le même prédicat de curseur commun. Il reste disponible en raison de problèmes de rétrocompatibilité.</td>
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
   <td>Recherchez des ressources en fonction de leur évaluation.<br /> </td>
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
   <td>Search assets based on the relative date of their creation<br /> </td>
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
   <td>Un prédicat de recherche courant étend le prédicat de plage avec la fonctionnalité de curseur. La valeur de la propriété recherchée doit être comprise entre les limites du curseur.</td>
   <td>
    <ul>
     <li>Libellé du champ</li>
     <li>Nom de la propriété*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Balise </td>
   <td>Recherche de fichiers en fonction de balises. Vous pouvez configurer la propriété de chemin d’accès pour renseigner les différentes balises dans la liste de balises.</td>
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
   <td>Recherche basée sur des balises.</td>
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
>* Les prédicats de recherche courants sont définis dans :
   >  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
   >
   >
   >

* Les prédicats de recherche liés uniquement à siteadmin (interface utilisateur classique) se trouvent sous :
   > `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
   >   * Elles sont obsolètes et disponibles uniquement pour une compatibilité ascendante.
>
>
Ces informations sont proposées à des fins de référence seulement. Vous ne devez pas apporter de modifications au répertoire `/libs`.

### Paramètres de prédicat {#predicate-settings}

En fonction du prédicat, une sélection de paramètres est disponible pour la configuration :

* **Libellé du champ**

   Libellé qui apparaîtra comme en-tête réductible ou comme libellé de champ du prédicat.

* **Description**

   Description de l’utilisateur.

* **Espace réservé**

   Texte vide ou espace réservé du prédicat au cas où aucun texte de filtrage n’est saisi.

* **Nom de la propriété**

   Propriété à rechercher. It uses a relative path and the wildcards `*/*/*` specify the depth of the property relative to the `jcr:content` node (each asterisk represents one node level).

   If you want to search only on a first level child node of the resource that has the `x` property on the `jcr:content` node use `*/jcr:content/x`

* **Détails de propriété**

   Profondeur maximale pour rechercher cette propriété dans les ressources. Une recherche sur cette propriété peut donc être exécutée sur une ressource et des enfants récursifs jusqu’au niveau auquel les enfants sont égaux à la profondeur spécifiée.

* **Valeur de la propriété**

   The property value as an absolute string or as an expression language; for example, `cq:Page` or

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texte de la plage**

   The label of the range field in the **Date Range** predicate.

* **Chemin d’accès aux options**

   L’utilisateur peut sélectionner le chemin d’accès à l’aide de l’explorateur de chemins dans l’onglet Paramètres de prédiction. puis cliquer sur l’icône « **+** » pour ajouter la sélection à la liste des options valides (puis sur l’icône « **-** » pour la supprimer, si nécessaire).

   Les options sont des noeuds de contenu créés par l’utilisateur, avec la structure suivante :

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Chemin d’accès au nœud d’options** Globalement identique à **Chemin d’accès aux options**, à la différence qu’il se trouve dans le champ de prédicat commun, tandis que l’autre est spécifique aux ressources.

* **Sélection simple** Si cette case est cochée, les options sont présentées sous forme de cases à cocher qui ne permettent qu’une sélection simple. Si cette option est sélectionnée par erreur, une case à cocher peut être désélectionnée.

* **Nom des propriétés de publication et Live Copy** Libellés des cases à cocher Publication et Live Copy pour le prédicat spécifique aux sites.

* The &amp;ast; on the field labels in the **Settings** tab means the fields are required and if left blank an error message will appear

## Configuration des formulaires de recherche {#configuring-your-search-forms}

### Création/ouverture d’une configuration personnalisée {#creating-opening-a-customized-configuration}

1. Sélectionnez **Outils** > **Opérations** > **Formulaires de recherche**.

1. Sélectionnez la configuration que vous souhaitez personnaliser.
1. Utilisez l’icône **Modifier** pour ouvrir la configuration pour la mise à jour.
1. S’il s’agit d’une nouvelle personnalisation, vous allez probablement [ajouter de nouveaux champs de prédicat et définir les paramètres](#add-edit-a-predicate-field-and-define-field-settings) requis. S’il s’agit d’une personnalisation existante, vous pouvez sélectionner un champ existant et [mettre à jour les paramètres](#add-edit-a-predicate-field-and-define-field-settings).
1. Sélectionnez **Terminé** pour enregistrer la configuration.

   >[!NOTE]
   >
   >Les configurations personnalisées sont enregistrées (de façon appropriée) sous :
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Ajout/modification d’un champ de prédicat et définition des paramètres de champ {#add-edit-a-predicate-field-and-define-field-settings}

Vous pouvez ajouter ou modifier des champs et définir/mettre à jour leurs paramètres :

1. [Ouvrez la configuration personnalisée](#creating-opening-a-customized-configuration) pour la mise à jour.
1. Si vous souhaitez ajouter un nouveau champ, ouvrez l’onglet **Sélectionner le prédicat** et faites glisser le prédicat souhaité vers l’emplacement souhaité. Par exemple, le **prédicat de plage de dates** :

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. Selon que :

   * Vous ajoutez un nouveau champ :

      Après avoir ajouté le prédicat, l’onglet **Paramètres** s’ouvre et affiche les propriétés qui peuvent être définies.

   * Vous souhaitez mettre à jour un prédicat existant :

      Sélectionnez le champ de prédicat (à droite), puis ouvrez l’onglet **Paramètres** .
   Par exemple, les paramètres du **prédicat de plage de dates** :

   ![chlimage_1-376](assets/chlimage_1-376.png)

1. Apportez les modifications nécessaires et confirmez-les en cliquant sur **Terminé**.

### Aperçu de la configuration de recherche {#previewing-the-search-configuration}

1. Sélectionnez l’icône Aperçu :

   ![](do-not-localize/chlimage_1-31.png)

1. Les formulaires de recherche s’affichent tels qu’ils apparaissent (totalement développés) dans la colonne Rechercher de la console appropriée.

   ![chlimage_1-377](assets/chlimage_1-377.png)

1. **Fermez** l’aperçu pour terminer la configuration.

### Suppression d’un champ de prédicat {#deleting-a-predicate-field}

1. [Ouvrez la configuration personnalisée](#creating-opening-a-customized-configuration) pour la mise à jour.
1. Sélectionnez le champ de prédicat (à droite), ouvrez l’onglet **Paramètres**, puis sélectionnez l’icône **Supprimer** (dans le coin inférieur gauche).

   ![](do-not-localize/chlimage_1-32.png)

1. Une boîte de dialogue vous invite à confirmer la suppression.

1. Confirmez la suppression et les autres modifications en cliquant sur **Terminé**.

### Suppression d’une configuration (pour rétablir la valeur par défaut) {#deleting-a-configuration-to-reinstate-the-default}

Une fois que vous avez personnalisé une configuration, cette option remplace les valeurs par défaut. Vous pouvez rétablir la configuration par défaut en supprimant la configuration personnalisée.

>[!NOTE]
>
>Vous ne pouvez pas supprimer les configurations par défaut.

Les configurations personnalisées doivent être supprimées à partir de la console :

1. Sélectionnez une configuration (par exemple, **Éditeur de page (Recherche sur des paragraphes)**), puis cliquez sur l’icône **Supprimer** de la barre d’outils :

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. La configuration personnalisée est supprimée et la valeur par défaut est rétablie (le symbole de cadenas réapparaît dans la console).

### Ajout de prédicats d’options {#adding-options-predicates}

Les prédicats d’options (options, propriété d’options) permettent de configurer un élément à rechercher. Ils servent généralement à rechercher un élément directement sous la page, par exemple, une propriété sur le nœud de page.

L’exemple ci-dessous (pour effectuer une recherche en fonction du modèle utilisé pour créer une page) illustre la procédure :

1. Créez le nœud définissant la propriété à rechercher.

   Vous avez besoin d’un nœud racine contenant les définitions des différentes options disponibles pour l’utilisateur.

   Les nœuds pour les différentes options ont besoin de propriétés :

   * `jcr:title` : libellé de champ à afficher dans le champ de recherche
   * `value` : valeur de la propriété à rechercher
   ![chlimage_1-379](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >You ***must*** not change anything in the `/libs` path.
   >
   >This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
   >
   >La méthode recommandée pour la configuration et d’autres modifications est la suivante :
   >
   >1. Recreate the required item, as it exists in `/libs`, under `/apps`. Dans ce cas dans :
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Make any changes within `/apps.`


1. Ouvrez la console **Formulaires de recherche** et sélectionnez la configuration à mettre à jour. Par exemple, le **rail de recherche d’administrateurs de sites**.

   Ensuite, cliquez/appuyez sur l’icône **Modifier des formulaires de recherche**.

1. En fonction de la configuration, ajoutez des **options** ou une **propriété d’options** à la configuration.
1. Mettez à jour les champs, en particulier :

   * **Nom de la propriété**

      Spécifiez la propriété de noeud à rechercher sur les noeuds cible. Par exemple :

      `jcr:content/cq:template`

   * **Chemin du noeud d’option**

      Sélectionnez le chemin vers lequel vos options sont conservées. Par exemple :

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![chlimage_1-380](assets/chlimage_1-380.png)

1. Sélectionnez **Terminé** pour enregistrer la configuration.
1. Accédez à la console appropriée (dans cet exemple, **Sites**) et ouvrez le rail **Rechercher**. Les formulaires de recherche qui viennent d’être définis, ainsi que les différentes options, sont visibles. Sélectionnez l’option nécessaire pour afficher les résultats de la recherche :

   ![chlimage_1-381](assets/chlimage_1-381.png)

## Autorisations d’utilisateur {#user-permissions}

Le tableau ci-dessous répertorie les autorisations nécessaires à la modification, à la suppression et à l’aperçu dans des formulaires de recherche.

<table>
 <tbody>
  <tr>
   <td><strong>Action</strong></td>
   <td><strong>Permissions</strong></td>
  </tr>
  <tr>
   <td>Modifier </td>
   <td>Autorisations de lecture et d’écriture sur le <code>/apps </code>noeud.</td>
  </tr>
  <tr>
   <td>Supprimer</td>
   <td>Autorisations de lecture, d’écriture et de suppression sur le <code>/apps</code> noeud</td>
  </tr>
  <tr>
   <td>Aperçu</td>
   <td>Autorisations de lecture, d’écriture et de suppression sur le <code>/var/dam/content</code> noeud.<br /> Autorisations de lecture et d’écriture sur le <code>/apps</code> noeud.</td>
  </tr>
 </tbody>
</table>

