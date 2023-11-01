---
title: Présentation des processus AEM Forms
description: Découvrez comment les processus AEM Forms englobent la création, l’envoi, la gestion des données, la validation, l’intégration, l’automatisation des workflows et la gestion des sorties.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 93%

---

# Présentation des processus AEM Forms {#understanding-aem-forms-processes}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Un cas dʼutilisation courant consiste à utiliser un ensemble de services AEM Forms sur un seul document. Vous pouvez envoyer une demande au conteneur de services en créant un processus à l’aide de Workbench. Un processus correspond à un processus métier que vous souhaitez automatiser. Pour plus d’informations sur la création de processus, consultez la section [Utiliser Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).

Une fois quʼun processus est activé, il se mue en service et peut être sollicité à lʼinstar dʼautres services. Une différence entre un service standard, tel que le service Encryption, et un service issu dʼun processus, est que ce dernier possède une opération qui exécute de nombreuses actions. En revanche, un service standard comporte de nombreuses opérations. Chaque opération exécute généralement une seule action, comme lʼapplication dʼune politique à un document ou le chiffrement dʼun document.

Les processus peuvent être de courte ou de longue durée. Un processus de courte durée est une opération qui est exécutée de manière synchrone et sur le même thread dʼexécution que celui à partir duquel elle a été sollicitée. Les opérations de courte durée sont similaires au comportement standard de la plupart des langages de programmation, où une application cliente appelle une méthode et attend une valeur de retour.

Cependant, il existe des situations où un processus ne peut pas être exécuté de manière synchrone en raison de facteurs tels que :

* La durée dʼun processus peut être très longue.
* Un processus peut transcender le cadre de lʼentreprise.
* Un processus a besoin d’une entrée externe pour se terminer. À titre dʼexemple, on peut imaginer une situation où un formulaire est envoyé à un responsable qui a quitté son bureau. Dans ces circonstances, le processus ne peut être achevé avant le retour du responsable qui remplit le formulaire.

  Ces types de processus sont appelés processus de longue durée. Un processus de longue durée est exécuté de manière asynchrone, ce qui permet aux systèmes dʼinteragir en fonction des ressources disponibles et dʼassurer le suivi et la surveillance de lʼopération. Lorsquʼun processus de longue durée est appelé, AEM Forms crée une valeur dʼidentificateur de lʼappel dans le cadre d’un enregistrement qui permet de suivre le statut du processus de longue durée. L’enregistrement est stocké dans la base de données dʼAEM Forms. Les enregistrements de processus de longue durée peuvent être supprimés définitivement lorsqu’ils ne sont plus nécessaires.

>[!NOTE]
>
>AEM Forms ne crée pas d’enregistrement lorsqu’un processus de courte durée est appelé.

La valeur dʼidentificateur de lʼappel vous permet de suivre le statut du processus de longue durée. Ainsi, vous pouvez utiliser la valeur dʼidentificateur de lʼappel du processus pour effectuer des opérations dans le gestionnaire de processus, comme par exemple mettre fin à une instance de processus en cours dʼexécution.

**Exemple de processus de courte durée**

L’illustration suivante représente un exemple de processus de courte durée nommé *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre les exemples de code qui expliquent comment appeler ce processus, créez un processus nommé `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

Lorsque ce processus est invoqué, il effectue les actions suivantes :

1. Obtenir le document PDF non protégé qui est transmis au processus sous la forme dʼune valeur dʼentrée.
1. Chiffrement du document PDF avec un mot de passe. Le nom du paramètre d’entrée de ce processus est `inDoc` et le type de données est document.
1. Enregistrer le document PDF protégé par mot de passe sous forme de fichier PDF dans le système de fichiers local. Ce processus renvoie le document PDF chiffré sous la forme dʼune valeur de sortie. Le nom du paramètre de sortie de ce processus est `outDoc` et le type de données est document.

   Ce processus est réalisé de manière synchrone sur le même thread dʼexécution que celui à partir duquel il a été appelé. Le nom de ce processus de courte durée est `MyApplication/EncryptDocument` et son opération est `invoke`.

   >[!NOTE]
   >
   >En règle générale, un processus de courte durée comprend plus de trois actions. La création dʼun processus sʼeffectue à lʼaide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

   La section *Programmation avec AEM Forms* décrit les différentes méthodes dʼappel par programmation de ce processus de courte durée, à savoir :

   * [Appeler un processus de courte durée en transmettant un document non protégé à lʼaide dʼAEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (au moyen une application Flex)
   * [Appel d’un processus de courte durée à l’aide de l’API d’appel](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (API d’appel Java™)
   * [Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (exemple de service web)
   * [Appeler AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (exemple de service web)
   * [Appeler AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (exemple de service web)
   * [Appeler AEM Forms en utilisant des données BLOB via HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (exemple de service web)
   * [Appeler AEM Forms à l’aide de DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (exemple de service web)
   * [Appeler le processus MyApplication/EncryptDocument à l’aide de REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Exemple de processus de longue durée**

L’illustration suivante est un exemple de processus de longue durée.

Ce processus est appelé lorsqu’un demandeur envoie un formulaire de prêt. Le processus n’est pas terminé tant qu’un responsable des prêts n’a pas approuvé ou rejeté la demande de prêt. Le nom de ce processus de longue durée est *FirstAppSolution/PreLoanProcess* et son opération est `invoke_Async`. Ce processus doit être appelé de manière asynchrone. Pour plus d’informations sur l’appel par programmation de ce processus de longue durée, consultez la section [Appeler les processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Ce processus peut être créé en suivant le tutoriel indiqué dans la section [Créer votre première application AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
