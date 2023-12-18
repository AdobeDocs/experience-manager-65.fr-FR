---
title: Framework d’intégration d’e-commerce
description: AEM eCommerce aide les spécialistes du marketing à offrir des expériences d’achat personnalisées sur le web, les appareils mobiles et les médias sociaux.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: ht
source-wordcount: '749'
ht-degree: 100%

---

# eCommerce{#ecommerce}

* [Concepts](/help/commerce/cif-classic/administering/concepts.md)
* [Administration (générique)](/help/commerce/cif-classic/administering/generic.md)

Adobe propose deux versions de framework d’intégration de Commerce :

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF on-Prem</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versions d’AEM prises en charge</p> </td>
   <td><p>AEM On-Prem ou AMS 6.x</p> </td>
   <td>AEM AMS 6.4 et 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Intégration monolithique, mappage de prégénération (modèle)</li>
     <li>Référentiel JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java et JavaScript</li>
     <li>Aucune donnée de commerce stockée dans le référentiel JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>Pages générées côté serveur AEM</p> </td>
   <td>Application de page mixte (rendu hybride)</td>
  </tr>
  <tr>
   <td><p>Catalogue de produits</p> </td>
   <td>
    <ul>
     <li>Importateur de produit, éditeur, mise en cache dans AEM</li>
     <li>Catalogues réguliers avec les pages d’AEM ou de proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Aucune importation de produit</li>
     <li>Modèles génériques</li>
     <li>Données à la demande via le connecteur</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Évolutivité</p> </td>
   <td>
    <ul>
     <li>Peut prendre en charge jusqu’à quelques millions de produits (selon le cas d’utilisation)</li>
     <li>Mise en cache sur Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Aucune limitation de volume</li>
     <li>Mise en cache sur Dispatcher ou CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modèle de données normalisé</td>
   <td>Non</td>
   <td>Oui, schéma Adobe Commerce GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilité</td>
   <td><p>Oui. SAP Commerce Cloud (extension mise à jour pour prendre en charge AEM 6.4 et Hybris 5 (par défaut) et maintenir la compatibilité avec Hybris 4).</p> <p>Commerce Cloud Salesforce (Connecteur Open Source pour prendre en charge AEM 6.4)</p> </td>
   <td>Oui via open source via GitHub. Adobe Commerce (prend en charge la version 2.3.2 (par défaut) et compatible avec la version 2.3.1)</td>
  </tr>
  <tr>
   <td>Quand l’utiliser</td>
   <td>Cas d’utilisation limités : dans le cas de scénarios dans lesquels de petits catalogues statiques doivent être importés.</td>
   <td>Solution préférée dans la plupart des cas d’utilisation</td>
  </tr>
 </tbody>
</table>

eCommerce, avec la gestion de l’information sur les produits (PIM), gère les activités d’un site web axé sur la vente de produits par le biais d’une boutique en ligne :

* Création, durée de vie et obsolescence d’un produit
* Gestion des prix
* Gestion des transactions
* Gestion de catalogues entiers
* Enregistrements de stockage dynamiques et centralisés
* Interfaces web

AEM eCommerce aide les spécialistes du marketing à offrir des expériences d’achat personnalisées sur le web, les appareils mobiles et les médias sociaux. L’environnement de création AEM vous permet de personnaliser les pages et les composants en fonction du contexte du visiteur ou de la visiteuse cible et des stratégies de marchandisage. Par exemple :

* Pages de produits
* Composants de panier
* Composants de passage en caisse

La mise en œuvre d’eCommerce permet d’accéder en temps réel à des informations sur le produit. Cela peut être utilisé pour appliquer les éléments suivants :

* Intégrité des informations sur les produits
* Tarifs
* Inventaire de la gestion des stocks
* Variations du statut d’un panier

