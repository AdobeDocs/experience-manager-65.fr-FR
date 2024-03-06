---
title: Personnalisation
description: Découvrez la personnalisation dans Adobe Experience Manager afin de fournir à l’utilisateur un environnement sur mesure affichant du contenu dynamique.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 91%

---

# Personnalisation {#personalization}

## Qu’est-ce que la personnalisation ? {#what-is-personalization}

Le volume de contenu disponible sur Internet, sur les sites extranet ou sur les sites intranet ne cesse d’augmenter.

La personnalisation consiste à fournir à l’utilisateur ou l’utilisatrice un environnement sur mesure affichant du contenu dynamique sélectionné selon ses besoins spécifiques, que ce soit sur la base de profils prédéfinis, de la sélection d’utilisateurs et d’utilisatrices ou du comportement interactif de l’utilisateur ou l’utilisatrice.

La personnalisation comporte trois éléments principaux :

### Utilisateurs {#users}

* Ils disposent de profils, qu’ils soient individuels ou de groupe. Ces profils présentent des caractéristiques (par exemple, description de poste, lieu, intérêts) qui peuvent être utilisées pour personnaliser le contenu que les utilisateurs peuvent afficher.
* Ils effectuent des actions. Ces actions peuvent être analysées et associées à des règles de comportement dans le but de personnaliser le contenu affiché.

### Contenu {#content}

* Constitue ce que l’utilisateur souhaite voir. Il s’agit de préférence d’un contenu ciblé et permettant à l’utilisateur d’effectuer ses tâches.
* Elles peuvent être catégorisées et donc mises à la disposition des utilisateurs selon des règles prédéfinies.
* Elles doivent être dynamiques.

En d’autres termes, le contenu doit, d’une certaine manière, dépendre de l’utilisateur. Si chaque utilisateur voit le même contenu, la personnalisation est redondante.

### Règles {#rules}

* Elles indiquent comment s’effectue la personnalisation (quel contenu l’utilisateur peut voir et quand).

La personnalisation peut être soit :

#### Explicite {#explicit}

* Personnalisation : l’utilisateur effectue des sélections à partir de différentes sources de contenu.

#### Implicite {#implicit}

* Basée sur les règles : les responsables d’entreprise définissent des règles spécifiques pour les actions en fonction de profils et/ou de comportements spécifiques.
* Filtrage simple : les sélections se font sur la base de profils prédéfinis au niveau de l’utilisateur ou l’utilisatrice et/ou du groupe.
* Filtrage collaboratif ou sur recommandation : le comportement de l’utilisateur est enregistré selon des règles prédéfinies. Ces règles sont basées sur le comportement observé chez des personnes ayant des centres d’intérêt similaires. Les informations collectées sont utilisées pour personnaliser les informations affichées pour l’utilisateur ou l’utilisatrice, notamment sous la forme de recommandations.

## Comment et quand la personnalisation peut-elle être utilisée ? {#how-and-when-can-personalization-be-used}

La personnalisation peut être utilisée dans de nombreuses situations :

### Dans des pages intranet {#intranet-pages}

* Le contenu peut être affiché en fonction du lieu, du service et du rôle de l’utilisateur, ces éléments étant déjà définis sur le réseau interne.
* Selon le choix disponible, l’utilisateur peut effectuer d’autres sélections.

### Des groupes d’utilisateurs spécifiques, restreints et ciblés - En extranet {#extranets}

* Les utilisateurs ont besoin d’une connexion pour l’autorisation. Celle-ci est liée à un profil qui fournit les informations nécessaires à la personnalisation ; des détails tels que leur emplacement, leur relation avec le produit, l’historique d’utilisation, les responsabilités budgétaires, etc.
* Ces instances peuvent s’étendre sur plusieurs sites, tels que :
* Des entreprises qui fournissent des sites web à une partie hautement spécialisée de leur marché, par exemple, une entreprise pharmaceutique qui fournit un site web spécialisé pour les médecins.
* Les entreprises qui fournissent des sites web permettant à leurs clients de consulter les informations de compte et de facturation actuelles ; par exemple, les opérateurs téléphoniques.

### Sur des sites web de vente et de distribution {#sales-site}

* Les sites web de vente et de distribution (par exemple, Amazon) peuvent combiner un profil utilisateur et l’historique des ventes et de la navigation de l’utilisateur pour lui suggérer d’autres choix susceptibles de l’intéresser.

### Sur des sites web de recherche {#search-site}

* La plupart des grands moteurs de recherche sont des outils analytiques très puissants qui enregistrent le comportement des utilisateurs, les termes qu’ils saisissent et les sites web qu’ils visitent. Ces données sont ensuite utilisées pour personnaliser le contenu fourni, notamment par rapport à l’affichage des publicités.

### Avantages liés à la personnalisation et aspects à prendre en considération {#strengths-of-personalization-and-points-to-consider}

Voici quelques raisons de recourir à la personnalisation :

