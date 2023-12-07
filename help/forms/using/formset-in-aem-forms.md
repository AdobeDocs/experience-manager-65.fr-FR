---
title: Jeu de formulaires dans AEM Forms
description: Cet article présente le jeu de formulaires et explique comment créer des jeux de formulaires en assemblant des formulaires HTML5. Cet article explique également comment préremplir des données XML dans un jeu de formulaires et comment utiliser des jeux de formulaires dans Process Management.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 40%

---

# Jeu de formulaires dans AEM Forms{#form-set-in-aem-forms}

## Présentation {#overview}

Vos clients doivent souvent envoyer plusieurs formulaires pour solliciter un service ou un avantage. Cela implique de trouver tous les formulaires pertinents et de les remplir, les envoyer et les suivre séparément. En outre, ils sont nécessaires pour remplir des détails communs plusieurs fois dans les formulaires. L’ensemble du processus devient encombrant et sujet aux erreurs s’il implique un grand nombre de formulaires. La fonction de jeu de formulaires d’AEM Forms peut aider à simplifier l’expérience de l’utilisateur dans de tels scénarios.

Un jeu de formulaires est un ensemble de formulaires HTML5 regroupés et présentés aux utilisateurs finaux sous la forme d’un jeu unique de formulaires. Lorsque les utilisateurs finaux commencent à remplir un jeu de formulaires, ils passent facilement d’un formulaire à un autre. A la fin, ils peuvent envoyer tous les formulaires en un seul clic.

AEM Forms fournit aux auteurs de formulaires une interface utilisateur intuitive pour créer, configurer et gérer des jeux de formulaires. En tant qu’auteur, vous pouvez classer les formulaires dans une séquence particulière que les utilisateurs finaux doivent suivre. Vous pouvez également appliquer des conditions ou des expressions d’éligibilité sur des formulaires individuels pour contrôler leur visibilité en fonction des entrées de l’utilisateur. Par exemple, vous pouvez configurer le formulaire de détails du conjoint pour qu’il s’affiche uniquement lorsque l’état civil indique Marié(e).

En outre, vous pouvez configurer des champs communs dans différents formulaires pour partager des liaisons de données communes. Lorsque des liaisons de données appropriées sont en place, les utilisateurs finaux doivent remplir les informations communes une seule fois, qui sont automatiquement renseignées dans les formulaires suivants.

Les jeux de formulaires sont également pris en charge dans l’application AEM Forms, ce qui permet à vos collaborateurs sur le terrain de prendre un jeu de formulaires hors ligne, de rendre visite aux clients, d’entrer des données et de se synchroniser ultérieurement avec le serveur AEM Forms pour envoyer des données de formulaires aux processus d’entreprise.

## Création et gestion de jeux de formulaires {#creating-and-managing-form-set}

Vous pouvez associer plusieurs XDP ou modèles de formulaire, créés via Designer, dans un jeu de formulaires. Des jeux de formulaires peuvent ensuite être utilisés pour rendre de manière sélective les XDP en fonction des valeurs saisies par les utilisateurs dans les formulaires initiaux et leurs profils.

Utilisez [l’interface utilisateur d’AEM Forms](../../forms/using/introduction-managing-forms.md) pour gérer tous vos formulaires, vos jeux de formulaires et vos ressources associés.

### Création d’un jeu de formulaires {#create-a-form-set}

Pour créer un jeu de formulaires, procédez comme suit :

1. Sélectionnez Forms > Forms et documents.
1. Sélectionnez Créer > Jeu de formulaires.

1. Sur la page Ajouter des propriétés , ajoutez les détails suivants et cliquez sur Suivant.

   * Titre : indique le titre du document. Le titre vous permet d’identifier le jeu de formulaires dans l’interface utilisateur d’AEM Forms.
   * Description : indique des informations détaillées relatives au document.
   * Balises : indique les balises pour individualiser le jeu de formulaires. Les balises aident à rechercher le jeu de formulaires. Pour créer des balises, saisissez les nouveaux noms de balise dans la boîte de dialogue Balises.
   * URL d’envoi : indique l’URL où les données envoyées sont publiées dans le cas d’un rendu autonome d’un jeu de formulaires (cas d’utilisation de l’application Non-AEM Forms). Les données sont envoyées vers ce point de terminaison en tant que données de formulaire multiples avec le paramètre de requête suivant :
   * dataXML : ce paramètre contient une représentation XML des données du jeu de formulaires envoyé. Si tous les formulaires du jeu utilisent un schéma commun, le code XML est généré selon ce schéma. Sinon, la balise XML racine contient une balise enfant pour chaque formulaire rempli du jeu de formulaires qui contient des données pour les pièces jointes du formulaire.
   * formsetPath : chemin du jeu de formulaires dans CRXDE, qui a été envoyé.
   * Profil de rendu de HTML : vous pouvez configurer certaines options telles que les champs flottants, les pièces jointes et la prise en charge de brouillon (pour le rendu d’un jeu de formulaires autonome) pour personnaliser l’aspect, le comportement et les interactions du jeu de formulaires. Vous pouvez personnaliser ou étendre le profil existant pour modifier les paramètres de profil de HTML de formulaire.

   ![Jeu de formulaires : ajouter les propriétés](assets/createformset1.png)

