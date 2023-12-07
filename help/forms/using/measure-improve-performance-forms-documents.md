---
title: Mesurer et améliorer l’efficacité et de la conversion des formulaires
description: AEM Forms s’intègre aux solutions Adobe Target et Adobe Analytics, ce qui vous permet de mesurer et d’améliorer les performances et le taux de conversion de vos formulaires.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 31%

---

# Mesure et amélioration de l’efficacité et de la conversion des formulaires{#measure-and-improve-effectiveness-and-conversion-of-forms}

## La difficulté {#the-challenge-br}

Les entreprises autorisent et encouragent de plus en plus leurs clients à avoir recours aux applications numériques en libre service sur plusieurs canaux. Cependant, en l’absence de mécanisme de commentaire linéaire, il devient difficile de mesurer la réussite et d’expérimenter des formulaires numériques pour améliorer l’expérience client et augmenter les conversions.

Pour optimiser le ROI, les entreprises doivent surveiller la manière dont leurs clients interagissent avec les services et tester leurs artefacts numériques (formulaires) pour améliorer les expériences client. Pour mesurer le succès et définir une stratégie d’amélioration, les entreprises doivent répondre à des questions telles que :

* Combien de clients ont tenté d’accéder à mes formulaires ou d’en effectuer des transactions ?
* Combien d&#39;entre eux ont terminé la transaction ?
* Combien d&#39;entre eux ont abandonné le formulaire ?
* Quels sont les secteurs problématiques auxquels les clients sont confrontés ?
* Quelles modifications puis-je apporter et comment tester ce qui entraîne une meilleure conversion ?

## La solution {#the-solution}

