---
title: Types de points d’entrée
description: Découvrez les différents types de points d’entrée. Différents types de points d’entrée, tels qu’E-mail, Dossier de contrôle, et bien d’autres, peuvent être ajoutés aux services.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 100%

---

# Types de points d’entrée {#types-of-endpoints}

Avant de pouvoir utiliser un service, vous devez configurer et activer un point d’entrée. Un point d’entrée spécifie comment un service doit être appelé.

>[!NOTE]
>
>Dans Workbench, les points d’entrée sont appelés points de départ.

Les types de points d’entrée suivants peuvent être ajoutés aux services. Tous les services ne prennent pas en charge tous les points d’entrée :

**E-mail :** permet à un utilisateur d’appeler un service en envoyant un e-mail, avec une ou plusieurs pièces jointes, à un compte de messagerie spécifié. Avant de configurer un point d’entrée de courrier électronique, vous devez configurer les comptes de messagerie requis. Voir Configuration des points d’entrée de courrier électronique.

**Watched Folder :** permet à un utilisateur d’appeler un service en plaçant un fichier dans un dossier balayé à intervalles réguliers. (voir Configuration des points d’entrée Watched Folder). 

**TaskManager :** permet à un utilisateur de Workspace d’appeler le service.

**Remoting :** permet à une application créée avec Flex dʼappeler le service qui utilise AEM Forms Remoting (obsolète pour AEM Forms). Un point d’entrée Remoting est automatiquement créé pour chaque service activé. Une destination Flex possède le même nom que le point d’entrée créé, et les clientes et clients Flex peuvent créer des objets à distance qui pointent vers cette destination pour appeler des opérations dans le service approprié.

**SOAP :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en mode SOAP. Un point d’entrée SOAP est automatiquement créé pour chaque service activé.

**Remarque** : *les documents Document Security peuvent être moins sécurisés si le point d’entrée SOAP est utilisé lorsque vous visualisez les documents dans Adobe Acrobat ou Adobe Reader. Pour plus d’informations sur la désactivation des points d’entrée SOAP dans vos documents LCRM, consultez la section [Désactivation des points d’entrée SOAP pour les documents Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*.

**EJB :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en mode Enterprise JavaBeans (EJB). Un point d’entrée EJB est automatiquement créé pour chaque service activé.

**WSDL :** permet à une application cliente développée à l’aide des API de programmation d’AEM Forms d’appeler le service en utilisant le langage WSDL (Web Service Definition Language). La page Configuration de base contient une option permettant d’activer la génération WSDL pour tous les services faisant partie d’AEM forms (voir Configuration des paramètres généraux d’AEM forms).

**REST :** les processus créés dans Workbench peuvent être configurés pour être invoqués via des demandes REST (Representational State Transfer). Les requêtes REST sont envoyées à partir de pages HTML. Ainsi, vous pouvez appeler un processus AEM Forms directement à partir d’une page Web en utilisant une requête REST.

L’e-mail, le TaskManager, le dossier de contrôle, et les points d’entrée Remoting n’exposent qu’une opération spécifique du service. L’ajout de ces points d’entrée nécessite une deuxième étape de configuration afin de sélectionner une méthode pour appeler le service, définir les paramètres de configuration, et spécifier les paramètres de mappage d’entrée/sortie.
