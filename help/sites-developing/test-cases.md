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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 33%

---

# Définir vos cas de test{#defining-your-test-cases}

Vos cas de test doivent être basés sur les éléments suivants :

**Cas d’utilisation**

* Ces fonctions définissent les fonctionnalités requises en termes d’interaction entre les acteurs (rôles qui déclenchent certaines actions) et le système.
* Les cas d’utilisation doivent être définis par le client.

**Spécification détaillée des exigences**

* Toutes les exigences fonctionnelles et de performance doivent être testées.

Les tests doivent définir clairement :

* Conditions préalables ; elles peuvent couvrir des systèmes, configurations ou expériences de test spécifiques.
* Étapes à suivre, à un niveau de détail approprié.
* Résultats attendus.
* Des critères clairs pour réussir ou échouer.

La perspective d’automatiser les cas de test est attrayante car elle élimine les tâches répétitives.

## Tests manuels ou automatisés {#manual-versus-automated-tests}

L’automatisation des cas de test constitue toutefois un investissement important. Il convient donc de prendre en compte certains aspects :

* La configuration et l’installation nécessitent du temps, des efforts et de l’expérience.
* Si le navigateur est basé sur , il existe un risque accru de problèmes lorsque les mises à jour du navigateur sont installées ; ce qui nécessite davantage de temps pour être corrigé.
* Seulement pour les projets de grande envergure.
* Ceci est utile lorsque plusieurs versions sont générées à des fins de test ou dans le plan de mise à jour à long terme.

## Test d’aspects spécifiques {#testing-specific-aspects}

Lors du test d’AEM, certains détails spécifiques présentent un intérêt particulier :

**Environnements de création et de publication**

Bien que couvert par [Environnements](/help/sites-developing/the-basics.md#environments), il est intéressant de souligner un facteur décisif d’AEM concernant les tests.

Considérez AEM comme deux applications :

* L’environnement *Auteur*
Cette instance permet aux auteurs de saisir et de publier du contenu.
Elle comporte un plus petit nombre prévisible d’utilisateurs et d’utilisatrices, pour qui des fonctionnalités et des performances spécifiques sont indispensables.

* la valeur *Publier* environnement Cette instance présente le site web sous sa forme publiée pour l’accès des visiteurs.
Elle comporte généralement un plus grand nombre d’utilisateurs pour lequel le volume de trafic n’est pas toujours prévisible à 100 %. La performance est toujours cruciale lors de la réponse aux demandes. Tenez également compte de la mise en cache et de l’équilibrage de charge.

Bien que le même logiciel soit utilisé, ils :

* servir différents objectifs ;
* ont des exigences différentes en ce qui concerne les fonctionnalités et les performances ;
* sont configurés différemment ;
* sont affinées séparément ;
* chacun possède son propre ensemble de tests d’acceptation

En d’autres termes, ils doivent être testés séparément et avec des cas de test différents.

**Personnalisation**

Lors du test de la personnalisation, chaque cas d’utilisation doit être répété à l’aide de plusieurs comptes d’utilisateurs afin de prouver son comportement.

Vérifiez également que la mise en cache présente un comportement correct.

**Le Dispatcher**

La plupart des projets installent Dispatcher pour la mise en cache et l’équilibrage de charge.

Les tests sont difficiles (la mise en cache se fait à différents niveaux et à divers endroits) et doivent être réalisés en boîte noire. Les aspects clés à tester sont les suivants :

* **Précision**
Vérifie que les mises à jour du contenu sont visibles par le visiteur du site web.

* **Continuité**
Assurez-vous que le site web est toujours disponible lorsqu’un serveur est arrêté.

* **Clusters**
Utilisé pour fournir les éléments suivants :

   * **Basculement**
Si un serveur tombe en panne, les autres serveurs du cluster prennent le relais.

   * **Performances**
L’équilibrage de charge avec basculement intégral améliore les performances d’un cluster.
Lorsqu’il est utilisé pour un projet client, le cluster doit être testé pour confirmer le bon fonctionnement de la configuration.

## Test de logiciels tiers {#testing-third-party-software}

Tout logiciel tiers associé à l’interface d’AEM est référencé dans le cahier des charges détaillé.

Il faut analyser tous les tests nécessaires (en fonction de la portée définie) et obtenir des résultats satisfaisants.
