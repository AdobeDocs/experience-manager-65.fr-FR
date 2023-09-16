---
title: Les tests - Quand et avec qui ?
description: Différents rôles peuvent être impliqués dans les tests et à diverses étapes du développement du projet.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 39%

---

# Les tests - Quand et avec qui ?{#testing-when-and-with-whom}

Différents rôles peuvent être impliqués dans les tests et à diverses étapes du développement du projet.

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
   <td>Ces tests sont les premiers de la chaîne, bien qu’ils soient répétés / étendus pendant le développement.</td>
  </tr>
  <tr>
   <td>Équipe d’assurance qualité</td>
   <td><p>Vous avez besoin d’une équipe d’assurance qualité (de toute taille appropriée) pour les tests fonctionnels et de performance.</p> <p>Il s’agit de testeurs neutres et dédiés. Dans le domaine du développement, la règle d’or veut que le développeur ne doit jamais tester son propre travail.</p> <p>Les membres de cette équipe peuvent être issus de l’équipe du projet Jour, l’équipe du partenaire et/ou celle de votre client.</p> </td>
   <td><p>La première version de la fonction doit être mise à la disposition des testeurs (si possible). Bien qu’une version intermédiaire anticipée puisse générer de nombreux bogues, elle peut fournir des commentaires précoces sur les problèmes critiques.</p> </td>
  </tr>
  <tr>
   <td>Équipe de test du client</td>
   <td><p>Selon le modèle de projet sélectionné, il peut être prévu que des membres de l’équipe client participent aux tests, en particulier les auteurs du site client.</p> <p>Ceci est avantageux car il s’agit des éléments suivants :</p>
    <ul>
     <li><p>Le client dispose de l’expérience du projet en cours de développement.</p> </li>
     <li><p>Permet de faire rapidement le point avec le client.</p> </li>
     <li><p>Les utilisateurs expriment souvent leurs besoins en termes d’expérience précédente ; impliquer les clients dans les tests le plus tôt possible augmente leur expérience du nouveau projet en termes de <i>main-mise</i> expérience.</p> </li>
    </ul> </td>
   <td><p>Là aussi, une participation au plus tôt est préférable. Toute version utilisée par les clients doit être stable et offrir un nombre raisonnable de fonctionnalités.</p> <p>Les premières impressions sont toujours importantes.</p> </td>
  </tr>
 </tbody>
</table>
