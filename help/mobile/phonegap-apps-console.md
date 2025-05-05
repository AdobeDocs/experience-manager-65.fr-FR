---
title: Création et modification d’applications à l’aide de la console Applications
description: Consultez cette page pour en savoir plus sur la création et la modification d’applications à l’aide de la console applications.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2654'
ht-degree: 1%

---

# Création et modification d’applications à l’aide de la console Applications{#creating-and-editing-apps-using-the-apps-console}

{{ue-over-mobile}}

Le processus de développement des applications mobiles d&#39;AEM reconnaît que les utilisateurs de différentes expertises contribuent au développement des applications mobiles. La cartographie des processus suivante illustre l’ordre général dans lequel les auteurs de contenu et les développeurs d’applications effectuent les tâches.

![chlimage_1-10](assets/chlimage_1-10.gif)

Les informations sur l’exécution des tâches du spécialiste marketing s’affichent sur cette page. Pour plus d’informations sur les tâches du développeur, voir Création d’applications PhoneGap.

## Structure des applications mobiles {#the-structure-of-mobile-applications}

AEM Mobile fournit le plan directeur de l’application Phonegap pour la création d’applications mobiles. Le plan directeur définit la structure des applications que vous créez. Les applications se composent des éléments suivants :

* Page racine.
* Variantes linguistiques de l’application.
* Page d’accueil de la variation de langue.

### Racine d’une application téléphonique {#the-root-of-a-phonegap-app}

La page principale des applications mobiles que vous créez dans AEM s’affiche dans la console Applications.

