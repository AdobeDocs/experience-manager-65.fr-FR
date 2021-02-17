---
title: Utilisation de bibliothèques côté client
seo-title: Utilisation de bibliothèques côté client
description: AEM fournit des dossiers de bibliothèques côté client qui vous permettent de stocker le code côté client dans le référentiel, de le classer dans des catégories, et de définir quand et comment chaque catégorie de code doit être diffusée au client.
seo-description: AEM fournit des dossiers de bibliothèques côté client qui vous permettent de stocker le code côté client dans le référentiel, de le classer dans des catégories, et de définir quand et comment chaque catégorie de code doit être diffusée au client.
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 5d33b48000cf607eb77c626ec539280cadab378e
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 78%

---


# Utilisation de bibliothèques côté client{#using-client-side-libraries}

Les sites web modernes sont très dépendants du traitement côté client effectué par du code JavaScript et CSS complexe. Organiser et optimiser la diffusion de ce code est une opération qui peut se révéler complexe.

Pour résoudre ce problème, AEM fournit des **dossiers de bibliothèques côté client** qui permettent de stocker le code côté client dans le référentiel, de le classer dans des catégories, et de définir quand et comment chaque catégorie de code doit être diffusée au client. Le système de bibliothèque côté client se charge alors de la génération des liens appropriés dans la page web finale pour charger le code correct.

## Fonctionnement des bibliothèques côté client dans AEM {#how-client-side-libraries-work-in-aem}

La méthode standard pour inclure une bibliothèque côté client (c’est-à-dire un fichier JS ou CSS) dans le code HTML d’une page consiste simplement à inclure une balise `<script>` ou `<link>` dans le JSP pour cette page, contenant le chemin d’accès au fichier en question. Par exemple,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Bien que cette méthode fonctionne dans AEM, elle peut entraîner des problèmes lorsque les pages et leurs composants constitutifs deviennent complexes. Dans ce cas, il y a un risque que plusieurs copies de la même bibliothèque JS soient incluses dans la sortie HTML finale. Pour éviter cela et permettre une organisation logique des bibliothèques côté client, AEM utilise des **dossiers de bibliothèques côté client**.

