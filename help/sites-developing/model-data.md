---
title: Modélisation de données – Modèle de David Nuescheler
seo-title: Modélisation de données – Modèle de David Nuescheler
description: Recommandations de David Nuescheler sur le plan de la modélisation de contenu
seo-description: Recommandations de David Nuescheler sur le plan de la modélisation de contenu
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 89%

---


# Modélisation de données – Modèle de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Source {#source}

Les informations suivantes sont des suggestions et des commentaires formulés par David Nuescheler.

David Nuescheler est l’un des fondateurs de Day Software AG, principal fournisseur de logiciels d’infrastructure de contenu et de gestion de contenu global, racheté par Adobe en 2010. Il occupait également le poste de directeur de la technologie au sein de cette société. Il est aujourd’hui vice-président de la technologie d’entreprise chez Adobe et dirige le développement de l’interface JSR-170, l’API JCR (Java Content Repository), qui est la technologie standard pour la gestion du contenu.

D&#39;autres mises à jour sont également disponibles sur [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introduction de David Nuescheler {#introduction-from-david}

Au cours de différentes discussions, j’ai pu constater que les développeurs étaient quelque peu mal à l’aise avec les fonctionnalités présentées par JCR sur le plan de la modélisation du contenu. Il n’existe, pour l’heure, aucune indication sur la façon de modéliser du contenu dans un référentiel et très peu d’experts se sont exprimés sur les avantages d’un modèle de contenu par rapport à un autre.

Bien que, dans le contexte relationnel, la modélisation des données soit largement documentée dans l’industrie du logiciel, nous n’en sommes qu’au tout début dans le domaine du référentiel de contenu.

J’aimerais combler cette lacune en exprimant mon opinion personnelle sur la façon de modéliser le contenu, en espérant qu’un jour cela puisse se transformer en quelque chose de plus significatif pour la communauté des développeurs. Je tiens toutefois à ajouter qu’il ne s’agit pas simplement de mon opinion, mais de quelque chose de plus généralement applicable. Veuillez donc considérer cela comme une première tentative de réponse, appelée à évoluer rapidement.

>[!NOTE]
>
>Clause de non-responsabilité : Ces lignes directrices sont l’expression de mes opinions personnelles, qui sont parfois sujettes à controverse. Je suis impatient d’en discuter et de les affiner.

## Sept règles simples {#seven-simple-rules}

### Règle 1 : Les données d&#39;abord, la structure plus tard. Peut-être. {#rule-data-first-structure-later-maybe}

#### Explication {#explanation-1}

Je recommande de ne pas s’inquiéter d’une structure de données déclarée, du point de vue de l’ERD. Du moins, au début.

Apprenez à aimer nt:unstructured (et ses amis) au cours du développement.

Je pense que Stefano résume cela assez bien.

Je vais vous livrer le fond de ma pensée : la structure est onéreuse et, dans bien des cas, il est parfaitement inutile de déclarer explicitement la structure au stockage sous-jacent.

Il existe un contrat implicite au sujet de la structure que votre application utilise par nature. Supposons que je stocke la date de modification d’un article de blog dans une propriété lastModified. Mon application sera, à nouveau, en mesure de lire automatiquement la date de modification à partir de cette même propriété ; il n’est donc vraiment pas nécessaire de la déclarer explicitement.

Des contraintes de données supplémentaires, comme des contraintes de type ou de valeur, ou des contraintes obligatoires, ne doivent être appliquées que si cela s’avère nécessaire à des fins d’intégrité des données.

#### Exemple {#example-1}

L’exemple d’utilisation de la propriété de date `lastModified` sur un nœud « article de blog » ne signifie pas vraiment qu’il faut utiliser un type de nœud particulier. Je vais certainement utiliser `nt:unstructured` pour mes nœuds d’article de blog, du moins au début. Puisque, dans mon application de création de blog, je vais simplement afficher la date de la dernière modification (éventuellement en exécutant la fonction « classer par »), je me soucie peu s’il s’agit d’une date. Étant donné que je fais implicitement confiance à mon application de création de blog pour placer une « date » à cet endroit, il n’est aucunement nécessaire de déclarer la présence d’une date `lastModified` sous la forme d’un type de nœud.

### Règle n° 2 : Prenez le contrôle de la hiérarchie de contenu, ne la laissez pas vous diriger. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explication {#explanation-2}

La hiérarchie de contenu est une ressource très précieuse. Ne laissez pas simplement les choses se faire, prenez en main la conception ! Si vous n&#39;avez pas de &quot;bon&quot; nom lisible par l&#39;homme pour un noeud, c&#39;est probablement quelque chose que vous devriez reconsidérer. Un nombre arbitraire constitue rarement un « nom acceptable ».

S’il peut s’avérer extrêmement simple de placer rapidement un modèle relationnel existant dans un modèle hiérarchique, ce processus doit faire l’objet d’une certaine réflexion.

