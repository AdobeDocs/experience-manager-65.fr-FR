---
title: Console de modération
seo-title: Console de modération
description: Accès à la console Modération
seo-description: Accès à la console Modération
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
translation-type: tm+mt
source-git-commit: 391893f7cf83c018d29af14200c6f160b6d83bdd
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 4%

---


# Moderation Console {#moderation-console}

En AEM Communities, la [modération en bloc du contenu](/help/communities/moderate-ugc.md) de la communauté est possible à la fois de la part de l’auteur et des environnements de publication par les administrateurs et les modérateurs de la communauté (membres de la communauté de confiance affectés en tant que modérateurs).

Les administrateurs et les modérateurs de la communauté peuvent également effectuer une modération [](/help/communities/in-context.md) dans le contexte dans l’environnement de publication.

Une fonctionnalité de tous les sites [de la](/help/communities/sites-console.md) communauté est un élément de `Administration` menu disponible pour les utilisateurs qui se connectent avec des privilèges d’administration. Le `Administration` lien permet d’accéder à la console de modération.

A partir de la console Modération, les administrateurs et les modérateurs de communauté auront accès à tout le contenu généré par l’utilisateur (UGC) pour lequel ils sont autorisés à modérer. S’il est autorisé à modérer plusieurs sites, il est possible de vue des publications sur tous les sites ou de filtrer selon les sites des communautés sélectionnées.

Pour plus d’informations, consultez [Gestion des utilisateurs et des groupes](/help/communities/users.md)d’utilisateurs.

La console Modération prend en charge :

* Exécution de tâches de modération en bloc.
* Recherche UGC.
* Affichage des détails de l’UGC.
* Affichage des détails de l’auteur UGC.

