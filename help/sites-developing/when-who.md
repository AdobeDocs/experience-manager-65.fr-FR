---
title: Test - quand et avec qui ?
seo-title: Testing - when and with whom?
description: Divers rôles peuvent participer aux tests et aux différentes étapes du développement du projet
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 41%

---

# Test - quand et avec qui ?{#testing-when-and-with-whom}

Divers rôles peuvent participer aux tests et aux différentes étapes du développement du projet.

<table>
 <tbody>
  <tr>
   <td>Équipe de test</td>
   <td>Responsable de... </td>
   <td>Quand...</td>
  </tr>
  <tr>
   <td>Équipe de développement</td>
   <td>L’équipe de développement est responsable de vos tests unitaires et de certains tests d’intégration.</td>
   <td>Ces tests sont les premiers de la chaîne, mais ils seront répétés/étendus au cours du développement.</td>
  </tr>
  <tr>
   <td>Équipe d’assurance qualité</td>
   <td><p>Vous aurez besoin d’une équipe d’assurance qualité (de la taille appropriée) pour les tests fonctionnels et de performance.</p> <p>Ce sont des testeurs neutres et dédiés. Dans le domaine du développement, la règle d’or veut que le développeur ne doit jamais tester son propre travail.</p> <p>Les membres de cette équipe peuvent être issus de l’équipe du projet Jour, l’équipe du partenaire et/ou celle de votre client.</p> </td>
   <td><p>La première version de la fonction doit être mise à la disposition des testeurs (dès que cela est réalisablement possible). Bien qu’une version intermédiaire puisse générer de nombreux bogues, elle permet néanmoins de faire le point sur des problèmes majeurs.</p> </td>
  </tr>
  <tr>
   <td>Équipe de test du client</td>
   <td><p>Selon le modèle de projet sélectionné, il peut être prévu que des membres de l’équipe client participent aux tests, en particulier les auteurs du site client.</p> <p>Les avantages sont les suivants :</p>
    <ul>
     <li><p>Offre au client une expérience du projet en cours de développement.</p> </li>
     <li><p>Fournit des commentaires anticipés du client.</p> </li>
     <li><p>Les utilisateurs expriment souvent leurs besoins en termes d'expérience passée. impliquer les clients dans les tests le plus tôt possible augmente leur expérience du nouveau projet en termes de <i>main-sur-le-champ</i> expérience.</p> </li>
    </ul> </td>
   <td><p>Là encore, une participation précoce est une bonne chose, bien que toute version que les clients utilisent doive être stable, avec des fonctionnalités raisonnables.</p> <p>Les premières impressions sont toujours importantes.</p> </td>
  </tr>
 </tbody>
</table>
