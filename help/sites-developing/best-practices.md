---
title: Bonnes pratiques pour les développeurs et développeuses AEM
description: Les équipes d’ingénierie et de conseil d’Adobe ont développé un ensemble complet de bonnes pratiques pour les développeurs et développeuses d’AEM.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 100%

---

# Bonnes pratiques{#best-practices}

## Bonnes pratiques pour les développeurs et développeuses - Prise en main {#best-practices-for-developers-getting-started}

Les équipes d’ingénierie et de conseil Adobe ont développé un ensemble complet de bonnes pratiques pour les développeurs AEM. Les développeurs et développeuses d’Adobe se conforment à ces bonnes pratiques lorsqu’ils développent des mises à jour de base pour les produits d’AEM et du code client pour les implémentations client.

Avant de commencer votre projet de développement AEM, passez en revue ces bonnes pratiques :

* [Bonnes pratiques en matière de développement](/help/sites-developing/development-practices.md)
* [Architecture de contenu](/help/sites-developing/content-architecture.md)
* [Architecture logicielle](/help/sites-developing/software-architecture.md)
* [Conseils pour bien coder](/help/sites-developing/coding-tips.md)
* [Les pièges du codage](/help/sites-developing/code-pitfalls.md)
* [Interaction JCR](/help/sites-developing/jcr-integration.md)
* [Bundles OSGi](/help/sites-developing/osgi-bundles.md)
* [Bonnes pratiques relatives aux API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=fr)

### Informations supplémentaires sur les bonnes pratiques {#additional-best-practices-information}

Les aspects suivants sont couverts par une documentation spécifique pour le développement de bonnes pratiques :

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Outillage/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Les documents spécifiques sont décrits et associés dans les tableaux qui suivent.

Pour connaître les bonnes pratiques en matière d’administration, de déploiement, de maintenance ou de création, reportez-vous à l’une des ressources suivantes :

* [Bonnes pratiques d’administration](/help/sites-administering/administer-best-practices.md)
* [Bonnes pratiques de création](/help/sites-authoring/best-practices.md)
* [Bonnes pratiques de déploiement](/help/sites-deploying/best-practices.md)

## Sites {#sites}

La gestion et la création du contenu de votre site web comportent les bonnes pratiques suivantes :

<table>
 <tbody>
  <tr>
   <td>Une partie de la théorie derrière l’IU tactile standard.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU tactile : concepts</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU tactile : structure</a></p> </td>
   <td>Ces documents présentent les concepts et la structure de l’IU tactile.</td>
  </tr>
  <tr>
   <td>IU tactile : personnalisation des consoles </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personnalisation des consoles d’IU tactile</a></td>
   <td>Ce document décrit la meilleure manière d’optimiser les consoles pour l’IU tactile.</td>
  </tr>
  <tr>
   <td>Interface utilisateur tactile : personnaliser la création de pages</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personnalisation de la création de pages pour l’IU tactile</a></td>
   <td>Décrit comment optimiser la création de pages pour l’interface utilisateur tactile.</td>
  </tr>
  <tr>
   <td>Workflows</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Développement et extension des workflows</a></td>
   <td><p>Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM) et peuvent représenter une grande partie du traitement qui se produit dans un environnement AEM. Il est donc hautement recommandé de planifier et de configurer avec soin les implémentations de workflows.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) simplifie la création et la gestion des communautés sur site.

Vous trouverez ici certaines bonnes pratiques pour AEM Communities :

|  |  |  |
|---|---|---|
| Bonnes pratiques relatives à l’utilisation du contenu généré par l’utilisateur (UGC) | [Consignes de codage](/help/communities/code-guide.md) | Consignes relatives au développement d’un code flexible et portable destiné à un [framework de composants sociaux](/help/communities/scf.md) (SCF). |
| Exemple d’utilisation des composants de communautés | [Guide de composants de communauté](/help/communities/components-guide.md) | Un outil de développement interactif. |

## Outillage/HTL {#tooling-htl}

Le langage de modèle HTML (HTL) est un nouveau système de modèle HTML, introduit avec AEM 6.0. Il remplace JSP et ESP en tant que système de modèle préféré d’AEM.

|  |  |  |
|---|---|---|
| Présentation de HTL | [Vue d’ensemble et syntaxe HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) | Ce document décrit ce qu’est HTL, comment passer à HTL, un exemple de projet, une syntaxe, des expressions et des instructions. |
| Utiliser l’API dans Java | [Use-API Java HTL](https://helpx.adobe.com/fr/experience-manager/htl/using/use-api.html) | L’Use-API Java HTL permet à un fichier HTL d’accéder aux méthodes d’assistance dans une classe Java personnalisée. |

>[!NOTE]
>
>Le didacticiel en plusieurs parties peut être intéressant pour la configuration d’un nouveau projet AEM, en détaillant les principaux composants, les modèles modifiables, les bibliothèques clientes et le développement de composants :
>[Prise en main du développement AEM Sites – Tutoriel WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr)
