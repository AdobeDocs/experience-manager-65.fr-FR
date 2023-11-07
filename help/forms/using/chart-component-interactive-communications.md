---
title: Utilisation de graphiques dans les communications interactives
seo-title: Chart component in Interactive Communications
description: En utilisant des graphiques dans une communication interactive, vous pouvez condenser de grandes quantités d’informations dans un format visuel facile à analyser.
seo-description: AEM Forms provides a chart component that you can use to create charts in your Interactive Communication. This document explains basic and agent configurations of the chart component.
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
feature: Interactive Communication
exl-id: 0f877a15-a17f-427f-8d89-62ada4d20918
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2608'
ht-degree: 84%

---

# Utilisation de graphiques dans les communications interactives{#using-charts-in-interactive-communications}

Un graphique ou un graphique est une représentation visuelle des données. Il condense de grandes quantités d’informations dans un format visuel facile à comprendre, ce qui permet aux destinataires de la communication interactive de mieux visualiser, interpréter et analyser les données complexes.

Lors de la création d’une communication interactive, vous pouvez ajouter des graphiques pour représenter visuellement des données bidimensionnelles à partir du modèle de données de formulaire de la communication interactive. Le composant Graphique vous permet d’ajouter et de configurer les types de graphiques suivants : Circulaire, Colonne, Anneau, Barre, Ligne, Ligne et Point, Point, Zone et Quadrant.

## Ajouter et configurer un graphique dans une communication interactive {#add-and-configure-chart-in-an-interactive-communication}

Pour ajouter et configurer un graphique dans une communication interactive, procédez comme suit :

1. Cliquez sur **Composants** dans la sidekick de la communication interactive.
1. Faites glisser, puis déposez le composant de **Graphique** sur l’un des composants suivants :

   * Canal d’impression : zone cible et champ Image
   * Canal web : panneau ou zone cible

1. Cliquez sur le composant de graphique dans l’éditeur de communication interactive et sélectionnez **[!UICONTROL Configurer (]** ![configure_icon](assets/configure_icon.png)) dans la barre d’outils Composant.

   Les propriétés du graphique s’affichent dans le volet gauche.

   ![Propriétés de base d’un graphique en ligne dans le canal d’impression](assets/chart_properties_print_new.png)

   Propriétés de base d’un graphique en ligne dans le canal d’impression

   ![Propriétés de base d’un graphique en ligne dans le canal web](assets/chart_properties_web_new.png)

   Propriétés de base d’un graphique en ligne dans le canal web

1. Configurez les [propriétés du graphique](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) selon le type de canal.
1. (Canal d’impression uniquement) Dans les **[!UICONTROL Paramètres d’agent]**, indiquez si l’utilisation de ce graphique est obligatoire pour l’agent. Si l’option **[!UICONTROL L’utilisation de ce graphique est obligatoire pour l’agent]** n’est pas sélectionnée, l’agent peut cliquer sur l’icône du graphique représentant un œil dans l’onglet **[!UICONTROL Contenu]** de l’interface utilisateur de l’agent pour afficher/masquer le graphique.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. Cliquez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du graphique.

   Cliquez sur **[!UICONTROL Prévisualisation]** pour afficher l’aspect et les données associées au graphique. Cliquez sur **[!UICONTROL Modifier]** pour reconfigurer les propriétés du graphique.

## Configurer les propriétés du graphique {#configure-chart-properties}

Configurez les propriétés suivantes lors de la création de graphiques pour les canaux d’impression et web :

