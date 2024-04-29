---
title: Comment appeler AEM Forms à l’aide d’API ?
description: Découvrez comment appeler les services AEM Forms en utilisant une API Java™, les services web, Remoting et REST.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '295'
ht-degree: 100%

---

# Appel d’AEM Forms à l’aide d’API {#invoking-aem-forms-using-apis}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Adobe Experience Manager Forms est un logiciel d’entreprise basé sur J2EE qui se compose de services fonctionnant dans une infrastructure partagée. Les opérations de service consomment ou produisent généralement des documents. En utilisant AEM Forms, vous pouvez combiner Forms Workflow avec les formulaires électroniques, la sécurité des documents et la génération de documents dans un ensemble intégré et cohérent de services. Ces services sont accessibles depuis l’intérieur et l’extérieur du pare-feu.

Les applications clientes peuvent appeler des services AEM Forms par programmation en utilisant une API Java™, des services web, Remoting et REST. À l’aide de la console d’administration, vous pouvez configurer un service pour exposer un point d’entrée qui permet aux services AEM Forms d’être appelés par programmation. Par défaut, la plupart des services sont préconfigurés pour exposer des points d’entrée de service Remoting, Java™ et web.

Les exigences de votre entreprise déterminent la méthode d’appel à utiliser. Par exemple, à l’aide de l’API Java™, vous pouvez intégrer la fonctionnalité AEM Forms à vos applications d’entreprise Java™, telles que Java™ Entity et Message Beans. De même, vous pouvez intégrer la fonctionnalité AEM Forms dans des projets .NET (ou d’autres projets développés avec des environnements de développement qui prennent en charge les normes de services web) à l’aide de services web.

Les services nécessitent un conteneur de services pour s’exécuter, de la même manière que Enterprise JavaBeans™ (EJB) nécessite un conteneur J2EE. AEM Forms ne comprend qu’une seule implémentation d’un conteneur de services. Le conteneur de service est chargé de la gestion de la durée de vie d’un service, y compris son déploiement et l’assurance que toutes les demandes sont envoyées au service approprié. Il gère également les documents qu’un service consomme ou produit.

>[!NOTE]
>
>La programmation avec AEM Forms ne comprend pas d’informations sur la manière d’appeler AEM Forms en utilisant des dossiers de contrôle ou des e-mails.
