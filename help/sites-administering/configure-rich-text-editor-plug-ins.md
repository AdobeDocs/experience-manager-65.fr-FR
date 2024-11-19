---
title: Configuration des modules externes d’éditeur de texte enrichi
description: Apprenez à configurer les modules externes d’éditeur de texte enrichi d’Adobe Experience Manager afin d’activer différentes fonctionnalités.
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: f64a1014dfd1155bcf815e75a27102244ef6c6de
workflow-type: ht
source-wordcount: '4391'
ht-degree: 100%

---


# Configuration des modules externes d’éditeur de texte enrichi {#configure-the-rich-text-editor-plug-ins}

Les fonctionnalités d’éditeur de texte enrichi sont rendues disponibles par l’intermédiaire d’une série de modules externes, chacun avec sa propriété features. Vous pouvez configurer la propriété features pour activer ou désactiver une ou plusieurs fonctionnalités de l’éditeur de texte enrichi. Cet article décrit comment configurer spécifiquement les modules externes d’éditeur de texte enrichi.

Pour plus d’informations sur les autres configurations d’éditeur de texte enrichi, consultez [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Lorsque vous utilisez CRXDE Lite, il est conseillé d’enregistrer régulièrement les modifications à l’aide de l’option [!UICONTROL Enregistrer tout].

## Activation d’un module externe et configuration de la propriété features {#activateplugin}

Pour activer un module externe, procédez comme suit : Certaines étapes ne sont nécessaires que lorsque vous configurez un module externe pour la première fois, car les nœuds correspondants n’existent pas.

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
   * Ils possèdent tous deux les propriétés suivantes :

      * **Nom** `name`
      * **Type** `String`
      * **Valeur** `./text`

1. Selon l’interface que vous configurez, créez un nœud `<rtePlugins-node>` s’il n’existe pas :

   * **Nom** `rtePlugins`
   * **Type** `nt:unstructured`

1. Voici comment créer un nœud pour chaque module externe à activer :

   * **Type** `nt:unstructured`
   * **Nom** ID du module externe requis

Après activation d’un module externe, suivez ces instructions pour configurer la propriété `features`.

| | Activer toutes les fonctions | Activer des fonctions spécifiques | Désactiver toutes les fonctions |
|---|---|---|---|
| Nom | features | features | features |
| Type | Chaîne | Chaîne[] (multichaîne ; définissez le type sur chaîne et cliquez sur Multi dans CRXDE Lite) | Chaîne |
| Valeur | `*` (astérisque) | définie sur une ou plusieurs valeurs de fonctions | - |

## Compréhension du module externe findreplace {#findreplace}

Le module externe `findreplace` n’a pas besoin de configuration. Il est prêt à l’emploi.

Lors de l’utilisation de la fonctionnalité de remplacement, la chaîne à remplacer doit être saisie en même temps que la chaîne de recherche. Cependant, vous pouvez toujours cliquer sur Rechercher pour rechercher la chaîne avant de la remplacer. Si la chaîne de remplacement est saisie après avoir cliqué sur Rechercher, la recherche est réinitialisée au début du texte.

La boîte de dialogue de recherche et de remplacement devient transparente lorsque l’utilisateur clique sur Rechercher et devient opaque lorsque l’utilisateur clique sur Remplacer. Cela permet au créateur ou à la créatrice de vérifier le texte qui sera remplacé. Si les utilisateurs et utilisatrices cliquent sur Remplacer tout, la boîte de dialogue se ferme et affiche le nombre de remplacements effectués.

## Configuration des modes de collage {#paste-modes}

Lorsqu’ils utilisent l’éditeur de texte enrichi, les créateurs et créatrices peuvent coller du contenu dans l’un des trois modes suivants :

* **Mode Navigateur** : collage de texte avec la mise en œuvre de collage par défaut du navigateur. Il ne s’agit pas d’une méthode recommandée, car elle peut introduire des balises indésirables.

* **Mode Texte brut** : collage du contenu du Presse-papiers en tant que texte brut. Cela supprime tous les éléments de style et de mise en forme du contenu copié avant insertion dans le composant [!DNL Experience Manager].

* **Mode MS® Word** : collage du texte, y compris de tableaux, avec la mise en forme lors de la copie à partir de MS® Word. La copie et le collage de texte à partir d’une autre source, telle qu’une page web ou MS® Excel ne sont pas pris en charge et conservent uniquement une mise en forme partielle.

### Configuration des options de collage disponibles sur la barre d’outils de l’éditeur de texte enrichi   {#configure-paste-options-available-on-the-rte-toolbar}

Les trois icônes ci-dessous peuvent être mises à la disposition des auteurs dans la barre d’outils de l’éditeur de texte enrichi :

* **[!UICONTROL Coller (Ctrl + V)]** : peut être préconfigurée pour correspondre à l’un des trois modes de collage ci-dessus.

* **[!UICONTROL Coller en tant que texte]** : fournit la fonctionnalité du mode Texte brut.

* **[!UICONTROL Coller à partir de Word]** : fournit la fonctionnalité du mode MS® Word.

Pour configurer l’éditeur de texte enrichi afin qu’il affiche les icônes requises, procédez comme suit.

1. Accédez à votre composant, par exemple `/apps/<myProject>/components/text`.
1. Accédez au nœud `rtePlugins/edit`. Voir [Activation d’un module externe](#activateplugin) si le nœud n’existe pas.
1. Créez la propriété `features` sur le nœud `edit` et ajoutez une ou plusieurs des fonctions. Enregistrez toutes les modifications.

### Configuration du comportement de l’icône et du raccourci Coller (Ctrl + V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Vous pouvez préconfigurer le comportement de l’icône **[!UICONTROL Coller (Ctrl+V)]** en vous aidant des étapes suivantes. Cette configuration définit également le comportement du raccourci clavier Ctrl+V que les créateurs et créatrices utilisent pour coller du contenu.

La configuration permet d’utiliser les trois types de cas suivants :

* Collage de texte avec la mise en œuvre de collage par défaut du navigateur. Il ne s’agit pas d’une méthode recommandée, car elle peut introduire des balises indésirables. Configuré à l’aide de `browser` ci-dessous.

* Collage du contenu du Presse-papiers en tant que texte brut. Cela supprime tous les éléments de style et de mise en forme du contenu copié avant insertion dans le composant AEM. Configuré à l’aide de `plaintext` ci-dessous.

* Collage du texte, y compris de tableaux, avec la mise en forme lors de la copie à partir de MS® Word. La copie et le collage de texte à partir d’une autre source, telle qu’une page web ou MS® Excel ne sont pas pris en charge et conservent uniquement une mise en forme partielle. Configuré à l’aide de `wordhtml` ci-dessous.

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/edit`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Dans le nœud `edit`, créez une propriété à l’aide des informations suivantes :

   * **Nom** `defaultPasteMode`
   * **Type** `String`
   * **Valeur** Un des modes de collage requis : `browser`, `plaintext` ou `wordhtml`.

### Configuration des formats autorisés lors du collage de contenu {#pasteformats}

Vous pouvez configurer le mode Coller comme élément Microsoft Word (`paste-wordhtml`) de manière plus détaillée pour définir explicitement les styles autorisés pour coller un élément dans AEM à partir d’un autre programme, comme Microsoft® Word.

Par exemple, s’il n’est possible de coller que des formats gras et des listes dans AEM, vous pouvez écarter les autres formats en les filtrant. Il s’agit du filtrage du collage configurable, qui peut être effectué pour les deux types de filtrage :

* [Texte](#paste-modes)
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

1. D’autres formats peuvent également être définis à l’aide de différentes propriétés ou de différents nœuds, également appliqués au nœud `htmlPasteRules`. Enregistrez toutes les modifications.

Vous pouvez utiliser les propriétés suivantes pour `htmlPasteRules`.

| Propriété | Type | Description |
|---|---|---|
| `allowBlockTags` | Chaîne | Définit la liste des balises block autorisées. Voici quelques balises block possibles : <ul> <li>titres (h1, h2, h3)</li> <li>paragraphes (p)</li> <li>listes (ol, ul)</li> <li>tableaux (table)</li> </ul> |
| `fallbackBlockTag` | Chaîne | Définit la balise block utilisée pour tout bloc contenant une balise block ne figurant pas dans `allowBlockTags`. En général, `p` suffit. |
| table | nt:unstructured | Définit le comportement lors du collage de tableaux. Ce nœud doit comporter la propriété `allow` (de type Boolean) pour définir s’il est autorisé de coller des tableaux. Si « allow » est défini sur `false`, vous devez spécifier la propriété `ignoreMode` (de type String) pour définir comment le contenu du tableau collé est géré. Les valeurs valides pour `ignoreMode` sont les suivantes : <ul> <li>`remove` : supprime le contenu du tableau.</li> <li>`paragraph` : transforme les cellules de tableau en paragraphes.</li> </ul> |
| list | nt:unstructured | Définit le comportement lors du collage de listes. Doit comporter la propriété `allow` (de type Boolean) pour définir s’il est autorisé de coller des listes. Si `allow` est défini sur `false`, vous devez spécifier la propriété `ignoreMode` (de type String) pour définir comment gérer le contenu d’une liste collée. Les valeurs valides pour `ignoreMode` sont les suivantes : <ul><li> `remove` : supprime le contenu de la liste.</li> <li>`paragraph` : transforme les éléments de la liste en paragraphes.</li> </ul> |

Voici un exemple de structure `htmlPasteRules` valide.

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

## Configuration des styles de texte {#textstyles}

Les créateurs et créatrices peuvent appliquer des styles pour modifier l’apparence d’une portion de texte. Les styles sont basés sur les classes CSS que vous avez prédéfinies dans votre feuille de style CSS. Le contenu stylisé est inclus dans les balises `span` à l’aide de l’attribut `class` pour faire référence à la classe CSS. Par exemple, `<span class=monospaced>Monospaced Text Here</span>`.

Lorsque le module externe Styles est activé pour la première fois, aucun style par défaut n’est disponible. La liste contextuelle est vide. Pour fournir des styles aux créateurs et créatrices, procédez comme suit :

* Activez le sélecteur de liste déroulante Style.
* Spécifiez l’emplacement des feuilles de style.
* Spécifiez les différents styles qui peuvent être sélectionnés dans la liste déroulante Style.

Pour les configurations ultérieures, suivez les instructions pour faire référence à une nouvelle feuille de style et spécifier les styles supplémentaires.

>[!NOTE]
>
>Vous pouvez définir des styles pour les [tableaux ou les cellules de tableau](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Ces configurations nécessitent des procédures distinctes.

### Activation de la liste du sélecteur de liste déroulante Style {#styleselectorlist}

Cette opération est effectuée en activant le module externe Style.

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/styles`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
1. Créez la propriété `features` sur le nœud `styles` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*` (astérisque)

1. Enregistrez toutes les modifications.

>[!NOTE]
>
>Une fois que le module externe Styles est activé, la liste déroulante Style s’affiche dans la boîte de dialogue de modification. Cependant, la liste est vide lorsqu’aucun style n’est configuré.

### Spécification de l’emplacement de la feuille de style {#locationofstylesheet}

Ensuite, spécifiez les emplacements des feuilles de style à référencer :

1. Accédez au nœud racine de votre composant Texte, par exemple `/apps/<myProject>/components/text`.
1. Ajoutez la propriété `externalStyleSheets` au nœud parent de `<rtePlugins-node>` :

   * **Nom** `externalStyleSheets`
   * **Type** `String[]` (multichaîne ; cliquez sur **Multi** dans CRXDE)
   * **Valeurs** Chemin et nom de fichier de chaque feuille de style à inclure. Utilisez les chemins d’accès au référentiel.

   >[!NOTE]
   >
   >Vous pouvez ajouter des références à d’autres feuilles de style ultérieurement.

1. Enregistrez toutes les modifications.

>[!NOTE]
>
>Lors de l’utilisation de l’éditeur de texte enrichi dans une boîte de dialogue (IU classique), vous pouvez spécifier des feuilles de style optimisées pour la modification de texte enrichi. En raison de restrictions techniques, le contexte CSS est perdu dans l’éditeur. Vous devrez peut-être émuler ce contexte afin d’améliorer l’expérience WYSIWYG.
>
>L’éditeur de texte enrichi utilise un élément DOM de conteneur avec un ID de `CQrte`, qui peut être utilisé afin de fournir différents styles pour l’affichage et la modification :
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### Spécification des styles disponibles dans la liste pop-up {#stylesindropdown}

1. Dans la définition du composant, accédez au nœud `<rtePlugins-node>/styles` tel que créé dans [Activation du sélecteur de liste déroulante Style](#styleselectorlist).
1. Sous le nœud `styles`, créez un nœud (également appelé `styles`) destiné à contenir la liste mise à disposition :

   * **Nom** `styles`
   * **Type** `cq:WidgetCollection`

1. Créez un nœud sous le nœud `styles` pour représenter un style individuel :

   * **Nom**, vous pouvez spécifier le nom, mais il doit être adapté au style
   * **Type** `nt:unstructured`

1. Ajoutez la propriété `cssName` à ce nœud pour pouvoir référencer la classe CSS :

   * **Nom** `cssName`
   * **Type** `String`
   * **Valeur** Nom de la classe CSS (non précédé d’un point « . » ; par exemple, `cssClass` au lieu de `.cssClass`)

1. Ajoutez la propriété `text` au même nœud. Elle définit le texte affiché dans la boîte de dialogue de sélection :

   * **Nom** `text`
   * **Type** `String`
   * **Valeur**. Description du style, s’affiche dans la zone de sélection de la liste déroulante Style.

1. Enregistrez les modifications.

   Répétez les étapes ci-dessus pour chaque style requis.

### Configuration de l’éditeur de texte enrichi pour des coupures de mots optimales en japonais {#jpwordwrap}

Les auteurs et autrices qui utilisent AEM pour créer du contenu en japonais peuvent appliquer un style aux caractères afin d’éviter un saut de ligne lorsqu’il n’est pas nécessaire. Les auteurs peuvent ainsi couper les phrases où ils le souhaitent. Le style de cette fonctionnalité est basé sur la classe CSS prédéfinie dans la feuille de style CSS.

>[!NOTE]
>
>Cette fonctionnalité nécessite au moins le pack de services 1 d’AEM 6.5.

Pour créer le style que les auteurs peuvent appliquer au texte japonais, procédez comme suit :

1. Créez un nœud sous le nœud styles. Voir [Spécification d’un nouveau style](#stylesindropdown).
   * Nom (name) : `jpn-word-wrap`
   * Type : `nt:unstructure`

1. Ajoutez la propriété `cssName` au nœud pour pouvoir référencer la classe CSS. Ce nom de classe est un nom réservé pour la fonction de retour automatique à la ligne du japonais.
   * Nom : `cssName`
   * Type : `String`
   * Valeur : `jpn-word-wrap` (sans préfixe `.`)

1. Ajoutez la propriété text au même nœud. La valeur est le nom du style que l’auteur ou l’autrice voit lors de la sélection du style.
   * Nom : `text`
*Type : `String`
   * Valeur : `Japanese word-wrap`

1. Créez une feuille de style et spécifiez son chemin d’accès. Consultez [Spécifier l’emplacement de la feuille de style](#locationofstylesheet). Ajoutez le contenu suivant à la feuille de style. Modifiez la couleur d’arrière-plan selon vos besoins.

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

Tout texte saisi dans l’éditeur de texte enrichi est placé dans une balise block dont la valeur par défaut est `<p>`. En activant le module externe `paraformat`, vous spécifiez d’autres balises block, qui peuvent être affectées à des paragraphes, à l’aide d’une liste déroulante de sélection. Les formats de paragraphe déterminent le type de paragraphe en affectant la balise block appropriée. L’auteur ou l’autrice peut les sélectionner et les attribuer à l’aide du sélecteur Format. Les exemples de balises block incluent, entre autres, le paragraphe standard &lt;p> et les en-têtes &lt;h1>, &lt;h2>, etc.

>[!CAUTION]
>
>Ce plug-in ne convient pas au contenu avec des structures complexes, telles que des listes ou des tableaux.

>[!NOTE]
>
>Si une balise block (par exemple, une balise &lt;hr>) ne peut pas être affectée à un paragraphe, ce n’est pas un cas d’utilisation valide pour un plug-in paraformat.

Lorsque le plug-in Formats de paragraphe est activé pour la première fois, aucun format de paragraphe par défaut n’est disponible. La liste contextuelle est vide. Pour fournir des formats de paragraphes aux auteurs et autrices, procédez comme suit :

* Activez la liste du sélecteur de liste déroulante Format.
* Spécifiez les balises block qui peuvent être sélectionnées comme formats de paragraphes dans la liste déroulante.

Pour les configurations ou reconfigurations ultérieures, par exemple, afin d’ajouter davantage de formats, suivez uniquement la partie correspondante des instructions.

### Activation du sélecteur de liste déroulante Format {#formatselectorlist}

Commencez d’abord par activer le module externe paraformat :

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/paraformat`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
1. Créez la propriété `features` sur le nœud `paraformat` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*` (astérisque)

>[!NOTE]
>
Si le module externe n’est pas configuré davantage, les formats par défaut suivants sont activés :
>
* Paragraphe ( `<p>`)
* En-tête 1 ( `<h1>`)
* En-tête 2 ( `<h2>`)
* En-tête 3 ( `<h3>`)
>

>[!CAUTION]
>
Lors de la configuration des formats de paragraphe de l’éditeur de texte enrichi, ne supprimez pas la balise de paragraphe &lt;p> comme option de mise en forme. Si vous supprimez la balise `<p>`, l’auteur ou l’autrice du contenu ne peut pas sélectionner l’option **Formats des paragraphes**, même si d’autres formats sont configurés.

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
   * **Valeur** La balise block pour le format, par exemple : p, t1, t2.

     Vous n’avez pas besoin de saisir les crochets de séparation.

1. Sur le même nœud, ajoutez une autre propriété pour que le texte descriptif s’affiche dans la liste déroulante :

   * **Nom** `description`
   * **Type** `String`
   * **Valeur** Texte descriptif pour ce format, par exemple, Paragraphe, Titre 1, Titre 2. Ce texte est affiché dans la liste de sélection Format.

1. Enregistrez les modifications.

   Répétez les étapes pour chaque format requis.

>[!CAUTION]
>
Si vous définissez des formats personnalisés, les formats par défaut (`<p>`, `<h1>`, `<h2>` et `<h3>`) sont supprimés. Recréez le format `<p>`, car il s’agit du format par défaut.

## Configuration des caractères spéciaux {#spchar}

Dans une installation AEM standard, lorsque le module externe `misctools` est activé pour les caractères spéciaux (`specialchars`), une sélection par défaut est disponible immédiatement. Par exemple, les symboles de copyright et de marque.

Vous pouvez configurer l’éditeur de texte enrichi de manière à mettre à disposition votre propre sélection de caractères, en définissant des caractères distincts ou une séquence entière.

>[!CAUTION]
>
Si vous ajoutez vos caractères spéciaux, ils remplacent la sélection par défaut. Si nécessaire, définissez ou redéfinissez ces caractères dans votre propre sélection.

### Définition d’un caractère unique {#definesinglechar}

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/misctools`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
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

1. Sous `chars`, ajoutez un nœud destiné à contenir une définition de caractère individuel :

   * **Nom** Vous pouvez spécifier le nom, mais il doit refléter le caractère, par exemple, « moitié ».
   * **Type** `nt:unstructured`

1. Ajoutez la propriété suivante à ce nœud :

   * **Nom** `entity`
   * **Type** `String`
   * **Valeur** Représentation HTML du caractère nécessaire, par exemple, `&189;` pour la fraction un demi.

1. Enregistrez les modifications.

Dans CRXDE, une fois la propriété enregistrée, le caractère représenté s’affiche. Voir ci-dessous sous l’exemple du caractère demi. Répétez les étapes ci-dessus afin de rendre plus de caractères spéciaux disponibles pour les auteurs et autrices.

![Dans CRXDE, ajoutez un caractère unique pour qu’il soit disponible dans la barre d’outils d’éditeur de texte enrichi](assets/chlimage_1-106.png " Dans CRXDE, ajoutez un caractère unique pour qu’il soit disponible dans la barre d’outils d’éditeur de texte enrichi")

### Définition d’une série de caractères {#definerangechar}

1. Utilisez les étapes 1 à 3 de la section [Définition d’un caractère unique](#definesinglechar).
1. Sous `chars`, ajoutez un nœud destiné à contenir la définition de la plage de caractères :

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

   Par exemple, définissez une plage de 9998 à 10000. Vous y trouverez les caractères suivants.

   ![Définition dans CRXDE d’une série de caractères pour qu’elle soit disponible dans l’éditeur de texte enrichi](assets/chlimage_1-107.png)

   *Figure : Définition dans CRXDE d’une série de caractères pour qu’elle soit disponible dans l’éditeur de texte enrichi*

   ![Les caractères spéciaux disponibles dans l’éditeur de texte enrichi sont affichés pour les auteurs dans une fenêtre pop-up](assets/rtepencil.png " Les caractères spéciaux disponibles dans l’éditeur de texte enrichi sont affichés pour les auteurs dans une fenêtre pop-up")

## Configuration des styles de tableau {#tablestyles}

Les styles sont généralement appliqués au texte, mais un ensemble distinct de styles peut également être appliqué à un tableau ou à quelques cellules de tableau. Ces styles sont à la disposition des auteurs au niveau de la boîte du sélecteur de style dans la boîte de dialogue de propriétés de la cellule ou du tableau. Les styles sont disponibles lors de la modification d’un tableau dans un composant Texte (ou dérivé), et non dans le composant Tableau standard.

>[!NOTE]
>
Vous pouvez définir des styles de tableaux et de cellules uniquement pour l’IU classique.

>[!NOTE]
>
La copie et le collage de tableaux dans ou depuis un composant d’éditeur de texte enrichi dépendent du navigateur. Cette fonction n’est pas prise en charge par défaut pour tous les navigateurs. Vous pouvez obtenir des résultats variables selon la structure du tableau et le navigateur. Par exemple, lorsque vous copiez et collez un tableau dans un composant d’éditeur de texte enrichi dans Mozilla Firefox dans les IU classique et tactile, la mise en page du tableau n’est pas conservée.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/table`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
1. Créez la propriété `features` sur le nœud `table` :

   * **Nom** `features`
   * **Type** `String`
   * **Valeur** `*` (astérisque)

   >[!NOTE]
   >
   Si vous ne souhaitez pas activer toutes les fonctionnalités de tableau, vous pouvez créer la propriété `features`, comme suit :
   >
   * **Type** `String[]`
   >
   * **Valeurs** Un ou deux des éléments ci-dessous, au besoin :
   * `table` pour permettre de modifier les propriétés du tableau, dont les styles.
   * `cellprops` pour permettre de modifier les propriétés des cellules, dont les styles.

1. Définissez l’emplacement des feuilles de style CSS afin de pouvoir y faire référence. Voir [Spécification de l’emplacement de votre feuille de style](#locationofstylesheet), car cela revient à définir les [styles de texte](#textstyles). L’emplacement peut être défini si vous avez défini d’autres styles.
1. Sous le nœud `table`, créez les nœuds suivants (au besoin) :

   * Pour définir des styles pour le tableau entier (disponibles sous **Propriétés du tableau**) :

      * **Nom** `tableStyles`
      * **Type** `cq:WidgetCollection`

   * Pour définir des styles pour des cellules individuelles (disponibles sous **Propriétés de la cellule**) :

      * **Nom** `cellStyles`
      * **Type** `cq:WidgetCollection`

1. Créez un nœud (sous le nœud `tableStyles` ou `cellStyles`, selon les besoins) pour représenter un style individuel :

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

### Configuration d’en-têtes masqués dans les tableaux pour l’accessibilité {#hiddenheader}

Dans certains cas, vous pouvez créer des tableaux de données sans texte visuel dans un en-tête de colonne en supposant que l’objectif de l’en-tête est induit par la relation visuelle de la colonne avec d’autres colonnes. Dans ce cas, il est nécessaire de fournir du texte interne masqué dans la cellule de l’en-tête. Cela permet aux lecteurs d’écran et aux autres technologies d’assistance d’aider les lecteurs et les lectrices ayant des besoins variés à comprendre l’objectif de la colonne.

Pour améliorer l’accessibilité dans de telles situations, l’éditeur de texte enrichi prend en charge les cellules d’en-tête masquées. De plus, il fournit des paramètres de configuration associés aux en-têtes masqués dans les tableaux. Ces paramètres permettent d’appliquer des styles CSS à des en-têtes masqués en mode modification et aperçu. Pour aider les auteurs à identifier les en-têtes masqués en mode modification, incluez les paramètres ci-dessous dans votre code :

* `hiddenHeaderEditingCSS` : spécifie le nom de la classe CSS appliquée à la cellule hidden-header lorsque l’éditeur de texte enrichi est modifié.
* `hiddenHeaderEditingStyle` : spécifie une chaîne Style appliquée à la cellule hidden-header lorsque l’éditeur de texte enrichi est modifié.

Si vous spécifiez la chaîne CSS et la chaîne Style dans le code, la classe CSS prévaut sur la chaîne Style et peut remplacer les modifications apportées à la configuration en raison de la chaîne Style.

Pour aider les créateurs à appliquer la feuille de style CSS à des en-têtes masqués en mode aperçu, vous pouvez inclure les paramètres ci-dessous dans votre code :

* `hiddenHeaderClassName` : spécifie le nom de la classe CSS appliquée à la cellule d’en-tête masqué en mode aperçu.
* `hiddenHeaderStyle` : spécifie une chaîne Style appliquée à la cellule d’en-tête masqué en mode aperçu.

Si vous spécifiez la chaîne CSS et la chaîne Style dans le code, la classe CSS prévaut sur la chaîne Style et peut remplacer les modifications apportées à la configuration en raison de la chaîne Style.

## Ajout de dictionnaires au vérificateur orthographique {#adddict}

Lorsque le module externe Contrôle d’orthographe est activé, l’éditeur de texte enrichi utilise les dictionnaires de chaque langue appropriée. Ils sont sélectionnés en fonction de la langue du site web, d’après la propriété « language » de la sous-arborescence ou à partir de la langue de l’adresse URL. Par exemple, la branche `/en/` est vérifiée pour l’anglais ; la branche `/de/` est vérifiée pour l’allemand.

>[!NOTE]
>
Le message `Spell checking failed` s’affiche si le système tente d’effectuer une vérification pour une langue non installée. Les dictionnaires standard sont situés à l’emplacement `/libs/cq/spellchecker/dictionaries`, avec les fichiers Lisez-moi correspondants. Ne modifiez pas les fichiers.

Une installation d’AEM standard inclut les dictionnaires pour l’anglais américain (`en_us`) et l’anglais britannique (`en_gb`). Pour ajouter d’autres dictionnaires, suivez les étapes suivantes.

1. Accédez à la page [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Effectuez l’une des opérations suivantes pour trouver un dictionnaire de votre choix de langue :

   * Recherchez le dictionnaire de votre choix de langue. Sur la page du dictionnaire, localisez le lien vers la source originale ou la page Web de l’auteur. Localisez les fichiers de dictionnaire pour v2.x sur une telle page.
   * Recherchez des fichiers de dictionnaire v2.x à l’adresse [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Téléchargez l’archive avec les définitions d’orthographe. Extrayez le contenu de l’archive dans votre système de fichiers.

   >[!CAUTION]
   >
   Seuls les dictionnaires au format `MySpell` pour OpenOffice.org v2.0.1 ou version inférieure, sont pris en charge. Comme les dictionnaires sont désormais des fichiers d’archive, il est recommandé de vérifier l’archive après son téléchargement.

1. Recherchez les fichiers `.aff` et `.dic`. Conservez le nom du fichier en minuscules. Par exemple, `de_de.aff` et `de_de.dic`.
1. Chargez les fichiers `.aff` et `.dic` dans le référentiel à l’emplacement `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
Le vérificateur orthographique de l’éditeur de texte enrichi est disponible sur demande. Il n’est pas exécuté automatiquement lorsque vous commencez à saisir du texte. Pour exécuter le vérificateur orthographique, cliquez sur le [!UICONTROL Vérificateur orthographique] de la barre d’outils. L’éditeur de texte enrichi vérifie l’orthographe des mots et souligne les mots mal orthographiés.
>
Si vous incorporez des modifications que le vérificateur orthographique suggère, le statut du texte change et les mots mal orthographiés ne sont plus mis en surbrillance. Pour exécuter le vérificateur orthographique, cliquez de nouveau sur le bouton Vérificateur orthographique.

## Configuration de la taille de l’historique pour les actions d’annulation et de rétablissement {#undohistory}

L’éditeur de texte enrichi permet aux auteurs et autrices d’annuler ou de rétablir quelques dernières modifications. Par défaut, 50 modifications sont stockées dans l’historique. Vous pouvez configurer cette valeur, au besoin.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/undo`. Créez ces nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
1. Sur le nœud `undo`, créez la propriété :

   * **Nom** `maxUndoSteps`
   * **Type** `Long`
   * **Valeur** Nombre d’étapes annulées à enregistrer dans l’historique. La valeur par défaut est de 50. Utilisez `0` pour désactiver complètement l’annulation/le rétablissement.

1. Enregistrez les modifications.

## Configuration de la taille de tabulation {#tabsize}

Lorsque vous appuyez sur le caractère de tabulation dans un texte, un nombre prédéfini d’espaces est inséré ; par défaut, il s’agit de trois espaces insécables et d’un espace.

Pour définir la taille de la tabulation :

1. Dans votre composant, accédez au nœud `<rtePlugins-node>/keys`. Créez les nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un plug-in](#activateplugin).
1. Sur le nœud `keys`, créez la propriété :

   * **Nom** `tabSize`
   * **Type** `String`
   * **Valeur** Nombre d’espaces à utiliser pour le tabulateur

1. Enregistrez les modifications.

## Définition de la marge de retrait {#indentmargin}

Lorsque la mise en retrait est activée (par défaut), vous pouvez définir la taille du retrait :

>[!NOTE]
>
Cette taille de retrait n’est appliquée qu’aux paragraphes (blocs) de texte. Elle n’affecte pas la mise en retrait des listes.

1. Dans votre composant, recherchez le nœud `<rtePlugins-node>/lists`. Créez ces nœuds s’ils n’existent pas. Pour plus d’informations, voir [Activation d’un module externe](#activateplugin).
1. Sur le nœud `lists`, créez le paramètre `indentSize` :

   * **Nom** : `indentSize`
   * **Type** : `Long`
   * **Valeur** Nombre de pixels nécessaires pour la marge en retrait.

## Configuration de la hauteur de l’espace modifiable {#editablespace}

>[!NOTE]
>
Cela ne s’applique que lors de l’utilisation de l’éditeur de texte enrichi dans une boîte de dialogue (et non lors de la modification statique dans l’interface utilisateur classique).

Vous pouvez définir la hauteur de l’espace modifiable affiché dans la boîte de dialogue du composant :

1. Sur le nœud `../items/text` de la définition de boîte de dialogue pour le composant, créez une propriété :

   * **Nom** `height`
   * **Type** `Long`
   * **Valeur** Hauteur du canevas de publication, exprimée en pixels.

   >[!NOTE]
   >
   Cette opération ne modifie pas la hauteur de la fenêtre de la boîte de dialogue.

1. Enregistrez les modifications.

## Configuration des styles et des protocoles pour les liens {#linkstyles}

Lors de l’ajout de liens dans AEM, vous pouvez définir :

* les styles CSS à utiliser ;
* les protocoles qui sont automatiquement acceptés.

Pour configurer la façon dont les liens sont ajoutés dans AEM à partir d’un autre programme, définissez des règles HTML.

1. À l’aide de CRXDE Lite, cherchez le composant Texte pour votre projet.
1. Créez un nœud au même niveau que `<rtePlugins-node>`, c’est-à-dire créez le nœud sous le nœud parent de `<rtePlugins-node>` :

   * **Nom** `htmlRules`
   * **Type** `nt:unstructured`

   >[!NOTE]
   >
   Le nœud `../items/text` possède la propriété :
   >
   * **Nom** `xtype`
   * **Type** `String`
   * **Valeur** `richtext`
   >
   L’emplacement du nœud `../items/text` peut varier en fonction de la structure de votre boîte de dialogue, par exemple `/apps/myProject>/components/text/dialog/items/text` et `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Sous `htmlRules`, créez un nœud.

   * **Nom** `links`
   * **Type** `nt:unstructured`

1. Sous le nœud `links`, définissez les propriétés, au besoin :

   * Style CSS pour les liens internes :

      * **Nom** `cssInternal`
      * **Type** `String`
      * **Valeur** Nom de la classe CSS (non précédé d’un point « . » ; par exemple, `cssClass` au lieu de `.cssClass`)

   * Style CSS pour les liens externes

      * **Nom** `cssExternal`
      * **Type** `String`
      * **Valeur** Nom de la classe CSS (non précédé d’un point « . » ; par exemple, `cssClass` au lieu de `.cssClass`)

   * Tableau des **protocoles** valides. Les protocoles pris en charge sont les suivants : `http://`, `https://`, `file://` et `mailto:`.

      * **Nom** `protocols`
      * **Type** `String[]`
      * **Valeur** un ou plusieurs protocoles

   * **defaultProtocol** (propriété de type **String**) : protocole à utiliser si l’utilisateur n’en a pas spécifié un explicitement.

      * **Nom** `defaultProtocol`
      * **Type** `String`
      * **Valeur** un ou plusieurs protocoles par défaut

   * Définition de la gestion de l’attribut cible d’un lien. Créez un nœud :

      * **Nom** `targetConfig`
      * **Type** `nt:unstructured`

     Sur le nœud `targetConfig`, définissez les propriétés obligatoires :

      * Spécifiez le mode cible :

         * **Nom** `mode`
         * **Type** `String`
         * **Valeur**.

            * `auto` : signifie qu’une cible automatique est choisie

              (spécifié par la propriété `targetExternal` pour les liens externes ou `targetInternal` pour les liens internes).

            * `manual` : non applicable dans ce contexte
            * `blank` : non applicable dans ce contexte

      * Cible des liens internes :

         * **Nom** `targetInternal`
         * **Type** `String`
         * **Valeur** Cible des liens internes (utilisée uniquement lorsque le mode est `auto`)

      * Cible des liens externes :

         * **Nom** `targetExternal`
         * **Type** `String`
         * **Valeur** Cible des liens externes (utilisé uniquement lorsque le mode est `auto`).

1. Enregistrez toutes les modifications.
