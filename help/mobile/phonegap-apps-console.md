---
title: Création et modification d’applications à l’aide de la console d’applications
seo-title: Création et modification d’applications à l’aide de la console d’applications
description: Suivez cette page pour en savoir plus sur la création et la modification d’applications à l’aide de la console d’applications.
seo-description: Suivez cette page pour en savoir plus sur la création et la modification d’applications à l’aide de la console d’applications.
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Création et modification d’applications à l’aide de la console d’applications{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le processus de développement des applications mobiles AEM reconnaît que les utilisateurs de différentes compétences contribuent au développement des applications mobiles. Le mappage de processus suivant illustre l’ordre général dans lequel les auteurs de contenu et les développeurs d’applications exécutent les tâches.

![chlimage_1-10](assets/chlimage_1-10.gif)

Des informations sur la manière d’exécuter les tâches du marketeur apparaissent sur cette page. Pour plus d’informations sur les tâches des développeurs, voir Création d’applications PhoneGap.

## La structure des applications mobiles {#the-structure-of-mobile-applications}

AEM Mobile fournit le plan directeur de l&#39;application PhoneGap pour la création d&#39;applications mobiles. Le plan directeur définit la structure des applications que vous créez. Les applications se composent des éléments suivants :

* Page racine.
* Variations de langue de l’application.
* Page d’accueil de la variation de langue.

### La racine d&#39;une application PhoneGap {#the-root-of-a-phonegap-app}

La page racine des applications mobiles que vous créez dans AEM s’affiche dans la console Applications.

La page racine est stockée sous la propriété Chemin de destination de l’application spécifiée lors de la création de l’application (le chemin par défaut est /content/phonegap/apps). Le nom de la page est la propriété Name de l’application. Par exemple, l’URL par défaut de la page racine du site nommé `myphonegapapp` est `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### Variation de langue d’une application PhoneGap {#the-language-variation-of-a-phonegap-app}

Les premières pages enfants de la page racine sont les variations de langue de l’application. Le nom de chaque page correspond à la langue de création de l’application. Par exemple, l’anglais est le nom de la variante anglaise de l’application.

**** Remarque : Le modèle PhoneGap par défaut crée uniquement une application en anglais. Votre développeur peut modifier le plan directeur afin de créer plus de variations de langage.

![chlimage_1-147](assets/chlimage_1-147.png)

La page de langue a deux objectifs :

* Le contenu de la page correspond à la page de la variation linguistique de l’application.
* Les propriétés de la page contrôlent plusieurs aspects de la conception de l’application, tels que l’URL à utiliser pour demander des mises à jour de contenu, ainsi que des informations sur la connexion à la version cloud et à l’intégration d’Adobe Analytics Services.

![chlimage_1-148](assets/chlimage_1-148.png)

### Page d’accueil {#the-home-page}

La page d&#39;accueil, ou page index.html d&#39;une variante de langue d&#39;une application, s&#39;affiche à l&#39;ouverture de l&#39;application. La page d&#39;accueil fournit aux utilisateurs un menu de liens vers diverses pages de l&#39;application. Le système de paragraphe vous permet d’ajouter des composants à la page pour la création de contenu.

## Création d’une application mobile {#creating-a-mobile-application}

Les applications mobiles reposent sur un plan directeur qui définit une structure de page et des propriétés. Vous pouvez configurer les propriétés d’application suivantes :

* **** Titre : Titre de l’application.
* **** Chemin de destination : Emplacement dans le référentiel où l’application est stockée. Conservez la valeur par défaut pour créer un chemin d’accès basé sur le nom de l’application.

* **** Nom : La valeur par défaut est la valeur de la propriété Title avec suppression des espaces. Le nom est utilisé dans CQ pour faire référence à l’application, par exemple pour le noeud de référentiel qui représente l’application.
* **** Description : Description de l’application.
* **** URL du serveur : L’URL qui fournit du contenu en direct (OTA) est mise à jour vers l’application. La valeur par défaut est l’URL du serveur de publication de l’instance utilisée pour créer une application (provenant du service externalizer). Remarque : il doit s’agir d’une instance de serveur de publication plutôt que d’un auteur, ce qui nécessite une authentification.

Vous pouvez également fournir un fichier image à utiliser comme miniature de l’application, sélectionner la configuration PhoneGap Build à utiliser et sélectionner la configuration d’analyse des applications mobiles à utiliser. Cette image est uniquement utilisée comme miniature pour représenter votre application mobile dans la console des applications mobiles dans Experience Manager.

Il existe d’autres onglets (et facultatifs) pour créer un service cloud et intégrer le module Adobe Mobile Services SDK dans votre application.

* Créer : Cliquez sur Gérer les configurations et configurez votre service de génération build.phonegap.com ici. Ensuite, à partir de la liste déroulante, vous pourrez sélectionner le nouveau service PhoneGap Build Cloud.
* Analytics : Cliquez sur Gérer les configurations et configurez votre service cloud SDK [](https://marketing.adobe.com/developer/en_US/get-started/mobile/c-measuring-mobile-applications) Adobe Mobile Services. Ensuite, à partir de la liste déroulante, vous pourrez sélectionner le nouveau service mobile à intégrer dans votre application mobile.

>[!NOTE]
>
>Les développeurs peuvent utiliser le kit de démarrage AEM PhoneGap pour créer des applications et les ajouter à la console.

La procédure suivante utilise l’interface utilisateur tactile pour créer une application mobile.

1. Dans le rail, cliquez sur Applications.
1. Cliquez ou appuyez sur l’icône Créer.

   ![](do-not-localize/chlimage_1-7.png)

1. (Facultatif) Dans l’onglet Avancé, fournissez une description de l’application et modifiez l’URL du serveur si nécessaire.
1. (Facultatif) Si vous utilisez PhoneGap Build pour compiler l’application, sélectionnez Configuration à utiliser dans l’onglet Créer.

   Pour créer une configuration de génération PhoneGap, cliquez sur Gérer les configurations.

1. (Facultatif) Si vous utilisez SiteCatalyst pour suivre l’activité de l’application, sélectionnez la configuration à utiliser dans l’onglet Analytics.

   Pour créer une configuration d’application mobile, cliquez sur Gérer les configurations.

1. (Facultatif) Pour afficher une icône d’application, cliquez sur le bouton Parcourir, sélectionnez le fichier image dans votre système de fichiers, puis cliquez sur Ouvrir.
1. Cliquez sur Créer.

### Modification des propriétés d’une application mobile {#changing-the-properties-of-a-mobile-application}

Après avoir créé une application mobile, vous pouvez modifier ses propriétés.

#### Modification du titre, de la description et de l’icône {#change-the-title-description-and-icon}

1. Dans le rail, cliquez ou appuyez sur Applications.
1. Sélectionnez l’application à configurer, puis cliquez sur l’icône Afficher les propriétés de la page.

   ![](do-not-localize/chlimage_1-8.png)

1. Pour modifier les valeurs de propriété, cliquez ou appuyez sur l’icône Modifier.

   ![](do-not-localize/chlimage_1-9.png)

1. Configurez les propriétés de base et avancées, puis cliquez ou appuyez sur l’icône Terminé.

   ![](do-not-localize/chlimage_1-10.png)

#### Configuration d’une variante de langue de l’application {#configure-a-language-variation-of-the-application}

1. Dans le rail, cliquez ou appuyez sur Applications.
1. Cliquez sur pour accéder à l’application mobile que vous souhaitez modifier dans la console d’administration des applications. Sélectionnez la version linguistique de l’application à configurer, puis cliquez sur l’icône Afficher les propriétés de l’application.

   ![](do-not-localize/chlimage_1-11.png)

1. Pour modifier les valeurs de propriété, cliquez ou appuyez sur l’icône Modifier.

   ![](do-not-localize/chlimage_1-12.png)

1. Configurez les propriétés dans les onglets Simple, Avancé, Créer et Analytics, puis cliquez ou appuyez sur l’icône Terminé.

   ![](do-not-localize/chlimage_1-13.png)

### Création du contenu d’une application mobile {#authoring-the-content-of-a-mobile-application}

Après avoir créé l’application mobile, ajoutez le contenu utilisé comme interface utilisateur de l’application.

1. Dans le rail, cliquez ou appuyez sur Applications.
1. Cliquez ou appuyez sur l’application, puis cliquez ou appuyez sur Anglais.
1. Modifiez la page d’accueil ou ajoutez des pages enfants selon vos besoins.

### Déplacement de contenu vers des applications mobiles {#moving-content-to-mobile-applications}

Le cache de synchronisation de contenu sur l’instance de publication AEM est utilisé comme référentiel de contenu pour les applications mobiles :

* Le contenu du cache Content Sync est inclus dans l’application lorsque les développeurs compilent l’application.
* Le contenu du cache est disponible pour les applications mobiles installées pour la mise à jour du contenu de l’application.

Les applications mobiles comprennent une commande Mises à jour qui télécharge et installe le contenu de l’application mis à jour. Lorsqu’une instance d’application envoie une demande de mise à jour, Content Sync détermine le contenu qui a changé depuis la dernière mise à jour ou installation de l’application et fournit le nouveau contenu.

![chlimage_1-149](assets/chlimage_1-149.png)

Pour rendre le contenu mis à jour disponible pour les applications, mettez à jour le cache de synchronisation de contenu. Lors de la première mise à jour du cache, tout le contenu publié est ajouté. Les mises à jour suivantes ajoutent uniquement le contenu publié qui a changé depuis la mise à jour précédente.

Content Sync effectue également le suivi des mises à jour. Grâce à ces informations, Content Sync peut déterminer la mise à jour du cache à envoyer à une application mobile.

Procédez comme suit sur l’instance où vous souhaitez mettre à jour le cache. Par exemple, si votre application demande des mises à jour à partir de l’instance de publication, effectuez la procédure sur l’instance de publication.

1. Dans le rail, cliquez ou appuyez sur Applications, puis cliquez ou appuyez sur votre application.
1. Sélectionnez la page de démarrage, puis cliquez ou appuyez sur l’icône Mettre à jour le cache.

   ![](do-not-localize/chlimage_1-14.png)

### Utilisation de modèles d’application {#using-app-templates}

Cette fonctionnalité est disponible avec les applications 6.1 Feature Pack 2 et offre un moyen facile d’exploiter les modèles d’application existants pour créer de nouvelles applications dans AEM.

Qu’est-ce qu’un modèle d’application ? Considérez-le comme un ensemble de modèles de page et de composants qui représentent une base ou une base d’application.
Lors de la création d’une application basée sur le modèle d’une autre application, vous obtenez une application dont le point de départ est représentatif de l’application à partir de laquelle elle a été créée.

Vous devez disposer d’un modèle d’application mobile existant (ou d’une application installée avec un modèle d’application) pour pouvoir utiliser cette fonctionnalité.

Le dernier package d’exemples d’applications AEM 6.1 comprend une version mise à jour de l’application Geometrixx avec un modèle d’application. Vous pouvez également installer le StarterKit qui fournit également un modèle.

Procédure de création d’une application basée sur un modèle d’application :

1. Assurez-vous que le dernier pack de fonctionnalités et les exemples de packages de référence des applications AEM 6.1 sont installés
1. Cliquez sur Applications dans le rail de gauche.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Cliquez sur le bouton + Créer dans la partie supérieure et sélectionnez Créer une application.
1. Une fois que vous avez reçu la liste des modèles d’application, sélectionnez-en un :

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Cliquez sur Suivant.
1. Indiquez un ID d’application et un titre, mais vous pouvez également inclure un nom et une description.

   1. De plus, vous pouvez fournir un fichier PNG (format d’icône PhoneGap pris en charge) en tant qu’icône en parcourant les ressources AEM.
   1. Rappelez-vous que vous pouvez modifier tous ces champs une fois l’application créée dans le volet Gérer l’application. A l’exception de l’ID d’application, une fois l’ID d’application défini, vous ne pouvez plus le modifier.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Cliquez sur le bouton Créer, vous obtiendrez 2 options, Terminé (revenir à la vue catalogue des applications) ou Gérer l’application (ouvre le tableau de bord de l’application).
1. Une fois créée, la nouvelle application doit apparaître dans le catalogue de l’application :

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Cliquez sur l’application pour l’ouvrir. Vous avez créé une nouvelle application à partir du modèle d’une application existante.

>[!NOTE]
>
>Si vous désinstallez le package d’application de référence Geometrixx Outdoors d’AEM et si vous avez créé une application basée sur son modèle, cette application ne sera plus fonctionnelle. L’application Geometrixx Outdoors peut être supprimée, mais le modèle d’application doit rester s’il est utilisé par d’autres applications mobiles.

## Exploration de l’application Geometrixx Outdoors {#exploring-the-sample-geometrixx-outdoors-app}

L’application Geometrixx Outdoors est un exemple d’application PhoneGap qui présente les fonctionnalités du modèle d’application PhoneGap par défaut et des exemples de composants mobiles.

Pour ouvrir l’application, cliquez sur Applications mobiles dans le rail, puis sélectionnez Application Geometrixx Outdoors.

### Fonctionnalités courantes de la page - Application mobile Geometrixx {#common-page-features-geometrixx-mobile-app}

Chaque page de l’application mobile comprend les fonctionnalités suivantes :

* Bouton Retour permettant de revenir à la page parente. Notez que le bouton Précédent n’apparaît pas sur la page d’accueil.
* Un rail extensible qui propose un menu de commandes et de liens :

   * Ouvrez la page Emplacements.
   * Ouvrez le panier.
   * Connectez-vous.
   * Mettez à jour l’application.

* Système de paragraphe, permettant d’ajouter des composants et de créer du contenu.

### Page d’accueil - Application mobile Geometrixx {#the-home-page-geometrixx-mobile-app}

Le contenu de la page d’accueil comprend les outils de navigation suivants :

* Composant de liste de menus qui fournit des liens vers les pages enfants Gear, Reviews, News et About Us.
* Composant du carrousel de glissement qui présente les pages enfants.

### Page d&#39;engrenage - Application mobile Geometrixx {#the-gear-page-geometrixx-mobile-app}

La page Engrenage permet aux utilisateurs d’accéder aux pages de produits. Un composant de liste de menus permet d’accéder aux pages enfants de la page d’engrenage. Les pages enfants sont des catégories de produits que le site Web propose.

* Saison
* Vêtements
* Sexe
* Activité

Chaque page de catégorie utilise la même structure de contenu que la page d’engrenage. Le carrousel donne accès aux pages enfants qui sont des sous-catégories de produits. Les pages de sous-catégorie contiennent des listes de produits qui fournissent des liens vers les pages de produits.

### Page Produits - Application mobile Geometrixx {#the-products-page-geometrixx-mobile-app}

La page Produits et son héritage de pages enfants implémentent un système de classification pour les pages de produits. Les pages les plus basses de chaque branche de l&#39;hiérarchie sont une page de produit qui contient un composant Produit ng.

La page Produits n’est pas disponible pour les utilisateurs de l’application. La page Engrenage donne accès à chaque page de produit.

### Page d’avis - Application mobile Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contient un bouton Retour. Le système de paragraphe vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page Révisions est disponible à partir du carrousel sur la page en anglais.

### Page d&#39;actualités - Application mobile Geometrixx {#the-news-page-geometrixx-mobile-app}

Contient un bouton Retour. Le système de paragraphe vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page Actualités est accessible à partir du carrousel sur la page en anglais.

### Page À notre sujet - Application mobile Geometrixx {#the-about-us-page-geometrixx-mobile-app}

La page Qui sommes-nous contient plusieurs composants de ligne à deux colonnes. Chaque colonne contient une image ou un composant Texte. Les composants sont modifiables et le système de paragraphe vous permet d’ajouter des composants.

Lors de l’utilisation de l’application, la page Qui sommes-nous est disponible à partir du carrousel sur la page en anglais.

### Page Emplacements - Application mobile Geometrixx {#the-locations-page-geometrixx-mobile-app}

La page Emplacements contient un composant Emplacements.

Lors de l’utilisation de l’application, la page Emplacements est disponible dans la liste des menus de la page en anglais.

## Exemples de composants mobiles {#sample-mobile-components}

Plusieurs composants sont immédiatement disponibles dans Sidekick lors de la création des pages d’une application mobile. Les composants appartiennent au groupe de composants PhoneGap.

### Carrousel de balayage {#swipe-carousel}

Le composant du carrousel de glissement est un outil de présentation et de navigation des pages du site. Le composant comprend un carrousel qui passe en revue les images des pages au-dessus d’une liste de liens de page. Modifiez le composant pour spécifier les pages à exposer et le comportement du carrousel.

Notez que les images apparaissent dans le carrousel pour les pages associées à une image d’une manière spécifique. Lorsque des pages ne sont pas associées à des images, seule la liste des liens apparaît.

![chlimage_1-151](assets/chlimage_1-151.png)

**Panneau Propriétés du carrousel**

Configurez le comportement du carrousel :

* Vitesse de lecture : Temps, en millisecondes, d’affichage de chaque image avant l’affichage de l’image suivante.
* Temps de transition : Durée, en millisecondes, de l’animation pour les transitions d’image.
* Style des commandes : Type de commandes fournies pour le déplacement entre les images.

**Onglet Propriétés de liste**

Spécifiez le mode de génération de la liste des pages :

* Créer une liste à l’aide de : Méthode à utiliser pour spécifier les pages à inclure dans le carrousel. Voir Création de la liste des pages.
* Order By : Sélectionnez une propriété de page à utiliser pour trier la liste des pages. Par exemple, sélectionnez jcr:title pour trier les pages par ordre alphabétique de titre.
* Limite : Nombre maximal de pages à inclure. Cette propriété est appropriée pour les méthodes de recherche de création de la liste des pages.

#### Création de la liste des pages {#building-the-page-list}

Le composant Glissement de carrousel fournit les valeurs suivantes pour la propriété Build List Using. La boîte de dialogue Modifier change en fonction de la valeur que vous sélectionnez :

**Pages enfants**

Le composant répertorie toutes les pages enfants d’une page spécifique. Après avoir sélectionné cette valeur, sélectionnez la page dans l’onglet Pages enfants ou ne spécifiez aucune valeur pour répertorier les enfants de la page active.

**Liste fixe**

Spécifiez une liste de pages d’inclusion. Après avoir sélectionné cette valeur, configurez la liste dans l’onglet Liste fixe qui s’affiche lorsque vous sélectionnez Liste fixe :

* Pour ajouter une page, cliquez sur Ajouter un élément, puis recherchez la page.
* Utilisez les icônes de flèche vers le haut et vers le bas pour déplacer la page dans la liste.
* Cliquez sur le bouton Supprimer pour supprimer une page de la liste.

La propriété Ordre par n’affecte pas l’ordre des listes fixes.

**Rechercher**

Renseignez la liste à l’aide des résultats d’une recherche par mot-clé. La recherche est effectuée dans les enfants d’une page que vous spécifiez :

1. Pour spécifier la page racine de la recherche, utilisez la propriété Démarrer dans pour sélectionner le chemin de la page. Ne spécifiez aucun chemin à rechercher sous la page active.
1. Dans la propriété Requête de recherche, saisissez les mots-clés de recherche.

**Recherche avancée**

Renseignez la liste à l’aide d’une requête [Querybuilder](/help/sites-developing/querybuilder-api.md) .

### Image {#image}

Ajoutez une image au contenu de votre application.

### Texte {#text}

Ajoutez du texte enrichi au contenu de votre application.

### Emplacements de magasin {#store-locations}

Le composant Emplacements de la boutique fournit aux utilisateurs des outils pour rechercher des points de vente :

* Rechercher
* Liste des emplacements proches ou éloignés des coordonnées GPS du dispositif.

Le composant nécessite que le référentiel contienne des informations d’emplacement pour chaque magasin. Les exemples d’emplacement sont installés sur le noeud /etc/commerce/locations/adobe. ![chlimage_1-152](assets/chlimage_1-152.png)

### Ligne à deux colonnes {#two-column-row}

Permet d’ajouter des composants côte à côte à une page.

![chlimage_1-153](assets/chlimage_1-153.png)
