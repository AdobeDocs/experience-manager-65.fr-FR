---
title: Concepts de base d’AEM
seo-title: The Basics
description: Présentation des concepts de base de la structure de l’AEM et du développement sur celle-ci, notamment la compréhension de JCR, Sling, OSGi, du Dispatcher, des workflows et de MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '3324'
ht-degree: 53%

---

# Concepts de base d’AEM {#aem-core-concepts}

>[!NOTE]
>
>Avant d’étudier les concepts de base d’AEM, Adobe vous recommande de suivre le tutoriel WKND dans le document [Prise en main du développement d’AEM Sites](/help/sites-developing/getting-started.md) pour obtenir un aperçu du processus de développement AEM et une introduction aux concepts clés.

## Conditions préalables pour le développement sur AEM {#prerequisites-for-developing-on-aem}

Vous avez besoin des compétences suivantes pour développer en plus de l’AEM :

* Connaissances de base des techniques des applications web, notamment :

   * le cycle request -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* connaissances opérationnelles d’Experience Server (CRX), y compris l’explorateur de contenu ;
* Pour développer dans l’IU classique, des connaissances de base de JSP (JavaServer Pages), notamment la possibilité de comprendre et de modifier des exemples JSP simples, sont également requises.

Il est également recommandé de lire et de suivre les [Recommandations et bonnes pratiques](/help/sites-developing/dev-guidelines-bestpractices.md).

## Référentiel de contenu Java™ {#java-content-repository}

La norme Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), spécifie une méthode indépendante du fournisseur et de l’implémentation pour accéder au contenu de manière bidirectionnelle à un niveau granulaire au sein d’un référentiel de contenu.

Les spécifications sont dirigées par Adobe Research (Suisse) SA.

Le package [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), javax.jcr.&amp;ast; est utilisé pour l’accès direct et la manipulation du contenu du référentiel.

## Experience Server (CRX) et Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server fournit les services d’expérience sur lesquels AEM est basé et qui peuvent être utilisés pour créer des applications personnalisées. Il incorpore également le référentiel de contenu basé sur Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) est une mise en oeuvre open source, entièrement conforme, de l’API JCR 2.0.

## Traitement des requêtes Sling {#sling-request-processing}

### Introduction à Sling {#introduction-to-sling}

