---
title: ClientContext
seo-title: Client Context
description: Découvrez comment utiliser ClientContext dans AEM.
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: 02afc4eb78acaacc40d3ba1830ccb1e9c3907d0f
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 100%

---

# ClientContext{#client-context}

>[!NOTE]
>
>ClientContext a été remplacé par ContextHub. Pour plus de détails, voir la documentation associée concernant la [configuration](/help/sites-developing/ch-configuring.md) et la [documentation développeur](/help/sites-developing/contexthub.md).

Le contexte client. est un mécanisme qui fournit certaines informations sur la page et le visiteur actifs. Il peut être ouvert via **Ctrl-Alt-C** (Windows) ou **Ctrl-Option-C** (Mac) :

![](assets/clientcontext_alisonparker.png)

Dans l’[environnement de publication et de création, il affiche des informations](#propertiesavailableintheclientcontext) sur :

* Le visiteur. En fonction de votre instance, certaines informations sont demandées ou dérivées.
* Les balises de page et le nombre de fois que ces balises ont été consultées par le visiteur actuel (ceci s’affiche lorsque vous placez le curseur de la souris sur une balise).
* Informations sur la page.
* Informations sur l’environnement technique, telles que l’adresse IP, le navigateur et la résolution d’écran.
* Tous les segments actuellement résolus.

Les icônes (disponibles uniquement dans l’environnement de création) vous permettent de configurer les détails du contexte client :

![](do-not-localize/clientcontext_icons.png)

* **Modifier**
Une nouvelle page s’ouvre, vous permettant de [modifier, d’ajouter ou de supprimer une propriété de profil](#editingprofiledetails).

* **Charger**
Vous pouvez [effectuer un choix dans une liste de profils et charger le profil](#loading-a-new-user-profile) que vous souhaitez tester.

* **Réinitialiser**
Vous pouvez [réinitialiser le profil](#resetting-the-profile-to-the-current-user) sur celui de l’utilisateur actuel.

## Composants ClientContext disponibles {#available-client-context-components}

ClientContext peut afficher les propriétés suivantes ([selon les éléments ayant été sélectionnés à l’aide de Modifier](#adding-a-property-component)) :

**Informations sur l’utilisateur**
Affiche les informations côté client suivantes :

* La valeur **Adresse IP**
* Les **mots-clés** utilisés pour le référencement au moteur de recherche
* Le **navigateur** en cours d’utilisation
* L’**OS** (système d’exploitation) utilisé
* L’écran **résolution**
* La position **X de la souris**
* La position **Y de la souris**

**Flux d’activités** Cette section fournit des informations sur l’activité sociale de l’utilisateur sur différentes plateformes, telles que les forums AEM, les blogs, les évaluations, etc.

**Campagne** Permet aux auteurs de simuler une expérience spécifique pour une campagne. Ce composant remplace la sélection normale de résolution et d’expérience de campagne pour permettre de tester différentes variantes.

La résolution de campagne est normalement basée sur la propriété de priorité de la campagne. L’expérience est normalement sélectionnée en fonction de la segmentation.

**Panier** Affiche les informations sur le panier, y compris les entrées de produits (titre, quantité, propriété priceFormatted, etc.), les promotions résolues (titre, message, etc.). et les bons (code, description, etc.).

La boutique de session de panier informe également le serveur des changements de promotion résolus (en fonction des modifications de segmentation) avec la propriété ClientContextCartServlet.

**Boutique générique** Composant générique qui affiche le contenu d’une boutique. Il s’agit d’une version de niveau inférieur du composant Propriétés de la boutique générique.

La boutique générique doit être configurée avec un rendu JS qui affiche les données d’une manière personnalisée.

**Propriétés de la boutique générique** Composant générique qui affiche le contenu d’une boutique. Il s’agit d’une version de niveau supérieur du composant Boutique générique.

Le composant Propriétés de la boutique générique inclut un rendu par défaut qui répertorie les propriétés configurées (ainsi qu’une miniature).

**Géolocalisation** Affiche la latitude et la longitude du client. Elle utilise l’API de géolocalisation HTML5 pour demander la position actuelle au navigateur. Il en résulte l’affichage d’une fenêtre dans laquelle le navigateur demande à l’utilisateur s’il accepte que son emplacement soit partagé.

Lorsqu’il est affiché dans le cloud contextuel, le composant utilise une API Google pour afficher une carte sous forme de vignette. Le composant est soumis aux [limites d’utilisation](https://developers.google.com/maps/documentation/staticmaps/intro#Limits) de l’API Google.

>[!NOTE]
>
>Dans AEM 6.1, la boutique Géolocalisation ne fournit plus la fonction de géocodage inversé. Par conséquent, elle ne récupère plus de détails concernant l’emplacement actuel, tels que le nom de ville ou le code pays. Les segments qui utilisent ces données de boutique ne fonctionneront pas correctement. La boutique Géolocalisation contient uniquement la latitude et la longitude de l’emplacement.

**Magasin JSONP** Un composant qui affiche le contenu qui dépend de votre installation.

La norme JSONP est un complément de JSON qui permet de contourner la stratégie de même origine (ce qui empêche les applications Web de communiquer avec les serveurs se trouvant sur un autre domaine). Elle consiste à envelopper l’objet JSON dans un appel de fonction afin de pouvoir le charger sous forme de `<script>` à partir de l’autre domaine (ce qui est une exception autorisée de la stratégie de même origine).

  La boutique JSONP est semblable à n’importe quelle autre boutique, mais elle charge des informations issues d’un autre domaine sans avoir besoin d’un proxy pour ces informations sur le domaine actuel. Consultez l’exemple figurant dans la section [Stockage de données dans le contexte client via JSONP](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>La boutique JSONP ne met pas en cache les informations figurant dans le cookie, mais récupère ces données à chaque chargement de la page.

**Données de profil** Affiche les informations collectées dans le profil utilisateur. Par exemple, le sexe, l’âge ou l’adresse électronique.

**Segments résolus** Indique quels segments sont actuellement résolus (souvent selon d’autres informations affichées dans le contexte client). Ceci s’avère utile lors de la configuration d’une campagne.

Par exemple, si la souris se trouve sur la partie gauche ou droite de la fenêtre. Ce segment est principalement utilisé à des fins de test, car les modifications sont visibles immédiatement.

**Graphique des réseaux sociaux** Affiche le graphique des réseaux sociaux des amis et des abonnés de l’utilisateur.

>[!NOTE]
>
>Il s’agit actuellement d’une fonction de démonstration qui repose sur des données pré-configurées définies sur les nœuds de profil de nos utilisateurs de démonstration. Pour obtenir un exemple, reportez-vous à :
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => propriété amis

**Nuage de balises** Affiche les balises définies sur la page actuelle et celles qui ont été collectées lors de la navigation sur le site. Déplacer le curseur sur une balise affiche le nombre de fois que l’utilisateur actuel a accédé aux pages contenant cette balise.

>[!NOTE]
>Les balises définies sur des ressources de gestion des ressources numériques qui s’affichent sur les pages visitées ne sont pas prises en compte.

**Boutique Technographics** Ce composant dépend de votre installation.

**ViewedProducts** Conserve la trace des produits que l’acheteur a affichés. Peut être interrogé pour connaître le produit le plus récemment affiché, ou le produit le plus récemment affiché ne figurant pas déjà dans le panier.

Cette boutique de session ne comporte pas de composant de contexte client par défaut.

Pour plus d’informations, consultez [Contexte client en détail](/help/sites-developing/client-context.md).

>[!NOTE]
>« Données de page » ne figure plus dans le contexte client sous la forme d’un composant par défaut. Au besoin, vous pouvez l’ajouter en modifiant le contexte client, en ajoutant le composant **Propriétés de la boutique générique**, puis en le configurant de manière à définir **Boutique** en tant que `pagedata`.

## Modification du profil ClientContext {#changing-the-client-context-profile}

ClientContext vous permet de modifier des détails de manière interactive :

* Modifier le profil utilisé dans ClientContext vous permet de voir les différentes expériences de l’utilisateur sur la page en cours.
* En plus de modifier le profil utilisateur, vous pouvez modifier certains détails du profil pour voir comment le contenu de la page diffère selon différentes conditions.

### Chargement d’un nouveau profil utilisateur {#loading-a-new-user-profile}

Vous pouvez changer le profil en effectuant l’une des opérations suivantes :

* [À l’aide de l’icône de chargement](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [À l’aide du curseur de sélection](#loadinganewvisitorprofilewiththeselectionslider)

Lorsque vous avez terminé, vous pouvez [réinitialiser le profil](#resetting-the-profile-to-the-current-user).

#### Chargement d’un nouveau profil de visiteur avec l’icône de chargement de profil {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. Cliquez sur l’icône de chargement de profil :

   ![](do-not-localize/clientcontext_loadprofile.png)

1. Cette action ouvre la boîte de dialogue, où vous pouvez sélectionner le profil à charger :

   ![](assets/clientcontext_profileloader.png)

1. Cliquez sur **OK** pour procéder au chargement.

#### Chargement d’un nouveau profil utilisateur avec le curseur de sélection {#loading-a-new-user-profile-with-the-selection-slider}

Vous pouvez également sélectionner un profil avec le curseur de sélection :

1. Double-cliquez sur l’icône représentant l’utilisateur actuel. Le sélecteur s’ouvre ; utilisez les flèches pour passer en revue les profils disponibles :

   ![](assets/clientcontext_profileselector.png)

1. Cliquez sur le profil à charger. Lorsque les informations sont chargées, cliquez en dehors du sélecteur pour le fermer.

#### Réinitialisation du profil sur l’utilisateur actuel {#resetting-the-profile-to-the-current-user}

1. Utilisez l’icône de réinitialisation pour réinitialiser le profil dans le contexte client sur celui de l’utilisateur actuel :

   ![](do-not-localize/clientcontext_resetprofile.png)

### Changement de la plateforme de navigateur {#changing-the-browser-platform}

1. Double-cliquez sur l’icône représentant la plateforme de navigateur. Le sélecteur s’ouvre ; utilisez les flèches pour passer en revue les plateformes/navigateurs disponibles :

   ![](assets/clientcontext_browserplatform.png)

1. Cliquez sur la plateforme de navigateur que vous souhaitez charger. Lorsque les informations sont chargées, cliquez en dehors du sélecteur pour le fermer.

### Changement de la géolocalisation {#changing-the-geolocation}

1. Double-cliquez sur l’icône de géolocalisation. Une carte étendue s’ouvre ; vous pouvez y faire glisser le marqueur vers un nouvel emplacement :

   ![](assets/clientcontext_geomocationrelocate.png)

1. Cliquez en dehors de la carte pour la fermer.

### Modification de la sélection des balises {#changing-the-tag-selection}

1. Double-cliquez sur la section Nuage de tags de ClientContext. La boîte de dialogue s’ouvre, et vous pouvez y sélectionner des balises :

   ![](assets/clientcontext_tagselection.png)

1. Cliquez sur OK pour procéder au chargement dans ClientContext.

## Modification de ClientContext {#editing-the-client-context}

La modification de ClientContext peut être utilisée pour définir (ou réinitialiser) les valeurs de certaines propriétés, ajouter une nouvelle propriété ou supprimer une propriété qui n’est plus utile.

### Modification des détails des propriétés {#editing-property-details}

La modification du contexte client peut être utilisée pour définir (ou réinitialiser) les valeurs de certaines propriétés. Ceci vous permet de tester certains scénarios spécifiques (ce qui est particulièrement utile pour la [segmentation](/help/sites-administering/campaign-segmentation.md) et les [campagnes](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)).

![](assets/clientcontext_alisonparker_edit.png)

### Ajout d’un composant de propriété {#adding-a-property-component}

Après avoir ouvert la **page de conception du contexte client**, vous pouvez également **Ajouter** une propriété entièrement nouvelle à l’aide des composants disponibles (les composants sont répertoriés dans le sidekick ou la boîte de dialogue **Insérer un nouveau composant** qui s’affiche si vous double-cliquez sur la case **Faire glisser des composants ou éléments ici**) :

![](assets/clientcontext_alisonparker_new.png)

### Suppression d’un composant de propriété {#removing-a-property-component}

Après avoir ouvert la **page de conception de ClientContext**, vous pouvez également **Supprimer** une propriété si elle n’est plus utile. Ceci comprend les propriétés fournies clé en main. L’option **Réinitialiser** restaure ces propriétés si elles ont été supprimées.

## Stockage des références dans ClientContext via JSONP {#storing-data-in-client-context-via-jsonp}

Suivez cet exemple pour utiliser le composant de boutique contextuel Boutique JSONP afin d’ajouter des données externes à ClientContext. Ensuite, créez un segment basé sur les informations issues de ces données. Cet exemple utilise le service JSONP que WIPmania.com fournit. Le service retourne des informations de géolocalisation en fonction de l’adresse IP du client web.

Cet exemple utilise l’exemple de site web Geometrixx Outdoors pour accéder à ClientContext et tester le segment créé. Vous pouvez utiliser un autre site web tant que la page a activé ClientContext. (Voir [Ajout de ClientContext à une page](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### Ajout du composant Boutique JSONP {#add-the-jsonp-store-component}

Ajoutez le composant Boutique JSONP à ClientContext et utilisez-le pour récupérer et stocker des informations de géolocalisation sur le client web.

1. Ouvrez la page d’accueil en anglais du site Geometrixx Outdoors sur l’instance de création AEM. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Pour ouvrir le contexte client, appuyez sur Ctrl+Alt+C (Windows) ou Ctrl+Option+C (Mac).
1. Cliquez sur l’icône de modification de ClientContext pour ouvrir le concepteur ClientContext.

   ![](do-not-localize/chlimage_1.png)

1. Faites glisser le composant Boutique JSONP sur ClientContext.

   ![](assets/chlimage_1-4.jpeg)

1. Double-cliquez sur le composant pour ouvrir la boîte de dialogue d’édition.
1. Dans la zone URL du service JSONP, saisissez l’URL suivante, puis cliquez sur Récupérer la boutique :

   `https://api.wipmania.com/jsonp?callback=${callback}`

   Le composant appelle le service JSONP et répertorie toutes les propriétés que les données renvoyées contiennent. Les propriétés qui figurent dans la liste sont celles qui seront disponibles dans ClientContext.

   ![](assets/chlimage_1-40.png)

1. Cliquez sur OK.
1. Revenez à la page d’accueil Geometrixx Outdoors et actualisez-la. ClientContext comprend désormais les informations du composant Boutique JSONP.

   ![](assets/chlimage_1-41.png)

### Création du segment {#create-the-segment}

Utilisez les données de la boutique de session que vous avez créée à l’aide du composant Boutique JSONP. Le segment utilise la latitude de la boutique de session et la date actuelle pour déterminer si c’est l’hiver là où se trouve le client.

1. Ouvrez la console Outils dans votre navigateur Web (`https://localhost:4502/miscadmin#/etc`).
1. Dans l’arborescence, cliquez sur le dossier Outils/Segmentation, puis sur Nouveau > Nouveau dossier. Spécifiez les valeurs de propriété suivantes, puis cliquez sur Créer :

   * Nom : mysegments
   * Titre : Mes segments

1. Sélectionnez le dossier Mes segments et cliquez sur Nouveau > Nouvelle page :

   1. Pour le Titre, saisissez Hiver.
   1. Sélectionnez le modèle de segment.
   1. Cliquez sur Créer.

1. Cliquez avec le bouton droit de la souris sur le segment Hiver et cliquez sur Ouvrir.
1. Faites glisser la propriété de la boutique générique vers le conteneur ET par défaut.

   ![](assets/chlimage_1-5.jpeg)

1. Double-cliquez sur le composant pour ouvrir la boîte de dialogue de modification, spécifiez les valeurs de propriété suivantes, puis cliquez sur OK :

   * Boutique : wipmania
   * Nom de la propriété : Latitude
   * Opérateur : Est supérieur à
   * Valeur de propriété : 30

1. Faites glisser le composant Script vers le même conteneur ET, puis ouvrez sa boîte de dialogue de modification. Ajoutez le script suivant, puis cliquez sur OK :

   `3 < new Date().getMonth() < 12`
