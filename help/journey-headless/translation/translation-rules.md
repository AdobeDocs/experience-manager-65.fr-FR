---
title: Configuration des règles de traduction
description: Découvrez comment définir des règles de traduction pour identifier le contenu à traduire.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---

# Configuration des règles de traduction {#configure-translation-rules}

Découvrez comment définir des règles de traduction pour identifier le contenu à traduire.

## Un peu d’histoire...  {#story-so-far}

Dans le document précédent du parcours de traduction AEM, [Configuration du connecteur de traduction](configure-connector.md) vous avez appris à installer et configurer votre connecteur de traduction et vous devez maintenant :

* Découvrez les paramètres importants de la structure d’intégration de traduction dans AEM.
* Vous pouvez configurer votre propre connexion à votre service de traduction.

Maintenant que votre connecteur est configuré, cet article vous guide tout au long de l’étape suivante pour identifier le contenu à traduire.

## Objectif {#objective}

Ce document vous aide à comprendre comment utiliser AEM règles de traduction pour identifier votre contenu de traduction. Après avoir lu ce document, vous devriez :

* Comprendre ce que font les règles de traduction.
* Vous pouvez définir vos propres règles de traduction.

## Règles de traduction {#translation-rules}

Les fragments de contenu, qui représentent votre contenu headless, peuvent contenir de nombreuses informations organisées par des champs structurés. Selon les besoins de votre projet, il est probable que tous les champs d’un fragment de contenu ne doivent pas être traduits.

Les règles de traduction identifient le contenu qui est inclus dans les projets de traduction ou qui en est exclu. Lorsque le contenu est traduit, AEM extrait ou récupère le contenu en fonction de ces règles. Ainsi, seul le contenu à traduire est envoyé au service de traduction.

Les règles de traduction incluent les informations suivantes :

* Chemin d’accès au contenu auquel la règle s’applique
   * La règle s’applique également aux descendants du contenu.
* Les noms des propriétés qui contiennent le contenu à traduire
   * Cette propriété peut être spécifique à un type de ressource en particulier ou à tous les types de ressource

Comme les modèles de fragment de contenu, qui définissent la structure de vos fragments de contenu, sont propres à votre propre projet, il est essentiel de configurer des règles de traduction pour AEM connaître les éléments de vos modèles de contenu à traduire.

>[!TIP]
>
>En règle générale, l’architecte de contenu met à la disposition du spécialiste de traduction les éléments suivants : **Nom de la propriété** de tous les champs nécessaires à la traduction. Ces noms sont nécessaires pour configurer les règles de traduction. En tant que traducteur, vous [peuvent trouver les **Nom de la propriété** s&#39;il vous plaît](getting-started.md#content-models) comme décrit précédemment dans ce parcours.

## Création de règles de traduction {#creating-rules}

Plusieurs règles peuvent être créées pour prendre en charge des exigences de traduction complexes. Par exemple, un projet sur lequel vous travaillez peut nécessiter la traduction de tous les champs du modèle, mais sur un autre, seuls les champs de description doivent être traduits, tandis que les titres ne sont pas traduits.

Les règles de traduction sont conçues pour gérer de tels scénarios. Cependant, dans cet exemple, nous illustrons comment créer des règles en se concentrant sur une configuration simple et unique.

Il existe une **Configuration de traduction** console disponible pour la configuration des règles de traduction. Pour y accéder :

1. Accédez à **Outils** -> **Général**.
1. Appuyez ou cliquez sur **Configuration de traduction**.

Dans le **Configuration de traduction** Dans l’interface utilisateur, plusieurs options sont disponibles pour vos règles de traduction. Nous mettons en évidence ici les étapes les plus nécessaires et les plus courantes requises pour une configuration de localisation de base sans interface.

1. Appuyez ou cliquez sur **Ajouter un contexte**, qui vous permet d’ajouter un chemin. Il s’agit du chemin d’accès du contenu qui sera affecté par la règle.
   ![Ajouter un contexte](assets/add-translation-context.png)
1. Utilisez l’explorateur de chemins d’accès pour sélectionner le chemin d’accès requis et appuyez ou cliquez sur l’icône **Confirmer** pour enregistrer. N’oubliez pas que les fragments de contenu, qui contiennent du contenu sans affichage, se trouvent généralement sous `/content/dam/<your-project>`.
   ![Sélectionner le chemin](assets/select-context.png)
1. AEM enregistre la configuration.
1. Vous devez sélectionner le contexte que vous venez de créer, puis appuyer ou cliquer sur **Modifier**. Cela ouvre la fenêtre **Éditeur de règles de traduction** pour configurer les propriétés.
   ![Éditeur de règles de traduction](assets/translation-rules-editor.png)
1. Par défaut, toutes les configurations sont héritées du chemin d’accès parent, dans ce cas. `/content/dam`. Décochez l’option . **Hériter de`/content/dam`** afin d&#39;ajouter des champs supplémentaires à la configuration.
1. Une fois la case décochée, sous **Général** dans la liste, ajoutez les noms des propriétés du ou des modèles de fragment de contenu que vous souhaitez [précédemment identifié comme champs à traduire.](getting-started.md#content-models)
   1. Saisissez le nom de la propriété dans le champ **Nouvelle propriété** champ .
   1. Les options **Traduire** et **Hériter** sont cochées automatiquement.
   1. Appuyez ou cliquez sur **Ajouter**.
   1. Répétez ces étapes pour tous les champs que vous devez traduire.
   1. Cliquez ou appuyez sur **Enregistrer**.
      ![Ajouter une propriété](assets/add-property.png)

Vous avez maintenant configuré vos règles de traduction.

## Utilisation avancée {#advanced-usage}

Plusieurs propriétés supplémentaires peuvent être configurées dans le cadre de vos règles de traduction. En outre, vous pouvez spécifier vos règles manuellement au format XML, ce qui vous permet d’obtenir plus de précision et de flexibilité.

Ces fonctionnalités ne sont généralement pas nécessaires pour commencer à localiser votre contenu headless, mais vous pouvez en apprendre plus à ce sujet dans la section [Ressources supplémentaires](#additional-resources) si vous êtes intéressé.

## Et après ? {#what-is-next}

Maintenant que vous avez terminé cette partie du parcours de traduction sans interface utilisateur graphique, vous devez :

* Comprendre ce que font les règles de traduction.
* Vous pouvez définir vos propres règles de traduction.

Tirez parti de ces connaissances et continuez votre parcours de traduction AEM sans interface utilisateur graphique en consultant le document. [Traduire le contenu](translate-content.md) où vous découvrirez comment votre connecteur et vos règles fonctionnent ensemble pour traduire du contenu headless.

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de traduction sans interface utilisateur graphique en consultant le document [Traduire le contenu](translate-content.md), voici quelques autres ressources facultatives qui approfondissent certains concepts mentionnés dans ce document, mais qui ne sont pas nécessaires pour continuer sur le parcours sans interface.

* [Identification du contenu à traduire](/help/sites-administering/tc-rules.md) - Découvrez comment les règles de traduction identifient le contenu à traduire.
