---
title: Recommandations relatives aux interfaces utilisateur pour les client(e)s
seo-title: User Interface Recommendations for Customers
description: Liste de recommandations relatives aux interfaces utilisateur classiques et optimisées pour les écrans tactiles.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 40%

---

# Recommandations relatives aux interfaces utilisateur pour les client(e)s{#user-interface-recommendations-for-customers}

Adobe Experience Manager s’accompagne de deux interfaces utilisateur : l’IU Experience Cloud unifiée (également appelée IU tactile) et l’IU classique.

Ce document est destiné à guider les clients dans leur choix de l’interface utilisateur à utiliser en fonction de leur situation.

Conditions d’intérêt :

* **IU (ou IU standard)** Interface utilisateur moderne, introduite avec la version 5.6.0 en tant qu’aperçu technologique, puis développée avec les versions suivantes. Elle est basée sur l’expérience utilisateur unifiée pour Adobe Experience Cloud, connue précédemment sous le nom d’interface utilisateur tactile.

* **IU classique**
Interface utilisateur basée sur la technologie ExtJS introduite avec CQ 5.1 en 2008.

* **Administration du site** Fonctionnalités de gestion de la hiérarchie du site (déplacer, activer, gérer les références) et de création de nouvelles pages.

* **Création de pages** Fonctionnalités d’ajout de contenu et de modification du contenu d’une page.

* **Administration de gestion des ressources numériques / de ressources**
Fonctionnalités de gestion des ressources numériques (y compris les images, les vidéos, les documents et les téléchargements).

* **ContextHub**
Fonctionnalités de regroupement des informations sur le visiteur en vue de les utiliser pour différents objectifs. Fournit une interface utilisateur pour simuler des personnes qui visitent le site. Depuis AEM 6.2, ContextHub a remplacé la technologie précédente, ClientContext.

## Général {#general}

Au cours des dernières années, Adobe a mis à jour toutes les solutions Adobe Experience Cloud avec une interface utilisateur unifiée. Les utilisateurs de toutes les solutions Experience Cloud bénéficient d’une expérience cohérente avec des schémas communs sur l’utilisation et le fonctionnement des applications. Avec chaque version, Adobe a amélioré son interface utilisateur en fonction des commentaires des clients travaillant dans les différentes solutions.

L’interface utilisateur d’origine de Adobe Experience Manager (précédemment connue sous le nom de CQ5), introduite en 2008 et utilisée par les clients utilisant les versions 5.0 à 5.6.1, est présente dans AEM 6.5. Cela garantit que les clients peuvent effectuer la mise à jour vers la version 6.5 et bénéficier d’une plateforme mise à jour avec de nouvelles fonctionnalités tout en continuant à utiliser la même interface utilisateur.

Adobe recommande aux utilisateurs de planifier le passage à la nouvelle interface utilisateur en 2018 ou 2019. Vous pouvez le faire pendant la mise à jour vers la version 6.5 ou dans un projet distinct après la mise à jour, qui inclut les réglages nécessaires aux personnalisations et aux boîtes de dialogue de composant.

L’interface utilisateur classique est obsolète avec AEM 6.4 et Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. Notez que l’interface utilisateur classique reste complètement prise en charge alors qu’elle est en passe de devenir obsolète.

### Règles et recommandations  {#rules-and-recommendations}

Vous trouverez ci-dessous une liste de recommandations provenant de la gestion des produits pour Adobe Experience Manager 6.5 :

