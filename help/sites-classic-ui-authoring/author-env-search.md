---
title: Rechercher
description: L’environnement de création d’AEM comporte divers mécanismes de recherche de contenu, selon le type de ressource que vous utilisez.
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 50%

---

# Rechercher{#searching}

L’environnement de création d’AEM comporte divers mécanismes de recherche de contenu, selon le type de ressource que vous utilisez.

>[!NOTE]
>
>En dehors de l’environnement de création, d’autres mécanismes sont également disponibles pour la recherche, tels que le [Query Builder](/help/sites-developing/querybuilder-api.md) et [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Principes de base de la recherche {#search-basics}

Pour accéder au panneau de recherche, cliquez sur l’onglet **Rechercher** dans la partie supérieure du volet de gauche de la console appropriée.

![chlimage_1-101](assets/chlimage_1-101.png)

Dans le panneau de recherche, vous pouvez effectuer des recherches dans toutes les pages de votre site Web. Il contient des champs et des widgets pour les éléments suivants :

* **Texte intégral**: Recherche du texte spécifié
* **Modifié après/avant**: Recherche uniquement les pages qui ont été modifiées entre les dates spécifiques
* **Modèle**: Recherche uniquement ces pages en fonction du modèle spécifié
* **Balises**: Recherche uniquement les pages contenant les balises spécifiées

>[!NOTE]
>
>Lorsque votre instance est configurée pour la [recherche Lucene](/help/sites-deploying/queries-and-indexing.md), vous pouvez utiliser l’expression suivante en **texte intégral** :
>
>* [Caractères génériques](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [Opérateurs booléens](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [Expressions régulières](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Regroupement de champs](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Amélioration](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>


Exécutez la recherche en cliquant sur **Rechercher** au bas du volet. Cliquez sur **Réinitialiser** pour effacer les critères de recherche.

## Filtrer {#filter}

À différents emplacements, un filtre peut être défini (et effacé) pour analyser en profondeur et affiner votre vue :

![chlimage_1-102](assets/chlimage_1-102.png)

## Rechercher et remplacer {#find-and-replace}

Dans le **Sites web** console **Chercher et Remplacer** l’option de menu vous permet de rechercher et de remplacer plusieurs instances d’une chaîne dans une section du site web.

1. Sélectionnez la page racine, ou le dossier, dans lequel vous souhaitez que l’action de recherche et de remplacement soit effectuée.
1. Sélectionner **Outils** then **Chercher et Remplacer**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. Le **Chercher et Remplacer** La boîte de dialogue effectue les opérations suivantes :

   * confirme le chemin racine où l’action de recherche doit commencer
   * définit le terme à rechercher.
   * définit le terme qui doit le remplacer ;
   * indique si la recherche doit être sensible à la casse
   * indique si seuls des mots entiers doivent être trouvés (sinon des sous-chaînes sont également trouvées)

   Cliquez sur **Aperçu** pour savoir où a été trouvé le terme. Vous pouvez sélectionner/désélectionner des instances spécifiques à remplacer :

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Cliquez sur **Remplacer** pour remplacer toutes les instances. Vous serez alors invité à confirmer l’opération.

L’étendue par défaut du servlet de recherche et de remplacement couvre les propriétés suivantes :

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

L’étendue peut être modifiée à l’aide de la console de gestion Web Apache Felix (par exemple, `https://localhost:4502/system/console/configMgr`). Sélectionnez `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` et configurez l’étendue suivant les besoins.

>[!NOTE]
>
>Dans une installation d’AEM standard, Find and Replace utilise Lucene comme fonctionnalité de recherche.
>
>Lucene indexe les propriétés de chaîne d’une longueur maximale de 16 Ko. Les chaînes en trop ne seront pas recherchées.
