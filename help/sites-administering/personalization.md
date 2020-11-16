---
title: 'Personnalisation  '
seo-title: 'Personnalisation  '
description: En savoir plus sur la personnalisation dans AEM.
seo-description: En savoir plus sur la personnalisation dans AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 78%

---


# Personnalisation  {#personalization}

## What is Personalization? {#what-is-personalization}

Le volume de contenu disponible aujourd’hui est en constante augmentation, que ce soit sur des sites Internet, extranet ou intranet.

La personnalisation vise à proposer à l’utilisateur un environnement sur mesure affichant un contenu dynamique sélectionné en fonction de ses besoins, que ce soit sur la base de profils prédéfinis, de choix faits par l’utilisateur ou du comportement interactif de l’utilisateur.

Trois éléments principaux sont impliqués dans la personnalisation :

**Utilisateurs**

* Ils disposent de profils, personnels ou de groupe. Ces profils présentent des caractéristiques (par exemple, description de poste, lieu, intérêts) qui peuvent être utilisées pour personnaliser le contenu que les utilisateurs peuvent afficher.
* Ils effectuent des actions. Ces actions peuvent être analysées et associées à des règles de comportement dans le but de personnaliser le contenu affiché.

**Contenu**

* Constitue ce que l’utilisateur souhaite voir. Il s’agit de préférence d’un contenu ciblé et permettant à l’utilisateur d’effectuer ses tâches.
* Il peut être classé, donc mis à la disposition des utilisateurs selon des règles prédéfinies. Le contenu doit être dynamique, à savoir qu’il doit être
* doit, d’une certaine manière, dépendre de l’utilisateur. Si chaque utilisateur voit le même contenu, la personnalisation est redondante.

Les **règles**

* définir comment la personnalisation se produit réellement - quel contenu l’utilisateur peut voir et quand.

La personnalisation peut être soit :

**Explicite**

* La personnalisation amène l’utilisateur à effectuer des sélections parmi différentes sources de contenu.

**Implicite**

* Elle repose sur des règles : les responsables de l’entreprise définissent des règles spécifiques pour chaque action en fonction de profils et/ou comportements spécifiques.
* Filtrage simple : les sélections sont effectuées sur la base de profils prédéfinis au niveau de l’utilisateur et/ou du groupe.
* Filtrage collaboratif/sur recommandation : le comportement de l’utilisateur est enregistré selon des règles prédéfinies. Ces règles sont basées sur le comportement observé chez des personnes ayant des centres d’intérêt similaires. Les informations collectées sont utilisées pour personnaliser les informations affichées sur l’écran de l’utilisateur, en particulier sous forme de recommandations.

## Comment et quand la personnalisation peut-elle être utilisée ? {#how-and-when-can-personalization-be-used}

La personnalisation peut être utilisée dans de nombreuses situations, par exemple :

**Pages intranet**

* Le contenu peut être diffusé en fonction de l&#39;emplacement, du département et/ou du rôle d&#39;un utilisateur, déjà défini dans un réseau interne.
* Selon le choix disponible, l’utilisateur peut effectuer d’autres sélections.

**Groupes d’utilisateurs spécifiques, restreints et ciblés (extranet)**

* Les utilisateurs ont besoin d’une connexion en vue de l’autorisation. Cette connexion est associée à un profil fournissant les informations nécessaires à la personnalisation et, le cas échéant, des détails tels que l’emplacement de l’utilisateur, son utilisation du produit, l’historique de son utilisation, les responsabilités budgétaires, etc.
* Ces instances peuvent être réparties sur plusieurs sites :
* Les entreprises qui fournissent des sites web à un segment hautement spécialisé de leur marché (par exemple, une entreprise pharmaceutique fournissant un site web professionnel destiné aux médecins).
* Les entreprises qui fournissent des sites web permettant au client de visualiser son compte et ses informations de facturation actuels (par exemple, les opérateurs de téléphonie).

**Site web de vente et de distribution**

* Les sites web de vente et de distribution (par exemple, Amazon) peuvent combiner un profil utilisateur et l’historique des ventes et de la navigation de l’utilisateur pour lui suggérer d’autres choix susceptibles de l’intéresser.

**Sites web de recherche**

* La plupart des grands moteurs de recherche sont des outils analytiques très puissants qui enregistrent le comportement des utilisateurs, les termes qu’ils saisissent et les sites web qu’ils visitent. Il est ensuite utilisé pour personnaliser le contenu fourni, notamment en ce qui concerne l&#39;affichage des publicités.

### Avantages liés à la personnalisation et aspects à prendre en considération {#strengths-of-personalization-and-points-to-consider}

Voici les raisons pour lesquelles la personnalisation doit être utilisée :

