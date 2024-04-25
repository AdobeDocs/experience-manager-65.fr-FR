---
title: Fonctionnalité de blog
description: Découvrez comment la fonction de blog prend en charge la fourniture d’informations de communauté dans un format de journalisation. Les entrées sont effectuées dans l’environnement de publication par les utilisateurs autorisés.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 1%

---

# Fonctionnalité de blog {#blog-feature}

## Présentation {#introduction}

La fonction de blog d’AEM Communities est passée d’une activité de création à une véritable activité communautaire qui a lieu dans l’environnement de publication.

La fonctionnalité de blog prend en charge la fourniture d’informations communautaires dans un format de journalisation. Les entrées de blog sont créées dans l’environnement de publication par des membres autorisés (utilisateurs enregistrés, connectés).

La fonction de blog fournit :

* Création côté publication d’articles de blog et de commentaires
* Modification de texte enrichi
* Images intégrées (avec prise en charge du glisser-déposer)
* Contenu de réseau social intégré ([Prise en charge de l’intégration](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Mode Brouillon
* Publication planifiée
* Composer au nom de (a [membre privilégié](/help/communities/users.md#privileged-members-group) peut créer du contenu au nom d’un autre membre de la communauté)
* [Modération contextuelle et en bloc](/help/communities/moderate-ugc.md) des articles de blog et des commentaires

Cette section de la documentation décrit :

* Ajout de la fonction de blog à un site AEM
* Paramètres de configuration des composants de blog

>[!NOTE]
>
>Les composants `Journal` et `Journal Sidebar` sont intitulés `Blog` et `Blog Sidebar`.
>
>La fonctionnalité de blog disponible dans AEM version 6.0 et antérieure est désormais supprimée. Il était basé sur un modèle et autorisait uniquement les auteurs à créer du contenu dans l’environnement de création.

## Ajout de composants de blog à une page {#adding-blog-components-to-a-page}

Si vous souhaitez ajouter un blog à une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Blog`
* `Communities / Blog Sidebar`

Faites-les glisser sur une page où le blog doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/blog-developer-basics.md#essentials-for-client-side) sont inclus, la variable `Blog` Le composant apparaît comme suit :

![add-blog-component](assets/add-blog-component.png)

### Configuration du blog {#configuring-blog}

Sélectionnez le `Blog` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

![Paramètres de blog](assets/blog-configure.png)

#### Onglet Paramètres {#settings-tab}

Sous , **Paramètres** , spécifiez les fonctions de base du blog :

* **Autoriser la miniature des pièces jointes**

  Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. de miniature des pièces jointes**

  Taille maximale (en pixels) de la miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image min. pour la miniature**

  Taille minimale (en octets) de l’image pour générer une miniature pour les images intégrées. La valeur par défaut est de 100000 octets (100 Ko).

* **Taille maximale des miniatures**

  Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Autoriser les membres privilégiés**

  Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres autorisés**

  Ajoutez les membres privilégiés autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition de l’auteur**

  S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode création.

* **Titre du journal**

  Titre du blog à afficher sur la page.

>[!NOTE]
>
>Le titre du journal permet de créer automatiquement l’URL du blog.
>
>50 caractères maximum (avec 5 caractères supplémentaires pour l’unicité) sont utilisés à partir du titre du journal que vous indiquez ici pour créer l’URL du blog.

* **Description du journal**

  Description du blog.

* **Sujets par page**

  Définit le nombre d’entrées/de commentaires de blog affichés par page. La valeur par défaut est 10.

* **Modéré**

  Si cette option est cochée, les entrées et les commentaires de blog doivent être approuvés avant d’apparaître sur un site publié. La valeur par défaut est décochée.

* **Fermé**

  Si cette case est cochée, le blog est fermé aux nouveaux commentaires et entrées de blog. La case par défaut est décochée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les entrées et les commentaires de blog peuvent être saisis avec des balises. La valeur par défaut est cochée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir **Champ de balise** ). La case par défaut est décochée.

* **Autoriser les chargements de fichiers**

  Si cette option est cochée, les fichiers joints peuvent être ajoutés à une entrée ou à un commentaire de blog. La case par défaut est décochée.

* **Taille de fichier maximale**

  Pertinent uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichiers autorisés**

  Pertinent uniquement si `Allow File Uploads` est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ils ne peuvent pas être transférés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses**

  Si cette option est cochée, les réponses aux commentaires sont publiées dans l’entrée de blog. La case par défaut est décochée.

* **Autoriser le vote**

  Si cette case est cochée, la fonction de vote est ajoutée à une entrée de blog. La case par défaut est décochée.

* **Autorisation des utilisateurs à supprimer des commentaires et des sujets**

  Si cette case est cochée, autorisez les membres à supprimer les commentaires et les entrées de blog qu’ils ont publiés. La case par défaut est décochée.

* **Autoriser l’exécution**

  Si cette case est cochée, incluez la fonction suivante pour les articles de blog, ce qui permet aux membres d’être [notifié](/help/communities/notifications.md) de nouvelles publications. La case par défaut est décochée.

* **Autoriser les abonnements aux emails**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Nécessite `Allow Following` à vérifier et [email configuré](/help/communities/email.md). La case par défaut est décochée.

* **Badges d’affichage**

  Si cette case est cochée, affichez les droits gagnés et attribués. [badges](/help/communities/implementing-scoring.md) avec l&#39;entrée de blog d&#39;un membre. La case par défaut est décochée.

* **Ne pas obtenir de réponses sur la page de liste**

* **Autoriser le contenu proposé**

  Si cette case est cochée, l’idée est identifiée comme [contenu proposé](/help/communities/featured.md). La case par défaut est décochée.

* **Activer la mention**

  S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs propres mentions.

* **Nombre max. de mentions**

  Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle de mention d’interface utilisateur**

  Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous , **Modération d’utilisateur** , spécifiez les paramètres de modération :

* **Refuser des publications**

  Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. La case par défaut est décochée.

* **Fermer/rouvrir les rubriques**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. La case par défaut est décochée.

* **Marquer les publications**

  Si cette case est cochée, les membres ont le droit de marquer les sujets ou commentaires d’autres personnes comme étant inappropriés. La case par défaut est décochée.

* **Marquer la liste de motifs**

  Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Motif de l’indicateur personnalisé**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. S’il est défini sur -1, le sujet ou le commentaire marqué n’est jamais masqué à la vue du public. Sinon, ce nombre doit être supérieur ou égal au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous , **Champ de balise** , indiquez les balises qui peuvent être appliquées si **Autoriser le balisage** est coché sur la **Paramètres** tab :

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous **Paramètres** . Les balises qui peuvent être appliquées sont limitées aux balises dans les catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestion**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur de -1 signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

### Configuration de la barre latérale de blog {#configuring-blog-sidebar}

Lorsque vous double-cliquez sur le `Blog Sidebar` , une boîte de dialogue de modification s’ouvre.

Sous , **Paramètres de la barre latérale du journal** , indiquez le format de date des archives et le type d’entrée à afficher dans la barre latérale :

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Format de date**

  Format utilisé pour l’affichage des archives des entrées de blog. Le format utilise des espaces réservés conformément à la convention Java™.

   * aaaa : année complète, par exemple &quot;2015&quot;
   * yy : courte année, par exemple &quot;15&quot;
   * MMMM : mois complet, comme juin
   * MMM : court mois, comme juin
   * MM : numéro du mois, par exemple 06

  La valeur par défaut est &quot;yyy MMMM&quot;, qui afficherait, par exemple, &quot;2015 June&quot;.

* **Type d’affichage**

  Titre et type des entrées de blog à afficher dans la barre latérale. Le choix se fait entre

   * Auteurs
   * Catégories
   * Archives

* **Chemin du composant Blog**

  *(Facultatif)* Emplacement de la ressource de blog à partir de laquelle les articles de blog doivent être répertoriés. Si rien n’est indiqué, le composant resourceType est utilisé. `social/journal/components/hbs/journal` qui s’affiche sur la même page.

   * Par exemple, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`.

* **Limite de suggestion**

  Nombre d’articles de blog à afficher. Une valeur de -1 signifie qu’aucune limite n’est définie. La valeur par défaut est -1.

## Expérience du visiteur du site {#site-visitor-experience}

Dans l’environnement de publication, la fonction de blog affiche l’article de blog le plus récent suivi des articles de blog plus anciens dans l’ordre décroissant de leur création. Les encadrés de blog permettent aux visiteurs du site d’appliquer des filtres pour limiter la sélection des articles de blog affichés.

L&#39;article de blog est suivi d&#39;un lien pour publier ou afficher des commentaires.

Lorsqu’un article de blog est sélectionné, l’article de blog et les commentaires s’affichent (s’ils sont activés).

Les autres fonctionnalités dépendent si le visiteur du site est modérateur, administrateur, membre de la communauté, membre privilégié ou anonyme.

### Utilisation des articles {#working-with-articles}

Lors de la création d’un article de blog, vous avez la possibilité d’effectuer les opérations suivantes :

1. Publier immédiatement
1. Publication d’un brouillon
1. Publier à une date et une heure planifiées

Les articles de blog s’affichent sous l’onglet approprié (Publié, Versions préliminaires ou Planifié) pour les membres pouvant créer sur publication.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut effectuer les opérations suivantes : [tâches de modération](/help/communities/moderate-ugc.md) (comme autorisé par la configuration du composant) sur tous les articles de blog et commentaires publiés sur un blog.

![modérateur-page d’accueil](assets/moderator-homepage.png)

#### Membres {#members}

Lorsque l’utilisateur connecté est membre de la communauté ou [membre privilégié](/help/communities/users.md#privileged-members-group) (selon la configuration), ils peuvent sélectionner `New Article` pour créer et publier un nouvel article de blog.

Plus précisément, ils peuvent :

* Création d’un article de blog
* Publier un nouvel article de blog au nom d’un autre membre
* Publication d’un commentaire sur un article de blog
* Modifier son propre article ou commentaire de blog
* Supprimer son propre article ou commentaire de blog
* Marquer les articles ou commentaires de blog d’autres

![member-homepage](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anonyme {#anonymous}

Les visiteurs qui ne sont pas connectés ne peuvent lire que les articles et commentaires de blog publiés, les traduire s’ils sont pris en charge, mais ne peuvent pas ajouter un article de blog ou un commentaire, ni marquer les articles ou commentaires d’autres personnes.

![anonymous-user-view](assets/anonymous-user-view.png)

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur les blogs](/help/communities/blog-developer-basics.md) pour les développeurs.

Pour la modération des commentaires et des entrées de blog, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les entrées et les commentaires de blog, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour obtenir la traduction des commentaires et des entrées de blog, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md).
