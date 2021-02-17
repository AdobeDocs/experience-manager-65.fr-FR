---
title: Configurez l’éditeur de texte enrichi pour créer du contenu dans Adobe Experience Manager.
description: Découvrez comment configurer l’éditeur de texte enrichi Adobe Experience Manager pour créer du contenu dans Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 430994c8e9951500378e0a4d56c8004e7e81c24f
workflow-type: tm+mt
source-wordcount: '3022'
ht-degree: 80%

---


# Configuration de l’éditeur de texte enrichi {#configure-the-rich-text-editor}

L’éditeur de texte enrichi met à la disposition des auteurs de nombreuses fonctionnalités pour modifier leur contenu textuel. Les icônes, les boîtes de dialogue de sélection, la barre d’outils et les menus apportent une expérience WYSIWYG de la modification des textes.

Pour savoir comment utiliser les fonctions de l’éditeur de texte enrichi pour la création, voir [Utilisation de l’éditeur de texte enrichi pour la création](/help/sites-authoring/rich-text-editor.md). L’éditeur de texte enrichi peut être configuré pour activer, désactiver et étendre les fonctions disponibles dans les composants de création. Le processus suivant illustre un ordre recommandé d&#39;exécution des tâches de configuration RTE dans le Experience Manager.

![Séquence d’étapes pour savoir comment configurer RTE](assets/rte_workflow_v1.png)

*Figure : Séquence d’étapes pour savoir comment configurer RTE*

## Présentation des IU tactile et classique {#understand-touch-enabled-ui-and-classic-ui}

L’interface utilisateur tactile est l’interface utilisateur standard du Experience Manager. Adobe a introduit l’interface utilisateur tactile avec [conception adaptée](/help/sites-authoring/responsive-layout.md) pour l’environnement de création. L’interface utilisateur tactile est conçue pour les périphériques tactiles et de bureau. L’interface diffère considérablement de l’interface utilisateur classique d’origine.

![Barre d’outils de l’éditeur de texte enrichi dans l’interface utilisateur tactile](assets/chlimage_1-35.png)

*Figure : Barre d’outils de l’éditeur de texte enrichi dans l’interface utilisateur tactile*

![Barre d’outils d’éditeur de texte enrichi dans l’IU classique](assets/rtedefault.png)

*Figure : Barre d’outils de l’éditeur de texte enrichi dans l’interface utilisateur classique*

>[!MORELIKETHIS]
>
>* [Recommandations relatives aux IU](/help/sites-deploying/ui-recommendations.md)
>* A propos de la dépréciation de l’interface utilisateur classique, voir [Notes de mise à jour du Experience Manager 6.5](/help/release-notes/deprecated-removed-features.md)
>* Pour connaître la différence entre les interfaces utilisateur, voir [Interface utilisateur tactile et IU classique](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/).
>* Pour comprendre en détail l’interface utilisateur tactile, voir [Concepts de l’interface utilisateur tactile du Experience Manager](/help/sites-developing/touch-ui-concepts.md).


## Différents modes de modification {#editingmodes}

Les auteurs peuvent créer et modifier du contenu textuel dans Experience Manager en utilisant les différents modes des composants. Les options de la barre d’outils pour la création et la mise en forme du contenu, et l’expérience utilisateur des composants compatibles avec l’éditeur de texte enrichi dans différents modes de modification, varient en fonction des configurations d’éditeur de texte enrichi.

| Mode de modification | Zone de modification | Fonctions dont l’activation est recommandée | IU tactile | IU classique |
|--- |--- |--- |--- |--- |
| En ligne | Modification en ligne pour des modifications rapides et mineures ; mettez en forme sans ouvrir une boîte de dialogue | Fonctions minimales d’éditeur de texte enrichi | O | O |
| Éditeur de texte enrichi en plein écran | Couvre la page entière | Toutes les fonctions requises d’éditeur de texte enrichi | O | N |
| Boîte de dialogue | Boîte de dialogue située en haut du contenu de page sans couvrir la page entière | Toutes les fonctions requises d’éditeur de texte enrichi dans l’IU classique ; activez les fonctions judicieusement dans l’IU tactile | O | O |
| Boîte de dialogue plein écran | Identique au mode plein écran ; contient des champs de la boîte de dialogue à côté de l’éditeur de texte enrichi | Toutes les fonctions requises d’éditeur de texte enrichi | O | N |