* Un utilisateur ou une utilisatrice peut découvrir un site web agréable et ciblé.
* La personnalisation peut être utilisée pour propager automatiquement l’accès à la dernière version du contenu.
* Les fonctionnalités de Social Collaboration permettent aux utilisateurs et utilisatrices de communiquer entre eux, car elles peuvent être identifiées par leurs profils.
* L’utilisateur reçoit le contenu dont il a besoin pour accomplir une tâche spécifique. Dans le cadre de l’intranet d’une entreprise,il peut s’agir d’un outil précieux de diffusion de l’information.
* L’utilisateur ou l’utilisatrice peut recevoir le contenu dont il ou elle a besoin, ce qui réduit le temps nécessaire pour effectuer des opérations de recherche.
* Le fournisseur de contenu peut diriger le contenu à afficher selon des catégories spécifiques d’utilisateurs et utilisatrices.
* Des règles peuvent être définies pour fournir le contenu en fonction de combinaisons associant à la fois les caractéristiques et le comportement de l’utilisateur. Cela fournit un mécanisme sophistiqué pour personnaliser leur expérience sur le web.

Lorsque vous utilisez la personnalisation, tenez compte des aspects suivants :

#### Les performances {#performance}

* Naturellement, toute analyse et toute évaluation supplémentaires peuvent avoir un impact sur les performances. Toutefois, les méthodes utilisées sont très sophistiquées et peuvent être optimisées pour minimiser l’impact.

#### L’autorisation {#authorization}

* La personnalisation requiert un mécanisme de connexion car le site web doit pouvoir identifier l’utilisateur.

#### La mise en cache {#caching}

* La mise en cache est un aspect que l’utilisateur perçoit en termes de performances et de précision (à quelle vitesse le site web affiche le contenu personnalisé et si ce contenu est toujours à jour).
* La mise en cache est une considération clé dans la configuration de la personnalisation, et du temps doit être consacré pour garantir que l’implémentation utilisée est adaptée.

>[!TIP]
>
>L’effet de la personnalisation sur les performances et des rubriques concernant la mise en cache associées sont abordés plus en détail dans le document [Optimisation des performances.](/help/sites-deploying/configuring-performance.md)

#### La précision des règles {#accuracy}

* La personnalisation réalisée en suivant le comportement de l’utilisateur ou l’utilisatrice, ou en définissant des règles basées sur le profil de l’utilisateur ou l’utilisatrice doit être précise et logique.
* Il n’y a rien de plus frustrant pour l’utilisateur ou l’utilisatrice que de se voir imposer ou refuser du contenu en raison de la logique inexacte d’une règle.
* Par conséquent, les règles doivent être pensées avec soin, en ayant d’abord à l’esprit les besoins de l’utilisateur. Cela peut nécessiter beaucoup d’efforts et ne doit pas être sous-estimé ; la définition des règles de fonctionnement l’emporte souvent sur l’effort technique lors de la mise en oeuvre de la personnalisation.

#### Le moment où l’utiliser {#when-to-use}

* Comme un grand nombre de fonctionnalités sur le web, la personnalisation doit être utilisée avec prudence. Son utilisation profitera-t-elle vraiment à l’utilisateur ou l’utilisatrice ? Cette question doit toujours être la première question posée. Mais on peut aussi se demander si l’objectif recherché peut être atteint à moindre effort par une autre méthode. La personnalisation peut courir le risque d’être une fonctionnalité que les utilisateurs ne configurent qu’une seule fois (pour voir comment elle fonctionne), dans la mesure où elle ne leur offre aucun avantage réel.
* La personnalisation n’a de sens que si le contenu affiché est dynamique et dépend d’une certaine manière de l’utilisateur. Si tous les utilisateurs voient le même contenu, la personnalisation est redondante.

#### La confidentialité {#confidentiality}

* De nombreux utilisateurs sont soucieux de la protection et de la sécurité des données, En particulier concernant les données récupérées lors du suivi de leur comportement lors de la navigation sur le web.

## Personnalisation et accès {#personalization-and-access}

La personnalisation doit être considérée séparément du contrôle d&#39;accès, mais ils sont interdépendants.

La personnalisation ne crée en elle-même aucune forme de contrôle d’accès. Il s’agit simplement d’une méthode permettant de piloter ce que l’utilisateur ou l’utilsatrice voit. Elle ne limite pas l’accès de l’utilisateur ou l’utilisatrice à un autre contenu et, comme pour tout contenu, les contrôles d’accès appropriés doivent être déjà attribués.

Toutefois, le contrôle d’accès peut être utilisé pour créer une forme de personnalisation. Si vous autorisez ou refusez à un utilisateur ou une utilisatrice l’accès au contenu, cela affecte inévitablement le choix du contenu dont il ou elle dispose, personnalisant ainsi son expérience web.

## Composants disponibles pour la personnalisation {#components-available-for-personalization}

Divers composants sont fournis avec AEM en vue de la personnalisation. Certains permettent aux utilisateurs et utilisatrices de se connecter et de modifier leurs profils, d’autres (comme Mes gadgets) leur permettent de configurer une page spécifique :

