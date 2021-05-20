---
title: Création et modification d’applications à l’aide de la console Applications
seo-title: Création et modification d’applications à l’aide de la console Applications
description: Consultez cette page pour en savoir plus sur la création et la modification d’applications à l’aide de la console d’applications.
seo-description: Consultez cette page pour en savoir plus sur la création et la modification d’applications à l’aide de la console d’applications.
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2638'
ht-degree: 2%

---

# Création et modification d’applications à l’aide de la console Applications{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le processus de développement des applications mobiles d’AEM reconnaît que des utilisateurs de différentes compétences contribuent au développement des applications mobiles. Le mappage de processus suivant illustre l’ordre général dans lequel les auteurs de contenu et les développeurs d’applications effectuent des tâches.

![chlimage_1-10](assets/chlimage_1-10.gif)

Des informations sur l’exécution des tâches du marketeur apparaissent sur cette page. Pour plus d’informations sur les tâches des développeurs, voir Création d’applications PhoneGap.

## Structure des applications mobiles {#the-structure-of-mobile-applications}

AEM Mobile fournit le plan directeur de l’application PhoneGap pour la création d’applications mobiles. Le plan directeur définit la structure des applications que vous créez. Les applications se composent des éléments suivants :

* Page racine.
* Variations de langue de l’application.
* Page d’accueil de la variation de langue.

### Racine d’une application PhoneGap {#the-root-of-a-phonegap-app}

La page racine des applications mobiles que vous créez dans AEM apparaît dans la console Applications.

