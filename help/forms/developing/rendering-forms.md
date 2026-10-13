---
title: Rendu de Forms
description: Le service Forms permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans le concepteur. Les auteurs et autrices de formulaires peuvent développer une conception de formulaire unique que le service Forms restitue au format PDF, SWF ou HTML dans différents environnements de navigateur.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 100%
---
# Rendu de Forms {#rendering-forms}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Forms**

Le service Forms permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans le concepteur. Les auteurs et autrices de formulaires peuvent développer une conception de formulaire unique que le service Forms restitue au format PDF, SWF ou HTML dans différents environnements de navigateur.

Quand un utilisateur final demande un formulaire, une application client envoie la demande au service Forms, qui renvoie le formulaire dans un format approprié. Dès que le service Forms reçoit une demande, il fusionne les données avec une conception de formulaire, puis transmet le formulaire au format souhaité. La sortie du service Form est un formulaire interactif, généralement un document PDF. Un formulaire interactif permet aux utilisateurs de remplir les champs situés sur le formulaire.

Selon le type d’application client, vous pouvez afficher le formulaire dans un navigateur web client ou l’enregistrer en tant que fichier PDF. Une application web peut afficher le formulaire dans un navigateur web. Une application de bureau peut enregistrer le formulaire en tant que fichier PDF. Pour expliquer comment écrire dans un navigateur web et un fichier PDF, les mises en route se trouvant dans la section *Générer des formulaires* sont organisées de la manière suivante :

* Les exemples d’API Java fortement typées (mode SOAP) sont des servlets Java.
* Les exemples de service web (Java Base64) sont un servlet Java.
* Les exemples de service web (MTOM) sont une application de console (tous les démarrages rapides n’ont pas un exemple de MTOM).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application web qui utilise des servlets Java pour appeler le service Forms, voir [Créer des applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Vous pouvez transmettre une conception de formulaire (un fichier XDP) ou un document PDF au service Forms en utilisant l’une des deux méthodes suivantes :

* Vous pouvez référencer la conception de formulaire à l’aide d’une valeur URL. Cette approche implique l’utilisation d’un objet `URLSpec`. La racine de contenu est transmise au service Forms à l’aide de la méthode `setContentRootURI` de l’objet `URLSpec`. Le nom de la conception de formulaire (`formQuery`) est transmis en tant que paramètre distinct. Les deux valeurs sont concaténées afin d’obtenir la référence absolue à la conception de formulaire. (La plupart des mises en route se trouvant dans la section *Générer des formulaires* utilisent cette approche.)
* Vous pouvez transmettre un `com.adobe.idp.Document` qui contient la conception de formulaire au service Forms. Deux nouvelles méthodes nommées `renderPDFForm2` et `renderHTMLForm2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire. (Voir [Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

Vous pouvez accomplir ces tâches à l’aide du service Forms :

* Renvoyer des formulaires PDF interactifs. (Voir [Renvoyer des formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Renvoyer des formulaires au client. (Voir [Renvoyer des formulaires au client](/help/forms/developing/rendering-forms-client.md).)
* Renvoyer des formulaires basés sur des fragments. (Voir [Renvoyer des formulaires basés sur des fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* Renvoyer des formulaires compatibles avec les droits. (Voir [Renvoyer des formulaires compatibles avec les droits](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Renvoyer des formulaires au format HTML. (Voir [Renvoyer des formulaires au format HTML](/help/forms/developing/rendering-forms-html.md).)
* Renvoyer des formulaires HTML à l’aide de fichiers CSS personnalisés ([Renvoyer des formulaires HTML à l’aide de fichiers CSS personnalisés](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Gérer les formulaires envoyés. (Voir [Gérer les formulaires envoyés](/help/forms/developing/handling-submitted-forms.md).)
* Créer des documents PDF avec des données XML envoyées. (Voir [Créer des documents PDF avec des données XML envoyées](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Préremplir les formulaires. (Voir [Préremplir les formulaires avec des mises en pages souples](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Transmettre des documents. (Voir [Transmettre des documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calculer des données de formulaire. (Voir [Calculer les données de formulaire](/help/forms/developing/calculating-form-data.md).)
* Optimiser une application. (Voir [Optimiser les performances du service Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
