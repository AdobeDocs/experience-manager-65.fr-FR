---
title: Contribution à AEM
description: AEM est développé selon des méthodologies éprouvées et utilisées couramment pour de grands projets open source.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2635'
ht-degree: 98%

---

# Contribution à AEM{#contributing-to-aem}

## Méthodologie de développement {#development-methodology}

AEM est développé selon des méthodologies éprouvées et utilisées couramment pour de grands projets open source. De nombreux éléments de base de la pile technologique d’AEM sont en fait maintenus en tant que projets open source actifs, tels que Sling et Jackrabbit, qui ont contribué à l’Apache Software Foundation. L’un des principaux aspects de l’esprit d’AEM est que nous vous encourageons à utiliser les listes de diffusion et les forums en ligne disponibles pour échanger directement avec l’équipe de développement.

Si vous contribuez à des composants d’AEM, familiarisez-vous avec AEM comme vous le feriez lorsque vous contribuez à un projet open source, et communiquez avec l’équipe principale existante comme vous le feriez lorsque vous avez l’intention de contribuer à un projet de ce type.

## Expérience requise {#required-experience}

Le protocole HyperText Transfer Protocol (HTTP) est au cœur de tous nos projets. Par conséquent, avant de contribuer à AEM, vous devez maîtriser HTTP. Idéalement, vous devez être capable d’écrire votre propre implémentation Java™ d’un serveur HTTP multithread avec un pool de threads. Vous devez également maîtriser le comportement de persistance HTTP/1.1 et posséder une connaissance approfondie des interactions côté serveur/client avec JavaScript, en particulier du style asynchrone d’interaction représenté par AJAX.

Étant donné que le dynamisme des pages et le contenu interactif sont déterminants pour l’expérience WM, il est impératif que vous maîtrisiez le modèle d’objet de document et son potentiel pour la manipulation programmatique en réponse aux événements. Vous devez, par exemple, avoir des connaissances en matière de manipulation DOM en temps réel et de comportement de glisser-déposer sur plusieurs documents de navigateur (à l’aide d’iframes, par exemple).

Au plus haut niveau, vous devez maîtriser les concepts suivants :