Seules les tâches de modération peuvent être exécutées lorsqu’elles sont connectées en tant qu’administrateur ou membre avec ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`.

## Publier l’accès aux Environnements {#publish-environment-access}

L’accès à la console Modération à partir d’un site communautaire publié s’effectue par le biais d’un lien Administration qui s’affiche lorsqu’un modérateur de communauté est connecté.

![publishweretail](assets/publishweretail.png)

En sélectionnant le lien Administration, la console Modération s’affiche :

![modération-console-publication](assets/moderation-console-publish.png)

## Accès à l’Environnement d’auteur {#author-environment-access}

Dans l’environnement d’auteur, pour accéder à la console Modération

* Dans la navigation globale, sélectionnez **[!UICONTROL Communautés]** > **[!UICONTROL Modération]**.

Seules les tâches de modération peuvent être exécutées lorsqu’elles sont connectées en tant qu’administrateur ou en tant que membre doté d’autorisations [de](/help/communities/in-context.md#identifyingtrustedmembers)modérateur. Le seul contenu de la communauté affiché est celui que le membre connecté est autorisé à modérer.

>[!NOTE]
>
>L’UGC de l’environnement de publication n’est visible sur l’auteur que si le fournisseur de services de gestion des ressources sélectionné met en oeuvre un magasin commun. Par exemple, par défaut, l’enregistrement est JSRP, qui n’est pas un magasin commun pour l’auteur et la publication. See [Community Content Storage](/help/communities/working-with-srp.md).


![modération-consoleauthor](assets/moderationconsoleauthor.png)

## Interface utilisateur de la console de modération {#moderation-console-ui}

En dehors du rail de navigation de gauche (qui s’affiche sur l’auteur, mais pas sur la publication), l’interface utilisateur de modération se compose des zones principales suivantes :

* **[Barre de navigation supérieure](#top-navigation-bar)**
* **[Barre d’outils](#toolbar)**
* **[Zone de contenu](#content-area)**

### Top Navigation Bar {#top-navigation-bar}

La barre de navigation supérieure est constante pour toutes les consoles. Pour plus d’informations, voir Gestion [](/help/sites-authoring/basic-handling.md)de base.

### Barre d’outils {#toolbar}

La barre d’outils, située sous la barre de navigation supérieure, propose le commutateur de bascule suivant sur le côté gauche :

* [Le rail](/help/communities/moderation.md#filterrail)de filtre ouvre un rail qui permet de filtrer le contenu en fonction de diverses propriétés.

La barre d’outils, située sous la barre de navigation supérieure, propose le commutateur de bascule suivant sur le côté gauche :

![toggleswitch](assets/toggleswitch.png)

[Le rail de filtre](/help/communities/moderation.md#filterrail)ouvre un rail, lors de la sélection de la recherche, ce qui permet de sélectionner plusieurs propriétés sur lesquelles filtrer le contenu.

![filterail](assets/filterrail.png)

### Zone de contenu {#content-area}

La zone de contenu contient des informations pour l&#39;UGC publié :

* Publié par UGC
* Nom du membre
* avatar du membre
* Emplacement de la publication.
* Quand elle a été publiée.
* Nombre de réponses à la publication.
* [Opinion](/help/communities/moderate-ugc.md#sentiment) associée à la publication
* Si elle est approuvée, une coche s’affiche.
* S’il y a une pièce jointe, un trombone s’affiche.

>[!NOTE]
> 
>La zone de contenu comporte un défilement ** infini, ce qui signifie que vous pourrez continuer à faire défiler le contenu jusqu’à ce que vous ayez atteint la fin du contenu. La barre d’outils reste à une position fixe et visible au-dessus de la zone de contenu, même si vous faites défiler la page.


### Rail de filtrage {#ootbfilters}

![open-filterail](assets/open-filterrail.png)

L’icône du panneau latéral ouvre le rail de filtre. Le rail de filtre, qui s’affiche à gauche de la zone de contenu, fournit différents filtres, chacun ayant un effet immédiat sur l’UGC référencé qui s’affiche dans la zone de contenu.

Les filtres de chaque catégorie sont **OU** ensemble, et les filtres de différentes catégories sont **ET** ensemble.

Par exemple, si vous cochez à la fois **Question** et **Réponse**, vous verrez le contenu qui est soit une **question** *ou une Réponse.*****

Cependant, si vous cochez **Question** et **En attente**, vous ne verrez que le contenu qui est une **question** et qui est **En attente.**

>[!NOTE]
>
>Les modérateurs de la communauté peuvent mettre en signet les filtres prédéfinis dans l’interface utilisateur de la console de modération. Comme ces filtres sont annexés à la fin de l’URL (en tant que paramètres de chaîne de requête), les modérateurs peuvent revenir aux filtres mis en signet ultérieurement et partager ces liens.


![searchicon](assets/searchicon.png)

Lorsque le rail de filtre est ouvert, l’icône Rechercher permet de basculer entre le panneau latéral et le panneau latéral fermé. Cependant, pour fermer le rail de filtre et ne faire que vue au contenu généré par l’utilisateur, cliquez sur l’icône Rechercher et sélectionnez l’option Contenu uniquement.

#### Chemin d’accès au contenu {#content-path}

Le chemin d’accès au contenu limite la référence de l’UGC affichée aux publications placées dans le référentiel de contenu spécifié.

![content-path](assets/content-path.png)

#### Recherche textuelle {#text-search}

La recherche textuelle limite l’affichage de l’UGC référencé aux publications contenant le texte saisi.

![recherche de texte](assets/text-search.png)

#### Site {#site}

Le site limite le contenu UGC référencé affiché aux publications à certains sites communautaires. Si aucun site n&#39;est coché, toutes les références à l&#39;UGC s&#39;affichent.

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>Lorsqu’un administrateur accède à la console de modération en bloc, toutes les références à l’UGC s’affichent, y compris les sites non créés avec l’assistant [de création de](/help/communities/sites-console.md)site, tels que les exemples de Geometrixx.
>
>Lorsque la console de modération en bloc est accessible lors de la publication par un membre approuvé de la communauté, seules les références à l’UGC créées pour les sites de la communauté que le membre est autorisé à modérer sont affichées et peuvent être filtrées avec le filtre Site.


#### Type de contenu {#content-type}

Le type de contenu limite l’UGC référencé affiché aux publications du type de ressource sélectionné. Un ou plusieurs des types suivants peuvent être sélectionnés. Tous les types sont affichés si aucun n’est sélectionné.

* **Commentaire**
* **Sujet du forum**
* **Réponse du forum**
* **Question Q&amp;R**
* **Réponse Q&amp;R**
* **Article de blog**
* **Commentaire du blog**
* **Événement de calendrier**
* **Commentaire de calendrier**
* **Dossier de bibliothèque de fichiers**
* **Document de bibliothèque de fichiers**
* **Concept**
* **Commentaire de conceptualisation**

![content-types](assets/content-types.png)

#### Types de contenu supplémentaires {#additional-content-types}

Pour ajouter des ressources supplémentaires sur lesquelles filtrer :

* Connectez-vous à votre instance d’auteur en tant qu’administrateur.
* Open [Web Console](https://localhost:4502/system/console/configMgr).
* Localisez `AEM Communities Moderation Dashboard Filters`.
* Sélectionnez la configuration à ouvrir en mode d’édition.
* Saisissez le type de ressource d&#39;un composant sur lequel filtrer :

   * Par exemple, pour filtrer les composants votants inclus, saisissez :

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* Sélectionnez Enregistrer.
* Actualisez la console Communautés - Modération.

Le résultat est un nouveau filtre sélectionnable pour `Voting` sous le groupe de `Content Type` filtres.

Lorsque ce filtre est sélectionné, le contenu du tableau de bord affiche l&#39;UGC correspondant à l&#39;un des types de ressources saisis.

#### État {#status}

L’état limite l’UGC référencé affiché aux publications de l’état sélectionné, qui peut être un ou plusieurs des statuts En attente, Approuvé, Refusé ou Fermé, ainsi que le brouillon ou Programmé pour les articles de blog et Répondu ou Non répondu pour les questions QnA. Si aucun n&#39;est sélectionné, tous sont affichés.

>[!NOTE]
>
>Si seul l’état Non répondu est sélectionné, le modérateur verra l’ensemble du contenu (pour tous les types de contenu), à l’exception des questions auxquelles il a répondu. En effet, la propriété responsable de la question à réponse n&#39;existe pas dans le cas de questions sans réponse et d&#39;autres contenus tels que le sujet du forum, l&#39;article de blog ou les commentaires.


![états](assets/statuses.png)

#### Marquage {#flagging}

Le marquage limite l’affichage de l’UGC référencé aux publications qui sont marquées ou masquées.

Une fois qu’un élément de contenu est marqué, il reste marqué jusqu’à ce que vous démarquiez ce seul élément de contenu en sélectionnant à nouveau le bouton **Indicateur** . Notez qu’il n’existe aucun niveau de marquage, tel qu’important ou suivi.

![indicateur](assets/flagging.png)

#### Membres {#members}

Les membres limitent l&#39;UGC référencé affiché à l&#39;UGC publié par le nom de membre saisi.

![members](assets/members.png)

#### Publié au cours du ou des derniers {#posted-in-the-last}

Publié dans les dernières limites, l’UGC référencé s’affichait pour les publications effectuées au cours de la dernière heure, du dernier jour, de la dernière semaine, du dernier mois ou de l’année.

![posté-dernier](assets/posted-last.png)

#### Opinion {#sentiment}

[L’opinion](/help/communities/moderate-ugc.md#sentiment) limite l’UGC référencé affiché aux publications dont la valeur d’opinion est positive, négative ou neutre.

![opinion](assets/sentiment.png)

## Custom Filters {#custom-filters}

Outre les filtres prêts à l’emploi du rail [de](/help/communities/moderation.md#ootbfilters)filtre, d’autres filtres personnalisés sur les métadonnées peuvent être ajoutés à l’interface utilisateur de modération. Les développeurs peuvent utiliser l’exemple de code dans Github pour étendre les filtres d’interface utilisateur de modération existants.

![filtre-balise personnalisée](assets/custom-tag-filter.png)

L’ [exemple de projet](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) sur Github implémente un filtre de balises afin de filtrer la liste UGC selon si les balises spécifiques sont appliquées au contenu généré par l’utilisateur. Vous pouvez suivre l’exemple de code et créer des filtres analogues pour d’autres champs de métadonnées UGC similaires.

Pour installer l’exemple du filtre Balises :

1. Ouvrez le gestionnaire de packages sur les instances de AEM Author ([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) et de AEM Publish ([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)).
1. Créez le package `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` à partir du code Github, puis installez et activez-le.
1. Ouvrez la console des lots sur les instances de AEM Author ( `https://[aem-author]:4502/system/console/bundles`) et de AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Créez le package ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` à partir de Github, installez et activez-le.
1. Accédez au noeud **/apps/social/modération/facettes** sur le AEM Author ([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/modération/facettes](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) et le AEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/modération/facettes](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)).
1. Ajoutez un utilisateur technique **communautés-utilitaire-reader** avec `jcr:read` des autorisations.

