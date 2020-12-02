---
title: Expérience du site publié
seo-title: Expérience du site publié
description: Accéder à un site publié
seo-description: Accéder à un site publié
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 2%

---


# Expérience du site publié {#experience-the-published-site}

## Accéder au nouveau site sur Publier {#browse-to-new-site-on-publish}

Maintenant que le site des communautés nouvellement créé a été publié, accédez à l’URL qui s’affiche lors de la création du site, mais sur le serveur de publication, par exemple :

* URL de l’auteur = https://localhost:4502/content/sites/engage/en.html
* URL de publication = https://localhost:4503/content/sites/engage/en.html

Pour éviter toute confusion quant au membre qui est connecté lors de l’auteur et de la publication, il est conseillé d’utiliser différents navigateurs pour chaque instance.

En arrivant sur le site publié, le visiteur du site n’était généralement pas déjà connecté et était anonyme.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![publié](assets/authorpublished.png)

## Visiteur de site anonyme {#anonymous-site-visitor}

Un visiteur de site anonyme voit les éléments suivants dans l’interface utilisateur :

* Titre du site (didacticiel de prise en main)
* Aucun lien de profil
* Aucun lien de message
* Aucun lien de notification
* Champ de recherche
* Lien de connexion
* La bannière de la marque
* Liens de menu pour les composants inclus dans le modèle de site de référence.

Si vous sélectionnez divers liens, vous constaterez qu’ils sont en mode lecture seule.

### Empêcher l’accès anonyme au JCR {#prevent-anonymous-access-on-jcr}

Une limitation connue expose le contenu du site de la communauté aux visiteurs anonymes par le biais du contenu jcr et json, bien que **autoriser l’accès anonyme** soit désactivé pour le contenu du site. Cependant, ce comportement peut être contrôlé à l’aide des restrictions Sling comme solution.

Pour protéger le contenu de votre site communautaire contre l’accès d’utilisateurs anonymes par le biais de contenu jcr et json, procédez comme suit :

1. Sur l’instance d’auteur AEM, accédez à https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >N’accédez pas au site localisé.

1. Accédez à **Propriétés de la page**.

   ![page-properties](assets/page-properties.png)

1. Accédez à l’onglet **Avancé**.

1. Activez **Authentification requise**.

   ![authentification de site](assets/site-authentication.png)

1. Ajoutez le chemin de la page de connexion. Par exemple, **/content/......./GetStarted**.
1. Publiez la page.

## Membre de la communauté approuvée {#trusted-community-member}

