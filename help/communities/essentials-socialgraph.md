---
title: Principes de base des graphiques sociaux
description: Découvrez les principes de base du graphique des réseaux sociaux en utilisant les composants suivants et Suivre sur un site communautaire.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%
---
# Principes de base des graphiques sociaux  {#social-graph-essentials}

La capacité d&#39;un membre de la Communauté de suivre des [activités](essentials-activities.md) et d&#39;être suivi est établie par deux éléments :

Le composant `following` doit être associé à une autre ressource. Cette association est déjà établie pour les membres et fonctionnalités existants de Communities dans un [site communautaire](overview.md#communitiessites).

Le composant `following` répertorie les membres qui suivent le membre actif ou qui sont suivis par le membre actif. Ce graphique social des relations entre les membres est inclus dans le profil utilisateur établi pour un site communautaire.

## Essentials pour le côté client {#essentials-for-client-side}

### Abonnement {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relations</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="socialgraph.md">Utilisation d’un graphique des réseaux sociaux</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> property</strong></td>
   <td>
    <ul>
     <li>Nom : <strong><code>outgoing</code></strong></li>
     <li>Type : booléen</li>
     <li>Valeur :<br />
      <ul>
       <li><i>Vrai </i>- Le composant <code>following</code> répertorie les membres qui ont connecté le membre <code>follows</code></li>
       <li><i>Faux </i>- Le composant <code>following</code> répertorie les membres qui <code>follow </code>le membre connecté)</li>
      </ul> </li>
    </ul> <p>La valeur par défaut est <i>true</i> si la propriété est manquante. Il n’est pas possible de définir cette propriété à l’aide de la boîte de dialogue de modification en mode Création. La propriété doit être ajoutée à une instance du nœud <code>following</code> à l’aide de <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### S’abonner {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inclusible**](scf.md#add-or-include-a-communities-component) | Non |
| **modèles** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Social Graph](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Points d’entrée du graphique des réseaux sociaux](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personnalisations côté serveur](server-customize.md)