>[!NOTE]
>
>La fonction d’édition source n’est pas disponible en mode d’édition intégré dans l’interface utilisateur tactile. Vous ne pouvez pas faire glisser les images en mode plein écran. Toutes les autres fonctions sont utilisables dans tous les modes.

### Modification en ligne {#inline-editing}

Une fois ouvert (avec une double pression ou un double clic lent), le contenu peut être modifié dans la page. Une barre d’outils compacte avec des options très basiques est présentée.

![Modification en ligne avec une barre d’outils de base dans l’IU tactile](assets/chlimage_1-36.png)

*Figure : Modification en ligne avec la barre d’outils de base dans l’interface utilisateur tactile*

Dans l’IU classique, un double clic lent sur le composant permet la modification en ligne, et le contenu est encadré en orange. Si l’outil de recherche de contenu est ouvert, une barre d’outils avec les options de mise en forme disponibles de l’éditeur de texte enrichi est affichée en haut de la fenêtre. Si l’outil de recherche n’est pas ouvert, les options de mise en forme n’apparaissent pas, et vous pouvez uniquement effectuer des modifications de base sur le texte.

### Modification en plein écran {#full-screen-editing}

Les composants du Experience Manager peuvent être ouverts dans une vue plein écran qui masque le contenu de la page et occupe l’écran disponible. Considérez la modification en plein écran comme une version détaillée de la modification en ligne, car elle offre le plus grand nombre d’options de modification. Vous pouvez l’ouvrir en cliquant sur ![rte_fullscreen](assets/rte_fullscreen.png), dans la barre d’outils compacte lorsque vous utilisez le mode de modification en ligne. 

En mode de boîte de dialogue plein écran, outre une barre d’outils détaillée d’éditeur de texte enrichi, les options et les composants disponibles dans une boîte de dialogue sont également disponibles. Il s’applique seulement aux boîtes de dialogue qui contiennent l’éditeur de texte enrichi à côté d’autres composants.

![Barre d’outils détaillée d’éditeur de texte enrichi lors de la modification en plein écran dans l’IU tactile](assets/chlimage_1-37.png)

*Figure : Barre d’outils RTE détaillée lors de la modification en mode plein écran dans l’interface utilisateur tactile*

### Modification dans une boîte de dialogue {#dialog-editing}

Lorsque vous double-cliquez sur un composant, une boîte de dialogue apparaît pour modifier le contenu. La boîte de dialogue s’ouvre dans la partie supérieure de la page existante. Dans quelques scénarios spécifiques, la boîte de dialogue s’affiche comme fenêtre contextuelle. Par exemple, quand un composant Texte fait partie d’une colonne dans une mise en page à plusieurs colonnes et que la zone disponible pour la boîte de dialogue est moindre.

![Mode de modification dans une boîte de dialogue dans l’IU tactile](assets/dialog_editing_modetouchui.png)

*Figure : Mode de modification de la boîte de dialogue dans l’interface utilisateur tactile*

![Zone de dialogue dans l’IU classique qui contient la barre d’outils détaillée pour la modification](assets/chlimage_1-38.png)

*Figure : Boîte de dialogue de l’interface utilisateur classique contenant une barre d’outils détaillée à modifier*

## À propos des modules externes de l’éditeur de texte enrichi et des fonctions associées {#aboutplugins}

Cette fonctionnalité est mise à disposition par le biais d’une série de modules externes, comportant chacun :

* Une propriété `features` :

   * utilisée afin d’activer ou désactiver une fonctionnalité de base pour ce module externe ;
   * configurable selon une procédure normalisée

* Le cas échéant, des propriétés et options supplémentaires nécessitant une configuration spécialisée.

Les fonctions de base d’éditeur de texte enrichi sont activées, ou désactivées, par la valeur de la propriété `features` sur un nœud spécifique au module externe approprié.

Le tableau ci-dessous répertorie les modules externes actuels et indique les informations suivantes :