>[!NOTE]
>
>Pour utiliser le framework d’intégration avec les prestataires eCommerce externes, vous devez tout d’abord installer les packages nécessaires. Pour plus d’informations, reportez-vous à [Déploiement d’e-commerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Pour plus d’informations sur les possibilités d’extension d’eCommerce, consultez [Développement du e-commerce](/help/commerce/cif-classic/developing/ecommerce.md).

## Principales fonctionnalités {#main-features}

AEM e-commerce fournit :

* Différents **composants AEM prêts à l’emploi** illustrent ce qu’il est possible d’obtenir pour votre projet :

   * Affichage des produits
   * Panier
   * Passage en caisse
   * Produits récemment consultés
   * Bons
   * et autres

  ![Exemple de composants geometrixx.](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >Le framework d’intégration fourni par AEM vous permet également de créer des composants AEM supplémentaires pour les fonctionnalités commerciales, indépendamment de votre moteur e-commerce spécifique.

* **Rechercher** avec :

   * La recherche AEM
   * La recherche du système e-commerce
   * Une recherche tierce
   * Ou une combinaison de ces trois fonctions.

  ![Exemple de recherche.](/help/sites-administering/assets/chlimage_1-131.png)

* Utilise les capacités d’AEM de **présenter du contenu sur plusieurs canaux**, qu’il s’agisse d’une fenêtre de navigateur ou d’un appareil mobile. Ainsi, vous proposez votre contenu au format adapté pour vos visiteurs.

  ![Exemple de vue mobile.](/help/sites-administering/assets/chlimage_1-132.png)

* La possibilité de **développer votre propre mise en œuvre de l’intégration en fonction du [framework d’AEM eCommerce](#the-framework)**.

  Les deux mises en œuvre actuellement disponibles reposent sur la même base et complètent l’API générale (la structure). La mise en œuvre d’une nouvelle intégration implique seulement de mettre en œuvre les fonctionnalités dont votre intégration a besoin. Les composants frontaux peuvent être utilisés par les nouvelles mises en œuvre puisqu’ils utilisent des interfaces (et sont donc indépendants de la mise en œuvre).

* Possibilité de développer un **commerce axé sur l’expérience en fonction des données et de l’activité des acheteurs**, Vous pouvez ainsi réaliser de nombreux scénarios :

   * Par exemple, une réduction des frais de livraison proposée lorsque le montant total d’une commande dépasse un montant spécifique.
   * Vous pouvez également proposer des offres saisonnières qui utilisent les données de profil (par exemple, la localisation). Elles peuvent ensuite être mises en évidence, selon d’autres facteurs, le cas échéant.

  Dans l’exemple ci-dessous, un teaser est affiché, car le contenu du panier est inférieur à 75 $ :

  ![Panier avec contexte client.](/help/sites-administering/assets/chlimage_1-133.png)

  Cela peut être modifié lorsque le contenu du panier est supérieur à 75 $ :

  ![Panier avec contexte client après modification.](/help/sites-administering/assets/chlimage_1-134.png)

* Et d’autres fonctionnalités, notamment :

   * Contenu du panier conservé d’une session à l’autre
   * Historique des commandes exhaustif
   * Mise à jour du catalogue express

## Le framework {#the-framework}

La section [Concepts](/help/commerce/cif-classic/administering/concepts.md) couvre le framework de manière plus détaillée, mais ce qui suit fournit une vue d’ensemble accélérée du framework :

### Quoi ? {#what}

* Le framework d’intégration fournit l’API, une gamme de composants pour illustrer la fonctionnalité et plusieurs extensions pour fournir des exemples de modes de connexion.
* Le framework fournit la structure de base nécessaire à la mise en œuvre d’un projet.
* Le framework est extensible.
* Le framework ne fournit pas de site prêt à l’emploi. Un certain travail de développement reste nécessaire pour adapter le framework à vos spécifications.

### Pourquoi ? {#why}

* Pour fournir les mécanismes de base nécessaires à la création rapide d’un site de commerce électronique personnalisé.
* Tp fournit la flexibilité nécessaire au développement d’un site d’e-commerce réel.
* Illustrer les bonnes pratiques.
