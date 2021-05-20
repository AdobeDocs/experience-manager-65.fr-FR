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
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 2%

---

# Présentation des processus AEM Forms {#understanding-aem-forms-processes}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Un cas d’utilisation courant est qu’un ensemble de services AEM Forms fonctionne sur un seul document. Vous pouvez envoyer une requête au conteneur de services en créant un processus à l’aide de Workbench. Un processus représente un processus d’entreprise que vous automatisez. Pour plus d’informations sur la création de processus, voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Une fois qu’un processus est activé, il devient un service et peut être appelé comme d’autres services. Une différence entre un service standard, tel que le service Encryption, et un service issu d’un processus, est que ce dernier comporte une opération qui effectue de nombreuses actions. En revanche, un service standard comporte de nombreuses opérations. Chaque opération effectue généralement une action, telle que l’application d’une stratégie à un document ou le chiffrement d’un document.

Les processus peuvent être de courte durée ou de longue durée. Un processus de courte durée est une opération effectuée de manière synchrone et sur le même thread d’exécution à partir duquel il a été appelé. Les opérations de courte durée sont comparables au comportement standard trouvé dans la plupart des langages de programmation, où une application cliente appelle une méthode et attend une valeur renvoyée.

Cependant, il existe des situations où un processus ne peut pas être exécuté de manière synchrone en raison de facteurs tels que :

* Un processus peut s’étendre sur un temps considérable.
* Un processus peut dépasser les limites organisationnelles.
* Un processus a besoin d’une entrée externe pour se terminer. Prenons l’exemple d’un formulaire envoyé à un responsable absent du bureau. Dans ce cas, le processus n’est pas terminé tant que le gestionnaire ne retourne pas et ne remplit pas le formulaire.

   Ces types de processus sont appelés processus de longue durée. Un processus de longue durée est exécuté de manière asynchrone, ce qui permet aux systèmes d’interagir lorsque les ressources le permettent et permet le suivi et la surveillance de l’opération. Lorsqu’un processus de longue durée est appelé, AEM Forms crée une valeur d’identifiant d’appel dans le cadre d’un enregistrement qui effectue le suivi de l’état du processus de longue durée. L’enregistrement est stocké dans la base de données AEM Forms. Vous pouvez purger les enregistrements de processus de longue durée lorsqu’ils ne sont plus nécessaires.

>[!NOTE]
>
>AEM Forms ne crée pas d’enregistrement lorsqu’un processus de courte durée est appelé.

La valeur de l’identifiant d’appel vous permet de suivre l’état du processus de longue durée. Par exemple, vous pouvez utiliser la valeur de l’identifiant d’appel de processus pour effectuer des opérations Process Manager, comme arrêter une instance de processus en cours d’exécution.

**Exemple de processus de courte durée**

L’illustration suivante est un exemple de processus de courte durée appelé *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre les exemples de code qui expliquent comment appeler ce processus, créez un processus nommé `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Lorsque ce processus de courte durée est appelé, il effectue les actions suivantes :

1. Obtient le document PDF non sécurisé transmis au processus en tant que valeur d’entrée.
1. Chiffrement du document PDF avec un mot de passe. Le nom du paramètre d’entrée pour ce processus est `inDoc` et le type de données est document.
1. Enregistre le document PDF chiffré par mot de passe en tant que fichier PDF dans le système de fichiers local. Ce processus renvoie le document PDF chiffré en tant que valeur de sortie. Le nom du paramètre de sortie pour ce processus est `outDoc` et le type de données est document.

   Ce processus est terminé de manière synchrone sur le même thread d’exécution à partir duquel il a été appelé. Le nom de ce processus de courte durée est `MyApplication/EncryptDocument`et son opération est `invoke`.

   >[!NOTE]
   >
   >En règle générale, un processus de courte durée comprend plus de trois actions. Vous créez un processus à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *La programmation avec AEM* forms décrit les méthodes suivantes par programmation pour appeler ce processus de courte durée :

   * [Appel d’un processus de courte durée en transmettant un document non sécurisé à l’aide d’AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)  (à l’aide d’une application Flex)
   * [Appel d’un processus de courte durée à l’aide de l’API d’appel ](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)  (API d’appel Java)
   * [Appel d’AEM Forms à l’aide de l’encodage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)  Base64 (exemple de service Web)
   * [Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)  (exemple de service Web)
   * [Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)  (exemple de service Web)
   * [Appel d’AEM Forms à l’aide de données BLOB sur HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)  (exemple de service Web)
   * [Appel d’AEM Forms à l’aide de DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime)  (exemple de service Web)
   * [Appel du processus MyApplication/EncryptDocument à l’aide de REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Exemple de processus de longue durée**

L’illustration suivante est un exemple de processus de longue durée.

Ce processus est appelé lorsqu’un demandeur envoie un formulaire de prêt. Le processus n’est pas terminé tant qu’un agent de prêt n’a pas approuvé ou rejeté la demande de prêt. Le nom de ce processus de longue durée est *FirstAppSolution/PreLoanProcess* et son opération est `invoke_Async`. Ce processus doit être appelé de manière asynchrone. Pour plus d’informations sur l’appel par programmation de ce processus de longue durée, voir [Appel de processus de longue durée pour des intervenants humains](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Ce processus peut être créé en suivant le tutoriel spécifié dans [Création de votre première application AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
