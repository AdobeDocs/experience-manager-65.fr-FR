---
title: Présentation des processus AEM Forms
seo-title: Présentation des processus AEM Forms
description: Présentation des processus AEM Forms
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 2%

---


# Présentation des processus AEM Forms {#understanding-aem-forms-processes}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Un cas d&#39;utilisation courant est qu&#39;un ensemble de services AEM Forms fonctionne sur un seul document. Vous pouvez envoyer une demande au conteneur de services en créant un processus à l’aide de Workbench. Un processus représente un processus d’entreprise que vous automatisez. Pour plus d’informations sur la création de processus, voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Une fois qu’un processus est activé, il devient un service et peut être appelé comme d’autres services. Une différence entre un service standard, tel que le service Encryption, et un service issu d’un processus, réside dans le fait que ce dernier dispose d’une opération qui exécute de nombreuses actions. En revanche, un service standard comporte de nombreuses opérations. Chaque opération exécute généralement une action, telle que l’application d’une stratégie à un document ou le chiffrement d’un document.

Les processus peuvent être de courte ou de longue durée. Un processus de courte durée est une opération exécutée de manière synchrone et sur le même thread d’exécution à partir duquel il a été appelé. Les opérations de courte durée sont comparables au comportement standard de la plupart des langages de programmation, où une application cliente appelle une méthode et attend une valeur renvoyée.

Cependant, il arrive qu’un processus ne puisse pas être exécuté de façon synchrone en raison de facteurs tels que :

* Un processus peut s’étendre sur une période considérable.
* Un processus peut dépasser les limites organisationnelles.
* Un processus a besoin d’une entrée externe pour se terminer. Prenons l’exemple d’un cas où un formulaire est envoyé à un responsable absent du bureau. Dans ce cas, le processus n’est pas terminé tant que le gestionnaire ne retourne pas et ne remplit pas le formulaire.

   Ces types de processus sont appelés processus de longue durée. Un processus de longue durée est exécuté de manière asynchrone, ce qui permet aux systèmes d’interagir lorsque les ressources le permettent et permet le suivi et la surveillance de l’opération. Lorsqu’un processus de longue durée est appelé, AEM Forms crée une valeur d’identificateur d’appel dans le cadre d’un enregistrement qui effectue le suivi de l’état du processus de longue durée. L&#39;enregistrement est stocké dans la base de données AEM Forms. Vous pouvez purger les enregistrements de processus de longue durée lorsqu’ils ne sont plus nécessaires.

>[!NOTE]
>
>AEM Forms ne crée pas d’enregistrement lorsqu’un processus de courte durée est appelé.

A l’aide de la valeur d’identifiant d’appel, vous pouvez suivre l’état du processus de longue durée. Par exemple, vous pouvez utiliser la valeur de l’identifiant d’appel de processus pour effectuer des opérations Process Manager telles que l’arrêt d’une instance de processus en cours d’exécution.

**Exemple de processus de courte durée**

L’illustration suivante illustre un exemple de processus de courte durée nommé *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre les exemples de code qui expliquent comment appeler ce processus, créez un processus nommé `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Lorsque ce processus de courte durée est appelé, il effectue les actions suivantes :

1. Obtient le document PDF non sécurisé transmis au processus en tant que valeur d’entrée.
1. Chiffrement du document PDF avec un mot de passe. Le nom du paramètre d&#39;entrée pour ce processus est `inDoc` et le type de données est document.
1. Enregistre le document PDF chiffré par mot de passe sous la forme d’un fichier PDF dans le système de fichiers local. Ce processus renvoie le document PDF chiffré en tant que valeur de sortie. Le nom du paramètre de sortie pour ce processus est `outDoc` et le type de données est document.

   Ce processus est terminé de manière synchrone sur le même thread d’exécution que celui à partir duquel il a été appelé. Le nom de ce processus de courte durée est `MyApplication/EncryptDocument`et son opération est `invoke`.

   >[!NOTE]
   >
   >En règle générale, un processus de courte durée comprend plus de trois actions. Vous créez un processus à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *La programmation avec des* formulaires AEM décrit les manières suivantes d’appeler ce processus de courte durée par programmation :

   * [Appeler un processus de courte durée en transmettant un document non sécurisé à l’aide de AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)  (à l’aide d’une application Flex)
   * [Appel d’un processus de courte durée à l’aide de l’API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)  d’appel (API d’appel Java)
   * [Appel d’AEM Forms à l’aide de l’encodage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)  Base64 (exemple de service Web)
   * [Appeler AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)  (exemple de service Web)
   * [Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)  (exemple de service Web)
   * [Appeler AEM Forms à l’aide de données BLOB sur HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)  (exemple de service Web)
   * [Appeler AEM Forms à l’aide de DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime)  (exemple de service Web)
   * [Appel du processus MyApplication/EncryptDocument à l’aide de REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Exemple de processus de longue durée**

L’illustration suivante illustre un processus de longue durée.

Ce processus est appelé lorsqu’un demandeur envoie un formulaire de prêt. Le processus n&#39;est pas terminé tant qu&#39;un agent de prêt n&#39;a pas approuvé ou rejeté la demande de prêt. Le nom de ce processus de longue durée est *FirstAppSolution/PreLoanProcess* et son opération est `invoke_Async`. Ce processus doit être appelé de manière asynchrone. Pour plus d’informations sur l’appel programmatique de ce processus de longue durée, voir [Appel de processus de longue durée centrés sur l’homme](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Ce processus peut être créé en suivant le didacticiel spécifié dans [Création de votre première application AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).