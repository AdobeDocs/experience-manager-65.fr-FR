---
title: Migration vers l’interface utilisateur tactile
seo-title: Migration vers l’interface utilisateur tactile
description: Migration vers l’interface utilisateur tactile
seo-description: Migration vers l’interface utilisateur tactile
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 15%

---


# Migration vers l’interface utilisateur tactile{#migration-to-the-touch-ui}

Depuis la version 6.0, Adobe Experience Manager (AEM) a introduit une nouvelle interface utilisateur appelée *interface utilisateur tactile* (également appelée simplement *interface utilisateur tactile*). Il est aligné sur le Adobe Marketing Cloud et sur les directives générales de l’interface utilisateur de l’Adobe. Il s’agit désormais de l’interface utilisateur standard en AEM avec l’interface héritée et orientée bureau, appelée *interface utilisateur classique*.

Si vous avez utilisé AEM avec une interface utilisateur classique, vous devez agir pour migrer votre instance. Cette page est destinée à servir de tremplin en fournissant des liens vers des ressources individuelles.

>[!NOTE]
>
>Un tel projet de migration peut avoir un impact significatif sur votre instance. Voir [Gestion des projets - Bonnes pratiques](/help/managing/best-practices.md) pour consulter les recommandations.

## Principes élémentaires {#the-basics}

Lors de la migration, vous devez tenir compte des différences (majeures) suivantes entre l’interface utilisateur classique et l’interface utilisateur tactile :

<table>
 <tbody>
  <tr>
   <td>IU classique</td>
   <td>Interface utilisateur optimisée pour les écrans tactiles</td>
  </tr>
  <tr>
   <td>Est décrit dans le référentiel JCR comme une structure de noeuds. Chaque noeud qui représente un élément de l’interface utilisateur est appelé <em>widget ExtJS</em> et rendu côté client par <code>ExtJS</code>.</td>
   <td>Également décrit dans le référentiel JCR comme une structure de noeuds. Cependant, dans ce cas, chaque noeud fait référence à un type de ressource Sling (composant Sling), qui est responsable de son rendu. L’interface utilisateur est donc (essentiellement) rendue côté serveur.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>non utilisé</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>utilisé</li>
     <li>par exemple<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Noeuds de la boîte de dialogue :</p>
    <ul>
     <li>Nom: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Noeuds de la boîte de dialogue :</p>
    <ul>
     <li>Nom: <code>cq:dialog</code></li>
     <li>jcr:primaryType : <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Emplacement Javascript :</p>
    <ul>
     <li>Les pièces impératives sont directement incorporées à l’aide d’écouteurs ou gérées dans clientlibs.</li>
    </ul> </td>
   <td><p>Emplacement Javascript :</p>
    <ul>
     <li>Les pièces impératives ne peuvent pas être incorporées dans la définition de la boîte de dialogue ; séparation des responsabilités.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>Les widgets de boîte de dialogue font directement référence au code JavaScript.</li>
    </ul> </td>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>Javascript observe les événements de dialogue.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendu effectué par le client :
    <ul>
     <li>Le client crée dynamiquement les composants de l’interface utilisateur.</li>
     <li>Le client demande une définition de composant (extraction) (en tant que JSON) à partir du serveur.</li>
    </ul> </td>
   <td>Rendu effectué par le serveur :
    <ul>
     <li>Le client demande des pages avec l’interface utilisateur associée.</li>
     <li>Le serveur envoie (Push) l’interface utilisateur sous la forme de documents HTML ; à l’aide des composants de l’interface utilisateur Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En d’autres termes, la migration d’une section de l’interface utilisateur classique vers l’interface utilisateur tactile signifie la migration d’un *widget ExtJS* vers un composant *Sling*. Pour pallier ce problème, l’interface utilisateur tactile est basée sur la structure de l’interface utilisateur Granite, qui fournit déjà certains composants Sling pour l’interface utilisateur (appelés composants de l’interface utilisateur Granite).

Avant de début, vérifiez l’état et les recommandations connexes :

* [État des fonctionnalités de l’interface utilisateur tactile](/help/release-notes/touch-ui-features-status.md)
* [Recommandations d’interfaces utilisateur aux clients](/help/sites-deploying/ui-recommendations.md)

Les bases du développement de l’interface utilisateur tactile fourniront une base solide :

* [Concepts de l’interface utilisateur (IU) tactile d’AEM](/help/sites-developing/touch-ui-concepts.md)
* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md)

## Migration de la création de page {#migrating-page-authoring}

Les boîtes de dialogue sont un facteur important de la migration de vos composants :

* [Développement de composants](/help/sites-developing/developing-components.md)  AEM (avec l’interface utilisateur tactile)
* [Migration à partir d’un composant classique](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Outil](/help/sites-developing/dialog-conversion.md)  de conversion de boîte de dialogue - pour vous aider à convertir les boîtes de dialogue de vos composants classiques de l&#39;interface utilisateur en interface utilisateur tactile

   * Il existe une couche de compatibilité dans l’interface utilisateur tactile pour ouvrir une boîte de dialogue classique dans un &quot;wrapper d’interface tactile&quot;, mais cette fonctionnalité est limitée et n’est pas recommandée à long terme.

* [Personnalisation des champs de la boîte de dialogue dans l’interface utilisateur tactile](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Création d’un composant de champ d’IU Granite](/help/sites-developing/granite-ui-component.md)
* [Personnalisation de la création](/help/sites-developing/customizing-page-authoring-touch.md)  de pages (avec l’interface utilisateur tactile)

## Migration des consoles {#migrating-consoles}

Vous pouvez également personnaliser les consoles :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md)  (pour l’interface utilisateur tactile)

## Considérations connexes {#related-considerations}

Bien qu’il ne soit pas directement lié à une migration vers l’interface utilisateur tactile, il existe des problèmes connexes qui méritent d’être examinés en même temps, car ils sont également recommandés :

* [Modèles](/help/sites-developing/templates.md)  - Modèles  [modifiables](/help/sites-developing/page-templates-editable.md)
* [Composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Voir aussi [Développement - Bonnes pratiques](/help/sites-developing/best-practices.md).

## Autres ressources {#further-resources}

Pour de plus amples renseignements sur l&#39;AEM en développement, voir la collecte des ressources sous :

* [Guide de l’utilisateur pour le développement](/help/sites-developing/home.md)
* [Documentation relative à l’interface utilisateur Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites Tutorials et vidéos](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Prise en main du développement d’AEM Sites – Tutoriel WKND](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Outils de modernisation d’AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Les outils de modernisation AEM sont un effort communautaire et ne sont ni appuyés ni justifiés par l&#39;Adobe.

