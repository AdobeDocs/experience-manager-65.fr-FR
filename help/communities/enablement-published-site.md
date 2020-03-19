---
title: Expérience du site publié
seo-title: Expérience du site publié
description: Accéder à un site publié pour l’activation
seo-description: Accéder à un site publié pour l’activation
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---



# Expérience du site publié {#experience-the-published-site}


**[⇐ Créer et affecter des ressources d&#39;activation](resource.md)**

## Accéder au nouveau site lors de la publication {#browse-to-new-site-on-publish}

Maintenant que le nouveau site de la communauté, ses ressources d&#39;activation et son parcours d&#39;apprentissage ont été publiés, il est possible de découvrir le site du didacticiel d&#39;activation.

Commencez par accéder à l’URL affichée lors de la création du site, mais sur le serveur de publication, par exemple.

* URL de l’auteur = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* URL de publication = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

Si le  [par défaut a été défini](enablement-create-site.md#changethedefaulthomepage), il suffit de naviguer jusqu’à [http://localhost:4503/](http://localhost:4503/) pour lancer le site.

Lors de sa première visite sur le site publié, le du site n’était généralement pas déjà connecté et était anonyme.

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## de site anonyme {#anonymous-site-visitor}

Un anonyme du site est immédiatement présenté avec la page de connexion de ce site de la communauté d&#39;activation privée. Notez qu’il n’existe pas d’option d’auto-inscription ni de connexion avec Facebook ou Twitter.

Remarquez que ce  affiche quatre options de menu : `Assignments, Ski Catalog, What's New` et `Discussions`, mais aucun ne peut être atteint sans se connecter.

>[!NOTE]
>
>Il est possible d&#39;accorder un accès anonyme à un site d&#39;activation sans permettre aux du site de s&#39;inscrire eux-mêmes.
>Si une ressource d&#39;activation est définie sur `show in catalog` et `allow anonymous access`, il sera possible pour les anonymes du site de de ressources dans le catalogue.

### Empêcher l’accès anonyme sur JCR {#prevent-anonymous-access-on-jcr}

Une limitation connue expose le contenu du site communautaire à des anonymes par le biais de contenu jcr et json, bien que l’ **[!UICONTROL autorisation d’accès]** anonyme soit désactivée pour le contenu du site. Cependant, ce comportement peut être contrôlé à l’aide des restrictions Sling comme solution de contournement.

Pour protéger le contenu de votre site communautaire contre l’accès d’utilisateurs anonymes par le biais de contenu jcr et json, procédez comme suit :

1. Sur l’instance d’auteur AEM, accédez à https://&lt;hôte>:&lt;port>/editor.html/content/site/&lt;nom du site>.html.

   >[!NOTE]
   >
   >N’accédez pas au site localisé.

1. Accédez aux Propriétés **[!UICONTROL de]** la page.

   ![page-properties-1](assets/page-properties-1.png)

1. Accédez à l’onglet **[!UICONTROL Avancé]**.
1. Enable **[!UICONTROL Authentication Requirement]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. Ajouter le chemin de la page de connexion. Par exemple, `/content/......./GetStarted`.
1. Publiez la page.

## Membre inscrit {#enrolled-member}

Cette expérience s’appuie sur les utilisateurs `Riley Taylor` et `Sidney Croft` sur le fait d’être [créés](enablement-setup.md#publishcreateenablementmembers) et [affectés](resource.md#settings) aux leçons de *ski parcours d’apprentissage par l’entremise de leur appartenance au groupe Communauté Ski Class.***

Connexion avec

* `Username: riley`
* `Password: password`

Si le utilisateur n’a pas été créé par l’auto-inscription, la première fois qu’un membre se connecte, sa page d’ s’affiche afin qu’il puisse le vérifier et le modifier selon les besoins.

La prochaine fois que le membre se connecte, le , identifié par le premier élément de menu, s’affiche.

![chlimage_1-434](assets/chlimage_1-434.png)

### Affectations {#assignments}

La page Affectations montre au membre tous les chemins d’apprentissage et les ressources d’activation qui lui sont affectés.

Chaque affectation fournit des informations de base sur

* Type d’affectation
* S’il s’agit d’une nouvelle affectation
* Le nom
* Détails pertinents pour le type d’affectation
* Contact d’affectation, expert et auteur (le cas échéant)

Le type d’affectation est indiqué par une icône dans le coin supérieur gauche de la carte. L&#39;image d&#39;une route est celle d&#39;un parcours d&#39;apprentissage avec le nombre de ressources d&#39;activation incluses.

![chlimage_1-435](assets/chlimage_1-435.png)

La sélection des leçons *de* ski affiche les deux ressources d&#39;activation référencées par le chemin d&#39;apprentissage.

![chlimage_1-436](assets/chlimage_1-436.png)

La sélection de la leçon de *ski 1* ouvrira la page des détails de la ressource d&#39;activation.

Sur la page des détails, le membre peut apprendre, [évaluer](rating.md) la leçon et ajouter des [commentaires](comments.md). Tout membre   sera reflété dans la section Nouveautés du site.

Les interactions avec la ressource d&#39;activation seront notées dans la section Rapport accessible dans le  de l&#39;auteur .

![chlimage_1-437](assets/chlimage_1-437.png)

### Catalogue de skis {#ski-catalog}

La page Catalogue de skis est le catalogue des ressources d’activation balisées avec des balises du   de. `Tutorial` Les deux ressources *Ski Lesson* sont balisées avec la `Skiing` balise, de sorte que si des balises autres que `All` ou `Tutorial: Sports / Skiing` sont sélectionnées, rien ne s’affiche.

Lorsqu’un membre n’a pas reçu de ressources d’activation, directement ou par le biais d’un parcours d’apprentissage, il est possible d’interagir avec les ressources d’activation situées dans un catalogue et de fournir des commentaires et des évaluations.

![chlimage_1-438](assets/chlimage_1-438.png)

### Discussions {#discussions}

Outre la notation et les commentaires sur les ressources d’activation ([lorsqu’elles sont activées](enablement-create-site.md#step33asettings)), le modèle de site de la communauté à partir duquel `Enablement Tutorial` a été créée inclut la fonction [de](functions.md#forum-function) forum (le titre est `Discussions)`le titre).

Sélectionnez le `Discussions`lien et publiez une rubrique.

Déconnectez-vous et connectez-vous en tant que Sidney Croft (sidney / password) et répondez à la question, ainsi que Suivez le sujet.

Notez qu’en plus de la modération en ligne, il existe des options pour partager la rubrique sur les réseaux sociaux ou pour envoyer la rubrique par courrier électronique.

![chlimage_1-439](assets/chlimage_1-439.png)

### Nouveautés {#what-s-new}

L&#39; `What's New` option de menu est le titre, étant donné la fonction [de flux de ](functions.md#activity-stream-function) dans la structure de ce site communautaire.

Toujours connecté en tant que Sidney, sélectionnez le `What's New` lien pour afficher le  .

![chlimage_1-440](assets/chlimage_1-440.png)

## Membre de la Communauté approuvé {#trusted-community-member}

Cette expérience suppose ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` qu’on a attribué les rôles de [modérateur](enablement-create-site.md#moderation) et de contact [des](resource.md#settings)ressources.

Connexion avec

* `Username: quinn`
* `Password: password`

Une fois connecté, notez qu’il existe une nouvelle option de menu `Administration`, qui s’affiche car le membre a reçu le rôle de modérateur.

![chlimage_1-441](assets/chlimage_1-441.png)

Le  est identifié par le premier élément de menu, Affectations. Quinn est le modérateur et le contact avec les ressources d&#39;activation et n&#39;a été inscrit à aucune ressource d&#39;activation ou chemin d&#39;apprentissage. Il n&#39;y a donc rien à afficher.

### Administration {#administration}

Ce qu&#39;il y a, c&#39;est   par les deux apprenants, `Riley Taylor` et `Sidney Croft`. En sélectionnant le `Administration` lien permettant d’accéder à la console de modération, Quinn peut utiliser la console [de modération](moderation.md) en bloc pour modérer ses publications.

La sélection de l’icône du panneau latéral permet d’ouvrir le utilisé pour rechercher du contenu de la communauté.

Le survol d’une carte de commentaires affiche des actions de modération.

![chlimage_1-442](assets/chlimage_1-442.png)

## Rapports sur l&#39;auteur {#reports-on-author}

Il existe deux façons d’accéder aux  sur les apprenants et les ressources d’activation.

Sur l’auteur, accédez à la console **[Communautés,](resources.md)**Ressources, où sont gérées les ressources d’activation, et après avoir sélectionné un site de la communauté, il est possible de générer des rapports pour

* Toutes les ressources d’activation et tous les chemins d’apprentissage
* Une ressource d&#39;activation spécifique ou un chemin d&#39;apprentissage

Accédez à la console **[Communautés,](reports.md)**Rapports et générez des rapports selon les

* Affectation aux ressources d’activation et aux chemins d’apprentissage
* Publications sur un site de la communauté pendant une période spécifique
*  (visites de site) d’un site communautaire sur une période spécifique

* Les publications et les  de peuvent être destinées à tout le contenu ou à un contenu spécifique :

   * Forum
   * Sujet du forum
   * Q&amp;R
   * Question Q&amp;R
   * Blog
   * Article de blog
   * Calendrier
   * Événement de calendrier

### Console Ressources {#resources-console}

Avec un peu de   et d&#39;interaction avec les Ressources sur la publication, l&#39;affichage des rapports sur l&#39;auteur vaut le coup d&#39;oeil.

* Sur l’auteur
* Connexion avec droits d’administrateur
* Accédez au menu principal **[!UICONTROL Collectivités > Ressources.]**
* Sélectionner le `Enablement Tutorial` site
* Sélectionner l&#39; `Report` icône d&#39;un résumé de toutes les ressources
* Sélectionnez une ressource, puis l&#39; `Report` icône d&#39;un rapport sur cette ressource.

Notez qu’il est probablement trop tôt pour afficher les données d’Adobe Analytics, qui peuvent prendre de 1 à 12 heures pour apparaître. Toutefois, des  SCORM de base sont déjà disponibles.

#### Rapport de ressources sur les leçons de ski {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Rapport utilisateur des leçons de ski {#ski-lessons-user-report}

* Sélectionner **[!UICONTROL Communautés > Ressources]**

* Ouvrir la carte `Enablement Tutorial`
* Ouvrir la carte `Ski Lessons`
* Sélectionner `Report > User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### Console Rapports{#reports-console} 

La console Rapports permet de générer des rapports sur

* **Affectation** à tout site de la communauté d&#39;activation
* **** pour tout site communautaire
* **Publications** pour tout site de la communauté

Pour les rapports sur les affectations :

* Sur l’auteur
* Connexion avec droits d’administrateur
* Accédez à **[!UICONTROL Communautés > Rapports > Rapport Affectations]**
* Sélectionnez un **[!UICONTROL site]** dans le menu déroulant (sélectionnez `Enablement Tutorial`)

* Sélectionner un **[!UICONTROL groupe]** (sélectionner `Community Ski Class`)

* Sélectionner une **[!UICONTROL affectation]** (sélectionner `Ski Lessons`)

* Sélectionner **[!UICONTROL Générer]**

![chlimage_1-445](assets/chlimage_1-445.png)

Pour les rapports sur les  de :

* Sur l’auteur
* Connexion avec droits d’administrateur
* Accédez à **[!UICONTROL Communautés > Rapports > Rapport]**
* Sélectionnez un **site **dans le menu déroulant (sélectionnez`Enablement Tutorial`)

* Sélectionner le type **[!UICONTROL de]** contenu (sélectionner `all`)

* Sélectionner une plage **[!UICONTROL de]** dates (sélectionner `Last 7 days`)

* Sélectionner **[!UICONTROL Générer]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ Créer et affecter des ressources d&#39;activation](resource.md)**