1. L’écran Sélectionner le(s) formulaire(s) affiche les formulaires XDP ou les fichiers XDP disponibles. Recherchez et sélectionnez les formulaires à inclure dans le jeu de formulaires, puis cliquez sur Ajouter au jeu de formulaires. Si nécessaire, recherchez à nouveau des formulaires à ajouter. Après avoir ajouté tous les formulaires au jeu de formulaires, cliquez sur Suivant.

   >[!NOTE]
   >
   >Assurez-vous que les noms des champs dans les formulaires XDP ne contiennent pas de points. Dans le cas contraire, tous les scripts contenant des points essayant de résoudre les champs ne seront pas en mesure de le faire.

1. Dans la page Configurer le(s) formulaire(s), vous pouvez effectuer les opérations suivantes : 

   * Ordre des formulaires : faites glisser les formulaires pour les réorganiser. L’ordre des formulaires définit l’ordre dans lequel les formulaires se présentent à l’utilisateur final dans l’application AEM Forms et le rendu autonome.
   * Identifiant de formulaire : indique une identité unique pour les formulaires à utiliser dans les expressions d’éligibilité.
   * Racine des données : pour chaque formulaire du jeu, l’auteur peut configurer XPATH où les données d’un formulaire donné sont situées dans les données XML envoyées. Par défaut, la valeur est /. Si tous les formulaires du jeu sont liés à un schéma et partagent le même schéma XML, vous pouvez modifier cette valeur. Il est recommandé que chaque champ du formulaire ait la liaison de données appropriée spécifiée dans XDP. Si deux champs de deux formulaires différents partagent la liaison de données commune, le champ du deuxième formulaire affiche les valeurs préremplies du premier formulaire. Ne liez pas deux sous-formulaires avec le même contenu interne au même nœud XML. Pour plus d’informations sur la structure XML du jeu de formulaires, voir [Préremplissage XML du jeu de formulaires](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * Expression d’éligibilité : spécifie une expression JavaScript qui évalue une valeur booléenne et indique si un formulaire du jeu de formulaires est éligible au remplissage. Si la valeur est false, l’utilisateur n’est pas invité ou le formulaire à remplir n’est même pas affiché. En règle générale, l’expression est basée sur les valeurs des champs qui sont collectées avant ce formulaire. Les expressions contiennent également des appels à la valeur de fs.valueOf de l’API du jeu de formulaires pour extraire les valeurs renseignées par l’utilisateur dans un champ de formulaire du jeu de formulaires :

   *fs.valueOf(&lt;Form Identifier>, &lt;fieldSom expression>) > &lt;value>*

   Par exemple, si vous avez deux formulaires dans le jeu de formulaires : frais d’exploitation et frais de voyage, vous pouvez ajouter un fragment de code JavaScript dans le champ Expression d’éligibilité pour ces deux formulaires afin de vérifier la saisie de l’utilisateur pour le type de dépenses dans un formulaire. Si l’utilisateur sélectionne Frais d’exploitation, le formulaire Frais d’exploitation est présenté à l’utilisateur final. Si l’utilisateur sélectionne des frais de transport, un autre formulaire est présenté à l’utilisateur final. Pour plus d’informations, voir Expression d’éligibilité.

   En outre, l’utilisateur peut aussi choisir de supprimer un formulaire du jeu de formulaires à l’aide de l’icône Supprimer dans le coin droit de chaque ligne, ou ajouter un autre jeu de formulaires à l’aide de l’icône « **+** » dans la barre d’outils. L’icône « **+** » redirige l’utilisateur vers l’étape précédente dans l’assistant, qui était « Sélectionner le(s) formulaire(s) ». Les sélections existantes sont conservées et toute sélection supplémentaire doit être ajoutée au jeu de formulaires à l’aide de l’icône Ajouter au jeu de formulaires de cette page.

   ![Jeu de formulaires : Configurer le(s) formulaire(s)](assets/createformset2.png)

   >[!NOTE]
   >
   >Tous les formulaires utilisés dans le jeu de formulaires sont gérés par l’interface utilisateur d’AEM Forms.

### Gestion d’un jeu de formulaires {#managing-a-form-set}

Une fois qu’un jeu de formulaires est créé, vous pouvez effectuer les actions suivantes sur ce jeu de formulaires :

* Cliquer une fois : lorsque le jeu de formulaires est créé et répertorié sur la page principale des actifs, vous pouvez cliquer une seule fois sur le jeu de formulaires pour l’afficher. Un jeu de formulaires s’ouvre et affiche tous les modèles de formulaire (XDP) dans ce jeu de formulaires.
* Modifier : en cliquant sur « Modifier » après la sélection d’un jeu de formulaires, l’écran « Configurer le(s) formulaire(s) » illustré ci-dessus dans « Procédure de création d’un jeu de formulaires » s’ouvre. Vous pouvez exécuter toutes les fonctionnalités décrites à ce point.
* Copier + Coller : permet de copier l’ensemble du jeu de formulaires d’un emplacement et de le coller au même emplacement ou dossier, ou ailleurs.
* Télécharger : vous pouvez télécharger le jeu de formulaires avec toutes ses dépendances.
* Lancer/Gérer la révision : une fois que le jeu de formulaires est créé, vous pouvez définir sa révision en cliquant sur Lancer la révision. Une fois la révision lancée pour un jeu de formulaires, l’option Gérer la révision s’affiche pour l’utilisateur. Dans l’écran Gérer la révision, vous pouvez mettre à jour/mettre fin à la révision. Pour les révisions que vous avez ajoutées, vous pouvez vérifier la révision et ajouter des commentaires, si nécessaire.
* Supprimer : supprime le jeu de formulaires complet. Les formulaires du jeu supprimé restent dans le référentiel.
* Publier/Annuler la publication : cette action publie/annule la publication du jeu de formulaires avec tous les formulaires qu’il contient et les actifs associés à ces formulaires.
* Aperçu : l’aperçu offre deux options : Aperçu par HTML (sans données) et Aperçu personnalisé avec des exemples de données.
* Afficher/modifier les propriétés : vous pouvez afficher/modifier les propriétés de métadonnées d’un jeu de formulaires sélectionné.

![createformset3](assets/createformset3.png)

### Modifier un jeu de formulaires {#edit-a-form-set}

Pour modifier un jeu de formulaires, procédez comme suit :

1. Sélectionnez Forms > Forms et documents.
1. Localisez le jeu de formulaires à modifier. Pointez le curseur dessus et sélectionnez Modifier (![icône Modifier](assets/editicon.png)).
1. Dans la page Configurer le(s) formulaire(s), vous pouvez modifier les éléments suivants : 

   * L’ordre des formulaires
   * Identifiant de formulaire
   * Racine des données
   * Expression d’éligibilité

   Vous pouvez également cliquer sur l’icône Supprimer correspondante pour supprimer le formulaire du jeu de formulaires.

## Jeu de formulaires dans Process Management {#form-set-in-process-management}

Une fois que vous avez créé un jeu de formulaires à l’aide de l’interface utilisateur de gestion d’AEM Forms, vous pouvez utiliser le jeu de formulaires dans une activité Point de départ ou Affectation de tâches à l’aide de Workbench.

### Utilisation du jeu de formulaires dans Tâche ou Point de départ {#using-form-set-in-task-or-start-point}

1. Lors de la conception d’un processus, sous la section Présentation et Données d’Assigner Tâche/Point de départ, sélectionnez **Utilisation d’un actif CRX**. Le navigateur des ressources CRX s’affiche. 

   ![Création d’un processus : utiliser un actif CRX](assets/formsetinprocessmgmt1.png)

1. Sélectionnez un jeu de formulaires afin de le filtrer dans le référentiel AEM (CRX).

   ![Création d’un processus : sélectionnez la boîte de dialogue Sélection de l’actif de formulaire](assets/formsetinprocessmgmt2.png)

1. Sélectionnez un jeu de formulaires, puis cliquez sur OK.

## Expressions d’éligibilité {#eligibility-expressions}

Les expressions d’éligibilité dans un jeu de formulaires sont utilisées pour définir et contrôler dynamiquement les formulaires affichés à l’utilisateur. Par exemple, pour afficher un formulaire donné uniquement si l’utilisateur appartient à une tranche d’âge particulière. Spécifiez et modifiez une expression d’éligibilité à l’aide de Forms Manager.

Une expression d’éligibilité peut être n’importe quelle instruction JavaScript valide renvoyant une valeur booléenne. La dernière instruction du fragment de code JavaScript est traitée comme une valeur booléenne qui détermine l’éligibilité du formulaire en fonction du traitement effectué dans le reste (lignes précédentes) du fragment de code JavaScript. Si la valeur de l’expression est vraie, le formulaire est éligible pour être affiché à l’utilisateur. Ces formulaires sont appelés formulaires éligibles.

>[!NOTE]
>
>L’expression d’éligibilité du premier formulaire dans le jeu de formulaires n’est pas exécutée. Le premier formulaire est toujours affiché, quelle que soit son expression d&#39;éligibilité.

Outre les fonctions JavaScript standard, le jeu de formulaires expose également la valeur fs.valueOf de l’API qui permet d’accéder à la valeur d’un champ d’un formulaire dans un jeu de formulaires. Utilisez cette API pour accéder à la valeur d’un champ de formulaire dans un jeu de formulaires. La syntaxe de l’API est fs.valueOf (formUid, fieldSOM), où :

* formUid (chaîne) : identifiant univoque d’un formulaire dans le jeu de formulaires. Vous pouvez le définir lors de la création du jeu de formulaires dans l’interface utilisateur de Forms Manager. Par défaut, il s’agit du nom du formulaire.
* fieldSOM (string): expression SOM du champ dans le formulaire spécifié par formUid. L’expression SOM ou expression de modèle d’objet de script est utilisée pour référencer des valeurs, des propriétés et des méthodes dans un modèle d’objet de document (DOM) particulier. Vous pouvez l’afficher dans le concepteur de formulaire sous l’onglet Scripts lorsque le champ est sélectionné.

>[!NOTE]
>
>Les paramètres formUid et fieldSOM doivent être littéraux de chaîne.

### Exemples {#examples}

Utilisation valide de l’API :

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

Utilisation non valide de l’API :

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## Préremplissage XML du jeu de formulaires {#prefill-xml-for-form-set}

Un jeu de formulaires est un ensemble de formulaires HTML5 multiples dont les schémas sont communs ou différents. Le jeu de formulaires prend en charge le préremplissage des champs du formulaire à l’aide d’un fichier XML. Vous pouvez associer un fichier XML à un jeu de formulaires. Ainsi, lorsque vous ouvrez un formulaire dans le jeu, certains champs du formulaire sont pré-remplis.

Le fichier XML de pré-remplissage est spécifié à l’aide du paramètre dataRef de l’URL du jeu de formulaires. Le paramètre dataRef indique le chemin d’accès absolu du fichier XML de données qui est fusionné avec le jeu de formulaires.

Par exemple, vous avez trois formulaires (formulaire1, formulaire2 et formulaire3), dans le jeu de formulaires avec la structure suivante :

form1

champ champformulaire1 

formulaire2

champ champformulaire2 

formulaire3

champ champformulaire3 

Chaque formulaire comporte un champ nommé communément &quot;champ&quot; et un champ nommé de manière unique &quot;formfield&quot;.

Vous pouvez préremplir ce jeu de formulaires à l’aide d’un XML dont la structure est la suivante :

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>La balise racine XML peut avoir n’importe quel nom, mais les balises d’élément correspondant aux champs doivent avoir le même nom que le champ. La hiérarchie du XML doit imiter la hiérarchie du formulaire, ce qui signifie que le XML doit avoir des balises correspondantes pour envelopper des sous-formulaires. 

L’extrait de code XML ci-dessus indique que le code XML de préremplissage du jeu de formulaires est une union des extraits de code XML prérempli des formulaires individuels. Si certains champs dans les différents formulaires présentent une hiérarchie de données/un schéma similaires entre eux, les champs sont préremplis avec les mêmes valeurs. Dans cet exemple, chacun des trois formulaires est prérempli avec la même valeur pour le champ commun « champ ». Il s’agit d’un moyen simple de transférer des données d’un formulaire à l’autre. Pour ce faire, vous pouvez également lier les champs à la même référence de schéma ou de données. Si vous souhaitez séparer les données du jeu de formulaires en fonction du schéma des formulaires. Pour ce faire, spécifiez l’attribut &quot;racine de données&quot; du formulaire lors de la création du jeu de formulaires (la valeur par défaut est &quot;/&quot;, qui mappe sur la balise racine du jeu de formulaires).

Dans l’exemple précédent, si vous spécifiez les racines de données : &quot;/form1&quot;, &quot;/form2&quot; et &quot;/form3&quot; respectivement pour les trois formulaires, vous devez utiliser un code XML de préremplissage de la structure suivante :

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

Dans un ensemble de formulaires, le code XML a défini un schéma XML avec la syntaxe suivante :

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>S’il existe deux formulaires dont les racines de données se chevauchent ou si la hiérarchie des éléments d’un formulaire chevauche la hiérarchie des racines de données d’un autre formulaire, dans le fichier xml de préremplissage, les valeurs des éléments chevauchés sont fusionnées. Le code XML d’envoi a une structure similaire à celle du code XML de préremplissage, mais le code XML d’envoi comporte plus de balises wrapper et certaines balises de données contextuelles de jeu de formulaires sont ajoutées à la fin.

### Description des éléments XML de préremplissage {#prefill-xml-elements-description}

Règles de syntaxe pour la création d’un fichier XML de préremplissage :

* éléments parents : élément(s) pouvant être son parent, où la valeur null indique que l’élément peut être à la racine du XML.
* cardinalité : représente le nombre de fois où l’élément peut être utilisé dans son élément parent.
* submitXML : indique si l’élément est toujours présent (P) ou optionnel (O) dans le XML envoyé.
* prefillXML : indique si l’élément est requis (R) ou optionnel (O) dans le XML prérempli.
* enfants : indique les éléments qui peuvent être ses enfants.

### FORMSET {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

Elément racine du XML du jeu de formulaires. Il est conseillé de ne pas utiliser ce mot comme nom de rootSubform d’un formulaire dans le jeu de formulaires.

### FS_DATA {#fs-data}

`parent elements:`

`formset`

Cardinalité : [1]

submitXML : P

prefillXML : O

`children: xdp:xdp/rootElement`

La sous-arborescence indique les données des formulaires dans le jeu de formulaires. L’élément est facultatif dans le code XML de préremplissage uniquement si l’élément du jeu de formulaires n’est pas présent

### XDP :XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

Cette balise indique le début du XML du formulaire HTML5. Il est ajouté dans le XML envoyé s’il est présent dans le XML prérempli ou s’il n’y a pas de XML prérempli. Cette balise peut être supprimée du code XML de préremplissage.

### XFA : DATASETS {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA:DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

Le rootElement du nom est simplement un espace réservé. Le nom réel est sélectionné dans les formulaires utilisés dans le jeu de formulaires. La sous-arborescence qui débute avec rootElement contient les données des champs et des sous-formulaires à l’intérieur des formulaires dans l’ensemble de formulaires. Plusieurs facteurs déterminent la structure de l’élément racine et de ses enfants.

Dans le code XML de préremplissage, cette balise est facultative, mais si elle est manquante, l’intégralité du code XML est ignorée.

NOM DE LA BALISE D’ÉLÉMENT RACINE

S’il existe un élément racine dans le XML prérempli, le nom de cet élément est également utilisé dans le XML envoyé. S’il n’existe aucun XML prérempli, le nom de l’élément rootElement est le nom du sous-formulaire racine du premier formulaire dans le jeu de formulaires dont la propriété dataRoot est définie sur « / ». S’il n’existe aucun formulaire de ce type, le nom rootElement est **fs_dummy_root**, qui est un mot-clé réservé.

## Jeu de formulaires dans l’application AEM Forms {#formset-in-workspace-app}

L’application AEM Forms permet aux agents de terrain de synchroniser leurs appareils mobiles avec un serveur AEM Forms et de travailler sur leurs tâches. L’application est exécutée même lorsque l’appareil est hors ligne et que les données y sont enregistrées en local. Grâce aux fonctions d’annotation, telles que les photographies, les agents de terrain peuvent fournir des informations précises à intégrer aux processus d’entreprise.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## Limites connues : modèles non entièrement pris en charge dans le jeu de formulaires {#known-limitations-patterns-not-fully-supported-in-form-set}

Les modèles de données suivants ne sont pas entièrement pris en charge dans le jeu de formulaires :

<table>
 <tbody>
  <tr>
   <td><strong>Modèle qui n’est pas intégralement pris en charge dans le jeu de formulaires</strong></td>
   <td><strong>Exemple</strong></td>
  </tr>
  <tr>
   <td>Discordance entre la taille d’entrée et la taille du modèle</td>
   <td><p>Lorsque pattern= num{z,zzz}</p> <p>Et input=</p> <p>12 345 ou</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>Modèles de clause d’image avec crochets « (" ") »</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>Formats de données multiples</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>Modèles courts </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.percent{}, ou</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