Pour exposer les filtres personnalisés sur des sites communautaires existants :

1. Modification `Clientlibs` de la page de modération existante `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Ajouter une nouvelle catégorie `cq.social.hbs.moderation.v2.`

1. Accédez à `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Définir sur le nouveau composant `sling:resourceType = social/moderation/v2/filters.`

1. Accédez à `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Définir sur le nouveau composant `sling:resourceType = social/moderation/v2/modcontainer`.

## Actions de modération {#moderation-actions}

[Les actions](/help/communities/moderate-ugc.md#moderation-actions) de modération peuvent être exécutées sur une ou plusieurs sélections effectuées dans la zone de contenu ou lors de l’affichage des détails du contenu.

Pour modérer en bloc les publications, dans la zone de contenu, cliquez sur l’icône Sélectionner (![sélection](assets/selecticon.png)) sur une publication, qui s’affiche lorsque vous passez la souris sur celle-ci (bureau) ou lorsque vous appuyez et maintenez un doigt sur la publication (mobile). Ce faisant, vous entrez dans le mode de sélection multiple et pouvez désormais sélectionner les publications suivantes à modérer en bloc en cliquant simplement sur celles-ci. Utilisez les boutons affichés sur la barre d’outils pour effectuer des actions de modération sur les publications sélectionnées. Toutes les actions vous invitent à confirmer.

Pour modérer une publication unique dans la zone de contenu, passez le curseur de la souris (bureau) ou appuyez sur le bouton et maintenez-le enfoncé (mobile) pour que les boutons s’affichent sur la publication. Lorsque vous travaillez sur un seul détail de contenu, seule une action de suppression vous invite à confirmer.

### Modération de plusieurs publications {#moderating-multiple-posts}

Pour passer en mode de sélection en bloc, cliquez sur l’ `Select` icône d’une publication :

![select-icon](assets/select-icon.png)

Pour quitter le mode de sélection en bloc, sélectionnez l’icône Annuler (x) sur la barre d’outils :

Les actions de modération qui peuvent être exécutées sur plusieurs publications sont les suivantes :

* Refuser
* Supprimer
* Fermer/rouvrir les publications

Les icônes permettant ces actions s’affichent uniquement sur la barre d’outils lorsque plusieurs publications sont sélectionnées.

![bulkmodéré](assets/bulkmoderate.png)

### Modération d’une seule publication {#moderating-a-single-post}

En mode de sélection unique, il est possible de :

* Vue des détails de l’utilisateur en sélectionnant son nom.
* Vue de la publication dans son contexte en sélectionnant le lien vers la publication.
* [Répondre](#reply)
* [Autoriser](#allow)
* [Refuser](#deny)
* [Supprimer](#delete)
* [Fermer](#close)
* Historique [de modération de Vue](#moderation-history)
* [Afficher les détails](#viewdetails)

Le texte de la publication figure sur la vue de carte au-dessus des icônes d’action de modération et les données ci-dessous indiquent :

* S&#39;il a des réponses, et dans l&#39;affirmative, précédées du nombre de réponses.
* S’il a été marqué.
* S&#39;il a été approuvé.
* Quand l&#39;UGC a été publié.

![singleselectmode](assets/singleselectmode.png)

#### Répondre {#reply}

![répondre](assets/reply.png)

Lorsque vous travaillez sur une seule publication, une icône de réponse s’affiche si le type UGC prend en charge les réponses et est configuré pour autoriser les réponses.

#### Autoriser {#allow}

![autoriser](assets/allow.png)

Lorsque vous travaillez sur une seule publication, l’icône Autoriser s’affiche lorsque la publication a été marquée ou refusée. Si elle est balisée, l&#39;option Autoriser efface tous les indicateurs.

#### Refuser {#deny}

![refuser](assets/deny.png)

L’action de modération **Refuser** n’est disponible que pour le contenu modéré et n’apparaît pas sur le contenu non modéré, sauf en mode de sélection multiple.

Le contenu non modéré est toujours approuvé.

Le contenu modéré entre dans un état En attente et peut être modifié ultérieurement pour être approuvé ou refusé.

Le contenu qui quitte l’état en attente ne peut jamais revenir à un état en attente. Le contenu marqué comme approuvé ou refusé peut à tout moment être modifié en un autre état.

#### Supprimer {#delete}

![Supprimez](assets/delete.png)

En mode sélection unique ou en mode vrac, vous pouvez sélectionner des éléments et les supprimer. L’action de suppression génère une boîte de dialogue de confirmation. Une fois supprimés, ces éléments disparaissent immédiatement de la zone de contenu. **Une fois l’UGC supprimé, il est définitivement supprimé du référentiel et ne peut plus être récupéré** ultérieurement.

#### Fermer {#close}

![close](assets/close.png)

Lorsque vous travaillez sur une seule publication, une icône Fermer s’affiche si le type UGC prend en charge la possibilité d’empêcher d’autres publications pour cette ressource.

#### Historique de modération {#moderation-history}

![modération](assets/moderation.png)

Lorsque vous travaillez sur une publication unique, une icône d’historique de modération s’affiche lorsque vous la survolez. La sélection de l’icône affiche un volet contenant l’historique des actions entreprises concernant la publication UGC.

Pour revenir à l’affichage de la zone de contenu de plusieurs publications UGC, sélectionnez le X dans le coin supérieur droit du volet des détails de la vue.

Par exemple :

![modération-historique](assets/moderation-history.png)

#### Afficher le détail {#view-detail}

![vue](assets/view.png)

Lorsque vous travaillez avec une seule publication, vous pouvez afficher plus de détails en ouvrant l’UGC en mode détaillé.

Pour ce faire, passez la souris sur la publication pour afficher l’ `View Detail` icône et sélectionnez-la pour afficher un panneau contenant plus de détails sur la publication.

Pour revenir à l’affichage de la zone de contenu de plusieurs publications UGC, sélectionnez le X dans le coin supérieur droit du volet des détails de la vue.

Par exemple :

![view1](assets/view1.png)

