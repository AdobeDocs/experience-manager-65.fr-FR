---
title: Tableaux dans les formulaires adaptatifs
seo-title: Tableaux dans les formulaires adaptatifs
description: Le composant Tableau d’AEM Forms permet de créer des tableaux dans les formulaires adaptatifs qui sont sensibles aux mises en page des périphériques mobiles. Il permet aussi d’utiliser des composants de table XDP.
seo-description: Le composant Tableau d’AEM Forms permet de créer des tableaux dans les formulaires adaptatifs qui sont sensibles aux mises en page des périphériques mobiles. Il permet aussi d’utiliser des composants de table XDP.
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 75%

---


# Tableaux dans les formulaires adaptatifs{#tables-in-adaptive-forms}

L’utilisation des tableaux est un moyen efficace, simplifié et organisé de présenter des données complexes. Cela permet aux utilisateurs d’identifier facilement les informations et leur fournit des données organisées sous forme de lignes et de colonnes. La plupart des formulaires des services financiers et des agences gouvernementales requièrent des tableaux de données volumineux pour saisir des données numériques et effectuer des calculs.

AEM Forms fournit un composant Tableau dans l’explorateur de composants de la barre latérale permettant de créer des tableaux dans les formulaires adaptatifs. Voici quelques-unes des capacités clés fournies :

* Disposition réactive sur périphériques mobiles
* Lignes et colonnes configurables
* Ajout et suppression dynamiques de lignes à l’exécution
* Combinaison ou fusion et fractionnement de cellules
* Accessibilité par les lecteurs d’écran
* Disposition personnalisée à l’aide de CSS
* Compatibilité et mappage avec un composant de tableau XDP
* Prise en charge de l’ajout de lignes ou de cellules à l’aide d’éléments complexes de type XSD
* Fusion des données à partir d’un fichier XML

## Création d’un tableau {#create-a-table}

Pour créer un tableau, faites glisser un composant Tableau à partir de l’explorateur de composants du panneau latéral d’un formulaire adaptatif. Par défaut, le tableau contient deux colonnes et trois lignes, dont la ligne d’en-tête.

![Composant Tableau dans la barre latérale AEM](assets/sidebar-tables.png)

### A propos de l’en-tête et des cellules du corps {#about-header-and-body-cells}

Les cellules d’en-tête sont des zones de texte. Pour modifier le libellé d’un en-tête, cliquez avec le bouton droit de la souris sur la cellule d’en-tête puis sur **Modifier**. Dans la boîte de dialogue Modifier, mettez à jour le libellé dans le champ **Valeur** et cliquez sur **OK**.

Les cellules du corps sont par défaut des zones de texte. Vous pouvez remplacer une cellule de corps par un autre composant de formulaire adaptatif disponible dans le panneau latéral, tel qu’une zone numérique, un sélecteur de date, ou une liste déroulante.

Par exemple, la première rangée du corps du tableau ci-dessous inclut les composants Zone de texte, Sélecteur de dates et Liste déroulante comme cellules.

![types de cellule-ligne](assets/row-cell-types.png)

Vous pouvez fusionner deux cellules du corps ou plus en sélectionnant les cellules que vous souhaitez fusionner, puis en cliquant avec le bouton droit et en choisissant la commande **Fusionner**. Vous pouvez aussi diviser une cellule fusionnée en cliquant sur celle-ci et en sélectionnant **Fractionner les cellules**.

### Ajout, suppression et déplacement de lignes et de colonnes  {#add-delete-move-rows-and-columns}

Vous pouvez ajouter et supprimer une ligne ou une colonne, ou encore déplacer une ligne vers le haut et vers le bas dans un tableau.

Pour ajouter ou supprimer une ligne ou une colonne ou déplacer une ligne, cliquez sur une cellule dans une ligne ou une colonne. Un menu contextuel s’affiche en haut de la colonne et à gauche de la ligne. Le menu de la partie supérieure fournit des options permettant d’ajouter ou de supprimer la colonne, alors que le menu de gauche permet d’ajouter, de supprimer ou de déplacer la ligne.

