---
title: Bonnes pratiques
seo-title: Bonnes pratiques
description: Les équipes d’ingénierie et de conseil Adobe ont développé un ensemble complet de bonnes pratiques pour les développeurs AEM
seo-description: Les équipes d’ingénierie et de conseil Adobe ont développé un ensemble complet de bonnes pratiques pour les développeurs AEM
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 77%

---

# Bonnes pratiques{#best-practices}

## Bonnes pratiques pour les développeurs - Prise en main {#best-practices-for-developers-getting-started}

Les équipes d’ingénierie et de conseil Adobe ont développé un ensemble complet de bonnes pratiques pour les développeurs AEM. Les développeurs d’Adobe adhèrent à ces bonnes pratiques en développant des mises à jour de base de produits AEM et le code client pour les implémentations client.

Avant de commencer votre projet de développement AEM, passez en revue ces bonnes pratiques :

* [Meilleures pratiques en matière de développement](/help/sites-developing/development-practices.md)
* [Architecture de contenu](/help/sites-developing/content-architecture.md)
* [Architecture logicielle](/help/sites-developing/software-architecture.md)
* [Conseils pour bien coder](/help/sites-developing/coding-tips.md)
* [Les pièges du codage](/help/sites-developing/code-pitfalls.md)
* [Interaction JCR](/help/sites-developing/jcr-integration.md)
* [Bundles OSGi](/help/sites-developing/osgi-bundles.md)
* [Bonnes pratiques relatives aux API Java](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informations supplémentaires sur les bonnes pratiques {#additional-best-practices-information}

La documentation disponible pour les domaines suivants est spécifique au développement de bonnes pratiques :

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Outillage/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Des documents spécifiques sont décrits dans les tableaux qui suivent et y sont reliés.

Pour connaître les bonnes pratiques en matière d’administration, de déploiement, de maintenance ou de développement, reportez-vous à l’une des ressources suivantes :

* [Meilleures pratiques d’administration](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques de création](/help/sites-authoring/best-practices.md)
* [Déploiement de meilleures pratiques](/help/sites-deploying/best-practices.md)

## Sites {#sites}

Les meilleures pratiques en termes de création et de gestion du contenu de votre site web sont les suivantes :

<table>
 <tbody>
  <tr>
   <td>Certains éléments de la théorie relative à l’IU standard, tactile.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU tactile : concepts </a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU tactile : structure </a></p> </td>
   <td>Ces documents présentent les concepts et la structure de l’IU tactile.</td>
  </tr>
  <tr>
   <td>IU tactile : Personnalisation des consoles </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personnalisation des consoles d’IU tactile</a></td>
   <td>Ce document explique comment étendre de manière optimale les consoles pour l’IU tactile.</td>
  </tr>
  <tr>
   <td>IU tactile : personnalisation de la création de pages</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personnalisation de la création de pages pour l’IU tactile</a></td>
   <td>Explique comment étendre la création de pages pour l’IU tactile.</td>
  </tr>
  <tr>
   <td>Workflows</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Développement et extension des workflows</a></td>
   <td><p>Les processus vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM) et peuvent représenter une grande partie du traitement effectué dans un environnement AEM. Il est donc vivement recommandé de planifier soigneusement les implémentations de vos processus.</p> </td>
  </tr>
 </tbody>
</table>

## Communautés {#communities}

[AEM ](/help/communities/overview.md) Communities simplifie la création et la gestion des communautés on-premise.

Les bonnes pratiques pour AEM Communities sont présentées ici :

|  |  |  |
|---|---|---|
| Bonnes pratiques relatives à l’utilisation du contenu généré par l’utilisateur | [Consignes de codage](/help/communities/code-guide.md) | Conseils pour le développement de code flexible et portable pour la [structure de composants sociaux](/help/communities/scf.md) (SCF). |
| Exemple d’utilisation des composants Communities | [Guide de composants de communauté](/help/communities/components-guide.md) | Un outil de développement interactif. |

## Outillage/HTL {#tooling-htl}

HTML Template Language (HTL) est un nouveau système de modèle HTML, introduit avec AEM 6.0. Se substituant à JSP et ESP, il s’agit aujourd’hui du système de modèle privilégié d’AEM.

|  |  |  |
|---|---|---|
| Présentation de HTL | [Présentation et syntaxe HTL](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html) | Ce document définit HTL et décrit la procédure de passage à HTL, un exemple de projet, la syntaxe, les expressions et les instructions HTL |
| Utilisation de l’API en Java | [Use-API Java HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | L’Use-API Java du langage de modèle HTML (HTL) permet à un fichier de HTL d’accéder aux méthodes d’assistance dans une classe Java. |

>[!NOTE]
>
>Le tutoriel en plusieurs parties suivant peut s’avérer intéressant pour la bonne pratique consistant à configurer un nouveau projet AEM, en détaillant les composants principaux, les modèles modifiables, les bibliothèques clientes et le développement de composants :
>[Prise en main du développement AEM Sites – Tutoriel WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
