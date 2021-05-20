---
title: eCommerce
description: AEM eCommerce aide les spécialistes du marketing à offrir des expériences d’achat personnalisées sur le web, les appareils mobiles et les médias sociaux.
topic-tags: e-commerce
content-type: reference
docset: aem65
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 88%

---

# eCommerce{#ecommerce}

* [Concepts ](/help/commerce/cif-classic/administering/concepts.md)
* [Administration (générique)](/help/commerce/cif-classic/administering/generic.md)

Adobe propose deux versions de la structure d’intégration de Commerce :

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF sur site</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versions d’AEM prises en charge</p> </td>
   <td><p>AEM sur site ou AMS 6.x</p> </td>
   <td>AEM AMS 6.4 et 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Intégration monolithique, mappage pré-build (modèle)</li>
     <li>Référentiel JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Magento</li>
     <li>Java et Javascript</li>
     <li>Aucune donnée de commerce stockée dans le référentiel JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Frontal</p> </td>
   <td><p>Pages rendues côté serveur AEM</p> </td>
   <td>Application de page mixte (rendu hybride)</td>
  </tr>
  <tr>
   <td><p>Catalogue de produits</p> </td>
   <td>
    <ul>
     <li>Importateur de produits, éditeur, mise en cache dans AEM</li>
     <li>Catalogues réguliers avec AEM ou pages proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Aucune importation de produit</li>
     <li>Modèles génériques</li>
     <li>Données à la demande via connecteur</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Évolutivité</p> </td>
   <td>
    <ul>
     <li>Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation)</li>
     <li>Mise en cache sur le Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Aucune limite de volume</li>
     <li>Mise en cache sur le Dispatcher ou le réseau de diffusion de contenu</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modèle de données normalisé</td>
   <td>Non</td>
   <td>Oui, schéma GraphQL Magento</td>
  </tr>
  <tr>
   <td>Disponibilité</td>
   <td><p>Oui. SAP Commerce Cloud (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4</p> <p>Salesforce Commerce Cloud (connecteur en open source pour prendre en charge AEM 6.4)</p> </td>
   <td>Oui via open source via GitHub. Magento Commerce (prend en charge Magento 2.3.2 (par défaut) et compatible avec Magento 2.3.1).</td>
  </tr>
  <tr>
   <td>Quand utiliser la personnalisation</td>
   <td>Cas d’utilisation limités : par ex., dans le cas des scénarios dans lesquels de petits catalogues statiques doivent être importés</td>
   <td>Solution conseillée dans la plupart des cas d’utilisation</td>
  </tr>
 </tbody>
</table>

Conjointement avec la gestion d’informations sur les produits, eCommerce gère les activités d’un site web de vente de produits dans une boutique en ligne :

* Création, durée de vie et obsolescence d’un produit
* Gestion des tarifs
* Gestion des transactions
* Gestion de catalogues entiers
* Enregistrements de stockage directs et centralisés
* Interfaces web

AEM eCommerce aide les spécialistes du marketing à offrir des expériences d’achat personnalisées sur le web, les appareils mobiles et les médias sociaux. L’environnement de création d’AEM permet de personnaliser des pages et des composants en fonction du contexte du visiteur cible et des stratégies de marchandisage, par exemple :

* Pages de produits
* Composants de panier
* Composants de passage en caisse

La mise en œuvre d’eCommerce permet d’accéder en temps réel à des informations sur le produit. Il peut être utilisé pour veiller aux points suivants :

* Intégrité des informations sur le produit
* Tarifs
* Inventaire de gestion des stocks
* Variantes de l’état d’un panier

>[!NOTE]
>
>Pour utiliser la structure d’intégration avec les fournisseurs prestataires eCommerce externes, vous devez tout d’abord installer les modules nécessaires. Pour plus d’informations, voir [Déploiement d’eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Pour plus d’informations sur l’extension des fonctionnalités d’eCommerce, voir [Développement d’eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).

## Principales fonctionnalités {#main-features}

AEM eCommerce fournit ce qui suit :

* Un certain nombre de **composants d’AEM prêts à l’emploi** pour illustrer ce qui peut être réalisé pour votre projet :

   * Affichage des produits
   * Panier
   * Passage en caisse
   * Produits récemment affichés
   * Bons
   * Autres

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >La structure d’intégration d’AEM permet également de créer d’autres composants AEM pour les fonctions de commerce indépendamment de votre moteur eCommerce spécifique.

* **Recherche** : à l’aide de l’une des fonctions suivantes :

   * Recherche AEM
   * Recherche du système de commerce électronique
   * Recherche tierce (Search&amp;Promote par exemple)
   * Ou une combinaison de ces trois fonctions

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* Utilise la possibilité de **présenter votre contenu sur plusieurs canaux**, que ce soit sur la fenêtre de navigateur complète ou sur un appareil mobile. Ainsi, vous proposez votre contenu au format nécessaire pour vos visiteurs.

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* La possibilité de **développer votre propre mise en œuvre de l’intégration en fonction de la [structure d’AEM eCommerce](#the-framework)**.

   Les deux mises en œuvre actuellement disponibles reposent sur la même base et complètent l’API générale (la structure). La mise en œuvre d’une nouvelle intégration implique seulement de mettre en œuvre les fonctionnalités dont votre intégration a besoin. Les composants frontaux peuvent être utilisés par les nouvelles mises en œuvre puisqu’ils utilisent des interfaces (et sont donc indépendants de la mise en œuvre).

* Possibilité de développer un **commerce axé sur l’expérience en fonction des données et de l’activité des acheteurs**, et ce dans divers scénarios :

   * Par exemple, une réduction des frais de livraison proposée lorsque le montant total d’une commande dépasse un montant spécifique.
   * Autre exemple : la possibilité de proposer des offres à certaines occasions à partir des informations de profil (tel le lieu). Ces possibilités peuvent ensuite être mises en avant, là encore en fonction d’autres facteurs, si nécessaire.

   Dans l’exemple ci-dessous, un teaser est affiché lorsque le contenu du panier est inférieur à 75 $ :

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   Ceci peut être modifié lorsque le contenu du panier dépasse 75 $ :

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* Et d’autres fonctionnalités, dont :

   * Contenu du panier conservé d’une session à l’autre
   * Historique des commandes exhaustif
   * Mise à jour rapide du catalogue

## Structure {#the-framework}

La section [Concepts](/help/commerce/cif-classic/administering/concepts.md) couvre la structure plus en détail. Vous trouverez ci-dessous un aperçu de la structure :

### Quoi ? {#what}

* La structure d’intégration fournit l’API, une série de composants illustrant les fonctionnalités et différentes extensions pour fournir des exemples de méthodes de connexion.
* La structure fournit la structure de base nécessaire à la mise en œuvre d’un projet.
* La structure est extensible.
* La structure ne fournit pas de site prêt à l’emploi. Un certain travail de développement reste nécessaire pour adapter la structure à vos spécifications.

### Pourquoi ? {#why}

* Fournit les mécanismes de base nécessaires pour réaliser rapidement un site de commerce électronique personnalisé.
* Offrir la flexibilité nécessaire pour développer un site de commerce électronique réel.
* Illustrer les pratiques recommandées.