Un dossier de bibliothèques côté client est un nœud de référentiel de type `cq:ClientLibraryFolder`. Sa définition en [notation CND](https://jackrabbit.apache.org/node-type-notation.html) est

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Par défaut, les noeuds `cq:ClientLibraryFolder` peuvent être placés n’importe où dans les sous-arborescences `/apps`, `/libs` et `/etc` du référentiel (ces valeurs par défaut et d’autres paramètres peuvent être contrôlés par le biais du **Gestionnaire de bibliothèque HTML Granite** de l’Adobe [Console système](https://localhost:4502/system/console/configMgr)).

Chaque dossier `cq:ClientLibraryFolder` est rempli avec un jeu de fichiers JS et/ou CSS, ainsi que quelques fichiers annexes (voir ci-dessous). Les propriétés de `cq:ClientLibraryFolder` sont configurées comme suit :

* `categories` : identifie les catégories dans lesquelles se trouve le jeu de fichiers JS et/ou CSS de ce dossier `cq:ClientLibraryFolder`. La propriété `categories` comportant plusieurs valeurs, elle permet à un dossier de bibliothèques d’appartenir à plusieurs catégories (voir ci-dessous pour savoir en quoi cela peut se révéler utile).

* `dependencies` : il s’agit d’une liste d’autres catégories de bibliothèques clientes dont dépend ce dossier de catégories. Par exemple, étant donné deux nœuds `cq:ClientLibraryFolder`, `F` et `G`, si un fichier du nœud `F` nécessite un autre fichier du nœud `G` pour fonctionner correctement, au moins l’une des propriétés `categories` de `G` doit figurer parmi les propriétés `dependencies` de `F`.

* `embed` : utilisé pour incorporer du code d’autres bibliothèques. Si le noeud F incorpore les noeuds G et H, le code HTML résultant sera une concentration de contenu des noeuds G et H.
* `allowProxy`: Si une bibliothèque cliente se trouve sous  `/apps`, cette propriété lui permet d’y accéder par le biais de la servlet proxy. Voir [Recherche d’un dossier de bibliothèques clientes et utilisation du servlet des bibliothèques clientes du proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) ci-dessous.

## Référencement des bibliothèques côté client {#referencing-client-side-libraries}

Le langage HTL étant la technologie recommandée pour développer des sites AEM, il doit être utilisé pour inclure des bibliothèques côté client dans AEM. Cependant, il est également possible d’utiliser JSP à cette fin.

### Utilisation de HTL  {#using-htl}

Dans HTL, les bibliothèques clientes sont chargées à l’aide d’un modèle d’assistance fourni par AEM, accessible via [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Trois modèles sont disponibles dans ce fichier, qui peut être appelé via [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call) :

* **css**  : charge uniquement les fichiers CSS des bibliothèques clientes référencées.
* **js**  - Charge uniquement les fichiers JavaScript des bibliothèques clientes référencées.
* **all** - Charge tous les fichiers des bibliothèques clientes référencées (CSS et JavaScript).

Chaque modèle d’assistance exige une option `categories` pour référencer les bibliothèques clientes souhaitées. Cette option peut être un tableau de valeurs de chaîne ou une chaîne contenant une liste de valeurs séparées par des virgules.

Pour plus d’informations et d’exemples d’utilisation, voir le document [Prise en main de la langue du modèle HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Utilisation de JSP {#using-jsp}

Ajoutez une balise `ui:includeClientLib` à votre code JSP pour ajouter un lien vers les bibliothèques clientes dans la page HTML générée. Pour référencer les bibliothèques, vous utilisez la valeur de la propriété `categories` du noeud `ui:includeClientLib`.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Par exemple, le noeud `/etc/clientlibs/foundation/jquery` est de type `cq:ClientLibraryFolder` avec une propriété de catégorie de valeur `cq.jquery`. Le code suivant dans un fichier JSP référence les bibliothèques :

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La page HTML générée contient le code suivant :

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Pour obtenir plus d’informations, y compris des attributs de filtrage des bibliothèques JS, CSS et thématiques, voir [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, qui par le passé était généralement utilisé pour inclure les bibliothèques clientes, a été abandonné depuis AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) devrait être utilisé à la place comme indiqué ci-dessus.

## Création de dossiers de bibliothèques clientes {#creating-client-library-folders}

Créez un nœud `cq:ClientLibraryFolder` pour définir des bibliothèques JS (JavaScript) et CSS (Cascading Style Sheet), et les mettre à la disposition des pages HTML. Utilisez la propriété `categories` du nœud pour identifier les catégories de bibliothèque auxquelles il appartient.

Le nœud contient un ou plusieurs fichiers sources qui, à l’exécution, sont fusionnés en un seul fichier JS et/ou CSS. Le nom du fichier généré est le nom de nœud avec l’extension `.js` ou `.css`. Par exemple, le nœud de bibliothèque nommé `cq.jquery` donne le nom de fichier généré `cq.jquery.js` ou `cq.jquery.css`.

Les dossiers de bibliothèques clientes contiennent les éléments suivants :

* Les fichiers sources JS et/ou CSS pour fusionner.
* Les ressources qui prennent en charge les styles CSS, tels que les fichiers images.

   **Remarque** : Vous pouvez utiliser des sous-dossiers pour organiser les fichiers sources.
* Un fichier `js.txt` et/ou un fichier `css.txt` qui identifie les fichiers sources à fusionner dans les fichiers JS et/ou CSS générés.

![clientlibarch](assets/clientlibarch.png)

Pour plus d’informations sur les exigences spécifiques aux bibliothèques clientes pour les widgets, voir [Utilisation et extension des widgets](/help/sites-developing/widgets.md).

Le client web doit être autorisé à accéder au nœud `cq:ClientLibraryFolder`. Vous pouvez également exposer les bibliothèques à partir de zones sécurisées du référentiel (voir la section « Incorporation de code d’autres bibliothèques »·ci-dessous).

### Remplacement de bibliothèques dans /lib  {#overriding-libraries-in-lib}

Les dossiers de bibliothèque client situés sous `/apps` ont priorité sur les dossiers portant le même nom qui se trouvent également dans `/libs`. Par exemple, `/apps/cq/ui/widgets` a la priorité sur `/libs/cq/ui/widgets`. Lorsque ces bibliothèques appartiennent à la même catégorie, la bibliothèque `/apps` ci-dessous est utilisée.

### Recherche d’un dossier de bibliothèques clientes et utilisation du servlet des bibliothèques clientes du proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Dans les versions précédentes, les dossiers de bibliothèque client se trouvaient sous `/etc/clientlibs` dans le référentiel. Cela est toujours pris en charge. Cependant, il est recommandé de placer désormais les bibliothèques clientes sous `/apps`. Il s’agit de localiser les bibliothèques clientes à proximité des autres scripts, qui se trouvent généralement sous `/apps` et `/libs`.

>[!NOTE]
>
>Les ressources statiques situées sous le dossier de bibliothèque client doivent se trouver dans un dossier appelé *resources*. Si vous ne disposez pas des ressources statiques, telles que les images, sous le dossier *resources*, il ne peut pas être référencé sur une instance de publication. En voici un exemple : https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Afin de mieux isoler le code du contenu et de la configuration, il est recommandé de localiser les bibliothèques clientes sous `/apps` et de les exposer via `/etc.clientlibs` en exploitant la propriété `allowProxy`.

Pour que les bibliothèques clientes situées sous `/apps` soient accessibles, un servlet proxy est utilisé. Les listes de contrôle d’accès (ACL) sont toujours appliquées sur le dossier de bibliothèques clientes, mais le servlet permet la lecture du contenu via `/etc.clientlibs/` si la propriété `allowProxy` est définie sur `true`.

Une ressource statique n’est accessible que par le biais du proxy, si elle réside sous une ressource située dans le dossier des bibliothèques clientes.

Par exemple :

* Vous avez une bibliothèque cliente dans `/apps/myproject/clientlibs/foo`.
* Vous avez une image statique dans `/apps/myprojects/clientlibs/foo/resources/icon.png`.

Ensuite, vous définissez la propriété `allowProxy` sur `foo` sur true.

* Vous pouvez ensuite demander `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Vous pouvez ensuite référencer l’image par `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Lors de l’utilisation de bibliothèques clientes par proxy, la configuration du répartiteur AEM peut nécessiter une mise à jour pour s’assurer que les URI avec les clientlibs d’extension sont autorisés.

>[!CAUTION]
>
>Adobe recommande de localiser les bibliothèques clientes sous `/apps` et de les rendre disponibles à l’aide de la servlet proxy. Cependant, gardez à l’esprit que les meilleures pratiques exigent toujours que les sites publics n’incluent jamais rien qui soit directement servi par un chemin `/apps` ou `/libs`.

### Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

1. Ouvrez le CRXDE Lite dans un navigateur Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Sélectionnez le dossier dans lequel vous souhaitez placer le dossier de bibliothèques clientes et cliquez ensuite sur **Créer > Créer un nœud**.
1. Attribuez un nom au fichier de bibliothèque, puis sélectionnez `cq:ClientLibraryFolder` dans la liste Type. Cliquez sur **OK**, puis sur **Enregistrer tout**.
1. Pour spécifier la ou les catégories auxquelles appartient la bibliothèque, sélectionnez le nœud `cq:ClientLibraryFolder`, ajoutez la propriété suivante, puis cliquez sur **Enregistrer tout** :

   * Nom : categories
   * Type : chaîne
   * Valeur : nom de la catégorie
   * Multi : Sélection

1. Ajoutez des fichiers sources au dossier de bibliothèques par n’importe quel moyen. Utilisez, par exemple, un client WebDav pour copier des fichiers ou créez un fichier et publiez le contenu manuellement.

   **Remarque** : Si vous le souhaitez, vous pouvez organiser les fichiers sources dans des sous-dossiers.

1. Sélectionnez le dossier de bibliothèques clientes et cliquez ensuite sur **Créer > Créer un fichier**.
1. Dans la zone du nom de fichier, saisissez l’un des noms suivants et cliquez ensuite sur OK :

   * **`js.txt` :** utilisez ce nom de fichier pour générer un fichier JavaScript.
   * **`css.txt` :** utilisez ce nom de fichier pour générer une feuille de style en cascade (CSS).

1. Ouvrez le fichier et saisissez le texte suivant pour identifier la racine du chemin d’accès des fichiers sources :

   `#base=*[root]*`

   Remplacez * `[root]`* par le chemin d’accès au dossier contenant les fichiers source, par rapport au fichier TXT. Utilisez, par exemple, le texte suivant lorsque les fichiers sources se trouvent dans le même dossier que le fichier TXT :

   `#base=.`

   Le code suivant définit la racine en tant que dossier nommé mobile sous le nœud `cq:ClientLibraryFolder` :

   `#base=mobile`

1. Sur les lignes situées sous `#base=[root]`, indiquez les chemins d’accès des fichiers sources par rapport à la racine. Placez chaque nom de fichier sur une ligne distincte.
1. Cliquez sur **Enregistrer tout**.

### Liaison vers des dépendances {#linking-to-dependencies}

Lorsque le code de votre dossier de bibliothèques clientes fait référence à d’autres bibliothèques, identifiez ces dernières en tant que dépendances. Dans le JSP, la balise `ui:includeClientLib` qui fait référence à votre dossier de bibliothèques clientes fait en sorte que le code HTML contienne un lien vers le fichier de bibliothèque généré, ainsi que les dépendances.

Les dépendances doivent être un autre nœud `cq:ClientLibraryFolder`. Pour identifier les dépendances, ajoutez une propriété à votre nœud `cq:ClientLibraryFolder` avec les attributs suivants :

* **Nom :** dependencies
* **Type :** chaîne[]
* **Valeurs :** valeur de la propriété categories du nœud cq:ClientLibraryFolder dont dépend le dossier de bibliothèques en cours.

Par exemple, / `etc/clientlibs/myclientlibs/publicmain` a une dépendance sur la bibliothèque `cq.jquery`. Le JSP qui fait référence à la bibliothèque cliente principale génère un fichier HTML qui comprend le code suivant :

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporation de code d’autres bibliothèques {#embedding-code-from-other-libraries}

Vous pouvez incorporer du code d’une bibliothèque cliente dans une autre bibliothèque cliente. Lors de l’exécution, les fichiers JS et CSS générés de la bibliothèque d’intégration contiennent le code de la bibliothèque incorporée.

Incorporer du code s’avère utile pour fournir l’accès aux bibliothèques qui sont stockées dans des zones sécurisées du référentiel.

#### Dossiers de bibliothèques clientes spécifiques à une application   {#app-specific-client-library-folders}

Il est conseillé de conserver tous les fichiers associés à une application dans leur dossier d’application sous `/app`. Il est également recommandé d’empêcher les internautes d’accéder au dossier `/app`. Pour répondre à ces deux exigences, créez sous `/etc` un dossier de bibliothèques clientes qui incorpore la bibliothèque cliente qui est située sous `/app`.

Utilisez la propriété categories pour identifier le dossier de bibliothèque cliente à incorporer. Pour incorporer la bibliothèque, ajoutez une propriété au nœud `cq:ClientLibraryFolder` d’intégration à l’aide des attributs de propriété suivants :

* **Nom :** embed
* **Type :** chaîne[]
* **Valeur :** valeur de la propriété categories du nœud `cq:ClientLibraryFolder` à incorporer.

#### Utilisation de l’incorporation pour réduire les requêtes {#using-embedding-to-minimize-requests}

Dans certains cas, il se peut que le code HTML final généré pour la page standard par votre instance de publication comporte un nombre relativement important d’éléments `<script>`, en particulier si votre site utilise des informations contextuelles client pour l’analyse ou le ciblage. Par exemple, dans un projet non optimisé, vous pouvez trouver la série d&#39;éléments `<script>` suivante dans le code HTML d&#39;une page :

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

Dans ce cas, il peut être utile de combiner tout le code de bibliothèque cliente requis dans un seul fichier afin de réduire le nombre de requêtes aller-retour lors du chargement de la page. Pour ce faire, vous pouvez incorporer (`embed`) les bibliothèques requises dans la bibliothèque cliente spécifique à l’application à l’aide de la propriété du nœud `cq:ClientLibraryFolder`.

Les catégories de bibliothèques clientes suivantes sont fournies avec AEM. N’incorporez que celles qui sont obligatoires pour le bon fonctionnement de votre site. Cependant, **vous devez conserver l’ordre indiqué ici** :

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### Chemins d’accès dans les fichiers CSS {#paths-in-css-files}

Lorsque vous incorporez des fichiers CSS, le code CSS généré utilise des chemins d’accès aux ressources qui sont relatifs à la bibliothèque d’intégration. Par exemple, la bibliothèque publiquement accessible `/etc/client/libraries/myclientlibs/publicmain` incorpore la bibliothèque cliente `/apps/myapp/clientlib` :

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

Le fichier `main.css` contient le style suivant :

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Le fichier CSS généré par le nœud `publicmain` contient le style suivant, en utilisant l’URL de l’image d’origine :

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Utilisation d’une bibliothèque pour des groupes mobiles spécifiques {#using-a-library-for-specific-mobile-groups}

Utilisez la propriété `channels` d’un dossier de bibliothèques clientes pour identifier le groupe mobile qui utilise la bibliothèque. La propriété `channels` est utile lorsque des bibliothèques de la même catégorie sont conçues pour différentes fonctionnalités de périphérique.

Pour associer un dossier de bibliothèque client à un groupe de périphériques, ajoutez une propriété à votre noeud `cq:ClientLibraryFolder` avec les attributs suivants :

* **Nom:** canaux
* **Type :** chaîne[]
* **Valeurs :** nom du groupe mobile. Pour exclure le dossier de bibliothèques d’un groupe, faites précéder son nom de domaine d’un point d’exclamation (« ! »).

Par exemple, le tableau suivant répertorie la valeur de la propriété `channels` pour chaque dossier de bibliothèques clientes de la catégorie `cq.widgets` :

| Dossier de bibliothèques clientes | Valeur de la propriété des canaux |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[aucune valeur]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## Utilisation de préprocesseurs {#using-preprocessors}

AEM autorise les préprocesseurs enfichables et prend en charge [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) pour CSS et JavaScript, ainsi que [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) pour JavaScript avec YUI défini comme préprocesseur par défaut d’AEM.

Les préprocesseurs enfichables garantissent une certaine souplesse d’utilisation :

* Définition de ScriptProcessors pouvant traiter des sources de script
* Processeurs configurables avec des options
* Processeurs pouvant être utilisés pour la minification, mais aussi pour des cas de figure des non minifiés
* Bibliothèque cliente (clientlib) pouvant définir le processeur à utiliser

>[!NOTE]
>
>Par défaut, AEM utilise YUI Compressor. Pour connaître la liste des problèmes connus, consultez la [documentation GitHub de YUI Compressor](https://github.com/yui/yuicompressor/issues). Basculer vers le compresseur GCC pour des bibliothèques clientes spécifiques permet de résoudre certains problèmes observés lors de l’utilisation de YUI.

>[!CAUTION]
>
>Ne placez pas de bibliothèque ayant fait l’objet d’une minification dans une bibliothèque cliente. Fournissez plutôt la bibliothèque brute et, si une minification est requise, utilisez les options des préprocesseurs.

### Utilisation {#usage}

Vous pouvez choisir de configurer les préprocesseurs par bibliothèque cliente ou à l’échelle du système.

* Ajoutez les propriétés à plusieurs valeurs `cssProcessor` et `jsProcessor` sur le nœud clientlibrary (bibliothèque cliente).

* Vous pouvez également définir la configuration par défaut du système par le biais de la configuration OSGi du **Gestionnaire de bibliothèques HTML**.

La configuration d’un préprocesseur sur le nœud clientlibrary est prioritaire sur la configuration OSGI.

### Format et exemples {#format-and-examples}

#### Format {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### YUI Compressor pour la minification CSS et GCC pour JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript pour le prétraitement, puis GCC pour la minification et l’obfuscation {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Options GCC supplémentaires {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Pour plus d’informations sur les options GCC, consultez la [documentation de GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Définition de l’outil de minification par défaut du système   {#set-system-default-minifier}

YUI est défini comme outil de minification par défaut dans AEM. Pour le définir sur GCC, procédez comme suit.

1. Accédez au Gestionnaire de configuration Apache Felix à l’adresse [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Recherchez et modifiez le **Gestionnaire de bibliothèques HTML Adobe Granite**.
1. Activez l’option **Minifier** (le cas échéant).
1. Définissez la valeur **Configuration par défaut du processeur JS** sur `min:gcc`.

   Les options peuvent être transmises si elles sont séparées par un point-virgule ; par exemple, `min:gcc;obfuscate=true`.

1. Cliquez sur **Enregistrer** pour enregistrer les modifications.

## Outils de débogage {#debugging-tools}

AEM s’accompagne de plusieurs outils pour déboguer et tester des dossiers de bibliothèques clientes.

### Affichage des fichiers incorporés  {#see-embedded-files}

Pour remonter à l’origine du code incorporé, ou vous assurer que les bibliothèques clientes incorporées produisent les résultats escomptés, vous pouvez afficher les noms des fichiers incorporés au moment de l’exécution. Pour afficher les noms de fichiers, ajoutez le paramètre `debugClientLibs=true` à l’URL de votre page web. La bibliothèque générée contient des instructions `@import` au lieu du code incorporé.

Dans l’exemple de la section [Incorporation de code d’autres bibliothèques](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries), le dossier de bibliothèques clientes `/etc/client/libraries/myclientlibs/publicmain` intègre le dossier `/apps/myapp/clientlib`. L’ajout du paramètre à la page web génère le lien suivant dans le code source de la page web :

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

L’ouverture du fichier `publicmain.css` fait apparaître le code suivant :

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Dans la barre d’adresse de votre navigateur web, ajoutez le texte suivant à l’URL de votre code HTML :

   `?debugClientLibs=true`
1. Au chargement de la page, affichez sa source.
1. Cliquez sur le lien fourni comme href de l’élément link pour ouvrir le fichier et afficher le code source.

### Détection de bibliothèques clientes {#discover-client-libraries}

Le composant `/libs/cq/granite/components/dumplibs/dumplibs` génère une page d’informations sur tous les dossiers de bibliothèques clientes du système. Le nœud `/libs/granite/ui/content/dumplibs` contient le composant comme type de ressource. Pour ouvrir la page, utilisez l’URL suivante (en changeant l’hôte et le port selon les besoins) :

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Les informations affichées sont le chemin d’accès à la bibliothèque et son type (CSS ou JS), ainsi que les valeurs des attributs de bibliothèque, tels que categories et dependencies. Les tableaux suivants présentent les bibliothèques dans chaque catégorie et canal.

### Affichage de la sortie générée {#see-generated-output}

Le composant `dumplibs` comprend un sélecteur de test qui affiche le code source généré pour les balises `ui:includeClientLib`. La page contient du code pour différentes combinaisons des attributs js, css et themed.

1. Appliquez l’une des méthodes suivantes pour ouvrir la page de sortie de test :

   * Sur la page `dumplibs.html`, cliquez sur le lien sous **Cliquez ici pour les résultats du test**.

   * Ouvrez l’URL suivante dans votre navigateur web (utilisez un hôte et un port différents, le cas échéant) :

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La page par défaut affiche le résultat pour les balises ne comportant aucune valeur pour l’attribut categories.

1. Pour afficher la sortie d’une catégorie, saisissez la valeur de la propriété `categories` de la bibliothèque cliente, puis cliquez sur **Envoyer la requête**.

## Configuration du traitement de la bibliothèque pour le développement et la production {#configuring-library-handling-for-development-and-production}

Le service Gestionnaire de bibliothèques HTML traite les balises `cq:ClientLibraryFolder` et génère les bibliothèques au moment de l’exécution. Le type d’environnement, développement ou production, détermine le mode de configuration du service :

* Augmenter le degré de sécurité : désactiver le débogage
* Améliorer les performances : supprimer les espaces et compresser les bibliothèques
* Améliorer la lisibilité : inclure un espace et ne pas compresser

Pour plus d’informations sur la configuration du service, voir [Gestionnaire de bibliothèques HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
