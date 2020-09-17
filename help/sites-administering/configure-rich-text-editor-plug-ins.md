---
title: 'Configuration des modules externes d’éditeur de texte enrichi '
description: Découvrez comment configurer les modules externes Adobe Experience Manager Rich Text Editor pour activer des fonctionnalités individuelles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6f5e650c99017c4b2f04ca8495eea8481b3236cd
workflow-type: tm+mt
source-wordcount: '4398'
ht-degree: 95%

---


# Configuration des modules externes d’éditeur de texte enrichi  {#configure-the-rich-text-editor-plug-ins}

Les fonctionnalités d’éditeur de texte enrichi sont rendues disponibles par l’intermédiaire d’une série de modules externes, chacun avec sa propriété features. Vous pouvez configurer la propriété features afin d’activer ou de désactiver une ou plusieurs fonctions de l’éditeur de texte enrichi. Cet article décrit comment configurer spécifiquement les modules externes d’éditeur de texte enrichi.

Pour plus d’informations sur les autres configurations d’éditeur de texte enrichi, voir [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Lorsque vous utilisez CRXDE Lite, il est conseillé d’enregistrer régulièrement les modifications à l’aide de l’option [!UICONTROL Tout enregistrer].

## Activation d’un module externe et configuration de la propriété features {#activateplugin}

Pour activer un module externe, suivez ces étapes. Certaines étapes sont uniquement nécessaires lorsque vous configurez un module externe pour la première fois, car les nœuds correspondants n’existent pas.

Par défaut, les modules externes `format`, `link`, `list`, `justify` et `control`, ainsi que toutes leurs fonctions, sont activés dans l’éditeur de texte enrichi.

>[!NOTE]
>
>Le nœud `rtePlugins` respectif est désigné sous le nom de `<rtePlugins-node>` pour éviter les doublons dans cet article.

1. À l’aide de CRXDE Lite, cherchez le composant Texte pour votre projet.
1. Créez le nœud parent `<rtePlugins-node>` s’il n’existe pas, avant de configurer tout module externe d’éditeur de texte enrichi :

   * Selon votre composant, les nœuds parents sont les suivants :

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nœud de configuration alternatif : `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Ils sont du type : **jcr:primaryType** `cq:Widget`
   * Possèdent tous deux les propriétés suivantes :

      * **Nom** `name`
      * **Type** `String`
      * **Valeur** `./text`


1. Selon l’interface pour laquelle vous effectuez la configuration, créez un nœud `<rtePlugins-node>`, s’il n’existe pas :

   * **Nom** `rtePlugins`
   * **Type** `nt:unstructured`

1. Voici comment créer un nœud pour chaque module externe à activer :

   * **Type** `nt:unstructured`
   * **Nom** ID du module externe requis

Après activation d’un module externe, suivez ces instructions pour configurer la propriété `features`.

|  | Activer toutes les fonctions | Activer des fonctions spécifiques | Désactiver toutes les fonctions |
|---|---|---|---|
| Nom | features | features | features |
| Type | Chaîne | Chaîne[] (multichaîne ; définissez le type sur chaîne et cliquez sur Multi dans CRXDE Lite) | Chaîne |
| Valeur | `*` (astérisque) | définie sur une ou plusieurs valeurs de fonctions | - |

## Compréhension du module externe findreplace {#findreplace}

Le module externe `findreplace` n’a pas besoin de configuration. Il est prêt à l’emploi.

Lors de l’utilisation de la fonctionnalité de remplacement, la chaîne à remplacer doit être saisie en même temps que la chaîne de recherche. Cependant, vous pouvez toujours cliquer sur Rechercher pour rechercher la chaîne avant de la remplacer. Si la chaîne de remplacement est saisie après avoir cliqué sur Rechercher, la recherche est réinitialisée au début du texte.

La boîte de dialogue de recherche et de remplacement devient transparente lorsque l’utilisateur clique sur Rechercher et devient opaque lorsque l’utilisateur clique sur Remplacer. Cela permet à l’auteur de vérifier le texte qui sera remplacé. Si les utilisateurs cliquent sur Tout remplacer, la boîte de dialogue se ferme et affiche le nombre de remplacements effectués.

## Configuration des modes de collage {#pastemodes}

Lors de l’utilisation de l’éditeur de texte enrichi, les auteurs peuvent copier le contenu selon l’un des trois modes suivants :

* **Mode Navigateur** : collage de texte avec la mise en œuvre de collage par défaut du navigateur.  Il ne s’agit pas d’une méthode recommandée, car elle peut introduire des balises indésirables.

* **Mode Texte brut** : collage du contenu du Presse-papiers en tant que texte brut. Cela supprime tous les éléments de style et de mise en forme du contenu copié avant insertion dans le composant AEM.

* **Mode MS Word** : collage du texte, y compris des tableaux, avec la mise en forme lors de la copie à partir de MS Word. La copie et le collage de texte depuis une autre source, telle qu’une page web ou MS Excel ne sont pas pris en charge et conservent uniquement une mise en forme partielle.

### Configuration des options de collage disponibles sur la barre d’outils de l’éditeur de texte enrichi {#configure-paste-options-available-on-the-rte-toolbar}

Les trois icônes ci-dessous peuvent être mises à la disposition des auteurs dans la barre d’outils de l’éditeur de texte enrichi :

* **[!UICONTROL Coller (Ctrl + V)]** : peut être préconfigurée pour correspondre à l’un des trois modes de collage ci-dessus.

* **[!UICONTROL Coller en tant que texte]** : fournit la fonctionnalité du mode Texte brut.

* **[!UICONTROL Coller à partir de Word]** : fournit la fonctionnalité du mode MS Word.

Pour configurer l’éditeur de texte enrichi afin qu’il affiche les icônes requises, procédez comme suit.

1. Accédez à votre composant, par exemple `/apps/<myProject>/components/text`.
1. Accédez au nœud `rtePlugins/edit`. Voir [Activation d’un module externe](#activateplugin) si le nœud n’existe pas.
1. Créez la propriété `features` sur le nœud `edit` et ajoutez une ou plusieurs des fonctions. Enregistrez toutes les modifications.

### Configuration du comportement de l’icône Coller (Ctrl + V) et du raccourci {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Vous pouvez préconfigurer le comportement de l’icône **[!UICONTROL Coller (Ctrl + V)]** en procédant comme suit. Cette configuration définit également le comportement du raccourci clavier Ctrl + V que les auteurs utilisent pour coller du contenu.

Cette configuration permet trois scénarios d’utilisation, à savoir :

* Collage de texte avec la mise en œuvre de collage par défaut du navigateur. Il ne s’agit pas d’une méthode recommandée, car elle peut introduire des balises indésirables. Configuré à l’aide de `browser` ci-dessous.

* Collage du contenu du Presse-papiers en tant que texte brut. Cela supprime tous les éléments de style et de mise en forme du contenu copié avant insertion dans le composant AEM. Configuré à l’aide de `plaintext` ci-dessous.

* Collage du texte, y compris des tableaux, avec la mise en forme lors de la copie à partir de MS Word. La copie et le collage de texte depuis une autre source, telle qu’une page web ou MS Excel ne sont pas pris en charge et conservent uniquement une mise en forme partielle. Configuré à l’aide de `wordhtml` ci-dessous.

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/edit`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Dans le nœud `edit`, créez une propriété à l’aide des informations suivantes :

   * **Nom** `defaultPasteMode`
   * **Type** `String`
   * **Valeur** Un des modes de collage requis : `browser`, `plaintext` ou `wordhtml`.

### Configuration des formats autorisés lors du collage de contenu {#pasteformats}

Le mode Coller comme élément Microsoft Word (`paste-wordhtml`) peut être configuré de manière plus détaillée de manière à pouvoir définir explicitement les styles autorisés pour coller un élément dans AEM à partir d’un autre programme, comme Microsoft Word.

Par exemple, s’il n’est possible de coller que des formats gras et des listes dans AEM, vous pouvez écarter les autres formats en les filtrant. Il s’agit du filtrage du collage configurable, qui peut être effectué pour les deux types de filtrage :

* [Texte](#pastemodes)
* [Liens](#linkstyles)

Pour les liens, vous pouvez également définir les protocoles acceptés automatiquement.

Pour configurer les formats autorisés afin de coller du texte dans AEM à partir d’un autre programme :

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/edit`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Créez un nœud sous le nœud `edit` destiné à contenir les règles de collage HTML :

   * **Nom** `htmlPasteRules`
   * **Type** `nt:unstructured`

1. Créez un nœud sous `htmlPasteRules`, destiné à contenir les détails des formats de base autorisés :

   * **Nom** `allowBasics`
   * **Type** `nt:unstructured`

1. Pour contrôler les différents formats admis, créez une ou plusieurs des propriétés ci-dessous sur le nœud `allowBasics` :

   * **Nom** `bold`
   * **Nom** `italic`
   * **Nom** `underline`
   * **Nom** `anchor` (pour les liens et les ancres nommées)
   * **Nom** `image`

   Toutes les propriétés sont de **type** `Boolean`. Ainsi, dans la **valeur** appropriée, vous pouvez cocher ou désélectionner la case pour activer/désactiver les fonctionnalités.

   >[!NOTE]
   >
   >Si le format n’est pas défini explicitement, la valeur par défaut true est utilisée et le format est admis.

1. D’autres formats peuvent également être définis à l’aide de différentes propriétés ou de différents nœuds, également appliqués au nœud `htmlPasteRules` :

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>allowBlockTags</td>
   <td>Chaîne[]</td>
   <td><p>Définit la liste des balises block autorisées.</p> <p>Voici quelques balises block possibles :</p>
    <ul>
     <li>Titres (h1, h2, h3)</li>
     <li>Paragraphes (p)</li>
     <li>Listes (ol, ul)</li>
     <li>Tableaux (table)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>fallbackBlockTag</td>
   <td>Chaîne</td>
   <td><p>Définit la balise block utilisée pour tout bloc contenant une balise block ne figurant pas dans allowBlockTags.</p> <p> p est suffisant dans la plupart des cas.</p> </td>
  </tr>
  <tr>
   <td>table</td>
   <td>nt:unstructured</td>
   <td><p>Définit le comportement lors du collage de tableaux.<br /> </p> <p>Ce nœud doit comporter la propriété <code>allow</code> (de type <code>Boolean</code>) pour définir s’il est autorisé de coller des tableaux.</p> <p>Si <code>allow</code> est défini sur <code>false</code>, vous devez spécifier la propriété <code>ignoreMode</code> (de type <code> String</code>) pour définir comment le contenu du tableau collé est géré. Les valeurs valides pour <code>ignoreMode</code> sont les suivantes :</p>
    <ul>
     <li><code>remove</code>: supprime le contenu du tableau.</li>
     <li><code>paragraph</code>: transforme les cellules de tableau en paragraphes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>list</td>
   <td>nt:unstructured</td>
   <td><p>Définit le comportement lors du collage de listes.<br /> </p> <p>Doit comporter la propriété <code>allow</code> (de type <code>Boolean</code>) pour définir s’il est autorisé de coller des listes.</p> <p>Si <code>allow</code> est défini sur <code>false</code>, vous devez spécifier la propriété <code>ignoreMode</code> (de type <code>String</code>) pour définir comment gérer le contenu d’une liste collée. Les valeurs valides pour <code>ignoreMode</code> sont les suivantes :</p>
    <ul>
     <li><code>remove</code>: supprime le contenu de la liste.</li>
     <li><code>paragraph</code>: transforme les éléments de la liste en paragraphes.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Exemple de structure `htmlPasteRules` valide :

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Enregistrez toutes les modifications.

## Configuration des styles de texte {#textstyles}

Les auteurs peuvent appliquer des styles pour modifier l’apparence d’une portion de texte. Les styles reposent sur les classes CSS que vous prédéfinissez dans votre feuille de style CSS. Le contenu stylisé est inclus dans les balises `span` à l’aide de l’attribut `class` pour faire référence à la classe CSS. Par exemple :

`<span class=monospaced>Monospaced Text Here</span>`

Lorsque le module externe Styles est activé pour la première fois, aucun style n’est disponible par défaut. La liste contextuelle est vide. Pour fournir des styles aux auteurs, procédez comme suit :

* Activez le sélecteur de liste déroulante Style.
* Spécifiez l’emplacement de la ou des feuilles de style.
* Spécifiez les différents styles qui peuvent être sélectionnés dans la liste déroulante Style.

Pour les configurations ultérieures (par exemple, afin d’ajouter davantage de styles), suivez les instructions pour faire référence à une nouvelle feuille de style et spécifier les styles supplémentaires.

>[!NOTE]
>
>Des styles peuvent également être définis pour [des tableaux ou des cellules de tableau](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Ces configurations nécessitent des procédures distinctes.

### Activation de la liste du sélecteur de liste déroulante Style {#styleselectorlist}

Cette opération et effectuée en activant le module externe Styles.

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/styles`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Créez la propriété `features` sur le nœud `styles` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*` (astérisque)

1. Enregistrez toutes les modifications.

>[!NOTE]
>
>Une fois que le module externe Styles est activé, la liste déroulante Style s’affiche dans la boîte de dialogue de modification. Cependant, la liste est vide lorsqu’aucun style n’est configuré.

### Spécification de l’emplacement de la feuille de style {#locationofstylesheet}

Ensuite, spécifiez l’emplacement de la ou des feuilles de style à référencer :

1. Accédez au nœud racine de votre composant Texte, par exemple. `/apps/<myProject>/components/text`
1. Ajoutez la propriété `externalStyleSheets` au nœud parent de `<rtePlugins-node>` :

   * **Nom** `externalStyleSheets`
   * **Type** `String[]` (multichaîne ; cliquez sur **Multi** dans CRXDE)
   * **Valeur(s)** Chemin d’accès et nom de fichier de chaque feuille de style à inclure. Utilisez les chemins de référentiel.

   >[!NOTE]
   >
   >Vous pouvez ajouter des références à d’autres feuilles de style ultérieurement.

1. Enregistrez toutes les modifications.

>[!NOTE]
>
>Lors de l’utilisation de l’éditeur de texte enrichi dans une boîte de dialogue (IU classique), vous pouvez spécifier des feuilles de style optimisées pour la modification de texte enrichi. En raison de restrictions techniques, le contexte CSS est perdu dans l’éditeur. Vous devrez peut-être émuler ce contexte afin d’améliorer l’expérience WYSIWYG.
>
>L’éditeur de texte enrichi utilise un élément DOM de conteneur avec un ID de `CQrte`, qui peut être utilisé afin de fournir différents styles pour l’affichage et la modification :
>
>
```
>#CQ td {
> // defines the style for viewing
> }
>```
>
>
```
>#CQrte td {
> // defines the style for editing
> }
>```

### Spécification des styles disponibles dans la liste contextuelle {#stylesindropdown}

1. Dans la définition du composant, accédez au nœud `<rtePlugins-node>/styles` tel que créé dans [Activation du sélecteur de liste déroulante Style](#styleselectorlist).
1. Sous le nœud `styles`, créez un nœud (également appelé `styles`) destiné à contenir la liste mise à disposition :

   * **Nom** `styles`
   * **Type** `cq:WidgetCollection`

1. Créez un nœud sous le nœud `styles` pour représenter un style individuel :

   * **Nom**, vous pouvez spécifier le nom, mais il doit être adapté au style
   * **Type** `nt:unstructured`

1. Ajoutez la propriété `cssName` à ce nœud pour référencer la classe CSS :

   * **Nom** `cssName`
   * **Type** `String`
   * **Valeur** Nom de la classe CSS (non précédé d’un point « . » ; par exemple, `cssClass` au lieu de `.cssClass`)

1. Ajoutez la propriété `text` au même nœud. Elle définit le texte affiché dans la boîte de dialogue de sélection :

   * **Nom** `text`
   * **Type** `String`
   * **Valeur** Description du style ; apparaît dans la boîte de dialogue de sélection de la liste déroulante Style.

1. Enregistrez les modifications.

   Répétez les étapes ci-dessus pour chaque style requis.

### Configuration de l’éditeur de texte enrichi pour des coupures de mots optimales en japonais  {#jpwordwrap}

Les auteurs qui utilisent AEM pour créer du contenu en japonais peuvent appliquer un style aux caractères afin d’éviter un saut de ligne lorsqu’il n’est pas nécessaire. Les auteurs peuvent ainsi couper les phrases où ils le souhaitent. Le style de cette fonctionnalité repose sur la classe CSS prédéfinie dans la feuille de style CSS.

>[!NOTE]
>
>Cette fonction nécessite au moins AEM 6.5 Service Pack 1.

Pour créer le style que les auteurs peuvent appliquer au texte japonais, procédez comme suit :

1. Créez un nœud sous le nœud styles. Consultez [spécification d’un nouveau style](#stylesindropdown).
   * Nom (name) : `jpn-word-wrap`
   * Type : `nt:unstructure

1. Ajoutez la propriété `cssName` au nœud pour référencer la classe CSS. Ce nom de classe est un nom réservé pour la fonction de retour automatique à la ligne du japonais.
   * Nom : `cssName`
   * Type : `String`
   * Valeur : `jpn-word-wrap` (sans préfixe `.`)

1. Ajoutez la propriété text au même nœud. La valeur est le nom du style que les auteurs voient lors de la sélection du style.
   * Nom : `text`
*Type : 
`String`
   * Valeur : `Japanese word-wrap`

1. Créez une feuille de style et spécifiez son chemin d’accès. Consultez [spécification de l’emplacement de la feuille de style](#locationofstylesheet). Ajoutez le contenu suivant à la feuille de style. Modifiez la couleur d’arrière-plan selon vos besoins.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Feuille de style pour rendre la fonction de retour automatique à la ligne du japonais disponible pour les auteurs](assets/rte_jpwordwrap_stylesheet.jpg)

## Configuration des formats de paragraphe {#paraformats}

Tout texte saisi dans l’éditeur de texte enrichi est placé dans une balise block dont la valeur par défaut est `<p>`. En activant le module externe `paraformat`, vous spécifiez d’autres balises block, qui peuvent être affectées à des paragraphes, à l’aide d’une liste déroulante de sélection. Les formats de paragraphe déterminent le type de paragraphe en affectant la balise block appropriée. L’auteur peut les sélectionner et les affecter à l’aide du sélecteur Format. Les balises block comprennent, par exemple, le paragraphe standard &lt;p> et les titres standard &lt;h1>, &lt;h2> et ainsi de suite.

>[!CAUTION]
>
>Ce module externe n’est pas adapté au contenu présentant une structure complexe, tel que les listes et les tableaux.

>[!NOTE]
>
>Si une balise block, par exemple une balise &lt;hr>, ne peut pas être affectée à un paragraphe, ce n’est pas un cas d’utilisation valide pour un module externe paraformat.

Lorsque le module externe Formats des paragraphes est activé pour la première fois, aucun format de paragraphe n’est disponible par défaut. La liste contextuelle est vide. Pour fournir des formats de paragraphes aux auteurs, procédez comme suit :

* Activez la liste du sélecteur de liste déroulante Format.
* Spécifiez les balises block qui peuvent être sélectionnées dans la liste déroulante.

Pour les configurations ultérieures, par exemple, afin d’ajouter davantage de formats, suivez uniquement la partie correspondante des instructions.

### Activation du sélecteur de liste déroulante Format  {#formatselectorlist}

Commencez d’abord par activer le module externe paraformat :

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/paraformat`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Créez la propriété `features` sur le nœud `paraformat` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*` (astérisque)

>[!NOTE]
Si le module externe n’est pas configuré davantage, les formats par défaut suivants sont activés :
* Paragraphe ( `<p>`)
* En-tête 1 ( `<h1>`)
* En-tête 2 ( `<h2>`)
* En-tête 3 ( `<h3>`)



>[!CAUTION]
Lors de la configuration des formats de paragraphe de l’éditeur de texte enrichi, ne supprimez pas la balise de paragraphe &lt;p> comme option de mise en forme. Si la balise `<p>` est supprimée, l’auteur du contenu ne peut pas sélectionner l’option **Formats des paragraphes**, même si d’autres formats sont configurés.

### Spécification des formats de paragraphe disponibles {#paraformatsindropdown}

Les formats de paragraphe peuvent être mis à disposition pour être sélectionnés :

1. Dans la définition du composant, accédez au nœud `<rtePlugins-node>/paraformat`, tel que créé dans [Activation du sélecteur de liste déroulante Format](#styleselectorlist).
1. Sous le nœud `paraformat`, créez un nœud destiné à contenir la liste de formats :

   * **Nom** `formats`
   * **Type** `cq:WidgetCollection`

1. Créez un nœud sous le nœud `formats`, qui contient les détails pour un format spécifique :

   * **Nom**, vous pouvez spécifier le nom, mais il doit être adapté au format (par exemple, myparagraph, myheading1).
   * **Type** `nt:unstructured`

1. Sur ce nœud, ajoutez la propriété pour définir la balise block utilisée :

   * **Nom** `tag`
   * **Type** `String`
   * **Valeur** La balise block pour le format, par exemple : p, h1, h2, etc.

      Vous n’avez pas besoin de saisir les crochets de séparation.

1. Sur le même nœud, ajoutez une autre propriété pour que le texte descriptif s’affiche dans la liste déroulante :

   * **Nom** `description`
   * **Type** `String`
   * **Valeur** Texte descriptif pour ce format, par exemple, paragraphe, titre 1, titre 2, etc. Ce texte s’affiche dans la liste de sélection Format.

1. Enregistrez les modifications.

   Répétez la procédure pour chaque format requis.

>[!CAUTION]
Si vous définissez des formats personnalisés, les formats par défaut (`<p>`, `<h1>`, `<h2>` et `<h3>`) sont supprimés. Recréez le format `<p>`, car il s’agit du format par défaut.

## Configuration des caractères spéciaux {#spchar}

Dans une installation AEM standard, lorsque le module externe `misctools` est activé pour les caractères spéciaux (`specialchars`), une sélection par défaut est disponible immédiatement. Par exemple, les symboles de copyright et de marque.

Vous pouvez configurer l’éditeur de texte enrichi de manière à mettre à disposition votre propre sélection de caractères, en définissant des caractères distincts ou une séquence entière.

>[!CAUTION]
Si vous ajoutez vos propres caractères spéciaux, ils remplacent la sélection par défaut. Si nécessaire, définissez ou redéfinissez ces caractères dans votre sélection.

### Définition d’un caractère unique  {#definesinglechar}

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/misctools`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Créez la propriété `features` sur le nœud `misctools` :

   * **Nom** `features`
   * **Type** `String[]`
   * **Valeur** `specialchars`

          (ou `String / *` si toutes les fonctions sont appliquées pour ce module externe)

1. Sous `misctools`, créez un nœud destiné à contenir les configurations de caractères spéciaux :

   * **Nom** `specialCharsConfig`
   * **Type** `nt:unstructured`

1. Sous `specialCharsConfig`, créez un autre nœud destiné à contenir la liste de caractères :

   * **Nom** `chars`
   * **Type** `nt:unstructured`

1. Sous `chars`, ajoutez un nouveau nœud destiné à contenir une définition de caractère individuel :

   * **Nom** Vous pouvez spécifier le nom, mais il doit refléter le caractère, par exemple, « moitié ».
   * **Type** `nt:unstructured`

1. Ajoutez la propriété suivante à ce nœud :

   * **Nom** `entity`
   * **Type** `String`
   * **Valeur** Représentation HTML du caractère nécessaire, par exemple, `&189;` pour la fraction un demi.

1. Enregistrez les modifications.

Dans CRXDE, une fois la propriété enregistrée, le caractère représenté s’affiche. Voir ci-dessous sous l’exemple du caractère demi. Répétez les étapes ci-dessus pour rendre plus de caractères spéciaux disponibles aux auteurs.

![Dans CRXDE, ajoutez un caractère unique pour qu’il soit disponible dans la barre d’outils d’éditeur de texte enrichi](assets/chlimage_1-106.png " Dans CRXDE, ajoutez un caractère unique pour qu’il soit disponible dans la barre d’outils d’éditeur de texte enrichi")

### Définition d’une série de caractères {#definerangechar}

1. Utilisez les étapes 1 à 3 de la section [Définition d’un caractère unique](#definesinglechar).
1. Sous `chars`, ajoutez un nouveau nœud destiné à contenir la définition de la plage de caractères :

   * **Nom** Vous pouvez spécifier le nom, mais il doit refléter la plage de caractères, par exemple, « crayons ».
   * **Type** `nt:unstructured`

1. Sous ce nœud (nommé en fonction de votre plage de caractères spéciaux), ajoutez les deux propriétés suivantes :

   * **Nom** `rangeStart`

      **Type** `Long`
      **Valeur** Représentation [Unicode](https://unicode.org/) (décimale) du premier caractère de la plage

   * **Nom** `rangeEnd`

      **Type** `Long`
      **Valeur** Représentation [Unicode](https://unicode.org/) (décimale) du dernier caractère de la plage

1. Enregistrez les modifications.

   Par exemple, la définition d’une série de 9998 à 10000 vous permet de bénéficier des caractères suivants.

   ![Définition dans CRXDE d’une série de caractères pour qu’elle soit disponible dans l’éditeur de texte enrichi](assets/chlimage_1-107.png)

   *Figure : Définition dans CRXDE d’une série de caractères pour qu’elle soit disponible dans l’éditeur de texte enrichi*

   ![Les caractères spéciaux disponibles dans l’éditeur de texte enrichi sont affichés pour les auteurs dans une fenêtre contextuelle](assets/rtepencil.png " Les caractères spéciaux disponibles dans l’éditeur de texte enrichi sont affichés pour les auteurs dans une fenêtre contextuelle")

## Configuration des styles de tableau {#tablestyles}

Les styles sont généralement appliqués au texte, mais un jeu de styles distinct peut également être appliqué à un tableau ou à certaines cellules de tableau. Ces styles sont à la disposition des auteurs au niveau de la boîte du sélecteur de style dans la boîte de dialogue de propriétés de la cellule ou du tableau. Les styles sont disponibles lors de la modification d’un tableau dans un composant Texte (ou dérivé), et non dans le composant Tableau standard.

>[!NOTE]
Vous pouvez définir des styles pour les tableaux et les cellules uniquement pour l’IU classique.

>[!NOTE]
La copie et le collage de tableaux dans ou à partir d’un composant d’éditeur de texte enrichi dépendent du navigateur. Ils ne sont pas pris en charge nativement pour tous les navigateurs. Vous pouvez obtenir des résultats variables selon la structure du tableau et le navigateur. Par exemple, lorsque vous copiez et collez un tableau dans un composant d’éditeur de texte enrichi dans Mozilla Firefox dans les IU classique et tactile, la mise en page du tableau n’est pas conservée.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/table`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Créez la propriété `features` sur le nœud `table` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*`

   >[!NOTE]
   Si vous ne souhaitez pas activer toutes les fonctionnalités de tableau, vous pouvez créer la propriété `features`, comme suit :
   * **Type** `String[]`

   * **Valeurs** Un ou deux des éléments ci-dessous, au besoin :
      * `table` pour permettre de modifier les propriétés du tableau, dont les styles.
      * `cellprops` pour permettre de modifier les propriétés des cellules, dont les styles.


1. Définissez l’emplacement des feuilles de style CSS pour y faire référence. Voir [Spécification de l’emplacement d’une feuille de style](#locationofstylesheet), car il s’agit de la même procédure que lorsque vous définissez des [styles de texte](#textstyles). L’emplacement peut être défini si vous avez défini d’autres styles.
1. Sous le nœud `table`, créez les nœuds suivants (au besoin) :

   * Pour définir des styles pour le tableau entier (disponibles sous **Propriétés du tableau**) :

      * **Nom** `tableStyles`
      * **Type** `cq:WidgetCollection`
   * Pour définir des styles pour des cellules individuelles (disponibles sous **Propriétés de la cellule**) :

      * **Nom** `cellStyles`
      * **Type** `cq:WidgetCollection`


1. Créez un nœud (sous le nœud `tableStyles` ou `cellStyles`, selon ce qui est approprié) pour représenter un style individuel :

   * **Nom** Vous pouvez spécifier le nom, mais il doit refléter le style.
   * **Type** `nt:unstructured`

1. Sur ce nœud, créez les propriétés :

   * Pour définir le style CSS à référencer

      * **Nom** `cssName`
      * **Type** `String`
      * **Valeur** Nom de la classe CSS (sans préfixe `.`, par exemple, `cssClass` au lieu de `.cssClass`)
   * Pour définir un texte descriptif à afficher dans le sélecteur de liste déroulante

      * **Nom** `text`
      * **Type** `String`
      * **Valeur** Texte à afficher dans la liste de sélection


1. Enregistrez toutes les modifications.

Répétez les étapes ci-dessus pour chaque style requis.

### Configuration d’en-têtes masqués dans les tableaux pour l’accessibilité  {#hiddenheader}

Dans certains cas, vous pouvez créer des tableaux de données sans texte visuel dans un en-tête de colonne en supposant que l’objectif de l’en-tête est induit par la relation visuelle de la colonne avec d’autres colonnes. Dans ce cas, il est nécessaire d’indiquer un texte masqué à l’intérieur de la cellule d’en-tête pour permettre aux lecteurs d’écran et aux autres dispositifs d’assistance d’aider les utilisateurs, indépendamment de leur validité, à comprendre l’objectif de la colonne.

Pour améliorer l’accessibilité dans de telles situations, l’éditeur de texte enrichi prend en charge les cellules d’en-tête masquées. De plus, il fournit des paramètres de configuration associés aux en-têtes masqués dans les tableaux. Ces paramètres permettent d’appliquer des styles CSS à des en-têtes masqués en mode modification et aperçu. Pour aider les auteurs à identifier les en-têtes masqués en mode modification, incluez les paramètres ci-dessous dans votre code :

* `hiddenHeaderEditingCSS` : spécifie le nom de la classe CSS appliquée à la cellule hidden-header lorsque l’éditeur de texte enrichi est modifié.
* `hiddenHeaderEditingStyle` : spécifie une chaîne Style appliquée à la cellule hidden-header lorsque l’éditeur de texte enrichi est modifié.

Si vous spécifiez la chaîne CSS et la chaîne Style dans le code, la classe CSS prévaut sur la chaîne Style et peut remplacer les modifications apportées à la configuration en raison de la chaîne Style.

Pour aider les créateurs à appliquer la feuille de style CSS à des en-têtes masqués en mode aperçu, vous pouvez inclure les paramètres ci-dessous dans votre code :

* `hiddenHeaderClassName` : spécifie le nom de la classe CSS appliquée à la cellule d’en-tête masqué en mode aperçu.
* `hiddenHeaderStyle` : spécifie une chaîne Style appliquée à la cellule d’en-tête masqué en mode aperçu.

Si vous spécifiez la chaîne CSS et la chaîne Style dans le code, la classe CSS prévaut sur la chaîne Style et peut remplacer les modifications apportées à la configuration en raison de la chaîne Style.

## Ajout de dictionnaires au vérificateur orthographique  {#adddict}

Lorsque le module externe Contrôle d’orthographe est activé, l’éditeur de texte enrichi utilise les dictionnaires de chaque langue appropriée. Ils sont sélectionnés en fonction de la langue du site web, d’après la propriété language de la sous-arborescence ou à partir de la langue de l’adresse URL, par exemple. Pour la branche `/en/`, la vérification est effectuée pour l’anglais ; pour la branche `/de/`, pour l’allemand.

>[!NOTE]
The message `Spell checking failed` is seen if a check is attempted for a language that is not installed. Les dictionnaires standard sont situés à l’emplacement `/libs/cq/spellchecker/dictionaries`, avec les fichiers Lisez-moi correspondants. Ne modifiez pas les fichiers.

Une installation AEM standard inclut les dictionnaires pour l&#39;anglais américain (`en_us`) et l&#39;anglais britannique (`en_gb`). Pour ajouter d’autres dictionnaires, procédez comme suit.

1. Accédez à la page [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Effectuez l’une des opérations suivantes pour trouver un dictionnaire de votre choix de langue :

   * Recherchez le dictionnaire de votre choix de langue. Sur la page du dictionnaire, recherchez le lien vers la source d’origine ou la page Web de l’auteur. Localisez les fichiers de dictionnaire pour v2.x sur une telle page.
   * Recherchez des fichiers de dictionnaire v2.x à l’adresse [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Téléchargez l&#39;archive avec les définitions orthographiques. Extrayez le contenu de l’archive dans votre système de fichiers.

   >[!CAUTION]
   Seuls les dictionnaires au format `MySpell` pour OpenOffice.org v2.0.1 ou version inférieure, sont pris en charge. Comme les dictionnaires sont désormais des fichiers archives, il est recommandé de les vérifier après les avoir téléchargés.

1. Recherchez les fichiers .aff et.dic. Conservez le nom en lettres minuscules. Par exemple, `de_de.aff` et `de_de.dic`.
1. Chargez les fichiers .aff et.dic dans le référentiel à l’emplacement `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
Le vérificateur orthographique de l’éditeur de texte enrichi est disponible sur demande. Il n’est pas exécuté automatiquement lorsque vous commencez à saisir du texte. To run the spell checker, click [!UICONTROL Spellchecker] from the toolbar. RTE vérifie l&#39;orthographe des mots et met en évidence les mots mal orthographiés.
Si vous incorporez une modification suggérée par le vérificateur orthographique, l’état du texte change et les mots mal orthographiés ne sont plus surlignés. Pour exécuter le vérificateur orthographique, appuyez/cliquez de nouveau sur le bouton Vérificateur orthographique.

## Configuration de la taille de l’historique pour les actions d’annulation et de rétablissement {#undohistory}

L’éditeur de texte enrichi permet aux auteurs d’annuler ou de rétablir quelques-unes des dernières modifications. Par défaut, 50 modifications sont stockées dans l’historique. Vous pouvez configurer cette valeur, au besoin.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/undo`. Créez ces nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Sur le nœud `undo`, créez la propriété :

   * **Nom** `maxUndoSteps`
   * **Type** `Long`
   * **Valeur** Nombre d’étapes annulées à enregistrer dans l’historique. La valeur par défaut est de 50. Utilisez `0` pour désactiver complètement l’annulation/le rétablissement.

1. Enregistrez les modifications.

## Configuration de la taille de tabulation  {#tabsize}

Lorsque le caractère de tabulation est activé dans un texte, un nombre prédéfini d’espaces est inséré. Par défaut, il s’agit de trois espaces insécables et d’un espace.

Pour définir la taille de la tabulation :

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/keys`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Sur le nœud `keys`, créez la propriété :

   * **Nom** `tabSize`
   * **Type** `String`
   * **Valeur** Nombre d’espaces à utiliser pour le tabulateur.

1. Enregistrez les modifications.

## Définition de la marge de retrait  {#indentmargin}

Lorsque la mise en retrait est activée (par défaut), vous pouvez définir la taille du retrait :

>[!NOTE]
Cette taille de retrait n’est appliquée qu’aux paragraphes (blocs) de texte. Elle n’affecte pas la mise en retrait des listes.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/lists`. Créez ces nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Sur le nœud `lists`, créez le paramètre `identSize` :

   * **Nom** : `identSize`
   * **Type** : `Long`
   * **Valeur** Nombre de pixels nécessaires pour la marge en retrait.

## Configuration de la hauteur de l’espace modifiable {#editablespace}

>[!NOTE]
Cela ne s’applique que lors de l’utilisation de l’éditeur de texte enrichi dans une boîte de dialogue (et non lors de la modification statique dans l’interface utilisateur classique).

Vous pouvez définir la hauteur de l’espace modifiable affiché dans la boîte de dialogue du composant :

1. Sur le nœud `../items/text` de la définition de boîte de dialogue pour le composant, créez une propriété :

   * **Nom** `height`
   * **Type** `Long`
   * **Valeur** Hauteur du canevas de publication, exprimée en pixels.

   >[!NOTE]
   Cette opération ne modifie pas la hauteur de la fenêtre de la boîte de dialogue.

1. Enregistrez les modifications.

## Configuration des styles et des protocoles pour les liens {#linkstyles}

Lorsque vous ajoutez des liens dans AEM, vous pouvez définir les éléments suivants :

* Styles CSS à utiliser
* Protocoles admis automatiquement

Pour configurer la façon dont les liens sont ajoutés dans AEM à partir d’un autre programme, définissez des règles HTML.

1. À l’aide de CRXDE Lite, cherchez le composant Texte pour votre projet.
1. Créez un nœud au même niveau que `<rtePlugins-node>`, c’est-à-dire créez le nœud sous le nœud parent de `<rtePlugins-node>` :

   * **Nom** `htmlRules`
   * **Type** `nt:unstructured`

   >[!NOTE]
   Le nœud `../items/text` possède la propriété :
   * **Nom** `xtype`
   * **Type** `String`
   * **Valeur** `richtext`

   L’emplacement du nœud `../items/text` peut varier en fonction de la structure de votre boîte de dialogue. Voici deux exemples :
   * `/apps/myProject>/components/text/dialog/items/text`
   * `/apps/<myProject>/components/text/dialog/items/panel/items/text`


1. Sous `htmlRules`, créez un nœud.

   * **Nom** `links`
   * **Type** `nt:unstructured`

1. Sous le nœud `links`, définissez les propriétés, au besoin :

   * Style CSS pour les liens internes :

      * **Nom** `cssInternal`
      * **Type** `String`
      * **Valeur** Nom de la classe CSS (non précédé d’un point « . »  ; par exemple, `cssClass` au lieu de `.cssClass`)
   * Style CSS pour les liens externes

      * **Nom** `cssExternal`
      * **Type** `String`
      * **Valeur** Nom de la classe CSS (non précédé d’un point « . »  ; par exemple, `cssClass` au lieu de `.cssClass`)
   * Tableau de **protocoles** valides. Les protocoles pris en charge sont `http://`, `https://`, `file://`et `mailto:`.

      * **Nom** `protocols`
      * **Type** `String[]`
      * **Valeurs** Un ou plusieurs protocoles
   * **defaultProtocol** (propriété de type **String**) : protocole à utiliser si l’utilisateur n’en a pas spécifié un explicitement.

      * **Nom** `defaultProtocol`
      * **Type** `String`
      * **Valeurs** Un ou plusieurs protocoles par défaut
   * Définition de la gestion de l’attribut cible d’un lien. Créez un nœud :

      * **Nom** `targetConfig`
      * **Type** `nt:unstructured`

      Sur le nœud `targetConfig` : définissez les propriétés nécessaires :

      * Spécifiez le mode cible :

         * **Nom** `mode`
         * **Type** `String`)
         * **Valeurs** :

            * `auto` : signifie qu’une cible automatique est choisie

               (spécifié par la propriété `targetExternal` pour les liens externes ou `targetInternal` pour les liens internes).

            * `manual` : non applicable dans ce contexte
            * `blank` : non applicable dans ce contexte
      * Cible des liens internes :

         * **Nom** `targetInternal`
         * **Type** `String`
         * **Valeur** Cible des liens internes (utilisé uniquement lorsque le mode est `auto`)
      * Cible des liens externes :

         * **Nom** `targetExternal`
         * **Type** `String`
         * **Valeur** Cible des liens externes (utilisé uniquement lorsque le mode est `auto`).








1. Enregistrez toutes les modifications.
