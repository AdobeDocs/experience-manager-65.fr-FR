---
title: Console de modération
description: Découvrez comment les administrateurs et les modérateurs de communauté peuvent utiliser la console Modération pour accéder à l’ensemble du contenu créé par l’utilisateur pour lequel ils sont autorisés à modérer.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 2%

---

# Console de modération {#moderation-console}

Dans AEM Communities, en bloc [modération du contenu communautaire](/help/communities/moderate-ugc.md) est possible à partir des environnements de création et de publication par les administrateurs et les modérateurs de la communauté (membres de la communauté de confiance affectés en tant que modérateurs).

Les administrateurs et les modérateurs de la communauté peuvent également effectuer des opérations [modération en contexte](/help/communities/in-context.md) dans l’environnement de publication.

Une fonctionnalité de tous les [sites communautaires](/help/communities/sites-console.md) est un `Administration` pour les utilisateurs qui se connectent avec des privilèges d’administrateur. La variable `Administration` permet d’accéder à la console Modération.

Dans la console Modération , les administrateurs et les modérateurs de communauté ont accès à tout le contenu généré par l’utilisateur pour lequel ils sont autorisés à modérer le contenu. S’il est autorisé à modérer plusieurs sites, il est possible d’afficher les publications sur tous les sites ou de filtrer selon les sites de communautés sélectionnés.

