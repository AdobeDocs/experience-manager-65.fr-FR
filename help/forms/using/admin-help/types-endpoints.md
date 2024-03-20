---
title: Types de points d’entrée
description: Découvrez les différents types de points de fin. Différents types de points de fin, tels que Email, Dossier de contrôle et bien d’autres, peuvent être ajoutés aux services.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 60%

---

# Types de points d’entrée {#types-of-endpoints}

Avant de pouvoir utiliser un service, vous devez configurer et activer un point de fin. Un point de terminaison spécifie comment un service doit être appelé.

>[!NOTE]
>
>Dans Workbench, les points de fin sont appelés points de départ.

Les types de points de fin suivants peuvent être ajoutés aux services. Tous les services ne prennent pas en charge tous les points de terminaison :

**E-mail :** permet à un utilisateur d’appeler un service en envoyant un e-mail, avec une ou plusieurs pièces jointes, à un compte de messagerie spécifié. Avant de configurer un point d’entrée de courrier électronique, vous devez configurer les comptes de messagerie requis. Voir Configuration des points d’entrée de courrier électronique.

**Watched Folder :** permet à un utilisateur d’appeler un service en plaçant un fichier dans un dossier balayé à intervalles réguliers. (voir Configuration des points d’entrée Watched Folder). 

**TaskManager :** permet à un utilisateur de Workspace d’appeler le service.

**Remoting :** permet à une application créée avec Flex dʼappeler le service qui utilise AEM Forms Remoting (obsolète pour AEM Forms). Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex qui porte le même nom que le point de terminaison est créée et les clients Flex peuvent créer des objets distants qui pointent vers cette destination pour appeler des opérations sur le service approprié.

**SOAP :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en mode SOAP. Un point d’entrée SOAP est automatiquement créé pour chaque service activé.

**Remarque** : *les documents Document Security peuvent être moins sécurisés si le point d’entrée SOAP est utilisé lorsque vous visualisez les documents dans Adobe Acrobat ou Adobe Reader. Pour plus d’informations sur la désactivation des points d’entrée SOAP dans vos documents LCRM, consultez la section [Désactivation des points d’entrée SOAP pour les documents Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*.

**EJB :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en mode Enterprise JavaBeans (EJB). Un point d’entrée EJB est automatiquement créé pour chaque service activé.

**WSDL :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en utilisant le langage WSDL (Web Service Definition Language). La page Configuration de base contient une option permettant d’activer la génération WSDL pour tous les services faisant partie d’AEM forms (voir Configuration des paramètres généraux d’AEM forms).

**REST :** les processus créés dans Workbench peuvent être configurés pour être invoqués via des demandes REST (Representational State Transfer). Les demandes REST sont envoyées à partir de pages de HTML. En d’autres termes, vous pouvez appeler un processus de formulaires AEM directement à partir d’une page web à l’aide d’une requête REST.

Les points de fin Email, TaskManager, Watched Folder et Remoting affichent uniquement une opération spécifique du service. L’ajout de ces points de fin nécessite une deuxième étape de configuration pour sélectionner une méthode d’appel du service, la définition des paramètres de configuration et la spécification des mappages des paramètres d’entrée et de sortie.