* L’opération Ajouter ajoute une ligne au-dessous ou une colonne à droite de la ligne ou de la colonne sélectionnée.
* L’opération Supprimer permet de supprimer la ligne ou la colonne sélectionnée.
* L’opération Déplacer permet de déplacer la ligne sélectionnée vers le haut et vers le bas.

Le menu déroulant pour la ligne propose également l’opération Modifier pour modifier les propriétés, les paramètres et les options de style de la ligne.

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>Alors qu’il est possible d’ajouter un nombre quelconque de lignes à un tableau, le nombre maximal de colonnes que vous pouvez ajouter est de six. En outre, vous ne pouvez pas supprimer la ligne d’en-tête du tableau.

### Ajouter une description de tableau  {#add-table-description}

Vous pouvez ajouter une description au tableau pour expliquer comment il organise les informations que les lecteurs peuvent interpréter et lire. Pour ajouter la description :

1. Sélectionnez le tableau et appuyez sur ![cmppr](assets/cmppr.png) pour afficher ses propriétés dans la barre latérale.
1. Spécifiez le résumé dans l’onglet Accessibilité.
1. Cliquez sur **Terminé**.

### Trier les colonnes d&#39;un tableau {#sortcolumnstable}

Vous pouvez trier les données en fonction de n’importe quelle colonne d’un tableau dans le formulaire adaptatif. Les valeurs de la colonne peuvent être triées par ordre croissant ou décroissant.

Le tri peut être appliqué aux colonnes du tableau contenant :

* Texte statique
* Propriétés de l’objet de modèle de données
* Combinaison de texte statique et de propriétés d’objet de modèle de données

Pour appliquer le tri sur les colonnes du tableau, les cellules des colonnes du tableau doivent contenir l’un des composants suivants : Zone numérique, Procédure pas à pas numérique, champ de saisie de date, sélecteur de date, texte ou zone de texte.

Pour activer le tri :

1. Sélectionnez le tableau et appuyez sur ![configure_icon](assets/configure_icon.png) (Configurer). Vous pouvez également sélectionner le tableau à l’aide du navigateur **Contenu** dans le panneau latéral de la communication interactive.
1. Sélectionnez **Activer le tri**.
1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du tableau. Les icônes de tri, les flèches vers le haut et vers le bas, dans les en-têtes de colonnes, indiquent que le tri a été activé.

   ![Activer le tri](assets/enable_sorting_new.png)

1. Passez au mode **Prévisualisation** pour vue de la sortie. Le tableau est automatiquement trié en fonction de la première colonne du tableau.
1. Cliquez sur l’en-tête de colonne pour trier les valeurs en fonction de la colonne.

   Un en-tête de colonne avec une flèche vers le haut indique que le tableau est trié en fonction de cette colonne. En outre, les valeurs de la colonne s’affichent dans l’ordre croissant.

   ![Tri dans l’ordre croissant](assets/sorting_ascending_new.png)

   De même, un en-tête de colonne avec une flèche vers le bas représente que les valeurs de la colonne sont affichées dans l’ordre décroissant.

   Vous pouvez également apporter des modifications au tableau en mode **Prévisualisation** et cliquer de nouveau sur l’en-tête de colonne pour trier les valeurs de colonne.

## Définir la largeur d&#39;une colonne pour un tableau {#set-column-width}

Exécutez les étapes suivantes pour définir la largeur de colonne d’un tableau :

1. Dans l&#39;onglet **[!UICONTROL Contenu]**, appuyez sur le composant **[!UICONTROL Table]** et appuyez sur l&#39;icône Configurer (![Configurer](assets/configure-icon.svg)).

