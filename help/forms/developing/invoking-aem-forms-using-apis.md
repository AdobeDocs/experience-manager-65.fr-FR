---
title: Appel d’AEM Forms à l’aide d’API
seo-title: Appel d’AEM Forms à l’aide d’API
description: Appel d’AEM Forms à l’aide d’API
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Appel d’AEM Forms à l’aide d’API {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms est un logiciel d’entreprise basé sur J2EE qui comprend des services qui fonctionnent au sein d’une infrastructure partagée. Les opérations de service consomment ou produisent généralement des documents. Grâce à AEM Forms, vous pouvez combiner le processus des formulaires à des formulaires électroniques, la sécurité des documents et la génération de documents dans un ensemble de services intégré et cohérent. Ces services sont accessibles à l’intérieur et à l’extérieur du pare-feu.

Les applications clientes peuvent appeler par programmation les services AEM Forms à l’aide d’une API Java, de services Web, de Remoting et de REST. A l’aide d’Administration Console, vous pouvez configurer un service pour exposer un point de terminaison qui permet aux services AEM Forms d’être appelés par programmation. Par défaut, la plupart des services sont préconfigurés pour exposer les points de terminaison des services Web, Java et Remoting.

Les exigences de votre entreprise déterminent la méthode d’appel à utiliser. Par exemple, à l’aide de l’API Java, vous pouvez intégrer des fonctionnalités AEM Forms à vos applications d’entreprise Java, telles que les beans d’entité Java et de message. De même, vous pouvez intégrer la fonctionnalité AEM Forms dans des projets .NET (ou d&#39;autres projets développés avec des environnements de développement qui prennent en charge les normes de service Web) à l&#39;aide de services Web.

Les services nécessitent l’exécution d’un conteneur de service, de la même manière que les EJB (Enterprise JavaBeans™) nécessitent un conteneur J2EE. AEM Forms ne comprend qu’une seule mise en oeuvre d’un conteneur de service. Le conteneur de service est chargé de gérer la durée de vie d’un service, notamment de le déployer et de s’assurer que toutes les demandes sont envoyées au service approprié. Il gère également les documents qu’un service consomme ou produit.

>[!NOTE]
>
>La programmation avec les formulaires AEM n’inclut pas d’informations sur la manière d’appeler AEM Forms à l’aide de dossiers de contrôle ou de courriers électroniques.

