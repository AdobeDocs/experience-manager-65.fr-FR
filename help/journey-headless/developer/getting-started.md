---
title: Prise en main d’AEM Headless
description: Dans cette partie du parcours de développement découplé AEM, découvrez les conditions préalables relatives à AEM découplé.
source-git-commit: 919cef01470dd930884e97b15f2d40a38872c0d0
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 77%

---

# Prise en main d’AEM Headless {#getting-started}

Dans cette partie du [parcours de développement découplé](overview.md), découvrez ce qui est nécessaire pour démarrer votre propre projet avec AEM découplé.

## Un peu d’histoire...  {#story-so-far}

Dans le document précédent relatif au parcours concernant AEM découplé, [Découvrir le développement découplé du système de gestion de contenu](learn-about.md) (CMS), vous avez appris la théorie de base d’un CMS découplé et vous devez maintenant :

* comprendre les concepts de base et la terminologie de la diffusion de contenus en mode découplé ;
* comprendre pourquoi et quand le mode découplé est nécessaire ;
* savoir de manière plus large comment les concepts de découplage sont utilisés et interagissent.

Cet article s’appuie sur ces principes fondamentaux pour vous permettre de comprendre comment utiliser AEM lors de la mise en œuvre d’une solution découplée.

## Objectif {#objective}

Ce document est destiné à vous permettre de mieux comprendre AEM découplé dans le contexte de votre propre projet. Après l’avoir lu, vous devriez :

* comprendre les principes de base des fonctionnalités d’AEM découplé ;
* connaître les conditions préalables requises pour utiliser les fonctionnalités AEM découplées ;
* avoir conscience des niveaux d’intégration AEM découplé ;
* être en mesure de définir la portée de votre projet.

## Notions de base concernant AEM {#aem-basics}

Avant de pouvoir définir votre projet découplé dans AEM, il est important de comprendre certains concepts AEM de base.

### Instance d’auteur {#author}

