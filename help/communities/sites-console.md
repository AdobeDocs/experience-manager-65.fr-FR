---
title: Console Sites de communautés
seo-title: Console Sites de communautés
description: Comment accéder à la console Sites des communautés
seo-description: Comment accéder à la console Sites des communautés
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3293'
ht-degree: 4%

---


# Console Sites des communautés {#communities-sites-console}

La console Sites des communautés permet d&#39;accéder à :

* Création du site
* Modification du site
* Gestion du site
* [Création et modification de groupes](/help/communities/groups.md)  imbriqués (sous-communautés)

Voir [Prise en main de AEM Communities](/help/communities/getting-started.md) pour savoir à quelle vitesse un site communautaire peut être créé dans l’environnement d’auteur, ainsi que comment créer des groupes communautaires à partir des environnements d’auteur et de publication.

>[!NOTE]
>
>Les principaux menus Collectivités pour la création de [sites communautaires](/help/communities/sites-console.md), [modèles de sites communautaires](/help/communities/sites.md), [modèles de groupes communautaires](/help/communities/tools-groups.md) et [fonctions communautaires](/help/communities/functions.md) ne sont utilisés que dans l&#39;environnement auteur.

## Conditions préalables {#prerequisites}

Avant de créer un site communautaire, il est *nécessaire* de :