1. Entrez la liste des valeurs séparées par des virgules dans le champ **[!UICONTROL Largeur de colonne]** pour spécifier la largeur proportionnelle de chaque colonne du tableau. Par exemple, pour un tableau qui comprend 3 colonnes, la spécification de 2,4,6 comme valeur dans le champ **[!UICONTROL Largeur de colonne]** entraîne la définition de la largeur des colonnes comme 2/12 pour la première colonne, 4/12 pour la deuxième colonne et 6/12 pour la troisième colonne. 2/12 car la largeur de la première colonne correspond à un sixième de la largeur du tableau. De même, le 12/4 définit la largeur de la deuxième colonne comme un tiers de la largeur du tableau et le 6/12 comme la largeur de la troisième colonne comme la moitié de la largeur du tableau.

## Configuration du style de tableau {#configure}

Vous pouvez définir le style d’un tableau à l’aide du mode Style dans la barre d’outils de la page. Exécutez les étapes suivantes pour passer en mode Style et modifier le style du tableau.

1. Dans la barre d’outils de la page, avant la Prévisualisation, appuyez sur ![menu déroulant Zone de travail](assets/canvas-drop-down.png) > **Style**.

1. Dans la barre latérale, sélectionnez le tableau et appuyez sur le bouton Modifier ![modifier-button](assets/edit-button.png).
Vous pouvez afficher les propriétés de style dans la barre latérale.

![Propriétés de style d’un tableau](assets/style-table.png)

>[!NOTE]
>
>Vous pouvez modifier le thème de couleur de l’en-tête et des lignes de corps en modifiant les valeurs des variables LESS. Pour plus d’informations, voir [Thèmes dans AEM Forms](/help/forms/using/themes.md) [](/help/forms/using/creating-custom-adaptive-form-themes.md).

## Ajout ou suppression dynamique d’une ligne {#add-or-delete-a-row-dynamically}

Les tableaux fournissent une assistance prête à l’emploi pour l’ajout ou la suppression dynamique de lignes au moment de l’exécution.

1. Sélectionnez une ligne de tableau et appuyez sur ![cmppr](assets/cmppr.png).
1. Dans l’onglet Paramètres de répétition, spécifiez les valeurs minimale et maximale pour limiter le nombre de lignes du tableau.
1. Cliquez sur **Terminé**.

Lors de l’exécution, vous verrez les boutons **+** et *-* pour ajouter ou supprimer une ligne.