AEM Forms s’intègre aux solutions [Adobe Marketing Cloud](https://www.adobe.com/fr/marketing-cloud.html), [Adobe Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html) et [Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html), qui peuvent vous aider à surveiller et à analyser les performances de vos formulaires et vous permettre de tester et d’identifier l’expérience qui conduit à un meilleur taux de conversion.

## Le workflow {#the-workflow}

Voyons en détail comment mesurer les performances et améliorer les taux de conversion des formulaires.

### Public cible {#target-audience}

* Utilisateurs commerciaux et analystes responsables des stratégies marketing et du succès
* Personnel informatique chargé de la configuration et de la maintenance des infrastructures et des solutions

### Composants et fonctionnalités AEM Forms impliqués {#aem-forms-components-and-features-involved}

* Formulaires adaptatifs
* Intégration à Adobe Analytics pour collecter, organiser et générer un rapport des interactions client avec vos formulaires adaptatifs
* Intégration à Adobe Target pour exécuter des tests A/B pour les formulaires adaptatifs

### Hypothèses {#assumptions}

* Vous disposez déjà d’un compte Adobe Marketing Cloud et vous êtes enregistré pour les solutions Analytics et Target.
* Vous avez publié un formulaire adaptatif auquel les clients peuvent accéder.

### Étapes du workflow {#workflow-steps}

#### Étape 1 : Configurer Analytics et Target dans AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configuration d’Analytics**

Pour obtenir des informations détaillées sur les interactions de vos clients avec vos formulaires, vous devez d’abord configurer Analytics dans AEM Forms. Exécutez les étapes suivantes :

1. Création d’une suite de rapports dans Adobe Analytics
1. Création d’une configuration de service Cloud dans AEM
1. Création de la structure de service Cloud dans AEM
1. Configuration du service de configuration d’AEM Forms Analytics dans AEM
1. Activation de l’analyse du formulaire dans AEM

Pour les étapes détaillées, voir [Configurer des analyses et des rapports pour les formulaires adaptatifs](../../forms/using/configure-analytics-forms-documents.md).

**Configuration de Target**

Pour créer et exécuter des tests A/B pour vos formulaires adaptatifs, configurez Target dans AEM Forms comme décrit dans [Configurer et intégrer Target dans AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Etape 2 : Afficher le rapport d’analyse {#step-view-analytics-report-br}

À mesure que vos clients accèdent aux formulaires sur lesquels vous avez activé Analytics et interagissent avec eux, leurs interactions sont capturées dans des bases de données Analytics hautement sécurisées. Les bases de données sont segmentées par clients et accessibles via des connexions sécurisées.

Vous pouvez afficher un rapport dans AEM pour les formulaires activés dans Analytics et analyser les données. Pour afficher le rapport :

1. Sur AEM serveur, accédez à **Forms > Forms et documents**.
1. Sélectionnez le formulaire pour lequel vous souhaitez obtenir le rapport d’analyse.
1. Cliquez sur l’icône Rapports Analytics . Le rapport s’affiche.

Regardons de plus près les points de données qu’Analytics collecte et génère des rapports pour les formulaires.

**Rapport d’analyse Forms**

Le rapport d’analyse pour les formulaires adaptatifs capture les indicateurs de performances clés (IPC) suivants au niveau du formulaire :

* **Durée moyenne de remplissage** : temps moyen passé au remplissage du formulaire.
* **Impressions** : nombre de fois que le formulaire s’est affiché dans des résultats de recherche. 

* **Rendus** : nombre de fois que le formulaire a été affiché ou ouvert.
* **Brouillons**: nombre de fois que le formulaire a été enregistré en tant que brouillon

* **Envois**: nombre de fois que le formulaire a été envoyé
* **Abandonner**: nombre de fois où les utilisateurs sont restés sans remplir le formulaire
* **Visites/envois**: ratio des visites par envoi

En outre, vous obtenez les détails suivants sur chaque panneau du formulaire :

* **Temps** : temps moyen passé (exprimé en secondes) dans le panneau et ses champs. 

* **Erreurs** : nombre d’erreurs survenues sur le panneau et ses champs par tranche de 1000 rendus de formulaire. 

* **Aide** : nombre de fois que les utilisateurs ont accédé à l’aide contextuelle pour le panneau et ses champs par tranche de 1000 rendus de formulaire

![Exemple de rapport d’analyse pour un formulaire adaptatif](assets/summary-report.png)

Pour plus d’informations sur les rapports d’analyse de formulaires, reportez-vous à la rubrique [Affichage et compréhension des rapports d’analyse AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Vous pouvez afficher les rapports détaillés et obtenir des informations plus précises sur vos clients et leurs interactions avec vos formulaires depuis votre compte Analytics sur Adobe Marketing Cloud.

#### Etape 3 : Analyser les points de données {#step-analyze-data-points}

Au cours de cette étape, vous allez analyser les points de données dans le rapport d’analyse et déduire les performances du formulaire. S’il ne répond pas à vos indicateurs de performance clés de succès, vous allez construire des hypothèses, basées sur les données, et trouver des solutions possibles pour résoudre les problèmes. Par exemple :

* Si le temps de remplissage moyen du formulaire est plus élevé que prévu, il est possible que votre formulaire soit complexe à comprendre pour les clients, qu’il n’utilise pas de terminologies standard, qu’il soit trop long, etc. Dans ce cas, vous pouvez simplifier la structure et les champs du formulaire, retravailler la conception du formulaire, raccourcir la longueur du formulaire ou ajouter des descriptions et des exemples d’aide pour les champs de formulaire non standard.
* Si les données indiquent que la plupart des clients accèdent à l’aide d’un panneau de formulaire, il est évident que les clients ne savent pas quelles informations remplir. Vous pouvez utiliser une terminologie différente ou ajouter des exemples d’entrée et une description de l’aide pour ce panneau.
* Si le taux d’abandon ou d’abandon d’un formulaire est plus élevé que prévu, cela peut être dû au temps nécessaire au rendu du formulaire, au fait que les clients arrivent par inadvertance sur le formulaire ou à un problème trop compliqué. Dans ce cas, vous pouvez optimiser la description du formulaire qui apparaît dans les résultats de recherche, simplifier le formulaire, optimiser le formulaire pour un chargement plus rapide, etc.

Une fois que vous avez analysé ces points de données et formulé une hypothèse, apportez les modifications requises au formulaire.

#### Étape 4 : Validez votre analyse et vos correctifs {#step-validate-your-analysis-and-fixes}

Au cours de cette étape, vous allez valider les modifications que vous avez apportées au formulaire et vérifier si elles affectent le taux de conversion.

**Exécution d’un test A/B**

L’intégration d’AEM Forms à Target permet de créer des tests A/B pour les formulaires adaptatifs. Dans les tests A/B, vous présentez aléatoirement différentes expériences d’un formulaire à vos clients en temps réel pour savoir quelle expérience fonctionne le mieux ou génère le plus de conversions. Une fois que vous disposez de données significatives indiquant qu’une expérience offre une meilleure conversion que l’autre, vous pouvez déclarer que les expériences ont remporté le prix. À partir de ce moment, elle devient l’expérience par défaut visible par tous les clients.

Pour plus d’informations sur la création d’un test A/B pour un formulaire adaptatif, voir [Test A/B des formulaires adaptatifs](../../forms/using/ab-testing-adaptive-forms.md).

![Exemple de rapport de synthèse de test A/B pour un formulaire adaptatif](assets/ab-test-report-4.png)

## Bonnes pratiques {#best-practices}

Les bonnes pratiques sont celles que vous identifiez vous-même lors de l’exécution de ce workflow. Elles sont propres à votre environnement et à vos exigences. Capturez vos apprentissages dans le workflow et documentez-les en tant que bonnes pratiques.

Voici quelques recommandations sur la conception de formulaires et l’exécution de tests A/B :

**Conception Forms**

* Faites en sorte que le formulaire reste simple, court et facile à parcourir. Utilisez des repères directionnels pour le parcourir.
* Utilisez des terminologies standard ou courantes pour les champs du formulaire.
* Expliquez le champ et l’entrée requise, avec des exemples ou une aide, là où les utilisateurs risquent d’être déconcertés.
* Validez les entrées des utilisateurs au fur et à mesure qu’ils les tapent, dans la mesure du possible, pour éviter des erreurs lors de l’envoi du formulaire.
* Optimisez les mises en page pour les ordinateurs de bureau et les appareils mobiles.
* Renseignez automatiquement les informations relatives aux utilisateurs connus.

**Tests A/B**

* Formulez une hypothèse et identifiez les mesures de succès avant d’exécuter le test A/B.
* Effectuez des variations minimales (dans l’idéal, une à la fois) de votre expérience alternative pour savoir ce qui a influé le taux de conversion.
* Testez fréquemment pour éliminer les inefficacités.