* L’utilisateur bénéficie d’un site web convivial et adapté à ses besoins.
* La personnalisation peut être utilisée pour propager automatiquement l’accès à la dernière version du contenu.
* Des fonctions de collaboration sociale permettent aux utilisateurs de communiquer entre eux, car ils peuvent être identifiés par leur profil.
* L’utilisateur reçoit le contenu dont il a besoin pour accomplir une tâche spécifique. Sur le réseau intranet de l’entreprise, la personnalisation peut constituer un outil inestimable pour diffuser des informations.
* L’utilisateur reçoit le contenu dont il a besoin ou qu’il souhaite consulter, ce qui réduit le temps passé à effectuer des recherches.
* Le fournisseur de contenu peut orienter le contenu de sorte qu’il soit vu par certaines catégories d’utilisateurs.
* Des règles peuvent être définies pour fournir le contenu en fonction de combinaisons associant à la fois les caractéristiques et le comportement de l’utilisateur. Ceci constitue un mécanisme élaboré permettant de personnaliser l’expérience web de l’utilisateur.

Lors de l’utilisation de la personnalisation, tenez compte des points suivants :

**Performances**

* Naturellement, toute analyse et toute évaluation supplémentaires peuvent avoir un impact sur les performances. Toutefois, les méthodes utilisées sont très sophistiquées et peuvent être optimisées pour minimiser cet impact.

**Autorisation**

* La personnalisation requiert un mécanisme de connexion, car le site web doit pouvoir identifier l’utilisateur.

**Mise en cache**

* La mise en cache est un aspect que l’utilisateur verra en termes de performances et de précision : à quelle vitesse le site Web diffuse-t-il du contenu personnalisé et est-il toujours à jour ?
* La mise en cache est une considération clé dans la configuration de la personnalisation, et du temps doit être consacré pour garantir que l’implémentation utilisée est adaptée. Cet aspect est décrit en détail plus loin.

**Précision des règles**

* La personnalisation qui se base sur la surveillance du comportement de l’utilisateur ou la définition de règles basées sur le profil de l’utilisateur doit être précise et logique.
* Il n’y a rien de plus frustrant pour un utilisateur que de se voir imposer ou refuser un contenu en raison de la logique inexacte d’une règle.
* Par conséquent, les règles doivent être bien pensées, les exigences de l&#39;utilisateur étant au premier plan. Cette étape peut nécessiter beaucoup d’efforts et ne doit pas être sous-estimée. En effet, la création des règles est souvent plus exigeante que l’effort technique nécessaire à la mise en œuvre de la personnalisation.

**Quand utiliser la personnalisation**

* Comme un grand nombre de fonctionnalités sur le web, la personnalisation doit être utilisée avec prudence. Son utilisation bénéficiera-t-elle vraiment à l’utilisateur ? Cette question doit toujours être la première question posée. Mais on peut aussi se demander si l’objectif recherché peut être atteint à moindre effort par une autre méthode. La personnalisation risque d’être une fonction que les utilisateurs configurent une fois (pour voir comment elle fonctionne) et une seule fois, car elle ne leur apporte aucun avantage réel.
* La personnalisation n’a de sens que lorsque le contenu est dynamique, en fonction de l’utilisateur d’une certaine manière. Si tous les utilisateurs voient le même contenu, la personnalisation est redondante.

**Confidentialité**

* De nombreux utilisateurs sont soucieux de la protection et de la sécurité des données, en particulier en ce qui concerne les données collectées en surveillant leur comportement sur le web.

## Personnalisation et accès {#personalization-and-access}

Même si ces deux aspects sont liés, la personnalisation et le contrôle d’accès doivent chacun être pris en compte de manière distincte.

La personnalisation ne crée en elle-même aucune forme de contrôle d’accès. Elle constitue tout simplement un moyen d’orienter le contenu que l’utilisateur voit. Elle n’empêche pas l’utilisateur d’accéder à un autre contenu et, comme pour n’importe quel contenu, les contrôles d’accès appropriés doivent déjà avoir été affectés à l’utilisateur.

Toutefois, le contrôle d’accès peut être utilisé pour créer une forme de personnalisation. Si vous autorisez ou refusez à un utilisateur l’accès à un contenu, ceci affecte inévitablement le choix de contenu dont cet utilisateur dispose, et donc la personnalisation de son expérience web.

## Composants disponibles pour la personnalisation {#components-available-for-personalization}

Divers composants sont fournis avec AEM en vue de la personnalisation. Certains de ces composants permettent aux utilisateurs de se connecter et de modifier leur profil, tandis que d’autres (par exemple, Mes gadgets) leur permettent de configurer une page spécifique :

