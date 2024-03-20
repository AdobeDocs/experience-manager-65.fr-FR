---
title: Utilisation de bibliothèques côté client
description: AEM fournit des dossiers de bibliothèques côté client qui vous permettent de stocker le code côté client dans le référentiel, de le classer dans des catégories, et de définir quand et comment chaque catégorie de code doit être diffusée au client.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2791'
ht-degree: 97%

---

# Utilisation de bibliothèques côté client{#using-client-side-libraries}

Les sites web modernes reposent largement sur un traitement côté client piloté par un code JavaScript et CSS complexe. Organiser et optimiser la diffusion de ce code est une opération qui peut se révéler complexe.

Pour résoudre ce problème, AEM fournit des **dossiers de bibliothèques côté client** qui permettent de stocker le code côté client dans le référentiel, de le classer par catégorie et de définir quand et comment chaque catégorie de code doit être diffusée au client. Le système de bibliothèque côté client se charge alors de la génération des liens appropriés dans la page Web finale pour charger le code correct.

## Fonctionnement des bibliothèques côté client dans AEM {#how-client-side-libraries-work-in-aem}

La méthode d’insertion standard d’une bibliothèque côté client (c’est-à-dire, un fichier JS ou CSS) dans le code HTML consiste simplement à inclure une balise `<script>` ou `<link>` dans le JSP de cette page, qui contient le chemin d’accès au fichier en question. Par exemple,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Bien que cette approche fonctionne dans AEM, elle peut entraîner des problèmes lorsque les pages et leurs composants constitutifs deviennent complexes. Dans ce cas, il existe le risque que plusieurs copies de la même bibliothèque JS soient incluses dans la sortie finale du HTML. Pour éviter cela et permettre une organisation logique des bibliothèques côté client, AEM utilise des **dossiers de bibliothèques côté client**.

