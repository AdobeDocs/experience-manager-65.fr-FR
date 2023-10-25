---
title: Migration vers l’interface utilisateur tactile
description: Découvrez la migration Adobe Experience Manager vers l’interface utilisateur tactile et comment elle vous affecte.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 76%

---

# Migration vers l’interface utilisateur tactile{#migration-to-the-touch-ui}

À compter de la version 6.0, Adobe Experience Manager (AEM) a introduit une nouvelle interface utilisateur appelée *IU optimisée pour les écrans tactiles* (également appelée simplement *IU tactile*). Il est aligné sur Adobe Experience Cloud et sur les directives générales de l’interface utilisateur de l’Adobe. Il s’agit dorénavant de l’interface utilisateur standard d’AEM, l’ancienne interface orientée bureau désormais appelée *IU classique*.

Si vous avez utilisé AEM avec l’interface utilisateur classique, prenez des mesures pour migrer votre instance. Cette page vous accompagnera à cet effet en vous fournissant des liens vers plusieurs ressources individuelles.

>[!NOTE]
>
>Un tel projet de migration peut avoir un impact important sur votre instance. Consultez la section [Gestion des projets - Bonnes pratiques](/help/managing/best-practices.md) pour obtenir des instructions recommandées.

## Principes élémentaires {#the-basics}

Lors de la migration, tenez compte des principales différences suivantes entre l’IU classique et l’IU tactile :

<table>
 <tbody>
  <tr>
   <td>Interface utilisateur classique</td>
   <td>Interface utilisateur optimisée pour les écrans tactiles</td>
  </tr>
  <tr>
   <td>Décrite dans le référentiel JCR comme une structure de nœuds. Chaque nœud qui représente un élément de l’interface utilisateur est appelé une <em>Widget ExtJS</em> et rendu côté client par <code>ExtJS</code>.</td>
   <td>Également décrite dans le référentiel JCR comme une structure de nœuds. Cependant, dans ce cas, chaque noeud fait référence à un type de ressource Sling (composant Sling), responsable de son rendu. L’interface utilisateur est (en fait) rendue côté serveur.</td>
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
   <td><p>Nœuds de boîte de dialogue :</p>
    <ul>
     <li>Nom : <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nœuds de boîte de dialogue :</p>
    <ul>
     <li>Nom : <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Emplacement JavaScript :</p>
    <ul>
     <li>Les parties nécessaires sont directement incorporées à l’aide de listeners ou gérées dans des bibliothèques clientes.</li>
    </ul> </td>
   <td><p>Emplacement JavaScript :</p>
    <ul>
     <li>Les parties nécessaires ne peuvent pas être incorporées dans la définition de boîte de dialogue, du fait de la séparation des responsabilités.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>Les widgets de boîte de dialogue font directement référence au code JavaScript.</li>
    </ul> </td>
   <td><p>Gestion des événements :</p>
    <ul>
     <li>JavaScript surveille les événements de boîte de dialogue.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendu effectué par le client :
    <ul>
     <li>Le client crée dynamiquement les composants de l’interface utilisateur.</li>
     <li>Le client demande la définition du composant (extraction) (au format JSON) au serveur.</li>
    </ul> </td>
   <td>Rendu effectué par le serveur :
    <ul>
     <li>Le client demande des pages avec l’interface utilisateur associée.</li>
     <li>Le serveur envoie (pousse) l’interface utilisateur sous la forme de documents HTML, à l’aide des composants de l’IU Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En d’autres termes, la migration d’une section de votre interface utilisateur de l’IU classique vers l’IU tactile correspond au portage d’un *Widget ExtJS* en *Composant Sling*. Pour plus de facilité, l’interface utilisateur tactile est basée sur le framework de l’interface utilisateur Granite, qui fournit déjà certains composants Sling pour l’interface utilisateur (appelés composants de l’interface utilisateur Granite).

Avant de commencer, vérifiez le statut et les recommandations associées :

* [Statut des fonctionnalités de l’IU tactile](/help/release-notes/touch-ui-features-status.md)
* [Recommandations d’interfaces utilisateur aux clients](/help/sites-deploying/ui-recommendations.md)

Les principes de base du développement de l’interface utilisateur tactile constituent une base solide :

* [Concepts de l’interface utilisateur (IU) tactile d’AEM](/help/sites-developing/touch-ui-concepts.md)
* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md)

## Migration de la création de pages {#migrating-page-authoring}

Les boîtes de dialogue constituent un élément majeur de la migration de vos composants :

* [Développement de composants AEM](/help/sites-developing/developing-components.md) (avec l’interface utilisateur tactile)
* [Migration à partir d’un composant classique](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Outils de modernisation d’AEM](/help/sites-developing/modernization-tools.md) - Pour vous aider à convertir les boîtes de dialogue de vos composants d’IU classique en IU tactile

   * Il existe une couche de compatibilité dans l’interface utilisateur tactile pour ouvrir une boîte de dialogue d’interface utilisateur classique dans un &quot;wrapper d’interface utilisateur tactile&quot;, mais cette fonctionnalité est limitée et n’est pas recommandée à long terme.

* [Personnalisation des champs de boîte de dialogue dans l’interface utilisateur tactile](https://helpx.adobe.com/fr/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Création d’un composant de champ d’IU Granite](/help/sites-developing/granite-ui-component.md)
* [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md) (avec l’interface utilisateur tactile)

## Migration des consoles {#migrating-consoles}

Vous pouvez également personnaliser les consoles :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md) (pour l’interface utilisateur tactile)

## Considérations annexes {#related-considerations}

Bien que cela ne soit pas directement lié à une migration vers l’interface utilisateur tactile, il existe des problèmes connexes qui méritent d’être pris en compte en même temps, car ils font également partie des bonnes pratiques recommandées :

* [Modèles](/help/sites-developing/templates.md) - [Modèles modifiables](/help/sites-developing/page-templates-editable.md)
* [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr)

>[!NOTE]
>
>Consultez également la section [Développement - Bonnes pratiques](/help/sites-developing/best-practices.md).

## Autres ressources {#further-resources}

Pour plus d’informations sur le développement d’AEM, consultez la collection de ressources sous :

* [Guide de l’utilisateur pour le développement](/help/sites-developing/home.md)
* [Documentation relative à l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutoriels et vidéos d’AEM 6.5 Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html?lang=fr)
* [Prise en main du développement d’AEM Sites – Tutoriel WKND](/help/sites-developing/getting-started.md)
* [AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=fr)
* [Outils de modernisation d’AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Les outils de modernisation AEM sont un effort communautaire et ne sont ni soutenus ni garantis par Adobe.
