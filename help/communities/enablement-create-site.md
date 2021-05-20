---
title: Création d’un site communautaire pour l’activation
seo-title: Création d’un site communautaire pour l’activation
description: Créer un site de communauté pour l’activation
seo-description: Créer un site de communauté pour l’activation
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
exl-id: 812bbf7b-c49f-4c34-a47d-636b0468e0ba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 4%

---

# Création d’un site communautaire pour l’activation {#author-a-new-community-site-for-enablement}

## Créer un site de communauté {#create-community-site}

[La ](/help/communities/sites-console.md) création d’un site communautaire s’accompagne d’un assistant qui vous guide tout au long des étapes de création d’un site communautaire. Il est possible de passer à l’étape `Next` ou `Back` à l’étape précédente avant de valider le site à l’étape finale.

Pour commencer à créer un site communautaire :

Utilisation de l’ [instance d’auteur](https://localhost:4502/)

* Connectez-vous avec les privilèges d’administrateur et accédez à **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**.

* Sélectionnez **Créer**.

### Étape 1 : Modèle de site {#step-site-template}

![modèle de site d&#39;activation](assets/enablement-site-template.png)

À l’étape **Modèle de site**, saisissez un titre, une description, le nom de l’URL, puis sélectionnez un modèle de site de communauté, par exemple :

* **Titre du site de la communauté**: `Enablement Tutorial`.

* **Description du site de la communauté**: `A site for enabling the community to learn.`

* **Racine du site de la communauté** : (laissez vide pour la racine par défaut  `/content/sites`)

* **Configurations du cloud** : (laissez ce champ vide si aucune configuration de cloud n’est spécifiée) fournissez le chemin d’accès aux configurations de cloud spécifiées.
* **Langue de base du site de la communauté** : (laissez intacte pour une seule langue : (anglais) utilisez la liste déroulante pour sélectionner une  *ou* plusieurs langues de base parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site communautaire sera créé pour chaque langue ajoutée et existera dans le même dossier de site, conformément aux bonnes pratiques décrites dans la section [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md). La page racine de chaque site contiendra une page enfant nommée par le code de langue de l’une des langues sélectionnées, comme &quot;en&quot; pour l’anglais ou &quot;fr&quot; pour le français.

* **Nom du site de la communauté**: `enable`

   * L’URL initiale s’affiche sous le nom du site de la communauté.
   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;
      *Par exemple*, https://localhost:4502/content/sites/  `enable/en.html`

* **Modèle de site de référence** : Menu déroulant pour choisir  `Reference Structured Learning Site Template`

Sélectionnez **Suivant**.

### Étape 2 : Conception {#step-design}

L’étape de conception est présentée dans deux sections pour sélectionner le thème et la bannière de marque :

#### THÈME DU SITE COMMUNAUTAIRE {#community-site-theme}

Sélectionnez le style à appliquer au modèle. Lorsqu’il est sélectionné, le thème est recouvert d’une coche.

#### MARQUE DU SITE COMMUNAUTAIRE {#community-site-branding}

(Facultatif) Téléchargez une image de bannière à afficher sur les pages du site. La bannière est épinglée sur le bord gauche du navigateur, entre l’en-tête du site de la communauté et le menu (liens de navigation). La hauteur de la bannière est recadrée à 120 pixels. Il n’existe aucun redimensionnement de la bannière pour s’adapter à la largeur du navigateur et à la hauteur de 120 pixels.

![site-branding1](assets/site-branding1.png)

![site-branding2](assets/site-branding2.png)

Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

À l’étape Paramètres , avant de sélectionner `Next`, vous pouvez observer que sept sections donnent accès aux configurations impliquant la gestion des utilisateurs, le balisage, les rôles, la modération, les analyses, la traduction et l’activation.

#### GESTION DES UTILISATEURS {#user-management}

Il est recommandé que les [communautés d’activation](/help/communities/overview.md#enablement-community) soient privées.

Un site communautaire est privé lorsque les visiteurs anonymes du site se voient refuser l’accès, qu’ils ne s’enregistrent pas eux-mêmes et qu’ils ne peuvent pas utiliser la connexion sociale.

Vérifiez que la plupart des cases à cocher sont désélectionnées pour [Gestion utilisateur](/help/communities/sites-console.md#user-management) :

* N’autorisez PAS les visiteurs du site à s’inscrire eux-mêmes.
* N’autorisez PAS les visiteurs anonymes du site à afficher le site.
* Facultatif : autoriser ou non la messagerie parmi les membres de la communauté.
* N’autorisez PAS la connexion avec Facebook.
* N’autorisez PAS la connexion avec Twitter.

![user-mgmt](assets/user-mgmt.png)

#### Balisage {#tagging}

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant AEM espaces de noms précédemment définis via la [console Balisage](/help/sites-administering/tags.md#tagging-console) (tels que l’ [espace de noms du tutoriel](/help/communities/enablement-setup.md#create-tutorial-tags)).

De plus, la sélection des espaces de noms de balise pour le site de la communauté limite la sélection présentée lors de la définition de catalogues et de ressources d’activation. Voir [Balisage des ressources d’activation](/help/communities/tag-resources.md) pour obtenir des informations importantes.

Il est facile de trouver des espaces de noms à l’aide d’une recherche par type. Par exemple,

* Type `tut`
* Sélectionner `Tutorial`

![activation-tagging](assets/enablement-tagging.png)

### RÔLES {#roles}

[Les ](/help/communities/users.md) rôles des membres de la communauté sont attribués via les paramètres de la section Rôles .

Pour permettre à un membre (ou à un groupe de membres) d’expérimenter le site en tant que responsable de la communauté, utilisez la recherche anticipée et sélectionnez le nom du membre ou du groupe dans les options de la liste déroulante.

Par exemple,

* Type `q`
* Sélectionnez [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Le ](/help/communities/deploy-communities.md#tunnel-service-on-author) service Tunnel permet de sélectionner des membres et des groupes existants uniquement dans l’environnement de publication.

![rôles d’activation](assets/site-admin.png)

#### MODÉRATION {#moderation}

Acceptez les paramètres globaux par défaut pour la [modération](/help/communities/sites-console.md#moderation) contenu généré par l’utilisateur (UGC).

![modération1](assets/moderation1.png)

#### ANALYTICS {#analytics}

Dans la liste déroulante, sélectionnez la structure de service cloud Analytics configurée pour ce site de communauté.

La sélection vue dans la capture d’écran, `Communities`, est l’exemple de structure de la [documentation de configuration.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![analyses](assets/analytics.png)

#### TRADUCTION {#translation}

Les [paramètres de traduction](/help/communities/sites-console.md#translation) indiquent si le contenu généré par l’utilisateur peut être traduit ou non et dans quelle langue, le cas échéant.

* Cochez **Autoriser la traduction automatique**
* Utiliser les paramètres par défaut

![traduction](assets/translation.png)

#### ACTIVATION {#enablement}

Pour une communauté d’activation, il est nécessaire d’identifier un ou plusieurs responsables d’activation de la communauté.

* **Gestionnaires d’activation**
 (requis) Membres de 
`Community Enablement Managers` sont disponibles pour être sélectionnés afin de gérer ce site de communauté.

   * Type `s`
   * Sélectionner `Sirius Nilson`

* **ID d’organisation de Marketing Cloud**
 (facultatif) ID d’un compte Adobe Analytics nécessaire lors de l’inclusion d’ [Analyses de pulsation ](/help/communities/analytics.md#video-heartbeat-analytics) vidéo dans les rapports d’activation.

![activation](assets/enablement.png)

Sélectionnez **Suivant**.

### Étape 4 : Créer un site de communauté {#step-create-community-site}

Sélectionnez **Créer.**

![aperçu](assets/preview.png)

Une fois le processus terminé, le dossier du nouveau site s’affiche dans la console Communautés > Sites .

![enablementsitecreated](assets/enablementsitecreated.png)

### Publier le nouveau site de la communauté {#publish-the-new-community-site}

Le site créé doit être géré à partir de la console Communautés - Sites , à partir de laquelle de nouveaux sites peuvent être créés.

Après avoir sélectionné le dossier du site de la communauté, pointez sur l’icône du site pour afficher quatre icônes d’action :

![siteactionicons](assets/siteactionicons.png)

Lorsque vous sélectionnez l’icône représentant des points de suspension (icône Autres actions), les options Exporter le site et Supprimer le site s’affichent.

![siteactionsnew](assets/siteactionsnew.png)

De gauche à droite, ils sont :

* **Ouvrir le site**

   Sélectionnez l’icône en forme de crayon pour ouvrir le site de la communauté en mode d’édition de création, afin d’ajouter et/ou de configurer des composants de page.

* **Modifier le site**

   Sélectionnez l’icône Propriétés pour ouvrir le site de la communauté afin de modifier les propriétés, comme le titre ou pour modifier le thème.

* **Publier le site**

   Sélectionnez l’icône du monde pour publier le site de la communauté (à localhost:4503 par défaut).

* **Exporter le site**

   Sélectionnez l’icône d’exportation pour créer un package du site de la communauté qui est stocké dans [gestionnaire de packages](/help/sites-administering/package-manager.md) et téléchargé.
Notez que le contenu généré par l’utilisateur n’est pas inclus dans le module du site.

* **Supprimer le site**

   Pour supprimer le site de la communauté, cliquez sur l’icône Supprimer le site qui s’affiche lorsque vous placez le pointeur de la souris sur le site dans la console du site Communities. Cette action supprime tous les éléments associés au site, tels que le contenu créé par l’utilisateur, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

   ![activer les iteactions](assets/enablesiteactions.png)

#### Sélectionnez Publier {#select-publish}

Sélectionnez l’icône mondiale pour publier le site de la communauté.

![publish-site](assets/publish-site.png)

Il y aura une indication que le site a été publié.

![site-publish](assets/site-published.png)

## Utilisateurs de la communauté et groupes d’utilisateurs {#community-users-user-groups}

### Remarquez les nouveaux groupes d’utilisateurs de la communauté {#notice-new-community-user-groups}

En plus du nouveau site de la communauté, de nouveaux groupes d’utilisateurs sont créés, qui disposent des autorisations appropriées pour diverses fonctions administratives. Pour plus d’informations, voir [Groupes d’utilisateurs pour les sites de la communauté](/help/communities/users.md#usergroupsforcommunitysites).

Pour ce nouveau site de communauté, étant donné le nom du site &quot;activer&quot; à l’étape 1, les nouveaux groupes d’utilisateurs qui existent dans l’environnement de publication peuvent être affichés à partir de la [console Membres et groupes de communautés](/help/communities/members.md#groups-console) :

![community_usergroup](assets/community_usergroup.png)

### Affecter des membres au groupe d’activation de la communauté {#assign-members-to-community-enable-members-group}

Sur l’instance de création, avec le service de tunnel activé, il est possible d’affecter les [utilisateurs créés lors de la configuration initiale](/help/communities/enablement-setup.md#publishcreateenablementmembers) au groupe Membres de la communauté pour le site de communauté nouvellement créé.

À l’aide de la console Groupes de communautés , les membres peuvent être ajoutés individuellement ou par le biais de l’appartenance à un groupe.

Dans cet exemple, le groupe `Community Ski Class` est ajouté en tant que membre du groupe `Community Enable Members` ainsi que membre `Quinn Harper`.

* Accédez à la console **Communautés, Groupes**
* Sélectionnez le groupe *Communauté Enable Members*
* Saisissez &quot;ski&quot; dans la zone de recherche **Ajouter des membres au groupe**
* Sélectionnez *Classe de ski communautaire* (groupe d’apprenants).
* Saisissez &quot;quinn&quot; dans la zone de recherche.
* Sélectionnez *Quinn Harper* (contact avec la ressource d’activation).

* Sélectionnez **Enregistrer**

![edit-group-settings](assets/edit-group-settings.png)

## Configurations sur la publication {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### Configurer pour l’erreur d’authentification {#configure-for-authentication-error}

Une fois qu’un site a été configuré et envoyé pour publication, [configurez le mappage de connexion](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) sur l’instance de publication. L’avantage est que lorsque les informations de connexion ne sont pas correctement saisies, l’erreur d’authentification réaffiche la page de connexion du site de la communauté avec un message d’erreur.

Ajoutez une balise `Login Page Mapping` comme suit :

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Facultatif) Modifiez la page d’accueil par défaut {#optional-change-the-default-home-page}

Lorsque vous utilisez le site de publication à des fins de démonstration, il peut s’avérer utile de remplacer la page d’accueil par défaut par le nouveau site.

Pour ce faire, il est nécessaire d’utiliser [CRX|DE](https://localhost:4503/crx/de) Lite afin de modifier la table [mapping de ressources](/help/sites-deploying/resource-mapping.md) lors de la publication.

Pour commencer :

1. Lors de la publication, accédez à CRXDE et connectez-vous avec des privilèges d’administrateur.

   * Par exemple, accédez à [https://localhost:4503/crx/de](https://localhost:4503/crx/de) et connectez-vous avec `admin/admin`.

1. Dans le navigateur du projet, développez `/etc/map`
1. Sélectionnez le noeud `http`

   * Sélectionnez **Créer un noeud**

      * **** Namelocalhost.4503

         (do *not* use &#39;:&#39;)

      * **** [Type:Mappage](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Avec le noeud `localhost.4503` nouvellement créé sélectionné

   * Ajouter une propriété

      * **Nom** sling:match
      * **** TypeString
      * **Valeur** localhost.4503/$

   (doit se terminer par &quot;$&quot; char)

   * Ajouter une propriété

      * **Nom** sling:internalRedirect
      * **** TypeString
      * **Valeur** /content/sites/enable/en.html


1. Sélectionnez **Enregistrer tout**.
1. (Facultatif) Supprimer l’historique de navigation
1. Accédez à https://localhost:4503/

   * Arrivez à l’adresse https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Pour le désactiver, il vous suffit de pré-ajouter la valeur de la propriété `sling:match` avec une valeur &#39;x&#39; - `xlocalhost.4503/$` - et **Enregistrer tout**.

![change-default-homepage](assets/change-default-homepage.png)

#### Dépannage : Erreur lors de l’enregistrement de la carte {#troubleshooting-error-saving-map}

Si vous ne parvenez pas à enregistrer les modifications, assurez-vous que le nom du noeud est `localhost.4503`, avec un séparateur &#39;point&#39;, et non `localhost:4503` avec un séparateur &#39;deux-points&#39;, car `localhost` n’est pas un préfixe d’espace de noms valide.

![error-map](assets/error-map.png)

#### Dépannage : Échec de la redirection {#troubleshooting-fail-to-redirect}

La valeur &#39;**$**&#39; à la fin de l’expression régulière `sling:match` est essentielle, de sorte que seul `https://localhost:4503/` est mappé exactement. Dans le cas contraire, la valeur de redirection est précédée de tout chemin d’accès pouvant exister après server:port dans l’URL. Par conséquent, lorsque AEM tente de rediriger vers la page de connexion, elle échoue.

## Modification du site de la communauté {#modifying-the-community-site}

Une fois le site créé, les auteurs peuvent utiliser l’[icône Ouvrir le site](/help/communities/sites-console.md#authoring-site-content) pour exécuter des activités de création d’AEM standard.

En outre, les administrateurs peuvent utiliser l’[icône Modifier le site](/help/communities/sites-console.md#modifying-site-properties) pour modifier les propriétés du site, telles que le titre.

Après toute modification, n’oubliez pas de **Enregistrer** et de re-**Publier** le site.

>[!NOTE]
>
>Si vous ne connaissez pas l’AEM, consultez la documentation sur la [gestion de base](/help/sites-authoring/basic-handling.md) et un [guide rapide pour créer des pages](/help/sites-authoring/qg-page-authoring.md).

### Ajout d’un catalogue {#add-a-catalog}

Le modèle de site de la communauté choisi pour ce site de la communauté doit contenir la fonctionnalité de catalogue.

Dans le cas contraire, la fonction de catalogue peut facilement être ajoutée. Cela permet aux autres membres de la communauté, qui ne sont pas affectés à des ressources d’activation ou à un parcours d’apprentissage, de sélectionner des ressources d’activation dans un catalogue.

Si la structure du site contient déjà la fonction de catalogue, son Titre peut être modifié.

Pour modifier la structure du site, accédez à la console **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**, ouvrez le dossier `enable` et sélectionnez l’icône **Modifier le site** pour accéder aux propriétés de `Enablement Tutorial`.

Sélectionnez le panneau STRUCTURE pour ajouter un catalogue ou modifier un catalogue existant :

* **Titre**: `Ski Catalog`

* **URL**: `catalog`

* **Sélectionner tous les espaces de noms** : laissez comme valeur par défaut.

* Sélectionnez **Enregistrer**.

![modify-site-structure](assets/modify-site-structure.png)

Utilisez l’icône Position pour déplacer la fonction Catalog vers la seconde position, après les affectations.

![move-catalog-func](assets/move-catalog-func.png)

Sélectionnez **Enregistrer** dans le coin supérieur droit pour enregistrer les modifications apportées au site de la communauté.

Ensuite, re-**Publiez** le site.
