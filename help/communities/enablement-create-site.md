---
title: Création d’un nouveau site communautaire pour l’activation
seo-title: Création d’un nouveau site communautaire pour l’activation
description: Créer un site communautaire pour l’activation
seo-description: Créer un site communautaire pour l’activation
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: e9d5a7acad04d841cbc7d62050163f3de998fab6
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 4%

---


# Création d’un nouveau site communautaire pour l’activation {#author-a-new-community-site-for-enablement}

## Créer un site de communauté {#create-community-site}

[La ](/help/communities/sites-console.md) création d’un site communautaire utilise un assistant qui vous guide tout au long des étapes de création d’un site communautaire. Il est possible de passer à l&#39;étape `Next` ou `Back` à l&#39;étape précédente avant de valider le site à l&#39;étape finale.

Pour commencer à créer un site communautaire :

Utilisation de l’instance d’auteur [](https://localhost:4502/)

* Connectez-vous avec les droits d’administrateur et accédez à **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**.

* Sélectionnez **Créer**.

### Étape 1 : Modèle de site {#step-site-template}

![modèle de site d&#39;activation](assets/enablement-site-template.png)

À l&#39;étape **Modèle de site**, saisissez un titre, une description, le nom de l&#39;URL, puis sélectionnez un modèle de site de la communauté, par exemple :

* **Titre du site de la communauté**: `Enablement Tutorial`.

* **Description du site de la communauté**: `A site for enabling the community to learn.`

* **Racine** du site de la communauté : (laisser vide pour la racine par défaut  `/content/sites`)

* **Configurations** du cloud : (laissez vide si aucune configuration de cloud n’est spécifiée) fournissez le chemin d’accès aux configurations de cloud spécifiées.
* **Langue** de base du site de la communauté : (ne pas toucher à la langue unique : Anglais) utilisez la liste déroulante pour choisir une  *ou* plusieurs langues parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site communautaire sera créé pour chaque langue ajoutée et existera dans le même dossier de site en suivant la bonne pratique décrite dans [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md). La page racine de chaque site contient une page enfant nommée par le code de langue de l&#39;une des langues sélectionnées, comme &quot;en&quot; pour l&#39;anglais ou &quot;fr&quot; pour le français.

* **Nom du site de la communauté**: `enable`

   * L&#39;URL initiale s&#39;affiche sous le nom du site de la communauté.
   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;
      *Par exemple*, https://localhost:4502/content/sites/  `enable/en.html`

* **Modèle** de site de référence : descendre pour choisir  `Reference Structured Learning Site Template`

Sélectionnez **Suivant**.

### Étape 2 : Conception {#step-design}

L’étape de conception est présentée en deux sections pour la sélection du thème et de la bannière de marque :

#### THÈME DU SITE COMMUNAUTAIRE {#community-site-theme}

Sélectionnez le style à appliquer au modèle. Une fois sélectionné, le thème sera superposé avec une coche.

#### MARQUE DU SITE COMMUNAUTAIRE {#community-site-branding}

(Facultatif) Téléchargez une image de bannière pour l’afficher sur les pages du site. La bannière est épinglée sur le bord gauche du navigateur, entre l’en-tête du site de la communauté et le menu (liens de navigation). La hauteur de la bannière est rognée à 120 pixels. Il n’existe aucun redimensionnement de la bannière pour s’adapter à la largeur du navigateur et à la hauteur de 120 pixels.

![site-branding1](assets/site-branding1.png)

![site-branding2](assets/site-branding2.png)

Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

À l’étape Paramètres, avant de sélectionner `Next`, vous pouvez constater que sept sections donnent accès à des configurations comprenant la gestion des utilisateurs, le balisage, les rôles, la modération, les analyses, la traduction et l’activation.

#### GESTION DES UTILISATEURS {#user-management}

Il est recommandé que [les communautés d&#39;activation](/help/communities/overview.md#enablement-community) soient privées.

Un site communautaire est privé lorsque des visiteurs anonymes du site se voient refuser l’accès, peuvent ne pas s’enregistrer eux-mêmes et ne pas utiliser de connexion sociale.

Vérifiez que la plupart des cases à cocher sont désélectionnées pour [User Management](/help/communities/sites-console.md#user-management) :

* N&#39;autorisez PAS les visiteurs du site à s&#39;inscrire eux-mêmes.
* N&#39;autorisez PAS les visiteurs anonymes du site à vue au site.
* Facultatif : autoriser ou non la messagerie parmi les membres de la communauté.
* N’autorisez PAS la connexion avec Facebook.
* N’autorisez PAS la connexion avec Twitter.

![user-mgmt](assets/user-mgmt.png)

#### BALISAGE {#tagging}

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant AEM espaces de nommage précédemment définis dans la [Console de balisage](/help/sites-administering/tags.md#tagging-console) (comme l&#39;[espace de nommage didacticiel](/help/communities/enablement-setup.md#create-tutorial-tags)).

En outre, la sélection des Espaces de nommage de balises pour le site communautaire limite la sélection présentée lors de la définition de catalogues et de ressources d’activation. Voir [Ressources d’activation du balisage](/help/communities/tag-resources.md) pour obtenir des informations importantes.

La recherche d&#39;espaces de nommage est facile avec la recherche par type. Par exemple,

* Type `tut`
* Sélectionner `Tutorial`

![activation-balisage](assets/enablement-tagging.png)

### RÔLES {#roles}

[Les rôles des membres de la communauté ](/help/communities/users.md) sont attribués par le biais des paramètres de la section Rôles.

Pour permettre à un membre de la communauté (ou à un groupe de membres) de découvrir le site en tant que responsable de la communauté, utilisez la recherche par type et sélectionnez le nom du membre ou du groupe dans les options de la liste déroulante.

Par exemple,

* Type `q`
* Sélectionnez [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Le ](/help/communities/deploy-communities.md#tunnel-service-on-author) service Tunnel permet de sélectionner les membres et les groupes existants uniquement dans l’environnement de publication.

![rôles d&#39;activation](assets/site-admin.png)

#### MODÉRATION {#moderation}

Acceptez les paramètres globaux par défaut pour [modération](/help/communities/sites-console.md#moderation) le contenu généré par l’utilisateur (UGC).

![modération1](assets/moderation1.png)

#### ANALYTICS {#analytics}

Dans la liste déroulante, sélectionnez la structure de service cloud Analytics configurée pour ce site de la communauté.

La sélection vue dans la capture d&#39;écran, `Communities`, est l&#39;exemple de structure de la documentation de configuration [](/help/communities/analytics.md#aem-analytics-framework-configuration).

![analyses](assets/analytics.png)

#### TRADUCTION {#translation}

Les [paramètres de traduction](/help/communities/sites-console.md#translation) indiquent si l&#39;UGC peut être traduit ou non et dans quelle langue, le cas échéant.

* Cochez **Autoriser la traduction automatique**.
* Utiliser les paramètres par défaut

![traduction](assets/translation.png)

#### ACTIVER {#enablement}

Pour une communauté d’activation, il est nécessaire d’identifier un ou plusieurs gestionnaires d’activation de la communauté.

* **Gestionnaires**
 d&#39;activation (requis) Membres de 
`Community Enablement Managers` sont disponibles pour être sélectionnés pour gérer ce site communautaire.

   * Type `s`
   * Sélectionner `Sirius Nilson`

* **ID**
 d’organisation du Marketing Cloud (facultatif) ID d’un compte Adobe Analytics nécessaire lors de l’inclusion des  [analyses de pulsation ](/help/communities/analytics.md#video-heartbeat-analytics) vidéo dans le rapports d’activation.

![activation](assets/enablement.png)

Sélectionnez **Suivant**.

### Étape 4 : Créer un site communautaire {#step-create-community-site}

Sélectionnez **Créer.**

![prévisualisation](assets/preview.png)

Une fois le processus terminé, le dossier du nouveau site s’affiche dans la console Communautés > Sites.

![activationsitecréé](assets/enablementsitecreated.png)

### Publier le nouveau site de la communauté {#publish-the-new-community-site}

Le site créé doit être géré à partir de la console Communautés - Sites, la même console que celle où de nouveaux sites peuvent être créés.

Après avoir sélectionné le dossier du site de la communauté, passez la souris sur l’icône du site pour afficher quatre icônes d’action :

![siteactionicones](assets/siteactionicons.png)

Lorsque vous sélectionnez l’icône représentant des points de suspension (icône Autres actions), les options Exporter le site et Supprimer le site s’affichent.

![siteactionsnew](assets/siteactionsnew.png)

De gauche à droite, ils sont :

* **Ouvrir le site**

   Sélectionnez l’icône représentant un crayon pour ouvrir le site de la communauté en mode d’édition de l’auteur, pour ajouter et/ou configurer des composants de page.

* **Modifier le site**

   Sélectionnez l’icône Propriétés pour ouvrir le site de la communauté en vue de modifier les propriétés, par exemple le titre ou pour modifier le thème.

* **Publier le site**

   Sélectionnez l’icône du monde pour publier le site de la communauté (sur localhost:4503 par défaut).

* **Exporter le site**

   Sélectionnez l’icône d’exportation pour créer un package du site communautaire qui est stocké dans [gestionnaire de packages](/help/sites-administering/package-manager.md) et téléchargé.
Notez que UGC n&#39;est pas inclus dans le package du site.

* **Supprimer le site**

   Pour supprimer le site de la communauté, sélectionnez l&#39;icône Supprimer le site qui s&#39;affiche lorsque vous placez le pointeur de la souris sur le site dans la console du site des communautés. Cette action supprime tous les éléments associés au site, tels que l’UGC, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

   ![activer les itéactions](assets/enablesiteactions.png)

#### Sélectionnez Publier {#select-publish}

Sélectionnez l’icône du monde pour publier le site de la communauté.

![site de publication](assets/publish-site.png)

Il y aura une indication que le site a été publié.

![site-publié](assets/site-published.png)

## Utilisateurs de la communauté et groupes d’utilisateurs {#community-users-user-groups}

### Avis Nouveaux groupes d&#39;utilisateurs de la communauté {#notice-new-community-user-groups}

En plus du nouveau site communautaire, de nouveaux groupes d’utilisateurs sont créés et disposent des autorisations appropriées définies pour diverses fonctions administratives. Pour plus d&#39;informations, consultez [Groupes d&#39;utilisateurs pour les sites communautaires](/help/communities/users.md#usergroupsforcommunitysites).

Pour ce nouveau site communautaire, étant donné le nom du site &quot;activer&quot; à l’étape 1, les nouveaux groupes d’utilisateurs qui existent dans l’environnement de publication peuvent être consultés à partir de la [console Membres et groupes des communautés](/help/communities/members.md#groups-console) :

![community_usergroup](assets/community_usergroup.png)

### Affecter des membres au groupe d&#39;activation de la communauté {#assign-members-to-community-enable-members-group}

Sur l’auteur, avec le service tunnel activé, il est possible d’affecter les [utilisateurs créés lors de la configuration initiale](/help/communities/enablement-setup.md#publishcreateenablementmembers) au groupe Membres de la communauté pour le site communautaire nouvellement créé.

A l’aide de la console Groupes de la communauté, les membres peuvent être ajoutés individuellement ou par le biais d’une adhésion à un groupe.

Dans cet exemple, le groupe `Community Ski Class` est ajouté en tant que membre du groupe `Community Enable Members` ainsi que membre `Quinn Harper`.

* Accédez à la console **Communautés, Groupes**.
* Sélectionner le groupe *Membres d&#39;activation de la communauté*
* Saisissez &#39;ski&#39; dans la zone de recherche **Ajouter les membres au groupe**.
* Sélectionnez *Classe de ski communautaire* (groupe d’apprenants).
* Saisissez &quot;quinn&quot; dans la zone de recherche.
* Sélectionnez *Quinn Harper* (contact avec la ressource d&#39;activation).

* Sélectionnez **Enregistrer**

![edit-group-settings](assets/edit-group-settings.png)

## Configurations sur la publication {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![activation-connexion](assets/enablement-login.png)

### Configurer pour l&#39;erreur d&#39;authentification {#configure-for-authentication-error}

Une fois qu’un site a été configuré et envoyé pour publication, [configurez le mappage de connexion](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) sur l’instance de publication. L’avantage est que lorsque les informations d’identification de connexion ne sont pas saisies correctement, l’erreur d’authentification affiche à nouveau la page de connexion du site de la communauté avec un message d’erreur.

Ajoutez un `Login Page Mapping` comme suit :

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Facultatif) Modifiez la Page d&#39;accueil par défaut {#optional-change-the-default-home-page}

Lorsque vous travaillez avec le site de publication à des fins de démonstration, il peut s’avérer utile de modifier la page d&#39;accueil par défaut du nouveau site.

Pour ce faire, il faut utiliser [CRX|DE](https://localhost:4503/crx/de) Lite pour modifier la table [mappage de ressources](/help/sites-deploying/resource-mapping.md) lors de la publication.

Pour commencer :

1. Lors de la publication, accédez à CRXDE et connectez-vous avec des droits d’administrateur.

   * Par exemple, accédez à [https://localhost:4503/crx/de](https://localhost:4503/crx/de) et connectez-vous avec `admin/admin`

1. Dans le navigateur du projet, développez `/etc/map`
1. Sélectionnez le noeud `http`

   * Sélectionnez **Créer un noeud**

      * **** Namelocalhost.4503

         (do *not* use &#39;:&#39;)

      * **** [Type:Mappage](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Avec le nouveau noeud `localhost.4503` sélectionné

   * Ajoute, propriété

      * **Nom** sling:match
      * **** TypeString
      * **Valeur** localhost.4503/$

   (doit se terminer par &#39;$&#39; char)

   * Ajoute, propriété

      * **Nom** sling:internalRedirect
      * **** TypeString
      * **Valeur**  /content/sites/enable/en.html


1. Sélectionner **Enregistrer tout**
1. (Facultatif) Supprimer l’historique de navigation
1. Accédez à https://localhost:4503/

   * Arrivez à https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Pour désactiver cette fonction, il vous suffit de pré-ajouter la valeur de propriété `sling:match` avec un &#39;x&#39; - `xlocalhost.4503/$` - et **Enregistrer tout**.

![change-default-homepage](assets/change-default-homepage.png)

#### Dépannage : Erreur lors de l&#39;enregistrement de la carte {#troubleshooting-error-saving-map}

Si vous ne parvenez pas à enregistrer les modifications, veillez à ce que le nom du noeud soit `localhost.4503`, avec un séparateur de point et non `localhost:4503` avec un séparateur de deux points, car `localhost` n&#39;est pas un préfixe d&#39;espace de nommage valide.

![error-map](assets/error-map.png)

#### Dépannage : Echec de la redirection {#troubleshooting-fail-to-redirect}

La valeur &#39;**$**&#39; à la fin de la chaîne `sling:match` de l&#39;expression régulière est cruciale, de sorte que seul `https://localhost:4503/` est mappé exactement, sinon la valeur de redirection est précédée de tout chemin d&#39;accès qui peut exister après le serveur:port dans l&#39;URL. Ainsi, lorsque AEM tente de rediriger vers la page de connexion, elle échoue.

## Modification du site communautaire {#modifying-the-community-site}

Une fois le site créé, les auteurs peuvent utiliser l&#39;[icône Ouvrir le site](/help/communities/sites-console.md#authoring-site-content) pour effectuer des activités de création d&#39;AEM standard.

En outre, les administrateurs peuvent utiliser l&#39;[icône Modifier le site](/help/communities/sites-console.md#modifying-site-properties) pour modifier les propriétés du site, comme le titre.

Après toute modification, n’oubliez pas de **Enregistrer** et de re-**publier** le site.

>[!NOTE]
>
>Si l&#39;AEM n&#39;est pas familier, vue la documentation sur la [gestion de base](/help/sites-authoring/basic-handling.md) et un [guide rapide de création de pages](/help/sites-authoring/qg-page-authoring.md).

### Ajouter un catalogue {#add-a-catalog}

Le modèle de site communautaire choisi pour ce site communautaire doit contenir la fonctionnalité de catalogue.

Dans le cas contraire, la fonction de catalogue peut être facilement ajoutée. Cela permettrait aux autres membres de la communauté, non affectés à des ressources d’activation ou à un chemin d’apprentissage, de sélectionner des ressources d’activation dans un catalogue.

Si la structure du site contient déjà la fonctionnalité de catalogue, son titre peut être modifié.

Pour modifier la structure du site, accédez à la console **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**, ouvrez le dossier `enable`, puis sélectionnez l&#39;icône **Modifier le site** pour accéder aux propriétés de `Enablement Tutorial`.

Sélectionnez le panneau STRUCTURE pour ajouter un catalogue ou modifier un catalogue existant :

* **Titre**: `Ski Catalog`

* **URL**: `catalog`

* **Sélectionner tous les Espaces de nommage** : laissez comme valeur par défaut.

* Sélectionnez **Enregistrer**.

![modify-site-structure](assets/modify-site-structure.png)

Utilisez l’icône Position pour déplacer la fonction Catalogue vers la deuxième position, après les affectations.

![move-catalog-func](assets/move-catalog-func.png)

Sélectionnez **Enregistrer** dans le coin supérieur droit pour enregistrer les modifications sur le site de la communauté.

Ensuite, re-**Publiez** le site.

