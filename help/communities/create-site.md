---
title: Création d’un site de communauté
seo-title: Author a New Community Site
description: Création d’un site AEM Communities
seo-description: How to author a new AEM Communities site
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 3%

---

# Création d’un site de communauté{#author-a-new-community-site}

## Création d’un site de communauté {#create-a-community-site}

Utilisez l’instance d’auteur pour créer un site de communauté. Sur l’instance d’auteur AEM :

1. Connectez-vous avec les privilèges d’administrateur.
1. Dans la navigation globale, accédez à **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**.

La console Sites de communautés fournit un assistant pour vous guider tout au long des étapes de création d’un site de communauté. Il est possible de passer à la `Next` étape ou `Back` à l’étape précédente avant de valider le site à l’étape finale.

Pour commencer à créer un site communautaire :

* Sélectionnez la `Create` bouton .

![createccommunity.site](assets/createcommunitysite.png)

### Étape 1 : Modèle de site {#step-site-template}

![modèle pour créer un site](assets/create-site.png)

Sur le [Étape Modèle de site](/help/communities/sites-console.md#step2013asitetemplate), saisissez un titre, une description, le nom de l’URL, puis sélectionnez un modèle de site de communauté, par exemple :

* **Titre du site de la communauté**: `Getting Started Tutorial`
* **Description du site de la communauté**: `A site for engaging with the community.`
* **Racine du site de la communauté**: (laissez vide pour la racine par défaut) `/content/sites`)
* **Configurations du cloud**: (laissez ce champ vide si aucune configuration de cloud n’est spécifiée) fournissez le chemin d’accès aux configurations de cloud spécifiées.
* **Langue de base du site de la communauté**: (laissez intacte pour une seule langue : en anglais) utilisez la liste déroulante pour en choisir une. *ou plus* Les langues de base disponibles sont l’allemand, l’italien, le français, le japonais, l’espagnol, le portugais (Brésil), le chinois (traditionnel) et le chinois (simplifié). Un site de communauté sera créé pour chaque langue ajoutée et existera dans le même dossier de site, conformément aux bonnes pratiques décrites dans la section [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md). La page racine de chaque site contiendra une page enfant nommée par le code de langue de l’une des langues sélectionnées, comme &quot;en&quot; pour l’anglais ou &quot;fr&quot; pour le français.

* **Nom du site de la communauté**: engager

   * Vérifiez deux fois le nom, car il n’est pas facilement modifié une fois le site créé.
   * L’URL initiale s’affiche sous le nom du site de la communauté.
   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;
   * *Par exemple*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modèle**: Menu déroulant pour choisir `Reference Site`

* Sélectionnez **Suivant**.

### Étape 2 : Conception {#step-design}

L’étape de conception est présentée dans deux sections pour sélectionner le thème et la bannière de marque :

#### THÈME DU SITE COMMUNAUTAIRE {#community-site-theme}

Sélectionnez le style à appliquer au modèle. Lorsqu’il est sélectionné, le thème est coché.

#### MARQUE DU SITE DE LA COMMUNAUTÉ {#community-site-branding}

(Facultatif) Téléchargez une image de bannière à afficher sur les pages du site. La bannière est épinglée sur le bord gauche du navigateur, entre l’en-tête du site de la communauté et les liens de navigation. La hauteur de la bannière est recadrée à 120 pixels. Il n’existe aucun redimensionnement de la bannière pour s’adapter à la largeur du navigateur et à la hauteur de 120 pixels.

