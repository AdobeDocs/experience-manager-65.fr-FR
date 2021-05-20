---
title: Configuration d’AEM Forms pour envoyer des données de formulaire aux processus AEM Forms sur JEE
seo-title: Configuration d’AEM Forms pour envoyer des données de formulaire aux processus AEM Forms sur JEE
description: AEM Forms vous permet d’intégrer des formulaires adaptatifs aux processus AEM Forms sur JEE pour traiter les données des formulaires.
seo-description: AEM Forms vous permet d’intégrer des formulaires adaptatifs aux processus AEM Forms sur JEE pour traiter les données des formulaires.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Administrator
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 83%

---

# Configuration d’AEM Forms pour envoyer des données de formulaire aux processus AEM Forms sur JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Les formulaires adaptatifs prennent en charge l’envoi de données à un processus AEM Forms sur JEE pour un traitement ultérieur. Ils vous permettent de déclencher un processus AEM Forms sur JEE avec les données fournies par le formulaire envoyé. Pour permettre à votre instance AEM Forms d’envoyer un formulaire adaptatif au processus AEM Forms on JEE, procédez comme suit :

## Configurez votre serveur AEM Forms {#configure-your-aem-forms-server}

Effectuez les étapes suivantes pour permettre à votre serveur AEM Forms d’envoyer des données à un serveur AEM Forms sur JEE :

1. Accédez à AEM console de configuration web à l’adresse https://[*host*]:[*port*]/system/console/configMgr.

1. Recherchez et cliquez sur le composant **Configuration du SDK client d’Adobe LiveCycle**.
1. Cliquer pour modifier l’URL du serveur de configuration, le nom d’utilisateur et le mot de passe du serveur AEM Forms sur JEE.
1. Vérifiez les paramètres et cliquez sur **Enregistrer**.

![Configuration de SDK client Adobe LiveCycle](assets/clientsdkconfiguration.jpg)

## Associez les données aux champs de processus {#map-data-with-process-fields}

Une fois que votre AEM Forms est configuré, associez les données XML et les pièces jointes du formulaire envoyé aux champs du processus AEM Forms sur JEE. Pour ce faire :

1. Dans la console de configuration web d’AEM, cliquez pour modifier la configuration **Localisateur et invocateur du processus Guide LiveCycle**.
1. Spécifiez les paramètres suivants :

   * **Nom du paramètre**  XML de données (obligatoire) : Spécifiez le fichier de propriétés XML du processus AEM Forms on JEE qui doit traiter les données envoyées. La valeur par défaut est **dataxml**.

   * **Nom du paramètre de pièces jointes**(facultatif) : spécifiez la liste d’objets de document que le processus AEM Forms sur JEE doit traiter. La valeur par défaut est **fileAttachmentsList**.

1. Vérifiez les paramètres et cliquez sur **Enregistrer**.

![Localisateur et invocateur du processus Guide LiveCycle](assets/test3.jpg)

Une fois configurée, l’action Envoi au processus de serveur de formulaires liste les processus du serveur AEM Forms sur JEE contenant le paramètre XML des données spécifié.