<table>
 <tbody>
  <tr>
   <td>Champ</td>
   <td>Description</td>
   <td>Type de canal</td>
  </tr>
  <tr>
   <td>Nom</td>
   <td>Identifiant de l’élément graphique. Le nom du graphique spécifié dans ce champ n’est pas visible sur le graphique. Il est utilisé lors de la référence à l’élément à partir d’autres composants, scripts et expressions SOM.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Type de graphique</td>
   <td>Type de graphique que vous souhaitez générer. Les options disponibles sont les suivantes : circulaire, en anneau, à barres, à colonnes, linéaire, linéaire et à points, à points et en aires.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Série &gt; Plusieurs séries</td>
   <td>Sélectionnez cette option pour ajouter plusieurs séries pour les éléments de collecte de modèle de données de formulaire tracés sur l’axe X et l’axe Y.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Série &gt; Objet de modèle de données</td>
   <td>Nom de l’élément de collecte de modèle de données de formulaire pour ajouter plusieurs séries au graphique.<br /> Choisissez une propriété d’objet de modèle de données de formulaire parent pour les propriétés tracées sur l’axe X et l’axe Y afin de former une série significative. L’objet de modèle de données que vous liez doit être de type Nombre, Chaîne ou Date.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Afficher les éléments empilés</td>
   <td>Choisissez d’empiler les valeurs de chaque série les unes sur les autres.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Axe X &gt; Titre</td>
   <td>Titre de l’axe X.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Axe X &gt; Objet du modèle de données</td>
   <td><p>Nom de l’élément de collection de modèles de données de formulaire à tracer sur l’axe X.</p> <p>Choisissez deux propriétés de type collection/tableau du même objet de modèle de données parent significatives l’une par rapport à l’autre à tracer sur les axes X et Y d’un graphique. L’objet de modèle de données que vous liez doit être de type Nombre, Chaîne ou Date.</p> </td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Axe Y &gt; Titre</td>
   <td>Titre de l’axe Y. </td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Axe Y &gt; Objet du modèle de données</td>
   <td><p>Élément de collection de modèles de données de formulaire à tracer sur l’axe Y. Dans le canal d’impression, l’objet de modèle de données pour l’axe Y doit être de type Nombre.</p> <p>Choisissez deux propriétés de type collection/tableau du même objet de modèle de données parent significatives l’une par rapport à l’autre à tracer sur les axes X et Y d’un graphique. </p> </td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Axe Y &gt; Fonction</td>
   <td>Fonction statistique/personnalisée à utiliser pour calculer les valeurs sur l’axe Y.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Masquer l’objet</td>
   <td>Sélectionnez cette option pour masquer le graphique au niveau de la sortie finale.</td>
   <td>Impression et web</td>
  </tr>
  <tr>
   <td>Titre</td>
   <td>Titre du graphique. </td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Hauteur</td>
   <td>Hauteur du graphique en pixels.</td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Largeur</td>
   <td>Largeur du graphique en pixels. Vous pouvez contrôler la largeur du graphique dans le canal web à l’aide du calque de style ou en appliquant un thème.</td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Saut de page obligatoire avant</td>
   <td>Sélectionnez cette option pour ajouter un saut de page obligatoire avant le graphique et pour placer le graphique en haut d’une nouvelle page. </td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Saut de page obligatoire après</td>
   <td>Sélectionnez cette option pour ajouter un saut de page obligatoire après le graphique et pour placer le contenu suivant le graphique en haut d’une nouvelle page. </td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Indentation</td>
   <td>Mise en retrait du graphique depuis le côté gauche de la page. </td>
   <td>Imprimer</td>
  </tr>
  <tr>
   <td>Info-bulle</td>
   <td><p>Format dans lequel l’info-bulle s’affiche lorsque le curseur de la souris survole un point de données du graphique dans le canal web. La valeur par défaut est ${x}(${y}). En fonction du type de graphique, lorsque vous passez le curseur sur un point, une barre ou une tranche du graphique, les variables ${x} et ${y} sont remplacées de manière dynamique par les valeurs correspondantes sur l’axe X et l’axe Y et elles s’affichent dans l’info-bulle.</p> <p>Pour désactiver l’info-bulle, laissez le champ <span class="uicontrol">Info-bulle</code> champ vide. Cette option ne s’applique pas aux graphiques en ligne ni en points. Par exemple, consultez <a href="#chartoutputprintweb">Exemple 1 : sortie du graphique sur papier et sur le Web</a>.</p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>Configurations spécifiques au graphique</td>
   <td><p>En plus des configurations courantes, la configuration spécifique au graphique suivante est disponible :</p>
    <ul>
     <li><strong>Afficher une légende : </strong>affiche une légende pour le graphique circulaire ou en anneau lorsqu’il est activé.</li>
     <li><strong>Position de la légende : </strong>spécifie la position de la légende par rapport au graphique. Les options disponibles sont Droite, Gauche, Haut et Bas. Utilisez la légende du côté droit dans le canal d’impression.</li>
     <li><strong>Rayon interne</strong> : disponible pour les graphiques en anneau pour indiquer le rayon (en pixels) du cercle intérieur dans le graphique.</li>
     <li><strong>Couleur de la ligne</strong> : disponible pour les graphiques linéaires, linéaires et à points, ou en aires pour spécifier la couleur de la ligne dans le graphique.</li>
     <li><strong>Couleur du point</strong> : disponible pour les graphiques à points et linéaires et à points, pour spécifier la couleur des points dans le graphique.<br /> </li>
     <li><strong>Couleur de zone</strong> : disponible pour les graphiques en aires pour spécifier la couleur pour la zone située sous la ligne dans le graphique.</li>
     <li><strong>Point de référence &gt; Type de liaison : </strong>disponible pour les graphiques a quadrants pour<strong> </strong>spécifier le type de liaison du point de référence. Utilisez le texte statique ou la propriété de l’objet de modèle de données pour définir la valeur du point de référence.</li>
     <li><strong>Point de référence &gt; Axe X : </strong>Disponible pour les graphiques quadrant si vous sélectionnez <span class="uicontrol">Statique</code> dans la liste déroulante Type de liaison pour spécifier la valeur de l’axe X pour le point de référence.</li>
     <li><strong>Point de référence &gt; Axe Y : </strong>Disponible pour les graphiques quadrant si vous sélectionnez <span class="uicontrol">Statique</code> dans la liste déroulante Type de liaison pour spécifier la valeur de l’axe Y du point de référence.</li>
     <li><strong>Point de référence &gt; Objet de modèle de données pour les séries : </strong>Disponible pour plusieurs séries de Quadrant si vous sélectionnez <span class="uicontrol">Objet de modèle de données</code> dans la liste déroulante Type de liaison . Définissez la propriété de l’objet de modèle de données du formulaire pour identifier la série pour le point de référence. </li>
     <li><strong>Point de référence &gt; Valeur d’objet de modèle de données pour les séries : </strong>Disponible pour plusieurs séries de Quadrant si vous sélectionnez <span class="uicontrol">Objet de modèle de données</code> dans la liste déroulante Type de liaison . Utilisez la propriété de l’objet de modèle de données du formulaire pour la série et la valeur définie dans ce champ afin d’identifier la série pour le point de référence.</li>
     <li><strong>Point de référence &gt; Objet de modèle de données pour le point de référence : </strong>Disponible pour les graphiques quadrant si vous sélectionnez <span class="uicontrol">Objet de modèle de données</code> dans la liste déroulante Type de liaison . Définissez une propriété d’objet de modèle de données de formulaire qui est apparentée aux propriétés tracées sur l’axe X et l’axe Y. En outre, pour les séries multiples, définissez une propriété d’objet de modèle de données qui est une entité enfant de la propriété d’objet de modèle de données définie pour la série.</li>
     <li><strong>Point de référence &gt; Valeur d’objet de modèle de données pour le point de référence : </strong>Disponible pour les graphiques quadrant si vous sélectionnez <span class="uicontrol">Objet de modèle de données</code> dans la liste déroulante Type de liaison . Utilisez la propriété d’objet de modèle de données de formulaire pour le point de référence et la valeur définie dans ce champ pour identifier le point de référence du graphique.<br /> <strong>Libellés du quadrant &gt; En haut à gauche :</strong> disponible pour les graphiques à quadrants afin de spécifier le nom du quadrant supérieur gauche.</li>
     <li><strong>Libellés du quadrant &gt; En haut à droite :</strong> disponible pour les graphiques à quadrants afin de spécifier le nom du quadrant supérieur droit.</li>
     <li><strong>Libellés du quadrant &gt; En bas à droite : </strong>disponible pour les graphiques à quadrants afin de spécifier le nom du quadrant inférieur droit.</li>
     <li><strong>Libellés du quadrant &gt; En bas à gauche : </strong>disponible pour les graphiques à quadrants afin de spécifier le nom du quadrant inférieur gauche.</li>
    </ul> </td>
   <td>Impression et web</td>
  </tr>
 </tbody>