![communauté-site-branding](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

À l’étape Paramètres , avant de sélectionner `Next`, notez que sept sections donnent accès aux configurations impliquant la gestion des utilisateurs, le balisage, la modération, la gestion des groupes, l’analyse et la traduction.

#### User Management {#user-management}

Cochez toutes les cases pour [Gestion des utilisateurs](/help/communities/sites-console.md#user-management)

* Pour autoriser les visiteurs du site à s’inscrire automatiquement
* Pour permettre aux visiteurs du site d’afficher le site sans se connecter
* Pour permettre aux membres d’envoyer et de recevoir des messages d’autres membres de la communauté
* Pour autoriser la connexion à Facebook au lieu d’enregistrer et de créer un profil
* Pour autoriser la connexion à Twitter au lieu d’enregistrer et de créer un profil

>[!NOTE]
>
>Pour un environnement de production, il est nécessaire de créer des applications Facebook et Twitter personnalisées. Voir [Connexion aux réseaux sociaux avec Facebook et Twitter](/help/communities/social-login.md).

![paramètres du site de communauté](assets/site-settings.png)

#### BALISAGE {#tagging}

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant AEM espaces de noms précédemment définis via la variable [Console Balisage](/help/sites-administering/tags.md#tagging-console) (par exemple, [Espace de noms du tutoriel](/help/communities/setup.md#create-tutorial-tags)).

Il est facile de trouver des espaces de noms à l’aide d’une recherche par type. Par exemple,

* Type `tut`
* Sélectionner `Tutorial`

![balisage](assets/tagging.png)

#### RÔLES {#roles}

[Rôles des membres de la communauté](/help/communities/users.md) sont affectées via les paramètres de la section Rôles .

Pour permettre à un membre (ou à un groupe de membres) d’expérimenter le site en tant que responsable de la communauté, utilisez la recherche anticipée et sélectionnez le nom du membre ou du groupe dans les options de la liste déroulante.

Par exemple,

* Type `q`
* Sélection de Quinn Harper

>[!NOTE]
>
>[Service Tunnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) permet la sélection de membres et de groupes existants uniquement dans l’environnement de publication.

![rôles utilisateur du nouveau site](assets/site-admin-1.png)

#### MODÉRATION {#moderation}

Acceptez les paramètres globaux par défaut pour [modération](/help/communities/sites-console.md#moderation) contenu généré par l’utilisateur.

![modération](assets/moderation1.png)

#### ANALYTICS {#analytics}

Si Adobe Analytics est sous licence et qu’un service cloud et une structure Analytics ont été configurés, il est possible d’activer Analytics et de sélectionner la structure.

Voir [Configuration d’Analytics pour les fonctionnalités des communautés](/help/communities/analytics.md).

![analyses](assets/analytics.png)

#### TRADUCTION {#translation}

Le [Paramètres de traduction](/help/communities/sites-console.md#translation) indiquez la langue de base du site, ainsi que si le contenu généré par l’utilisateur peut être traduit ou non et dans quelle langue, le cas échéant.

* Vérifier **Autoriser la traduction automatique**
* Laissez les langues par défaut sélectionnées pour la traduction par le service de traduction automatique par défaut.
* Laissez le fournisseur de traduction et la configuration par défaut
* Il n’est pas nécessaire d’avoir un magasin global car il n’y a pas de copies de langue
* Sélectionner **Traduire toute la page**
* Laissez l’option de persistance par défaut

![translation-settings](assets/translation-settings.png)

### Étape 4 : Créer un site de communautés {#step-create-communities-site}

Sélectionnez **Créer.**

![create-site](assets/create-site2.png)

Une fois le processus terminé, le dossier du nouveau site s’affiche dans la console Communautés - Sites .

![communitiessitesconsole](assets/communitiessitesconsole.png)

## Publication du site de la communauté {#publish-the-community-site}

Le site créé doit être géré à partir de la console Communautés - Sites , à partir de laquelle de nouveaux sites peuvent être créés.

Après avoir sélectionné le dossier du site de la communauté pour l’ouvrir, survolez l’icône du site avec la souris afin que quatre icônes d’action s’affichent :

![siteactionicons-1](assets/siteactionicons-1.png)

Lorsque vous sélectionnez la quatrième icône représentant des points de suspension (Autres actions), les options Exporter le site et Supprimer le site s’affichent.

![siteactionsnew-1](assets/siteactionsnew-1.png)

De gauche à droite, ils sont :

* **Ouvrir le site**

   Sélectionnez l’icône en forme de crayon pour ouvrir le site de la communauté en mode d’édition de création, pour ajouter et/ou configurer des composants de page.

* **Modifier le site**

   Sélectionnez l’icône Propriétés pour ouvrir le site de la communauté afin de modifier les propriétés, telles que le titre ou pour modifier le thème.

* **Publier le site**

   Sélectionnez l’icône du monde pour publier le site de la communauté (par exemple, si votre serveur de publication s’exécute sur votre ordinateur local, puis sur localhost:4503 par défaut).

* **Exporter le site**

   Sélectionnez l’icône d’exportation pour créer un package du site de la communauté qui est stocké tous les deux dans [gestionnaire de modules](/help/sites-administering/package-manager.md) et téléchargés.
Notez que le contenu généré par l’utilisateur n’est pas inclus dans le module du site.

* **Supprimer le site**

   Sélectionner l’icône Supprimer pour supprimer le site de la communauté de l’intérieur **[!UICONTROL Communautés > Console Sites]**. Cette action supprime tous les éléments associés au site, tels que le contenu créé par l’utilisateur, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Si vous n’utilisez pas le port par défaut 4503 pour l’instance de publication, modifiez l’agent de réplication par défaut pour définir le numéro de port sur la valeur correcte.
>
>Sur l’instance d’auteur, dans le menu principal :
>
>1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]** .
>1. Sélectionner **[!UICONTROL Agents sur l’auteur]**.
>1. Sélectionner **[!UICONTROL Agent par défaut (publication)]**.
>1. En regard de **[!UICONTROL Paramètres]**, sélectionnez **[!UICONTROL Modifier]**.
>1. Dans la boîte de dialogue contextuelle Paramètres de l’agent, sélectionnez **[!UICONTROL Transport]** .
>1. Dans l’URI, remplacez le numéro de port, 4503, par le numéro de port souhaité. Par exemple, pour utiliser le port 6103 : https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Sélectionnez **[!UICONTROL OK]**.
>1. (Facultatif) Sélectionnez **[!UICONTROL Effacer]** ou **[!UICONTROL Forcer une nouvelle tentative]** pour réinitialiser la file d’attente de réplication.


### Sélectionnez Publier . {#select-publish}

Une fois que le serveur de publication est en cours d’exécution, sélectionnez l’icône mondiale pour publier le site de la communauté.

![publish-site](assets/publish-site.png)

Une fois le site de la communauté publié, un message s’affiche brièvement &quot;Site publié&quot;.

### Nouveaux groupes d’utilisateurs de la communauté {#new-community-user-groups}

En plus du nouveau site de la communauté, de nouveaux groupes d’utilisateurs sont créés, qui disposent des autorisations appropriées pour diverses fonctions administratives. Pour plus d’informations, rendez-vous sur [Groupes d’utilisateurs pour les sites de la communauté](/help/communities/users.md#usergroupsforcommunitysites).

Pour ce nouveau site de communauté, étant donné le nom &quot;s’engager&quot; du site à l’étape 1, les quatre nouveaux groupes d’utilisateurs peuvent être vus depuis le [Console Groupes](/help/communities/members.md) (navigation globale) : Communautés, groupes) :

* Responsable de la communauté Community Engage
* Administrateurs du groupe d’interaction communautaire
* Membres de la communauté
* Modérateurs d’engagement de la communauté
* Membres privilégiés de la communauté Engage
* Interagir de la communauté Gestionnaire de contenu du site

Notez que [Aaron McDonald](/help/communities/tutorials.md#demo-users) est un membre de

* Responsable de la communauté Community Engage
* Modérateurs d’engagement de la communauté
* Membres de la communauté Engage (indirectement en tant que membre du groupe Modérateurs)

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engager](assets/engage.png)

## Configuration d’une erreur d’authentification {#configure-for-authentication-error}

Une fois qu’un site a été configuré et envoyé pour publication, [configuration du mapping de connexion](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) sur l’instance de publication. L’avantage est que lorsque les informations de connexion ne sont pas correctement saisies, l’erreur d’authentification réaffiche la page de connexion du site de la communauté avec un message d’erreur.

Ajouter un `Login Page Mapping` as

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Étapes facultatives {#optional-steps}

### Modification de la page d’accueil par défaut {#change-the-default-home-page}

Lorsque vous utilisez le site de publication à des fins de démonstration, il peut s’avérer utile de remplacer la page d’accueil par défaut par le nouveau site.

Pour ce faire, utilisez [CRXDE](https://localhost:4503/crx/de) Pour modifier le [mapping des ressources](/help/sites-deploying/resource-mapping.md) sur publication.

Pour commencer :

1. Sur l’instance de publication, connectez-vous avec les privilèges d’administrateur.
1. Accédez à [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. Dans l’explorateur de projets, développez `/etc/map.`
1. Sélectionnez la `http` node:

   * Sélectionner **Créez un noeud :**

      * **Nom** localhost.4503 (do *not* use &#39;:&#39;)

      * **Type** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Avec `localhost.4503` noeud sélectionné :

   * Ajouter une propriété:

   * **Nom** sling:match
      * **Type** Chaîne
      * **Valeur** localhost.4503/$ (doit se terminer par &#39;$&#39; char)
   * Ajouter une propriété:

      * **Nom** sling:internalRedirect
      * **Type** Chaîne
      * **Valeur** /content/sites/engage/en.html


1. Sélectionnez **Enregistrer tout.**
1. (Facultatif) Supprimez l’historique de navigation.
1. Accédez à https://localhost:4503/.

   * Arrivez à l’adresse https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Pour désactiver, il vous suffit de préfixer la variable `sling:match` valeur de propriété avec un &quot;x&quot; - `xlocalhost.4503/$` - et **Enregistrer tout**.

![optional-steps](assets/optional-steps.png)

#### Dépannage : Erreur lors de l’enregistrement de la carte {#troubleshooting-error-saving-map}

Si vous ne parvenez pas à enregistrer les modifications, assurez-vous que le nom du noeud est `localhost.4503`, avec un séparateur &quot;point&quot;, et non `localhost:4503` avec un séparateur &quot;deux-points&quot;, comme `localhost`n’est pas un préfixe d’espace de noms valide.

![error-message](assets/error-message.png)

#### Dépannage : Échec de la redirection {#troubleshooting-fail-to-redirect}

Le &quot;**$**&#39; à la fin de l’expression régulière `sling:match`chaîne est cruciale, de sorte que uniquement exactement `https://localhost:4503/` est mappée, sinon la valeur de redirection est précédée de n’importe quel chemin d’accès pouvant exister après server:port dans l’URL. Par conséquent, lorsque AEM tente de rediriger vers la page de connexion, elle échoue.

### Modification du site {#modify-the-site}

Une fois le site créé, les auteurs peuvent utiliser la variable [Icône Ouvrir le site](/help/communities/sites-console.md#authoring-site-content) pour exécuter des activités de création d’AEM standard.

En outre, les administrateurs peuvent utiliser la variable [Icône Modifier le site](/help/communities/sites-console.md#modifying-site-properties) pour modifier les propriétés du site, telles que le titre.

Après toute modification, pensez à **Enregistrer** et re-**Publier** le site.

>[!NOTE]
>
>Si vous ne connaissez pas AEM, consultez la documentation sur [gestion de base](/help/sites-authoring/basic-handling.md) et un [guide rapide pour la création de pages](/help/sites-authoring/qg-page-authoring.md).