![add-delete-rows-dynamiquement](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>L’ajout ou la suppression dynamique d’une ligne n’est pas prise en charge dans les en-têtes à gauche de la disposition des tableaux mobiles.

## Expressions dans un tableau  {#expressions-in-a-table}

Les tableaux des formulaires adaptatifs permettent d’écrire des expressions en JavaScript pour induire des comportements, tels qu’afficher ou masquer un tableau ou une ligne, ajouter tous les nombres et afficher le total dans une cellule, activer ou désactiver une cellule, valider une entrée utilisateur, etc. Ces expressions utilisent le modèle de script API des formulaires adaptatifs.

Alors que les tableaux et les lignes ne prennent en charge que les expressions de visibilité pour contrôler leur visibilité en fonction de la valeur renvoyée par une expression, les cellules prennent en charge les expressions suivantes :

* **Script d’initialisation** : pour effectuer une action à l’initialisation d’un champ.
* **Script de validation de valeur :** pour modifier les composants d’un formulaire après modification de la valeur d’un champ.

>[!NOTE]
>
>Si le script de modification/édition XFA est également appliqué au même champ, il s’exécute avant le script de validation de valeur.

* **Expressions de calcul** : pour calculer automatiquement la valeur d’un champ.
* **Expressions de validation** : pour valider un champ.
* **Expressions d’accès** : pour activer/désactiver un champ.
* **Expression de visibilité** : pour contrôler la visibilité d’un champ et d’un panneau.

L’expression de visibilité d’un tableau ou d’une ligne peut être définie dans l’onglet Propriétés du panneau de la boîte de dialogue Modifier le composant correspondant. Les expressions pour une cellule peuvent être définies dans l’onglet Script de la boîte de dialogue Modifier le composant correspondant.

Pour obtenir la liste complète des classes de formulaires adaptatifs, des événements, des objets et des API publiques, consultez la [référence d’API de bibliothèque JavaScript pour les formulaires adaptatifs.](https://helpx.adobe.com/fr/experience-manager/6-5/forms/javascript-api/index.html)

## Dispositions pour appareils mobiles {#mobile-layouts}

Les tableaux des formulaires adaptatifs fournissent une expérience sans précédent pour les périphériques mobiles en raison de leurs dispositions fluides et réactives. AEM Forms offre deux types de dispositions mobiles pour les tableaux : En-têtes à gauche et Colonnes réductibles.

Vous pouvez configurer une disposition de tableau pour périphériques mobiles depuis l’onglet Style de la boîte de dialogue Modifier le composant.

### Disposition En-têtes à gauche  {#headers-on-left}

Dans la disposition En-têtes à gauche, les en-têtes du tableau sont transposés à gauche. Une seule cellule apparaît pour un en-tête. Chaque ligne dans cette disposition s’affiche en tant que partie distincte. Les images suivantes comparent un tableau sur un bureau et le même tableau sur un périphérique mobile.

![vue de bureau](assets/desktopview_new.png)

Vue Bureau d’un tableau avec disposition En-têtes à gauche

![En-têtes à gauche](assets/headersontheleft_new.png)

Vue Mobile d’un tableau avec disposition En-têtes à gauche

### Disposition Colonnes réductibles {#collapsible-columns-layout}

Dans la disposition Colonnes réductibles, les colonnes du tableau sont réduites pour afficher une ou deux colonnes, selon la taille du périphérique. Les autres colonnes sont réduites. Vous pouvez cliquer sur l’icône Réduire/Développer pour afficher les autres colonnes de la table.

>[!NOTE]
>
>Bien que la disposition Colonnes réductibles soit optimisée pour les périphériques mobiles, elle fonctionne également sur le bureau, si la largeur disponible ne suffit pas à afficher toutes les colonnes d’un tableau.

Les images suivantes comparent l’aspect d’un tableau affiché sur un périphérique, l’un comportant des colonnes réduites, l’autre les affichant développées.

![colonne réduite](assets/collapsed-column.png)

Colonnes réduites d’un tableau comportant uniquement deux colonnes, apparaissant sur un périphérique mobile

![collapse_column](assets/collapsible_column.png)

Colonne développée d’un tableau sur un périphérique mobile

## Fusion de données dans un tableau  {#merge-data-in-a-table}

Les tableaux des formulaires adaptatifs permettent de renseigner le tableau lors de l’exécution avec des données provenant d’un fichier XML. Le fichier XML de données peut résider dans le système de fichiers local de l’ordinateur sur lequel le serveur AEM Forms est exécuté ou dans le référentiel CRX.

Prenons l’exemple du tableau récapitulatif de transaction bancaire suivant, que nous voulons renseigner avec des données provenant d’un fichier XML.

![tableau de fusion-données](assets/data-merge-table.png)

Dans cet exemple, la propriété Nom d’élément pour :

* la ligne est **Row1**
* la cellule de corps sous Date de transaction est **tableItem1**
* la cellule de corps sous Description est **tableItem2**
* la cellule de corps sous Type de transaction est **type**
* la cellule de corps sous Montant en euros est **tableItem3**

Le fichier XML contenant les données au format suivant : 

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>
```

Dans l’exemple XML, les données d’une ligne sont définies par les balises `<Row1>`, qui est le nom de l’élément pour la ligne du tableau. Dans la balise `<Row1>`, les données de chaque cellule sont définies dans la balise pour son nom d’élément, tel que `<tableItem1>`, `<tableItem2>`, `<tableItem3>` et `<type>`.

Pour les fusionner dans le tableau au moment de l’exécution, vous devez indiquer le formulaire adaptatif contenant le tableau à l’emplacement XML absolu avec le mode WCM désactivé. Par exemple, si le formulaire adaptatif se trouve à l’emplacement *https://localhost:4502/myForms/bankTransaction.html* et que le fichier XML de données est enregistré à l’emplacement *C:/myTransactions/bankSummary.xml*, vous pouvez vue le tableau avec des données à l’adresse URL suivante :

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![tableau fusionné de données](assets/data-merged-table.png)

## Utilisation des composants XDP et des types complexes de schéma XSD {#use-xdp-components-and-xsd-complex-types}

Si vous avez créé un formulaire adaptatif en fonction d’un modèle de formulaire XFA, les éléments XFA sont disponibles dans l’onglet Modèle de données de l’outil de recherche de contenu AEM. Vous pouvez faire glisser ces éléments XFA, notamment des tableaux, dans le formulaire adaptatif.

L’élément de tableau XFA est mappé sur le composant Tableau et fonctionne dans les formulaires adaptatifs prêts à l’emploi. Toutes les propriétés et fonctionnalités de tableau XDP sont conservées lors du déplacement dans le formulaire adaptatif, et vous pouvez effectuer n’importe quelle opération sur celui-ci comme vous le feriez avec le tableau natif du formulaire adaptatif. Par exemple, si une ligne dans un tableau XDP est marquée comme pouvant être répétée, elle sera répétée dans les formulaires adaptatifs également.

En outre, vous pouvez faire glisser et déposer le sous-formulaire XDP pour ajouter une nouvelle ligne au tableau. Toutefois, notez que déposer un sous-formulaire imbriqué ne fonctionne pas.

>[!NOTE]
>
>Un tableau XDP sans ligne d’en-tête ne sera pas mappé au composant Tableau de formulaire adaptatif. Au lieu de cela, il sera mappé sur le composant Panneau de formulaire adaptatif ayant une disposition fluide. En outre, lorsque vous ajoutez un tableau imbriqué XDP à un formulaire adaptatif, le tableau externe est converti en panneau tout en conservant le tableau interne.

Vous pouvez aussi faire glisser et déposer un groupe d’éléments de type complexe XSD pour créer une ligne de tableau. Une nouvelle ligne est créée sous la ligne sur laquelle vous avez déposé les éléments. Les cellules créées avec des éléments de type complexe XSD conservent une référence de liaison au schéma XSD. Vous pouvez également remplacer une cellule de corps par un élément de type complexe XSD en déposant l’élément sur la cellule.

>[!NOTE]
>
>Le nombre d’éléments dans un composant de tableau XDP, un sous-formulaire, ou un type complexe XSD ne peut pas dépasser le nombre de cellules dans une ligne. Par exemple, vous ne pouvez pas faire glisser quatre éléments sur une ligne qui n’a que trois cellules. Cela provoquera une erreur.
>
>Si le nombre d’éléments est inférieur au nombre de cellules dans une ligne, la nouvelle ligne ajoute d’abord les cellules en fonction des éléments, puis les cellules par défaut sont ajoutées pour remplir les autres cellules de la ligne. Par exemple, si vous déposez un groupe de trois éléments dans une ligne qui comporte quatre cellules, les trois premières cellules sont basées sur les éléments déposés et la cellule restante sera la cellule de tableau par défaut.

## Considérations principales {#key-considerations}

* Si vous déplacez des lignes vers le haut et vers le bas tout en créant un tableau à partir d’un schéma XSD, une perte de données des lignes du tableau est visible dans les données XML générées lors de l’envoi du formulaire.
* Dans un tableau par défaut, chaque cellule de contenu est associée à un nom d’élément prédéfini. Si vous ajoutez un autre tableau dans le formulaire adaptatif, les cellules de contenu par défaut du nouveau tableau auront le même nom d’élément que dans le premier. Dans ce cas, les données générées lors de l’envoi du formulaire comprennent uniquement les données des cellules de contenu par défaut de l’un des tableaux. Par conséquent, assurez-vous que vous renommez les noms d’élément pour les cellules de contenu par défaut pour qu’elles restent uniques et éviter toute perte de données.

   Notez que cela s’applique uniquement aux cellules de contenu par défaut. Si vous ajoutez d’autres lignes ou colonnes à un tableau, des noms d’éléments uniques seront générés automatiquement pour les cellules de contenu non définies par défaut.