Dans sa forme la plus simple, AEM se compose d’une instance d’auteur et d’une [instance de publication](#publish) qui fonctionnent conjointement pour créer, gérer et publier votre contenu.

Le contenu commence sur l’instance de création C’est là que les auteurs de contenu créent leur contenu. L’environnement de création propose différents outils pour que les auteurs puissent créer, organiser et réutiliser leur contenu.

### Instance de publication {#publish}

Une fois que le contenu a été créé sur l’instance d’auteur, il doit être publié pour permettre à d’autres services de l’utiliser. Une instance de publication contient tous les contenus publiés.

### Réplication {#replication}

La réplication consiste à transférer le contenu entre l’instance de création et celle de publication. Cette opération est effectuée automatiquement par AEM lorsqu’un auteur ou un autre utilisateur disposant des droits appropriés publie du contenu.

### Résumé des notions de base concernant AEM {#aem-basics-summary}

À son niveau le plus simple, la création d’expériences numériques dans AEM nécessite les étapes suivantes :

1. Vos auteurs de contenu créent votre contenu sans interface dans l’instance de création.
1. Lorsque ce contenu est prêt, il est répliqué sur l’instance de publication.
1. Il est ensuite possible d’appeler les API pour récupérer ce contenu.

AEM Headless tire parti de cette base technique en offrant des outils puissants pour gérer le contenu headless : [décrits dans la section suivante.](#aem-headless-basics)

## Concepts de base d’AEM découplé {#aem-headless-basics}

Les fonctionnalités d’AEM découplé sont basées sur quelques fonctionnalités essentielles. Elles sont expliquées en détail dans les parties ultérieures du parcours. Le plus important, pour le moment, c’est de savoir pour l’essentiel ce que font ces fonctionnalités et leur dénomination.

### Modèles de fragment de contenu {#content-fragment-models}

Les modèles de fragment de contenu définissent la structure des données et du contenu que vous créez et gérez dans AEM. Il s’agit en quelque sorte du squelette de votre contenu. Lorsque vous choisissez de créer du contenu, vos auteurs effectuent une sélection dans les modèles de fragment de contenu que vous définissez, ce qui les guide dans la création de contenu.

### Fragments de contenu {#content-fragments}

Les fragments de contenu permettent de concevoir, créer, organiser et publier du contenu indépendant des pages. Ils permettent de préparer le contenu prêt à être utilisé dans des emplacements multiples et sur plusieurs canaux.

Les fragments de contenu contiennent du contenu structuré et peuvent être diffusés au format JSON.

### API GraphQL et REST {#apis}

Pour modifier votre contenu en mode découplé, AEM propose deux API robustes.

* L’API GraphQL permet de créer des requêtes d’accès et de diffusion de fragments de contenu.
* L’API REST Assets permet de créer et de modifier des fragments de contenu (et d’autres ressources).

Vous découvrirez ces API et comment les utiliser dans une partie ultérieure du parcours AEM découplé. Pour plus d’informations, reportez-vous à la section [Ressources supplémentaires](#additional-resources) ci-dessous.

## Niveaux d’intégration en mode découplé {#integration-levels}

AEM prend en charge les modèles Découplé et Pile complète traditionnelle d’un CMS. Cependant, AEM offre non seulement ces deux choix exclusifs, mais aussi la possibilité de prendre en charge des modèles hybrides conjuguant les avantages de l’un et de l’autre, offrant ainsi une flexibilité inégalée pour votre projet découplé.

Pour vous assurer de bien comprendre le concept de découplage, ce parcours de développement découplé AEM se concentre sur le modèle purement découplé, ce qui vous permettra d’être opérationnel le plus rapidement possible sans codage dans AEM.

Toutefois, vous devez tenir compte des possibilités hybrides supplémentaires qui s’offrent à vous une fois que vous avez compris les fonctionnalités d’AEM découplé. Ces cas sont présentés ci-dessous pour votre connaissance. À la fin du parcours, vous découvrirez ces concepts plus en détail si une telle flexibilité est requise pour votre projet.

### Vous utilisez déjà de manière externe des contenus découplés, par exemple avec les applications sur une seule page (SPA). {#already-have-a-spa}

Supposons que votre besoin de base soit au minimum de diffuser du contenu depuis AEM vers un service externe existant.

#### Niveau 1 : intégration de fragments de contenu – Modèle découplé traditionnel {#level-1}

Ce niveau d’intégration est le modèle découplé traditionnel. Il permet aux auteurs de créer des contenus dans AEM et de les diffuser sans interface utilisateur vers un certain nombre de services externes à l’aide de GraphQL, ou de les modifier dans des services externes à l’aide de l’API Assets. Aucun codage n’est nécessaire dans AEM.

Dans ce modèle, AEM n’est utilisé que pour créer et diffuser du contenu à l’aide d’AEM fragments de contenu. Le rendu et l’interaction avec le contenu sont délégués à l’application externe consommatrice, souvent une application sur une seule page (SPA).

#### Niveau 2 : incorporation de la SPA dans AEM – Modèle hybride {#level-2}

Ce niveau d’intégration repose sur le premier niveau, mais permet également à l’application externe (SPA) d’être incorporée dans AEM afin que les auteurs puissent voir le contenu dans le contexte de l’application externe, dans AEM. L’application peut également prendre en charge la modification limitée de l’application externe dans AEM.

Ce niveau a l’avantage de permettre aux auteurs de créer du contenu de manière flexible et sécurisée dans AEM. Les contenus sont ainsi présentés dans leur contexte avec une SPA externe incorporée, tout en diffusant le contenu hors interface utilisateur.

#### Niveau 3 : incorporation et activation complète des SPA dans AEM – Modèle hybride {#level-3}

Ce niveau d’intégration repose sur le niveau 2 en permettant de modifier l’essentiel du contenu de la SPA externe dans AEM.

### Vous n’avez pas encore de consommateur externe de contenu découplé, par exemple les applications sur une seule page (SPA). {#do-not-have-a-spa}

Si votre objectif est de créer une SPA qui consomme du contenu en toute sécurité depuis AEM, vous pouvez utiliser des fonctionnalités telles que les fragments de contenu pour gérer votre contenu découplé et créer également une SPA avec le framework de l’éditeur de SPA d’AEM.

Avec cet éditeur, la SPA consomme non seulement des contenus issus d’AEM, mais elle est en outre entièrement modifiable dans AEM par les auteurs de contenu, ce qui vous donne à la fois la flexibilité d’une diffusion découplée et de la modification replacée dans son contexte au sein d’AEM.

## Exigences et conditions préalables {#requirements-prerequisites}

Un certain nombre d’exigences s’imposent avant de vous engager dans votre projet AEM découplé.

### Connaissances {#knowledge}

* GraphQL
* Expérience de développement pour créer des SPA avec les frameworks React ou Angular
* Compétences AEM de base pour la création de fragments de contenu et l’utilisation de l’éditeur

### Outils {#tools}

* Accès aux environnements de test pour tester le déploiement de votre projet
* Instance de développement locale pour la modélisation et le test des données
* SPA externe existante ou autre consommateur de contenu AEM découplé

## Définition de votre projet {#defining-your-project}

Pour la réussite d’un projet, il est important de définir clairement non seulement les exigences du projet, mais aussi les rôles et les responsabilités.

### Portée {#scope}

Il est important de définir clairement la portée du projet. La portée définit les critères d’acceptation et permet d’établir une définition de l’état « terminé ».

La première question que vous devez poser est : &quot;Qu&#39;est-ce que j&#39;essaie de faire avec AEM sans tête ?&quot; En règle générale, la réponse doit être que vous disposez ou aurez à l’avenir une application d’expérience que vous avez créée avec vos propres outils de développement et non avec AEM. Cette application d’expérience peut être une application mobile, un site web ou toute autre application d’expérience destinée aux utilisateurs finaux. La finalité d’AEM découplé est d’alimenter votre application d’expérience en contenus créés, stockés et gérés dans AEM à l’aide d’API dernier cri. Celles-ci appellent AEM découplé pour récupérer du contenu, ou même du contenu intégralement CRUD, directement depuis votre application d’expérience. Si ce n’est pas ce que vous souhaitez faire, vous devrez probablement [revenir à la documentation d’AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr) et déterminer la section la mieux adaptée à ce que vous souhaitez accomplir.

### Rôles et responsabilités {#roles-responsibilities}

Les rôles de chaque projet varient, mais les rôles importants à prendre en compte dans le contenu d’AEM développement sans interface sont les suivants :

* [Administrateur](#administrator)
* [Auteur de contenu](#content-author)
* [Architecte de contenu](#content-architect)
* [Développeur](#developer)

#### Administrateur {#administrator}

L’administrateur est responsable de l’installation et de la configuration de base de votre système. Par exemple, l’administrateur configure votre organisation dans le système de gestion des utilisateurs Adobe, appelé Système Identity Management (IMS). L’administrateur est le premier utilisateur de l’organisation à recevoir une invitation par courrier électronique de l’Adobe une fois que votre organisation a été créée par Adobe dans IMS. L’administrateur peut se connecter à IMS et ajouter des utilisateurs d’autres personnes.

Une fois les utilisateurs configurés par l’administrateur, ils disposent des autorisations nécessaires pour accéder à toutes les ressources AEM afin d’accomplir leur travail en tant que contributeurs à la diffusion de l’application d’expérience à l’aide d’AEM Headless.

L’administrateur doit être l’utilisateur qui a installé AEM et préparé l’environnement d’exécution pour permettre aux [auteurs de contenu](#content-author) de créer et de mettre à jour du contenu, et aux [développeurs](#developer) d’utiliser des API qui récupèrent ou modifient du contenu pour leurs applications d’expérience.

#### Auteur de contenu {#content-author}

Les auteurs de contenu créent et gèrent le contenu diffusé de manière découplée par AEM. Pour gérer leurs contenus, les auteurs utilisent les fonctionnalités d’AEM, notamment les fragments de contenu et la console Assets.

Ils doivent garder à l’esprit les bonnes pratiques suivantes.

#### Plan de traduction {#translation}

Prévoyez la traduction dès le début du projet. Considérez le &quot;spécialiste de traduction&quot; comme une personne distincte dont la responsabilité est de définir quel contenu doit être traduit et ce qui ne doit pas être traduit, et quel contenu traduit peut être modifié par les producteurs de contenu régionaux ou locaux.

Créez un plan sur la traduction de contenu dont vous avez besoin.

* Avez-vous besoin de différentes langues ou aussi d&#39;une langue pour adopter des spécificités régionales ?
* Avez-vous besoin que les contenus multimédias enrichis comme les images ou les vidéos soient différents selon les paramètres régionaux ?

Soyez clair au sujet de votre workflow de mise à jour du contenu. Quel est le processus d’approbation que le système doit prendre en charge ? Est-il possible d’utiliser des workflows AEM pour automatiser ce processus ?

Notez que votre [hiérarchie du contenu](#content-hierarchy) peut être utilisé pour faciliter la traduction.

Voir [ressources supplémentaires](#additional-resources) pour obtenir de la documentation supplémentaire sur les processus AEM et les outils de traduction, y compris des liens vers le Parcours de traduction AEM sans affichage.

##### Tirer parti de la hiérarchie du contenu {#content-hierarchy}

La hiérarchie des dossiers peut répondre à deux préoccupations majeures concernant la gestion des contenus :

* [Traduction](#translation) : AEM gère la traduction du contenu en conservant des copies du contenu dans des dossiers spécifiques aux paramètres régionaux.
* Organisation : les dossiers servent à définir une hiérarchie de contenu nécessaire à la prise en charge des besoins de traduction et à gérer logiquement les fragments de contenu.

AEM permet une structure de contenu flexible et une hiérarchie peut être arbitrairement volumineuse. Toutefois, il est important de comprendre que toute modification de la structure des dossiers peut avoir des conséquences inattendues sur les requêtes existantes qui [dépendent du chemin d’accès au contenu.](#developer) Par conséquent, une hiérarchie bien définie, clairement définie à l’avance, peut s’avérer utile aux auteurs de contenu.

Les dossiers peuvent également être limités de manière à n’autoriser que certains types de contenu (en fonction des modèles de fragment de contenu). Il est recommandé de toujours spécifier explicitement les modèles autorisés pour tous les dossiers de la hiérarchie. Spécification du contenu autorisé pour un dossier donné :

* Empêche les auteurs de créer du contenu n’appartenant pas au dossier.
* Optimise le processus de création de contenu en filtrant les types de contenu autorisés dans le dossier au cours de la création pour n’afficher que les types de contenu valides.

En créant une structure de contenu appropriée, il devient plus facile de coordonner la création de contenus découplés sur plusieurs canaux afin d’optimiser la réutilisation de ces contenus. L’utilisation du contenu sur plusieurs canaux améliore considérablement l’efficacité de la production de contenu et la gestion des modifications.

##### Définir de bonnes conventions d’affectation de noms {#naming-conventions}

Les noms des fragments de contenu doivent être explicites pour les auteurs de contenu. AEM gère de manière transparente l’échappement et/ou la troncation des noms utilisés pour les ID au niveau du référentiel. Les noms logiques attribués par les auteurs de contenu doivent donc toujours être lisibles et représenter le contenu.

* Nom incorrect : `cta_btn_1`
* Nom approprié : `Call To Action Button`

Voir la section [Ressources supplémentaires](#additional-resources) pour accéder à d’autres documentations à propos des conventions d’affectation de noms de pages dans AEM.

##### Ne pas étendre excessivement l’imbrication de contenu {#content-nesting}

Les [fragments de contenu](#content-fragments) sont utilisés dans AEM pour créer des contenus en mode découplé. AEM prend en charge jusqu’à dix niveaux d’imbrication pour les fragments de contenu. Toutefois, il est important de garder à l’esprit que AEM doit résoudre de manière itérative chaque référence définie dans le fragment de contenu parent, puis vérifier s’il existe des références enfants dans tous les frères. Ces opérations peuvent rapidement se cumuler et poser des problèmes de performances.

En règle générale, les références aux fragments de contenu ne doivent pas être imbriquées au-delà de cinq niveaux.

#### Architecte de contenu {#content-architect}

Les architectes de contenu analysent les exigences relatives aux données qui doivent être distribuées sans interface utilisateur et définissent la structure de ces données. Dans AEM, ces structures sont appelées [Modèles de fragment de contenu](#content-fragment-models). Les modèles de fragments de contenu servent de base pour les fragments de contenu créés par les auteurs.

Une approche utile lors de la définition de modèles de fragment de contenu consiste à créer des modèles qui mappent les composants UX des applications qui utilisent le contenu.

Comme les auteurs interagissent avec les modèles de manière permanente lorsqu’ils créent des contenus, l’alignement des modèles avec l’expérience utilisateur les aide à visualiser l’expérience digitale obtenue. Pour aller plus loin, vous pouvez attribuer des icônes aux modèles de fragment de contenu qui représentent l’élément d’expérience utilisateur afin que les auteurs puissent sélectionner intuitivement le bon modèle en fonction des indices visuels.

#### Développeur {#developer}

Les développeurs sont chargés de rapprocher le contenu créé dans AEM découplé et le consommateur de ce contenu. Souvent il s’agit d’une application sur une seule page (SPA), d’une application web progressive (PWA), d’une boutique en ligne ou d’un autre service extérieur à AEM.

GraphQL sert de « liant » entre AEM et les consommateurs de contenu en mode découplé. GraphQL est un langage qui permet d’interroger AEM pour obtenir le contenu nécessaire.

Les développeurs doivent garder à l’esprit quelques recommandations de base lorsqu’ils planifient leurs requêtes :

* Les requêtes ne doivent pas dépendre d’un chemin d’accès fixe (`ByPath`) pour récupérer les fragments de contenu.
   * [Les auteurs de contenu contrôlent complètement la hiérarchie des fragments de contenu](#content-hierarchy) et peuvent éventuellement effectuer des modifications susceptibles de rompre cette requête.
   * Les requêtes doivent plutôt adopter des références de modèles de fragments de contenu associés à des paramètres de requête dynamiques pour filtrer les résultats et générer ainsi la charge utile souhaitée.
* Pour des requêtes plus performantes avec AEM, utilisez toujours des requêtes persistantes. Celles-ci sont abordées plus loin dans le parcours.
* GraphQL est déclaratif suivant la devise &quot;Demandez exactement ce dont vous avez besoin et obtenez exactement cela&quot;. En d’autres termes, lors de la création de requêtes GraphQL, évitez systématiquement les requêtes de type `select *` que vous pourriez créer dans une base de données relationnelle.

Pour une [mise en œuvre découplée de type général à l’aide d’AEM,](#level-1) un développeur n’a besoin d’aucune connaissance en matière de codage avec AEM.

### Exigences de performance {#performance-requirements}

Pour la réussite d’un projet, les performances doivent être prises en compte avant la création d’un contenu.

Vous devez comprendre les attentes de vos utilisateurs/visiteurs et concevoir le projet pour eux. Définissez des objectifs de niveau de service (SLO) et mesurez-les pour savoir si vous répondez aux attentes de vos utilisateurs.

#### Modèles de trafic {#traffic-patterns}

Pour comprendre le trafic et les schémas de trafic, commencez par recueillir des connaissances à propos du passé, puis effectuez une projection de la croissance attendue pour les prochaines années. Certaines des variables les plus importantes à prendre en compte :

* Combien d’appels d’API par heure, par jour ou par mois attendez-vous et y a-t-il des possibilités de pointes d’activités ou de crêtes saisonnières ?
* Combien y a-t-il d’auteurs de contenu différents ?
* Combien d’auteurs de contenu travaillant simultanément prévoyez-vous ?
* Quelle est la fréquence des mises à jour de contenus ?
* Combien de modèles de contenu sont-ils nécessaires ?
* Combien d’instances de modèles sont nécessaires ?

#### Fréquence de mise à jour {#update-frequency}

Souvent, différentes sections d’expériences ont différentes fréquences de mises à jour de contenu. Il est important de comprendre cela pour pouvoir affiner les configurations du réseau de diffusion de contenu (CDN) et du cache. Il s’agit également d’une contribution importante pour la variable [Architectes de contenu](#content-architects) pendant qu’ils conçoivent des modèles pour représenter votre contenu. Prenez en compte les éléments suivants :

* Certains types de contenu doivent-ils expirer au-delà d’une certaine période ?
* Certains éléments sont-ils spécifiques à l’utilisateur, donc sans pouvoir être mis en cache ?

## Et après ? {#what-is-next}

Maintenant que vous avez terminé cette partie du parcours de développement découplé AEM, vous devriez pouvoir :

* comprendre les principes de base des fonctionnalités d’AEM découplé ;
* connaître les conditions préalables requises pour utiliser les fonctionnalités AEM découplées ;
* avoir conscience des niveaux d’intégration AEM découplé ;
* être en mesure de définir la portée de votre projet.

Vous devriez poursuivre votre parcours avec AEM découplé en consultant le document [Accès à votre première expérience à l’aide d’AEM découplé](path-to-first-experience.md). Vous pourrez y découvrir comment configurer les outils nécessaires et commencer à réfléchir à la modélisation de vos données dans AEM.

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de développement en mode découplé en examinant le document [Accès à votre première expérience à l’aide d’AEM découplé](path-to-first-experience.md), vous trouverez ci-après quelques ressources facultatives supplémentaires pour approfondir un certain nombre de concepts mentionnés dans ce document, mais non obligatoires pour poursuivre le parcours en mode découplé.

* [AEM Parcours de traduction sans affichage](/help/journey-headless/translation/overview.md) - Ce parcours de documentation vous donne une large compréhension de la technologie sans interface, de la manière dont AEM diffuse du contenu sans interface et de la manière dont vous pouvez le traduire.
* [Tutoriels sur AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr) – Ces tutoriels pratiques vous permettront de découvrir comment utiliser, avec AEM, les différentes options de diffusion de contenu vers des points de terminaison en mode découplé et choisir ce qui vous convient.
* [Gestion de contenu en mode découplé à l’aide des API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) – Suivez ce cours pour bénéficier d’une présentation de l’API GraphQL implémentée dans AEM. L’authentification à l’aide de l’Adobe ID est requise.
* [AEM Guides WKND – GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) – Ce projet GitHub comprend des exemples d’applications qui mettent en évidence les API GraphQL d’AEM.
* [Concepts de création](/help/sites-authoring/author.md) – Documentation technique pour l’environnement de création d’AEM, avec notamment des détails sur la configuration auteur-publication.
* [Publication de pages](/help/sites-authoring/publishing-pages.md) – Documentation technique pour la publication de contenu sur AEM
* [Convention d’affectation de noms](/help/sites-developing/naming-conventions.md) – Documentation technique relative aux restrictions d’affectation de noms de pages dans AEM
* [Multi Site Manager et traduction](/help/sites-administering/msm-and-translation.md) – Documentation technique sur les puissantes fonctionnalités de traduction d’AEM
* [Workflows AEM](/help/sites-authoring/workflows.md) – Documentation technique sur l’automatisation des workflows dans AEM
* [Fragments de contenu](/help/assets/content-fragments/content-fragments.md) – Documentation technique sur les fragments de contenu.
* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) – Documentation technique sur les modèles de fragment de contenu.
* [Documentation technique GraphQL](https://graphql.org) – La définition de GraphQL (lien externe)
* [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) – Documentation technique expliquant comment créer des demandes d’accès et de diffusion de fragments de contenu.
* [API REST Assets](/help/assets/assets-api-content-fragments.md) – Documentation technique expliquant comment créer et modifier des fragments de contenu (et d’autres ressources).
* [Requêtes persistantes](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) – Documentation technique sur les requêtes persistantes dans AEM
* [Modes Pile complète et Découplé dans AEM](/help/sites-developing/headful-headless.md) – Discussion complète sur les niveaux d’intégration en mode découplé disponibles dans AEM.
