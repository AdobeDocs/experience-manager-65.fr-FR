---
title: Détails du document pour le moteur de rendu
description: Informations conceptuelles sur le fonctionnement des rendus dans l’espace de travail AEM Forms pour le rendu des différents types de formulaires et de fichiers pris en charge.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 53%

---

# Détails du document pour le moteur de rendu {#document-details-for-renderer}

## Présentation {#introduction}

Dans l’espace de travail AEM Forms, plusieurs types de formulaires sont pris en charge en toute transparence. Celles-ci comprennent les éléments suivants :

* PDF forms (XDP/Acroform/PDF plats)
* Nouveaux formulaires de HTML
* Images
* Applications tierces (par exemple, Correspondence Management)

Ce document explique le fonctionnement de ces rendus du point de vue de la personnalisation sémantique/réutilisation des composants, afin que les exigences du client soient satisfaites sans compromettre le rendu. L’espace de travail AEM Forms autorise tous les changements d’interface utilisateur/sémantiques, mais il est recommandé de ne pas modifier la logique de rendu de différents types de formulaires car les résultats peuvent être imprévisibles. Ce document fournit des conseils/des connaissances pour prendre en charge le rendu du même formulaire, en utilisant les mêmes composants de l’espace de travail dans différents portails, et non pour modifier la logique de rendu elle-même.

## PDF forms {#pdf-forms}

Les formulaires PDF sont rendus par `PdfTaskForm View`.

Lorsqu’un formulaire XDP est rendu au format PDF, un `FormBridge` JavaScript™ est ajouté par le service FormsAugmenter. Ce JavaScript™ (dans le formulaire PDF) permet d’effectuer des actions telles que l’envoi d’un formulaire, la sauvegarde d’un formulaire ou la mise hors ligne d’un formulaire.

Dans l’espace de travail AEM Forms, la vue PDFTaskForm communique avec le `FormBridge`JavaScript, au moyen d’un HTML intermédiaire présent à l’adresse `/lc/libs/ws/libs/ws/pdf.html`. Le flux est :

**Vue PDFTaskForm - pdf.html**

Communique à l’aide de `window.postMessage` / `window.attachEvent('message')`.

Cette méthode est la méthode standard de communication entre un cadre parent et un iframe. Les écouteurs d’événement existants issus de formulaires PDF précédemment ouverts sont supprimés avant d’en ajouter un nouveau. Cette purge prend également en compte le passage de l’onglet Formulaire à l’onglet Historique dans la vue Détails de la tâche.

**pdf.html - `FormBridge`JavaScript dans le PDF rendu**

Communique à l’aide de `pdfObject.postMessage` / `pdfObject.messageHandler`.

Cette méthode est la méthode standard de communication d’un PDF Javascript depuis un fichier HTML. La vue PdfTaskForm prend également en charge un PDF plat et le rend brut.

>[!NOTE]
>
>Il n’est pas recommandé de modifier le pdf.html/contenu de la vue PdfTaskForm.

## Nouvelle Forms de HTML {#new-html-forms}

Les nouveaux formulaires de HTML sont rendus par la vue NewHTMLTaskForm.

Lorsqu’un formulaire XDP est rendu en tant que HTML à l’aide du package Mobile Forms déployé sur CRX, il ajoute également un Javascript `FormBridge` supplémentaire au formulaire, ce qui fournit différentes méthodes pour l’enregistrement et l’envoi des données de formulaire.

Ce code JavaScript est différent de celui mentionné dans les PDF forms ci-dessus, mais a un objectif similaire.

>[!NOTE]
>
>Adobe ne recommande pas de modifier le contenu de la vue NewHTMLTaskForm.

## Forms et guides Flex {#flex-forms-and-guides}

Flex Forms est rendu par SwfTaskForm et les guides sont rendus par les vues HtmlTaskForm respectivement.

Dans l’espace de travail AEM Forms, ces vues communiquent avec le SWF réel qui constitue le formulaire/guide Flex® à l’aide d’un SWF intermédiaire présent dans `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La communication se fait par `swfObject.postMessage` / `window.flexMessageHandler`.

Ce protocole est défini par le `WsNextAdapter.swf`. Les `flexMessageHandlers` existants sur l’objet de la fenêtre, issus des formulaires SWF précédemment ouverts sont supprimés avant d’en ajouter un nouveau. La logique prend également en compte le passage de l’onglet Formulaire à l’onglet Historique dans la vue Détails de la tâche. La variable `WsNextAdapter.swf` sert à effectuer diverses actions de formulaire, telles que l’enregistrement ou l’envoi.

>[!NOTE]
>
>il n’est pas recommandé de modifier `WSNextAdapter.swf` ou le contenu de la vue SwfTaskForm / HtmlTaskForm.

## Applications tierces (par exemple, Correspondence Management) {#third-party-applications-for-example-correspondence-management}

Les applications tierces sont rendues à l’aide de la vue ExtAppTaskForm.

**Communication entre l’application tierce et l’espace de travail AEM Forms**

L’espace de travail AEM Forms écoute sur `window.global.postMessage([Message],[Payload])`.

[Message] peut être une chaîne spécifiée comme `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage` dans le `runtimeMap`. Les applications tierces doivent utiliser cette interface pour avertir l’espace de travail AEM Forms si nécessaire. L’utilisation de cette interface est obligatoire, car l’espace de travail AEM Forms doit savoir lorsque la tâche est envoyée pour nettoyer la fenêtre de tâche.

**Communication entre lʼespace de travail AEM Forms et l’application tierce**

Si les boutons d’action directe de l’espace de travail AEM Forms sont visibles, il appelle `window.[External-App-Name].getMessage([Action])`, où `[Action]` est lu à partir de `routeActionMap`. L’application tierce doit écouter sur cette interface, puis informer lʼespace de travail AEM Forms via l’API `postMessage ()`.

Par exemple, une application Flex peut définir `ExternalInterface.addCallback('getMessage', listener)` pour prendre en charge cette communication. Si l’application tierce souhaite gérer l’envoi de formulaire via ses propres boutons, vous devez spécifier `hideDirectActions = true() in the runtimeMap` et vous pouvez ignorer cet écouteur. Par conséquent, ce concept est facultatif.

Pour en savoir plus sur l’intégration d’applications tierces concernant Correspondence Management, voir [Intégration de Correspondence Management dans l’espace de travail AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
