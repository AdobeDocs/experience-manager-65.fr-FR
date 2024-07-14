---
title: Notions fondamentales sur les graphiques sociaux
description: Découvrez les principes de base de Social Graph à l’aide des composants Suivants et Suivants d’un site de communauté.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 4%

---

# Notions fondamentales sur les graphiques sociaux  {#social-graph-essentials}

La possibilité pour un membre de la communauté de suivre [activities](essentials-activities.md) et d’être suivi est établie par deux composants :

Le composant `following` doit être associé à une autre ressource, et cette association est déjà établie pour les membres et fonctionnalités de Communities existants dans un [site de communauté](overview.md#communitiessites).

Le composant `following` répertorie les membres qui suivent le membre actuel ou qui sont suivis par le membre actuel. Ce graphique social des relations entre les membres est inclus dans le profil utilisateur établi pour un site communautaire.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

### Abonnement {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relations</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="socialgraph.md">Utilisation du graphique social</a></td>
  </tr>
  <tr>
   <td><strong> propriété facultative<br /></strong></td>
   <td>
    <ul>
     <li>Nom : <strong><code>outgoing</code></strong></li>
     <li>Type : booléen</li>
     <li>Valeur :<br />
      <ul>
       <li><i>True </i> - Le composant <code>following</code> répertorie les membres qui le membre connecté. <code>follows</code></li>
       <li><i>False </i> - Le composant <code>following</code> répertorie les membres qui <code>follow </code>le membre connecté</li>
      </ul> </li>
    </ul> <p>La valeur par défaut est <i>true</i> si la propriété est manquante. Il n’est pas possible de définir cette propriété à l’aide de la boîte de dialogue de modification en mode Auteur. La propriété doit être ajoutée à une instance du noeud <code>following</code> à l’aide de <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### S’abonner {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**includable**](scf.md#add-or-include-a-communities-component) | Non |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API Social Graph](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Points d’entrée du graphique social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personnalisations côté serveur](server-customize.md)
