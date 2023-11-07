---
title: Configuration des règles de traduction
description: Découvrez comment définir des règles de traduction pour identifier le contenu à traduire.
exl-id: 262503af-361b-491c-8639-0bb32f0a4c0e
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 76%

---

# Configuration des règles de traduction {#configure-translation-rules}

Découvrez comment définir des règles de traduction pour identifier le contenu à traduire.

## Un peu d’histoire… {#story-so-far}

Dans le document précédent du parcours de traduction AEM, [Configuration de l’intégration de traduction](configure-connector.md) vous avez appris à installer et configurer votre intégration de traduction et vous devez maintenant :

* comprendre les paramètres importants de la structure d’intégration de traduction dans AEM ;
* savoir configurer votre propre connexion à votre service de traduction.

Maintenant que votre intégration est configurée, cet article vous guide tout au long de l’étape suivante d’identification du contenu à traduire.

## Objectif {#objective}

Ce document vous aide à comprendre comment utiliser les règles de traduction d’AEM pour identifier votre contenu de traduction. Après avoir lu ce document, vous devriez :

* comprendre ce que font les règles de traduction ;
* être capable de définir vos propres règles de traduction.

## Règles de traduction {#translation-rules}

Les fragments de contenu, qui représentent votre contenu découplé, peuvent contenir de nombreuses informations organisées dans des champs structurés. Selon les besoins de votre projet, il est probable que tous les champs d’un fragment de contenu ne doivent pas être traduits.

Les règles de traduction identifient le contenu à inclure dans les projets de traduction ou à exclure. Lorsque le contenu est traduit, AEM extrait ou récupère le contenu en fonction de ces règles. Ainsi, seul le contenu à traduire est envoyé au service de traduction.

Les règles de traduction comprennent les informations suivantes :

* Le chemin d’accès au contenu auquel la règle s’applique
   * La règle s’applique également aux descendants du contenu
* Les noms des propriétés contenant le contenu à traduire
   * Cette propriété peut être spécifique à un type de ressource en particulier ou à tous les types de ressource

Les modèles de fragment de contenu, qui définissent la structure de vos fragments de contenu, sont uniques à votre projet, c’est pourquoi il est essentiel de configurer des règles de traduction pour qu’AEM sache quels éléments traduire parmi vos modèles de contenu.

>[!TIP]
>
>En règle générale, l’architecte de contenu met à la disposition du spécialiste de traduction les éléments suivants : **Nom de la propriété** de tous les champs nécessaires à la traduction. Ces noms sont nécessaires pour configurer les règles de traduction. En tant que spécialiste de la traduction, vous [pouvez trouver vous-même les **Noms de la propriété**](getting-started.md#content-models) comme décrit précédemment dans ce parcours.

## Création de règles de traduction {#creating-rules}

Plusieurs règles peuvent être créées pour prendre en charge des exigences de traduction complexes. Par exemple, un projet sur lequel vous travaillez peut nécessiter la traduction de tous les champs du modèle, mais pour un autre, seuls les champs de description doivent être traduits, tandis que les titres ne sont pas traduits.

Les règles de traduction sont conçues pour gérer ces scénarios. Cependant, dans cet exemple, nous illustrons comment créer des règles en se concentrant sur une configuration simple et unique.

Il existe une console **Configuration de traduction** disponible pour la configuration des règles de traduction. Pour y accéder :

1. Accédez à **Outils** -> **Général**.
1. Appuyez ou cliquez sur **Configuration de traduction**.

Dans le **Configuration de traduction** Dans l’interface utilisateur, plusieurs options sont disponibles pour vos règles de traduction. Dans cette partie, nous mettons en évidence les étapes les plus nécessaires et les plus courantes requises pour une configuration de localisation découplée de base.

1. Appuyez ou cliquez sur **Ajouter un contexte**, qui vous permet d’ajouter un chemin. Il s’agit du chemin d’accès du contenu qui sera affecté par la règle.
   ![Ajoutez du contexte](assets/add-translation-context.png)
1. Utilisez le navigateur de chemins d’accès pour sélectionner le chemin requis et appuyez ou cliquez sur le bouton **Confirmer** pour enregistrer. N’oubliez pas que les fragments de contenu, qui contiennent du contenu découplé, se trouvent généralement sous `/content/dam/<your-project>`.
   ![Sélectionnez le chemin d’accès](assets/select-context.png)
1. AEM enregistre la configuration.
1. Vous devez sélectionner le contexte que vous avez créé, puis appuyer ou cliquer sur **Modifier**. Vous ouvrez ainsi la fenêtre de l’**Éditeur de règles de traduction** pour configurer les propriétés.
   ![Éditeur de règles de traduction](assets/translation-rules-editor.png)
1. Par défaut, toutes les configurations sont héritées du chemin d’accès parent, dans ce cas `/content/dam`. Décochez l’option **Hériter de`/content/dam`** pour ajouter des champs supplémentaires à la configuration.
1. Une fois la case désélectionnée, dans la section **Général** de la liste, ajoutez les noms des propriétés du ou des modèles de fragment de contenu que vous avez [précédemment identifiés comme des champs à traduire](getting-started.md#content-models).
   1. Saisissez le nom de la propriété dans le champ **Nouvelle propriété**.
   1. Les options **Traduire** et **Hériter** sont cochées automatiquement.
   1. Appuyez ou cliquez sur **Ajouter**.
   1. Répétez ces étapes pour tous les champs que vous devez traduire.
   1. Cliquez ou appuyez sur **Enregistrer**.
      ![Ajouter une propriété](assets/add-property.png)

Vous avez maintenant configuré vos règles de traduction.

## Utilisation avancée {#advanced-usage}

Plusieurs propriétés supplémentaires peuvent être configurées dans le cadre de vos règles de traduction. En outre, vous pouvez spécifier vos règles manuellement au format XML, ce qui vous permet d’obtenir plus de précision et de flexibilité.

Ces fonctionnalités ne sont généralement pas nécessaires pour commencer à localiser votre contenu découplé, mais vous pouvez en apprendre plus à ce sujet dans la section [Ressources supplémentaires](#additional-resources), si vous êtes intéressé.

## Prochaines étapes {#what-is-next}

Maintenant que vous avez terminé cette partie du parcours de traduction découplée, vous devriez savoir :

* comprendre ce que font les règles de traduction ;
* être capable de définir vos propres règles de traduction.

Tirez parti de ces connaissances et continuez votre parcours de traduction AEM sans interface utilisateur graphique en consultant le document. [Traduire le contenu](translate-content.md) où vous apprendrez comment votre intégration et vos règles fonctionnent ensemble pour traduire du contenu headless.

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de traduction découplée en consultant le document [Traduire du contenu](translate-content.md), vous trouverez ci-après quelques ressources facultatives supplémentaires pour approfondir un certain nombre de concepts mentionnés dans ce document, même s’ils ne sont pas nécessaires pour poursuivre le parcours en mode découplé.

* [Identification du contenu à traduire](/help/sites-administering/tc-rules.md) – Découvrez comment les règles de traduction identifient le contenu à traduire.