Pour obtenir des informations plus détaillées, consultez [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

La console Modération prend en charge :

* Exécution de tâches de modération en bloc.
* Recherche du contenu généré par l’utilisateur.
* Affichage des détails du contenu généré par l’utilisateur.
* Affichage des détails de l’auteur UGC.

Uniquement lorsqu’il est connecté en tant qu’administrateur ou membre avec ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, peuvent être effectuées des tâches de modération.

## Accès à l’environnement de publication {#publish-environment-access}

L’accès à la console Modération à partir d’un site de communauté publié s’effectue par le biais d’un lien Administration qui s’affiche lorsqu’un modérateur de communauté est connecté.

![publishweretail](assets/publishweretail.png)

En sélectionnant le lien Administration, la console Modération s’affiche :

![modération-console-publication](assets/moderation-console-publish.png)

## Accès à l’environnement de création {#author-environment-access}

Dans l’environnement de création, pour accéder à la console Modération

* Dans la navigation globale, sélectionnez **[!UICONTROL Communautés]** > **[!UICONTROL Modération]**.

Uniquement lorsqu’il est connecté en tant qu’administrateur ou en tant que membre avec [autorisations du modérateur](/help/communities/in-context.md#identifyingtrustedmembers), des tâches de modération peuvent être exécutées. Le seul contenu de la communauté affiché est celui que le membre connecté est autorisé à modérer.

>[!NOTE]
>
>Le contenu généré par l’utilisateur de l’environnement de publication n’est visible sur l’auteur que si la SRP choisie met en oeuvre un magasin commun. Par exemple, par défaut, le stockage est JSRP, ce qui n’est pas un magasin courant pour l’auteur et la publication. Consultez la section [Stockage de contenu de la communauté](/help/communities/working-with-srp.md).

![modération-consoleauthor](assets/moderationconsoleauthor.png)

## Interface utilisateur de la console de modération {#moderation-console-ui}

En mettant de côté le rail de navigation de gauche (qui s’affiche sur l’instance de création, mais pas sur l’instance de publication), l’interface utilisateur de modération se compose des éléments suivants :

* **[Barre de navigation supérieure](#top-navigation-bar)**
* **[Barre d’outils](#toolbar)**
* **[Zone de contenu](#content-area)**

### Barre de navigation supérieure {#top-navigation-bar}

La barre de navigation supérieure est constante pour toutes les consoles. Pour plus d’informations, voir [Manipulation de base](/help/sites-authoring/basic-handling.md).

### Barre d’outils {#toolbar}

La barre d’outils, située sous la barre de navigation supérieure, propose le bouton d’activation/désactivation suivant sur le côté gauche :

* [Filtrer le rail](/help/communities/moderation.md#filterrail)
ouvre un rail qui permet de sélectionner les propriétés sur lesquelles filtrer le contenu.

La barre d’outils, située sous la barre de navigation supérieure, propose le bouton d’activation/désactivation suivant sur le côté gauche :

![toggeswitch](assets/toggleswitch.png)

[Filtrer le rail](/help/communities/moderation.md#filterrail)
ouvre un rail lors de la sélection de la fonction de recherche, ce qui permet de sélectionner les propriétés sur lesquelles filtrer le contenu.

![filterrail](assets/filterrail.png)

### Zone de contenu {#content-area}

La zone de contenu contient des informations sur le contenu généré par l’utilisateur :

* Publié par l&#39;UGC
* Nom du membre
* avatar du membre
* Emplacement de la publication
* Quand elle a été publiée
* Nombre de réponses à la publication
* [Opinion](/help/communities/moderate-ugc.md#sentiment) associée à la publication
* Si elle est approuvée, une coche s’affiche.
* S’il existe une pièce jointe, un trombone est affiché.

>[!NOTE]
> 
>La zone de contenu comporte une *défilement infini*, ce qui signifie qu’il vous permet de continuer le défilement jusqu’à ce que vous ayez atteint la fin du contenu. La barre d’outils reste à une position fixe et visible au-dessus de la zone de contenu, même lorsque vous faites défiler l’écran.

### Rail de filtres {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

L’icône du panneau latéral ouvre le rail de filtrage. Le rail de filtre, qui s’affiche à gauche de la zone de contenu, fournit différents filtres, chacun ayant un effet immédiat sur le contenu créé par l’utilisateur référencé qui apparaît dans la zone de contenu.

Les filtres de chaque catégorie sont les suivants : **OU**&quot;d&quot; et les filtres dans différentes catégories sont **ET** Je suis ensemble.

Par exemple, si vous cochez les deux **Question** et **Réponse**, le contenu affiché sous la forme d’une **Question** *ou* an **Réponse**.

Toutefois, si vous cochez la case **Question** et **En attente**, seul le contenu correspondant à un **Question** et est **En attente**.

>[!NOTE]
>
>Les modérateurs de la communauté peuvent mettre en signet les filtres prédéfinis sur l’interface utilisateur de la console de modération. Comme ces filtres sont ajoutés à la fin de l’URL (en tant que paramètres de chaîne de requête), les modérateurs peuvent revenir ultérieurement aux filtres mis en signet et partager ces liens.

![searchicon](assets/searchicon.png)

Lorsque le rail de filtrage est ouvert, l’icône Rechercher permet de basculer entre le panneau latéral et le panneau fermé. Toutefois, pour fermer le rail de filtrage et afficher uniquement le contenu généré par l’utilisateur, cliquez sur l’icône Rechercher et sélectionnez l’option Contenu uniquement .

#### Chemin d’accès au contenu {#content-path}

Le chemin d’accès au contenu limite le contenu généré par l’utilisateur de référence affiché aux publications placées dans le référentiel de contenu spécifié.

![content-path](assets/content-path.png)

#### Recherche textuelle {#text-search}

La recherche de texte limite le contenu généré par l’utilisateur référencé aux publications qui contiennent le texte saisi.

![text-search](assets/text-search.png)

#### Site {#site}

Le site limite le contenu créé par l’utilisateur référencé aux publications sur les sites de communauté sélectionnés. Si aucun site n’est coché, toutes les références au contenu généré par l’utilisateur s’affichent.

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>Lorsqu’un administrateur accède à la console de modération en bloc, toutes les références au contenu généré par l’utilisateur s’affichent, y compris les sites non créés avec la fonction [assistant de création de site](/help/communities/sites-console.md), comme les exemples de Geometrixx.
>
>Lorsque la console de modération en bloc est accessible lors de la publication par un membre de la communauté approuvé, seules les références au contenu créé pour les sites de la communauté que le membre est autorisé à modérer s’affichent. Il peut également être filtré à l’aide du filtre Site.

#### Type de contenu {#content-type}

Type de contenu limite le contenu généré par l’utilisateur référencé affiché aux publications du type de ressource sélectionné. Un ou plusieurs des types suivants peuvent être sélectionnés. Tous les types sont affichés s’ils ne sont pas sélectionnés.

* **Commentaire**
* **Sujet du forum**
* **Réponse du forum**
* **Question Q**
* **Réponse Q&amp;R**
* **Article de blog**
* **Commentaire du blog**
* **Événement de calendrier**
* **Commentaire du calendrier**
* **Dossier de bibliothèque de fichiers**
* **Document de bibliothèque de fichiers**
* **Idée**
* **Commentaire de l’idée**

![content-types](assets/content-types.png)

#### Types de contenu supplémentaires {#additional-content-types}

Pour ajouter des ressources supplémentaires sur lesquelles filtrer :

* Connectez-vous à votre instance d’auteur en tant qu’administrateur.
* Ouvrir [Console web](https://localhost:4502/system/console/configMgr).
* Localiser `AEM Communities Moderation Dashboard Filters`.
* Sélectionnez la configuration pour pouvoir l’ouvrir en mode d’édition.
* Saisissez le ResourceType d’un composant sur lequel filtrer :

   * Par exemple, pour filtrer selon les composants de vote inclus, saisissez :

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* Sélectionnez Enregistrer.
* Actualisez la console Communautés - Modération .

Le résultat est un nouveau filtre sélectionnable pour `Voting` sous le `Content Type` groupe de filtres.

Lorsque ce filtre est sélectionné, le contenu du tableau de bord affiche le contenu généré par l’utilisateur correspondant à l’un des types de ressources renseignés.

#### Statut {#status}

État limite le contenu généré par l’utilisateur référencé aux publications ayant le statut sélectionné, qui peuvent être en attente, approuvées, refusées ou fermées, brouillon ou planifiées pour les articles de blog, et répondre ou non aux questions Q&amp;R. Si aucun paramètre n’est sélectionné, tous sont affichés.

>[!NOTE]
>
>Si seul l’état Non reçu est sélectionné, le modérateur voit tout le contenu (pour tous les types de contenu), à l’exception des questions auxquelles il a répondu. En effet, la propriété responsable de la question à laquelle la réponse a été donnée n’existe pas si des questions sans réponse et d’autres contenus tels que le sujet du forum, l’article de blog ou les commentaires n’ont pas reçu de réponse.

![stats](assets/statuses.png)

#### Marquage {#flagging}

Le marquage limite le contenu généré par l’utilisateur référencé aux publications qui sont marquées ou masquées.

Une fois qu’un élément de contenu est marqué, il reste marqué jusqu’à ce que vous ne le marquiez pas en sélectionnant l’option **Indicateur** à nouveau. Il n’existe aucun niveau de marquage, tel que important ou suivi.

![indicateur](assets/flagging.png)

#### Membres {#members}

Les membres limitent le contenu créé par l’utilisateur référencé à celui publié par le nom du membre saisi.

![members](assets/members.png)

#### Publié au cours du ou des derniers {#posted-in-the-last}

Publié dans les dernières limites Le contenu créé par l’utilisateur référencé s’affiche pour les publications effectuées au cours de la dernière heure, du dernier jour, de la dernière semaine, du dernier mois ou de l’année.

![post-last](assets/posted-last.png)

#### Opinion {#sentiment}

[Opinion](/help/communities/moderate-ugc.md#sentiment) limite le contenu généré par l’utilisateur référencé aux publications dont la valeur d’opinion est positive, négative ou neutre.

![sentiment](assets/sentiment.png)

## Filtres personnalisés {#custom-filters}

Excepté les filtres prêts à l’emploi dans [Rail de filtres](/help/communities/moderation.md#ootbfilters), des filtres personnalisés supplémentaires sur les métadonnées peuvent être ajoutés à l’interface utilisateur de modération. Les développeurs peuvent utiliser l’exemple de code dans GitHub pour étendre les filtres de l’interface utilisateur de modération existants.

![custom-tag-filter](assets/custom-tag-filter.png)

La variable [exemple de projet](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) sur GitHub, implémentez un filtre de balises pour filtrer la liste du contenu généré par l’utilisateur selon que les balises spécifiques sont appliquées au contenu généré par l’utilisateur. Vous pouvez suivre l’exemple de code et créer des filtres analogues pour d’autres champs de métadonnées UGC similaires.

Pour installer l’exemple pour le filtre Balises :

1. Ouvrez le gestionnaire de modules sur AEM Auteur (`https://[aem-author]:4502/crx/packmgr/index.jsp`) et AEM Publier (`https://[aem-publish]:4503/crx/packmgr/index.jsp`).
1. Création du package `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` à partir du code GitHub, puis installez et activez-le.
1. Ouvrez la console des lots sur AEM Auteur ( `https://[aem-author]:4502/system/console/bundles`) et AEM Publier ( `https://[aem-publish]:4503/system/console/bundles`).
1. Créez le package (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) à partir de GitHub, puis installez et activez-le.
1. Accédez à **/apps/social/modération/facettes** noeud sur AEM Auteur (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) et AEM Publier (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`).
1. Ajout d’un utilisateur technique **communities-utility-reader** avec `jcr:read` autorisations.

Pour afficher les filtres personnalisés sur les sites de la communauté existants :

1. Modifier `Clientlibs` de la page de modération existante `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Ajouter une nouvelle catégorie `cq.social.hbs.moderation.v2.`

1. Accédez à `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`.

   * Définir sur le nouveau composant `sling:resourceType = social/moderation/v2/filters.`

1. Accédez à `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Définir sur le nouveau composant `sling:resourceType = social/moderation/v2/modcontainer`.

## Actions de modération {#moderation-actions}

[Actions de modération](/help/communities/moderate-ugc.md#moderation-actions) peut être effectué sur une ou plusieurs sélections effectuées dans la zone de contenu ou lors de l’affichage des détails du contenu.

Pour modérer les publications en bloc, dans la zone de contenu, cliquez sur Sélectionner (![sélecteur](assets/selecticon.png)) sur une publication, qui s’affiche lorsque vous pointez dessus avec la souris (bureau) ou appuyez et maintenez un doigt sur la publication (mobile). Ce faisant, vous accédez au mode de sélection multiple et pouvez désormais sélectionner les publications suivantes à modérer en bloc en cliquant simplement sur celles-ci. Utilisez les boutons affichés sur la barre d’outils pour effectuer des actions de modération sur les publications sélectionnées. Toutes les actions demandent de confirmation.

Pour modérer une seule publication dans la zone de contenu, passez le curseur de la souris (bureau) ou appuyez et maintenez un doigt sur la publication (mobile) afin que les boutons s’affichent sur la publication. Lors d’un fonctionnement sur un seul détail de contenu, seule une action de suppression est appelée pour confirmation.

### Modération de plusieurs publications {#moderating-multiple-posts}

Passez en mode de sélection en bloc en cliquant sur le bouton `Select` sur une publication :

![select-icon](assets/select-icon.png)

Pour quitter le mode de sélection en bloc, sélectionnez l’icône Annuler (x) dans la barre d’outils :

Les actions de modération qui peuvent être effectuées sur plusieurs publications sont les suivantes :

* Refuser
* Supprimer
* Fermer/rouvrir les publications

Les icônes permettant d’effectuer ces actions apparaissent uniquement dans la barre d’outils lorsque plusieurs publications sont sélectionnées.

![bulkmodérer](assets/bulkmoderate.png)

### Modération d’une seule publication {#moderating-a-single-post}

En mode de sélection unique, il est possible de :

* Pour afficher les détails de l’utilisateur, sélectionnez son nom.
* Affichez la publication dans le contexte en sélectionnant le lien vers la publication.
* [Répondre](#reply)
* [Autoriser](#allow)
* [Refuser](#deny)
* [Supprimer](#delete)
* [Fermer](#close)
* Affichage [Historique de modération](#moderation-history)
* [Afficher les détails](#viewdetails)

Le texte de la publication est présent dans le mode Carte au-dessus des icônes d’action de modération et les données suivantes indiquent :

* S’il contient des réponses, et si tel est le cas, précédé du nombre de réponses
* S’il a été marqué
* S’il a été approuvé
* Quand le contenu généré par l’utilisateur a été publié

![singleselectmode](assets/singleselectmode.png)

#### Répondre {#reply}

![répondre](assets/reply.png)

Lorsque vous utilisez une seule publication, une icône Répondre s’affiche si le type de contenu créé par l’utilisateur prend en charge les réponses et est configuré pour autoriser les réponses.

#### Autoriser {#allow}

![autoriser](assets/allow.png)

Lorsque vous travaillez avec une seule publication, l’icône Autoriser s’affiche lorsque la publication a été marquée ou refusée. Si elle est marquée comme une marque, la sélection de l’option Autoriser efface tous les indicateurs.

#### Refuser {#deny}

![deny](assets/deny.png)

La variable **Refuser** l’action de modération n’est disponible que pour le contenu modéré qui n’apparaît pas sur le contenu non modéré, sauf en mode multi-sélection.

Le contenu non modéré est toujours approuvé.

Le contenu modéré passe initialement à l’état En attente et peut être modifié ultérieurement pour approbation ou refus.

Le contenu qui quitte l’état en attente ne peut jamais revenir à l’état en attente. Le contenu marqué comme approuvé ou refusé peut à tout moment être remplacé par un autre état.

#### Supprimer {#delete}

![delete](assets/delete.png)

En mode de sélection unique ou en bloc, vous pouvez sélectionner des éléments et les supprimer. L’action de suppression génère une boîte de dialogue de confirmation. Une fois supprimés, ces éléments disparaissent immédiatement de la zone de contenu. **Une fois le contenu créé par l’utilisateur supprimé, il est définitivement supprimé du référentiel et ne peut plus être récupéré ultérieurement.**.

#### Fermer {#close}

![close](assets/close.png)

Lorsque vous travaillez avec une seule publication, une icône Fermer s’affiche si le type de contenu créé par l’utilisateur permet d’empêcher d’autres publications pour cette ressource.

#### Historique de modération {#moderation-history}

![modération](assets/moderation.png)

Lorsque vous utilisez une seule publication, une icône Historique de modération s’affiche lorsque vous la survolez. La sélection de l’icône affiche un volet contenant un historique des actions entreprises concernant la publication du contenu généré par l’utilisateur.

Pour revenir à l’affichage de la zone de contenu de plusieurs publications générées par l’utilisateur, sélectionnez le X dans le coin supérieur droit du volet d’affichage des détails.

Par exemple :

![modération-history](assets/moderation-history.png)

#### Afficher le détail {#view-detail}

![view](assets/view.png)

Lorsque vous travaillez avec une seule publication, vous pouvez afficher plus de détails en ouvrant le contenu généré par l’utilisateur en mode détaillé.

Pour ce faire, passez la souris sur la publication pour afficher la variable `View Detail` et sélectionnez-la pour afficher un panneau contenant plus de détails sur la publication.

Pour revenir à l’affichage de la zone de contenu de plusieurs publications générées par l’utilisateur, sélectionnez le X dans le coin supérieur droit du volet d’affichage des détails.

Par exemple :

![view1](assets/view1.png)
