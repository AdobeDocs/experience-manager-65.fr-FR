---
title: Principes de base des graphiques sociaux
seo-title: Principes de base des graphiques sociaux
description: suivre la présentation du composant et du composant suivant
seo-description: suivre la présentation du composant et du composant suivant
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 13%

---


# Principes de base des graphiques sociaux  {#social-graph-essentials}

The ability for a Community member to follow [activities](essentials-activities.md) as well as be followed is established through two components:

Le `following` composant doit être associé à une autre ressource, et cette association est déjà établie pour les membres et les fonctionnalités des communautés existantes dans un site [](overview.md#communitiessites)communautaire.

The `following` component lists the members that are either following the current member or are being followed by the current member. Ce graphique social des relations entre les membres est inclus dans le profil d’utilisateur établi pour un site de communauté.

## Essentials for Client-Side {#essentials-for-client-side}

### Abonnement {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relations</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
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
   <td>Voir <a href="socialgraph.md">Utilisation d’un graphique de réseau social.</a></td>
  </tr>
  <tr>
   <td><strong> propriété facultative<br /></strong></td>
   <td>
    <ul>
     <li>Nom: <strong><code>outgoing</code></strong></li>
     <li>Type : booléen</li>
     <li>Valeur : <br />
      <ul>
       <li><i>True </i>- Le <code>following</code> composant liste les membres qui ont signé le membre actuellement <code>follows</code></li>
       <li><i>False </i>- Le <code>following</code> composant liste les membres qui <code>follow </code>le membre actuellement connecté</li>
      </ul> </li>
    </ul> <p>La valeur par défaut est <i>true</i> si la propriété est manquante. Actuellement, il n’est pas possible de définir cette propriété à l’aide de la boîte de dialogue de modification en mode création. La propriété doit être ajoutée à une instance du <code>following </code>noeud à l'aide de <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### S’abonner {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inclus**](scf.md#add-or-include-a-communities-component) | Non |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Social Graph](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Points de terminaison du graphique social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personnalisations côté serveur](server-customize.md)