D’expérience, je peux dire que le contrôle d’accès et le confinement sont généralement deux éléments favorables pour la hiérarchie du contenu. Pensez-y comme s’il s’agissait de votre système de fichiers. Peut-être même pouvez-vous utiliser des fichiers et des dossiers afin de le modéliser sur votre disque dur local.

Personnellement, je préfère, dans la majorité des cas, utiliser les conventions de hiérarchie plutôt que le système de définition de type de nœud au début, et introduire le typage par la suite.

>[!CAUTION]
>
>La structure d’un référentiel de contenu peut également se répercuter sur les performances. Pour de meilleures performances, le nombre de nœuds enfants associés à des nœuds individuels dans un référentiel de contenu doit généralement être inférieur à 1 000.
>
>Voir [Combien de données CRX peut-il gérer ?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) pour plus d’informations.

#### Exemple {#example-2}

Je vais modéliser un simple système de blogage comme suit. Vous constaterez qu’au début, je ne me soucie même pas des types de nœud respectifs que j’utilise.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Je pense que l&#39;une des choses qui deviennent évidentes est que nous comprenons tous la structure du contenu basé sur l&#39;exemple sans aucune explication supplémentaire.

Au début, le fait que je ne stocke pas les « commentaires » avec l’article peut sembler étonnant. Cela est dû au contrôle d’accès que je souhaite appliquer d’une manière hiérarchique raisonnable.

Grâce au modèle de contenu ci-dessus, je peux facilement autoriser l’utilisateur « anonyme » à « créer » des commentaires, tout en le limitant à un accès en lecture seule sur le reste de l’espace de travail.

### Règle n° 3 : Les espaces de travail sont réservés aux méthodes clone(), merge() et update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explication {#explanation-3}

Si vous n&#39;utilisez pas les méthodes `clone()`, `merge()` ou `update()` dans votre application, un seul espace de travail est probablement la solution.

La « correspondance des nœuds » est un concept défini dans la spécification JCR. Il s’agit, en fait, de nœuds qui représentent le même contenu dans ce que l’on désigne comme des espaces de travail différents.

JCR introduit le concept très abstrait d’espace de travail dont bon nombre de développeurs ne comprennent pas très bien la finalité. J’aimerais que vous teniez compte de ce qui suit pour tester votre utilisation des espaces de travail.

Si vous constatez un chevauchement important des nœuds « correspondants » (essentiellement des nœuds portant le même UUID) dans plusieurs espaces de travail, il est probable que vous en fassiez un bon usage.

En l’absence de chevauchement des nœuds portant le même UUID, il est probable que vous utilisiez les espaces de travail à mauvais escient.

Les espaces de travail ne doivent pas être utilisés pour le contrôle d’accès. La visibilité du contenu pour un groupe d’utilisateurs donné ne constitue pas un argument valable pour séparer les éléments dans des espaces de travail différents. À cette fin, JCR propose un « contrôle d’accès » dans le référentiel de contenu.

Les espaces de travail constituent une frontière pour les références et les requêtes.

#### Exemple {#example-3}

Utilisez des espaces de travail pour les éléments suivants :

* v1.2 de votre projet par rapport à une v1.3 de votre projet
* Un état « publié », « développement » ou « QA » du contenu

N’utilisez pas d’espaces de travail pour les éléments suivants :

* Répertoires personnels de l’utilisateur
* Contenu distinct pour différentes audiences cibles, telles que public, privé, local, etc.
* Boîtes de réception pour différents utilisateurs

### Règle n° 4 : Méfiez-vous des SNS (Same Name Siblings)  {#rule-beware-of-same-name-siblings}

#### Explication {#explanation-4}

Bien que les SNS (Same Name Siblings) aient été introduits dans la spécification pour permettre la compatibilité avec des structures de données conçues pour et exprimées par le biais de XML, ce qui les rend particulièrement utiles pour JCR, ils entraînent une augmentation sensible de la surcharge et de la complexité pour le répertoire.

Tout chemin d’accès d’un répertoire de contenu dont l’un des segments contient un SNS devient beaucoup moins stable, si ce SNS est supprimé ou réorganisé, ce qui aura une incidence sur les chemins de tous les autres SNS et leurs enfants.

Dans le cas d’une importation de code XML ou d’une interaction avec un code XML existant, un SNS peut s’avérer nécessaire et utile. Cependant, je n’en ai jamais utilisé dans mes nouveaux modèles de données, et je ne compte pas le faire.

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

### Règle n° 5 : Les références sont considérées comme dangereuses.  {#rule-references-considered-harmful}

#### Explication {#explanation-5}

Les références supposent une intégrité référentielle. Je trouve qu’il est important de comprendre que les références n’entraînent pas seulement une augmentation des coûts pour le référentiel qui gère l’intégrité référentielle. Elles s’avèrent également coûteuses sur le plan de la flexibilité du contenu.

