---
title: Contribution à AEM
seo-title: Contributing to AEM
description: AEM est développé selon des méthodologies éprouvées couramment pratiquées dans d’importants projets open source
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 67%

---

# Contribution à AEM{#contributing-to-aem}

## Méthodologie de développement {#development-methodology}

AEM est développé selon des méthodologies éprouvées couramment pratiquées dans d’importants projets open source. De nombreux éléments de base de la pile technologique d’AEM sont en fait maintenus en tant que projets open source actifs, tels que Sling et Jackrabbit, qui ont contribué à The Apache Software Foundation. Cette approche collaborative se retrouve dans AEM où vous êtes encouragé à utiliser les listes de diffusion et les forums en ligne pour interagir directement avec l’équipe de développement.

Si vous contribuez aux développement de composants d’AEM, vous devez vous familiariser avec AEM et communiquer avec l’équipe en place comme vous le feriez si vous preniez part à un projet open source.

## Expérience requise {#required-experience}

Le protocole HyperText Transfer Protocol (HTTP) est au cœur de tous nos projets. Par conséquent, avant de contribuer à AEM, vous devez maîtriser HTTP, idéalement dans la mesure où vous devez être capable d’écrire votre propre implémentation Java d’un serveur HTTP multithread avec un pool de threads. Par ailleurs, vous devez comprendre parfaitement le comportement HTTP/1.1 keep-alive et avoir une connaissance approfondie des interactions serveur/client avec JavaScript, en particulier le type d’interaction asynchrone représenté par AJAX.

Étant donné que le dynamisme des pages et le contenu interactif sont déterminants pour l’expérience WM, il est impératif que vous maîtrisiez le modèle d’objet de document et son potentiel pour la manipulation programmatique en réponse aux événements. Vous devez par exemple connaître la manipulation DOM en temps réel et le comportement de glisser-déposer sur plusieurs documents de navigateur (par exemple, en utilisant des iframes).

Au plus haut niveau, vous devez maîtriser les concepts suivants :