Cette expérience suppose que [Aaron McDonald](/help/communities/tutorials.md#demo-users) se voit attribuer les rôles de [gestionnaire communautaire et modérateur](/help/communities/create-site.md#roles). Dans le cas contraire, revenez à l’environnement auteur pour [modifier les paramètres du site](/help/communities/sites-console.md#modifying-site-properties) et sélectionnez Aaron McDonald comme gestionnaire de communauté et modérateur.

Dans le coin supérieur droit, sélectionnez `Log in` et signez avec le nom d&#39;utilisateur (aaron.mcdonald@mailinator.com) et le mot de passe (mot de passe). Vous pouvez vous connecter à l’aide des informations d’identification Twitter ou Facebook.

![Connexion](assets/login.png)

Une fois connecté en tant que membre enregistré de la communauté, notez les options de menu suivantes pour cliquer et explorer votre site communautaire :

* **L’** option Profil vous permet de vue et de modifier votre profil.
* [](/help/communities/configure-messaging.md) Messagesoption vous dirige vers la section de messagerie directe, où vous pouvez :

   1. Vue des messages directs que vous avez reçus (boîte de réception), envoyés (Éléments envoyés) et supprimés (corbeille).
   1. Composez de nouveaux messages directs à envoyer aux individus et aux groupes.

* [L’option ](/help/communities/notifications.md) Notifications vous dirige vers la section Notifications, où vous pouvez vue vos événements d’intérêt et modifier les paramètres de notification.
* [Si vous disposez de privilèges de modération, ](/help/communities/published-site.md#moderationlink) l’administration vous dirige vers la page de modération AEM Communities.

![adminscreen](assets/adminscreen.png)

Notez que la page Calendrier correspond à la page d&#39;accueil, car le modèle de site de référence choisi comprenait d’abord la fonction Calendrier, suivie de la fonction de flux d’Activité, de la fonction de forum, etc. Cette structure est visible à partir de la console [Modèle de site](/help/communities/sites.md#edit-site-template) ou lors de la modification des propriétés du site dans l’environnement d’auteur :

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Pour plus d&#39;informations sur les composants et les fonctions des communautés, consultez :
>
>* [Composants](/help/communities/author-communities.md)  de communautés (pour les auteurs)
>* [Composants, fonctions et fonctionnalités essentiels](/help/communities/essentials.md)  (pour les développeurs)


### Lien du forum {#forum-link}

Vue la fonction de base du forum en sélectionnant le lien du forum.

Les membres peuvent publier un nouveau sujet ou suivre un sujet.

Les visiteurs du site peuvent vue et trier les publications de différentes manières.

![forumlink](assets/forumlink.png)

### Lien Groupes {#groups-link}

Etant donné qu’Aaron est un administrateur de groupe, la sélection du lien Groupes permettra à Aaron de créer un nouveau groupe communautaire en sélectionnant un modèle de groupe, une image, que le groupe soit ouvert ou secret, et en invitant des membres.

Il s’agit d’un exemple de création d’un groupe dans l’environnement de publication.

Les groupes peuvent également être créés dans l’environnement d’auteur et gérés dans le site communautaire de l’environnement d’auteur ([console Groupes communautaires](/help/communities/groups.md)). L&#39;expérience de [création de groupes sur author](/help/communities/nested-groups.md) est présentée dans ce didacticiel.

![grouplink](assets/grouplink.png)

Créer un groupe de référence :

1. Sélectionner **Nouveau groupe**
1. **Onglet Settings**

   * Nom du groupe : `Sports`
   * Description : `A parent group for various sporting groups`.
   * Nom de l’URL de groupe : `sports`
   * Sélectionnez `Open Group` (autoriser tout membre de la communauté à participer en y participant).

1. **Onglet Modèle**

   * Sélectionnez `Reference Group` (contient une fonction de groupes dans sa structure pour autoriser les groupes imbriqués).

1. Sélectionner **Créer un groupe**

   ![creategroup](assets/creategroup.png)

Une fois le nouveau groupe créé, **sélectionnez le nouveau groupe Sports** afin de créer deux groupes (imbriqués) au sein de celui-ci. Comme une structure de site ne peut pas commencer par la fonction de groupes, après avoir ouvert le groupe Sports, il est nécessaire de sélectionner le lien Groupes :

![grouplink1](assets/grouplink1.png)

Le deuxième ensemble de liens, commençant par `Blog`, appartient au groupe actuellement sélectionné, le groupe `Sports`. En sélectionnant le lien Sports `Groups`, vous pouvez imbriquer deux groupes dans le groupe Sports.

Par exemple, ajoutez deux `new groups`.

* Un nom nommé `Baseball`

   * Laissez-le défini comme `Open Group` (adhésion obligatoire).
   * Sous l&#39;onglet Modèles, sélectionnez `Conversational Group`.

* Un nom nommé `Gymnastics`

   * Modifiez son paramètre en `Member Only Group` (adhésion restreinte).
   * Sous l&#39;onglet Modèles, sélectionnez `Conversational Group`.

**Avis**:

* Une actualisation de la page peut s’avérer nécessaire avant l’affichage des deux groupes.
* Ce modèle n&#39;inclut *pas* la fonction de groupes, de sorte qu&#39;il n&#39;est pas possible d&#39;imbriquer davantage de groupes.
* Sur l’auteur, la console [Groupes](/help/communities/groups.md) fournit un troisième choix : un `Public Group` (abonnement facultatif).

Une fois les deux groupes créés, sélectionnez le groupe de baseball, un groupe ouvert, et notez ses liens :

`Discussions` `What's New` `Members`

Les liens du groupe s&#39;affichent sous les liens du site principal et les résultats s&#39;affichent comme suit :

![grouplink2](assets/grouplink2.png)

Sur author - with administrative privilèges, accédez à la console [Groupes de communautés](/help/communities/members.md) et ajoutez Weston McCall au groupe `Community Engage Gymnastics <uid> Members`.

Poursuivant sur la publication, déconnectez-vous en tant que Aaron McDonald, et vue des groupes du groupe Sports en tant que visiteur anonyme du site :

* De la page d&#39;accueil
* Sélectionner le lien `Groups`
* Sélectionner le lien `Sports`
* Sélectionnez le lien Sports `Groups`

Seul le groupe de baseball sera visible.

Connectez-vous en tant que Weston McCall (weston.mccall@dodgit.com / mot de passe) et accédez au même emplacement. Notez que Weston peut `Join` ouvrir le groupe `Baseball` et `enter or Leave` le groupe privé `Gymnastics`.

![grouplink3](assets/grouplink3.png)

### Lien de page Web {#web-page-link}

Vue de la page Web de base incluse dans le site en sélectionnant le lien Page Web. Les outils de création AEM standard peuvent être utilisés pour ajouter du contenu à cette page dans l’environnement d’auteur.

Par exemple, accédez à l&#39;instance **author**, ouvrez le dossier `engage` dans la console [Sites des communautés](/help/communities/sites-console.md), sélectionnez l&#39;icône **Ouvrir le site** pour passer en mode d&#39;édition de l&#39;auteur. Sélectionnez ensuite le mode de prévisualisation pour sélectionner le lien `Web Page`, puis sélectionnez le mode de modification pour ajouter les composants Titre et Texte. Enfin, republiez uniquement la page ou l’ensemble du site.

![webpagelink](assets/webpagelink.png)

### Lien de modération {#moderationlink}

Lorsque le membre de la communauté dispose de privilèges de modération, le lien de modération est visible et sa sélection affiche le contenu de la communauté publié et lui permet d’être [modéré](/help/communities/moderate-ugc.md) d’une manière similaire à la [console de modération](/help/communities/moderation.md) de l’environnement d’auteur.

Utilisez le bouton Retour du navigateur pour revenir au site publié. La plupart des consoles ne sont pas accessibles à partir de la navigation globale dans l’environnement de publication. [](/help/communities/moderate-ugc.md)

![modérationLink](assets/moderationlink.png)

## Auto-inscription {#self-registration}

Une fois déconnecté, il est possible de créer une nouvelle inscription d’utilisateur.

* Sélectionner `Log In`
* Sélectionner `Sign up for a new account`

![enregistrement](assets/registration.png)

![inscription](assets/signup.png)

Par défaut, l’adresse électronique correspond à l’identifiant de connexion. Si cette option n’est pas cochée, le visiteur peut saisir son propre identifiant de connexion (nom d’utilisateur). Le nom d’utilisateur doit être unique dans l’environnement de publication.

Après avoir spécifié le nom, l’adresse électronique et le mot de passe de l’utilisateur, la sélection de `Sign Up` crée l’utilisateur et lui permet de le signer.

Une fois connecté, la première page présentée est leur `Profile` page, qu’ils peuvent personnaliser.

![son profil](assets/profile.png)

Si le membre oublie son ID de connexion, il est possible de récupérer son adresse électronique.

![forgotusername](assets/forgotusername.png)

