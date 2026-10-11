---
title: Élaborer un plan de tests
description: Les cas de test individuels sont amalgamés dans votre plan de test.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
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
source-wordcount: '194'
ht-degree: 100%
---
# Élaborer un plan de tests{#compiling-your-test-plan}

Les cas de test individuels sont ensuite amalgamés dans votre plan de test, qui définit également :

**Priorités**

Certains tests auront plus d’importance que d’autres. Il est donc conseillé d’indiquer leur priorité.

Par exemple, certains tests peuvent affecter une décision Go/No-Go et doivent donc être confirmés à chaque version intermédiaire testée.

**Itérations**

Si votre projet utilise une forme d’itération de développement (impliquant la mise à disposition de plusieurs versions), une indication des résultats pour chaque itération peut se révéler utile ou nécessaire. Cela peut être utilisé pour indiquer les éléments suivants :

* Les tests qui seront couverts dans telle ou telle itération.
* Les résultats vus pour les tests répétés dans diverses itérations.
* Que les tests de priorité et les tests sur les fonctionnalités de base sont répétés à intervalles réguliers.

**Testeur**

À un moment donné, vous pouvez affecter soit l’équipe de test appropriée, soit une personne spécifique au test (en fonction des disponibilités et/ou de l’expérience).

**Résumé ou vue d’ensemble**

Afin de créer des rapports, vous souhaitez fournir une vue d’ensemble des résultats de test :

* Pourcentage de tests déjà couverts.
* Pourcentage de réussite/échec.
* Chiffres spécifiques relatifs aux tests de priorité.
