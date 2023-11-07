---
title: Conteneur de services
seo-title: Service container
description: Services AEM Forms dans le conteneur de services
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 93%

---

# Conteneur de services {#service-container}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Les services AEM Forms du conteneur de services (y compris les services standard tels que le service Encryption, les processus de longue durée et de courte durée) peuvent être appelés à l’aide de divers fournisseurs, tels qu’un fournisseur EJB. Un fournisseur EJB permet aux services AEM Forms d’être appelés via RMI/IIOP. Un fournisseur de services web expose les services en tant que services Web (génération WSDL) en utilisant des normes telles que SOAP/HTTP et SOAP/JMS.

Le tableau suivant décrit les différentes manières dont vous pouvez appeler les services AEM Forms par programmation.

<table>
 <thead>
  <tr>
   <th><p>Méthode d’appel</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Intégration à distance</p></td>
   <td><p>L’intégration à distance permet aux clients Flex d’appeler des opérations de service. (Voir <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM forms)</a>).</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Une API Java peut appeler un service AEM Forms. L’API Java est organisée en bibliothèques client et en API d’appel Java. (Voir <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Appel d’AEM Forms à l’aide de l’API Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>Services Web</p></td>
   <td><p>AEM Forms prend en charge les normes de service web telles que SOAP/HTTP. Un service peut être exposé comme un service Web, dont le WSDL est conforme aux normes de service web définies par le W3C.</p><p>Un service peut être appelé à partir de n’importe quelle pile de services web, notamment .NET Framework et le SDK Sun™ Web Services. (Voir <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Appel d’AEM Forms à l’aide de services web</a>).</p></td>
  </tr>
  <tr>
   <td><p>Requêtes REST</p></td>
   <td><p>AEM Forms prend en charge les requêtes REST. Un service peut être appelé directement à partir d’une page HTML. (Voir <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Appel d’AEM Forms à l’aide de requêtes REST</a>).</p></td>
  </tr>
 </tbody>
</table>

L’illustration suivante fournit une représentation visuelle des différentes manières dont les services AEM Forms peuvent être appelés par programmation.

>[!NOTE]
>
>En plus d’utiliser le SDK AEM Forms pour créer des applications clientes qui peuvent appeler les services AEM Forms, vous pouvez également créer des composants qui peuvent être déployés dans le conteneur de services. Par exemple, vous pouvez créer un composant Bank qui contient des types de données personnalisés pouvant être utilisés dans les processus. En d’autres termes, vous pouvez créer un type de données tel que `com.adobe.idp.BankAccount`. Vous pouvez ensuite créer des instances `com.adobe.idp.BankAccount` dans vos applications clientes.

Le conteneur de services offre les fonctionnalités suivantes :

* Permet d’appeler les services AEM Forms à l’aide de différentes méthodes. Vous pouvez configurer un service en définissant des points d’entrée afin qu’il puisse être appelé à l’aide de toutes les méthodes : Remoting, l’API Java, les services web et REST. (Voir [Gestion par programmation des points d’entrée](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)).
* Convertit un message en un format normalisé appelé demande d’appel. Une demande d’appel est envoyée d’une application cliente (ou d’un autre service) à un service dans le conteneur de services. Une demande d’appel contient des informations telles que le nom du service à appeler et les valeurs de données requises pour effectuer l’opération. De nombreux services nécessitent un document pour effectuer une opération. Par conséquent, une demande d’appel contient généralement un document, qui peut être des données PDF, des données XDP, des données XML, etc.
* Achemine les demandes d’appel vers les services appropriés (le nom du service à appeler fait partie de la demande d’appel).
* Effectue des tâches telles que déterminer si l’appelant a l’autorisation d’appeler l’opération de service spécifiée. La demande d’appel doit contenir un nom d’utilisateur et un mot de passe AEM Forms valides.

  Il existe différentes manières d’envoyer une demande d’appel à un service. Il existe également différentes manières d’envoyer les valeurs d’entrée requises au service. Par exemple, supposons que vous utilisiez l’API Java pour appeler un service qui nécessite un document PDF. La méthode Java correspondante contient un paramètre qui accepte un document PDF. Dans ce cas, le type de données du paramètre est `com.adobe.idp.Document`. (Voir [Transmettre des données aux services AEM Forms à l’aide de l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)).

  Si vous appelez un service en utilisant des dossiers de contrôle, une demande d’appel est envoyée lorsque vous placez un fichier dans un dossier de contrôle configuré. Si vous appelez un service en utilisant l’e-mail, une demande d’appel est envoyée à un service lorsqu’un e-mail arrive dans une boîte de réception configurée.

  Le conteneur de services renvoie une réponse d’appel une fois l’opération effectuée. Une réponse d’appel contient des informations telles que les résultats de l’opération. Par exemple, si l’opération modifie un document PDF, la réponse d’appel contient le document PDF modifié. Si l’opération a échoué, la réponse d’appel contient un message d’erreur.

  Une réponse d’appel peut être récupérée de la même manière qu’une demande d’appel est envoyée. En d’autres termes, si la demande d’appel est envoyée à l’aide de l’API Java, une réponse d’appel peut être récupérée à l’aide de l’API Java. Supposons, par exemple, qu’une opération modifie un document PDF. Vous pouvez récupérer le document PDF modifié en obtenant la valeur renvoyée de la méthode Java qui a appelé le service.

  Lorsqu’un processus de longue durée est appelé, une réponse d’appel contient une valeur d’identifiant associée à la demande d’appel. Cette valeur d’identifiant vous permet de vérifier ultérieurement l’état du processus. Prenons l’exemple du service de longue durée MortgageLoan. À l’aide de la valeur d’identifiant, vous pouvez vérifier si le processus s’est correctement terminé. (Voir [Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  Le diagramme suivant montre une application cliente (qui utilise l’API Java) appelant un service.

  Lorsqu’une application cliente appelle un service, trois événements se produisent :

   1. Une application cliente envoie une demande d’appel à un service.
   1. Le service effectue l’opération spécifiée dans la demande d’appel.
   1. Le conteneur de services renvoie une réponse d’appel à l’application cliente.

**Voir également**

[Présentation des processus AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Appeler AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Appel d’AEM Forms en utilisant l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Appel d’AEM Forms utilisant des services Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Appeler AEM Forms à l’aide de demandes REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
