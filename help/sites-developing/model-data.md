---
title: Modélisation des données – Modèle de David Nuescheler
description: Recommandations de modélisation de contenu de David Nuescheler
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 7%

---

# Modélisation des données – Modèle de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Source {#source}

Les détails suivants sont des idées et des commentaires exprimés par David Nuescheler.

David a été co-fondateur et responsable technique de Day Software AG, un fournisseur leader de logiciels d’infrastructure de contenu et de gestion de contenu mondial, racheté par Adobe en 2010. David est désormais membre et vice-président de la technologie d’entreprise à Adobe et dirige également le développement de JSR-170, l’interface de programmation d’application (API) de Java™ Content Repository (JCR), la norme technologique pour la gestion de contenu.

D’autres mises à jour sont également disponibles sur [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## Présentation de David {#introduction-from-david}

Au cours de diverses discussions, j’ai constaté que les développeurs sont un peu mal à l’aise avec les fonctionnalités présentées par JCR lors de la modélisation de contenu. Il n’y a pas encore de guide et peu d’expérience sur la façon de modéliser le contenu dans un référentiel et pourquoi un modèle de contenu est meilleur que l’autre.

Bien que dans le monde relationnel, le secteur du logiciel ait de l’expérience sur la façon de modéliser les données, il en est encore aux premiers stades pour l’espace de référentiel de contenu.

Je voudrais commencer à combler ce vide en exprimant mes opinions sur la façon dont le contenu doit être modélisé. J&#39;espère que cela pourra un jour se transformer en quelque chose de plus significatif pour la communauté des développeurs, qui n&#39;est pas seulement &quot;mon opinion&quot; mais quelque chose de plus largement applicable. Considérez que c&#39;est mon premier coup de poignet qui évolue rapidement.

>[!NOTE]
>
>Clause de non-responsabilité : ces lignes directrices sont l’expression de mes opinions personnelles, qui sont parfois sujettes à controverse. Je suis impatient de débattre de ces directives et de les affiner.

## Sept règles simples {#seven-simple-rules}

### Règle n°1 : l es données d’abord, la structure ensuite. Normalement… {#rule-data-first-structure-later-maybe}

#### Explication {#explanation-1}

Je vous recommande de ne pas vous soucier d&#39;une structure de données déclarée au sens de l&#39;ERD. Initialement.

Apprenez à aimer nt:unstructured (&amp; amis) dans le développement.

Mon point final : la structure est chère et il est souvent totalement inutile de déclarer explicitement la structure au stockage sous-jacent.

Il existe un contrat implicite sur la structure que votre application utilise par nature. Supposons que je stocke la date de modification d’une publication de blog dans une propriété lastModified. Mon application sait automatiquement lire à nouveau la date de modification à partir de cette même propriété. Il n’est vraiment pas nécessaire de la déclarer explicitement.

D’autres contraintes sur les données, telles que les contraintes obligatoires ou de type et de valeur, ne doivent être appliquées que si nécessaire pour des raisons d’intégrité des données.

#### Exemple {#example-1}

L’exemple ci-dessus d’utilisation d’une `lastModified` La propriété de date sur le noeud &quot;billet de blog&quot;, par exemple, ne signifie pas vraiment qu’un type de noeud spécial est nécessaire. Je vais à coup sûr utiliser `nt:unstructured` pour mes nœuds d’article de blog, du moins au début. Puisque dans mon application de blog, tout ce que je vais faire, c&#39;est d&#39;afficher la date lastModified de toute façon (éventuellement &quot;commander par&quot;), je me fiche à peine s&#39;il s&#39;agit d&#39;une date. Parce que je fais implicitement confiance à mon application de création de blog pour y mettre de toute façon une &quot;date&quot;, il n&#39;y a vraiment pas besoin de déclarer la présence d&#39;une `lastModified` date sous la forme d’un type de noeud.

### Règle #2 : piloter la hiérarchie du contenu ; ne pas laisser cela se produire. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explication {#explanation-2}

La hiérarchie de contenu est une ressource précieuse. Ne le laissez pas arriver ; concevez-le. Si vous n’avez pas de &quot;bon&quot; nom lisible par l’homme pour un noeud, c’est probablement quelque chose que vous devriez reconsidérer. Les nombres arbitraires ne sont pas un &quot;bon nom&quot;.

Bien qu&#39;il soit facile de placer rapidement un modèle relationnel existant dans un modèle hiérarchique, il faut y réfléchir.

D&#39;après mon expérience, si l&#39;on considère le contrôle d&#39;accès et le confinement comme de bons pilotes pour la hiérarchie du contenu. Pensez-y comme si c&#39;était votre système de fichiers. Vous pouvez peut-être même utiliser des fichiers et des dossiers pour le modéliser sur votre disque local.

Personnellement, je préfère d&#39;abord les conventions de hiérarchie au système de saisie de noeud, et j&#39;introduis la saisie ultérieurement.

>[!CAUTION]
>
>La structure d’un référentiel de contenu peut également avoir un impact sur les performances. Pour de meilleures performances, le nombre de noeuds enfants associés à des noeuds individuels dans un référentiel de contenu ne doit pas dépasser 1 000.
>
>Pour plus d’informations, reportez-vous à la section [Quelle quantité de données CRX peut-il traiter ?](https://helpx.adobe.com/fr/experience-manager/kb/CrxLimitation.html)

#### Exemple {#example-2}

Je modéliserais un simple système de blogs comme suit. Au départ, je ne me soucie même pas des types de noeuds respectifs que j’utilise à ce stade.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Je pense que l&#39;une des choses qui devient visible est que la structure du contenu est comprise en se basant sur l&#39;exemple sans aucune explication supplémentaire.

Ce qui peut être inattendu dans un premier temps, c&#39;est pourquoi je ne stockerais pas les &quot;commentaires&quot; avec le &quot;post&quot;, ce qui est dû au contrôle d&#39;accès que je voudrais appliquer d&#39;une manière raisonnablement hiérarchique.

En utilisant le modèle de contenu ci-dessus, je peux facilement permettre à l’utilisateur &quot;anonyme&quot; de &quot;créer&quot; des commentaires, mais de garder l’utilisateur anonyme en lecture seule pour le reste de l’espace de travail.

### Règle #3 : les espaces de travail sont destinés à clone(), merge() et update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explication {#explanation-3}

Si vous n’utilisez pas de méthode `clone()`, `merge()` ou `update()` dans votre application, l’espace de travail unique est probablement la voie à suivre.

&quot;Noeuds correspondants&quot; est un concept défini dans la spécification JCR. Essentiellement, il se résume à des noeuds qui représentent le même contenu, dans différents soi-disant espaces de travail.

JCR introduit le concept abstrait des espaces de travail, ce qui laisse de nombreux développeurs dans l’incertitude sur la manière de les utiliser. Je vous propose de mettre à l’épreuve votre utilisation des espaces de travail comme suit.

Si vous avez un chevauchement considérable des noeuds &quot;correspondants&quot; (essentiellement les noeuds ayant le même UUID) dans plusieurs espaces de travail, vous pouvez probablement utiliser les espaces de travail à bon escient.

S’il n’existe aucun chevauchement de noeuds avec le même UUID, vous abusez probablement des espaces de travail.

N’utilisez pas d’espaces de travail pour le contrôle d’accès. La visibilité du contenu d’un groupe d’utilisateurs spécifique n’est pas un bon argument pour séparer les éléments dans différents espaces de travail. JCR propose un &quot;contrôle d’accès&quot; dans le référentiel de contenu pour y répondre.

Les espaces de travail sont les limites des références et des requêtes.

#### Exemple {#example-3}

Utilisez des espaces de travail pour des éléments tels que :

* v1.2 du projet par rapport à la version v1.3 du projet
* un &quot;développement&quot;, un &quot;contrôle qualité&quot; et un état de contenu &quot;publié&quot; ;

N’utilisez pas d’espaces de travail pour des éléments tels que :

* répertoires d’accueil des utilisateurs
* contenu distinct pour différentes audiences cibles, telles que public, privé, local, etc.
* boîtes de réception pour différents utilisateurs

### Règle #4 : Attention aux frères du même nom. {#rule-beware-of-same-name-siblings}

#### Explication {#explanation-4}

Same Name Siblings (SNS) a été introduit dans la spécification afin de permettre la compatibilité avec les structures de données conçues et exprimées au moyen de XML et, par conséquent, utiles à JCR. Toutefois, le SNS s’accompagne de surcharge et de complexité pour le référentiel.

Tout chemin d’accès dans le référentiel de contenu qui contient un SNS dans l’un de ses segments de chemin d’accès devient beaucoup moins stable. Si un SNS est supprimé ou réorganisé, il a un impact sur les chemins de tous les autres SNS et de leurs enfants.

Pour l&#39;import de XML ou l&#39;interaction avec du XML existant, le SNS peut être nécessaire et utile, mais je n&#39;ai jamais utilisé le SNS (et je n&#39;ai jamais eu l&#39;intention) dans mes modèles de données &quot;champ vert&quot;.

#### Exemple {#example-4}

Utilisez

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

Au lieu de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Règle #5 : Les références sont considérées comme nocives. {#rule-references-considered-harmful}

#### Explication {#explanation-5}

Les références impliquent une intégrité référentielle. Il est important de comprendre que les références ajoutent un coût supplémentaire pour la gestion de l’intégrité référentielle, mais qu’elles sont également coûteuses du point de vue de la flexibilité du contenu.

Personnellement, je n’utilise que des références lorsque je ne peux pas vraiment gérer une référence agressive et utiliser autrement un chemin, un nom ou un UUID de chaîne pour faire référence à un autre noeud.

#### Exemple {#example-5}

Supposons que j’autorise les &quot;références&quot; d’un document (a) à un autre document (b). Si je modélise cette relation à l’aide de propriétés de référence, cela signifie que les deux documents sont liés au niveau du référentiel. Je ne peux pas exporter/importer le document (a) individuellement, car la cible de la propriété de référence n’existe peut-être pas. D’autres opérations telles que la fusion, la mise à jour, la restauration ou le clonage sont également affectées.

Je vais donc soit modéliser ces références comme &quot;références faibles&quot; (dans JCR v1.0, cela se résume essentiellement aux propriétés de chaîne qui contiennent l’uuid du noeud cible), soit utiliser simplement un chemin d’accès. Parfois, le chemin est plus significatif pour commencer.

Je pense qu&#39;il y a des cas d&#39;utilisation où un système ne peut vraiment pas fonctionner si une référence est pendouillante, mais je ne peux simplement pas trouver un bon exemple &quot;réel&quot; mais simple de mon expérience directe.

### Règle n°6 : des fichiers sont des fichiers. {#rule-files-are-files}

#### Explication {#explanation-6}

Si un modèle de contenu expose quelque chose qui ressemble même de loin à un fichier ou à un dossier, j’essaie d’utiliser (ou d’étendre à partir de) `nt:file`, `nt:folder`, et `nt:resource`.

D’après mon expérience, de nombreuses applications génériques permettent d’interagir implicitement avec nt:folder et nt:files et savent gérer et afficher ces événements s’ils sont enrichis de méta-informations supplémentaires. Par exemple, une interaction directe avec des implémentations de serveur de fichiers comme CIF ou WebDAV assis sur JCR devient implicite.

Je pense que la bonne règle de base pourrait utiliser les éléments suivants : Si vous devez stocker le nom de fichier et le type MIME, alors `nt:file`/ `nt:resource` est une bonne correspondance. Si vous pouvez avoir plusieurs « fichiers », nt:folder constitue l’emplacement de stockage idéal.

Si vous devez ajouter des méta-informations pour votre ressource, supposons qu’il s’agisse d’une propriété &quot;author&quot; ou &quot;description&quot;, étendez `nt:resource` not the `nt:file`. J’étends rarement un nt:file, mais souvent un `nt:resource`.

#### Exemple {#example-6}

Supposons que quelqu’un souhaite télécharger une image dans une entrée de blog à l’adresse :

```xml
/content/myblog/posts/iphone_shipping
```

Et peut-être que la première réaction intestinale serait d&#39;ajouter une propriété binaire contenant l&#39;image.

Bien qu’il existe de bons cas d’utilisation pour l’utilisation d’une propriété binaire (supposons que le nom n’est pas pertinent et que le type MIME soit implicite), dans ce cas, je recommande la structure suivante pour mon exemple de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Règle #7 : Les identifiants sont mauvais. {#rule-ids-are-evil}

#### Explication {#explanation-7}

Dans les bases de données relationnelles, les identifiants sont un moyen nécessaire pour exprimer les relations, de sorte que les gens ont tendance à les utiliser également dans les modèles de contenu. Surtout pour les mauvaises raisons.

Si votre modèle de contenu est plein de propriétés qui se terminent par &quot;Id&quot;, vous n’utilisez probablement pas correctement la hiérarchie.

Il est vrai que certains noeuds ont besoin d’une identification stable tout au long de leur cycle de vie ; moins que vous ne le pensez. Mais `mix:referenceable` dispose d’un tel mécanisme intégré dans le référentiel. Il n’est donc pas nécessaire de trouver un moyen supplémentaire d’identifier un noeud de manière stable.

Gardez également à l’esprit que les éléments peuvent être identifiés par le chemin d’accès. Et, même si les &quot;symlinks&quot; ont plus de sens pour la plupart des utilisateurs que les liens durs dans un système de fichiers UNIX®, un chemin d’accès a un sens pour la plupart des applications pour faire référence à un noeud cible.

Plus important encore, il s’agit **mix**:référenceable, ce qui signifie qu’il peut être appliqué à un noeud au moment où vous devez le référencer.

Ainsi, le fait que vous souhaitiez potentiellement référencer un noeud de type &quot;Document&quot; ne signifie pas que votre type de noeud &quot;Document&quot; doit s’étendre à partir de `mix:referenceable` d&#39;une manière statique. En effet, il peut être ajouté dynamiquement à n’importe quelle instance du &quot;document&quot;.

#### Exemple {#example-7}

Utilisez :

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

Au lieu de :

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