La page racine est stockée sous la propriété Chemin de destination de l’application qui a été spécifiée lors de la création de l’application (le chemin par défaut est /content/phonegap/apps). Le nom de la page est la propriété Nom de l’application. Par exemple, l’URL par défaut de la page racine du site nommé `myphonegapapp` est `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### Variante linguistique d’une application PhoneGap {#the-language-variation-of-a-phonegap-app}

Les premières pages enfants de la page racine sont les variations de langue de l’application. Le nom de chaque page correspond à la langue pour laquelle l’application est créée. Par exemple, « English » est le nom de la variante anglaise de l’application.

**Remarque :** le plan directeur PhoneGap par défaut crée uniquement une application en anglais. Votre développeur peut modifier le plan directeur afin de pouvoir créer d’autres variations de langue.

![chlimage_1-147](assets/chlimage_1-147.png)

La page Langue a deux objectifs :

* Le contenu de la page est la page de spash pour la variation de langue de l’application.
* Les propriétés de page contrôlent plusieurs aspects de conception de l’application, tels que l’URL à utiliser pour demander des mises à jour de contenu et les informations sur la connexion à la version cloud et l’intégration des services Adobe Analytics.

![chlimage_1-148](assets/chlimage_1-148.png)

### La page d’accueil {#the-home-page}

La page d&#39;accueil, ou page index.html, d&#39;une variation de langue d&#39;une application apparaît à l&#39;ouverture de l&#39;application. La page d’accueil fournit aux utilisateurs et utilisatrices un menu de liens vers différentes pages de l’application. Le système de paragraphes permet d’ajouter des composants à la page pour créer du contenu.

## Création d’une application mobile {#creating-a-mobile-application}

Les applications mobiles sont basées sur un plan directeur qui définit une structure et des propriétés de page. Vous pouvez configurer les propriétés d’application suivantes :

* **Titre :** le titre de l’application.
* **Chemin de destination :** emplacement dans le référentiel où l’application est stockée. Conservez la valeur par défaut pour créer un chemin d’accès en fonction du nom de l’application.

* **Name :** la valeur par défaut est la valeur de la propriété Title avec les espaces supprimés. Le nom est utilisé dans CQ pour faire référence à l’application, par exemple, pour le nœud de référentiel qui représente l’application.
* **Description :** une description de l’application.
* **URL du serveur :** l’URL qui fournit des mises à jour de contenu par voie hertzienne (OTA) à l’application. La valeur par défaut est l’URL du serveur de publication de l’instance utilisée pour créer une application (provenant du service d’externaliseur). Notez qu’il doit s’agir d’une instance de serveur de publication plutôt que d’un auteur, ce qui nécessite une authentification.

Vous pouvez également fournir un fichier image à utiliser comme miniature de l’application, sélectionner la configuration de PhoneGap Build à utiliser, puis sélectionner la configuration d’analyse des applications mobiles à utiliser. Cette image est uniquement utilisée sous forme de miniature pour représenter votre application mobile dans la console des applications mobiles dans Experience Manager.

Il existe d’autres onglets (facultatifs) pour créer le service cloud et intégrer le plug-in SDK Adobe Mobile Services dans votre application.

* Build : cliquez sur gérer les configurations et configurez votre service de build build.phonegap.com ici. Ensuite, dans la liste déroulante, vous pourrez sélectionner le service cloud PhoneGap build que vous venez de créer.
* Analytics : cliquez sur Gérer les configurations et configurez votre service cloud [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=fr). Ensuite, dans la liste déroulante, vous pourrez sélectionner le service mobile nouvellement créé à intégrer à votre application mobile.

>[!NOTE]
>
>Les développeurs peuvent utiliser le kit de démarrage AEM PhoneGap pour créer des applications et les ajouter à la console.

La procédure suivante utilise l’interface utilisateur tactile pour créer une application mobile.

1. Sur le rail, cliquez sur Applications.
1. Cliquez sur l’icône Créer .

   ![Icône Créer indiquée par un signe plus à l’intérieur d’un carré.](do-not-localize/chlimage_1-7.png)

1. (Facultatif) Dans l’onglet Avancé , fournissez une description de l’application et modifiez l’URL du serveur si nécessaire.
1. (Facultatif) Si vous utilisez PhoneGap Build pour compiler l’application, dans l’onglet Créer , sélectionnez la Configuration à utiliser.

   Pour créer une configuration de build PhoneGap, cliquez sur Gérer les configurations.

1. (Facultatif) Si vous utilisez SiteCatalyst pour suivre l’activité de l’application, dans l’onglet Analytics , sélectionnez la configuration à utiliser.

   Pour créer une configuration d’application mobile, cliquez sur Gérer les configurations.

1. (Facultatif) Pour fournir une icône d’application, cliquez sur le bouton Parcourir , sélectionnez le fichier image dans votre système de fichiers, puis cliquez sur Ouvrir.
1. Cliquez sur Créer.

### Modification des propriétés d’une application mobile {#changing-the-properties-of-a-mobile-application}

Après avoir créé une application mobile, vous pouvez modifier les propriétés.

#### Modifier le titre, la description et l’icône {#change-the-title-description-and-icon}

1. Sur le rail, cliquez sur Applications.
1. Sélectionnez l’application à configurer, puis cliquez sur l’icône Afficher les propriétés de la page .

   ![Icône Afficher les propriétés de page indiquée par la lettre I dans un cercle.](do-not-localize/chlimage_1-8.png)

1. Pour modifier les valeurs de propriété, cliquez sur l’icône Modifier .

   ![Icône Modifier indiquée par un crayon.](do-not-localize/chlimage_1-9.png)

1. Configurez les propriétés De base et Avancé , puis cliquez sur l’icône Terminé .

   ![Icône Terminé signalée par une coche.](do-not-localize/chlimage_1-10.png)

#### Configuration d’une variante linguistique de l’application {#configure-a-language-variation-of-the-application}

1. Sur le rail, cliquez sur Applications.
1. Cliquez pour explorer l’application mobile que vous souhaitez modifier dans l’Admin Console d’applications. Sélectionnez la version linguistique de l’application à configurer et cliquez sur l’icône Afficher les propriétés de l’application .

   ![Icône Afficher les propriétés de l&#39;application indiquée par la lettre I dans un cercle.](do-not-localize/chlimage_1-11.png)

1. Pour modifier les valeurs de propriété, cliquez sur l’icône Modifier .

   ![Icône Modifier indiquée par un crayon.](do-not-localize/chlimage_1-12.png)

1. Configurez les propriétés sur les onglets De base, Avancé, Build et Analytics, puis cliquez sur l’icône Terminé .

   ![Icône Terminé signalée par une coche.](do-not-localize/chlimage_1-13.png)

### Création du contenu d’une application mobile {#authoring-the-content-of-a-mobile-application}

Après avoir créé l’application mobile, ajoutez le contenu utilisé comme interface utilisateur de l’application.

1. Sur le rail, cliquez sur Applications.
1. Cliquez sur l&#39;application, puis sur Français.
1. Modifiez la page d’accueil ou ajoutez des pages enfants selon vos besoins.

### Déplacement de contenu vers des applications mobiles {#moving-content-to-mobile-applications}

Le cache de synchronisation de contenu sur l’instance de publication AEM est utilisé comme référentiel de contenu pour les applications mobiles :

* Le contenu du cache de synchronisation du contenu est inclus dans l’application lorsque les développeurs la compilent.
* Le contenu du cache est disponible pour les applications mobiles installées afin de mettre à jour le contenu de l’application.

Les applications mobiles incluent une commande Mises à jour qui télécharge et installe le contenu de l’application mis à jour. Lorsqu’une instance d’application envoie une demande de mise à jour, la synchronisation de contenu détermine quel contenu a été modifié depuis la dernière mise à jour ou installation de l’application et fournit le nouveau contenu.

![chlimage_1-149](assets/chlimage_1-149.png)

Pour mettre le contenu mis à jour à la disposition des applications, mettez à jour le cache de synchronisation du contenu. La première fois que vous mettez à jour le cache, tout le contenu publié est ajouté. Les mises à jour suivantes ajoutent uniquement le contenu publié qui a été modifié depuis la mise à jour précédente.

La synchronisation de contenu effectue également le suivi des mises à jour. Grâce à ces informations, la synchronisation de contenu peut déterminer la mise à jour du cache à envoyer à une application mobile.

Effectuez la procédure suivante sur l’instance sur laquelle vous souhaitez mettre à jour le cache. Par exemple, si votre application demande des mises à jour à l’instance de publication, effectuez la procédure sur l’instance de publication.

1. Sur le rail, cliquez sur Applications, puis sur votre application.
1. Sélectionnez la page de démarrage, puis cliquez sur l’icône Mettre à jour le cache .

   ![Icône Mettre à jour le cache indiquée par un canon rayé recouvert d’un symbole de recyclage.](do-not-localize/chlimage_1-14.png)

### Utilisation de modèles d’application {#using-app-templates}

Il s’agit d’une fonctionnalité disponible dans le pack de fonctionnalités 2 d’Apps 6.1. Elle permet d’utiliser facilement les modèles d’application existants pour créer de nouvelles applications dans AEM.

Qu’est-ce qu’un modèle d’application ? Considérez-le comme un ensemble de modèles de page et de composants qui représentent une ligne de base ou la base d’une application.
Lors de la création d’une application basée sur le modèle d’une autre application, vous obtiendrez une application qui dispose d’un point de départ représentatif de l’application à partir de laquelle elle a été créée.

Pour utiliser cette fonctionnalité, vous devez disposer d’un modèle d’application mobile existant (ou d’une application installée disposant d’un modèle d’application).

Le dernier package d’exemples d’AEM Apps 6.1 comprend une version mise à jour de l’application Geometrixx avec un modèle d’application. Vous pouvez également installer le StarterKit qui fournit également un modèle.

Étapes de création d’une application basée sur un modèle d’application :

1. Assurez-vous d’avoir installé le dernier pack de fonctionnalités et les packages d’exemples de référence d’AEM Apps 6.1
1. Cliquez sur Applications dans le rail de gauche.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Cliquez sur le bouton + Créer en haut et sélectionnez Créer une application.
1. Une fois que la liste des modèles d’application vous est présentée, sélectionnez-en un :

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Cliquez sur Suivant.
1. Fournissez un titre et un identifiant d’application, mais vous pouvez également inclure un nom et une description.

   1. En outre, vous pouvez fournir un fichier PNG (format d’icône PhoneGap pris en charge) sous forme d’icône en parcourant les ressources AEM.
   1. Pour rappel, vous pouvez modifier tous ces champs une fois l’application créée dans la mosaïque Gérer l’application . À l’exception de l’ID d’application, une fois l’ID d’application défini, vous ne pouvez pas le modifier.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Cliquez sur le bouton Créer pour voir s’afficher 2 options : Terminé (revenez à la vue Catalogue d’applications) ou Gérer l’application (ouvre le tableau de bord de l’application).
1. Une fois créée, la nouvelle application doit s’afficher dans le catalogue d’applications :

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Cliquez sur l’application pour l’ouvrir. Vous avez créé une application basée sur le modèle d’une application existante.

>[!NOTE]
>
>Si vous désinstallez le package d’application de référence Geometrixx Outdoors d’AEM et qu’une application est créée en fonction de son modèle, cette application ne sera plus fonctionnelle. L’application Geometrixx Outdoors peut être supprimée. Toutefois, le modèle d’application doit rester s’il est utilisé par d’autres applications mobiles.

## Exploration de l’exemple d’application Geometrixx Outdoors {#exploring-the-sample-geometrixx-outdoors-app}

L’application Geometrixx Outdoors est un exemple d’application PhoneGap qui présente les fonctionnalités du plan directeur de l’application PhoneGap par défaut et les exemples de composants mobiles.

Pour ouvrir l’application, dans le rail, cliquez sur Applications mobiles , puis sélectionnez Application Geometrixx Outdoors .

### Fonctionnalités de page courantes - Application mobile Geometrixx {#common-page-features-geometrixx-mobile-app}

Chaque page de l’application mobile comprend les fonctionnalités suivantes :

* Un bouton Précédent pour revenir à la page parente. Le bouton Précédent n’apparaît pas sur la page d’accueil.
* Un rail extensible qui offre un menu de commandes et de liens :

   * Ouvrez la page Emplacements .
   * Ouvrez le panier .
   * Se connecter.
   * Mettez à jour l’application.

* Le système de paragraphes, pour ajouter des composants et créer du contenu.

### Page d’accueil - Application mobile Geometrixx {#the-home-page-geometrixx-mobile-app}

Le contenu de la page d’accueil se compose des outils de navigation suivants :

* Composant Liste de menus qui fournit des liens vers les pages enfants Engrenage, Révisions, Actualités et À propos de nous .
* Composant Carrousel de balayage qui affiche les pages enfants.

### La page sur l’engrenage - Application mobile Geometrixx {#the-gear-page-geometrixx-mobile-app}

La page Engrenage permet aux utilisateurs d’accéder aux pages de produits. Un composant Liste de menus permet d’accéder aux pages enfants de la page Engrenage. Les pages enfants sont des catégories de produits présentées sur le site Web.

* Saison
* Habillement
* Genre
* Activity

Chaque page de catégorie utilise la même structure de contenu que la page d’engrenage. Le carrousel permet d’accéder aux pages enfants qui sont des sous-catégories de produits. Les pages de sous-catégorie contiennent des listes de produits qui fournissent des liens vers des pages de produits.

### Page Produits - Application mobile Geometrixx {#the-products-page-geometrixx-mobile-app}

La page Produits et sa hiérarchie de pages enfants implémentent un système de classification pour les pages de produits. Les pages les plus basses de chaque branche de la hiérarchie sont des pages de produits contenant un composant de produit.

La page Produits n’est pas disponible pour les utilisateurs de l’application. La page Engrenage permet d’accéder à chaque page de produit.

### La page des avis - Application mobile Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contient un bouton Précédent. Le système de paragraphes permet d’ajouter des composants.

Lorsque vous utilisez l’application, la page Commentaires est disponible à partir du carrousel sur la page en anglais.

### La Page D’Actualités - Application Mobile Geometrixx {#the-news-page-geometrixx-mobile-app}

Contient un bouton Précédent. Le système de paragraphes permet d’ajouter des composants.

Lorsque vous utilisez l’application , la page Informations est disponible à partir du carrousel sur la page en anglais.

### La Page À Propos De Nous - Application Mobile Geometrixx {#the-about-us-page-geometrixx-mobile-app}

La page À propos de nous contient plusieurs composants Deux lignes de colonne. Chaque colonne contient un composant Image ou Texte . Les composants sont modifiables et le système de paragraphe permet d’ajouter des composants.

Lorsque vous utilisez l’application , la page À propos de nous est disponible à partir du carrousel sur la page en anglais.

### Page Emplacements - Application mobile Geometrixx {#the-locations-page-geometrixx-mobile-app}

La page Emplacements contient un composant Emplacements .

Lors de l’utilisation de l’application, la page Emplacements est disponible à partir de la liste de menus de la page English .

## Exemples de composants mobiles {#sample-mobile-components}

Plusieurs composants sont immédiatement disponibles dans Sidekick lors de la création des pages d’une application mobile. Les composants appartiennent au groupe de composants PhoneGap .

### Carrousel de balayage {#swipe-carousel}

Le composant Carrousel de balayage est un outil permettant de présenter et de parcourir les pages d’un site. Le composant comprend un carrousel qui parcourt les images des pages au-dessus d’une liste de liens de page. Modifiez le composant pour spécifier les pages à exposer et le comportement du carrousel.

Notez que les images apparaissent dans le carrousel pour les pages qui sont associées à une image d’une manière spécifique. Lorsque les pages ne sont pas associées à des images, seule la liste des liens apparaît.

![chlimage_1-151](assets/chlimage_1-151.png)

**Onglet Propriétés du carrousel**

Configurez le comportement du carrousel :

* Vitesse de lecture : temps en millisecondes pendant lequel chaque image s’affiche avant d’afficher l’image suivante.
* Temps de transition : durée en millisecondes de l’animation pour les transitions d’image.
* Style des contrôles : type des contrôles fournis pour le déplacement entre les images.

**Onglet Propriétés de la liste**

Spécifiez le mode de génération de la liste de pages :

* Créer la liste à l’aide de : méthode à utiliser pour spécifier les pages à inclure dans le carrousel. Voir Création de la liste de pages.
* Classer par : permet de sélectionner une propriété de page à utiliser pour trier la liste de pages. Par exemple, sélectionnez jcr:title pour trier les pages par titre dans l’ordre alphabétique.
* Limite : nombre maximal de pages à inclure. Cette propriété est appropriée pour les méthodes de recherche de création de la liste de pages.

#### Création de la liste de pages {#building-the-page-list}

Le composant Carrousel de balayage fournit les valeurs suivantes pour la propriété Créer la liste à l’aide de . La boîte de dialogue de modification change en fonction de la valeur sélectionnée :

**Pages enfants**

Le composant répertorie toutes les pages enfants d’une page spécifique. Après avoir sélectionné cette valeur, sélectionnez la page dans l’onglet Pages enfants ou ne spécifiez aucune valeur pour répertorier les enfants de la page active.

**Liste fixe**

Spécifiez une liste de pages à inclure. Après avoir sélectionné cette valeur, configurez la liste dans l’onglet Liste fixe qui s’affiche lorsque vous sélectionnez Liste fixe :

* Pour ajouter une page, cliquez sur Ajouter un élément, puis recherchez la page.
* Utilisez les icônes fléchées vers le haut et vers le bas pour déplacer la page dans la liste.
* Cliquez sur le bouton Supprimer pour supprimer une page de la liste.

La propriété Order By n’affecte pas l’ordre des listes fixes.

**Recherche**

Renseignez la liste à l’aide des résultats d’une recherche par mot-clé. La recherche est effectuée dans les enfants d’une page que vous spécifiez :

1. Pour spécifier la page racine de la recherche, utilisez la propriété Début dans pour sélectionner le chemin d’accès à la page. Ne spécifiez aucun chemin d’accès à rechercher sous la page active.
1. Dans la propriété Requête de recherche , saisissez les mots-clés de recherche.

**Recherche avancée**

Renseignez la liste à l’aide d’une requête [QueryBuilder](/help/sites-developing/querybuilder-api.md).

### Image {#image}

Ajoutez une image au contenu de votre application.

### Texte {#text}

Ajoutez du texte enrichi au contenu de votre application.

### Emplacements de magasin {#store-locations}

Le composant Emplacements de magasin fournit aux utilisateurs des outils permettant de trouver des points de vente professionnels :

* Recherche
* Listes des emplacements proches ou distants des coordonnées GPS de l’appareil.

Le composant nécessite que le référentiel contienne des informations d’emplacement pour chaque magasin. Les exemples d’emplacement sont installés sur le nœud /etc/commerce/locations/adobe . ![chlimage_1-152](assets/chlimage_1-152.png)

### Ligne à deux colonnes {#two-column-row}

Permet d’ajouter des composants côte à côte à une page.

![chlimage_1-153](assets/chlimage_1-153.png)
