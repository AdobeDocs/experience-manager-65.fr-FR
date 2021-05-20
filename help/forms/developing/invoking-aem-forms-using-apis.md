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
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Appel d’AEM Forms à l’aide d’API {#invoking-aem-forms-using-apis}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Adobe Experience Manager Forms est un logiciel d’entreprise basé sur J2EE qui se compose de services opérant au sein d’une infrastructure partagée. Les opérations de service utilisent ou produisent généralement des documents. Avec AEM Forms, vous pouvez combiner le processus des formulaires à des formulaires électroniques, à Document Security et à la génération de documents dans un ensemble de services intégré et cohérent. Ces services sont accessibles à l’intérieur et à l’extérieur du pare-feu.

Les applications clientes peuvent appeler par programmation les services AEM Forms à l’aide d’une API Java, de services web, d’Remoting et de REST. À l’aide d’Administration Console, vous pouvez configurer un service afin d’exposer un point de terminaison qui permet aux services AEM Forms d’être appelés par programmation. Par défaut, la plupart des services sont préconfigurés pour exposer les points d’entrée Remoting, Java et Web service.

Les exigences de votre entreprise déterminent la méthode d’appel à utiliser. Par exemple, à l’aide de l’API Java, vous pouvez intégrer la fonctionnalité AEM Forms à vos applications d’entreprise Java, telles que Java Entity et Message Beans. De même, vous pouvez intégrer des fonctionnalités AEM Forms dans des projets .NET (ou d’autres projets développés avec des environnements de développement qui prennent en charge les normes de service Web) à l’aide de services Web.

Les services requièrent l’exécution d’un conteneur de services, comme pour les Enterprise JavaBeans™ (EJB), qui nécessitent un conteneur J2EE. AEM Forms ne comprend qu’une seule implémentation d’un conteneur de services. Le conteneur de services est chargé de gérer la durée de vie d’un service, notamment de le déployer et de s’assurer que toutes les demandes sont envoyées au service approprié. Il gère également les documents qu’un service consomme ou produit.

>[!NOTE]
>
>La programmation avec AEM forms n’inclut pas d’informations sur l’appel d’AEM Forms à l’aide de dossiers de contrôle ou d’e-mail.
