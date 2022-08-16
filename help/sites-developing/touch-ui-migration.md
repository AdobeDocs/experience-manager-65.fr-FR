---
title: Migration vers l’interface utilisateur tactile
seo-title: Migration to the Touch UI
description: Migration vers l’interface utilisateur tactile
seo-description: Migration to the Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 15%

---

# Migration vers l’interface utilisateur tactile{#migration-to-the-touch-ui}

À compter de la version 6.0, Adobe Experience Manager (AEM) a introduit une nouvelle interface utilisateur appelée *IU tactile* (également appelé simplement *IU tactile*). Il est aligné sur Adobe Marketing Cloud et sur les directives générales de l’interface utilisateur de l’Adobe. L’interface utilisateur standard d’ est devenue AEM avec l’ancienne interface orientée bureau appelée *IU classique*.

Si vous avez utilisé AEM avec l’interface utilisateur classique, vous devez prendre des mesures pour migrer votre instance. Cette page est destinée à servir de tremplin en fournissant des liens vers des ressources individuelles.

>[!NOTE]
>
>Un tel projet de migration peut avoir un impact important sur votre instance. Voir [Gestion des projets - Bonnes pratiques](/help/managing/best-practices.md) pour obtenir des instructions recommandées.

## Principes élémentaires {#the-basics}

Lors de la migration, vous devez tenir compte des différences (majeures) suivantes entre l’IU classique et l’IU tactile :

<table>
 <tbody>
  <tr>
   <td>Interface utilisateur classique</td>
   <td>Interface utilisateur optimisée pour les écrans tactiles</td>
  </tr>
  <tr>
   <td>Est décrit dans le référentiel JCR comme une structure de noeuds. Chaque noeud qui représente un élément de l’interface utilisateur est appelé une <em>Widget ExtJS</em> et rendu côté client par <code>ExtJS</code>.</td>
   <td>Également décrit dans le référentiel JCR comme une structure de noeuds. Cependant, dans ce cas, chaque noeud fait référence à un type de ressource Sling (composant Sling), responsable de son rendu. L’interface utilisateur est (en fait) rendue côté serveur.</td>
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
   <td><p>Noeuds de boîte de dialogue :</p>
    <ul>
     <li>Nom: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Noeuds de boîte de dialogue :</p>
    <ul>
     <li>Nom: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Emplacement JavaScript :</p>
    <ul>
     <li>Les parties impératives sont directement incorporées à l’aide d’écouteurs ou gérées dans des bibliothèques clientes.</li>
    </ul> </td>
   <td><p>Emplacement JavaScript :</p>
    <ul>
     <li>Les parties impératives ne peuvent pas être incorporées dans la définition de boîte de dialogue ; la séparation des responsabilités.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>Les widgets de boîte de dialogue font directement référence au code JavaScript.</li>
    </ul> </td>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>Javascript observe les événements de boîte de dialogue.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendu effectué par le client :
    <ul>
     <li>Le client crée dynamiquement les composants de l’interface utilisateur.</li>
     <li>Le client demande la définition du composant (extraction) (au format JSON) au serveur.</li>
    </ul> </td>
   <td>Rendu effectué par le serveur :
    <ul>
     <li>Le client demande des pages avec l’interface utilisateur associée.</li>
     <li>Le serveur envoie (push) l’interface utilisateur sous la forme de documents HTMLS ; à l’aide des composants de l’IU Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En d’autres termes, la migration d’une section de votre interface utilisateur de l’IU classique vers l’IU tactile signifie la portage d’une *Widget ExtJS* à *Composant Sling*. Pour faciliter cela, l’interface utilisateur tactile est basée sur la structure de l’interface utilisateur Granite, qui fournit déjà certains composants Sling pour l’interface utilisateur (appelés composants de l’interface utilisateur Granite).

Avant de commencer, vérifiez l’état et les recommandations associées :

* [État des fonctionnalités de l’interface utilisateur tactile](/help/release-notes/touch-ui-features-status.md)
* [Recommandations d’interfaces utilisateur aux clients](/help/sites-deploying/ui-recommendations.md)

Les principes de base du développement de l’interface utilisateur tactile fourniront une base solide :

* [Concepts de l’interface utilisateur (IU) tactile d’AEM](/help/sites-developing/touch-ui-concepts.md)
* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md)

## Migration de la création de pages {#migrating-page-authoring}

Les boîtes de dialogue constituent un facteur majeur lors de la migration de vos composants :

* [Développement de composants AEM](/help/sites-developing/developing-components.md) (avec l’interface utilisateur tactile)
* [Migration à partir d’un composant classique](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Outils de modernisation d’AEM](/help/sites-developing/modernization-tools.md) - pour vous aider à convertir les boîtes de dialogue de vos composants d’IU classique en IU tactile

   * Il existe une couche de compatibilité dans l’interface utilisateur tactile pour ouvrir une boîte de dialogue d’interface utilisateur classique dans un &quot;wrapper d’interface utilisateur tactile&quot;, mais cette fonctionnalité est limitée et n’est pas recommandée à long terme.

* [Personnalisation des champs de boîte de dialogue dans l’interface utilisateur tactile](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Création d’un composant de champ d’IU Granite](/help/sites-developing/granite-ui-component.md)
* [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md) (avec l’interface utilisateur tactile)

## Migration des consoles {#migrating-consoles}

Vous pouvez également personnaliser les consoles :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md) (pour l’interface utilisateur tactile)

## Considérations connexes {#related-considerations}

Bien qu’il ne soit pas directement lié à une migration vers l’interface utilisateur tactile, il existe des problèmes connexes qui méritent d’être pris en compte en même temps, car ils sont également recommandés :

* [Modèles](/help/sites-developing/templates.md) - [Modèles modifiables](/help/sites-developing/page-templates-editable.md)
* [Composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/fr-FR/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Voir aussi [Développement - Bonnes pratiques](/help/sites-developing/best-practices.md).

## Autres ressources {#further-resources}

Pour plus d’informations sur le développement d’AEM, voir la collecte de ressources sous :

* [Guide de l’utilisateur pour le développement](/help/sites-developing/home.md)
* [Documentation relative à l’interface utilisateur Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutorials et vidéos d’AEM 6.5 Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Prise en main du développement d’AEM Sites – Tutoriel WKND ](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Outils de modernisation d’AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Les outils de modernisation d’AEM sont un effort de la communauté et ne sont ni soutenus ni garantis par Adobe.