| Titre dans le sidekick | Objectif |
|---|---|
| Champ du mot de passe coché | Demande le mot de passe et la confirmation de celui-ci. |
| Connexion combinée | Permet à l’utilisateur de se connecter à un compte existant ou d’enregistrer un nouveau compte. |
| Champ d’adresse de formulaire | Un champ complexe permettant la saisie d’une adresse internationale. |
| Début de formulaire | Commence une définition de formulaire. |
| Captcha de formulaire | Champ constitué d’un mot alphanumérique qui s’actualise automatiquement. Le composant captcha protège les sites web contre les robots. |
| Groupe de cases à cocher de formulaire | Plusieurs éléments organisés en une liste et précédés de cases à cocher. Les utilisateurs et utilisatrices peuvent cocher plusieurs cases. |
| Liste déroulante de formulaire | Plusieurs éléments organisés dans une liste déroulante. Le commutateur Plusieurs sélections possibles spécifie si plusieurs éléments peuvent être sélectionnés depuis la liste. |
| Fin de formulaire | Termine la définition du formulaire. |
| Chargement du fichier de formulaire | Un élément de chargement qui permet à l’utilisateur de charger un fichier sur le serveur. |
| Champ masqué de formulaire | Ce champ ne s’affiche pas pour l’utilisateur ou l’utilisatrice. Il peut être utilisé pour transférer une valeur vers le client et revenir au serveur. Ce champ ne doit pas avoir de contraintes. |
| Bouton Image de formulaire | Un bouton d’envoi supplémentaire pour le formulaire qui est rendu en une image. |
| Champ de mot de passe de formulaire | Similaire au champ de texte mais seule une ligne est autorisée et la saisie de texte par l’utilisateur n’est pas visible dans le champ. |
| Groupe de cases d’option de formulaire | Plusieurs éléments organisés en une liste précédés d’un bouton radio. Les utilisateurs et utilisatrices ne doivent sélectionner qu’un seul bouton radio. |
| Bouton Envoyer de formulaire | Un bouton d’envoi supplémentaire pour le formulaire avec le titre affiché comme texte sur le bouton. |
| Champ de texte de formulaire | Champ de texte qui permet aux utilisateurs de saisir des informations. |
| Mes gadgets | Permet d’inclure l’une des sélections de gadgets disponibles. |
| Photo de l’avatar du profil | Permet le chargement d’une photo d’avatar. |
| Nom détaillé du profil | Saisie des détails du nom, y compris des éléments tels que le titre, le deuxième nom et le suffixe si nécessaire. |
| Nom d’affichage du profil | Nom à afficher. |
| E-mail du profil | Saisie d’une adresse électronique. |
| Genre du profil | Permet la saisie du genre. |
| Numéro de téléphone principal du profil | Permet la saisie d’un numéro de téléphone. |
| Principale URL du profil | Permet la saisie d’une URL. |
| Propriété du texte général du profil | Propriétés du profil. |
| Connexion | Permet d’envoyer un nom d’utilisateur et un mot de passe lors de la connexion. |
| Déconnexion | Indique l’utilisateur est actuellement connecté et fournit un lien pour se déconnecter. |
| Nuage de balises | Un nuage de balises pour représenter graphiquement une sélection de balises dans votre site web. |
| Teaser | Un élément de contenu (habituellement une image) affiché sur une page principale pour « inciter » les utilisateurs à accéder au contenu sous-jacent. |

## Personnalisation et contenu de la communauté {#personalization-and-community-content}

Les fonctions de communauté telles que les blogs, les forums et les calendriers entraînent la création de contenu de communauté, généralement appelé contenu créé par l’utilisateur. Lorsque du contenu créé par l’utilisateur est entré dans un environnement de publication consistant en plusieurs instances AEM ([ferme de publication](/help/communities/topologies.md)), il était difficile de trouver un moyen de synchroniser ce contenu sur toutes les instances.

Avec l’extension [AEM Communities 6.1](/help/communities/overview.md), ce problème est résolu avec un [magasin commun pour tout le contenu créé par l’utilisateur](/help/communities/working-with-srp.md). Concernant la personnalisation, Communities comprend la [connexion sociale](/help/communities/social-login.md), à savoir la possibilité pour les visiteurs du site de se connecter via Facebook et Twitter.

Sans l’extension Communities, les différentes méthodes à examiner pour résoudre le problème lié à l’homogénéité du contenu créé par l’utilisateur sont les suivantes :

* Synchroniser de multiples instances de publication si nécessaire
* Envoyer le contenu créé par l’utilisateur de l’instance de publication à l’environnement de création, à partir duquel il peut être publié de façon similaire à la publication du contenu des pages

La méthode utilisée pour obtenir la cohérence du contenu généré par l’utilisateur dans un environnement de publication constitué de plusieurs instances de publication doit être soigneusement conçue et testée pour assurer les performances et la cohérence.