Personnellement, je veille à n’utiliser des références que lorsqu’il m’est véritablement impossible de traiter une « référence pendouillante » (dangling reference) et d’utiliser un chemin d’accès, un nom ou un UUID de chaîne pour faire référence à un autre nœud.

#### Exemple {#example-5}

Supposons que j’autorise des « références» d’un document (a) vers un autre document (b). Si je modélise cette relation à l’aide de propriétés de référence, cela signifie que les deux documents sont liés au niveau du référentiel. Je ne peux pas exporter/importer le document (a) isolément, étant donné que la cible de la propriété de référence n’existe peut-être pas. D’autres opérations, telles qu’une fusion, une mise à jour, une restauration ou un clonage, sont également affectées.

Par conséquent, je vais soit modéliser ces références sous la forme de « références faibles » (dans JCR v1.0, cela se résume principalement à des propriétés de chaîne contenant l’UUID du nœud cible), soit utiliser simplement un chemin d’accès. Parfois, il est préférable de commencer par le chemin d’accès.

Je pense qu’il est des situations dans lesquelles il est impossible qu’un système fonctionne si une référence est « pendouillante ». Cependant, il ne me vient, en ce moment, aucun exemple simple qui pourrait illustrer ce type de situation.

### Règle #6 : Les fichiers sont des fichiers. {#rule-files-are-files}

#### Explication {#explanation-6}

Si un modèle de contenu expose quelque chose qui sent *à distance* comme un fichier ou un dossier que j&#39;essaie d&#39;utiliser (ou d&#39;étendre à) `nt:file`, `nt:folder` et `nt:resource`.

Avec l’expérience, j’ai constaté que de nombreuses applications génériques autorisaient implicitement une interaction avec nt:folder et nt:files, et savaient comment traiter et afficher ces événements s’ils étaient enrichis de méta-informations supplémentaires. Par exemple, une interaction directe avec des implémentations de serveurs de fichiers, comme CIFS ou WebDAV au-dessus de JCR, deviennent implicites.

Je pense qu&#39;en règle générale, on pourrait utiliser ce qui suit : Si vous devez stocker le nom de fichier et le type mime, `nt:file`/ `nt:resource` correspond très bien. Si plusieurs « fichiers » sont possibles, nt:folder constitue l’emplacement de stockage idéal.

Si vous devez ajouter des méta-informations pour votre ressource (une propriété « description » ou « auteur », par exemple), étendez `nt:resource` et non `nt:file`. J&#39;étend rarement nt:file et j&#39;étend fréquemment `nt:resource`.

#### Exemple {#example-6}

Supposons qu’un utilisateur souhaite télécharger une image dans une entrée de blog à l’adresse :

```xml
/content/myblog/posts/iphone_shipping
```

Peut-être la réaction instinctive initiale sera-t-elle d’ajouter une propriété binaire contenant l’image.

Bien qu’il existe certainement des scénarios dans lesquels l’utilisation d’une simple propriété binaire se justifie (par exemple, lorsque le nom n’est pas pertinent et que le type MIME est implicite), je recommanderais la structure suivante pour mon exemple de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Règle n° 7 : Les ID, c’est le mal !  {#rule-ids-are-evil}

#### Explication {#explanation-7}

Dans les bases de données relationnelles, les ID sont nécessaires pour exprimer des relations. Les utilisateurs ont donc tendance à les employer également dans des modèles de contenu, mais principalement pour de mauvaises raisons. 

Si votre modèle de contenu regorge de propriétés qui se terminent par « Id », il est probable que vous n’utilisiez pas correctement la hiérarchie.

Il est vrai que certains nœuds ont besoin d’une identification stable tout au long de leur cycle de vie. Cependant, ils sont bien moins nombreux que vous ne le pensez. mix:referenceable fournit un tel mécanisme intégré dans le référentiel. Il n’est donc pas nécessaire d’ajouter une autre méthode pour identifier un nœud de manière stable.

Gardez également à l’esprit que les éléments peuvent être identifiés par un chemin d’accès et, autant il est judicieux d’utiliser des « liens symboliques » plutôt que des liens matériels dans un système de fichiers UNIX, autant l’utilisation d’un chemin d’accès semble logique dans la plupart des applications pour faire référence à un nœud cible.

Plus important encore, il est **mix**:referenceable, ce qui signifie qu’il peut être appliqué à un noeud au moment où vous devez le référencer.

Dès lors, ce n’est pas parce que vous aimeriez être en mesure de référencer un nœud de type « Document » que votre type de nœud « Document » doit s’étendre de manière statique depuis mix:referenceable, car il peut être ajouté de façon dynamique à n’importe quelle instance du « Document ».

#### Exemple {#example-7}

Utilisez:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

au lieu de :

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