* Vérifiez qu’une ou plusieurs instances de publication sont en cours d’exécution.
* Activez le [service tunnel](/help/communities/deploy-communities.md#tunnel-service-on-author) pour gérer les membres et les groupes de membres.
* Identifiez l&#39;éditeur [Principal](/help/communities/deploy-communities.md#primary-publisher).
* [Configurez la ](/help/communities/deploy-communities.md#replication-agents-on-author) réplication lorsque le port d’éditeur Principal n’est pas le port par défaut (4503).

Pour s&#39;assurer que le site est prêt à prendre en charge de nombreuses fonctionnalités, il est recommandé de suivre les étapes suivantes :

* Installez le [dernier Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack).
* Activez [Adobe Analytics](/help/communities/analytics.md) pour AEM Communities.
* Configurer [courriel](/help/communities/email.md)
* Identifiez [les administrateurs de la communauté](/help/communities/users.md#creating-community-members).
* [Activez le gestionnaire OAuth ](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) pour la connexion sociale.

## Accès à la console Sites des communautés {#accessing-communities-sites-console}

Dans l’environnement de l’auteur, pour accéder à la console Sites des communautés :

* A partir de la navigation globale : **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**

La console Sites des communautés affiche tous les sites communautaires existants. A partir de cette console, les sites communautaires peuvent être créés, modifiés, gérés et supprimés.

Pour créer un site de communauté, sélectionnez l&#39;icône **Créer**.

Pour accéder à un site communautaire existant, afin de créer, modifier, publier, exporter ou ajouter un groupe imbriqué, sélectionnez l’icône de dossier du site.

Par exemple, l&#39;image suivante montre la console Sites des communautés principale affichant les dossiers de deux sites de la communauté : [activer](/help/communities/getting-started-enablement.md) et [engager](/help/communities/getting-started.md):

![site-console](assets/site-console.png)

## Création du site {#site-creation}

La console de création de site fournit une approche pas à pas pour assembler les fonctionnalités du site en fonction d&#39;un [modèle de site communautaire ](/help/communities/sites.md) sélectionné et des paramètres.

Chaque site créé comprend une fonction de connexion, car les visiteurs du site doivent se connecter pour pouvoir publier du contenu, envoyer des messages ou participer à un groupe. Les autres fonctionnalités incluses sont les profils utilisateur, la messagerie, les notifications, le menu du site, la recherche, le thème et l’identité graphique.

Le processus est lancé en sélectionnant le bouton `Create` situé en haut de la console Sites des communautés.

Le processus de création est une série d’étapes présentées sous la forme de panneaux contenant un ensemble de fonctions à configurer (présentées sous la forme de sous-panneaux). Il est possible de passer à l&#39;étape **Suivant** ou **Précédent** à l&#39;étape précédente avant de valider le site à l&#39;étape finale.

### Étape 1 : Modèle de site {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

Dans le panneau Modèle de site, le titre, la description, la racine du site, la langue de base, le nom et le modèle de site sont spécifiés :

* **Titre du site de la communauté**

   Titre d’affichage du site.

   Le titre s’affiche sur le site publié ainsi que dans l’interface utilisateur d’administration du site.

* **Description du site de la communauté**

   Description du site.

   La description n’apparaît pas sur le site publié.

* **Racine du site de la communauté**

   Chemin d’accès racine au site.

   La racine par défaut est `/content/sites`, mais elle peut être déplacée à n’importe quel emplacement du site Web.

* **Langue de base du site de la communauté**

   (Ne pas modifier pour une seule langue : Anglais) Utilisez le menu déroulant pour choisir une *ou plusieurs* langues de base parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site communautaire sera créé pour chaque langue ajoutée et existera dans le même dossier de site en suivant la bonne pratique décrite dans [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md). La page racine de chaque site contient une page enfant nommée par le code de langue de l&#39;une des langues sélectionnées, comme &quot;en&quot; pour l&#39;anglais ou &quot;fr&quot; pour le français.

* **Nom du site de la communauté**:

   Nom de la page racine du site qui apparaît dans l’URL.

   * Vérifiez par doublon le nom car il n&#39;est pas facilement modifié une fois le site créé.
   * L&#39;URL de base ( `https://server:port/site root/site name)`) s&#39;affiche sous `Community Site Name`.

   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;

      *Par exemple*, `https://localhost:4502/content/sites/mysight/en.html`

* **Site communautaire** Templatemenu

   Utilisez le menu déroulant pour choisir un modèle de site communautaire [disponible](/help/communities/tools.md).

* Sélectionnez **Suivant**.

### Étape 2 : Conception {#step-design}

Le panneau Conception contient 2 sous-panneaux permettant de sélectionner le thème et la bannière d’identité graphique :

#### THÈME DU SITE COMMUNAUTAIRE {#community-site-theme}

![sitetheme](assets/sitetheme.png)

La structure utilise [le Bootstrap Twitter](https://twitterbootstrap.org/) pour apporter une conception adaptée et flexible au site. Un des nombreux thèmes de Bootstrap préchargés peut être sélectionné pour mettre en forme le modèle de site de communauté sélectionné ou un thème de Bootstrap peut être téléchargé.

Lorsqu’il est sélectionné, le thème est superposé avec une coche bleue opaque.

Une fois le site de la communauté publié, il est possible de [modifier les propriétés](#modifying-site-properties) et de sélectionner un autre thème.

#### MARQUE DU SITE COMMUNAUTAIRE {#community-site-branding}

![marque de site](assets/site-branding.png)

L’image de marque du site de la communauté est une image affichée en-tête en haut de chaque page.

L’image doit être dimensionnée de manière à être aussi large que l’affichage prévu de la page dans le navigateur et à 120 pixels de hauteur.

Lors de la création ou de la sélection d’une image, gardez à l’esprit :

* La hauteur de l’image sera rognée à 120 pixels, mesurée à partir du bord supérieur de l’image.
* L’image est épinglée sur le bord gauche de la fenêtre du navigateur.
* Il n&#39;y a pas de redimensionnement de l&#39;image, de telle sorte que lorsque la largeur de l&#39;image est...

   * Moins que la largeur du navigateur, l’image se répète horizontalement.
   * Plus grande que la largeur du navigateur, l’image semble recadrée.

* Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

Le panneau Paramètres contient plusieurs sous-panneaux présentant les fonctionnalités à configurer avant de passer à la dernière étape de création du site.

* [GESTION DES UTILISATEURS](#user-management)
* [BALISAGE](#tagging)
* [RÔLES](#roles)
* [MODÉRATION](#moderation)
* [ANALYTICS](#analytics)
* [TRADUCTION](#translation)
* [ACTIVER](#enablement)

>[!NOTE]
>
>**Activer le service de tunnel**
>
>Plusieurs des sous-panneaux Paramètres permettent à un membre de confiance de modérer l’UGC, de gérer des groupes ou d’être des contacts pour les ressources d’activation dans l’environnement de publication.
>
>La convention vise à ce que les [utilisateurs et les groupes d’utilisateurs ](/help/communities/users.md) côté publication (membres et groupes de membres) ne soient pas dupliqués dans l’environnement d’auteur.
>
>Ainsi, lors de la création du site communautaire dans l’environnement d’auteur et de l’affectation de membres de confiance à divers rôles, il est nécessaire de récupérer les données des membres de l’environnement de publication.
>
>Pour ce faire, l&#39;environnement d&#39;auteur doit activer ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`.

#### GESTION DES UTILISATEURS {#user-management}

![createsitetetetetsettings](assets/createsitesettings.png)

>[!NOTE]
>
>Il est recommandé que [les sites de la communauté d&#39;activation](/help/communities/overview.md#enablement-community) soient privés (pour plus d&#39;informations, contactez votre gestionnaire de compte).
>
>Un site communautaire est privé lorsque des visiteurs anonymes du site se voient refuser l’accès, peuvent ne pas s’enregistrer eux-mêmes et ne pas utiliser de connexion sociale.

* **Autoriser l&#39;enregistrement d&#39;utilisateur**

   Si cette option est cochée, les visiteurs du site peuvent devenir membres de la communauté en s&#39;inscrivant eux-mêmes.
Si cette option n&#39;est pas cochée, le site communautaire est *restreint* et les visiteurs du site doivent être affectés au groupe de membres du site communautaire, faire une demande ou être envoyés par courriel. Si cette option n’est pas cochée, l’accès anonyme ne doit pas être autorisé.
Dérecherchez un site de communauté *privé*. Cette option est cochée par défaut.

* **Autoriser l&#39;accès anonyme**

   Si cette case est cochée, le site communautaire est *ouvert *et tout visiteur du site peut y accéder.
Si cette option n’est pas cochée, seuls les membres connectés peuvent accéder au site.
Décochez la recherche d&#39;un *site communautaire *privé. Cette option est cochée par défaut.

* **Autoriser les messages**

   Si cette case est cochée, les membres peuvent envoyer des messages les uns aux autres et au groupe sur le site communautaire.
Si cette option n’est pas cochée, la messagerie n’est pas configurée pour la communauté.
Cette option n’est pas cochée par défaut.

* **Autoriser les connexions sociales : Facebook**

   Si cette case est cochée, autorisez les visiteurs du site à se connecter à l’aide de leurs identifiants de compte Facebook. La [configuration de cloud Facebook ](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) sélectionnée doit être configurée pour ajouter des utilisateurs au groupe de membres du site de la communauté une fois le site de la communauté créé.
Si cette option n’est pas cochée, aucune connexion Facebook n’est présentée.
Ne cochez pas la case pour un site de communauté *privé*. Cette option n’est pas cochée par défaut.

* **Autoriser les connexions sociales : Twitter**

   Si cette case est cochée, autorisez les visiteurs du site à se connecter à l’aide de leurs identifiants de compte Twitter. La [configuration de cloud Twitter ](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) sélectionnée doit être configurée pour ajouter des utilisateurs au groupe de membres du site de la communauté une fois le site de la communauté créé.
Si cette option n’est pas cochée, aucune connexion Twitter n’est présentée.
Ne cochez pas la case pour un site de communauté *privé*. Cette option n’est pas cochée par défaut.

>[!NOTE]
>
>**Autorisation des connexions aux réseaux sociaux**
>
>Bien que des exemples de configurations Facebook et Twitter puissent exister et être sélectionnables, pour un [environnement de production](/help/sites-administering/production-ready.md), il est nécessaire de créer des applications Facebook et Twitter personnalisées. Voir [Connexion aux réseaux sociaux avec Facebook et Twitter](/help/communities/social-login.md).

#### BALISAGE {#tagging}

![balisage de site](assets/site-tagging.png)

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant des Espaces de nommage de balises précédemment définis dans la [Console de balisage](/help/sites-administering/tags.md#tagging-console).

En outre, la sélection des espaces de nommage de balises pour le site de la communauté limite la sélection présentée lors de la définition de catalogues et de ressources. Voir [Ressources d’activation du balisage](/help/communities/tag-resources.md) pour obtenir des informations importantes.

* zone de recherche de texte : Saisie de débuts pour identifier les balises autorisées sur le site.

#### RÔLES {#roles}

![Rôles communautaires](assets/site-admin-2.png)

Les rôles [des membres de la communauté](/help/communities/users.md) sont assignés avec ces paramètres.

Il est facile de trouver des membres de la communauté en effectuant une recherche par anticipation.

* **Gestionnaires de la communauté**

   Début de saisie pour sélectionner un ou plusieurs membres de la communauté ou groupes de membres qui peuvent gérer les membres de la communauté et les groupes de membres.

* **Modérateurs de la communauté**

   Début de saisie permettant de sélectionner un ou plusieurs membres de la communauté ou groupes de membres à approuver en tant que modérateurs du contenu généré par l’utilisateur.

* **Membres privilégiés de la communauté**

   Début de saisie permettant de sélectionner un ou plusieurs membres de la communauté ou groupes de membres pour qu’ils puissent créer un nouveau contenu lorsque `Allow Privileged Member` a été sélectionné pour une fonction [communautaire](/help/communities/functions.md).

* **Administrateurs de la communauté**

   Début de saisie permettant de sélectionner un ou plusieurs administrateurs du site capables de gérer la structure du site indépendamment des autres administrateurs du site et de l’administrateur de la communauté par défaut. Ils peuvent créer un groupe à n’importe quel niveau de la hiérarchie et devenir l’administrateur par défaut des groupes imbriqués (mais ils peuvent ensuite être supprimés du rôle d’administration des groupes imbriqués).

#### MODÉRATION {#moderation}

![site-modération](assets/site-moderation.png)

Le paramètre global de modération du contenu généré par l’utilisateur (UGC) est contrôlé par ces paramètres. Les composants individuels disposent de paramètres supplémentaires pour contrôler la modération.

* **Le contenu est prémodéré**

   Si cette option est cochée, le contenu de la communauté publié n’apparaîtra pas avant d’être approuvé par un modérateur. Cette option n’est pas cochée par défaut. Pour plus d’informations, voir [Modération du contenu de la communauté](/help/communities/moderate-ugc.md#premoderation).

* **Seuil de marquage avant que le contenu ne soit masqué**

   Si la valeur est supérieure à 0, le nombre de fois où une rubrique ou une publication doit être marquée avant d’être masquée de la vue publique. Si elle est définie sur -1, la rubrique ou la publication marquée n’est jamais masquée de la vue publique. La valeur par défaut est 5.

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **Enable Analytics (Activer Adobe Analytics)**

   Disponible uniquement lorsque Adobe Analytics a été [configuré](/help/communities/analytics.md) pour les fonctionnalités des communautés.
Cette option n’est pas cochée par défaut. Si cette case est cochée, un menu de sélection supplémentaire s&#39;affiche :

![site-analytics-enable](assets/site-analytics-enable.png)

* **Référence de la structure de configuration du cloud**

   Dans le menu déroulant, sélectionnez la structure de service cloud Analytics configurée pour ce site de la communauté.
   `Communities` est l’exemple de cadre de la documentation sur la configuration  [Analytics pour les ](/help/communities/analytics.md#aem-analytics-framework-configuration) fonctionnalités des communautés.

#### TRADUCTION {#translation}

![site-translation](assets/site-translation.png)

* **Activer la traduction automatique**

   Si cette option est cochée (la valeur par défaut est désactivée), la traduction automatique est activée pour l’UGC dans le site. Ceci n’affecte aucun autre contenu, tel que le contenu de la page, même si le site est configuré en tant que site multilingue. Voir [Traduction du contenu généré par l’utilisateur](/help/communities/translate-ugc.md) pour plus d’informations sur la configuration d’un service de traduction sous licence pour AEM Communities. Voir [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md) pour un aperçu complet.

![allow-machine-translation](assets/allow-machine-translation.png)

* **Activer la traduction automatique pour les langues sélectionnées**

   Par défaut, les langues activées pour la traduction automatique correspondent au paramètre système spécifié par la configuration de l&#39;intégration de traduction [](/help/communities/translate-ugc.md#translation-integration-configuration). Ces paramètres par défaut peuvent être remplacés pour ce site en supprimant les valeurs par défaut et/ou en sélectionnant d&#39;autres langues dans le menu déroulant.

* **Sélectionner le fournisseur de traduction**

   Par défaut, le prestataire est un service d’évaluation utilisant `microsoft` pour la démonstration uniquement. Si aucun prestataire de traduction n’est autorisé, **Autoriser la traduction automatique** doit être désactivé.

* **Sélectionner le magasin partagé global**

   Pour un site Web avec plusieurs copies de langue, une boutique partagée globale fournit un seul thread de conversation, visible à partir de chaque copie de langue. Pour ce faire, sélectionnez l&#39;une des langues incluses comme copie de langue. La valeur par défaut est *Pas de stockage partagé global*.

* **Sélectionner la configuration du fournisseur de traduction**

   Choisissez une structure d&#39;intégration de traduction [](/help/sites-administering/tc-tic.md) créée pour le fournisseur de traduction sous licence.

* **Sélectionner les options de traduction pour votre site de la communauté**

   * **Traduire la page entière**

      Si cette option est sélectionnée, tous les UGC d’une page sont traduits dans la langue de base de la page.

      La valeur par défaut est *non sélectionnée*.

   * **Traduire la sélection uniquement**

      Si cette option est sélectionnée, une option de traduction s’affiche en regard de chaque publication, ce qui permet de traduire des publications individuelles dans la langue de base de la page.
La valeur par défaut est *sélectionnée*.

* **Sélectionner les options de rémanence**

   * **Traduisez les contributions sur demande de l’utilisateur et conservez-les**
par la suite. Si cette option est sélectionnée, le contenu n’est pas traduit tant qu’une requête n’a pas été effectuée. Une fois traduite, la traduction est stockée dans le référentiel.

      La valeur par défaut est *non sélectionnée*.

   * **Ne pas conserver les traductions**

      Si cette option est sélectionnée, les traductions ne sont pas stockées dans le référentiel.

      Si cette option n’est pas sélectionnée, les traductions sont conservées.

      La valeur par défaut est *non sélectionnée*.

* **Rendu dynamique**

   Sélectionnez l&#39;une des options suivantes :

   * `Always show contributions in the original language` (default)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### ACTIVER {#enablement}

![activation de site](assets/site-enablement.png)

Les paramètres `ENABLEMENT`s&#39;appliquent lorsque le modèle de site de communauté choisi inclut la fonction [assignations](/help/communities/functions.md#assignments-function), disponible lorsque les fonctionnalités d&#39;activation sont sous licence et [configurées](/help/communities/enablement.md). Le modèle de site de référence qui inclut la fonction assignations est `Reference Structured Learning Site Template.`

* **Gestionnaires**
 d&#39;activation (Obligatoire) Seuls les membres du  `Community Enablementmanagers` groupe peuvent être sélectionnés pour la gestion de cette communauté d&#39;activation. Les gestionnaires d&#39;activation sont chargés d&#39;affecter les membres aux ressources. Voir aussi [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

* **ID d’entreprise Marketing Cloud**

   (Facultatif) ID d’une licence [Video Heartbeat Analytics](/help/communities/analytics.md#video-heartbeat-analytics).

* Sélectionnez **Suivant**.

### Étape 4 : Créer un site de communautés {#step-create-communities-site}

Si des ajustements sont nécessaires, utilisez le bouton **Précédent** pour les effectuer.

Une fois **Create** sélectionné et démarré, le processus de création du site ne peut pas être interrompu.

Une fois le site créé :

* La modification de l’URL (nom du noeud) n’est pas prise en charge.
* Les modifications futures apportées au modèle de site communautaire n’auront aucune incidence sur le site communautaire créé.
* La désactivation du modèle de site de la communauté n’affectera pas le site créé.
* Il est possible de modifier la [STRUCTURE](#modify-structure) d&#39;un site communautaire en modifiant ses propriétés.

![create-site](assets/create-site1.png)

Une fois le processus terminé, le dossier du nouveau site s&#39;affiche dans la console Sites des communautés, d&#39;où les auteurs peuvent ajouter du contenu de page ou les administrateurs peuvent modifier les propriétés du site.

![modify-site-property](assets/modify-site-property.png)

Pour modifier un site de la communauté, sélectionnez le dossier de projet qui lui correspond pour l’ouvrir :

![site-project](assets/site-project.png)

Lorsque vous passez la souris sur un site ou touchez une carte de site, des icônes s’affichent qui permettent [de modifier le site en mode d’auteur](#authoring-site-content), [d’ouvrir les propriétés du site pour modification](#modifying-site-properties), [de publier le site](#publishing-the-site), [d’exporter le site](#exporting-the-site) et [de supprimer le site&lt;a9/ .](#deleting-the-site)

## Création de contenu du site {#authoring-site-content}

Le contenu d&#39;un site peut être créé avec les mêmes outils que tout autre site AEM. Pour ouvrir le site à des fins de création, sélectionnez l&#39;icône `Open Site` qui s&#39;affiche lorsque vous survolez le site avec la souris. Le site s&#39;ouvre dans un nouvel onglet de sorte que la console Sites des communautés reste accessible.

![site-content](assets/site-content.png)

>[!NOTE]
>
>Si l&#39;AEM n&#39;est pas familier, vue la documentation sur la [gestion de base](/help/sites-authoring/basic-handling.md) et un [guide rapide de création de pages](/help/sites-authoring/qg-page-authoring.md).

## Modification des propriétés du site {#modifying-site-properties}

![edit-site](assets/edit-site.png)

Les propriétés d&#39;un site existant, spécifiées pendant le processus de création du site, peuvent être modifiées en sélectionnant l&#39;icône `Edit Site`qui s&#39;affiche lorsque vous survolez le site avec la souris.

`Details of the following properties match the descriptions provided in the` [Section ](#site-creation) Création du site.

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### Modifier de base {#modify-basic}

Le panneau BASIC permet de modifier :

* Titre du site de la communauté
* Description du site de la communauté

Le nom du site de la communauté ne peut pas être modifié.

Le choix d’un autre modèle de site communautaire n’aurait aucun effet sur un site communautaire existant, car il n’y a plus de connexion entre les modèles et les sites.

Au lieu de cela, la [STRUCTURE](#modify-structure) du site communautaire peut être modifiée.

### Modifier la structure {#modify-structure}

Le panneau STRUCTURE permet de modifier la structure initialement créée à partir du modèle de site communautaire sélectionné. Depuis le panneau, il est possible de :

* Faites glisser d&#39;autres [fonctions communautaires](/help/communities/functions.md) dans la structure du site.
* Sur une instance d’une fonction de communauté dans la structure du site :

   * **`gear icon`**

      Modifiez les paramètres, y compris le titre d’affichage et le nom d’URL*, ainsi que les [groupes de membres privilégiés](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

      Supprimez (supprimez) des fonctions de la structure du site.

   * **`grid icon`**

      Modifiez l&#39;ordre des fonctions tel qu&#39;il s&#39;affiche dans la barre de navigation de niveau supérieur du site.

>[!NOTE]
>
>Vous pouvez modifier l&#39;ordre de toutes les fonctions de la Structure du site, à l&#39;exception de la fonction située en haut. Par conséquent, la page d&#39;accueil du site des communautés ne peut pas être modifiée.

>[!CAUTION]
>
>* Bien que le titre d’affichage puisse être modifié sans effets secondaires, il n’est pas recommandé de modifier le nom d’URL d’une fonction de communauté appartenant à un site communautaire.
>
>
Par exemple, renommer l’URL ne déplace pas l’UGC existant, avec pour effet de &quot;perdre&quot; l’UGC.

>[!CAUTION]
>
>La fonction groups doit *ne pas* être la *première fonction ou la seule* fonction dans la structure du site.
>
>Toute autre fonction, telle que la fonction de page [page](/help/communities/functions.md#page-function), doit être incluse et répertoriée en premier.

#### Exemple : Ajouter une fonction de catalogue à une structure de site communautaire {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### Modifier la conception {#modify-design}

Le panneau DESIGN permet d’appliquer un nouveau thème :

* [Thème des sites de la communauté](#community-site-theme)
* [Valorisation de marque des sites de la communauté](#community-site-branding)

   * Faites défiler l’écran jusqu’au bas du panneau pour modifier l’image de marque.

### Modifier les paramètres {#modify-settings}

Le panneau PARAMÈTRES permet d’accéder à la plupart des paramètres sous les sous-panneaux de l’étape 3 de la création d’un site communautaire :

* [Gestion des utilisateurs](#user-management)
* [Balises](#tagging)
* [Modération](#moderation)
* [Rôles des membres](#roles)
* [Analyses](#analytics)
* [Traduction](#translation)

### Modifier la miniature {#modify-thumbnail}

Le panneau MINIATURE permet de télécharger une image pour représenter le site dans la console Sites des communautés.

### Modifier l&#39;activation {#modify-enablement}

Le panneau ENABLEMENT permet d&#39;accéder aux paramètres fournis lors de la création du site communautaire.

Voir la description de [ENABLEMENT](#enablement).

## Publication du site {#publishing-the-site}

Une fois qu&#39;un site communautaire a été créé ou modifié, il est possible de le publier (d&#39;activer) en sélectionnant l&#39;icône `Publish Site` qui s&#39;affiche lorsque vous pointez la souris sur le site.

![site de publication](assets/publish-site.png)

Il y aura une indication après la publication du site.

![site-publié](assets/site-published.png)

### Publication avec des groupes imbriqués {#publishing-with-nested-groups}

Après la publication d’un site communautaire, il est nécessaire de publier individuellement chaque sous-communauté (groupe imbriqué) créée à l’aide de la [console Groupes](/help/communities/groups.md).

## Exportation du site {#exporting-the-site}

![site d&#39;exportation](assets/export-site.png)

Sélectionnez l’icône d’exportation, placez le pointeur de la souris sur le site, pour créer un package du site communautaire qui est à la fois stocké dans [gestionnaire de packages](/help/sites-administering/package-manager.md) et téléchargé.

Notez que UGC n&#39;est pas inclus dans le package du site.

## Suppression du site {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

Pour supprimer le site de la communauté, sélectionnez l&#39;icône Supprimer le site qui s&#39;affiche lorsque vous placez le pointeur de la souris sur le site dans la console du site des communautés. Cette action supprime tous les éléments associés au site, tels que l’UGC, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

## Groupes d’utilisateurs de la communauté créés {#created-community-user-groups}

Une fois le nouveau site de la communauté publié, les nouveaux groupes de membres (groupes d’utilisateurs créés dans l’environnement de publication) disposent des autorisations appropriées définies pour divers rôles d’administrateur et de membre.

Le nom créé pour les groupes de membres comprend le *nom-site* donné au site à l&#39;[étape 1](#step13asitetemplate) (nom qui s&#39;affiche dans l&#39;URL) ainsi qu&#39;un identifiant unique afin d&#39;éviter les conflits avec les sites et groupes communautaires ayant le même nom-site pour des racines de site différentes.

Par exemple, si le nom était &quot;engagement&quot; pour un site intitulé &quot;Didacticiel de prise en main&quot;, le groupe d’utilisateurs pour les modérateurs serait :

* titre : Modérateurs d’engagement de la communauté
* name: community-*engager-uid*-modérateurs

Notez que tous les membres affectés des rôles en tant que modérateurs ou administrateurs de groupe lors de la création du site, seront affectés au groupe approprié ainsi qu’au groupe de membres. Ces groupes et affectations de membres sont créés lors de la publication du nouveau site.

Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

>[!NOTE]
>
>Si [Autoriser la connexion aux réseaux sociaux : Facebook](#user-management) est activé une fois le groupe d’utilisateurs
>
>* `community-<site-name>-<uid>-members`
>
>
est créée, le [service cloud Facebook ](/help/communities/social-login.md#createafacebookcloudservice) appliqué doit être configuré pour ajouter des utilisateurs à ce groupe.

## Configurer pour l&#39;erreur d&#39;authentification {#configure-for-authentication-error}

Par défaut, un site de la communauté redirige vers un exemple de page de connexion lorsque l’utilisateur saisit des informations d’identification erronées et ne parvient pas à se connecter. Cet exemple de connexion ne sera pas présent sur un [serveur de production](/help/sites-administering/production-ready.md).

Pour rediriger correctement un site, une fois qu’il a été configuré et poussé vers la publication, procédez comme suit pour obtenir l’échec d’authentification de la redirection vers le site de la communauté :

* Sur chaque instance de publication AEM.
* Connectez-vous avec des droits d’administrateur.
* Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md).

   * Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* Recherchez `Adobe Granite Login Selector Authentication Handler`.
* Sélectionnez l&#39;icône `pencil` pour ouvrir la configuration à modifier.
* Saisissez les **Mappages de page de connexion** comme suit :

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   Par exemple :
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* Sélectionnez **Enregistrer**.

![auth-error](assets/auth-error.png)

### Redirection de l&#39;authentification de test {#test-authentication-redirection}

Sur la même instance de publication AEM configurée avec un mappage de page de connexion pour le site de la communauté :

* Accédez à la page d&#39;accueil du site de la communauté.

   * Par exemple, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* Sélectionnez Déconnexion.
* Sélectionnez Log In.
* Entrez des informations d’identification manifestement incorrectes, telles que le nom d’utilisateur &quot;x&quot; et le mot de passe &quot;x&quot;.
* La page de connexion doit s&#39;afficher avec une erreur de connexion non valide.

![authentification test](assets/test-authentication.png)

## Accès aux sites de la communauté à partir de la console des sites principaux {#accessing-community-sites-from-main-sites-console}

Dans la console Sites de navigation globale, les sites de la communauté se trouvent dans le dossier `Community Sites`.

Bien qu&#39;il soit possible d&#39;accéder à un site communautaire de cette façon, pour les tâches administratives, le site communautaire doit être accessible à partir de la console Sites communautaires.

![access-site](assets/access-site.png)



