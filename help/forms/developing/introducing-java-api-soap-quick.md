---
title: Présentation de l’API Java QuickStart
seo-title: Présentation de l’API Java QuickStart
description: Présentation de l’API Java QuickStart
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Présentation du Début rapide API Java {#introducing-java-api-quickstart}

Le Début rapide de l’API AEM Forms Adobe peut vous aider à accélérer vos efforts pour développer des programmes qui interagissent avec les services AEM Forms. *Les* Débuts rapides sont des programmes complets que vous pouvez copier et coller dans vos propres projets et utiliser comme point de départ. Vous pouvez exécuter un Début rapide pour voir comment il se comporte et le modifier en fonction de vos besoins.

Les opérations AEM Forms peuvent être effectuées à l’aide de l’API AEM Forms fortement typée et le mode de connexion doit être défini sur SOAP.

Le Début rapide API Java fortement typé fournit une liste des fichiers JAR nécessaires à l’exécution de l’application Java. La plupart des Débuts Java Quick sont des applications de console qui s’exécutent dans `main`. Cependant, le Début rapide API Java Forms fortement typé est mis en oeuvre en tant que servlet Java s’exécutant dans une application Web.

La liste des fichiers JAR se trouve dans une section de commentaires située au début du Début rapide. Par exemple, le commentaire suivant se trouve dans un début rapide de sortie et est une liste de fichiers JAR standard que l’on trouve dans chaque Début rapide Java.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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

## Début rapide de plusieurs services {#multiple-services-quick-start}

La plupart des Débuts rapides situés dans *Programmation avec AEM Forms on JEE* appellent un service spécifique pour effectuer une opération. Cependant, certains Débuts rapides appellent plusieurs services AEM Forms pour exécuter un flux de travail donné. La liste suivante fournit des débuts rapides Java qui appellent plusieurs services AEM Forms :

[Début rapide (mode SOAP) : Transmission d’un document situé dans le référentiel AEM Forms au service Output à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) Java (appelle le service Repository et Output)

[Début rapide (mode SOAP) : Création d’un document PDF basé sur des fragments à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) Java (invoque le service Assembler et Output)

[Début rapide (mode SOAP) : Création de Documents PDF avec des données XML envoyées à l’aide de l’API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) Java (invoque le service Forms, Output et Document Management)

[Début rapide (mode SOAP) : Transmission de documents au service Forms à l’aide de l’API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) Java (appelle le service Forms et Document Management)

[Début rapide (mode SOAP) : Signature numérique d’un formulaire XFA à l’aide de l’API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) Java (appelle le service Forms and Signature)

[Début rapide (mode SOAP) : Gestion des rôles et des autorisations à l’aide de l’API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) Java (invoque DirectoryManager et le service AuthorizationManager )

[Début rapide (mode SOAP) : Transmission de documents au service Output à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) Java (appel du service Output and Document Management)

>[!NOTE]
>
>Les Débuts rapides situés dans Programmation avec AEM Forms reposent sur le déploiement de AEM Forms sur JBoss® Application Server et sur le système d’exploitation Microsoft® Windows®. Cependant, si vous utilisez un autre système d’exploitation, tel qu’UNIX®, remplacez les chemins spécifiques à Windows par les chemins pris en charge par le système d’exploitation concerné. De même, si vous utilisez un autre serveur d’applications J2EE, veillez à spécifier des propriétés de connexion valides. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La plupart des Débuts Quick Service sont écrits en C# et utilisent la structure .NET. Cependant, vous pouvez créer une logique d’application cliente capable d’appeler les services AEM Forms dans tout environnement de développement prenant en charge les normes SOAP. (See [Invoking AEM Forms Using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