* le protocole[HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (de préférence [HTML5](https://html.spec.whatwg.org/))
* les feuilles de style en cascade
* Extensible Markup Language (XML)
* les modèles de conception JavaScript et XML (AJAX) asynchrones
* JavaScript Object Notation (JSON)
* le modèle d’objet de document
* les interactions avec ou sans état
* les [Uniform Resource Identifiers (URI)](https://www.ietf.org/rfc/rfc2396.txt)
* les cookies de navigateur
* et d’autres concepts de développement web modernes

La pile technologique d’Adobe Experience Manager est basée sur le conteneur OSGI [Apache Felix](https://felix.apache.org/documentation/index.html) avec le framework web [Apache Sling](https://sling.apache.org/index.html). Elle intègre un référentiel de contenu Java™ ([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)) basé sur [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html). Vous devez vous familiariser avec ces projets particuliers, ainsi qu’avec tous les autres composants open source (par exemple, Apache Lucene) utilisés dans le domaine où vous avez l’intention d’apporter une contribution.

## Connaissances internes {#tribal-knowledge}

Certains concepts et principes directeurs sont profondément enracinés dans l’ancienne culture du développement. Cette section énumère quelques-uns des problèmes profondément ancrés que vous devez connaître.

### Tout est du contenu. {#everything-is-content}

Le contenu n’inclut pas seulement les données que l’application web conserve. Le code de programme, les bibliothèques, scripts, modèles, HTML, CSS, images et artefacts de toutes sortes, absolument tout est conservé dans le référentiel de contenu et importé/exporté sous la forme de packages via le gestionnaire de modules et le partage de modules.

### Modèle de David {#david-s-model}

La façon dont le contenu doit être modélisé dans un référentiel de contenu Java™ nécessite une approche totalement différente de la pratique courante dans le secteur du développement logiciel pour la modélisation de données dans le monde relationnel. Le guide [David’s Model: A guide for content modeling](https://wiki.apache.org/jackrabbit/DavidsModel) est une lecture incontournable pour tout débutant dans la gestion de contenu selon l’approche JCR.

### RESTfulness {#restfulness}

L’approche REST est profondément ancrée dans tous nos projets. Cela signifie, entre autres, d’éviter les interactions avec état et de garder à l’esprit que les URI sont des adresses définitives pour le contenu et les services.

REST (REpresentational State Transfer) fait référence à l’architecture logicielle sur laquelle le World Wide Web est basé. Il décrit les éléments clés qui font fonctionner le web et fournit ainsi un ensemble de principes pour la conception d’un logiciel basé sur le web. Lors de la conception d’une API à utiliser sur le Web, il est donc logique de suivre ces « bonnes pratiques ».

REST offre une approche que nous suivons dans nombreux de nos projets, et que vous devriez suivre également pour maîtriser les principes de la conception RESTful. Un bon point de départ est la [thèse de Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Résolution des requêtes Sling {#sling-request-resolution}

Dans AEM, il est impératif de cerner la relation entre les requêtes entrantes et le comportement du contenu et des applications, de comprendre la structure du contenu dans le référentiel de contenu et de savoir où AEM recherche la logique de l’application pour gérer la requête. Découvrez la [décomposition de l’URL Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html) et la manière dont elle applique le style architectural REST et ses contraintes système sans état, pouvant être mises en cache et superposées.

Les aspects clés de la résolution des requêtes d’Apache Sling sont : la manière dont les requêtes sont principalement mappées à une ressource spécifique dans le référentiel de contenu, la manière dont les propriétés supplémentaires de la requête, ainsi que les propriétés de ces objets de contenu, déterminent le code d’application appelé pour le rendu du contenu, et la manière dont le code dans /apps remplace le code dans /libs.

### Démarrage rapide {#quickstart}

Pas de troisième étape : pour installer et exécuter, il suffit de télécharger et de double-cliquer sur le fichier JAR Quickstart. Il n’y a pas de troisième étape. Toute fonctionnalité facultative supplémentaire ne doit nécessiter rien de plus que l’installation du package approprié à partir du partage de modules.

Petite taille du fichier Quickstart : conservez la taille minimale du fichier JAR Quickstart. Utilisez les bibliothèques de manière intelligente et optimisée en déplaçant les fonctionnalités facultatives vers le partage de modules.

Démarrage plus rapide : lorsque vous effectuez une modification susceptible d’affecter le temps de démarrage, veillez à ce qu’il soit plus court, et non plus long.

### Simple et efficace {#lean-and-mean}

Nous privilégions le code et les projets qui sont légers, petits, rapides et élégants. « Assez bien » n’est pas assez bien.

Réutilisation du code : notre architecture de produits basée sur OSGi et notre approche « tout est du contenu » signifie que nous nous donnons plus d’occasions de réutiliser le code et les artefacts. Nous essayons d’en profiter chaque fois que possible pour que les fonctionnalités restent simples et efficaces.

Couplage lâche : nous privilégions les interactions à couplage faible à des dépendances étroites et des échanges trop serrés non souhaités. Le couplage faible permet également de réutiliser du code.

### Ne pas interrompre la démonstration {#don-t-break-the-demo}

Familiarisez-vous avec les scripts de démonstration et les fonctionnalités des produits qui sont le plus souvent présentés dans les démos. Sachez que rien de ce que vous codez ne doit nuire à une fonctionnalité de « script de démonstration ». Le produit principal doit toujours être prêt pour une démonstration, même pendant le développement.

### Conception pour la fiabilité {#design-for-reliability}

Nous nous efforçons de concevoir et de coder des fonctionnalités de manière réactive, de sorte (par exemple) qu’un problème avec un seul élément DOM n’entraîne pas le rendu d’une page entière. En d’autres termes : laisser ce qui doit être fatal l’être. Tout le reste doit être viable. Rendez le produit « indulgent ».

### L’anormal est la nouvelle norme {#abnormal-is-the-new-normal}

Ne dépendez pas des points d&#39;arrêt, assurez-vous de procéder au nettoyage au démarrage. Un arrêt anormal est un arrêt normal.

`shutdown == kill -9 == power outage`

### Se tenir prêt pour un clustering élastique {#be-ready-for-elastic-clustering}

Il est essentiel de se tenir prêt pour un clustering élastique ; supposez toujours qu’il y a un clustering. En règle générale, le respect de tout ce qui réside dans le référentiel de contenu signifie une prise en charge de clustering intégré.

### Une conception avec une compatibilité ascendante {#design-for-backward-compatibility}

Rien de ce que vous codez ne doit endommager l’ancien code d’un client. N’utilisez que la `/libs` pour stocker le code du produit qui peut être mis à jour pendant une mise à niveau. La section `/apps` du référentiel est le code du projet et la section `/etc` contient des configurations personnalisées à conserver. En règle générale, ne remplacez rien dans `/apps`, `/content` et `/home`. Après une mise à niveau, l’ancien code de projet, les configurations et le contenu doivent continuer à fonctionner comme avant la mise à niveau.

Une conception prenant en charge la rétrocompatibilité garantit également que l’expérience de mise à niveau correspond à la simplicité de l’installation initiale. Il suffit en principe d’arrêter AEM, de remplacer le fichier JAR de démarrage rapide et de redémarrer AEM. Avec une base d’installation en pleine expansion, une mise à niveau efficace est un avantage de plus en plus recherché.

Même si les API existantes peuvent et doivent être rendues obsolètes lorsqu’une fonctionnalité plus récente et plus performante les remplace, toutes les API rendues publiques dans une version 5.x précédente doivent rester fonctionnelles, car elles peuvent être utilisées dans le code d’application personnalisé. Aucune API de ce type ne doit être supprimée.

il convient également de garder à l’esprit la rétrocompatibilité en ce qui concerne la cohérence générale de la structure de contenu et de l’expérience utilisateur.

## Concepts de base {#core-concepts}

**Instance de création** : généralement, pour des raisons de sécurité, de gouvernance et autres, un site de production divise les instances d’AEM en instances de création et de publication. Pour plus d’informations sur l’architecture de déploiement (y compris les instances de création et de publication), consultez la documentation relative aux instances AEM.

**Caching, frying et baking** - Traditionnellement, les concepts de baking et de frying sont une distinction importante entre différents systèmes de gestion de contenu Web. Dans le jargon CMS, le « baking » fait référence au concept de validation de données dans des fichiers statiques au moment de la publication, tandis que le « frying » fait référence au concept de traitement des données pour la présentation finale au moment de la requête (c’est-à-dire juste à temps).

**Clustering et équilibrage de charge** : pour augmenter la disponibilité et améliorer les performances d’un environnement de production, il est courant de combiner plusieurs instances de création et/ou de publication (en clusters), soit en les mettant à la disposition de différents groupes d’utilisateurs et utilisatrices, soit en équilibrant leur charge derrière une configuration du dispatcher.

Il est également possible de combiner plusieurs instances du référentiel de contenu pour créer une solution JCR *haute disponibilité*, laquelle peut ensuite être intégrée à votre solution AEM pour optimiser la protection contre les défaillances matérielles et logicielles. Consultez [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) pour plus d’informations.

**Composant** - Dans AEM, un composant est un type d’objet dont les instances peuvent généralement être créées en les faisant glisser depuis le sidekick, par exemple. Ainsi, par exemple, les composants prêts à l’emploi fournis avec AEM incluent les composants Texte, Titre, Nuage de balises, Carrousel, Image et Liste, tous disponibles depuis le sidekick au moment de l’exécution.

**Outil de recherche de contenu** - En mode création, l’outil de recherche de contenu est un panneau spécial (frame) sur le côté gauche de la page qui, selon l’onglet que vous sélectionnez en haut, affiche des listes d’images, de documents, des éléments Flash, des pages, des paragraphes ou des ressources de référentiel que vous pouvez faire glisser de l’outil de recherche de contenu vers la page dans laquelle vous travaillez (sur la droite).

**Eléments numériques** Dans AEM, les ressources numériques sont (généralement) des images et des fichiers multimédias. Pour plus d’informations, consultez Utilisation des ressources numériques dans la gestion des ressources numériques.

**Dispatcher** : le Dispatcher est un outil de mise en cache et d’équilibrage de charge qui fournit certaines mesures de sécurité.

**Widgets ExtJS** : la plupart des éléments d’interface utilisateur d’AEM utilisent ExtJS, qui est une bibliothèque de widgets tiers écrite en JavaScript. ExtJS offre des widgets d’IU personnalisables et haute performance ainsi qu’un modèle de composant bien conçu et extensible.

**JCR, référentiel de contenu Java™** : la spécification de référentiel de contenu Java™ (JSR-283) fournit à la fois un modèle de données abstrait et une interface de programmation d’application pour élaborer un référentiel de données NoSQL massivement évolutif qui combine les fonctionnalités d’un système de fichiers et d’une base de données objet. Bien que vous n’ayez pas besoin de comprendre JSR-283 en détail, vous devriez prendre le temps de vous familiariser avec les fonctionnalités de base de JCR et le modèle de données qui le sous-tend, car JCR est ce qui rend possible la philosophie « tout est contenu » d’AEM.

En substance, JCR est un système de nœuds et de propriétés, dans lequel les nœuds peuvent hériter des autres nœuds et tout le contenu est stocké en tant que *valeurs* de propriété. Notez qu’en plus de l’héritage ordinaire, JCR autorise un concept de nœuds « mixin », ce qui permet la modélisation de l’héritage multiple.

JCR possède plusieurs types de nœuds prédéfinis et types de propriétés, mais en général le système de typage est assez flexible et (d’ailleurs) l’une des forces de JCR est qu’il permet de facilement stocker/gérer le contenu structuré et non structuré. En d’autres termes, JCR peut s’adapter à des données hautement structurées, mais peut également s’adapter à des structures de données dynamiques arbitraires sans contraintes de schéma.

L’API Java™ de JavaDoc pour JCR est disponible [ici](https://jackrabbit.apache.org/jcr/jcr-api.html).

Avant de lire la spécification JavaDoc ou JCR elle-même, vous pouvez consulter [cette explication d’expert](/help/sites-developing/the-basics.md#java-content-repository) sur JCR, telle qu’elle est implémentée par Adobe Experience Services.

**Multi-Site Manager (MSM)** - La fonctionnalité MSM d’AEM aide les clients à gérer le contenu multilingue et multinational pour uniformiser leur branding centralisé avec du contenu localisé.

**OSGi** : OSGi est la technologie d’exécution orientée services qui constitue la base du développement Java™ modulaire dans AEM. C’est un framework qui fournit non seulement un environnement de chargement de classes hautement dynamique (et sécurisé) pour les ressources de code (appelés bundles), mais aussi un contrôle complet de la visibilité et du cycle de vie des différents services exposés par des bundles. Un registre de services fournit un modèle de coopération pour les bundles qui tient compte de la dynamique du cycle de vie (et des exigences de version). OSGi résout de nombreux problèmes que les serveurs d’applications étaient censés résoudre, mais de manière légère et très dynamique, ce qui permet, par exemple, de déployer à chaud des services (rendant le nouveau code immédiatement disponible sans redémarrer le serveur).

**Parsys, système de paragraphes** - Le système de paragraphe (parsys) est un composant composé qui permet aux auteurs d’ajouter des composants de différents types à une page et qui contient tous les autres composants de paragraphe. Chaque type de paragraphe est représenté en tant que composant. Le système de paragraphes lui-même est également un composant, qui contient les autres composants de paragraphe.

**Microkernel** - Chaque espace de travail du référentiel peut être configuré séparément pour stocker ses données via un micro-noyau spécifique (classe qui gère la lecture et l’écriture des données). De même, le magasin de versions à l’échelle du référentiel peut également être configuré indépendamment pour utiliser un micro-noyau particulier. Plusieurs micro-noyaux différents sont disponibles et capables de stocker des données dans de nombreux formats de fichiers ou de bases de données relationnelles. (Par exemple, il existe des gestionnaires de persistance pour MongoDB, DB2® ou Oracle). Le micro-noyau par défaut pour AEM est TarMK (voir plus loin).

**Instance de publication** - Généralement, pour des raisons de sécurité, de gouvernance et autres, un site d’exploitation divise les instances d’AEM en instances de création et de publication. Pour plus d’informations sur l’architecture de déploiement (y compris les instances de création et de publication), consultez la documentation relative aux instances AEM.

**Démarrage rapide** - Contrairement à beaucoup d’autres programmes, AEM s’installe à l’aide d’un seul fichier JAR auto-extractable Quickstart. Lorsque vous double-cliquez sur le fichier JAR pour la première fois, tout ce dont vous avez besoin est automatiquement installé. Le fichier JAR Quickstart comprend tous les fichiers requis pour le référentiel CRX (y compris les fonctions administratives), les services de référentiel virtuel, les services d’indexation et de recherche, les services de workflow, la sécurité et un serveur web, ainsi que le CQ Servlet Engine (CQSE) et les services AEM. Il n’y a pas d’autres fichiers à installer : Quickstart est autonome.

La première fois que vous lancez Quickstart, il crée en arrière-plan un référentiel complet compatible JCR, ce qui peut prendre plusieurs minutes. Après ce démarrage initial, les démarrages suivants sont beaucoup plus rapides, car l’infrastructure de référentiel a déjà été définie.

De nombreuses options de démarrage (telles que le numéro de port actif et le fait d’indiquer si l’instance AEM en question doit être une instance de publication ou une instance de création, et bien d’autres) peuvent être contrôlées en renommant le fichier Quickstart de manière appropriée. Pour afficher la liste des options à cet égard, exécutez le fichier JAR avec « -help » sur la ligne de commande :

```shell
java -jar <quickstartfilename>.jar -help
```

**Agents de réplication** : les agents de réplication sont au cœur d’AEM et forment le mécanisme utilisé pour Publier (activer) le contenu d’un auteur ou d’une autrice dans un environnement de publication, vider le contenu du cache du Dispatcher, renvoyer le contenu généré par l’utilisateur ou l’utilisatrice (par exemple, la saisie de formulaire) depuis l’environnement de publication vers l’environnement de création.

**Génération de modèles automatique** : grâce à la génération de modèles automatique, vous pouvez créer un formulaire (que l’on désigne sous le nom de modèle automatique) dont les champs représentent la structure souhaitée pour vos pages, puis l’utiliser afin de créer aisément des pages sur la base de cette structure.

**Segments** - Les visiteurs de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. Le fait de comprendre ces objectifs et de satisfaire à leurs attentes est un important facteur de réussite en matière de marketing en ligne. La segmentation permet d’y parvenir en analysant et en profilant le visiteur :

**Sidekick** - Le Sidekick est une fenêtre flottante de type palette visible dans la page modifiable à partir de laquelle les nouveaux composants peuvent être déplacés et les actions qui s’appliquent à la page peuvent être exécutées.

**SiteCatalyst** - SiteCatalyst offre aux spécialistes du marketing un seul endroit pour mesurer, analyser et optimiser les données intégrées de toutes les initiatives en ligne sur plusieurs canaux marketing. Vous pouvez utiliser Adobe SiteCatalyst pour analyser les données des sites Web AEM.

**Stockage Tar (TarMK)** - TarMK est le système de persistance par défaut dans AEM. Bien qu’AEM puisse être configuré pour utiliser un autre système de persistance (tel que MongoDB), TarMK présente certains avantages en ce sens qu’il est optimisé pour les utilisations classiques de JCR (donc rapide), utilise un format de données standard et peut être sauvegardé rapidement et facilement.

**Modèle** - Dans AEM, un modèle spécifie un type de page spécialisé. Il définit la structure d’une page (tout en spécifiant généralement une image miniature et diverses propriétés). Par exemple, vous pouvez avoir des modèles distincts pour les pages de produits, les plans de site et les coordonnées.

**Workflow** - Le système de Workflow AEM permet la création de processus automatisés associés à des pages ou des ressources.
