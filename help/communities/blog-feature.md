---
title: Fonction Blog
seo-title: Fonction Blog
description: Informations sur la communauté dans un format journalistique
seo-description: Informations sur la communauté dans un format journalistique
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Fonction Blog {#blog-feature}

## Présentation {#introduction}

La fonction Blog pour AEM Communities a été transformée. D’une activité de création, elle est passée à une véritable activité communautaire au sein même de l’environnement de publication.

Elle présente des informations issues des membres de la communauté dans un format similaire à un journal. Les entrées de blog sont créées dans l’environnement de publication par les membres autorisés (utilisateurs inscrits et connectés).

La fonction Blog comporte les éléments suivants :

* Création du côté publication des articles et des commentaires de blog
* Modification de texte enrichi
* Images intégrées (avec glisser-déposer)
* Contenu de réseaux sociaux intégré ([prise en charge du format oEmbed](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Mode Brouillon
* Publication planifiée
* Fonction Composer au nom d’un utilisateur (un [membre privilégié](/help/communities/users.md#privileged-members-group) peut créer du contenu pour le compte d’un autre membre de la communauté)
* [Modération contextuelle et globale](/help/communities/moderate-ugc.md) des articles et des commentaires de blog

Cette section de la documentation décrit : :

* Ajout de la fonction de blog à un site AEM
* Paramètres de configuration des composants de blog

>[!NOTE]
>
>Les composants `Journal`et `Journal Sidebar` sont intitulés `Blog` et `Blog Sidebar`.
>
>La fonction Blog disponible dans AEM 6.0 et versions antérieures a été supprimée. Elle était basée sur un modèle et autorisait uniquement les auteurs à créer du contenu dans l’environnement de création.

## Ajout de composants de blog à une page {#adding-blog-components-to-a-page}

Si vous souhaitez ajouter un blog à une page en mode création, utilisez le navigateur de composants pour localiser

* `Communities / Blog`
* `Communities / Blog Sidebar`

et faites glisser les composants sur la page à l’endroit où le blog doit figurer.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/blog-developer-basics.md#essentials-for-client-side) are included, this is how the `Blog`component will appear :

![chlimage_1-229](assets/chlimage_1-229.png)

Et comment `Blog Sidebar` apparaîtra :

![chlimage_1-230](assets/chlimage_1-230.png)

### Configuration du blog {#configuring-blog}

Select the placed `Blog` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-231](assets/chlimage_1-231.png) Paramètres ![du blog](assets/blog-configure.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, définissez les fonctionnalités de base du blog :

* **Autoriser les miniatures de pièces jointes**

   Si cette option est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**

   Taille minimale (en octets) de l’image pour la génération de vignettes pour les images en ligne. La valeur par défaut est 100 000 octets (100 Ko).

* **Taille maximale de la miniature**

   Taille maximale (en pixels) de l’image miniature pour l’image intégrée. La valeur par défaut est 800 x 800.

* **Autoriser les membres privilégiés**

   Si cette option est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**

   Ajouter les membres privilégiés sont autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Titre du journal**

   Titre du blog à afficher sur la page.

>[!NOTE]
>
>Le titre du  permet de créer automatiquement l&#39;URL du blog.
>50 caractères au maximum (5 caractères supplémentaires pour l&#39;unicité) sont utilisés à partir du titre du  que vous spécifiez ici pour créer l&#39;URL du blog.

* **Description du journal**

   Description du blog.

* **Sujets par page**

   Définit le nombre d&#39;entrées/commentaires de blog affichés par page. La valeur par défaut est 10.

* **Modéré**

   Si cette option est cochée, la publication des entrées et commentaires du blog doit être approuvée avant qu&#39;ils ne s&#39;affichent sur un site publié. La valeur par défaut est désactivée.

* **Fermé**

   Si cette option est cochée, le blog est fermé aux nouveaux commentaires et entrées de blog. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les entrées et les commentaires du blog peuvent être saisis avec une annotation. Cette option est cochée par défaut.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l&#39;ajout de pièces jointes à une entrée de blog ou à un commentaire. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   N’est pertinent que si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 1 048 57 600 (10 Mo).

* **Types de fichier autorisés**

   N’est pertinent que si `Allow File Uploads` est coché. d’extensions de fichier séparé par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **Taille max. du fichier image joint**

   N’est pertinent que si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Permettre des réponses**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés dans l&#39;entrée de blog. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, incluez la fonction de vote avec une entrée de blog. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et les entrées de blog qu&#39;ils ont publiés. La valeur par défaut est** **uncheck.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les articles de blog, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette option est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([](/help/communities/subscriptions.md)). Requiert `Allow Following` la vérification et la configuration [du](/help/communities/email.md)courrier électronique. Cette option n’est pas cochée par défaut.

* **Afficher les badges**

   Si cette option est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. Cette option n’est pas cochée par défaut.

* **Ne pas recevoir de réponses sur la page de liste**

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)incitatif. Cette option n’est pas cochée par défaut.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple : ~{{familyName}}{{donnname}}.

#### Onglet Modération utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur**, définissez les paramètres de modération :

* **Refuser les publications**

   Si cette option est cochée, les modérateurs membres de confiance seront autorisés à refuser les publications et à empêcher leur publication de s’afficher sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs de membres de confiance peuvent fermer une rubrique pour apporter d’autres modifications et commentaires et rouvrir une rubrique. Cette option n’est pas cochée par défaut.

* **Marquer les publications**

   Si cette option est cochée, autorisez les membres à signaler les sujets ou commentaires d’autres personnes comme inappropriés. Cette option n’est pas cochée par défaut**.**

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans un  déroulant, la raison pour laquelle ils signalent une rubrique ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à entrer leur propre raison de signaler une rubrique ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut**.**

* **Seuil de modération**

   Entrez le nombre de fois où une rubrique ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Entrez le nombre de fois où une rubrique ou un commentaire doit être marqué avant d’être masqué dans les  publics. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, spécifiez les balises qui peuvent être appliquées si l’option **Autoriser le balisage** est activée dans l’onglet **Paramètres** :

* **Espaces de noms autorisés**

   Pertinent si `Allow Tagging` est coché sous l’onglet **Paramètres **onglet. Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. Le de  inclut les balises standard (le par défaut) ainsi que l’option Inclure toutes les balises. La valeur par défaut n’est pas cochée, ce qui signifie que tous les  de  sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur -1 signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

### Configuration de la barre latérale de blog {#configuring-blog-sidebar}

When you double-click the `Blog Sidebar` component, an edit dialog opens up.

Sous l’onglet **Paramètres de la barre latérale du journal**, spécifiez le format de date pour les archives et le type d’entrées à afficher dans la barre latérale :

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Format de la date**

   Format utilisé pour afficher les archives des entrées de blog. Ce format utilise des espaces réservés conformes à la convention Java.

   * yyyy : année à 4 chiffres, par exemple « 2015 »
   * yy : année à 2 chiffres, par exemple « 15 »
   * MMMMM : mois complet, par exemple juin
   * MMM : mois abrégé, par exemple juil.
   * MM : numéro du mois, par exemple 06
   La valeur par défaut est &quot;yyyy MMMM&quot; qui s’afficherait, par exemple, &quot;2015 June&quot;

* **Type d&#39;affichage**

   Titre et type des entrées de blog à afficher dans la barre latérale. Le choix est le suivant

   * Auteurs
   * Catégories
   * Archives

* **Chemin d’accès au composant flopg**

   *(Facultatif)* Emplacement de la ressource de blog à partir de laquelle les articles de blog doivent être répertoriés. Si rien n’est indiqué, le composant de resourceType `social/journal/components/hbs/journal` qui apparaît sur la même page sera utilisé.

   * Par exemple, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite de suggestions**

   Nombre d&#39;articles de blog à afficher. La valeur -1 signifie aucune limite. La valeur par défaut est -1.

## Expérience des visiteurs {#site-visitor-experience}

Dans l’environnement de publication, la fonction Blog présente l’article de blog le plus récent suivi des articles plus anciens, dans l’ordre décroissant de leur création. Les barres latérales de blog permettent aux visiteurs d’appliquer des filtres pour limiter la sélection aux articles de blog affichés.

L’article de blog est suivi d’un lien qui permet de publier ou d’afficher des commentaires.

Lorsqu’un article de blog est sélectionné, l’article et ses commentaires sont affichés (si les commentaires sont activés).

Les autres choix varient selon que le visiteur est modérateur, administrateur, membre de la communauté, membre privilégié ou anonyme.

### Fonctionnement des articles {#working-with-articles}

Lors de la création d’un nouvel article de blog, vous avez le choix entre:

1. le publier immédiatement ;
1. publier son brouillon ;
1. le publier à une date et une heure définies.

Les articles de blog sont visibles sous l’onglet correspondant (Publié, Versions préliminaires ou Planifié) pour les membres autorisés à créer ou à publier.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’[activités de modération](/help/communities/moderate-ugc.md) (autorisées par la configuration du composant) pour tous les articles et commentaires de blog publiés sur un blog.

![chlimage_1-232](assets/chlimage_1-232.png)

#### Membres {#members}

When the signed in user is a community member or [privileged member](/help/communities/users.md#privileged-members-group) (depending on configuration), they are able to select `New Article` to create and post a new blog article.

Plus précisément, il est autorisé à:

* Création d’un article de blog
* Publier un nouvel article de blog pour le compte d&#39;un autre membre
* Publication d’un commentaire sur un article de blog
* Modifier un article ou un commentaire de blog
* Supprimer leur propre article ou commentaire de blog
* Marquer les articles ou commentaires des autres blogs

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### Anonyme {#anonymous}

Les visiteurs non inscrits peuvent lire les articles et les commentaires publiés sur un blog et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter un article ou un commentaire de blog, ni à marquer les articles ou les commentaires d’autres membres.

![chlimage_1-235](assets/chlimage_1-235.png)

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous aux [notions fondamentales sur la fonction Blog](/help/communities/blog-developer-basics.md) pour les développeurs.

Pour des informations sur la modération des commentaires et des entrées de blog, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

Pour baliser les entrées et commentaires de blog, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour des informations sur la traduction des commentaires et des entrées de blog, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
