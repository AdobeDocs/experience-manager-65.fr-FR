---
title: Console Sites Communities
description: Découvrez comment accéder à la console Sites des communautés pour la création, la modification et la gestion de sites.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3084'
ht-degree: 1%

---

# Console Sites Communities {#communities-sites-console}

La console Sites de Communities permet d’accéder aux éléments suivants :

* Création de site
* Modification du site
* Gestion de site
* [Création et modification de groupes imbriqués](/help/communities/groups.md) (sous-communautés)

Reportez-vous à la section [Prise en main d’AEM Communities](/help/communities/getting-started.md) où vous pouvez découvrir à quelle vitesse un site communautaire peut être créé dans l’environnement de création et comment créer des groupes communautaires à partir des environnements de création et de publication.

>[!NOTE]
>
>Les principaux menus de Communities pour la création de [ sites communautaires](/help/communities/sites-console.md), de [ modèles de site communautaire](/help/communities/sites.md), de [ modèles de groupe de communautés ](/help/communities/tools-groups.md) et de [fonctions communautaires](/help/communities/functions.md) sont destinés uniquement à l’environnement de création.

## Conditions préalables {#prerequisites}

Avant de créer un site communautaire, il est *requis* pour :

* Vérifiez qu’une ou plusieurs instances Publish sont en cours d’exécution.
* Activez le [service tunnel](/help/communities/deploy-communities.md#tunnel-service-on-author) pour gérer les membres et les groupes de membres.
* Identifiez l’ [éditeur principal](/help/communities/deploy-communities.md#primary-publisher).
* [Configurez la réplication](/help/communities/deploy-communities.md#replication-agents-on-author) lorsque le port principal de l’éditeur n’est pas le port par défaut (4503).

Pour vous assurer que le site est prêt à prendre en charge de nombreuses fonctionnalités, la bonne pratique consiste à procéder comme suit :

* Installez le [dernier Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack).
* Activez [Adobe Analytics](/help/communities/analytics.md) pour AEM Communities.
* Configurer [email](/help/communities/email.md)
* Identifiez les [administrateurs de la communauté](/help/communities/users.md#creating-community-members).
* [Activez le gestionnaire OAuth](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) pour la connexion sociale.

## Accès à la console Sites des communautés {#accessing-communities-sites-console}

Dans l’environnement de création, pour accéder à la console Sites des communautés :

* À partir de la navigation globale : **[!UICONTROL Communities]** > **[!UICONTROL Sites]**

La console Sites de communautés affiche tous les sites de communautés existants. Dans cette console, les sites de communauté peuvent être créés, modifiés, gérés et supprimés.

Pour créer un site communautaire, sélectionnez l’icône **Créer** .

Pour accéder à un site communautaire existant en vue de créer, modifier, publier, exporter ou ajouter un groupe imbriqué, sélectionnez l’icône de dossier du site.

## Création du site {#site-creation}

La console de création de site fournit une approche détaillée pour assembler les fonctionnalités du site en fonction d’un [modèle de site communautaire](/help/communities/sites.md) et de paramètres sélectionnés.

Chaque site créé comprend une fonction de connexion, car les visiteurs du site doivent se connecter avant de pouvoir publier du contenu, envoyer des messages ou participer à un groupe. Les autres fonctionnalités incluent les profils utilisateur, la messagerie, les notifications, le menu du site, la recherche, le thème et la valorisation de marque.

Le processus est lancé en sélectionnant le bouton `Create` en haut de la console Sites des communautés .

Le processus de création est une série d’étapes présentées sous la forme de panneaux contenant un ensemble de fonctionnalités à configurer (présentées sous la forme de sous-panneaux). Il est possible de passer à l’étape **Suivant** ou **Précédent** à l’étape précédente avant de valider le site à l’étape finale.

### Étape 1 : modèle de site {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

Dans le panneau Modèle de site, le titre, la description, la racine du site, la langue de base, le nom et le modèle de site sont spécifiés :

* **Titre du site de la communauté**

  Titre affiché du site.

  Le titre apparaît sur le site publié et dans l’interface utilisateur d’administration du site.

* **Description du site de la communauté**

  Description du site.

  La description n’apparaît pas sur le site publié.

* **Racine du site de la communauté**

  Chemin d’accès racine au site.

  La racine par défaut est `/content/sites`, mais elle peut être déplacée à n’importe quel emplacement du site web.

* **Langue de base du site de la communauté**

  (Laissez intacte pour une seule langue : anglais) Utilisez le menu déroulant pour choisir une ou plusieurs langues de base *ou plus* parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site de communauté est créé pour chaque langue ajoutée et existe dans le même dossier de site, conformément aux bonnes pratiques décrites dans la section [Traduction de contenu pour des sites multilingues](/help/sites-administering/translation.md). La page racine de chaque site contient une page enfant nommée par le code de langue de l’une des langues sélectionnées, comme &quot;en&quot; pour l’anglais ou &quot;fr&quot; pour le français.

* **Nom de site de la communauté** :

  Nom de la page racine du site qui apparaît dans l’URL.

   * Vérifiez deux fois le nom, car il n’est pas facilement modifié une fois le site créé.
   * L’URL de base ( `https://server:port/site root/site name)`) s’affiche sous le `Community Site Name`.

   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;

     *Par exemple*, `https://localhost:4502/content/sites/mysight/en.html`

* Menu **Modèle de site communautaire**

  Utilisez le menu déroulant pour choisir un [ modèle de site communautaire](/help/communities/tools.md) disponible.

* Sélectionnez **Suivant**.

### Etape 2 : Conception {#step-design}

Le panneau Conception contient deux sous-panneaux pour sélectionner le thème et la bannière de marque :

#### THÈME DU SITE COMMUNAUTAIRE {#community-site-theme}

![sitetheme](assets/sitetheme.png)

La structure utilise `Twitter Bootstrap` pour apporter une conception réactive et flexible au site. Un des nombreux thèmes de Bootstrap préchargés peut être sélectionné pour mettre en forme le modèle de site de communauté sélectionné ou un thème de Bootstrap peut être chargé.

Lorsqu’il est sélectionné, le thème est recouvert d’une coche bleue opaque.

Une fois le site de la communauté publié, il est possible de [modifier les propriétés](#modifying-site-properties) et sélectionner un autre thème.

#### MARQUE DU SITE DE LA COMMUNAUTÉ {#community-site-branding}

![site-branding](assets/site-branding.png)

La valorisation de marque du site de la communauté est une image affichée en tant qu’en-tête dans la partie supérieure de chaque page.

L’image doit être dimensionnée de manière à être aussi large que l’affichage prévu de la page dans le navigateur et de 120 pixels de hauteur.

Lors de la création ou de la sélection d’une image, gardez à l’esprit les points suivants :

* La hauteur de l’image est recadrée à 120 pixels mesurés à partir du bord supérieur de l’image.
* L’image est épinglée sur le bord gauche de la fenêtre du navigateur.
* L’image n’est pas redimensionnée, de sorte que lorsque la largeur de l’image est...

   * Moins que la largeur du navigateur, l’image se répète horizontalement.
   * Plus grande que la largeur du navigateur, l’image semble recadrée.

* Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

Le panneau Paramètres contient plusieurs sous-panneaux présentant les fonctionnalités à configurer avant de passer à la dernière étape pour créer le site.

* [GESTION DES UTILISATEURS](#user-management)
* [BALISAGE](#tagging)
* [RÔLES](#roles)
* [MODÉRATION](#moderation)
* [ANALYTICS](#analytics)
* [TRADUCTION](#translation)

>[!NOTE]
>
>**Activer le service de tunnel**
>
>Plusieurs sous-panneaux Paramètres permettent à un membre de confiance d’être affecté pour modérer le contenu créé par l’utilisateur, gérer des groupes ou être un contact pour les ressources d’activation dans l’environnement de publication.
>
>La convention est que les [utilisateurs et groupes d’utilisateurs](/help/communities/users.md) côté publication (membres et groupes de membres) ne soient pas dupliqués dans l’environnement de création.
>
>Ainsi, lors de la création du site de la communauté dans l’environnement de création et de l’affectation de membres approuvés à différents rôles, il est nécessaire de récupérer les données de membres de l’environnement de publication.
>
>Pour ce faire, activez l’ ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` pour l’environnement de création.

#### GESTION DES UTILISATEURS {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **Autoriser l’enregistrement des utilisateurs**

  Si cette case est cochée, les visiteurs du site peuvent devenir membres de la communauté en s’inscrivant automatiquement.
Si cette option n’est pas cochée, le site de la communauté est *limité* et les visiteurs du site doivent être affectés au groupe des membres du site de la communauté, faire une demande ou recevoir une invitation par courrier électronique. Si cette option n’est pas cochée, l’accès anonyme ne doit pas être autorisé.
Dérecherchez un site communautaire *private* . La valeur par défaut est cochée.

* **Autoriser l’accès anonyme**

  Si cette case est cochée, le site de la communauté est *ouvert* et tout visiteur du site peut y accéder.
Si cette option n’est pas cochée, seuls les membres connectés peuvent accéder au site.
Dérecherchez un site communautaire *private* . La valeur par défaut est cochée.

* **Autoriser la messagerie**

  Si cette case est cochée, les membres peuvent envoyer des messages les uns aux autres et au groupe sur le site de la communauté.
Si cette option n’est pas cochée, la messagerie n’est pas configurée pour la communauté.
La case par défaut est décochée.

* **Autoriser les connexions au réseau social : Facebook**

  Si cette case est cochée, les visiteurs du site peuvent se connecter à l’aide des informations d’identification de leur compte Facebook. La [configuration cloud Facebook](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) sélectionnée doit être configurée pour ajouter des utilisateurs au groupe de membres du site de la communauté une fois le site de la communauté créé.
Si cette option n’est pas cochée, aucune connexion Facebook n’est présentée.
Ne cochez pas la case pour un site communautaire *private* . La case par défaut est décochée.

* **Autoriser les connexions au réseau social : Twitter**

  Si cette case est cochée, les visiteurs du site peuvent se connecter à l’aide des informations d’identification de leur compte de Twitter. La [configuration de cloud de Twitter](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) sélectionnée doit être configurée pour ajouter des utilisateurs au groupe de membres du site de la communauté une fois le site de la communauté créé.
Si cette option n’est pas cochée, aucun identifiant de Twitter n’est présenté.
Ne cochez pas la case pour un site communautaire *private* . La case par défaut est décochée.

>[!NOTE]
>
>**Autorisation des connexions au réseau social**
>
>Bien que des exemples de configurations Facebook et Twitter puissent exister et être sélectionnables pour un [environnement de production](/help/sites-administering/production-ready.md), il est nécessaire de créer des applications Facebook et Twitter personnalisées. Voir [Connexion sociale avec Facebook et Twitter](/help/communities/social-login.md).

#### BALISAGE {#tagging}

![site-tagging](assets/site-tagging.png)

Les balises (qui peuvent être appliquées au contenu de la communauté) sont contrôlées en sélectionnant Espaces de noms de balise précédemment définis via la [console de balisage](/help/sites-administering/tags.md#tagging-console).

En outre, la sélection des espaces de noms de balise pour le site de la communauté limite la sélection présentée lors de la définition des catalogues et des ressources.

* Zone de recherche de texte : commencez à saisir le texte pour identifier les balises autorisées à être utilisées sur le site.

#### RÔLES {#roles}

![Rôles de la communauté](assets/site-admin-2.png)

Les [rôles des membres de la communauté](/help/communities/users.md) sont attribués avec ces paramètres.

Il est facile de trouver des membres de la communauté à l’aide d’une recherche anticipée.

* **Chefs de communauté**

  Commencez à taper pour sélectionner un ou plusieurs membres de la communauté ou groupes de membres pouvant gérer les membres de la communauté et les groupes de membres.

* **Modérateurs de la communauté**

  Commencez à saisir le texte pour sélectionner un ou plusieurs membres de la communauté ou groupes de membres à approuver en tant que modérateurs du contenu généré par l’utilisateur.

* **Membres privilégiés de la communauté**

  Commencez à taper pour sélectionner un ou plusieurs membres de la communauté ou groupes de membres auxquels la possibilité de créer du contenu lorsque `Allow Privileged Member` a été sélectionné pour une [fonction de la communauté](/help/communities/functions.md).

* **Admins de la communauté**

  Commencez à saisir pour sélectionner un ou plusieurs administrateurs du site qui peuvent gérer la structure du site indépendamment des autres administrateurs du site et de l’administrateur de la communauté par défaut. Ils peuvent créer des groupes à n’importe quel niveau de la hiérarchie et devenir l’administrateur par défaut des groupes imbriqués (mais ils peuvent ensuite être supprimés du rôle d’administrateur des groupes imbriqués).

#### MODÉRATION {#moderation}

![site-modération](assets/site-moderation.png)

Le paramètre global de modération du contenu généré par l’utilisateur est contrôlé par ces paramètres. Les composants individuels disposent de paramètres supplémentaires pour contrôler la modération.

* **Le contenu est prémodéré**

  Si cette case est cochée, le contenu de la communauté publié n’apparaît pas tant qu’il n’a pas été approuvé par un modérateur. La case par défaut est décochée. Pour plus d’informations, voir [Modération de contenu de la communauté](/help/communities/moderate-ugc.md#premoderation).

* **Seuil de marquage avant le masquage du contenu**

  Si la valeur est supérieure à 0, le nombre de fois où une rubrique ou une publication doit être marquée avant d’être masquée dans la vue publique. S’il est défini sur -1, le sujet ou la publication marqué n’est jamais masqué à la vue du public. La valeur par défaut est 5.

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **Activer Analytics**

  Disponible uniquement lorsque Adobe Analytics a été [configuré](/help/communities/analytics.md) pour les fonctionnalités de Communities.
La case par défaut est décochée. Lorsque cette case est cochée, un menu de sélection supplémentaire s’affiche :

![site-analytics-enable](assets/site-analytics-enable.png)

* **Référence du framework de configuration cloud**

  Dans le menu déroulant, sélectionnez la structure de service Analytics Cloud configurée pour ce site de la communauté.
  `Communities` est l’exemple de structure de la documentation [Configuration d’Analytics pour les fonctionnalités des communautés](/help/communities/analytics.md#aem-analytics-framework-configuration).

#### TRADUCTION {#translation}

![site-translation](assets/site-translation.png)

* **Autoriser la traduction automatique**

  Lorsque cette option est cochée (la valeur par défaut est décochée), la traduction automatique est activée pour le contenu généré par l’utilisateur dans le site. Cela n’affecte aucun autre contenu, tel que le contenu de la page, même si le site est configuré en tant que site multilingue. Pour plus d’informations sur la configuration d’un service de traduction sous licence pour AEM Communities, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md) . Voir [Traduction de contenu pour des sites multilingues](/help/sites-administering/translation.md) pour une présentation complète.

![allow-machine-translation](assets/allow-machine-translation.png)

* **Activer la traduction automatique pour les langues sélectionnées**

  Les langues activées pour la traduction automatique sont par défaut définies par le paramètre système [configuration de l’intégration de traduction](/help/communities/translate-ugc.md#translation-integration-configuration). Ces paramètres par défaut peuvent être remplacés pour ce site en supprimant les paramètres par défaut et/ou en sélectionnant d’autres langues dans le menu déroulant.

* **Choisir un fournisseur de traduction**

  Par défaut, le fournisseur de services est un service d’évaluation utilisant `microsoft` pour la démonstration uniquement. Si aucun fournisseur de services de traduction n’est autorisé, la case **Autoriser la traduction automatique** doit être décochée.

* **Choisir un magasin partagé global**

  Pour un site web comportant plusieurs copies de langue, un magasin partagé global fournit un fil de conversation unique, visible à partir de chaque copie de langue. Pour ce faire, sélectionnez l’une des langues incluses comme copie de langue. La valeur par défaut est *No Global Shared Store*.

* **Choisir la configuration du fournisseur de traduction**

  Sélectionnez une [structure d’intégration de traduction](/help/sites-administering/tc-tic.md) créée pour le fournisseur de traduction sous licence.

* **Sélectionnez les options de traduction du site de votre communauté**

   * **Traduire toute la page**

     Si cette option est sélectionnée, tout le contenu généré par l’utilisateur d’une page est traduit dans la langue de base de la page.

     La valeur par défaut est *non sélectionné*.

   * **Traduire la sélection uniquement**

     Si cette option est sélectionnée, une option de traduction s’affiche en regard de chaque publication, ce qui permet de traduire des publications individuelles dans la langue de base de la page.
La valeur par défaut est *selected*.

* **Sélectionner les options de persistance**

   * **Traduire les contributions sur demande de l’utilisateur et persister par la suite**
Si cette option est sélectionnée, le contenu n’est pas traduit tant qu’une requête n’a pas été effectuée. Une fois traduite, la traduction est stockée dans le référentiel.

     La valeur par défaut est *non sélectionné*.

   * **Ne pas conserver les traductions**

     Si cette option est sélectionnée, les traductions ne sont pas stockées dans le référentiel.

     Si cette option n’est pas sélectionnée, les traductions sont conservées.

     La valeur par défaut est *non sélectionné*.

* **Smart Render**

  Sélectionnez l’une des options suivantes :

   * `Always show contributions in the original language` (par défaut)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### Étape 4 : Création d’un site de communautés {#step-create-communities-site}

Si des ajustements sont nécessaires, utilisez le bouton **Précédent** pour les effectuer.

Une fois **Créer** sélectionné et démarré, le processus de création du site ne peut pas être interrompu.

Une fois le site créé :

* La modification de l’URL (nom du noeud) n’est pas prise en charge.
* Les futures modifications apportées au modèle de site communautaire n’ont aucune incidence sur le site communautaire créé.
* La désactivation du modèle de site de communauté n’a aucune incidence sur le site de communauté créé.
* Il est possible de modifier la [STRUCTURE](#modify-structure) d’un site communautaire en modifiant ses propriétés.

![create-site](assets/create-site1.png)

Une fois le processus terminé, le dossier du nouveau site s’affiche dans la console Sites des communautés , à partir de laquelle les auteurs peuvent ajouter du contenu de page, ou les administrateurs peuvent modifier les propriétés du site.

![modify-site-property](assets/modify-site-property.png)

Pour modifier un site de communauté, sélectionnez son dossier de projet pour l’ouvrir :

![site-project](assets/site-project.png)

Lorsque vous placez le pointeur de la souris sur un site ou que vous touchez une carte de site, des icônes s’affichent pour vous permettre ce qui suit :

* [modification du site en mode création](#authoring-site-content)
* [ouverture des propriétés du site pour modification](#modifying-site-properties)
* [publication du site](#publishing-the-site)
* [exporter le site](#exporting-the-site)
* [suppression du site](#deleting-the-site)

## Création de contenu du site {#authoring-site-content}

Le contenu d’un site peut être créé avec les mêmes outils que tout autre site web AEM. Pour ouvrir le site à des fins de création, sélectionnez l’icône `Open Site` qui s’affiche lorsque vous pointez dessus avec la souris. Le site s’ouvre dans un nouvel onglet, de sorte que la console Sites des communautés reste accessible.

![site-content](assets/site-content.png)

>[!NOTE]
>
>Si vous ne connaissez pas AEM, consultez la documentation sur la [gestion de base](/help/sites-authoring/basic-handling.md) et un [ guide rapide sur la création de pages](/help/sites-authoring/qg-page-authoring.md).

## Modification des propriétés du site {#modifying-site-properties}

![edit-site](assets/edit-site.png)

Les propriétés d’un site existant, spécifiées pendant le processus de création du site, peuvent être modifiées en sélectionnant l’icône `Edit Site` qui s’affiche lorsque vous pointez sur le site avec la souris.

`Details of the following properties match the descriptions provided in the` [Création de site](#site-creation) .

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### Modification de base {#modify-basic}

Le panneau BASIC permet de modifier les éléments suivants :

* Titre du site de la communauté
* Description du site de la communauté

Le nom du site de la communauté ne peut pas être modifié.

Le choix d’un modèle de site de communauté différent n’aurait aucun effet sur un site de communauté existant, car il n’existe aucune connexion entre les modèles et les sites.

Au lieu de cela, la [STRUCTURE](#modify-structure) du site de la communauté peut être modifiée.

### Modifier la structure {#modify-structure}

Le panneau STRUCTURE permet de modifier la structure initialement créée à partir du modèle de site de communauté sélectionné. Dans le panneau , vous pouvez effectuer les opérations suivantes :

* Faites glisser des [fonctions communautaires](/help/communities/functions.md) supplémentaires dans la structure du site.
* Sur une instance d’une fonction de communauté dans la structure du site :

   * **`gear icon`**

     Modifiez les paramètres, y compris le titre d’affichage et le nom de l’URL, et [groupes de membres privilégiés](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

     Supprimer (supprimer) des fonctions de la structure du site.

   * **`grid icon`**

     Modifiez l’ordre des fonctions tel qu’affiché dans la barre de navigation supérieure du site.

>[!NOTE]
>
>Vous pouvez modifier l’ordre de toutes les fonctions de la structure du site, à l’exception de la fonction située en haut. Par conséquent, la page d’accueil d’un site communautaire ne peut pas être modifiée.

>[!CAUTION]
>
>* Bien que le titre d’affichage puisse être modifié sans effets secondaires, il n’est pas recommandé de modifier le nom d’URL d’une fonction de communauté appartenant à un site de communauté.
>
>Par exemple, renommer l’URL ne déplace pas le contenu créé par l’utilisateur existant, ce qui entraîne la &quot;perte&quot; du contenu créé par l’utilisateur.

>[!CAUTION]
>
>La fonction groups doit *ne pas* être la *première fonction et la seule* de la structure du site.
>
>Toute autre fonction, telle que la [fonction de page](/help/communities/functions.md#page-function), doit être incluse et répertoriées en premier.

#### Exemple : ajout d’une fonction de catalogue à une structure de site de communauté {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### Modifier la conception {#modify-design}

Le panneau CONCEPTION permet d’appliquer un nouveau thème :

* [Thème des sites de la communauté](#community-site-theme)
* [Valorisation de marque des sites de la communauté](#community-site-branding)

   * Faites défiler l’écran jusqu’au bas du panneau pour pouvoir modifier l’image de marque.

### Modifier les paramètres {#modify-settings}

Le panneau PARAMÈTRES permet d’accéder à la plupart des paramètres sous les sous-panneaux de l’ Étape 3 de la création d’un site de communauté :

* [Gestion des utilisateurs et utilisatrices](#user-management)
* [Balises](#tagging)
* [Modération](#moderation)
* [Rôles des membres](#roles)
* [Analytics](#analytics)
* [Traduction](#translation)

### Modifier la miniature {#modify-thumbnail}

Le panneau MINIATURE permet de charger une image représentant le site dans la console Sites des communautés .

## Publication du site {#publishing-the-site}

Une fois qu’un site communautaire a été créé ou modifié, il est possible de le publier (d’activer) en sélectionnant l’icône `Publish Site` qui s’affiche lorsque vous pointez sur le site.

![publish-site](assets/publish-site.png)

Une indication s’affiche une fois le site publié.

![site-publish](assets/site-published.png)

### Publication avec des groupes imbriqués {#publishing-with-nested-groups}

Après la publication d’un site de communauté, il est nécessaire de publier individuellement chaque sous-communauté (groupe imbriqué) créée à l’aide de la [console Groupes](/help/communities/groups.md).

## Exportation du site {#exporting-the-site}

![export-site](assets/export-site.png)

Sélectionnez l’icône d’exportation, survolez le site avec la souris, de sorte que vous puissiez créer un module du site de la communauté qui est à la fois stocké dans le [Gestionnaire de modules](/help/sites-administering/package-manager.md) et téléchargé.

Le contenu généré par l’utilisateur n’est pas inclus dans le module du site.

## Suppression du site {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

Pour supprimer le site de la communauté, sélectionnez l’icône Supprimer le site qui s’affiche lorsque vous placez le pointeur de la souris sur le site dans la console du site Communities. Cette action supprime tous les éléments associés au site, tels que le contenu créé par l’utilisateur, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

## Groupes d’utilisateurs de la communauté créés {#created-community-user-groups}

Une fois le nouveau site de la communauté publié, les nouveaux groupes de membres (groupes d’utilisateurs créés dans l’environnement de publication) disposent des autorisations appropriées pour différents rôles d’administrateur et de membre.

Le nom créé pour les groupes de membres inclut le *nom-site* donné à l’ [étape 1](#step13asitetemplate) (nom qui apparaît dans l’URL). Il comprend également un identifiant unique afin d’éviter les conflits avec les sites et les groupes de communautés ayant le même nom de site pour différentes racines de site de communauté.

Par exemple, si le nom était &quot;engagement&quot; pour un site intitulé &quot;Tutoriel de prise en main&quot;, le groupe d’utilisateurs pour les modérateurs serait :

* titre : Modérateurs d’interactions communautaires
* nom : community-*engage-uid*-modérateurs

Tous les membres affectés comme modérateurs ou administrateurs de groupe lors de la création du site sont affectés au groupe approprié et affectés au groupe de membres. Ces groupes et affectations de membres sont créés lors de la publication lorsque le nouveau site est publié.

Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

>[!NOTE]
>
>Si [Autoriser la connexion au réseau social : Facebook](#user-management) est activé, une fois le groupe d’utilisateurs `community-<site-name>-<uid>-members`
>est créé, le [service cloud Facebook](/help/communities/social-login.md#createafacebookcloudservice) appliqué doit être configuré pour ajouter des utilisateurs à ce groupe.

## Configuration d’une erreur d’authentification {#configure-for-authentication-error}

Par défaut, un site de communauté redirige vers un exemple de page de connexion lorsque l’utilisateur saisit des informations d’identification erronées et ne parvient pas à se connecter. Cet exemple de connexion n&#39;est pas présent sur un [serveur de production](/help/sites-administering/production-ready.md).

Pour rediriger correctement, une fois qu’un site a été configuré et envoyé pour publication, procédez comme suit pour obtenir l’échec d’authentification à rediriger vers le site de la communauté :

* Sur chaque instance de publication AEM.
* Connectez-vous avec les privilèges d’administrateur.
* Accédez à la [console web](/help/sites-deploying/configuring-osgi.md).

   * Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* Recherchez `Adobe Granite Login Selector Authentication Handler`.
* Sélectionnez l’icône `pencil` pour ouvrir la configuration à modifier.
* Saisissez un **mappage de page de connexion** comme suit :

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  Par exemple :
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* Sélectionnez **Enregistrer**.

![auth-error](assets/auth-error.png)

### Tester la redirection de l’authentification {#test-authentication-redirection}

Sur la même instance de publication AEM configurée avec un mappage de page de connexion pour le site de la communauté :

* Accédez à la page d’accueil du site de la communauté.

   * Par exemple, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* Sélectionnez Déconnexion.
* Sélectionnez Connexion.
* Saisissez des informations d’identification incorrectes, telles que le nom d’utilisateur &quot;x&quot; et le mot de passe &quot;x&quot;.
* La page de connexion doit s’afficher avec une erreur &quot;login non valide&quot;.

![test-authentication](assets/test-authentication.png)

## Accès aux sites de la communauté à partir de la console Sites principale {#accessing-community-sites-from-main-sites-console}

Dans la console Sites de navigation globale, les sites de la communauté se trouvent dans le dossier `Community Sites` .

Bien qu’il soit possible d’accéder à un site communautaire de cette manière, pour les tâches administratives, le site de la communauté doit être accessible à partir de la console Sites des communautés .

![access-site](assets/access-site.png)