Un dossier de bibliothèques côté client est un nœud de référentiel de type `cq:ClientLibraryFolder`. Sa définition au [format CND](https://jackrabbit.apache.org/node-type-notation.html) est :

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Par défaut, les nœuds `cq:ClientLibraryFolder` peuvent être placés n’importe où dans les sous-arborescences `/libs`, `/apps` et `/etc` du référentiel (ces paramètres par défaut et d’autres paramètres peuvent être réglés dans le panneau **Gestionnaire de bibliothèques HTML Adobe Granite** de la [Console Système](https://localhost:4502/system/console/configMgr)).

Chaque dossier `cq:ClientLibraryFolder` est rempli avec un jeu de fichiers JS et/ou CSS, ainsi que quelques fichiers annexes (voir ci-dessous). Les propriétés du dossier `cq:ClientLibraryFolder` sont configurées comme suit :

* `categories` : identifie les catégories dans lesquelles se trouve le jeu de fichiers JS et/ou CSS de ce dossier `cq:ClientLibraryFolder`. La propriété `categories` comportant plusieurs valeurs, elle permet à un dossier de bibliothèques d’appartenir à plusieurs catégories (voir ci-dessous pour savoir en quoi cela peut se révéler utile).

* `dependencies` : il s’agit d’une liste d’autres catégories de bibliothèques clientes dont dépend ce dossier de catégories. Par exemple, pour deux nœuds `cq:ClientLibraryFolder`, `F` et `G`, si un fichier de `F` nécessite un autre fichier de `G` pour fonctionner correctement, au moins l’une des propriétés `categories` de `G` doit figurer parmi les propriétés `dependencies` de `F`.

* `embed` : utilisé pour incorporer du code d’autres bibliothèques. Si le nœud F incorpore les nœuds G et H, le code HTML qui en résulte sera une concentration du contenu des nœud G et H.
* `allowProxy` : si une bibliothèque cliente se trouve sous `/apps`, cette propriété permet d’y accéder via un servlet proxy. Consultez ci-dessous [Recherche d’un dossier de bibliothèques clientes et utilisation du servlet des bibliothèques clientes du proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

## Référencement des bibliothèques côté client {#referencing-client-side-libraries}

Comme HTL est la technologie privilégiée pour le développement de sites AEM, elle doit être utilisée pour inclure des bibliothèques côté client dans AEM. Cependant, il est également possible de le faire à l’aide de JSP.

### Utilisation de HTL {#using-htl}

Dans HTL, les bibliothèques clientes sont chargées à l’aide d’un modèle d’assistance fourni par AEM, accessible via [`data-sly-use`](https://helpx.adobe.com/fr/experience-manager/htl/using/block-statements.html#use). Trois modèles sont disponibles dans ce fichier, qui peut être appelé via [`data-sly-call`](https://helpx.adobe.com/fr/experience-manager/htl/using/block-statements.html#template-call) :

* **CSS** - Charge seulement les fichiers CSS des bibliothèques client référencées.
* **js** - Charge seulement les fichiers javascript des bibliothèques client référencées.
* **all** - Charge tous les fichiers des bibliothèques client référencées (CSS et JavaScript).

Chaque modèle d’assistance exige une option `categories` pour référencer les bibliothèques clientes souhaitées. Cette option peut être un tableau de valeurs de chaîne ou une chaîne contenant une liste de valeurs séparées par des virgules.

Pour obtenir plus d’informations et consulter un exemple d’utilisation, consultez le document [Prise en main du langage de modèle HTML (HTL)](https://helpx.adobe.com/fr/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Utilisation de JSP {#using-jsp}

Ajoutez une balise `ui:includeClientLib` à votre code JSP pour ajouter un lien aux bibliothèques clientes sur la page HTML générée. Pour référencer les bibliothèques, vous utilisez la valeur de la propriété `categories` du nœud `ui:includeClientLib`.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Par exemple, le nœud `/etc/clientlibs/foundation/jquery` est de type `cq:ClientLibraryFolder` avec une propriété Catégories dont la valeur est `cq.jquery`. Le code suivant d’un fichier JSP fait référence aux bibliothèques :

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La page HTML générée contient le code suivant :

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Pour obtenir des informations complètes, y compris des attributs pour le filtrage des bibliothèques JS, CSS ou de thème, voir [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, qui auparavant était généralement utilisé pour inclure des bibliothèques clientes, est obsolète depuis AEM 5.6. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) doit être utilisé à la place comme décrit ci-dessus.

## Création de dossiers de bibliothèques clientes {#creating-client-library-folders}

Créez un nœud `cq:ClientLibraryFolder` pour définir des bibliothèques JS (JavaScript) et CSS (Cascading Style Sheet), et les mettre à la disposition des pages HTML. Utilisez la propriété `categories` du nœud pour identifier les catégories de bibliothèque auxquelles il appartient.

Le nœud contient un ou plusieurs fichiers sources qui, à l’exécution, sont fusionnés en un seul fichier JS et/ou CSS. Le nom du fichier généré est le nom de nœud avec l’extension `.js` ou `.css`. Par exemple, le nœud de bibliothèque nommé `cq.jquery` donne le nom de fichier généré `cq.jquery.js` ou `cq.jquery.css`.

Les dossiers de bibliothèques clientes contiennent les éléments suivants :

* Fichiers source JS et/ou CSS à fusionner.
* Les ressources qui prennent en charge les styles CSS, tels que les fichiers images.

  **Remarque** : vous pouvez utiliser des sous-dossiers pour organiser les fichiers sources.
* Un fichier `js.txt` et/ou un fichier `css.txt` qui identifie les fichiers sources à fusionner dans les fichiers JS et/ou CSS générés.

![clientlibarch](assets/clientlibarch.png)

Pour plus d’informations sur les exigences spécifiques aux bibliothèques clientes pour les widgets, consultez [Utilisation et extension des widgets](/help/sites-developing/widgets.md).

Le client Web doit être autorisé à accéder au nœud `cq:ClientLibraryFolder`. Vous pouvez également exposer les bibliothèques à partir de zones sécurisées du référentiel (voir la section « Incorporation de code d’autres bibliothèques » ci-dessous).

### Ignorer les bibliothèques dans /lib {#overriding-libraries-in-lib}

Dossiers de bibliothèques clientes situés sous `/apps` ont la priorité sur les dossiers portant le même nom qui sont similaires dans `/libs`. Par exemple : `/apps/cq/ui/widgets` a priorité sur `/libs/cq/ui/widgets`. Lorsque ces bibliothèques appartiennent à la même catégorie, la bibliothèque située sous `/apps` est utilisée.

### Recherche d’un dossier de bibliothèques clientes et utilisation du servlet des bibliothèques clientes du proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Dans les versions précédentes, les dossiers de bibliothèques clientes se trouvaient sous `/etc/clientlibs` dans le référentiel. Cela est toujours pris en charge. Cependant, il est recommandé de placer désormais les bibliothèques clientes sous `/apps`. L’objectif est de placer les bibliothèques clientes près des autres scripts, qui se situent généralement sous `/apps` et `/libs`.

>[!NOTE]
>
>Les ressources statiques situées sous le dossier de bibliothèque cliente doivent se trouver dans un dossier appelé *ressources*. Si vous ne disposez pas des ressources statiques, telles que des images, sous le dossier *ressources*, il ne peut pas être référencé sur une instance de publication. Voici un exemple : https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Pour mieux isoler le code du contenu et de la configuration, il est recommandé de localiser les bibliothèques clientes sous `/apps` et les exposer via `/etc.clientlibs` en utilisant la variable `allowProxy` .

Pour que les bibliothèques clientes situées sous `/apps` soient accessibles, un servlet proxy est utilisé. Les listes de contrôle d’accès (ACL) sont toujours appliquées sur le dossier de bibliothèques clientes, mais le servlet permet la lecture du contenu via `/etc.clientlibs/` si la propriété `allowProxy` est définie sur `true`.

Une ressource statique n’est accessible que par le biais du proxy, si elle réside sous une ressource située sous le dossier de bibliothèque cliente.

Par exemple :

* Vous avez une bibliothèque cliente dans `/apps/myproject/clientlibs/foo`.
* Vous avez une image statique dans `/apps/myprojects/clientlibs/foo/resources/icon.png`.

Vous pouvez définir la propriété `allowProxy` sur `foo` sur true.

* Vous pouvez ensuite demander `/etc.clientlibs/myprojects/clientlibs/foo.js`.
* Vous pouvez alors référencer l’image via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`.

>[!CAUTION]
>
>Lorsque vous utilisez des bibliothèques clientes en proxy, la configuration d’AEM Dispatcher peut nécessiter une mise à jour pour s’assurer que les URI avec l’extension clientlibs sont autorisées.

>[!CAUTION]
>
>Adobe recommande de placer les bibliothèques clientes sous `/apps` et de les rendre disponibles par le biais du servlet proxy. Veuillez toutefois garder à l’esprit que les sites publics ne doivent jamais inclure d’éléments diffusés directement sur un chemin `/apps` ou `/libs`.

### Création d’un dossier de bibliothèques clientes {#create-a-client-library-folder}

1. Ouvrez CRXDE Lite dans un navigateur Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Sélectionnez le dossier dans lequel vous souhaitez placer le dossier de bibliothèques clientes et cliquez ensuite sur **Créer > Créer un nœud**.
1. Attribuez un nom au fichier de bibliothèque, puis sélectionnez `cq:ClientLibraryFolder` dans la liste Type. Cliquez sur **OK**, puis sur **Enregistrer tout**.
1. Pour spécifier la ou les catégories auxquelles appartient la bibliothèque, sélectionnez le nœud `cq:ClientLibraryFolder`, ajoutez la propriété suivante, puis cliquez sur **Enregistrer tout** :

   * Nom : categories
   * Type : chaîne
   * Valeur : nom de la catégorie
   * Multi : sélection

1. Ajoutez des fichiers sources au dossier de bibliothèque par n’importe quel moyen. Par exemple, utilisez un client WebDav pour copier des fichiers ou créez un fichier et le contenu manuellement.

   **Remarque** : si vous le souhaitez, vous pouvez organiser les fichiers sources dans des sous-dossiers.

1. Sélectionnez le dossier de bibliothèques clientes et cliquez ensuite sur **Créer > Créer un fichier**.
1. Dans la zone du nom de fichier, saisissez l’un des noms suivants et cliquez ensuite sur OK :

   * **`js.txt` :** utilisez ce nom de fichier pour générer un fichier JavaScript.
   * **`css.txt` :** utilisez ce nom de fichier pour générer une feuille de style en cascade (CSS).

1. Ouvrez le fichier et saisissez le texte suivant pour identifier la racine du chemin d’accès des fichiers sources :

   `#base=*[root]*`

   Remplacez *`[root]`* par le chemin d’accès au dossier contenant les fichiers sources, par rapport au fichier TXT. Utilisez, par exemple, le texte suivant lorsque les fichiers sources se trouvent dans le même dossier que le fichier TXT :

   `#base=.`

   Le code suivant définit la racine en tant que dossier nommé mobile sous le nœud `cq:ClientLibraryFolder` :

   `#base=mobile`

1. Sur les lignes situées sous `#base=[root]`, indiquez les chemins d’accès des fichiers sources par rapport à la racine. Placez chaque nom de fichier sur une ligne distincte.
1. Cliquez sur **Enregistrer tout**.

### Liaison vers des dépendances {#linking-to-dependencies}

Lorsque le code de votre dossier de bibliothèques clientes fait référence à d’autres bibliothèques, identifiez ces dernières en tant que dépendances. Dans le JSP, la variable `ui:includeClientLib` qui fait référence à votre dossier de bibliothèques clientes, le code de HTML inclut un lien vers le fichier de bibliothèque généré et les dépendances.

Les dépendances doivent être un autre nœud `cq:ClientLibraryFolder`. Pour identifier les dépendances, ajoutez une propriété à votre nœud `cq:ClientLibraryFolder` avec les attributs suivants :

* **Nom :** dependencies
* **Type :** chaîne[]
* **Valeurs :** valeur de la propriété categories du nœud cq:ClientLibraryFolder dont dépend le dossier de bibliothèques en cours.

Par exemple, `etc/clientlibs/myclientlibs/publicmain` comporte une dépendance sur la bibliothèque `cq.jquery`. Le JSP qui fait référence à la bibliothèque cliente principale génère un fichier HTML qui comprend le code suivant :

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporation de code d’autres bibliothèques {#embedding-code-from-other-libraries}

Vous pouvez incorporer du code d’une bibliothèque cliente dans une autre bibliothèque cliente. Au moment de l’exécution, les fichiers JS et CSS générés de la bibliothèque d’intégration incluent le code de la bibliothèque incorporée.

L’incorporation de code se révèle utile pour permettre l’accès aux bibliothèques stockées dans des zones sécurisées du référentiel.

#### Dossiers de bibliothèques clientes spécifiques à une application {#app-specific-client-library-folders}

Il est conseillé de conserver tous les fichiers associés à une application dans leur dossier d’application sous `/apps`. Il est également recommandé d’empêcher les internautes d’accéder au dossier `/apps`. Pour répondre à ces deux exigences, créez un dossier de bibliothèques clientes sous `/apps` et rendez-le accessible par le biais du servlet proxy, comme décrit sous [Recherche d’un dossier de bibliothèques clientes et utilisation du servlet des bibliothèques clientes du proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Utilisez la propriété categories pour identifier le dossier de bibliothèque cliente à incorporer. Pour incorporer la bibliothèque, ajoutez une propriété au nœud `cq:ClientLibraryFolder` d’intégration à l’aide des attributs de propriété suivants :

* **Nom :** embed
* **Type :** chaîne[]
* **Valeur :** valeur de la propriété categories du nœud `cq:ClientLibraryFolder` à incorporer.

#### Utilisation de l’incorporation pour réduire les requêtes {#using-embedding-to-minimize-requests}

Dans certains cas, vous constaterez peut-être que le code HTML final généré pour une page type par votre instance de publication contient un nombre relativement élevé d’éléments `<script>`, en particulier si votre site utilise des informations de contexte client à des fins d’analyse ou de ciblage. Par exemple, dans un projet non optimisé, il se peut que le code HTML d’une page contienne la série d’élément `<script>` suivante :

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

Dans ce cas, il peut être utile de combiner tout le code de bibliothèque cliente requis dans un seul fichier afin de réduire le nombre de requêtes aller-retour lors du chargement de la page. Pour ce faire, vous pouvez incorporer (`embed`) les bibliothèques requises dans la bibliothèque cliente spécifique à l’application à l’aide de la propriété du nœud `cq:ClientLibraryFolder`.

Les catégories de bibliothèque cliente ci-après sont incluses avec AEM. Vous devez incorporer uniquement celles qui sont requises pour le fonctionnement de votre site spécifique. Cependant, **vous devez conserver l’ordre indiqué ici** :

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

Utilisez la propriété `channels` d’un dossier de bibliothèques clientes pour identifier le groupe mobile qui utilise la bibliothèque. La propriété `channels` est utile lorsque des bibliothèques de la même catégorie sont conçues pour différentes fonctionnalités d’appareil.

Pour associer un dossier de bibliothèques clientes à un groupe d’appareils, ajoutez une propriété à votre nœud `cq:ClientLibraryFolder` avec les attributs suivants :

* **Nom :** canaux
* **Type :** chaîne[]
* **Valeurs :** nom du groupe mobile Pour exclure le dossier de bibliothèques d’un groupe, faites précéder son nom de domaine d’un point d’exclamation (« ! »).

Par exemple, le tableau suivant répertorie la valeur de la propriété `channels` pour chaque dossier de bibliothèques clientes de la catégorie `cq.widgets` :

| Dossier de bibliothèques clientes | Valeur de la propriété channels |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Utilisation de préprocesseurs {#using-preprocessors}

AEM autorise les préprocesseurs enfichables et prend en charge [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) pour CSS et JavaScript, ainsi que [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler?hl=fr) pour JavaScript avec YUI défini comme préprocesseur par défaut d’AEM.

Les préprocesseurs enfichables permettent une utilisation flexible, notamment :

* La définition de ScriptProcessors peut traiter des sources de script.
* Les processeurs peuvent être configurés avec des options.
* Les processeurs peuvent être utilisés pour la minification, mais également pour les cas non minimisés.
* La bibliothèque cliente peut définir le processeur à utiliser.

>[!NOTE]
>
>Par défaut, AEM utilise YUI Compressor. Pour connaître la liste des problèmes connus, consultez la [documentation GitHub de YUI Compressor](https://github.com/yui/yuicompressor/issues). Le passage au compresseur GCC pour des clientlibs spécifiques peut résoudre certains problèmes observés lors de l’utilisation de YUI.

>[!CAUTION]
>
>Ne placez pas de bibliothèque minimisée dans une bibliothèque cliente. Fournissez plutôt la bibliothèque brute et, si une minification est requise, utilisez les options des préprocesseurs.

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

### Définition de l’outil de minification par défaut du système {#set-system-default-minifier}

YUI est défini comme minificateur par défaut dans AEM. Pour modifier ce paramètre en GCC, procédez comme suit.

1. Accédez à Apache Felix Config Manager à l’adresse [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Recherchez et modifiez le **Gestionnaire de bibliothèques HTML Adobe Granite**.
1. Activez l’option **Minifier** (le cas échéant).
1. Définissez la valeur **Configuration par défaut du processeur JS** sur `min:gcc`.

   Les options peuvent être transmises si elles sont séparées par un point-virgule, par exemple, `min:gcc;obfuscate=true`.

1. Cliquez sur **Enregistrer** pour enregistrer les modifications.

## Outils de débogage {#debugging-tools}

AEM s’accompagne de plusieurs outils pour déboguer et tester des dossiers de bibliothèques clientes.

### Voir Fichiers incorporés {#see-embedded-files}

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
1. Au chargement de la page, affichez la source de la page.
1. Cliquez sur le lien fourni comme href de l’élément de lien pour ouvrir le fichier et afficher le code source.

### Détection de bibliothèques clientes {#discover-client-libraries}

Le composant `/libs/cq/granite/components/dumplibs/dumplibs` génère une page d’informations sur tous les dossiers de bibliothèques clientes du système. Le nœud `/libs/granite/ui/content/dumplibs` contient le composant comme type de ressource. Pour ouvrir la page, utilisez l’URL suivante (en changeant l’hôte et le port selon les besoins) :

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Les informations comprennent le chemin et le type de bibliothèque (CSS ou JS), ainsi que les valeurs des attributs de bibliothèque, tels que les catégories et les dépendances. Les tableaux suivants de la page affichent les bibliothèques dans chaque catégorie et canal.

### Affichage de la sortie générée {#see-generated-output}

Le composant `dumplibs` comprend un sélecteur de test qui affiche le code source généré pour les balises `ui:includeClientLib`. La page contient du code pour différentes combinaisons des attributs js, css et themed.

1. Appliquez l’une des méthodes suivantes pour ouvrir la page de sortie de test :

   * Sur la page `dumplibs.html`, cliquez sur le lien sous **Cliquez ici pour les résultats du test**.

   * Ouvrez l’URL suivante dans votre navigateur web (utilisez un hôte et un port différents, le cas échéant) :

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La page par défaut affiche le résultat pour les balises ne comportant aucune valeur pour l’attribut categories.

1. Pour afficher la sortie d’une catégorie, saisissez la valeur de la propriété `categories` de la bibliothèque cliente, puis cliquez sur **Envoyer la requête**.

## Configuration du traitement de la bibliothèque pour le développement et la production {#configuring-library-handling-for-development-and-production}

Le service Gestionnaire de bibliothèques HTML traite les balises `cq:ClientLibraryFolder` et génère les bibliothèques au moment de l’exécution. Le type d’environnement, de développement ou de production détermine comment configurer le service :

* Sécurité renforcée : désactivez le débogage.
* Amélioration des performances : supprimez les espaces blancs et compressez les bibliothèques.
* Amélioration de la lisibilité : incluez des espaces blancs et ne compressez pas.

Pour plus d’informations sur la configuration du service, voir [Gestionnaire de bibliothèques HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