* le protocole[HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (de préférence [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* CSS (Cascading Style Sheets)
* XML (Extensible Markup Language)
* Les tendances en matière de conception AJAX (Asynchronous JavaScript and XML)
* JSON (JavaScript Object Notation)
* le modèle d’objet de document
* les interactions avec et sans état
* [Identificateurs de ressources uniformes](https://www.ietf.org/rfc/rfc2396.txt)
* les cookies de navigateur
* et d’autres concepts modernes de développement web

La pile technologique d’Adobe Experience Manager est basée sur la variable [Apache Felix](https://felix.apache.org/) Conteneur OSGI avec [Apache Sling](https://sling.apache.org/site/index.html) structure web et incorpore un référentiel de contenu Java ([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)) en fonction de [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Vous devez vous familiariser avec ces projets individuels, ainsi qu’avec tous les autres composants open source (par exemple, Apache Lucene) utilisés dans le domaine où vous avez l’intention d’apporter une contribution.

## Connaissances exclusives {#tribal-knowledge}

Certains concepts et principes directeurs sont profondément enracinés dans l’ancienne culture du développement. Cette section énumère quelques-uns des problèmes profondément ancrés que vous devez connaître.

### Tout est contenu {#everything-is-content}

Le contenu n’inclut pas seulement les données que l’application web conserve. Le code du programme, les bibliothèques, les scripts, les modèles, le HTML, CSS, les images et les artefacts de tous types, tout et n’importe quoi est conservé dans le référentiel de contenu et importé/exporté sous la forme de modules via le gestionnaire de modules et le partage de modules.

### David’s Model {#david-s-model}

La façon dont le contenu doit être modélisé dans un référentiel de contenu Java nécessite une approche totalement différente de ce qui est courant dans le secteur du développement logiciel pour la modélisation de données dans le monde relationnel. Le guide [David’s Model: A guide for content modeling](https://wiki.apache.org/jackrabbit/DavidsModel) est une lecture incontournable pour tout débutant dans la gestion de contenu selon l’approche JCR.

### Conception RESTful {#restfulness}

L’approche REST est profondément ancrée dans tous nos projets. Cela signifie, entre autres, que nous évitons les interactions avec état et appliquons le principe que les URI sont des adresses définitives pour le contenu et les services.

REST (REpresentational State Transfer) fait référence à l’architecture logicielle sur laquelle le World Wide Web est basé. Il décrit les éléments clés qui font fonctionner le web et fournit ainsi un ensemble de principes pour la conception d’un logiciel basé sur le web. Lors de la conception d’une API à utiliser sur le Web, il est donc logique de respecter ces &quot;bonnes pratiques&quot;.

Dans la mesure où REST offre une approche que nous suivons dans nombreux de nos projets, vous devriez vous attacher à maîtriser les principes de la conception RESTful. La dissertation de [Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) est un excellent point de départ.

### Résolution de requête Sling {#sling-request-resolution}

Dans AEM, il est impératif de cerner la relation entre les requêtes entrantes et le comportement du contenu et des applications, de comprendre la structure du contenu dans le référentiel de contenu et de savoir où AEM recherche la logique de l’application pour gérer la requête. Renseignez-vous sur la [décomposition d’URL Apache Sling](https://sling.apache.org/site/url-decomposition.html) et la façon dont elle applique l’approche architecturale REST et ses contraintes d’un système sans état, cachable et en couches.

En matière de résolution de requête Apache Sling, il faut comprendre comment les requêtes sont essentiellement mappées à une ressource spécifique dans le référentiel de contenu, comment les propriétés supplémentaires de la requête, ainsi que les propriétés de ces objets, déterminent le code d’application à afficher et comment le code dans /apps remplace le code dans /libs.

### Démarrage rapide {#quickstart}

Pas de troisième étape : pour installer et exécuter, il suffit de télécharger et de double-cliquer sur le fichier JAR Quickstart. Il n’y a pas de troisième étape. Toute fonctionnalité facultative supplémentaire ne devrait rien nécessiter hormis l’installation du module approprié à partir du partage de modules.

Petite taille du fichier Quickstart : conservez la taille minimale du fichier JAR Quickstart. Utilisez les bibliothèques de manière intelligente et optimisée, en déplaçant les fonctionnalités facultatives vers le partage de modules.

Temps de démarrage plus rapide : lorsque vous effectuez une modification susceptible de se répercuter sur le temps de démarrage, assurez-vous de l’écourter et non pas le contraire.

### Lean et Mean {#lean-and-mean}

Nous privilégions le code et les projets qui sont légers, petits, rapides et élégants. « Assez bien » n’est pas suffisant.

Réutilisation du code : notre architecture de produits basée sur OSGi et notre approche « tout est contenu » signifie que nous nous donnons plus d’occasions de réutiliser le code et les artefacts. Nous essayons d’appliquer ce principe dans toute la mesure du possible pour développer des fonctionnalités lean-and-mean.

Couplage lâche : nous privilégions les interactions à couplage faible à des dépendances étroites et des échanges trop serrés non souhaités. Le couplage lâche permet également une réutilisation du code.

### Ne pas casser les démos {#don-t-break-the-demo}

Familiarisez-vous avec les scripts de démonstration et les fonctionnalités de produit qui s’affichent le plus souvent dans les démonstrations. Sachez que rien de ce que vous codez ne doit endommager une fonctionnalité de « script de démonstration ». Le produit de base doit toujours être prêt pour démo, même en phase de développement.

### Une conception qui privilégie la fiabilité {#design-for-reliability}

Nous nous efforçons de concevoir et de coder les fonctionnalités sans qu’un bogue n’ai de lourdes répercussions. Par exemple, il faut éviter qu’un problème lié à un seul élément DOM empêche le rendu de toute une page. En d’autres termes : laisser ce qui doit être fatal l’être. Tout le reste doit être viable. Le produit doit être « indulgent ».

### Ce qui est anormal est normal {#abnormal-is-the-new-normal}

Ne dépendez pas des shutdown hooks, nettoyez au démarrage. Un arrêt anormal est un arrêt normal.

`shutdown == kill -9 == power outage`

### Se tenir prêt pour un clustering élastique {#be-ready-for-elastic-clustering}

Soyez toujours prêt pour la mise en grappe élastique, supposez toujours qu’il y a de la mise en grappe. En règle générale, le respect de tout ce qui réside dans le référentiel de contenu signifie une prise en charge de clustering intégré.

### Une conception avec une compatibilité ascendante {#design-for-backward-compatibility}

Rien de ce que vous codez ne doit endommager l’ancien code d’un client. Considérer uniquement `/libs` pour contenir le code de produit qui peut être mis à jour lors d’une mise à niveau. Le `/apps` du référentiel est le code du projet et la variable `/etc` contient des configurations personnalisées qui doivent être conservées. En règle générale, ne remplacez rien dans `/apps`, `/content` et `/home`. Après une mise à niveau, l’ancien code de projet, les configurations et le contenu doivent continuer à fonctionner comme avant la mise à niveau.

Une conception prenant en charge la rétrocompatibilité garantit également que l’expérience de mise à niveau correspond à la simplicité de l’installation initiale. Il suffit en principe d’arrêter AEM, de remplacer le fichier JAR Quickstart et de redémarrer AEM. Avec une base d’installation en pleine expansion, une efficace optimale est un avantage de plus en plus recherché.

Même si les API existantes peuvent et doivent être rendues obsolètes lorsqu’une fonctionnalité plus récente et plus performante les remplace, toutes les API rendues publiques dans une version 5.x précédente doivent rester fonctionnelles, car elles peuvent être utilisées dans le code d’application personnalisé. Aucune API de ce type ne doit être supprimée.

La rétrocompatibilité doit également être envisagée pour la cohérence générale de la structure du contenu et de l’expérience client.

## Concepts de base {#core-concepts}

**Instance de création** - En règle générale, pour des raisons de sécurité, de gouvernance et autres, un site de production divise les instances d’AEM en instances d’auteur et de publication. Pour plus d’informations sur l’architecture de déploiement (y compris les instances d’auteur/de publication), consultez la documentation sur les instances d’AEM.

**Mise en cache, friture et cuisson** - Traditionnellement, les concepts de cuisson et de friture sont une distinction importante entre les différents systèmes de gestion de contenu web. Dans le jargon CMS, le « baking » fait référence au concept de validation de données dans des fichiers statiques au moment de la publication, tandis que le « frying » fait référence au concept de traitement des données pour la présentation finale au moment de la requête (juste à temps).

**Mise en grappe et équilibrage de charge** - Pour accroître la disponibilité et améliorer les performances d’un environnement de production, il est courant de combiner plusieurs instances d’auteur et/ou de publication (en grappes), soit en les mettant à la disposition de différents groupes d’utilisateurs, soit en les équilibrant par la charge derrière une configuration de Dispatcher.

Il est également possible de combiner plusieurs instances du référentiel de contenu pour créer une *haute disponibilité* Solution JCR, qui peut ensuite être intégrée à votre solution AEM afin de maximiser la protection contre les défaillances matérielles et logicielles. Consultez [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) pour plus d’informations.

**Composant** - Dans AEM, un composant est un type d’objet, dont les instances peuvent généralement être créées en les faisant glisser à partir du sidekick, par exemple. Ainsi, par exemple, les composants prêts à l’emploi fournis avec AEM incluent les composants Texte, Titre, Nuage de balises, Carrousel, Image et Liste, tous disponibles depuis le Sidekick au moment de l’exécution.

**Outil de recherche de contenu** - En mode de création, l’outil de recherche de contenu est un panneau spécial (cadre) situé à gauche de la page qui, selon l’onglet que vous sélectionnez en haut, affiche des listes d’images, de documents, de ressources de Flash, de pages, de paragraphes ou de ressources de référentiel que vous pouvez faire glisser de l’outil de recherche de contenu vers la page sur laquelle vous travaillez (à droite).

**Ressources numériques** - Dans AEM, les ressources numériques sont (généralement) des images et des fichiers multimédias enrichis. Pour plus d’informations, voir Utilisation des actifs numériques dans DAM.

**Dispatcher** - Dispatcher est à la fois un outil de mise en cache et d’équilibrage de charge, et fournit certaines protections de sécurité.

**Widgets ExtJS** - La plupart des éléments d’interface utilisateur d’AEM utilisent ExtJS, qui est une bibliothèque de widgets tiers écrite en JavaScript. ExtJS offre des widgets d’IU personnalisables et haute performance ainsi qu’un modèle de composant bien conçu et extensible.

**JCR, référentiel de contenu Java** - La spécification Java Content Repository (JSR-283) fournit à la fois un modèle de données abstrait et une interface de programmation d’application pour réaliser un référentiel de données NoSQL massivement évolutif qui combine les fonctionnalités d’un système de fichiers et d’une base de données d’objets. Bien que vous n’ayez pas besoin de comprendre JSR-283 en détail, prenez le temps de vous familiariser avec les fonctionnalités de base de la spécification JCR et le modèle de données qui la sous-tend, car JCR est ce qui rend possible l’approche « tout est contenu ».

En substance, JCR est un système de nœuds et de propriétés, dans lequel les nœuds peuvent hériter des autres nœuds et tout le contenu est stocké en tant que *valeurs* de propriété. Notez qu’en plus de l’héritage ordinaire, JCR est associé à un concept de nœuds « mixin », ce qui permet la modélisation de l’héritage multiple.

JCR possède un certain nombre de types de nœuds prédéfinis et de types de propriétés, mais en général le système de typage est assez flexible et (d’ailleurs) l’une des forces de JCR est qu’il permet de facilement stocker/gérer le contenu structuré et non structuré. C’est-à-dire que JCR peut prendre en charge des données hautement structurées, mais accepte également des structures de données dynamiques arbitraires sans contraintes de schéma.

L’API Java de JavaDoc pour JCR est disponible [ici](https://jackrabbit.apache.org/jcr/jcr-api.html).

Avant de lire la spécification JavaDoc ou JCR elle-même, vous pouvez consulter [cette explication d’expert](/help/sites-developing/the-basics.md#java-content-repository) sur JCR, telle qu’elle est implémentée par Adobe Experience Services.

**Multi-site Manager (MSM)** - La fonctionnalité MSM d’AEM aide les clients à gérer le contenu multilingue et multinational, ce qui leur permet d’équilibrer la valorisation de marque centralisée avec le contenu localisé.

**OSGi** - OSGi est la technologie d’exécution basée sur les services qui constitue la base du développement Java modulaire dans AEM. C’est un framework qui fournit non seulement un environnement de chargement de classes hautement dynamique (et sécurisé) pour les ressources de code (appelébundles), mais aussi un contrôle complet de la visibilité et du cycle de vie des différents services exposés par des bundles. Un registre de services fournit un modèle de coopération pour les bundles qui tient compte de la dynamique du cycle de vie (et des exigences de version). OSGi résout de nombreux problèmes que les serveurs d’applications étaient censés résoudre, mais de manière légère et hautement dynamique. Cela permet, par exemple, de déployer à chaud des services (et de rendre le nouveau code immédiatement disponible sans redémarrer le serveur).

**Parsys, système de paragraphes** - Le système de paragraphes (parsys) est un composant composé qui permet aux auteurs d’ajouter des composants de différents types à une page et qui contient d’autres composants de paragraphe. Chaque type de paragraphe est représenté en tant que composant. Le système de paragraphe lui-même est également un composant, qui contient les autres composants de paragraphe.

**Microkernel** - Chaque espace de travail du référentiel peut être configuré séparément pour stocker ses données par le biais d’un micro-noyau spécifique (une classe qui gère la lecture et l’écriture des données). De même, le magasin de versions à l’échelle du référentiel peut également être configuré indépendamment pour utiliser un micro-noyau particulier. Plusieurs micro-noyaux différents sont disponibles et capables de stocker des données dans une variété de formats de fichiers ou de bases de données relationnelles. (Par exemple, il existe des gestionnaires de persistance pour MongoDB, DB2 ou Oracle). Le micro-noyau par défaut pour AEM est TarMK (voir plus loin).

**Instance de publication** - Pour des raisons de sécurité, de gouvernance et autres, un site de production divise généralement les instances d’AEM en instances d’auteur et de publication. Pour plus d’informations sur l’architecture de déploiement (y compris les instances d’auteur/de publication), consultez la documentation sur les instances d’AEM.

**Quickstart** - Contrairement à de nombreux autres programmes, vous installez AEM en utilisant un seul fichier JAR à extraction automatique &quot;Quickstart&quot;. Lorsque vous double-cliquez sur le fichier JAR pour la première fois, tout ce dont vous avez besoin est automatiquement installé. Le fichier JAR Quickstart comprend tous les fichiers requis pour le référentiel CRX (y compris les fonctions administratives), les services de référentiel virtuel, les services d’indexation et de recherche, les services de workflow, la sécurité et un serveur web, ainsi que le CQ Servlet Engine (CQSE) et les services AEM. Il n’y a pas d’autres fichiers à installer : Quickstart est autonome.

La première fois que vous lancez Quickstart, il crée en arrière-plan un référentiel complet compatible JCR, ce qui peut prendre plusieurs minutes. Après ce premier démarrage, les démarrages ultérieurs sont beaucoup plus rapides car l’infrastructure du référentiel a déjà été définie.

De nombreuses options de démarrage (telles que le numéro de port actif et le fait d’indiquer si l’instance AEM en question doit être une instance de publication ou une instance de création, et bien d’autres) peuvent être contrôlées en renommant le fichier Quickstart de manière appropriée. Pour voir une liste de ces options, exécutez le fichier JAR avec &quot;-help&quot; dans la ligne de commande :

```shell
java -jar <quickstartfilename>.jar -help
```

**Agents de réplication** - Les agents de réplication sont essentiels pour AEM en tant que mécanisme utilisé pour publier (activer) le contenu d’un auteur vers un environnement de publication ; vider le contenu du cache de Dispatcher ; renvoyer le contenu généré par l’utilisateur (par exemple, les entrées de formulaire) de l’environnement de publication vers l’environnement de création.

**Génération de modèles automatique** - Avec la génération de modèles automatique, vous pouvez créer un formulaire (un modèle automatique) avec des champs qui reflètent la structure souhaitée pour vos pages, puis utiliser ce formulaire pour créer facilement des pages en fonction de cette structure.

**Segmentation** - Les visiteurs du site ont des intérêts et des objectifs différents lorsqu’ils se rendent sur un site. Le fait de comprendre ces objectifs et de satisfaire à leurs attentes est un important facteur de réussite en matière de marketing en ligne. La segmentation permet d’y parvenir en analysant et en profilant le visiteur :

**Sidekick** - Le sidekick est une fenêtre flottante de type palette qui s’affiche sur la page modifiable, à partir de laquelle vous pouvez faire glisser de nouveaux composants et exécuter les actions qui s’appliquent à la page.

**SiteCatalyst** - SiteCatalyst offre aux marketeurs un emplacement unique où mesurer, analyser et optimiser les données intégrées de toutes les initiatives en ligne sur plusieurs canaux marketing. Vous pouvez utiliser Adobe SiteCatalyst pour analyser les données des sites web AEM.

**Stockage Tar (TarMK)** - TarMK est le système de persistance par défaut dans AEM. Bien qu’AEM puisse être configuré pour utiliser un autre système de persistance (tel que MongoDB), TarMK présente certains avantages en ce sens qu’il est optimisé pour les utilisations classiques de JCR (donc très rapide), utilise un format de données standard et peut être sauvegardé rapidement et facilement.

**Modèle** - Dans AEM, un modèle spécifie un type de page particulier. Il définit la structure d’une page (tout en spécifiant généralement une image miniature et diverses propriétés). Vous pouvez, par exemple, disposer de modèles distincts pour des pages de produit, des plans de site et des coordonnées de contact.

**Workflow** - Le système de workflow AEM permet la création de processus automatisés impliquant des pages ou des ressources.
