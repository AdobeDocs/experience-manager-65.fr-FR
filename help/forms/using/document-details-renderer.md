---
title: Détails de document pour le rendu
seo-title: Détails de document pour le rendu
description: Informations conceptuelles sur le mode de fonctionnement du rendu de différents types de formulaires et de fichiers dans AEM Forms.
seo-description: Informations conceptuelles sur le mode de fonctionnement du rendu de différents types de formulaires et de fichiers dans AEM Forms.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 56%

---

# Détails de document pour le rendu {#document-details-for-renderer}

## Présentation {#introduction}

Dans l’espace de travail AEM Forms, plusieurs types de formulaires sont pris en charge en toute simplicité. Celles-ci comprennent :

* Formulaires PDF (XDP / Acroform / PDF aplatis)
* Nouveaux formulaires HTML
* Images
* Applications tierces (par exemple, Correspondence Management)

Ce document explique le fonctionnement de ces rendus du point de vue de la personnalisation sémantique/réutilisation des composants, afin que les exigences du client soient satisfaites sans compromettre le rendu. Bien que l’espace de travail AEM Forms autorise des modifications sémantiques/de l’interface utilisateur, il est recommandé de ne pas modifier la logique de rendu des différents types de formulaires, sinon les résultats peuvent être imprévisibles. Ce document fournit des conseils/des connaissances pour prendre en charge le rendu du même formulaire, avec les mêmes composants de Workspace dans différents portails, et non pour modifier la logique de rendu elle-même.

## Formulaires PDF {#pdf-forms}

Les PDF forms sont rendus par `PdfTaskForm View`.

Lorsqu’un formulaire XDP est rendu au format PDF, un `FormBridge` JavaScript™ est ajouté par le service FormsAugmenter. Ce JavaScript™ (dans le formulaire PDF) permet d’effectuer des actions telles que l’envoi d’un formulaire, la sauvegarde d’un formulaire ou la mise hors ligne d’un formulaire.

Dans l’espace de travail AEM Forms, la vue PDFTaskForm communique avec `FormBridge`javascript, via un code HTML intermédiaire présent à `/lc/libs/ws/libs/ws/pdf.html`. Le flux est :

**Vue PDFTaskForm - pdf.html**

Communique à l’aide de `window.postMessage` / `window.attachEvent('message')`

Cette méthode est la méthode standard de communication entre un cadre parent et un iframe. Les écouteurs d’événement existants issus de formulaires PDF précédemment ouverts sont supprimés avant d’en ajouter un nouveau. Cette purge tient également compte du passage de l’onglet Formulaire à l’onglet Historique et vice-versa dans la vue Détails de la tâche.

**PDF.html - `FormBridge` javascript dans le PDF rendu**

Communique à l’aide de `pdfObject.postMessage` / `pdfObject.messageHandler`

Cette méthode est la méthode de communication standard avec un PDFJavaScript à partir d’un code HTML. La vue PdfTaskForm prend aussi en charge le PDF aplati et effectue le rendu clair.

>[!NOTE]
>
>Il n’est pas recommandé de modifier le pdf.html/contenu de la vue PdfTaskForm.

## Nouveaux formulaires HTML  {#new-html-forms}

Les nouveaux formulaires HTML sont rendus par la vue NewHTMLTaskForm.

Lorsqu’un formulaire XDP est rendu au format HTML à l’aide du package de formulaires mobiles déployé sur CRX, il ajoute également du code JavaScript `FormBridge`supplémentaire au formulaire, qui expose différentes méthodes d’enregistrement et d’envoi de données de formulaire.

Ce code JavaScript est différent de celui référencé dans les PDF forms ci-dessus, mais a un objectif similaire.

>[!NOTE]
>
>Il n’est pas recommandé de modifier le contenu de la vue NewHTMLTaskForm.

## Guides et formulaires Flex {#flex-forms-and-guides}

Les formulaires Flex sont rendus par SwfTaskForm et les guides sont rendus par les vues HtmlTaskForm respectivement.

Dans l’espace de travail AEM Forms, ces vues communiquent avec le fichier SWF réel qui constitue le formulaire/guide flex à l’aide d’un fichier SWF intermédiaire présent à `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La communication se fait à l’aide de `swfObject.postMessage` / `window.flexMessageHandler`.

Ce protocole est défini par le `WsNextAdapter.swf`. Les `flexMessageHandlers` existants sur l’objet de la fenêtre, issus des formulaires SWF précédemment ouverts sont supprimés avant d’en ajouter un nouveau. La logique tient également compte du passage de l’onglet Formulaire à l’onglet Historique et vice-versa dans la vue Détails de la tâche. `WsNextAdapter.swf` est utilisé pour effectuer diverses actions de formulaire, comme la sauvegarde ou l’envoi.

>[!NOTE]
>
>il n’est pas recommandé de modifier `WSNextAdapter.swf` ou le contenu de la vue SwfTaskForm / HtmlTaskForm.

## Applications tierces (par exemple, Correspondence Management) {#third-party-applications-for-example-correspondence-management}

Les applications tierces sont rendues à l’aide de la vue ExtAppTaskForm.

**Communication entre l’application tierce et l’espace de travail AEM Forms**

L’espace de travail AEM Forms écoute sur `window.global.postMessage([Message],[Payload])`

[] Le message peut être une chaîne spécifiée comme  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|  `actionEnabledMessage`dans le  `runtimeMap`. Les applications tierces doivent utiliser cette interface pour avertir l’espace de travail AEM Forms si nécessaire. L’utilisation de cette interface est obligatoire, car l’espace de travail AEM Forms doit savoir que lorsque la tâche est envoyée, afin qu’elle puisse nettoyer la fenêtre de la tâche.

**Communication entre l’espace de travail AEM Forms et une application tierce**

Si les boutons d’action directe de l’espace de travail AEM Forms sont visibles, il appelle `window.[External-App-Name].getMessage([Action])`, où `[Action]` est lu à partir de la balise `routeActionMap`. L’application tierce doit écouter sur cette interface, puis notifier AEM Forms workspace via l’API `postMessage ()`.

Par exemple, une application Flex peut définir `ExternalInterface.addCallback('getMessage', listener)` pour prendre en charge cette communication. Si l’application tierce souhaite gérer l’envoi du formulaire via ses propres boutons, vous devez spécifier `hideDirectActions = true() in the runtimeMap` et vous pouvez ignorer cet écouteur. Par conséquent, cette syntaxe est facultative.

Pour plus d’informations sur l’interaction d’applications tierces, notamment Correspondence Management, voir [Intégration de Correspondence Management dans l’espace de travail AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
