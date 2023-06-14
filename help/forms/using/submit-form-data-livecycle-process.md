---
title: Configuration d’AEM Forms pour envoyer des données à un processus AEM Forms on JEE
description: Intégration de formulaires adaptatifs aux processus AEM Forms on JEE pour le traitement des données de formulaire.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 28%

---

# Configuration d’AEM Forms pour envoyer des données de formulaire à un processus AEM de formulaire sur JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Les formulaires adaptatifs prennent en charge l’envoi de données au processus AEM Forms on JEE pour un traitement ultérieur. Il vous permet de déclencher un processus AEM Forms on JEE avec les données disponibles à partir du formulaire envoyé. Effectuez les étapes suivantes afin de permettre à votre instance AEM Forms d’envoyer un formulaire adaptatif au processus AEM Forms on JEE :

## Configuration de votre serveur AEM Forms {#configure-your-aem-forms-server}

Effectuez les étapes suivantes afin de permettre à votre serveur AEM Forms d’envoyer des données à un serveur AEM Forms on JEE :

1. Accédez à la configuration de console web AEM à l’adresse https://[*host*]:[*port*]/system/console/configMgr.

1. Recherchez et cliquez sur le composant **Configuration du SDK client d’Adobe LiveCycle**.
1. Cliquez pour modifier l’URL du serveur de configuration, le nom d’utilisateur et le mot de passe du serveur AEM Forms on JEE.
1. Vérifiez les paramètres et cliquez sur **Enregistrer**.

![Configuration de SDK client Adobe LiveCycle](assets/clientsdkconfiguration.jpg)

## Associez les données aux champs de processus {#map-data-with-process-fields}

Après avoir configuré AEM Forms, mappez les données XML et les pièces jointes du formulaire envoyé aux champs du processus AEM Forms on JEE. Procédez comme suit :

1. Dans AEM console de configuration web, cliquez sur pour éditer le **Localisateur et invocateur du processus de LiveCycle de guide** configuration.
1. Spécifiez les paramètres suivants :

   * **Nom du paramètre xml de données** (obligatoire) : Spécifiez le fichier de propriétés XML du processus AEM Forms on JEE qui doit traiter les données envoyées. La valeur par défaut est **dataxml**.

   * **Nom du paramètre de pièces jointes** (facultatif) : Spécifiez la liste des objets de document que le processus AEM Forms on JEE doit traiter. La valeur par défaut est **fileAttachmentsList**.

1. Vérifiez les paramètres et cliquez sur **Enregistrer**.

![Localisateur et invocateur du processus Guide LiveCycle](assets/test3.jpg)

Une fois configurée, l’action Envoi au processus de serveur de formulaires liste les processus du serveur AEM Forms sur JEE contenant le paramètre XML des données spécifié.
