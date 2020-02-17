---
title: Types de points de fin
seo-title: Types de points de fin
description: Découvrez les différents types de points de fin.
seo-description: Découvrez les différents types de points de fin.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Types de points de fin {#types-of-endpoints}

Avant de pouvoir utiliser un service, vous devez configurer et activer un point de fin. Un point de fin spécifie la méthode d’appel d’un service.

>[!NOTE]
>
>dans Workbench, les points de fin sont appelés points de départ.

Les types de points de fin suivants peuvent être ajoutés à un service. Certains services ne prennent pas en charge la totalité des points de fin :

**** Courriel : Permet à un utilisateur d’appeler un service en envoyant un message électronique avec une ou plusieurs pièces jointes à un compte de messagerie spécifié. Avant de configurer un point de fin de courrier électronique, vous devez configurer les comptes de messagerie requis. Voir Configuration des points de fin de courrier électronique.

**** Watched Folder : Permet à un utilisateur d’appeler un service en plaçant un fichier dans un dossier, qui est analysé à intervalles définis. (voir Configuration des points de fin Watched Folder). 

**** TaskManager : Permet à un utilisateur de Workspace d’appeler le service.

**** Remoting : Permet à une application créée avec Flex d’appeler le service à l’aide d’AEM forms Remoting (obsolète pour AEM forms). Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex portant le même nom que le point de fin est créée, ce qui permet aux clients Flex de créer des objets distants pointant vers cette destination afin d’appeler des opérations sur le service adéquat.

**** SOAP : Permet à une application cliente développée à l’aide des API de programmation d’AEM forms d’appeler le service en mode SOAP. Un point de fin SOAP est automatiquement créé pour chaque service activé.

**remarque**: La *protection peut être supprimée des documents Document Security lorsque le point de fin SOAP est utilisé lors de l’affichage des documents dans Adobe Acrobat ou Adobe Reader. Pour plus d’informations sur la désactivation des points de fin SOAP dans vos documents LCRM, consultez la section[Désactivation des points de fin SOAP pour les documents Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*.

**** EJB : Permet à une application cliente développée à l’aide des API de programmation d’AEM forms d’appeler le service en mode Enterprise JavaBeans (EJB). Un point de fin EJB est automatiquement créé pour chaque service activé.

**** WSDL : Permet à une application cliente développée à l’aide des API de programmation d’AEM forms d’appeler le service à l’aide du langage WSDL (Web Service Definition Language). La page Configuration de base contient une option permettant d’activer la génération WSDL pour tous les services faisant partie d’AEM forms (voir Configuration des paramètres généraux d’AEM forms).

**** REST : Les processus créés dans Workbench peuvent être configurés afin que vous puissiez les appeler par le biais de demandes REST (Reading State Transfer). Ces demandes sont envoyées à partir de pages HTML. C’est pourquoi, vous pouvez appeler un processus AEM forms directement à partir d’une page Web à l’aide d’une requête REST.

Les points de fin de courrier électronique, TaskManager, Watched Folder et Remoting indiquent uniquement une opération particulière du service. L’ajout de ces points de fin nécessite une seconde étape de configuration pour sélectionner une méthode d’appel du service, la définition de paramètres de configuration et la spécification des mappages de paramètres d’entrée et de sortie.