AEM repose sur [Sling](https://sling.apache.org/index.html), un framework d’application web basé sur des principes REST. Il facilite le développement d’applications orientées contenu. Sling utilise un référentiel JCR, tel qu’Apache Jackrabbit ou, dans le cas d’AEM, le référentiel de contenu CRX, comme entrepôt de données. The Apache Software Foundation a contribué au développement de Sling. Plus d’informations sont disponibles sur Apache.

Avec Sling, le type de contenu à diffuser n’est pas la première considération en matière de traitement. Il s’agit plutôt de savoir si l’URL se résout en un objet de contenu pour lequel un script peut ensuite être identifié afin d’effectuer le rendu. Cela offre une excellente prise en charge aux auteurs de contenu web pour créer des pages facilement personnalisées selon leurs besoins.

Les avantages liés à cette flexibilité sont évidents dans les applications comportant un vaste éventail d’éléments de contenu différents ou dans les cas où des pages facilement personnalisables sont nécessaires. En particulier, lors de la mise en oeuvre d’un système de gestion de contenu web tel que WCM dans la solution AEM.

Voir [Découvrir Sling en 15 minutes](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) pour connaître les premières étapes de développement avec Sling.

Le schéma suivant explique la résolution du script sling : il montre comment passer de la requête HTTP au nœud de contenu, du nœud de contenu au type de ressource, du type de ressource au script, ainsi que les variables de script disponibles.

![Présentation de la résolution du script Apache Sling](assets/sling-cheatsheet-01.png)

Le schéma suivant décrit tous les paramètres de requête invisibles, mais puissants, que vous pouvez utiliser avec SlingPostServlet, le gestionnaire par défaut pour toutes les requêtes POST. Ce dernier offre des options infinies pour créer, modifier, supprimer, copier et déplacer des nœuds dans le référentiel.

![Utilisation de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling est centré sur le contenu {#sling-is-content-centric}

Sling est *centré sur le contenu*. Cela signifie que le traitement est axé sur le contenu, car chaque requête (HTTP) est mappée sur le contenu sous la forme d’une ressource JCR (un noeud de référentiel) :

* la première cible est la ressource (noeud JCR) contenant le contenu.
* deuxièmement, la représentation, ou le script, se trouve à partir des propriétés de ressource combinées à certaines parties de la requête (par exemple, les sélecteurs et/ou l’extension).

### Sling RESTful {#restful-sling}

En raison de son approche centrée sur le contenu, Sling implémente un serveur orienté REST et propose ainsi un nouveau concept dans les frameworks d’applications web. Les avantages sont les suivants :

* très RESTful, pas seulement à la surface; les ressources et les représentations sont correctement modélisées dans le serveur.
* supprime un ou plusieurs modèles de données

   * Auparavant, les éléments suivants étaient nécessaires : Structure d’URL, objets métier, schéma de base de données ;
   * cela est désormais réduit à : URL = ressource = structure JCR

### Décomposition d’URL {#url-decomposition}

Dans Sling, le traitement est piloté par l’URL de la requête de l’utilisateur. C’est l’URL qui définit le contenu à afficher par les scripts appropriés. Pour ce faire, les informations sont extraites de l’URL.

Si nous analysons l’URL suivante :

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Nous pouvons le diviser en plusieurs parties composites :

| protocol | host | content path | selector(s) | extension |  | suffixe |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | tools/spy | .printable.a4. | html | / | a/b | ? | x=12 |

**protocol** HTTP

**host** Nom du site web.

**content path** Chemin d’accès spécifiant le contenu à rendre. Est utilisé en combinaison avec l’extension. Dans cet exemple, on obtient tools/spy.html.

**Selector(s)** Utilisé pour les méthodes secondaires de rendu du contenu ; dans cet exemple, il s’agit de la version imprimable au format A4.

**extension** Format de contenu ; spécifie également le script à utiliser pour le rendu.

**suffix** Peut servir à spécifier des informations supplémentaires.

**param(s)** Tout paramètre requis pour le contenu dynamique.

#### De l’URL au contenu et aux scripts {#from-url-to-content-and-scripts}

En suivant ces principes :

* le mappage utilise le chemin d’accès au contenu extrait de la requête pour localiser la ressource.
* lorsque la ressource appropriée est localisée, le type de ressource sling est extrait et utilisé pour localiser le script à utiliser pour le rendu du contenu.

La figure ci-dessous illustre le mécanisme utilisé, qui sera abordé plus en détail dans les sections suivantes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Avec Sling, vous spécifiez le script à appliquer pour le rendu d’une entité donnée (en définissant la propriété `sling:resourceType` dans le nœud JCR). Ce mécanisme offre plus de liberté que celui selon lequel le script accède aux entités de données (comme le ferait une instruction SQL dans un script PHP) puisqu’une ressource peut avoir plusieurs rendus.

#### Mappage des requêtes aux ressources {#mapping-requests-to-resources}

La requête est décomposée et les informations nécessaires sont extraites. Le référentiel est recherché pour la ressource demandée (noeud de contenu) :

* D’abord, Sling vérifie si un nœud existe à l’emplacement spécifié dans la requête. Par exemple, `../content/corporate/jobs/developer.html`. 
* Si aucun nœud n’est identifié, l’extension est supprimée et la recherche recommence ; par exemple, `../content/corporate/jobs/developer`. 
* si aucun noeud n’est trouvé, Sling renvoie le code http 404 (Not Found).

Sling permet également à des éléments autres que des nœuds JCR d’être des ressources, mais il s’agit là d’une fonctionnalité avancée.

### Localisation du script {#locating-the-script}

Lorsque la ressource appropriée (nœud de contenu) est localisée, le **type de ressource sling** est extrait. Il s’agit d’un chemin d’accès qui localise le script à utiliser pour le rendu du contenu.

Le chemin spécifié par le `sling:resourceType` peut être :

* absolu
* relatif à un paramètre de configuration

   Les chemins relatifs sont recommandés par Adobe car ils contribuent à plus de portabilité.

Tous les scripts Sling sont stockés dans des sous-dossiers `/apps` ou `/libs` qui font l’objet d’une recherche dans cet ordre (voir [Personnalisation de composants et d’autres éléments](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Un certain nombre d’autres points sont à noter :

* lorsque la méthode (GET, POST) est requise, elle est spécifiée en majuscules, conformément à la spécification HTTP, par exemple jobs.POST.esp (voir ci-dessous).
* différents moteurs de script sont pris en charge :

   * HTL (Langage de modèle de HTML - Adobe Experience Manager système de modèle côté serveur préféré et recommandé pour le HTML) : `.html`
   * Pages ECMAScript (JavaScript) (exécution côté serveur) : `.esp, .ecma`
   * Java™ Server Pages (exécution côté serveur) : `.jsp`
   * Compilateur de servlet Java™ (exécution côté serveur) : `.java`
   * Modèles JavaScript (exécution côté client) : `.jst`

La liste des moteurs de script pris en charge par l’instance donnée d’AEM figure dans la Felix Management Console (`http://<host>:<port>/system/console/slingscripting`).

Apache Sling prend également en charge l’intégration à d’autres moteurs de script populaires (par exemple, Groovy, JRuby, Freemarker) et permet d’intégrer de nouveaux moteurs de script.

En reprenant l’exemple ci-dessus, si `sling:resourceType` est `hr/jobs` alors pour :

* Les requêtes GET/HEAD et les URL se terminant par .htmp (types de requête par défaut, format par défaut)

   Le script est /apps/hr/jobs/jobs.esp; la dernière section de sling:resourceType forme le nom de fichier.

* Requêtes POST (tous les types de requête, à l’exclusion des GET/HEAD, le nom de la méthode doit être en majuscules)

   POST est utilisé dans le nom du script.

   Le script est `/apps/hr/jobs/jobs.POST.esp`.

* URL dans d’autres formats, qui ne se terminent pas par .html

   Par exemple, `../content/corporate/jobs/developer.pdf`

   Le script sera `/apps/hr/jobs/jobs.pdf.esp` ; le suffixe est ajouté au nom du script.

* URL avec sélecteurs

   Les sélecteurs peuvent être utilisés pour afficher le même contenu dans un autre format. Par exemple une version imprimable, un flux rss ou un résumé.

   Si nous étudions une version adaptée à l’imprimante dans laquelle le sélecteur peut être *print* ; comme dans `../content/corporate/jobs/developer.print.html`.

   Le script sera `/apps/hr/jobs/jobs.print.esp` ; le sélecteur est ajouté au nom du script.

* Si aucun sling:resourceType n’a été défini, alors :

   * le chemin d’accès au contenu sera utilisé pour rechercher un script approprié (si le ResourceTypeProvider basé sur le chemin est principal).

      par exemple, le script pour `../content/corporate/jobs/developer.html` génère une recherche dans `/apps/content/corporate/jobs/` ;

   * le type de noeud Principal sera utilisé.

* Si aucun script n’est trouvé, le script par défaut est utilisé.

   Le rendu par défaut est actuellement pris en charge sous la forme de texte brut (.txt), HTML (.html) et JSON (.json) qui répertorie toutes les propriétés du nœud (correctement mises en forme). Le rendu par défaut pour l’extension .res, ou les requêtes sans extension de requête, consiste à spouiller la ressource (si possible).
* Pour la gestion des erreurs http (codes 403 ou 404), Sling recherche un script dans :

   * l’emplacement /apps/sling/servlet/errorhandler pour [script personnalisé](/help/sites-developing/customizing-errorhandler-pages.md)
   * ou l’emplacement des scripts standard /libs/sling/servlet/errorhandler/403.esp, ou 404.esp, respectivement.

Si plusieurs scripts s’appliquent pour une requête donnée, celui avec la meilleure correspondance est sélectionné. Plus une correspondance est précise, mieux elle est; en d’autres termes, plus le sélecteur correspond mieux, quelle que soit l’extension de requête ou la correspondance de nom de méthode.

Par exemple, envisagez une demande d’accès à la ressource

`/content/corporate/jobs/developer.print.a4.html`
de type
`sling:resourceType="hr/jobs"`.

En supposant que les scripts suivants sont présents dans l’emplacement correct :

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

L’ordre de préférence serait (8) – (7) – (6) – (5) – (4) – (3) – (2) – (1).

En plus des types de ressources (principalement définis par la propriété `sling:resourceType`), il existe également le super type de ressource. Il est généralement indiqué par la propriété `sling:resourceSuperType`. Ces super types sont aussi pris en compte lors de la recherche d’un script. Les super types de ressources présentent l’avantage de former une hiérarchie de ressources où le type de ressource par défaut `sling/servlet/default` (utilisé par les servlets par défaut) est effectivement la racine.

Le super type de ressource d’une ressource peut être défini de deux manières :

* par la propriété `sling:resourceSuperType` de la ressource ;
* par la propriété `sling:resourceSuperType` du nœud vers lequel pointe `sling:resourceType`.

Par exemple :

* /

   * a
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




La hiérarchie de type de :

* `/x`
   * est `[ c, b, a, <default>]`
* alors que pour `/y`
   * la hiérarchie est `[ c, a, <default>]`.

Ceci est dû au fait que `/y` possède la propriété `sling:resourceSuperType` contrairement à `/x`, et donc son super-type est issu de son type de ressource.

#### Les scripts Sling ne peuvent pas être appelés directement {#sling-scripts-cannot-be-called-directly}

Dans Sling, les scripts ne peuvent pas être appelés directement, car cela violerait le concept strict d’un serveur REST ; vous mélangeriez des ressources et des représentations.

Si vous appelez la représentation (le script) directement, vous masquez la ressource dans le script, donc le framework (Sling) ne peut plus la détecter. Vous perdez ainsi certaines fonctionnalités :

* la gestion automatique des méthodes http autres que GET, notamment :

   * les méthodes POST, PUT, DELETE qui sont gérées avec une implémentation par défaut de Sling ;
   * le script `POST.jsp` dans votre emplacement sling:resourceType.

* l’architecture de votre code n’est plus aussi propre ni aussi clairement structurée qu’elle devrait l’être ; d’une importance primordiale pour le développement à grande échelle

### API Sling {#sling-api}

Il utilise le package d’API Sling org.apache.sling.&amp;ast; et les bibliothèques de balises.

### Référencement d’éléments existants avec sling:include {#referencing-existing-elements-using-sling-include}

En dernier lieu, il faut considérer la nécessité de référencer les éléments existants dans les scripts.

Des scripts plus complexes (agrégation de scripts) peuvent demander un accès à plusieurs ressources (par exemple, navigation, barre latérale, pied de page, éléments d’une liste) en ajoutant *resource*.

Pour ce faire, vous pouvez utiliser la commande sling:include(&quot;/&lt;chemin>/&lt;ressource>&quot;). Cela inclut effectivement la définition de la ressource référencée, comme dans l’instruction suivante qui fait référence à une définition existante pour le rendu des images :

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi désigne une architecture permettant de développer et de déployer des applications et des bibliothèques modulaires (également connu sous le nom de Dynamic Module System for Java). Les conteneurs OSGi vous permettent de décomposer votre application en modules distincts (des fichiers jar contenant des méta-informations supplémentaires appelés « bundles » dans le jargon OSGi) et de gérer les interdépendances qui existent entre eux avec :

* services implémentés dans le conteneur
* un contrat entre le conteneur et votre application

Ces services et contrats fournissent une architecture qui permet à des éléments individuels de se découvrir dynamiquement les uns les autres à des fins de collaboration.

Une structure OSGi vous offre ensuite un chargement/déchargement dynamique, une configuration et un contrôle de ces lots, sans nécessiter de redémarrage.

>[!NOTE]
>
>Vous trouverez des informations complètes sur la technologie OSGi sur le [site web d’OSGi](https://www.osgi.org).
>
>En particulier, la page Basic Education (formation de base) contient un ensemble de présentations et de tutoriels.

Cette architecture vous permet d’étendre Sling en lui ajoutant des modules spécifiques aux applications. Sling, et donc CQ5, utilise l’implémentation [Apache Felix](https://felix.apache.org/documentation/index.html) d’OSGI (Open Services Gateway Initiative) et est basé sur les spécifications OSGi Service Platform Release 4, Version 4.2. Il s’agit de deux groupes OSGi s’exécutant dans une structure OSGi.

Vous pouvez ainsi effectuer les actions suivantes sur l’un des packages de votre installation :

* installation
* start
* stop
* mise à jour
* désinstallation
* voir l’état actuel
* accéder à des informations plus détaillées (nom symbolique, version, emplacement, etc.) sur les lots spécifiques ;

Pour plus d’informations, reportez-vous aux sections [Console web](/help/sites-deploying/web-console.md), [Configuration OSGI](/help/sites-deploying/configuring-osgi.md) et [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md).

## Objets de développement dans l’environnement AEM {#development-objects-in-the-aem-environment}

Les éléments suivants présentent un intérêt pour le développement :

**Élément** Un élément est un nœud ou une propriété.

Pour plus d’informations sur la manipulation des objets Élément, reportez-vous aux [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) de l’interface javax.jcr.Item.

**Nœud (et leurs propriétés)** Les nœuds et leurs propriétés sont définis dans la spécification JCR API 2.0 (JSR 283). Ils stockent le contenu, les définitions d’objets, les scripts de rendu et d’autres données.

Les noeuds définissent la structure du contenu et leurs propriétés stockent le contenu réel et les métadonnées.

Les nœuds de contenu pilotent le rendu. Sling récupère le nœud de contenu de la requête entrante. La propriété sling:resourceType de ce noeud pointe vers le composant de rendu Sling à utiliser.

Un noeud, qui est un nom JCR, est également appelé une ressource dans l’environnement Sling.

Par exemple, pour obtenir les propriétés du noeud actif, vous pouvez utiliser le code suivant dans votre script :

`PropertyIterator properties = currentNode.getProperties();`

currentNode étant l’objet du nœud actif.

Pour plus d’informations sur la manipulation des objets Node, reportez-vous aux [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** Dans AEM, toutes les entrées utilisateur sont gérées par des widgets. Ils sont souvent utilisés pour contrôler la modification d’un élément de contenu.

Les boîtes de dialogue sont créées en combinant des widgets.

AEM a été développé à l’aide de la bibliothèque de widgets ExtJS.

**Boîte de dialogue** Une boîte de dialogue est un type spécial de widget.

Pour modifier le contenu, AEM utilise des boîtes de dialogue définies par le développeur de l’application. Ils combinent une série de widgets pour présenter à l’utilisateur tous les champs et actions nécessaires pour modifier le contenu associé.

Les boîtes de dialogue sont également utilisées pour modifier les métadonnées et par divers outils d’administration.

**Composant** Un composant logiciel est un élément système offrant un service ou un événement prédéfini et capable de communiquer avec d’autres composants.

Dans AEM, un composant est souvent utilisé pour effectuer le rendu du contenu d’une ressource. Lorsque la ressource est une page, le composant chargé de son rendu est appelé « composant de niveau supérieur » ou « composant de page ». Cependant, un composant n’a pas à effectuer le rendu du contenu ni à être lié à une ressource spécifique ; par exemple, un composant de navigation affiche des informations sur plusieurs ressources.

La définition d’un composant comprend :

* le code utilisé pour effectuer le rendu du contenu ;
* une boîte de dialogue pour l’entrée utilisateur et la configuration du contenu résultant.

**Modèle** Un modèle est la base d’un type de page spécifique. Lors de la création d’une page dans l’onglet Sites web, l’utilisateur doit sélectionner un modèle. La nouvelle page est alors créée en copiant ce modèle.

Un modèle est une hiérarchie de noeuds ayant la même structure que la page à créer, mais sans contenu réel.

Il définit le composant de page utilisé pour afficher la page et le contenu par défaut (contenu principal de premier niveau). Le contenu définit la manière dont il est rendu, AEM étant centré sur le contenu.

**Composant de page (composant de niveau supérieur)** Composant à utiliser pour effectuer le rendu de la page.

**Page** Une page est une « instance » d’un modèle.

Une page comporte un nœud de hiérarchie de type cq:Page et un nœud de contenu de type cq:PageContent. La propriété sling:resourceType du noeud de contenu pointe vers le composant Page utilisé pour le rendu de la page.

Par exemple, pour obtenir le nom de la page active, vous pouvez utiliser le code suivant dans votre script :

S`tring pageName = currentPage.getName();`

currentPage étant l’objet de la page active. Pour plus d’informations sur la manipulation des objets Page, reportez-vous aux [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**Gestionnaire de pages** Le gestionnaire de page est une interface qui fournit des méthodes pour les opérations au niveau de la page.

Par exemple, pour obtenir la page conteneur d’une ressource, vous pouvez utiliser le code suivant dans votre script :

Page myPage = pageManager.getContainerPage(myResource);

pageManager étant l’objet de gestionnaire de page et myResource un objet de ressource. Pour plus d’informations sur les méthodes fournies par le gestionnaire de page, reportez-vous aux [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## Structure dans le référentiel {#structure-within-the-repository}

La liste suivante donne un aperçu de la structure que vous voyez dans le référentiel.

>[!CAUTION]
>
>Les modifications apportées à cette structure, ou aux fichiers qu’elle contient, doivent être entreprises avec prudence.
>
>Des modifications sont nécessaires lorsque vous développez, mais vous devez veiller à bien comprendre les implications de toute modification que vous apportez.

>[!CAUTION]
>
>Ne modifiez rien dans la variable `/libs` chemin d’accès. Pour la configuration et d’autres modifications, copiez l’élément de `/libs` dans `/apps` et apportez des modifications dans `/apps`.

* `/apps`

    Application connexe qui inclut des définitions de composants spécifiques à votre site web. Les composants que vous développez peuvent être basés sur les composants prêts à l’emploi disponibles dans `/libs/foundation/components`.

* `/content`

   Contenu créé pour votre site web.

* `/etc`

* `/home`

   Informations sur les utilisateurs et les groupes.

* `/libs`

    Bibliothèques et définitions appartenant au noyau d’AEM. Les sous-dossiers dans `/libs` représentent les fonctionnalités d’AEM d’usine telles que la recherche ou la réplication. Le contenu de `/libs` ne doit pas être modifié car il affecte le fonctionnement d’AEM. Les fonctionnalités spécifiques à votre site web doivent être développées sous `/apps` (voir [Personnalisation de composants et d’autres éléments](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Espace de travail temporaire.

* `/var`

   Fichiers qui évoluent et sont mis à jour par le système, tels que les journaux d’audit, les statistiques, la gestion des événements.

## Environnements {#environments}

Avec AEM, un environnement de production se compose souvent de deux types d’instances différents : an [Création et instances de publication](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Le dispatcher {#the-dispatcher}

Le dispatcher est un outil Adobe qui sert à la mise en cache et/ou l’équilibrage de charge. Vous trouverez plus d’informations sous [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en).

## FileVault (système de révision source) {#filevault-source-revision-system}

FileVault fournit à votre référentiel JCR des fonctions de mappage du système de fichiers et de gestion des versions. Il peut être utilisé pour gérer AEM projets de développement avec une prise en charge complète du stockage et de la gestion des versions du code de projet, du contenu, des configurations, etc., dans les systèmes de contrôle de version standard (par exemple, Subversion).

Voir [Outil FileVault](/help/sites-developing/ht-vlttool.md) documentation pour plus d’informations.

## Workflows {#workflows}

Votre contenu est souvent soumis à des processus organisationnels, y compris des étapes telles que l’approbation et la validation par différents participants. Ces processus peuvent être représentés sous forme de workflows, [définis et développés dans AEM](/help/sites-developing/workflows-models.md), puis appliqué à la variable [pages de contenu appropriées](/help/sites-administering/workflows.md) ou [ressources numériques](/help/assets/assets-workflow.md) selon les besoins.

Le moteur de workflow permet de gérer l’implémentation de vos workflows et leur application ultérieure dans votre contenu.

## Gestion multisite {#multi-site-management}

Multi Site Manager (MSM) permet de gérer facilement plusieurs sites web partageant du contenu commun. MSM vous permet de définir des relations entre les sites, de sorte que les modifications de contenu d’un site soient automatiquement répliquées sur d’autres sites.

Par exemple, les sites web sont souvent proposés dans plusieurs langues à l’intention d’un public international. Lorsque le nombre de sites dans la même langue est faible (de trois à cinq), un processus manuel de synchronisation du contenu entre les sites est possible. Cependant, lorsque le nombre de sites augmente ou que plusieurs langues sont impliquées, il devient plus efficace d’automatiser le processus.

* Gérez efficacement différentes versions linguistiques d’un site web.
* Mettre automatiquement à jour un ou plusieurs sites en fonction d’un site source :

   * Application d’une structure de base commune et utilisation de contenu commun sur plusieurs sites.
   * Optimiser l’utilisation des ressources disponibles.
   * Maintenir un aspect commun.
   * Concentrez-vous sur la gestion du contenu qui diffère entre les sites.

Pour plus d’informations, voir [Multi Site Manager](/help/sites-administering/msm.md).