La page racine est stockée sous la propriété Destination Path de l’application qui a été spécifiée lors de la création de l’application (le chemin par défaut est /content/phonegap/apps). Le nom de la page est la propriété Name de l’application. Par exemple, l’URL par défaut de la page racine du site nommée `myphonegapapp` est `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### Variation linguistique d’une application PhoneGap {#the-language-variation-of-a-phonegap-app}

Les premières pages enfants de la page racine sont les variations de langue de l’application. Le nom de chaque page est la langue pour laquelle l’application est créée. Par exemple, l’anglais est le nom de la variante anglaise de l’application.

**Remarque :** Le plan directeur PhoneGap par défaut crée uniquement une application en anglais. Votre développeur peut modifier le plan directeur afin qu’il puisse créer d’autres variations de langue.

![chlimage_1-147](assets/chlimage_1-147.png)

La page Langue a deux objectifs :

* Le contenu de la page est la page d’accrochage de la variante linguistique de l’application.
* Les propriétés de page contrôlent plusieurs aspects de conception de l’application, tels que l’URL à utiliser pour demander des mises à jour de contenu, ainsi que des informations sur la connexion à la version cloud et à l’intégration des services Adobe Analytics.

![chlimage_1-148](assets/chlimage_1-148.png)

### Page d’accueil {#the-home-page}

La page d’accueil, ou la page index.html d’une variante linguistique d’une application s’affiche à l’ouverture de celle-ci. La page d’accueil propose aux utilisateurs un menu de liens vers différentes pages de l’application. Le système de paragraphes permet d’ajouter des composants à la page pour créer du contenu.

## Création d’une application mobile {#creating-a-mobile-application}

Les applications mobiles sont basées sur un plan directeur qui définit une structure de page et des propriétés. Vous pouvez configurer les propriétés de l’application suivantes :

* **Titre :** titre de l’application.
* **Chemin d’accès de destination :**  emplacement dans le référentiel où est stockée l’application. Laissez la valeur par défaut pour créer un chemin d’accès en fonction du nom de l’application.

* **Nom :** la valeur par défaut est la valeur de la propriété Title avec les caractères d’espace supprimés. Le nom est utilisé dans CQ pour faire référence à l’application, par exemple pour le noeud de référentiel qui représente l’application.
* **Description :**  description de l’application.
* **URL du serveur :** URL qui fournit des mises à jour de contenu en direct (OTA) à l’application. La valeur par défaut est l’URL du serveur de publication de l’instance utilisée pour créer une application (provenant du service externalizer). Notez qu’il doit s’agir d’une instance de serveur de publication plutôt que d’un auteur, ce qui nécessite une authentification.

Vous pouvez également fournir un fichier image à utiliser comme miniature de l’application, sélectionner la configuration de PhoneGap Build à utiliser et sélectionner la configuration d’analyse de l’application mobile à utiliser. Cette image est utilisée uniquement comme miniature pour représenter votre application mobile dans la console des applications mobiles en Experience Manager.

Il existe des onglets supplémentaires (et facultatifs) pour créer le service cloud et intégrer le module SDK Mobile Services Adobe dans votre application.

* Build : Cliquez sur Gérer les configurations et configurez ici votre service de génération build build.phonegap.com. Ensuite, dans la liste déroulante, vous pourrez sélectionner le nouveau service cloud PhoneGap Build.
* Analytics : Cliquez sur Gérer les configurations et configurez le service cloud [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/using/home.html). Ensuite, dans la liste déroulante, vous pourrez sélectionner le service mobile nouvellement créé à intégrer à votre application mobile.

>[!NOTE]
>
>Les développeurs peuvent utiliser le AEM PhoneGap Starter Kit pour créer des applications et les ajouter à la console.

La procédure suivante utilise l’interface utilisateur tactile pour créer une application mobile.

1. Sur le rail, cliquez sur Applications.
1. Cliquez ou appuyez sur l’icône Créer .

   ![](do-not-localize/chlimage_1-7.png)

1. (Facultatif) Dans l’onglet Avancé , fournissez une description de l’application et modifiez l’URL du serveur si nécessaire.
1. (Facultatif) Si vous utilisez PhoneGap Build pour compiler l’application, dans l’onglet Créer , sélectionnez la configuration à utiliser.

   Pour créer une configuration de version PhoneGap, cliquez sur Gérer les configurations.

1. (Facultatif) Si vous utilisez SiteCatalyst pour effectuer le suivi de l’activité de l’application, sélectionnez la configuration à utiliser dans l’onglet Analytics.

   Pour créer une configuration d’application mobile, cliquez sur Gérer les configurations.

1. (Facultatif) Pour fournir une icône d’application, cliquez sur le bouton Parcourir , sélectionnez le fichier image dans votre système de fichiers, puis cliquez sur Ouvrir.
1. Cliquez sur Créer.

### Modification des propriétés d’une application mobile {#changing-the-properties-of-a-mobile-application}

Après avoir créé une application mobile, vous pouvez modifier ses propriétés.

#### Modifier le titre, la description et l’icône {#change-the-title-description-and-icon}

1. Sur le rail, cliquez ou appuyez sur Applications.
1. Sélectionnez l’application à configurer, puis cliquez sur l’icône Afficher les propriétés de page .

   ![](do-not-localize/chlimage_1-8.png)

1. Pour modifier les valeurs de propriété, cliquez ou appuyez sur l’icône Modifier .

   ![](do-not-localize/chlimage_1-9.png)

1. Configurez les propriétés de base et avancées, puis cliquez ou appuyez sur l’icône Terminé .

   ![](do-not-localize/chlimage_1-10.png)

#### Configuration d’une variation linguistique de l’application {#configure-a-language-variation-of-the-application}

1. Sur le rail, cliquez ou appuyez sur Applications.
1. Cliquez pour accéder à l’application mobile que vous souhaitez modifier dans l’Admin Console des applications. Sélectionnez la version linguistique de l’application à configurer, puis cliquez sur l’icône Afficher les propriétés de l’application .

   ![](do-not-localize/chlimage_1-11.png)

1. Pour modifier les valeurs de propriété, cliquez ou appuyez sur l’icône Modifier .

   ![](do-not-localize/chlimage_1-12.png)

1. Configurez les propriétés dans les onglets De base, Avancé, Créer et Analytics, puis cliquez ou appuyez sur l’icône Terminé.

   ![](do-not-localize/chlimage_1-13.png)

### Création du contenu d’une application mobile {#authoring-the-content-of-a-mobile-application}

Après avoir créé l’application mobile, ajoutez le contenu utilisé comme interface utilisateur de l’application.

1. Sur le rail, cliquez ou appuyez sur Applications.
1. Cliquez ou appuyez sur l’application, puis sur Anglais.
1. Modifiez la page d’accueil ou ajoutez des pages enfants selon les besoins.

### Déplacement de contenu vers des applications mobiles {#moving-content-to-mobile-applications}

Le cache de synchronisation de contenu sur l’instance de publication AEM est utilisé comme référentiel de contenu pour les applications mobiles :

* Le contenu du cache de synchronisation de contenu est inclus dans l’application lorsque les développeurs compilent l’application.
* Le contenu du cache est disponible pour les applications mobiles installées afin de mettre à jour le contenu de l’application.

Les applications mobiles incluent une commande de mises à jour qui télécharge et installe le contenu d’application mis à jour. Lorsqu’une instance d’application envoie une demande de mise à jour, la synchronisation de contenu détermine le contenu qui a changé depuis la dernière mise à jour ou installation de l’application et fournit le nouveau contenu.

![chlimage_1-149](assets/chlimage_1-149.png)

Pour rendre le contenu mis à jour disponible pour les applications, mettez à jour le cache de synchronisation de contenu. La première fois que vous mettez à jour le cache, tout le contenu publié est ajouté. Les mises à jour suivantes ajoutent uniquement le contenu publié qui a changé depuis la mise à jour précédente.

La synchronisation de contenu effectue également le suivi lorsque les mises à jour se produisent. Grâce à ces informations, la synchronisation de contenu peut déterminer la mise à jour du cache à envoyer à une application mobile.

Procédez comme suit sur l’instance où vous souhaitez mettre à jour le cache. Par exemple, si votre application demande des mises à jour à partir de l’instance de publication, effectuez la procédure sur l’instance de publication.

1. Sur le rail, cliquez ou appuyez sur Applications, puis sur votre application.
1. Sélectionnez la page de démarrage, puis cliquez ou appuyez sur l’icône Mettre à jour le cache .

   ![](do-not-localize/chlimage_1-14.png)

### Utilisation des modèles d’application {#using-app-templates}

Il s’agit d’une fonctionnalité disponible avec les applications 6.1 Feature Pack 2 et qui permet d’exploiter facilement les modèles d’applications existants pour créer de nouvelles applications dans AEM.

Qu’est-ce qu’un modèle d’application ? Considérez-le comme un ensemble de modèles de page et de composants qui représentent une ligne de base ou une base d’une application.
Lors de la création d’une application basée sur le modèle d’une autre application, vous obtenez une application dont le point de départ est représentatif de l’application à partir de laquelle elle a été créée.

Pour utiliser cette fonctionnalité, vous devez disposer d’un modèle d’application mobile (ou d’une application installée avec un modèle d’application).

Le dernier exemple de package d’AEM Apps 6.1 comprend une version mise à jour de l’application Geometrixx avec un modèle d’application. Vous pouvez également installer le StarterKit qui fournit également un modèle.

Procédure de création d’une application basée sur un modèle d’application :

1. Assurez-vous que le dernier Feature Pack et les exemples de packages de référence d’AEM Apps 6.1 sont installés.
1. Cliquez sur Applications dans le rail de gauche.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Cliquez sur le bouton + Créer en haut de l’écran, puis sélectionnez Créer une application.
1. Une fois que la liste des modèles d’application s’affiche, sélectionnez-en un :

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Cliquez sur Suivant.
1. Fournissez un ID d’application et un titre, mais vous pouvez également inclure un nom et une description.

   1. En outre, vous pouvez fournir un fichier PNG (format d’icône PhoneGap pris en charge) en tant qu’icône en parcourant AEM ressources.
   1. N’oubliez pas que vous pouvez modifier tous ces champs une fois l’application créée dans la mosaïque Gérer l’application . À l’exception de l’ID d’application, une fois l’ID d’application défini, vous ne pouvez pas le modifier.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Cliquez sur le bouton Créer. Deux options s’affichent : Terminé (retour à la vue Catalogue d’applications) ou Gérer l’application (ouverture du tableau de bord de l’application).
1. Une fois créée, la nouvelle application doit être répertoriée dans le catalogue d’applications :

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Cliquez sur l’application pour l’ouvrir. Vous avez réussi à créer une application basée sur le modèle d’une application existante.

>[!NOTE]
>
>Si vous désinstallez le package d’application de référence Geometrixx Outdoors d’AEM et qu’une application est créée en fonction de son modèle, cette application ne sera plus fonctionnelle. L’application Geometrixx Outdoors peut être supprimée, mais le modèle d’application doit rester s’il est utilisé par d’autres applications mobiles.

## Exploration de l’application Exemples de Geometrixx Outdoors {#exploring-the-sample-geometrixx-outdoors-app}

L’application Geometrixx Outdoors est un exemple d’application PhoneGap qui présente les fonctionnalités du plan directeur de l’application PhoneGap par défaut et les exemples de composants mobiles.

Pour ouvrir l’application, cliquez sur Applications mobiles dans le rail, puis sélectionnez Application Geometrixx Outdoors.

### Fonctionnalités de page courantes - Application mobile Geometrixx {#common-page-features-geometrixx-mobile-app}

Chaque page de l’application mobile comprend les fonctionnalités suivantes :

* Bouton Retour permettant de revenir à la page parente. Notez que le bouton Retour n’apparaît pas sur la page d’accueil.
* Un rail extensible qui offre un menu de commandes et de liens :

   * Ouvrez la page Emplacements .
   * Ouvrez le panier.
   * Connectez-vous.
   * Mettez à jour l’application.

* Le système de paragraphes, pour l’ajout de composants et la création de contenu.

### Page d’accueil - Application mobile Geometrixx {#the-home-page-geometrixx-mobile-app}

Le contenu de la page d’accueil se compose des outils de navigation suivants :

* Un composant Liste de menus qui fournit des liens vers les pages enfants Écran, Révisions, Actualités et À propos de nous .
* Composant Faire glisser le carrousel qui affiche les pages enfants.

### Page d’engrenage - Application mobile Geometrixx {#the-gear-page-geometrixx-mobile-app}

La page Engrenage permet aux utilisateurs d’accéder aux pages de produits. Un composant de liste de menus permet d’accéder aux pages enfants de la page d’engrenage. Les pages enfants sont des catégories de produits que le site web propose.

* Saison
* Vêtements
* Sexe
* Activité

Chaque page de catégorie utilise la même structure de contenu que la page d’engrenage. Le carrousel permet d’accéder aux pages enfants qui sont des sous-catégories de produits. Les pages de sous-catégorie contiennent des listes de produits qui fournissent des liens vers les pages de produits.

### Page Produits - Application mobile Geometrixx {#the-products-page-geometrixx-mobile-app}

La page Produits et son hiérarchie de pages enfants implémentent un système de classification pour les pages de produits. Les pages les plus basses de chaque branche de l’hiérarchie sont une page de produit qui contient un composant Produit ng .

La page Produits n’est pas disponible pour les utilisateurs de l’application. La page Engrenage permet d’accéder à chaque page de produit.

### Page Révisions - Application mobile Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contient un bouton Précédent. Le système de paragraphes vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page Révisions est disponible à partir du carrousel sur la page en anglais.

### Page d’actualités - Application mobile Geometrixx {#the-news-page-geometrixx-mobile-app}

Contient un bouton Précédent. Le système de paragraphes vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page Actualités est disponible dans le carrousel sur la page en anglais.

### Page À propos de nous - Application mobile Geometrixx {#the-about-us-page-geometrixx-mobile-app}

La page À propos de nous contient plusieurs composants de ligne à deux colonnes. Chaque colonne contient un composant Image ou Texte . Les composants sont modifiables et le système de paragraphes vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page À propos de nous est disponible dans le carrousel sur la page en anglais.

### Page Emplacements - Application mobile Geometrixx {#the-locations-page-geometrixx-mobile-app}

La page Emplacements contient un composant Emplacements .

Lors de l’utilisation de l’application, la page Emplacements est disponible dans la liste de menus de la page en anglais.

## Exemples de composants mobiles {#sample-mobile-components}

Plusieurs composants sont immédiatement disponibles dans le sidekick lors de la création des pages d’une application mobile. Les composants appartiennent au groupe de composants PhoneGap.

### Carrousel de balayage {#swipe-carousel}

Le composant Faire glisser le carrousel est un outil permettant de présenter et de parcourir les pages du site. Le composant comprend un carrousel qui effectue un parcours des images pour les pages situées au-dessus d’une liste de liens de page. Modifiez le composant pour spécifier les pages à exposer et le comportement du carrousel.

Notez que les images apparaissent dans le carrousel pour les pages associées à une image d’une manière spécifique. Lorsque les pages ne sont pas associées aux images, seule la liste des liens s’affiche.

![chlimage_1-151](assets/chlimage_1-151.png)

**Onglet Propriétés du carrousel**

Configurez le comportement du carrousel :

* Vitesse de lecture : Durée en millisecondes pendant laquelle chaque image est affichée avant d’afficher la prochaine image.
* Temps de transition : Durée en millisecondes de l’animation pour les transitions d’image.
* Style des commandes : Le type de contrôles fourni pour le déplacement entre les images.

**Onglet Propriétés de liste**

Indiquez le mode de génération de la liste de pages :

* Créer la liste à l’aide de : Méthode à utiliser pour spécifier les pages à inclure dans le carrousel. Voir Création de la liste des pages.
* Classer par : Sélectionnez une propriété de page à utiliser pour trier la liste des pages. Par exemple, sélectionnez jcr:title pour trier les pages par ordre alphabétique de titre.
* Limite : Nombre maximal de pages à inclure. Cette propriété est appropriée pour les méthodes basées sur la recherche permettant de créer la liste de pages.

#### Création de la liste des pages {#building-the-page-list}

Le composant Faire glisser le carrousel fournit les valeurs suivantes pour la propriété Build List Using . La boîte de dialogue de modification change en fonction de la valeur que vous sélectionnez :

**Pages enfants**

Le composant répertorie toutes les pages enfants d’une page spécifique. Après avoir sélectionné cette valeur, sélectionnez la page dans l’onglet Pages enfants ou n’indiquez aucune valeur pour répertorier les enfants de la page active.

**Liste fixe**

Spécifiez une liste de pages d’inclusion. Après avoir sélectionné cette valeur, configurez la liste dans l’onglet Liste fixe qui s’affiche lorsque vous sélectionnez Liste fixe :

* Pour ajouter une page, cliquez sur Ajouter un élément, puis recherchez la page.
* Utilisez les flèches haut et bas pour déplacer la page dans la liste.
* Cliquez sur le bouton Supprimer pour supprimer une page de la liste.

La propriété Classer par n’a aucune incidence sur l’ordre des listes fixes.

**Rechercher**

Renseignez la liste à l’aide des résultats d’une recherche par mot-clé. La recherche est effectuée sur les enfants d’une page que vous spécifiez :

1. Pour spécifier la page racine de la recherche, utilisez la propriété Démarrer dans pour sélectionner le chemin de la page. Ne spécifiez aucun chemin d’accès à rechercher sous la page active.
1. Dans la propriété Search Query, saisissez les mots-clés de recherche.

**Recherche avancée**

Renseignez la liste à l’aide d’une requête [Query Builder](/help/sites-developing/querybuilder-api.md).

### Image {#image}

Ajoutez une image au contenu de votre application.

### Texte {#text}

Ajoutez du texte enrichi au contenu de votre application.

### Emplacements de magasin {#store-locations}

Le composant Emplacements de magasin fournit aux utilisateurs des outils pour trouver des points de vente :

* Rechercher
* Listes des emplacements proches ou distants des coordonnées GPS de l’appareil.

Le composant nécessite que le référentiel contienne des informations d’emplacement pour chaque magasin. Des exemples d’emplacements sont installés sur le noeud /etc/commerce/locations/adobe . ![chlimage_1-152](assets/chlimage_1-152.png)

### Ligne à deux colonnes {#two-column-row}

Permet d’ajouter des composants côte à côte à une page.

![chlimage_1-153](assets/chlimage_1-153.png)