<table>
 <tbody>
  <tr>
   <th>Mon projet...</th>
   <th>Recommandations</th>
  </tr>
  <tr>
   <td>Commence à utiliser Adobe Experience Manager.</td>
   <td>Utilisez l’interface utilisateur par défaut.</td>
  </tr>
  <tr>
   <td><p>Utilise AEM depuis un moment.</p> <p>A utilisé l’interface utilisateur du produit prête à l’emploi et développé des composants personnalisés pour les sites.<br /> </p> </td>
   <td>
    <ol>
     <li>Mise à jour vers la version 6.5</li>
     <li>Utilisez l’interface utilisateur par défaut pour l’administration du site, les ressources, etc. etc.<br /> </li>
     <li>Configurez l’action "Modifier la page" pour ouvrir l’éditeur de page de l’IU classique. Voir <a href="#selecting-your-ui">Sélection de l’interface utilisateur</a>.</li>
    </ol> <p>Ensuite, dans une seconde phase :</p>
    <ol>
     <li>Mettez à jour vos boîtes de dialogue de composants pour utiliser le format de boîte de dialogue Coral 3. Adobe recommande d’utiliser la variable <a href="/help/sites-developing/modernization-tools.md">Outils de modernisation d’AEM</a> pour mettre à jour les composants.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>A créé un site utilisant ClientContext avec les intégrations.<br /> </td>
   <td>
    <ol>
     <li>Mise à jour vers la version 6.5</li>
     <li>Utilisez l’interface utilisateur par défaut pour l’administration du site, les ressources, etc. etc.</li>
     <li>Configurez l’action "Modifier la page" pour ouvrir l’éditeur de page de l’IU classique. Voir <a href="#selecting-your-ui">Sélection de l’interface utilisateur</a>.</li>
    </ol> <p>Ensuite, dans une seconde phase :</p>
    <ol>
     <li>Mettez à jour vos boîtes de dialogue de composants pour utiliser le format de boîte de dialogue Coral 3. Adobe recommande d’utiliser la variable <a href="/help/sites-developing/modernization-tools.md">Outils de modernisation d’AEM</a> pour mettre à jour les composants.</li>
     <li>Configurez ContextHub (le remplacement du ClientContext) et mettez à jour les modèles de page pour utiliser ContextHub. Notez que ContextHub dispose d’un mode de compatibilité qui permet de charger des magasins de ClientContext personnalisés.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Utilise CQ/AEM depuis de nombreuses années.</p> <p>A étendu l’interface utilisateur du produit (par exemple, l’administrateur de site) et créé des composants avec des boîtes de dialogue de modification complètes.</p> </td>
   <td><p>Passez à la version 6.5 et configurez l’IU classique en tant qu’interface utilisateur par défaut pour la création de page pour tous les utilisateurs. Voir <a href="#selecting-your-ui">Sélection de l’interface utilisateur</a>.</p> <p>Démarrez ensuite un projet pour appliquer la personnalisation et optimiser les boîtes de dialogue des composants au format Coral 3. Voir <a href="#resources-to-help">Ressources d’aide</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### FAQ {#faq}

Voir l’article de la base de connaissances, [FAQ sur la création dans l’interface utilisateur tactile](https://helpx.adobe.com/fr/experience-manager/kb/index/touchui_faq.html), pour plus d’informations, notamment sur la planification de l’obsolescence de l’IU classique.

### Sélection de l’interface utilisateur {#selecting-your-ui}

Consultez la section [Choix de l’interface utilisateur](/help/sites-authoring/select-ui.md) pour plus d’informations sur la configuration de votre système.

### État de l’interface utilisateur tactile {#touch-enabled-ui-status}

Pour plus d’informations sur les améliorations apportées à l’interface utilisateur tactile dans AEM 6.5, voir [Nouveautés](/help/release-notes/release-notes.md#what-s-new) dans les notes de mise à jour.

Pour découvrir une présentation complète, consultez la page [Statut des fonctionnalités de l’interface utilisateur optimisée pour les écrans tactiles](/help/release-notes/touch-ui-features-status.md).

### Ressources d’aide {#resources-to-help}

Pour plus d’informations sur la gestion de base :

* [Créer des pages](/help/sites-authoring/page-authoring.md).

Pour plus d’informations sur le développement :

* [Architecture de l’interface utilisateur tactile](/help/sites-developing/touch-ui-concepts.md).
* Utilisez les [Outils de modernisation AEM](/help/sites-developing/modernization-tools.md) pour convertir les boîtes de dialogue de modification des composants de l’interface utilisateur classique en interface utilisateur optimisée pour les écrans tactiles.

* [Structure de l’interface utilisateur optimisée pour les écrans tactiles](/help/sites-developing/touch-ui-structure.md).

* [Personnalisation des consoles de l’IU optimisée pour les écrans tactiles](/help/sites-developing/customizing-consoles-touch.md) (comprend un exemple de code).

* [Personnalisation de la création de page dans l’interface utilisateur optimisée pour les écrans tactiles](/help/sites-developing/customizing-page-authoring-touch.md) (comprend un exemple de code).

* [Documentation sur l’interface utilisateur Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
