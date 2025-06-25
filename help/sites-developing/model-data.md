---
title: Modélisation des données - Modèle de David Nuescheler
description: Recommandations de David Nuescheler en matière de modélisation de contenu
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: ht
source-wordcount: '1767'
ht-degree: 100%

---

# Modélisation des données - Modèle de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Source {#source}

Les informations suivantes sont des idées et des commentaires exprimés par David Nuescheler.

David a été co-fondateur et CTO de Day Software AG, l’un des principaux éditeurs de logiciels de gestion de contenu et d’infrastructure de contenu, acquis par Adobe en 2010. David est désormais membre et vice-président des technologies d’entreprise chez Adobe et dirige également le développement de JSR-170, l’interface de programmation d’applications (API) Java™ Content Repository (JCR), la norme technologique pour la gestion de contenu.

Vous trouverez d’autres informations à l’adresse suivante : [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## Présentation de David {#introduction-from-david}

Lors de diverses discussions, j’ai constaté que les développeurs et les développeuses étaient quelque peu mal à l’aise avec les fonctions et fonctionnalités présentées par JCR lors de la modélisation de contenu. Il n’existe pas encore de guide et il y a peu d’expériences sur la modélisation du contenu dans un référentiel et les raisons pour lesquelles un modèle de contenu est meilleur qu’un autre.

Même si dans le monde relationnel, l’industrie du logiciel a de l’expérience dans la modélisation des données, elle en est encore à ses débuts dans le domaine des référentiels de contenu.

J’aimerais commencer à combler ce vide en exprimant mes opinions sur la manière dont le contenu doit être modélisé. J’espère que cela pourra un jour devenir quelque chose de plus significatif pour la communauté des développeurs et des développeuses, qui n’est pas seulement « mon opinion », mais quelque chose de plus généralement applicable. Considérez donc cela comme ma première tentative, qui évolue rapidement.

>[!NOTE]
>
>Clause de non-responsabilité : ces lignes directrices sont l’expression de mes opinions personnelles, qui sont parfois sujettes à controverse. Je suis impatient d’en discuter et de les affiner.

## Sept règles simples {#seven-simple-rules}

### Règle n°1 : l es données d’abord, la structure ensuite. Normalement… {#rule-data-first-structure-later-maybe}

#### Explication {#explanation-1}

Je recommande de ne pas vous soucier d’une structure de données déclarée au sens ERD. Dans un premier temps.

Apprenez à aimer nt:unstructured (et ses amis) dans le développement.

Ma conclusion : la structure coûte cher et il est souvent totalement inutile de déclarer explicitement la structure au stockage sous-jacent.

Il existe un contrat implicite concernant la structure que votre application utilise de manière inhérente. Imaginons que je stocke la date de modification d’un article de blog dans une propriété lastModified. Mon application sait automatiquement relire la date de modification à partir de cette même propriété, il n’est donc pas nécessaire de la déclarer explicitement.

D’autres contraintes de données, telles que des contraintes obligatoires ou de type et de valeur, ne doivent être appliquées que lorsque cela est nécessaire pour des raisons d’intégrité des données.

#### Exemple {#example-1}

L’exemple ci-dessus d’utilisation de la propriété de date `lastModified` sur un nœud « article de blog » ne signifie pas vraiment qu’il faut utiliser un type de nœud particulier. J’utiliserais sans aucun doute `nt:unstructured` pour mes nœuds d’article de blog, du moins au début. Puisque, dans mon application de création de blog, je vais simplement afficher la date de la dernière modification (éventuellement en exécutant la fonction « classer par »), je me soucie peu s’il s’agit d’une date. Étant donné que je fais implicitement confiance à mon application de création de blog pour placer une « date » à cet endroit, il n’est aucunement nécessaire de déclarer la présence d’une date `lastModified` sous la forme d’un type de nœud.

### Règle n°2 : prenez le contrôle de la hiérarchie de contenu, ne la laissez pas vous diriger. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explication {#explanation-2}

La hiérarchie de contenu est un atout précieux. Ne la laissez pas vous guider ; dirigez-la. Si vous ne disposez pas d’un nom facilement lisible pour un nœud, vous devriez y réfléchir un peu plus. Les nombres arbitraires ne constituent pas un « bon nom ».

Bien qu’il puisse être facile de transformer rapidement un modèle relationnel existant en un modèle hiérarchique, il convient de réfléchir à ce processus.

D’après mon expérience, si l’on considère le contrôle d’accès et le confinement comme de bons moteurs pour la hiérarchie du contenu. Pensez-y comme s’il s’agissait de votre système de fichiers. Utilisez même peut-être des fichiers et des dossiers pour le modéliser sur votre disque local.

Personnellement, je préfère initialement les conventions hiérarchiques au système de typage de nœuds, et j’introduis le typage plus tard.

>[!CAUTION]
>
>La structure d’un référentiel de contenu peut également avoir un impact sur les performances. Pour des performances optimales, le nombre de nœuds enfants associés à des nœuds individuels dans un référentiel de contenu ne doit pas dépasser 1 000.

#### Exemple {#example-2}

Je vais modéliser un système de blog simple comme suit. Au départ, je ne me soucie même pas des types de nœuds respectifs que j’utilise à ce stade.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Il est évident que nous comprenons tous la structure du contenu sur la base de l’exemple, sans qu’aucune autre explication ne soit nécessaire.

Ce qui peut être inattendu au départ, c’est pourquoi je ne stockerais pas les « commentaires » avec la « publication », ce qui est dû au contrôle d’accès que j’aimerais appliquer de manière raisonnablement hiérarchique.

À l’aide du modèle de contenu ci-dessus, je peux facilement autoriser l’utilisateur « anonyme » à « créer » des commentaires, tout en gardant l’utilisateur anonyme en lecture seule pour le reste de l’espace de travail.

### Règle n°3 : les espaces de travail sont destinés à clone(), merge() et update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explication {#explanation-3}

Si vous n’utilisez pas de méthode `clone()`, `merge()` ou `update()` dans votre application, l’espace de travail unique est probablement la bonne solution.

Les « nœuds correspondants » sont un concept défini dans la spécification JCR. Essentiellement, cela se résume à des nœuds qui représentent le même contenu, dans différents espaces de travail.

JCR introduit le concept abstrait d’espaces de travail qui laisse de nombreux développeurs et développeuses dans le flou quant à leur utilisation. Je vous propose de tester votre utilisation des espaces de travail comme suit.

Si vous avez un chevauchement considérable de nœuds « correspondants » (essentiellement les nœuds avec le même UUID) dans plusieurs espaces de travail, vous faites probablement bon usage des espaces de travail.

S’il n’y a pas de chevauchement de nœuds avec le même UUID, vous abusez probablement des espaces de travail.

N’utilisez pas les espaces de travail pour le contrôle d’accès. La visibilité du contenu pour un groupe particulier d’utilisateurs et utilisatrices n’est pas un bon argument pour séparer les éléments en différents espaces de travail. JCR propose un « contrôle d’accès » dans le référentiel de contenu pour y parvenir.

Les espaces de travail sont les limites des références et des requêtes.

#### Exemple {#example-3}

Utilisez les espaces de travail pour les choses suivantes :

* v1.2 de votre projet par rapport à une v1.3 de votre projet
* un état de contenu « développement », « QA » et « publié »

N’utilisez pas les espaces de travail pour les éléments suivants :

* répertoires de base des utilisateurs et utilisatrices
* contenu distinct pour différentes audiences cibles comme public, privé, local...
* boîtes de réception pour différents utilisateurs et utilisatrices

### Règle n°4 : méfiez-vous des enfants portant le même nom (SNS). {#rule-beware-of-same-name-siblings}

#### Explication {#explanation-4}

Les enfants portant le même nom (Same Name Siblings [SNS]) ont été introduit dans la spécification pour permettre la compatibilité avec les structures de données conçues et exprimées via XML et, par conséquent, sont précieuses pour JCR. Cependant, les SNS entraînent une surcharge et une complexité pour le référentiel.

Tout chemin vers le référentiel de contenu contenant des SNS dans l’un de ses segments de chemin devient beaucoup moins stable. Si des SNS sont supprimés ou réorganisés, cela a un impact sur les chemins de tous les autres SNS et de leurs enfants.

Pour l’importation de code XML ou l’interaction avec du code XML existant, les SNS peuvent être nécessaires et utiles, mais je n’ai jamais utilisé de SNS (et je n’en ai jamais eu l’intention) dans mes modèles de données « champ vert »

#### Exemple {#example-4}

Utilisez

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

au lieu de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Règle n°5 : les références sont considérées comme nuisibles. {#rule-references-considered-harmful}

#### Explication {#explanation-5}

Les références impliquent l’intégrité référentielle. Il est important de comprendre que les références impliquent non seulement un coût supplémentaire pour le référentiel qui gère l’intégrité référentielle, mais qu’elles sont également coûteuses du point de vue de la flexibilité du contenu.

Personnellement, je n’utilise des références que lorsque je ne peux vraiment pas gérer une référence en suspens et j’utilise autrement un chemin, un nom ou une chaîne UUID pour faire référence à un autre nœud.

#### Exemple {#example-5}

Supposons que j’autorise les « références » d’un document (a) vers un autre document (b). Si je modélise cette relation à l’aide de propriétés de référence, cela signifie que les deux documents sont liés au niveau du référentiel. Je ne peux pas exporter/importer le document (a) individuellement, car la cible de la propriété de référence peut ne pas exister. D’autres opérations telles que la fusion, la mise à jour, la restauration ou le clonage sont également affectées.

Je peux donc modéliser ces références comme des « références faibles » (dans JCR v1.0, cela se résume à des propriétés de chaîne qui contiennent l’UUID du nœud cible) ou simplement utiliser un chemin. Parfois, le chemin est plus significatif au départ.

Je pense qu’il existe des cas d’utilisation dans lesquels un système ne peut vraiment pas fonctionner si une référence est suspendue, mais je n’arrive tout simplement pas à trouver un bon exemple « réel » mais simple tiré de mon expérience personnelle.

### Règle n°6 : des fichiers sont des fichiers. {#rule-files-are-files}

#### Explication {#explanation-6}

Si un modèle de contenu expose quelque chose qui, même de loin, ressemble à un fichier ou un dossier, j’essaie d’utiliser (ou de développer à partir de) `nt:file`, `nt:folder` et `nt:resource`.

D’après mon expérience, de nombreuses applications génériques permettent une interaction implicite avec nt:folder et nt:files et savent comment gérer et afficher ces événements s’ils sont enrichis de méta-informations supplémentaires. Par exemple, une interaction directe avec des implémentations de serveurs de fichiers telles que CIFS ou WebDAV reposant sur JCR devient implicite.

Je pense qu’il est judicieux d’appliquer la méthode suivante : si vous devez stocker le nom de fichier et le type MIME, `nt:file`/`nt:resource` convient parfaitement. Si vous pouvez avoir plusieurs « fichiers », nt:folder constitue l’emplacement de stockage idéal.

Si vous devez ajouter des méta-informations pour votre ressource (une propriété « description » ou « auteur ou autrice », par exemple), étendez `nt:resource` et non `nt:file`. J’étends rarement un nt:file, mais souvent un `nt:resource`.

#### Exemple {#example-6}

Supposons qu’une personne souhaite charger une image sur une entrée de blog à l’adresse :

```xml
/content/myblog/posts/iphone_shipping
```

Peut-être que la réaction instinctive initiale serait d’ajouter une propriété binaire contenant l’image.

Bien qu’il existe de bons cas d’utilisation pour utiliser simplement une propriété binaire (disons que le nom n’est pas pertinent et que le type MIME est implicite), dans ce cas, je recommande la structure suivante pour mon exemple de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Règle n°7 : les identifiants sont à éviter. {#rule-ids-are-evil}

#### Explication {#explanation-7}

Dans les bases de données relationnelles, les identifiants sont un moyen nécessaire pour exprimer les relations, c’est pourquoi les utilisateurs et utilisatrices ont également tendance à les utiliser dans les modèles de contenu. Surtout pour de mauvaises raisons.

Si votre modèle de contenu est rempli de propriétés se terminant par « Id », vous n’utilisez probablement pas correctement la hiérarchie.

Il est vrai que certains nœuds ont besoin d’une identification stable tout au long de leur cycle de vie ; mais c’est moins fréquent que vous ne le pensez. Mais `mix:referenceable` dispose d’un tel mécanisme intégré au référentiel, il n’est donc pas nécessaire de trouver un moyen supplémentaire d’identifier un nœud de manière stable.

Gardez également à l’esprit que les éléments peuvent être identifiés par chemin. Et, même si les « liens symboliques » ont bien plus de sens pour la plupart des utilisateurs et utilisatrices que les liens physiques dans un système de fichiers UNIX®, un chemin a du sens pour la plupart des applications lorsqu’il fait référence à un nœud cible.

Plus important encore : **mix**:referenceable signifie qu’il peut être appliqué à un nœud au moment où il est vraiment nécessaire de le référencer.

Ainsi, ce n’est pas parce que vous aimeriez pouvoir potentiellement référencer un nœud de type « Document » que votre type de nœud « Document » doit s’étendre de `mix:referenceable` de façon statique. En effet, il peut être ajouté dynamiquement à n’importe quelle instance du « Document ».

#### Exemple {#example-7}

Utilisez :

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

Au lieu de :

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
