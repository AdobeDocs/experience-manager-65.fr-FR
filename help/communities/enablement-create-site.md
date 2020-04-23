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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Création d’un nouveau site communautaire pour l’activation {#author-a-new-community-site-for-enablement}

## Créer un site de communauté {#create-community-site}

[La création](/help/communities/sites-console.md) d’un site de communauté utilise un assistant qui vous guide tout au long des étapes de création d’un site de communauté. Il est possible de passer à l&#39; `Next` étape ou `Back` à l&#39;étape précédente avant de valider le site dans l&#39;étape finale.

Pour commencer à créer un nouveau site communautaire :

Utilisation de l’instance [d’auteur](https://localhost:4502/)

* Connexion avec droits d’administrateur
* Accédez à **[!UICONTROL Communautés > Sites]**

* Sélectionnez **Créer**

### Étape 1 : Modèle de site {#step-site-template}

![modèle de site d&#39;activation](assets/enablement-site-template.png)

A l’étape Modèle **de** site, saisissez un titre, une description, le nom de l’URL, puis sélectionnez un modèle de site communautaire, par exemple :

* **Titre du site de la communauté**: `Enablement Tutorial`

* **Description du site de la communauté**: `A site for enabling the community to learn.`

* **Racine** du site de la communauté : (laisser vide pour la racine par défaut `/content/sites`)

* **Configurations** du cloud : (laissez vide si aucune configuration de cloud n’est spécifiée) fournissez le chemin d’accès aux configurations de cloud spécifiées.
* **Langue** de base du site de la communauté : (laissez intacte pour la langue unique : anglais) utilisez la liste déroulante pour choisir une *ou plusieurs* langues de base parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site communautaire sera créé pour chaque langue ajoutée et existera dans le même dossier de site, conformément aux bonnes pratiques décrites dans la section [Traduction de contenu pour les sites](/help/sites-administering/translation.md)multilingues. La page racine de chaque site contiendra une page enfant nommée par le code de langue de l&#39;une des langues sélectionnées, comme &quot;en&quot; pour l&#39;anglais ou &quot;fr&quot; pour le français.

* **Nom du site de la communauté**: `enable`

   * L’URL initiale s’affichera sous le nom du site de la communauté.
   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;
      *Par exemple*, https://localhost:4502/content/sites/ `enable/en.html`

* **Modèle** de site de référence : tirez vers le bas pour choisir `Reference Structured Learning Site Template`

Sélectionnez **Suivant**

### Étape 2 : Conception {#step-design}

L’étape de conception est présentée en deux sections pour la sélection du thème et de la bannière de marque :

#### COMMUNITY SITE THEME {#community-site-theme}

Sélectionnez le style à appliquer au modèle. Une fois sélectionné, le thème sera superposé avec une coche.

#### COMMUNITY SITE BRANDING {#community-site-branding}

(Facultatif) Téléchargez une image de bannière à afficher sur les pages du site. La bannière est épinglée sur le bord gauche du navigateur, entre l’en-tête du site de la communauté et le menu (liens de navigation). La hauteur de la bannière est rognée à 120 pixels. La bannière n’est pas redimensionnée pour s’adapter à la largeur du navigateur et à la hauteur de 120 pixels.

![chlimage_1-2](assets/chlimage_1-2.png) ![chlimage_1](assets/chlimage_1.jpeg)

Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

À l’étape Paramètres, avant de sélectionner `Next`, notez que sept sections donnent accès à des configurations impliquant la gestion des utilisateurs, le balisage, les rôles, la modération, les analyses, la traduction et l’activation.

#### USER MANAGEMENT {#user-management}

Il est recommandé que les communautés [d’](/help/communities/overview.md#enablement-community) activation soient privées.

Un site communautaire est privé lorsque des anonymes du site se voient refuser l’accès, peuvent ne pas s’enregistrer eux-mêmes et ne pas utiliser la connexion sociale.

Vérifiez que la plupart des cases à cocher sont désélectionnées pour [User Management](/help/communities/sites-console.md#user-management) :

* NE PAS autoriser les du site à s&#39;inscrire
* N&#39;autorisez PAS les anonymes du site à
* Facultatif pour autoriser ou non la messagerie entre les membres de la communauté
* Ne PAS autoriser la connexion à Facebook
* Ne PAS autoriser la connexion avec Twitter

![chlimage_1-3](assets/chlimage_1-3.png)

#### TAGGING {#tagging}

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant AEM   précédemment définies dans la console [de](/help/sites-administering/tags.md#tagging-console) balisage (par exemple, le [de  du](/help/communities/enablement-setup.md#create-tutorial-tags)didacticiel).

En outre, la sélection de la balise   pour le site de la communauté limite la sélection présentée lors de la définition de catalogues et de ressources d’activation. Voir Ressources [d’activation du](/help/communities/tag-resources.md) balisage pour obtenir des informations importantes.

Trouver   de est facile avec la recherche par type. Par exemple :

* Type `tut`
* Sélectionner `Tutorial`

![chlimage_1-4](assets/chlimage_1-4.png)

### ROLES {#roles}

[Les rôles](/help/communities/users.md) des membres de la communauté sont attribués via les paramètres de la section Rôles.

Pour permettre à un membre de la communauté (ou à un groupe de membres) de découvrir le site en tant que gestionnaire de la communauté, utilisez la recherche par type et sélectionnez le nom du membre ou du groupe dans les options de la liste déroulante.

Par exemple :

* Type `q`
* Sélectionner [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Le service](/help/communities/deploy-communities.md#tunnel-service-on-author) Tunnel permet de sélectionner les membres et les groupes existants uniquement dans le  de publication .

![rôles d’activation](assets/site-admin.png)

#### MODERATION {#moderation}

Acceptez les paramètres généraux par défaut pour la [modération](/help/communities/sites-console.md#moderation) du contenu généré par l’utilisateur (UGC).

![chlimage_1-5](assets/chlimage_1-5.png)

#### ANALYTICS {#analytics}

Dans la liste déroulante, sélectionnez la structure de service cloud Analytics configurée pour ce site de la communauté.

La sélection affichée dans la capture d’écran `Communities`, est l’exemple de structure de la documentation de [configuration.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![chlimage_1-6](assets/chlimage_1-6.png)

#### TRANSLATION {#translation}

Les paramètres [de](/help/communities/sites-console.md#translation) traduction indiquent si l’UGC peut être traduit ou non et dans quelle langue, le cas échéant.

* Cocher **Autoriser la traduction automatique**
* Utiliser les paramètres par défaut

![chlimage_1-7](assets/chlimage_1-7.png)

#### ENABLEMENT {#enablement}

Pour une communauté d’activation, il est nécessaire d’identifier un ou plusieurs gestionnaires d’activation de la communauté.

* **Gestionnaires** d&#39;activation (requis) Les membres du `Community Enablement Managers` groupe peuvent être sélectionnés pour gérer ce site de la communauté.

   * Type `s`
   * Sélectionner `Sirius Nilson`

* **Identifiant** d’organisation Marketing Cloud (facultatif) Identifiant d’un compte Adobe Analytics nécessaire lors de l’inclusion d’Analyses [de pulsation](/help/communities/analytics.md#video-heartbeat-analytics) vidéo dans le  d’activation.

![chlimage_1-8](assets/chlimage_1-8.png)

Sélectionnez **Suivant**.

### Étape 4 : Créer un site communautaire {#step-create-community-site}

Sélectionnez **Créer.**

![chlimage_1-9](assets/chlimage_1-9.png)

Une fois le processus terminé, le dossier du nouveau site s’affiche dans la console Communautés > Sites.

![activationsitecréée](assets/enablementsitecreated.png)

### Publication du nouveau site de la communauté {#publish-the-new-community-site}

Le site créé doit être géré à partir de la console Communautés - Sites, la même console à partir de laquelle de nouveaux sites peuvent être créés.

Après avoir sélectionné le dossier du site de la communauté, passez la souris sur l’icône du site pour afficher quatre icônes d’action :

![siteactionicons](assets/siteactionicons.png)

Lorsque vous sélectionnez l’icône d’ellipses (icône Autres actions), les options Exporter le site et Supprimer le site s’affichent.

![siteactionsnew](assets/siteactionsnew.png)

De gauche à droite, ils sont :

* **Ouvrir le site**

   Sélectionnez l’icône représentant un crayon pour ouvrir le site de la communauté en mode d’édition de l’auteur, ajouter et/ou configurer des composants de page.

* **Modifier le site**

   Sélectionnez l’icône Propriétés pour ouvrir le site de la communauté en vue de modifier les propriétés, comme le titre ou le thème.

* **Publier le site**

   Sélectionnez l’icône du monde pour publier le site de la communauté (sur localhost:4503 par défaut).

* **Exporter le site**

   Sélectionnez l’icône d’exportation pour créer un package du site de la communauté stocké dans le gestionnaire de [packages](/help/sites-administering/package-manager.md) et téléchargé.
Notez que l’UGC n’est pas inclus dans le package du site.

* **Supprimer le site**

   Pour supprimer le site de la communauté, sélectionnez l&#39;icône Supprimer le site qui s&#39;affiche lorsque vous passez la souris sur le site dans la console du site Communautés. Cette action supprime tous les éléments associés au site, tels que l’UGC, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

![activer les itéactions](assets/enablesiteactions.png)

#### Sélectionnez Publier {#select-publish}

Sélectionnez l’icône du monde pour publier le site de la communauté.

![chlimage_1-10](assets/chlimage_1-10.png)

Il y aura une indication que le site a été publié.

![chlimage_1-11](assets/chlimage_1-11.png)

## Utilisateurs de la communauté et groupes d’utilisateurs {#community-users-user-groups}

### Avis de nouveaux groupes d’utilisateurs de la communauté {#notice-new-community-user-groups}

En plus du nouveau site de la communauté, de nouveaux groupes d’utilisateurs sont créés et disposent des autorisations appropriées pour diverses fonctions administratives. Pour plus d’informations, consultez Groupes [d’utilisateurs pour les sites](/help/communities/users.md#usergroupsforcommunitysites)de la communauté.

Pour ce nouveau site communautaire, étant donné le nom du site &quot;activer&quot; à l’étape 1, les nouveaux groupes d’utilisateurs qui existent dans le  de publication  peuvent être vus à partir de la console [Membres et groupes](/help/communities/members.md#groups-console) des communautés :

![chlimage_1-12](assets/chlimage_1-12.png)

### Affecter des membres au groupe Activer la communauté {#assign-members-to-community-enable-members-group}

Sur l’auteur, avec le service tunnel activé, il est possible d’affecter les [utilisateurs créés lors de la configuration](/help/communities/enablement-setup.md#publishcreateenablementmembers) initiale au groupe Membres de la communauté pour le nouveau site communautaire.

A l’aide de la console Groupes de communautés, les membres peuvent être ajoutés individuellement ou par le biais d’un abonnement à un groupe.

Dans cet exemple, le groupe `Community Ski Class` est ajouté en tant que membre du groupe `Community Enable Members` ainsi qu’en tant que membre `Quinn Harper`.

* Accédez à **Communautés, Console Groupes** .
* Sélectionner le groupe Activer les membres ** de la communauté
* Entrez &quot;ski&quot; dans la zone de recherche **Ajouter Membres à regrouper** .
* Sélectionner la classe *de ski* communautaire (groupe d’apprenants)
* Entrez &quot;quinn&quot; dans la zone de recherche
* Sélectionnez *Quinn Harper* (contact ressource d&#39;activation)

* Sélectionnez **Enregistrer**

![chlimage_1-13](assets/chlimage_1-13.png)

## Configurations sur la publication {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![chlimage_1-14](assets/chlimage_1-14.png)

### Erreur de configuration pour l’authentification {#configure-for-authentication-error}

Une fois qu’un site a été configuré et envoyé pour publication, [configurez le mappage](/help/communities/sites-console.md#configure-for-authentication-error) de connexion ( `Adobe Granite Login Selector Authentication Handler`) sur l’instance de publication. L’avantage est que lorsque les informations d’identification de connexion ne sont pas saisies correctement, l’erreur d’authentification affiche à nouveau la page de connexion du site de la communauté avec un message d’erreur.

Ajouter a `Login Page Mapping` comme

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Facultatif) Modification du par défaut {#optional-change-the-default-home-page}

Lorsque vous travaillez avec le site de publication à des fins de démonstration, il peut s’avérer utile de modifier le par défaut en nouveau site.

Pour ce faire, vous devez utiliser [CRX|DE](https://localhost:4503/crx/de) Lite pour modifier la table de mappage [des](/help/sites-deploying/resource-mapping.md) ressources lors de la publication.

Pour commencer

1. Lors de la publication, accédez à CRXDE et connectez-vous avec des droits d’administrateur

   * Par exemple, accédez à [https://localhost:4503/crx/de](https://localhost:4503/crx/de) et connectez-vous avec `admin/admin`

1. Dans le navigateur du projet, développez `/etc/map`
1. Sélectionner le `http` noeud

   * Sélectionner **Créer un noeud**

      * **Nom** localhost.4503

         (do *not* use &#39;:&#39;)

      * **Type** [sling:Mappage](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Avec le nouveau `localhost.4503` noeud sélectionné

   * Ajouter, propriété

      * **Nom** sling:match
      * **Chaîne de type**
      * **Valeur** localhost.4503/$
   (doit se terminer par &#39;$&#39; char)

   * Ajouter, propriété

      * **Nom** sling:internalRedirect
      * **Chaîne de type**
      * **Valeur** /content/sites/enable/en.html


1. Select **Save All**
1. (Facultatif) Supprimer l’historique de navigation
1. Accédez à https://localhost:4503/

   * Arrivée à https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Pour le désactiver, il vous suffit de pré-ajouter la valeur de la `sling:match` propriété à l’aide de &quot;x&quot; - `xlocalhost.4503/$` - et **d’enregistrer tout**.

![chlimage_1-15](assets/chlimage_1-15.png)

#### Dépannage : Erreur lors de l&#39;enregistrement de la carte {#troubleshooting-error-saving-map}

Si vous ne parvenez pas à enregistrer les modifications, veillez à ce que le nom du noeud soit `localhost.4503`, avec un séparateur de point, et non `localhost:4503` avec un séparateur de point, car `localhost` il ne s’agit pas d’un préfixe   valide.

![chlimage_1-16](assets/chlimage_1-16.png)

#### Dépannage : Echec de la redirection {#troubleshooting-fail-to-redirect}

Le paramètre &quot;**$**&quot; à la fin de la `sling:match`chaîne de classique est crucial. De ce fait, seul `https://localhost:4503/` est mappé, sinon la valeur de redirection est précédée d’un chemin d’accès qui peut exister après le paramètre server:port dans l’URL. Ainsi, lorsqu’AEM tente de rediriger vers la page de connexion, elle échoue.

## Modification du site communautaire {#modifying-the-community-site}

Une fois le site créé, les auteurs peuvent utiliser l’icône [](/help/communities/sites-console.md#authoring-site-content) Ouvrir le site pour créer   AEM standard.

En outre, les administrateurs peuvent utiliser l&#39;icône [](/help/communities/sites-console.md#modifying-site-properties) Modifier le site pour modifier les propriétés du site, comme le titre.

Après toute modification, n’oubliez pas d’ **enregistrer** et de republier **** le site.

>[!NOTE]
>
>If not familiar with AEM, view the documentation on [basic handling](/help/sites-authoring/basic-handling.md) and a [quick guide to authoring pages](/help/sites-authoring/qg-page-authoring.md).

### Ajouter d’un catalogue {#add-a-catalog}

Le modèle de site de la communauté choisi pour ce site de la communauté doit contenir la fonctionnalité de catalogue.

Dans le cas contraire, la fonction de catalogue peut être facilement ajoutée. Cela permettrait aux autres membres de la communauté, non affectés à des ressources d’activation ou à un chemin d’apprentissage, de sélectionner des ressources d’activation dans un catalogue.

Si la structure du site contient déjà la fonctionnalité de catalogue, son titre peut être modifié.

Pour modifier la structure du site, accédez à la console **Communautés, Sites** , ouvrez le `enable` dossier, puis sélectionnez l’icône **Modifier le site** pour accéder aux propriétés de `Enablement Tutorial`.

Sélectionnez le panneau STRUCTURE pour ajouter un catalogue ou modifier un catalogue existant :

* **Titre**: `Ski Catalog`

* **URL**: `catalog`

* **Sélectionner tout** de : laissez comme valeur par défaut.
* sélectionnez **Enregistrer**

![chlimage_1-17](assets/chlimage_1-17.png)

Utilisez l’icône Position pour déplacer la fonction Catalogue vers la deuxième position, après les affectations.

![chlimage_1-18](assets/chlimage_1-18.png)

Sélectionnez **Enregistrer** dans le coin supérieur droit pour enregistrer les modifications sur le site de la communauté.

Publiez à nouveau **le site** .