</table>

## Utilisation des fonctions dans le graphique {#use-functions-in-chart}

Vous pouvez configurer un graphique pour qu’il utilise des fonctions statistiques afin de calculer des valeurs à partir des données source pour un graphique sur le graphique. L’application de fonctions dans un graphique vous permet de tracer des données qui ne sont pas directement fournies par le modèle de données de formulaire.

![Fonctions dans les graphiques](assets/functions_charts_new.png)

Outre les fonctions intégrées du composant de graphique, vous pouvez rédiger des [fonctions personnalisées](#customfunctionsweb) et les rendre disponibles pour qu’elles soient utilisées dans la configuration du graphique dans le canal web.

Les fonctions suivantes sont disponibles par défaut avec le composant de graphique :

**Moyenne** renvoie la moyenne des valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Somme** renvoie la somme de toutes les valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Maximum** renvoie le nombre maximal de valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Fréquence** renvoie le nombre de valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Plage** renvoie la différence entre le nombre maximal et minimal des valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Médian** renvoie la valeur qui sépare les valeurs les plus élevées et les valeurs les plus basses de la moitié sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Minimum** renvoie le nombre minimal de valeurs sur l’axe X ou Y pour une même valeur sur l’autre axe.

**Mode** renvoie la valeur avec le plus d’occurrences sur l’axe X ou Y pour une même valeur sur l’autre axe.

Pour plus d’informations, consultez la section [Exemple 2 : application des fonctions Somme et Fréquence dans un graphique linéaire](#applicationsumfrequency).

### Fonctions personnalisées dans le canal web {#customfunctionsweb}

Outre l’utilisation des fonctions par défaut dans les graphiques, vous pouvez créer des fonctions personnalisées dans JavaScript™ et les rendre disponibles dans la liste des fonctions du composant de graphique pour le canal web.

Une fonction prend un tableau ou des valeurs et un nom de catégorie comme entrées et renvoie une valeur. Par exemple :

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

Une fois que vous avez rédigé une fonction personnalisée, procédez comme suit pour la rendre disponible pour une utilisation dans la configuration du graphique :

1. Ajoutez la fonction personnalisée dans la bibliothèque cliente associée à la communication interactive appropriée. Pour plus d’informations, consultez les sections [Configurer l’action d’envoi](/help/forms/using/configuring-submit-actions.md) et [Utiliser les bibliothèques côté client](/help/sites-developing/clientlibs.md).

1. Pour afficher la fonction personnalisée dans le menu déroulant Fonction dans CRXDe Lite, créez un nœud `nt:unstructured` dans le dossier d’applications avec les propriétés suivantes :

   * Ajoutez la propriété `guideComponentType` avec une valeur définie sur `fd/af/reducer`. (mandatory)

   * Ajoutez la propriété `value` à un nom complet de la fonction JavaScript™ personnalisée. (obligatoire) et définissez sa valeur sur le nom de la fonction personnalisée, telle que Multiplier.
   * Ajoutez la propriété `jcr:description` avec la valeur que vous souhaitez afficher comme nom de la fonction personnalisée apparaissant dans le menu déroulant Fonction. Par exemple, **Multiplier**. 

   * Ajoutez la propriété `qtip` avec une valeur représentant une brève description de la fonction personnalisée. Elle s’affiche sous forme d’info-bulle lorsque le curseur est placé sur le nom de la **fonction** dans la liste déroulante.

1. Cliquez sur **Enregistrer tout** pour enregistrer la configuration.

La fonction peut désormais être utilisée dans le graphique.

## Exemple 1 : sortie du graphique sur papier et sur le web {#chartoutputprintweb}

Dans l’onglet Réglages de base, définissez le type de graphique, les propriétés de modèle de données du formulaire source contenant des données, les libellés à mapper sur l’axe X et l’axe Y du graphique et éventuellement la fonction statistique pour calculer les valeurs à tracer sur le graphique.

Examinons en détail les informations minimales requises de ces propriétés de base à l’aide d’un relevé de carte généré via une communication interactive. Supposons que vous souhaitiez générer un graphique afin de représenter le montant des différentes dépenses dans le relevé. Vous souhaitez utiliser différents types de graphiques pour l’impression et la sortie web de la communication interactive.

### Graphique à colonnes pour l’impression {#columnchartprint}

Pour ce faire, spécifiez les propriétés suivantes :

* **[!UICONTROL Nom]** : indiquez le nom du graphique.
* **[!UICONTROL Type de graphique]** : sélectionnez **Colonne** dans la liste déroulante.
* **[!UICONTROL Titre]** : indiquez le type de dépense à l’axe X et le montant de la transaction à l’axe Y.
* **[!UICONTROL Objets de modèle de données]** : sélectionnez les propriétés de l’objet de modèle de données afin de créer des liaisons de données pour l’axe X (Type de dépense) et l’axe Y (Montant de la transaction).

![Graphique à colonnes dans le canal d’impression d’une communication interactive](assets/sample_chart_print_column_new.png)

Graphique à colonnes dans le canal d’impression d’une communication interactive

### Graphique en anneau pour le Web {#donutchartweb}

Pour ce faire, spécifiez les propriétés suivantes :

* **[!UICONTROL Nom]** : indiquez le nom du graphique.
* **[!UICONTROL Type de graphique]** : sélectionnez **[!UICONTROL Anneau]** dans la liste déroulante.
* **[!UICONTROL Objets de modèle de données]** : sélectionnez les propriétés des objets de modèle de données pour créer des liaisons de données pour l’axe X (Type de dépense) et l’axe Y (Montant de la transaction).
* **[!UICONTROL Rayon interne]** : définissez la valeur du rayon interne sur 150 pour indiquer le rayon (en pixels) du cercle intérieur dans le graphique.
* **[!UICONTROL Info-bulle]** : utilisez le format par défaut ${x}(${y}) pour afficher l’info-bulle. L’info-bulle s’affiche comme suit : type de dépense (montant de la transaction). Exemple : « Debit for Bitcoin(10000) ».

![Graphique en anneau dans le canal web d’une communication interactive](assets/sample_chart_web_new.png)

Graphique en anneau dans le canal web d’une communication interactive

## Exemple 2 : application des fonctions Somme et Fréquence dans un graphique en ligne {#applicationsumfrequency}

L’application de fonctions dans un graphique vous permet de tracer des données qui ne sont pas directement fournies par le modèle de données de formulaire. Ici, nous utilisons un exemple de relevé de carte de crédit pour comprendre comment les fonctions Somme et Fréquence peuvent être appliquées au graphique.

![Graphique linéaire sans fonction comportant deux transactions « Debit for AirBnB »](assets/line_chart_web_new.png)

Graphique linéaire sans fonction comportant deux transactions « Debit for AirBnB »

### Sum, fonction {#sum-function}

Vous pouvez appliquer la fonction sum pour additionner les valeurs de plusieurs instances d’une même propriété de données et les afficher une seule fois. Par exemple, dans le graphique suivant, la fonction Somme s’applique à l’axe Y et additionne le montant des deux transactions « Debit for AirBnB » (2050 et 1050) pour afficher une seule transaction (3100).

La fonction Somme peut rendre le graphique plus utile si vous souhaitez assembler et afficher la somme de plusieurs instances de la même propriété Data.

![Graphique linéaire avec fonction Somme](assets/line_chart_web_sum_new.png)

### Fonction Fréquence {#frequency-function}

La fonction Fréquence renvoie le nombre de valeurs sur l’axe Y pour une même valeur sur l’autre axe. Grâce à l’utilisation de la fonction Fréquence sur l’axe Y (Montant de la transaction), le graphique affiche deux occurrences de transactions « Debit for AirBnB » et une occurrence du reste des types de transactions.

![Graphique linéaire avec fonction Fréquence](assets/line_chart_web_functions_frequency_new.png)

## Exemple 3 : graphique à quadrants multi-séries dans le Web {#example-multi-series-quadrant-chart-in-web}

Le graphique représente le montant des transactions effectuées au cours dʼune période donnée. Le graphique à quadrants permet de diviser le graphique en quatre sections identifiables. Le graphique utilise un point de référence statique pour l’axe X et l’axe Y. Utilisez la fonctionnalité de séries multiples pour séparer les données en fonction du nom de la banque.

Pour ce faire, spécifiez les propriétés suivantes :

* **Nom :** indiquez le nom du graphique.
* **Type de graphique :** sélectionnez **Quadrant** dans la liste déroulante.

* Cochez la case **Séries multiples**.
* **Objet de modèle de données**: spécifiez la propriété d’objet de modèle de données de la série. La propriété de l’objet de modèle de données pour le nom de la banque est un parent des propriétés de l’objet de modèle de données mappées sur l’axe X et l’axe Y.
* **Objets de modèle de données :** sélectionnez les propriétés de l’objet de modèle de données afin de créer des liaisons de données pour l’axe X (Date de transaction) et l’axe Y (Montant de transaction).
* Dans la section **Point de référence**, sélectionnez **Statique** comme type de liaison.

* Spécifiez les valeurs des points de référence de l’axe X et de l’axe Y.
* Indiquez les libellés des quadrants supérieur gauche, supérieur droit, inférieur droit et inférieur gauche.
* Cochez la case **Afficher les légendes** pour afficher les codes couleur des noms de banque.

![Graphiques à quadrants](assets/charts_quadrant_example_new.png)