| Titre dans le Sidekick | Objectif |
|---|---|
| Champ du mot de passe coché | Demande le mot de passe et la confirmation de celui-ci. |
| Inscription combinée | Permet à l’utilisateur de se connecter à un compte existant ou de s’inscrire à un nouveau compte. |
| Champ d’adresse Forms | Un champ complexe permettant la saisie d’une adresse internationale. |
| Début de Forms | Début d’une définition de formulaire |
| Forms Captcha | Un champ consistant en un mot alphanumérique actualisé automatiquement. Le composant Captcha protège les sites Web contre les virus. |
| Groupe de cases à cocher Forms | Plusieurs éléments organisés en une liste et précédés par des cases à cocher. Les utilisateurs peuvent sélectionner plusieurs cases à cocher. |
| Liste déroulante Forms | Plusieurs éléments organisés en une liste déroulante. Le commutateur Plusieurs sélections possibles spécifie si plusieurs éléments peuvent être sélectionnés depuis la liste. |
| Fin de Forms | Termine la définition du formulaire. |
| Transfert de fichier Forms | Un élément de téléchargement qui permet à l’utilisateur de télécharger un fichier sur le serveur. |
| Champ masqué Forms | Ce champ ne s’affiche pas pour l’utilisateur. Il peut être utilisé pour le transport d’une valeur au client et de retour au serveur. Ce champ ne devrait avoir aucune contrainte. |
| Bouton Forms Image | Un bouton d’envoi supplémentaire pour le formulaire qui est rendu en une image. |
| Champ Mot de passe Forms | Similaire au champ de texte mais seule une ligne est autorisée et la saisie de texte par l’utilisateur n’est pas visible dans le champ. |
| Groupe radio Forms | Plusieurs éléments organisés en une liste et précédés par des cases d’option. Les utilisateurs ne doivent sélectionner qu’une seule case d’option. |
| Bouton Envoyer Forms | Un bouton d’envoi supplémentaire pour le formulaire avec le titre affiché comme texte sur le bouton. |
| Champ de texte Forms | Champ de texte qui permet aux utilisateurs de saisir des informations. |
| My Gadgets | Vous permet d&#39;inclure l&#39;un des gadgets disponibles. |
| Photo de l’avatar du profil | Permet la saisie d’une photo Avatar. |
| Nom détaillé du profil | Entrée des détails du nom, y compris les éléments tels que le titre, le deuxième prénom et le suffixe le cas échéant. |
| Nom d&#39;affichage du profil | Nom à afficher. |
| Courrier électronique du profil | Saisie d’une adresse de courrier électronique. |
| Sexe du profil | Permet la saisie du sexe. |
| Principal numéro de téléphone du profil | Permet la saisie d’un numéro de téléphone. |
| Principale URL du profil | Permet la saisie d’une URL. |
| Profil Texte général, propriété | Propriétés du profil. |
| Connexion | Permet d’envoyer un nom d’utilisateur et un mot de passe lors de la connexion. |
| Se déconnecter | Indique l’utilisateur actuellement connecté et fournit un lien permettant de se déconnecter. |
| Nuage de tags | Cloud de balises pour afficher une sélection de balises présentée sous forme graphique dans votre site Web |
| Teaser | Elément de contenu (généralement une image) affiché sur une page principale pour &quot;inciter&quot; les utilisateurs à accéder au contenu sous-jacent. |

## Personnalisation et contenu de la communauté {#personalization-and-community-content}

Les fonctions de communauté telles que les blogs, les forums et les calendriers entraînent la création de contenu de communauté, généralement appelé contenu créé par l’utilisateur. Lorsque du contenu créé par l’utilisateur est entré dans un environnement de publication consistant en plusieurs instances AEM ([ferme de publication](/help/communities/topologies.md)), un problème majeur est de trouver un moyen de synchroniser ce contenu sur toutes les instances.

With [AEM Communities 6.1](/help/communities/overview.md) extension, this issue is solved by using a [common store for UGC](/help/communities/working-with-srp.md). In regards, to personalization, Communities includes [Social Login](/help/communities/social-login.md) - the ability to provide the option for site visitors to sign in with Facebook and Twitter.

Sans l’extension Communities, les différentes méthodes à examiner pour résoudre le problème lié à l’homogénéité du contenu créé par l’utilisateur sont les suivantes :

* Synchroniser les instances de publication multiples si nécessaire
* Envoyer le contenu créé par l’utilisateur de l’instance de publication à l’environnement de création, à partir duquel il peut être publié de façon similaire à la publication du contenu des pages

La méthode utilisée pour obtenir l’homogénéité du contenu créé par l’utilisateur dans tout l’environnement de publication consistant en plusieurs instances de publication doit être soigneusement conçue et testée en termes de performances et d’homogénéité.
