---
title: Création d’un nouveau site de la communauté
seo-title: Création d’un nouveau site de la communauté
description: Comment créer un nouveau site AEM Communities
seo-description: Comment créer un nouveau site AEM Communities
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: d5f4b8a8c42df86831bb57b73949e443ec19d7ea
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 4%

---


# Création d’un nouveau site de la communauté{#author-a-new-community-site}

## Créer un site communautaire {#create-a-community-site}

Utilisez l’instance d’auteur pour créer un site communautaire. Sur l&#39;instance de AEM Author :

1. Connectez-vous avec des droits d’administrateur.
1. A partir de la navigation globale, accédez à **Navigation, Communautés, Sites.**

La console Sites des communautés fournit un assistant qui vous guide tout au long des étapes de création d&#39;un site communautaire. Il est possible de passer à l&#39; `Next` étape ou `Back` à l&#39;étape précédente avant de valider le site dans l&#39;étape finale.

Pour commencer à créer un site communautaire :

* Sélectionnez le `Create` bouton.

![createcommunitsite](assets/createcommunitysite.png)

### Étape 1 : Modèle de site {#step-site-template}

![modèle pour créer un site](assets/create-site.png)

À l’étape [Modèle de](/help/communities/sites-console.md#step2013asitetemplate)site, saisissez un titre, une description, le nom de l’URL, puis sélectionnez un modèle de site communautaire, par exemple :

* **Titre du site de la communauté**: `Getting Started Tutorial`
* **Description du site de la communauté**: `A site for engaging with the community.`
* **Racine** du site de la communauté : (laisser vide pour la racine par défaut `/content/sites`)
* **Configurations** du cloud : (laissez vide si aucune configuration de cloud n’est spécifiée) fournissez le chemin d’accès aux configurations de cloud spécifiées.
* **Langue** de base du site de la communauté : (ne pas modifier pour une seule langue : Anglais) utilisez la liste déroulante pour choisir une *ou plusieurs* langues de base parmi les langues disponibles : allemand, italien, français, japonais, espagnol, portugais (Brésil), chinois (traditionnel) et chinois (simplifié). Un site communautaire sera créé pour chaque langue ajoutée et existera dans le même dossier de site selon les meilleures pratiques décrites dans la section [Traduction de contenu pour les sites](/help/sites-administering/translation.md)multilingues. La page racine de chaque site contient une page enfant nommée par le code de langue de l&#39;une des langues sélectionnées, comme &quot;en&quot; pour l&#39;anglais ou &quot;fr&quot; pour le français.

* **Nom** du site de la communauté : engager

   * Doublon-vérifier le nom car il n&#39;est pas facilement modifié après la création du site
   * L&#39;URL initiale s&#39;affiche sous le nom du site de la communauté.
   * Pour une URL valide, ajoutez un code de langue de base + &quot;.html&quot;
   * *Par exemple*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modèle**: descendre pour choisir `Reference Site`

* Sélectionnez **Suivant**.

### Étape 2 : Conception {#step-design}

L’étape de conception est présentée en deux sections pour la sélection du thème et de la bannière de marque :

#### COMMUNITY SITE THEME {#community-site-theme}

Sélectionnez le style à appliquer au modèle. Une fois sélectionné, le thème sera superposé avec une coche.

#### COMMUNITY SITE BRANDING {#community-site-branding}

(Facultatif) Téléchargez une image de bannière pour l’afficher sur les pages du site. La bannière est épinglée sur le bord gauche du navigateur, entre l’en-tête du site de la communauté et les liens de navigation. La hauteur de la bannière est rognée à 120 pixels. Il n’existe aucun redimensionnement de la bannière pour s’adapter à la largeur du navigateur et à la hauteur de 120 pixels.

![chlimage_1-284](assets/chlimage_1-284.png)

![upload-image-site](assets/upload-image-site.png)

Sélectionnez **Suivant**.

### Étape 3 : Paramètres {#step-settings}

A l’étape Paramètres, avant de sélectionner `Next`, notez que sept sections donnent accès à des configurations impliquant la gestion des utilisateurs, le balisage, la modération, la gestion de groupe, les analyses, la traduction et l’activation.

Consultez le didacticiel [Prise en main des AEM Communities pour l’activation](/help/communities/getting-started-enablement.md) pour découvrir comment utiliser les fonctionnalités d’activation.

#### Gestion des utilisateurs {#user-management}

Cochez toutes les cases de gestion des [utilisateurs.](/help/communities/sites-console.md#user-management)

* Pour permettre aux visiteurs du site de s&#39;inscrire eux-mêmes
* Permettre aux visiteurs du site de vue sans se connecter
* Permettre aux membres d&#39;envoyer et de recevoir des messages d&#39;autres membres de la communauté
* Pour autoriser la connexion avec Facebook au lieu de l&#39;enregistrement et de la création d&#39;un profil
* Pour autoriser la connexion avec Twitter au lieu de l’enregistrement et de la création d’un profil

>[!NOTE]
>
>Pour un environnement de production, il est nécessaire de créer des applications Facebook et Twitter personnalisées. Voir Connexion [aux réseaux sociaux avec Facebook et Twitter](/help/communities/social-login.md).


![paramètres du site communautaire](assets/site-settings.png)

#### TAGGING {#tagging}

Les balises qui peuvent être appliquées au contenu de la communauté sont contrôlées en sélectionnant les espaces de nommage AEM précédemment définis dans la console [de](/help/sites-administering/tags.md#tagging-console) balisage (tel que l’espace de nommage [de](/help/communities/setup.md#create-tutorial-tags)didacticiel).

La recherche d&#39;espaces de nommage est facile avec la recherche par type. Par exemple :

* Type `tut`
* Sélectionner `Tutorial`

![chlimage_1-286](assets/chlimage_1-286.png)

#### ROLES {#roles}

[Les rôles](/help/communities/users.md) des membres de la communauté sont attribués via les paramètres de la section Rôles.

Pour permettre à un membre de la communauté (ou à un groupe de membres) de découvrir le site en tant que responsable de la communauté, utilisez la recherche par type et sélectionnez le nom du membre ou du groupe dans les options de la liste déroulante.

Par exemple :

* Type `q`
* Sélectionner [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Le service](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) Tunnel permet de sélectionner les membres et les groupes existants uniquement dans l’environnement de publication.


![rôles d’utilisateur dans le nouveau site](assets/site-admin-1.png)

#### MODERATION {#moderation}

Acceptez les paramètres globaux par défaut pour la [modération](/help/communities/sites-console.md#moderation) du contenu généré par l’utilisateur (UGC).

![chlimage_1-287](assets/chlimage_1-287.png)

#### ANALYTICS {#analytics}

Si Adobe Analytics est sous licence et qu’un service et une structure de cloud Analytics ont été configurés, il est possible d’activer Analytics et de sélectionner la structure.

Voir Configuration [Analytics pour les fonctionnalités](/help/communities/analytics.md)des communautés.

![chlimage_1-288](assets/chlimage_1-288.png)

#### TRANSLATION {#translation}

Les paramètres [de](/help/communities/sites-console.md#translation) traduction spécifient la langue de base du site ainsi que si l&#39;UGC peut être traduit ou non et dans quelle langue, le cas échéant.

* Vérifier **autoriser la traduction automatique**
* Laissez les langues par défaut sélectionnées pour la traduction par le service de traduction automatique par défaut
* Quitter le fournisseur de traduction par défaut et la configuration
* Il n&#39;est pas nécessaire d&#39;avoir un magasin global car il n&#39;y a pas de copies de langue
* Sélectionner **Traduire la page entière**
* Option de persistance par défaut

![chlimage_1-289](assets/chlimage_1-289.png)

#### ENABLEMENT {#enablement}

Laissez vide lorsque vous créez une communauté d’engagement.

Pour consulter un didacticiel similaire sur la création rapide d’une communauté [d’](/help/communities/overview.md#enablement-community)activation, voir [Prise en main des AEM Communities pour l’activation](/help/communities/getting-started-enablement.md).

Sélectionnez **Suivant**.

![chlimage_1-290](assets/chlimage_1-290.png)

### Étape 4 : Créer un site de communautés {#step-create-communities-site}

Sélectionnez **Créer.**

![chlimage_1-291](assets/chlimage_1-291.png)

Une fois le processus terminé, le dossier du nouveau site s&#39;affiche dans la console Communautés - Sites.

![communitiessitesconsole](assets/communitiessitesconsole.png)

## Publication du site de la communauté {#publish-the-community-site}

Le site créé doit être géré à partir de la console Communautés - Sites, la même console que celle où de nouveaux sites peuvent être créés.

Après avoir sélectionné le dossier du site de la communauté pour l’ouvrir, passez la souris sur l’icône du site pour afficher quatre icônes d’action :

![siteactionicons-1](assets/siteactionicons-1.png)

Lorsque vous sélectionnez la quatrième icône d’ellipses (Autres actions), les options Exporter le site et Supprimer le site s’affichent.

![siteactionsnew-1](assets/siteactionsnew-1.png)

De gauche à droite, ils sont :

* **Ouvrir le site**

   Sélectionnez l’icône représentant un crayon pour ouvrir le site de la communauté en mode d’édition de l’auteur, pour ajouter et/ou configurer des composants de page.

* **Modifier le site**

   Sélectionnez l’icône Propriétés pour ouvrir le site de la communauté en vue de modifier les propriétés, comme le titre ou pour modifier le thème.

* **Publier le site**

   Sélectionnez l’icône du monde pour publier le site de la communauté (par exemple, si votre serveur de publication s’exécute sur votre ordinateur local, puis sur localhost:4503 par défaut).

* **Exporter le site**

   Sélectionnez l’icône d’exportation pour créer un package du site de la communauté qui est à la fois stocké dans le gestionnaire de [packages](/help/sites-administering/package-manager.md) et téléchargé.
Notez que UGC n&#39;est pas inclus dans le package du site.

* **Supprimer le site**

   Sélectionnez l&#39;icône Supprimer pour supprimer le site de la communauté dans la console **** Communautés > Sites. Cette action supprime tous les éléments associés au site, tels que l’UGC, les groupes d’utilisateurs, les ressources et les enregistrements de base de données.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Si vous n’utilisez pas le port par défaut 4503 pour l’instance de publication, modifiez l’agent de réplication par défaut afin de définir le numéro de port sur la valeur correcte.
>
>Sur l’instance d’auteur, dans le menu principal :
>
>1. Accédez au menu **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]** .
>1. Sélectionnez **[!UICONTROL Agents sur l’auteur]**.
>1. Sélectionnez Agent **[!UICONTROL par défaut (publication)]**.
>1. En regard de **[!UICONTROL Paramètres]**, sélectionnez **[!UICONTROL Modifier]**.
>1. Dans la boîte de dialogue contextuelle Paramètres de l&#39;agent, sélectionnez l&#39;onglet **[!UICONTROL Transport]** .
>1. Dans URI, modifiez le numéro de port, 4503, en numéro de port souhaité. Par exemple, pour utiliser le port 6103 : https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. **[!UICONTROL Cliquez sur OK]**.
>1. (Facultatif) Sélectionnez **[!UICONTROL Effacer]** ou **[!UICONTROL Forcer une nouvelle tentative]** pour réinitialiser la file d&#39;attente de réplication.

>



### Sélectionnez Publier {#select-publish}

Une fois que le serveur de publication est en cours d’exécution, sélectionnez l’icône du monde pour publier le site de la communauté.

![chlimage_1-292](assets/chlimage_1-292.png)

Une fois le site de la communauté publié, un message s’affiche brièvement :

![chlimage_1-293](assets/chlimage_1-293.png)

### Nouveaux groupes d’utilisateurs de la communauté {#new-community-user-groups}

En plus du nouveau site communautaire, de nouveaux groupes d’utilisateurs sont créés et disposent des autorisations appropriées définies pour diverses fonctions administratives. Pour plus d’informations, consultez Groupes d’ [utilisateurs pour les sites](/help/communities/users.md#usergroupsforcommunitysites)de la communauté.

Pour ce nouveau site communautaire, étant donné le nom du site &quot;s’engager&quot; à l’étape 1, les quatre nouveaux groupes d’utilisateurs peuvent être vus à partir de la console [](/help/communities/members.md) Groupes (navigation globale : Communautés, groupes) :

* Collectif Interagir avec les gestionnaires communautaires
* Administrateurs du groupe d’engagement de la communauté
* Membres de la communauté
* Modérateurs d’engagement de la communauté
* Participation de la communauté aux membres privilégiés
* Community Interagir avec le gestionnaire de contenu du site

Notez que [Aaron McDonald](/help/communities/tutorials.md#demo-users) est membre de

* Collectif Interagir avec les gestionnaires communautaires
* Modérateurs d’engagement de la communauté
* Interagir avec la communauté Membres (indirectement en tant que membre du groupe Modérateurs)

![chlimage_1-294](assets/chlimage_1-294.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-311](assets/chlimage_1-311.png)

## Erreur de configuration pour l’authentification {#configure-for-authentication-error}

Une fois qu’un site a été configuré et envoyé pour publication, [configurez le mappage](/help/communities/sites-console.md#configure-for-authentication-error) de connexion ( `Adobe Granite Login Selector Authentication Handler`) sur l’instance de publication. L’avantage est que lorsque les informations d’identification de connexion ne sont pas saisies correctement, l’erreur d’authentification affiche à nouveau la page de connexion du site de la communauté avec un message d’erreur.

Ajouter un `Login Page Mapping` comme

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Étapes facultatives {#optional-steps}

### Modification de la Page d&#39;accueil par défaut {#change-the-default-home-page}

Lorsque vous travaillez avec le site de publication à des fins de démonstration, il peut s’avérer utile de modifier la page d&#39;accueil par défaut du nouveau site.

Pour ce faire, il est nécessaire d’utiliser [CRXDE](https://localhost:4503/crx/de) Lite pour modifier la table de mappage [des](/help/sites-deploying/resource-mapping.md) ressources lors de la publication.

Pour commencer :

1. Sur l’instance de publication, connectez-vous avec des droits d’administrateur.
1. Accédez à [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. Dans le navigateur du projet, développez `/etc/map.`
1. Sélectionnez le `http` noeud :

   * Sélectionnez **Créer un noeud :**

      * **Nommer** localhost.4503(n&#39;utilisez *pas* &#39;:&#39;)

      * **Type** [sling:Mappage](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Avec le nouveau `localhost.4503` noeud sélectionné :

   * Ajouter, propriété :

   * **Nom** sling:match
      * **Chaîne de type**
      * **Valeur** localhost.4503/$(doit se terminer par &#39;$&#39; char)
   * Ajouter, propriété :

      * **Nom** sling:internalRedirect
      * **Chaîne de type**
      * **Valeur** /content/sites/engage/en.html


1. Select **Save All.**
1. (Facultatif) Supprimez l’historique de navigation.
1. Accédez à https://localhost:4503/.

   * Arrivez à https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Pour le désactiver, il vous suffit de préfixer la valeur de la `sling:match` propriété avec un &quot;x&quot; - `xlocalhost.4503/$` - et **Enregistrer tout**.


![chlimage_1-297](assets/chlimage_1-297.png)

#### Dépannage : Erreur lors de l&#39;enregistrement de la carte {#troubleshooting-error-saving-map}

Si vous ne parvenez pas à enregistrer les modifications, assurez-vous que le nom du noeud est `localhost.4503`, avec un séparateur de points, et non `localhost:4503` avec un séparateur de points, car `localhost`il ne s’agit pas d’un préfixe d’espace de nommage valide.

![chlimage_1-298](assets/chlimage_1-298.png)

#### Dépannage : Echec de la redirection {#troubleshooting-fail-to-redirect}

La valeur &quot;**$**&quot; à la fin de la `sling:match`chaîne d’expression normale est cruciale, de sorte que seul le mappage exact `https://localhost:4503/` est effectué, sinon la valeur de redirection est précédée d’un chemin d’accès qui peut exister après le serveur:port dans l’URL. Par conséquent, lorsqu’AEM tente de rediriger vers la page de connexion, elle échoue.

### Modifier le site {#modify-the-site}

Une fois le site créé, les auteurs peuvent utiliser l’icône [](/help/communities/sites-console.md#authoring-site-content) Ouvrir le site pour effectuer des activités de création AEM standard.

En outre, les administrateurs peuvent utiliser l&#39;icône [](/help/communities/sites-console.md#modifying-site-properties) Modifier le site pour modifier les propriétés du site, comme le titre.

Après toute modification, n’oubliez pas d’ **enregistrer** et de publier à nouveau **** le site.

>[!NOTE]
>
>If not familiar with AEM, view the documentation on [basic handling](/help/sites-authoring/basic-handling.md) and a [quick guide to authoring pages](/help/sites-authoring/qg-page-authoring.md).


