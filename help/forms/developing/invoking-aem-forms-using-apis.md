---
title: Appel d’AEM Forms à l’aide d’API
seo-title: Appel d’AEM Forms à l’aide d’API
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Appel d’AEM Forms à l’aide d’API {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms est un logiciel d’entreprise basé sur J2EE qui comprend des services qui fonctionnent dans une infrastructure partagée. Les opérations de service consomment ou produisent généralement des documents. Avec AEM Forms, vous pouvez combiner le processus des formulaires avec des formulaires électroniques, la sécurité des documents et la génération de documents dans un ensemble de services intégré et cohérent. Ces services sont accessibles à l’intérieur et à l’extérieur du pare-feu.

Les applications clientes peuvent appeler par programmation les services AEM Forms à l’aide d’une API Java, de services Web, de Remoting et de REST. A l’aide d’Administration Console, vous pouvez configurer un service pour exposer un point de fin qui permet aux services AEM Forms d’être appelés par programmation. Par défaut, la plupart des services sont préconfigurés pour exposer les points de fin Remoting, Java et de service Web.

Les exigences de votre entreprise déterminent la méthode d’appel à utiliser. Par exemple, à l’aide de l’API Java, vous pouvez intégrer la fonctionnalité AEM Forms à vos applications d’entreprise Java, telles que l’entité Java et les beans de message. De même, vous pouvez intégrer la fonctionnalité AEM Forms dans des projets .NET (ou d’autres projets développés avec des environnements de développement qui prennent en charge les normes de service Web) à l’aide de services Web.

Les services nécessitent l’exécution d’un conteneur de services, de la même manière que les fichiers EJB (Enterprise JavaBeans™) nécessitent un conteneur J2EE. AEM Forms ne comprend qu’une seule implémentation d’un conteneur de services. Le conteneur de services est chargé de gérer la durée de vie d’un service, notamment de le déployer et de s’assurer que toutes les demandes sont envoyées au service approprié. Il gère également les documents qu’un service consomme ou produit.

>[!NOTE]
>
>La programmation avec AEM forms n’inclut pas d’informations sur la manière d’appeler AEM Forms à l’aide de dossiers de contrôle ou de courriers électroniques.

