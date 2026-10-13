---
title: Définir vos cas de test
description: Vos cas de test doivent être basés sur les cas d’utilisation et la spécification des exigences détaillées.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 83%
---
# Définir vos cas de test{#defining-your-test-cases}

Vos cas de test doivent être basés sur les éléments suivants :

**Cas d’utilisation**

* Ces fonctions définissent les fonctionnalités requises en termes d’interaction entre les acteurs (rôles qui déclenchent certaines actions) et le système.
* Les cas d’utilisation doivent être définis par le client ou la cliente.

**Spécification détaillée des exigences**

* Toutes les exigences fonctionnelles et de performances doivent être testées.

Les tests doivent définir clairement les éléments suivants :

* Conditions préalables ; elles peuvent couvrir des systèmes, configurations ou expériences de test spécifiques.
* Étapes à suivre ; à un niveau de détail approprié.
* Résultats attendus.
* Critères clairs de réussite et d’échec.

La perspective d’automatiser les cas de test est attrayante, car elle élimine les tâches répétitives.

## Tests manuels ou automatisés {#manual-versus-automated-tests}

L’automatisation des cas de test constitue toutefois un investissement important. Il convient donc de prendre en compte certains aspects :

* La configuration et l’installation nécessitent du temps, des efforts et de l’expérience.
* Si l’automatisation est basée sur le navigateur, il existe un risque accru de problèmes lorsque les mises à jour du navigateur sont installées, ce qui nécessite davantage de temps pour être corrigé.
* Seulement pour les projets de grande envergure.
* Cela est utile lorsque plusieurs versions sont générées à des fins de test ou dans le plan de mise à jour à long terme.

## Test d’aspects spécifiques {#testing-specific-aspects}

Lors du test d’AEM, certains détails sont particulièrement intéressants :

**Environnements de création et de publication**

Bien que le sujet soit traité dans [Environnements](/help/sites-developing/the-basics.md#environments), il convient de souligner un facteur déterminant dans AEM pour ce qui concerne les choix en matière de tests.

Vous devez traiter AEM comme s’il s’agissait de deux applications séparées :

* l’environnement *Auteur* ;
Cette instance permet aux auteurs de saisir et de publier du contenu.
Elle comporte un plus petit nombre prévisible d’utilisateurs et d’utilisatrices, pour qui des fonctionnalités et des performances spécifiques sont indispensables.

* l’environnement *Publication* ;
Cette instance présente le site web sous sa forme publiée pour que les visiteurs puissent y accéder.
Elle comporte généralement un plus grand nombre d’utilisateurs pour lequel le volume de trafic n’est pas toujours prévisible à 100 %. La performance est toujours cruciale lors de la réponse aux demandes. Tenez également compte de la mise en cache et de la répartition de charge.

Bien que le même logiciel soit utilisé, ces éléments :

* servent à différents objectifs ;
* ont des exigences différentes en ce qui concerne les fonctionnalités et les performances ;
* sont configurés différemment ;
* sont affinés séparément ;
* possèdent chacun leur propre ensemble de tests d’acceptation.

En d’autres termes, ils doivent être testés séparément et avec des cas de test différents.

**Personnalisation**

Lors du test de la personnalisation, chaque cas d’utilisation doit être répété à l’aide de plusieurs comptes d’utilisateur et d’utilisatrice afin de prouver son comportement.

Vérifiez également que la mise en cache présente un comportement correct.

**Dispatcher**

La plupart des projets installent Dispatcher pour la mise en cache et la répartition de charge.

Les tests sont difficiles (la mise en cache se fait à différents niveaux et à divers endroits) et doivent être réalisés en boîte noire. Les aspects clés à tester sont les suivants :

* **Précision**
Garantit que les mises à jour du contenu sont visibles pour le visiteur du site Web.

* **Continuité**
Assurez-vous que le site web est toujours disponible lorsqu’un serveur est arrêté.

* **Clusters**
Utilisé pour fournir les éléments suivants :

  * **Basculement**
    Si un serveur tombe en panne, les autres serveurs du cluster prennent le relais.

  * **Performance**
    L’équilibrage de charge avec basculement intégral améliore les performances d’un cluster.
    Lorsqu’il est utilisé pour un projet client, le cluster doit être testé pour confirmer le bon fonctionnement de la configuration.

## Test de logiciels tiers {#testing-third-party-software}

Tout logiciel tiers associé à l’interface d’AEM est référencé dans le cahier des charges détaillé.

Il faut analyser tous les tests nécessaires (en fonction de la portée définie) et obtenir des résultats satisfaisants.
