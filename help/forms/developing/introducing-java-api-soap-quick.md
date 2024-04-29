---
title: Présentation du démarrage rapide de lʼAPI Java™
description: Découvrez comment les opérations AEM Forms peuvent être effectuées à l’aide de l’API Java™ fortement typée d’AEM Forms activée et avec une connexion définie sur SOAP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '532'
ht-degree: 100%

---

# Présentation du démarrage rapide de lʼAPI Java™ {#introducing-java-api-quickstart}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le démarrage rapide de l’API Adobe AEM Forms peut vous aider à accélérer vos efforts de développement de programmes qui interagissent avec les services AEM Forms. Les *démarrages rapides* sont des programmes complets que vous pouvez copier et coller dans vos propres projets et qui vous servent de point de départ. Vous pouvez exécuter un démarrage rapide pour ce quʼil accomplit et le modifier en fonction de vos besoins.

Les opérations AEM Forms peuvent être effectuées à l’aide de l’API fortement typée dʼAEM Forms et le mode de connexion doit être défini sur SOAP.

Le démarrage rapide de lʼAPI Java™ fortement typée fournit une liste des fichiers JAR requis pour exécuter l’application Java™. La plupart des démarrages rapides Java™ sont des applications de console qui s’exécutent dans `main`. Toutefois, le démarrage rapide de l’API fortement typée Forms Java™ est implémenté en tant que servlet Java™ qui s’exécute dans une application web.

La liste des fichiers JAR se trouve dans une section de commentaires située au début du démarrage rapide. Par exemple, le commentaire suivant se trouve dans un démarrage rapide du service Output et reprend une liste de fichiers JAR standard que lʼon trouve dans chaque démarrage rapide Java™.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Démarrage rapide de plusieurs services {#multiple-services-quick-start}

La plupart des démarrages rapides situés dans *Programmation avec AEM Forms sur JEE* appellent un service spécifique pour effectuer une opération. Cependant, certains démarrages rapides appellent plusieurs services AEM Forms pour effectuer un workflow donné. La liste suivante fournit des démarrages rapides Java™ qui appellent plusieurs services AEM Forms :

[Démarrage rapide (mode SOAP) : transmettre un document situé dans le référentiel AEM Forms au service Output à l’aide de l’API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (appelle les services Repository et Output).

[Démarrage rapide (mode SOAP) : créer un document PDF basé sur des fragments à l’aide de l’API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (appelle les services Assembler et Output).

[Démarrage rapide (mode SOAP) : créer des documents PDF avec des données XML envoyées à l’aide de l’API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (appelle les services Forms, Output et Document Management).

[Démarrage rapide (mode SOAP) : transmettre des documents au service Forms à l’aide de l’API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (appelle les services Forms et Document Management).

[Démarrage rapide (mode SOAP) : signer numériquement un formulaire XFA à l’aide de l’API Java™](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (appelle les services Forms et Signature).

[Démarrage rapide (mode SOAP) : gérer les rôles et les autorisations à l’aide de l’API Java™](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (appelle les services DirectoryManager et AuthorizationManager).

[Démarrage rapide (mode SOAP) : transmettre des documents au service Output à l’aide de l’API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (appelle les services Output et Document Management).

>[!NOTE]
>
>Les démarrages rapides situés dans Programmation avec AEM Forms sont basés sur le déploiement d’AEM Forms sur le serveur d’applications JBoss® et le système d’exploitation Microsoft® Windows®. Cependant, si vous utilisez un autre système d’exploitation, comme UNIX®, remplacez les chemins spécifiques à Windows par ceux pris en charge par le système d’exploitation approprié. De même, si vous utilisez un autre serveur d’applications J2EE, veillez à spécifier des propriétés de connexion valides. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La plupart des démarrages rapides des services Web sont écrits en C# et utilisent le framework .NET. Cependant, vous pouvez créer une logique d’application cliente capable d’appeler les services AEM Forms dans n’importe quel environnement de développement prenant en charge les normes SOAP. (Consultez la section [Appeler AEM Forms à lʼaide de services web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)).