* Les ID des modules externes avec un lien vers la documentation des API. L’ID est utilisé comme nom de nœud lors de l’[activation d’un module externe](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* Les valeurs admises pour la propriété `features`.
* Une description de la fonctionnalité fournie par le module externe.

| ID du module externe | features | Description |
|--- |--- |--- |
| edit | cut copy paste-default paste-plaintext paste-wordhtml | [Couper, copier et les trois modes de collage](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [findreplace](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | find replace | Rechercher et remplacer. |
| [format](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | bold italic underline | [Mise en forme textuelle de base](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [image](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | image | Prise en charge de base des images (faire glisser à partir du contenu ou de l’outil de recherche de contenu). Selon le navigateur, la prise en charge présente différents comportements pour les auteurs |
| [keys](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | Pour définir cette valeur, voir [taille de tabulation](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | justifyleft justifycenter justifyright | Alignement de paragraphe. |
| [links](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | modifylink unlink anchor | [Liens hypertextes et ancres](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| [lists](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | ordered unordered indent outdent | Ce module externe contrôle à la fois la [mise en retrait et les listes](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin), y compris les listes imbriquées. |
| [misctools](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | Divers outils permettent aux auteurs de saisir des [caractères spéciaux](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) ou de modifier la source HTML. En outre, vous pouvez ajouter toute une gamme de [caractères spéciaux](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) si vous voulez définir votre propre liste. |
| Paraformat | paraformat | Les formats de paragraphe par défaut sont : Paragraphe, En-tête 1, En-tête 2 et En-tête 3 (`<p>`, `<h1>`, `<h2>` et `<h3>`). Vous pouvez [ajouter davantage de formats de paragraphe](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) ou prolonger la liste. |
| spellcheck | checktext | [Vérificateur orthographique sensible à la langue](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| styles | styles | Prise en charge de l’application d’un style en utilisant une classe CSS. [Ajoutez de nouveaux styles de texte](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) si vous voulez ajouter (ou étendre) votre propre gamme de styles utilisables avec du texte. |
| subsuperscript | subscript superscript | Extensions des formats de base, en ajoutant l’indice et l’exposant. |
| table | table removetable insertrow removerow insertcolumn removecolumn cellprops mergecells splitcell selectrow selectcolumns | Voir [Configuration des styles de tableau](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles) si vous voulez ajouter vos propres styles pour des tableaux entiers ou des cellules individuelles. |
| undo | undo redo | Taille de l’historique des opérations [d’annulation et de rétablissement](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory). |

>[!NOTE]
>
>Le module externe Plein écran n’est pas pris en charge en mode de boîte de dialogue. Utilisez le paramètre `dialogFullScreen` pour configurer la barre d’outils en mode plein écran.

## Présentation des chemins et des emplacements de configuration {#understand-the-configuration-paths-and-locations}

[Mode de modification d’éditeur de texte enrichi (et de l’IU)](#editingmodes) que vous fournissez pour que les auteurs déterminent l’emplacement des informations de configuration lorsque vous [activez les modules externes d’éditeur de texte enrichi](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin) :

| Mode de modification | Emplacement de l’IU tactile | Emplacement de l’IU classique |
|---|---|---|
| En ligne | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| Plein écran | `cq:editConfig/cq:inplaceEditing` | Non applicable |
| Boîte de dialogue | `cq:dialog` | `dialog` |
| Boîte de dialogue plein écran | `cq:dialog` | Non applicable |

>[!NOTE]
>
>Ne donnez pas le nom `cq:inplaceEditing` au nœud sous `config`. Sur le nœud `cq:inplaceEditing`, définissez les propriétés suivantes :
>* **Nom** : `configPath`
>* **Type** : `String`
>* **Valeur** : chemin du nœud qui contient la configuration proprement dite.

>
>
Ne donnez pas le nom `config` au nœud de configuration de l’éditeur de texte enrichi (RTE). Autrement, les configurations de l’éditeur de texte enrichi prennent effet seulement pour les administrateurs et non pour les utilisateurs du groupe `content-author`.

Configurez les propriétés suivantes qui s’appliquent uniquement au mode de modification dans la boîte de dialogue dans l’IU tactile :

* `useFixedInlineToolbar` : configurez cette propriété booléenne définie sur le nœud d’éditeur de texte enrichi (une avec sling:resourceType=`cq/gui/components/authoring/dialog/richtext`) sur `True` pour que la barre d’outils de l’éditeur de texte enrichi reste fixe au lieu d’être flottante.

    Lorsque cette propriété est définie sur true, la modification en texte démarre par défaut sur l’événement « foundation-contentloaded ».

   Pour éviter cette situation, définissez la propriété `customStart` sur `True` et déclenchez l’événement « rte-start » pour commencer la modification avec l’éditeur de texte enrichi. Lorsque cette propriété est définie sur true, le comportement par défaut (l’éditeur de texte enrichi démarre en cas de clic) ne fonctionne pas.

* `customStart` : configurez cette propriété booléenne définie sur le nœud de l’éditeur de texte enrichi sur `True` pour contrôler à quel moment démarrer l’éditeur de texte enrichi en déclenchant l’événement `rte-start`.

* `rte-start` : déclenchez cet événement sur l’élément `contenteditable-div` d’éditeur de texte enrichi lorsque vous commencez la modification avec l’éditeur de texte enrichi. Cette option ne fonctionne que si `customStart` a été défini sur true.

Lorsque l’éditeur de texte enrichi est utilisé dans la boîte de dialogue optimisée pour les écrans tactiles, la définition de la propriété `useFixedInlineToolbar` sur true est obligatoire pour éviter des problèmes.

## Personnalisation de la modification en place {#customizing-in-place-editing}

Vous pouvez définir sur quel sélecteur HTML l’éditeur de texte début en configurant les propriétés suivantes :

* **`editElementQuery`** - Définie sur  `cq:InplaceEditingConfig`, cette propriété est utilisée pour spécifier un sélecteur de l&#39;élément HTML sur lequel la modification intégrée du composant de texte sera lancée. Si elle n’est pas spécifiée, la modification en ligne est directement lancée sur le composant HTML de texte.
* **`textPropertyName`** - Définie sur  `cq:InplaceEditingConfig`, cette propriété est utilisée pour spécifier le nom de la propriété qui sera enregistrée sur le noeud de contenu où la valeur HTML du composant de texte sera conservée après modification en ligne.

La propriété correspondante pour le mode boîte de dialogue est `name`.

## Activation des fonctionnalités d’éditeur de texte enrichi en activant des modules externes {#enable-rte-functionalities-by-activating-plug-ins}

Les fonctionnalités d’éditeur de texte enrichi sont rendues disponibles par l’intermédiaire d’une série de modules externes, chacun avec sa propriété features. Vous pouvez configurer la propriété features afin d’activer ou de désactiver une ou plusieurs fonctions de chaque module externe.

Pour consulter des configurations détaillées des modules externes de l’éditeur de texte enrichi, voir [Activation et configuration des modules externes de l’éditeur de texte enrichi](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**Exemple** : Téléchargez  [cet exemple de ](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) configuration qui illustre comment configurer RTE. Dans ce module, toutes les fonctionnalités sont activées.

>[!NOTE]
>
>Le [composant textuel des composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) permet aux éditeurs de modèle de configurer de nombreux modules externes de l’éditeur de texte enrichi en tant que stratégies de contenu dans une interface utilisateur graphique, rendant ainsi inutile toute configuration technique. Les stratégies de contenu peuvent fonctionner avec les configurations d’interface utilisateur de l’éditeur de texte enrichi décrites dans ce document.
>
>Pour plus d’informations, voir la section [Paramètres de l’interface utilisateur de l’éditeur de texte enrichi et stratégies de contenu](/help/sites-administering/rich-text-editor.md) de ce document ainsi que [Création de modèles de page](/help/sites-authoring/templates.md) et la [documentation du développeur des composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>À titre de référence, les composants Texte par défaut (fournis dans le cadre d’une installation standard) se trouvent sous :
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
Pour créer votre propre composant textuel, copiez le composant ci-dessus au lieu de modifier ces composants.

## Configuration de la barre d’outils de l’éditeur de texte enrichi  {#dialogfullscreen}

AEM vous permet de configurer différemment l’interface de l’éditeur de texte enrichi pour les différents modes de modification. Les paramètres par défaut sont fournis ci-dessous. Vous pouvez remplacer ces paramètres par défaut en fonction de vos besoins. Vous personnalisez uniquement les fonctionnalités de la barre d’outils que vous souhaitez fournir à vos auteurs. Vous n’avez pas besoin de définir toutes les configurations de barre d’outils.

Pour configurer la barre d’outils pour `dialogFullScreen`, utilisez l’exemple de configuration suivant.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Différents paramètres d’IU sont utilisés pour les modes en ligne et plein écran. La propriété toolbar est utilisée pour spécifier les boutons de la barre d’outils.

Par exemple, si le bouton est lui-même une fonctionnalité (par exemple, `Bold`), il est spécifié comme `PluginName#FeatureName` (par exemple, `links#modifylink`).

Si le bouton est une fenêtre contextuelle (contenant certaines fonctionnalités d’un module externe), il est spécifié comme `#PluginName` (par exemple, `#format`).

Les séparateurs (`|`) entre un groupe de boutons peuvent être spécifiés avec `-`.

Le nœud pop-up sous le mode en ligne ou plein écran contient la liste des éléments contextuels utilisés. Chaque nœud enfant sous le nœud « popovers » (éléments contextuels) est nommé en fonction du module externe (format, par exemple). Il possède des « éléments » de propriété contenant la liste des fonctions du module externe (format#bold, par exemple).

## Paramètres de l’interface utilisateur de l’éditeur de texte enrichi et stratégies de contenu   {#rtecontentpolicies}

Les administrateurs peuvent contrôler les options de l’éditeur de texte enrichi à l’aide de stratégies de contenu, au lieu de procéder à la configuration en suivant les instructions ci-dessus, par exemple. Les stratégies de contenu définissent les propriétés de conception d’un composant lorsqu’il est utilisé dans le cadre d’un [modèle modifiable](/help/sites-authoring/templates.md). Par exemple, si un composant textuel qui utilise l’éditeur de texte enrichi est employé avec un modèle modifiable, la stratégie de contenu peut définir que l’option Gras doit être disponible, au même titre que quelques options de mise en forme de paragraphe. Les stratégies de contenu sont réutilisables et peuvent être appliquées à plusieurs modèles.

Les options disponibles dans l’éditeur de texte enrichi sont transmises depuis les configurations de l’interface utilisateur en amont vers les stratégies de contenu.

* Les paramètres de configuration de l’interface utilisateur définissent les options disponibles pour les stratégies de contenu.
* Si un élément a été supprimé ou n’est pas activé par la configuration d’interface utilisateur de l’éditeur de texte enrichi, la stratégie de contenu ne peut pas le configurer.
* Un auteur n’a accès à une fonctionnalité de ce type que si elle est mise à sa disposition par les configurations de l’interface utilisateur et les stratégies de contenu.

Pour consulter un exemple, reportez-vous à la [documentation du composant principal Texte](https://docs.adobe.com/help/fr-FR/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personnalisation de l’association entre les commandes et les icônes de la barre d’outils {#iconstoolbar}

Vous pouvez personnaliser l’association entre les icônes Coral affichées dans la barre d’outils de l’éditeur de texte enrichi et les commandes disponibles. Vous ne pouvez utiliser que les icônes Coral.

1. Créez un nœud intitulé `icons` sous `uiSettings/cui`.

1. Sous ce nœud, créez des nœuds pour les différentes icônes.
1. Sur chacun des nœuds d’icône, spécifiez une icône Coral et une commande à laquelle elle doit être associée.

Vous trouverez, ci-dessous, un exemple de fragment de code pour associer la commande Gras à l’icône Coral intitulée `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Passage à l’éditeur de texte enrichi CoralUI 2 {#switch-to-coralui-rich-text-editor}

Sur une page, vous pouvez inclure CoralUI 2 RTE clientlib ou CoralUI 3 RTE clientlib. Par défaut, l’éditeur de texte enrichi comprend la bibliothèque client de CoralUI 3. Pour passer à l’éditeur de texte enrichi CoralUI 2, exécutez les étapes suivantes.

>[!NOTE]
>
>Adobe ne le recommande pas comme une bonne pratique. Passez à l’éditeur de texte enrichi CoralUI 2 en dernier recours. Les modules externes personnalisés pour l’éditeur de texte enrichi CoralUI 2 fonctionnent avec l’éditeur de texte CoralUI 3 s’ils ne dépendent pas d’éléments internes à l’éditeur de texte, tels que des classes.
>
>Si vous employez des modules externes personnalisés pour l’éditeur de texte enrichi CoralUI3, utilisez la bibliothèque `rte.coralui3`.


1. Recouvrez le noeud `/libs/cq/gui/components/authoring/editors/clientlibs/core` sous `/apps`, puis procédez comme suit :

   * Remplacez `rte.coralui3` par `rte.coralui2` pour la propriété des dépendances.
   * Remplacez `cq.authoring.editor.core.inlineediting.rte.coralui3` par `cq.authoring.editor.core.inlineediting.rte.coralui2` pour la propriété embed.
   * Remplacez `cq.authoring.rte.coralui3` par `cq.authoring.rte.coralui2` pour la propriété embed.

1. Incrustez les noeuds `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` et `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` sous `/apps`.

   Supprimez la catégorie `cq.authoring.dialog` de `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` et ajoutez-la à `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. Changez n’importe quelle autre dépendance incluse à la page de `rte.coralui3` à `rte.coralui2`. Par exemple, après avoir superposé le noeud `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` sous `/apps`, remplacez toute dépendance de `rte.coralui3` par `rte.coralui2`.

1. Incrustez le noeud `cq/ui/widgets` sous `/apps`. Remplacez la dépendance `cq.rte` au noeud `/apps/cq/ui/widgets` par `cq.coralui2.rte`.

>[!NOTE]
>
>L’éditeur de texte enrichi CoralUI 2 utilise des modèles handlebars pour les boîtes de dialogue des modules externes. Par conséquent, la bibliothèque client de l’éditeur de texte enrichi CoralUI 2 dépendait de la bibliothèque client handlebars. L’éditeur de texte enrichi CoralUI 3 n’utilise pas de modèles handlebars, et aucune dépendance n’y est associée. Si vos modules externes personnalisés utilisent des modèles handlebars, ajoutez la bibliothèque client handlebars dans votre page web.

## Informations supplémentaires {#further-information}

Pour plus d’informations sur la configuration de l’éditeur de texte enrichi, voir la référence de l’[API des widgets AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText).

En particulier, pour connaître les modules externes et les options associées disponibles :

* Le composant [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) contient un champ de formulaire permettant de modifier les informations de texte stylisé (texte enrichi) : Pour connaître tous les paramètres disponibles pour le formulaire de texte enrichi, voir les options de configuration.
* Le composant RichText fournit un large éventail de fonctionnalités en utilisant les modules externes répertoriés sous [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). Pour chaque module externe :

   * voir les fonctions pour plus d’informations sur les fonctionnalités qui peuvent être activées (ou désactivées) ;
   * voir les options de configuration afin de connaître tous les paramètres disponibles pour la configuration détaillée du module externe approprié.

* Vous trouverez également plus d’informations sur les règles HTML pour les liens.

Ils peuvent être utilisés pour étendre et personnaliser votre propre RTE. Par exemple, pour répertorier les ancres disponibles dans la page en créant un lien, vous pouvez fournir votre propre mise en œuvre de `LinkPlugin`.

## Limitations connues {#known-limitations}

La fonctionnalité AEM RTE présente les limites suivantes :

* Les fonctionnalités de l’éditeur de texte enrichi sont prises en charge seulement dans les boîtes de dialogue des composants d’AEM. L’éditeur de texte enrichi n’est pas pris en charge sur les assistants ou les formulaires de base comme [Propriétés de la page](/help/sites-developing/page-properties-views.md) et [Génération de modèles automatique](/help/sites-authoring/scaffolding.md) sur l’IU tactile.

* AEM ne fonctionne pas sur les [dispositifs hybrides](/help/release-notes/known-issues.md).

* Ne donnez pas le nom `config` au nœud de configuration de l’éditeur de texte enrichi (RTE). Autrement, les configurations de l’éditeur de texte enrichi prennent effet seulement pour les administrateurs et non pour les utilisateurs du groupe `content-author`.

* RTE ne prend pas en charge les images intégrées ni les iframes pour incorporer un contenu.

## Bonnes pratiques et astuces {#best-practices-and-tips}

* Activez uniquement les modules externes sans fenêtre contextuelle pour afficher une boîte de dialogue flottante. Les modules externes sans fenêtre contextuelle sont plus petits et sont les mieux adaptés aux boîtes de dialogue flottantes.
* Activez les modules externes avec une fenêtre contextuelle plus grande, comme le module externe `Paste`, uniquement en mode Boîte de dialogue plein écran ou en mode Plein écran. Les modules externes possédant une grande fenêtre contextuelle nécessitent davantage d’espace sur l’écran pour offrir une expérience de création optimale.
* Si vous employez des modules externes personnalisés pour l’éditeur de texte enrichi CoralUI3, utilisez la bibliothèque `rte.coralui3`.

## Résolution des problèmes fréquents avec RTE {#troubleshoot-issues-with-aem-rich-text-editor}

**Comment sélectionner plusieurs cellules d’un tableau ?**

Pour sélectionner plusieurs cellules dans un tableau, appuyez sur la touche `Ctrl` ou `Cmd`, puis cliquez sur les cellules du tableau une par une.

Vous pouvez maintenant faire votre manipulation sur la sélection, par exemple définir les propriétés des cellules sélectionnées.

**Les liens hypertexte sont perdus lors de la modification d’un composant à l’aide du bouton Configurer**

Ajoutez un lien hypertexte dans un composant de texte en le modifiant à l’aide du bouton Configurer. Vous risquez de perdre le lien hypertexte si vous le modifiez à nouveau et que vous le validez une deuxième fois.

Une solution consiste à cliquer dans le composant de texte lorsque la boîte de dialogue de modification est affichée une seconde fois, puis à exécuter la validation du lien.

Ce problème est résolu dans AEM 6.3 et dans les versions ultérieures.

**Le contenu HTML ajouté en mode de modification de la source est perdu**

N’ajoutez pas de code HTML allant à l’encontre de XSS. AEM, et non pas l’éditeur de texte enrichi, peut supprimer du contenu HTML pour se conformer aux règles AntiSamy XSS.

Pour vérifier que le code HTML collé est enregistré, vérifiez le contenu enregistré dans CRXDE (dans le nœud de contenu).

S’il n’est pas enregistré, le code HTML a probablement été supprimé par l’éditeur de texte enrichi car il n’est pas conforme à ses règles.

Si elle est enregistrée dans CRXDE mais pas rendue sur la page (pour vérifier le rendu, voir la [prévisualisation](/help/sites-authoring/editing-content.md#preview-mode) de la page, elle est supprimée par AEM règles XSS.

**Le composant multichamp ne fonctionne pas comme prévu**

Pour créer un composant multichamp, utilisez uniquement CoralUI 3. N’utilisez pas les boîtes de dialogue de composant CoralUI 2.

Vérifiez également que le code de mise en œuvre multichamp et la structure de nœud sont corrects.

**La configuration disponible pour les administrateurs n’est pas accessible aux auteurs**

Si les mises à jour de configuration de l’interface apparaissent pour les comptes des administrateurs mais pas pour les auteurs, vérifiez que le nœud de configuration n’est pas nommé `config`. Utilisez la propriété [`configPath`](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [Configuration des modules externes d’éditeur de texte enrichi](configure-rich-text-editor-plug-ins.md)
>* [Utilisation de l’éditeur de texte enrichi pour la création](../sites-authoring/rich-text-editor.md)
>* [Configuration de l’éditeur de texte enrichi pour les sites accessibles](rte-accessible-content.md)
>* [Parité des fonctions entre les IU tactile et classique](../release-notes/touch-ui-features-status.md)
>* [Extrait d’un tutoriel pour créer un composant multichamp composite](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

