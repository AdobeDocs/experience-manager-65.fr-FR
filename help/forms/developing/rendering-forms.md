---
title: Rendu Forms
seo-title: Rendu Forms
description: Utilisez le service Forms pour créer des applications clientes de capture de données interactives qui valident, traitent, transforment et délivrent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms rend au format PDF, SWF ou HTML dans divers environnements de navigateur.
seo-description: Utilisez le service Forms pour créer des applications clientes de capture de données interactives qui valident, traitent, transforment et délivrent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms rend au format PDF, SWF ou HTML dans divers environnements de navigateur.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Rendu de Forms {#rendering-forms}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

**À propos du service Forms**

Le service Forms vous permet de créer des applications clientes de capture de données interactives qui valident, traitent, transforment et délivrent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms rend au format PDF, SWF ou HTML dans divers environnements de navigateur.

Lorsqu’un utilisateur final demande un formulaire, une application cliente envoie la demande au service Forms, qui renvoie le formulaire dans un format approprié. Dès que le service Forms reçoit une demande, il fusionne les données avec une conception de formulaire, puis livre le formulaire au format souhaité. La sortie du service Form est un formulaire interactif, généralement un document PDF. Un formulaire interactif permet aux utilisateurs de remplir les champs situés sur le formulaire.

Selon le type d’application cliente, vous pouvez écrire le formulaire dans un navigateur Web client ou l’enregistrer dans un fichier PDF. Une application Web peut écrire le formulaire dans un navigateur Web. Une application de bureau peut enregistrer le formulaire au format PDF. Pour démontrer comment écrire dans un navigateur Web et dans un fichier PDF, les débuts rapides situés dans la section *Rendu Forms* sont organisés de la manière suivante :

* Les exemples d’API Java fortement typés (mode SOAP) sont une servlet Java.
* Les exemples de service Web (Java Base64) sont une servlet Java.
* Les exemples de service Web (MTOM) sont une application de console (tous les débuts rapides n’ont pas d’exemple MTOM).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application Web qui utilise des servlets java pour appeler le service Forms, voir [Création d’Applications web renvoyées par Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Vous pouvez transmettre une conception de formulaire (un fichier XDP) ou un document PDF au service Forms en utilisant l’une des deux méthodes suivantes :

* Vous pouvez référencer la conception de formulaire à l’aide d’une valeur d’URL. Cette approche implique l&#39;utilisation d&#39;un objet `URLSpec`. La racine de contenu est transmise au service Forms à l’aide de la méthode `URLSpec` de l’objet `setContentRootURI`. Le nom de la conception de formulaire ( `formQuery`) est transmis en tant que paramètre distinct. Les deux valeurs sont concaténées pour obtenir la référence absolue à la conception de formulaire. (La plupart des débuts rapides situés dans la section *Rendu Forms* utilisent cette approche.)
* Vous pouvez transmettre au service Forms un `com.adobe.idp.Document` contenant la conception de formulaire. Deux nouvelles méthodes nommées `renderPDFForm2` et `renderHTMLForm2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire. (Voir [Transmission de Documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

Vous pouvez accomplir ces tâches à l’aide du service Forms :

* Générer des PDF forms interactifs. (Voir [Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Générer des formulaires au niveau du client. (Voir [Rendu de Forms sur le client](/help/forms/developing/rendering-forms-client.md).)
* Rendu des formulaires reposant sur des fragments. (Voir [Rendu de Forms basé sur des fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* Générer des formulaires activés pour les droits. (Voir [Rendu de Forms prenant en charge les droits](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Générer des formulaires au format HTML. (Voir [Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md).)
* Rendu de HTML Forms à l’aide de fichiers CSS personnalisés ([Rendu de HTML Forms à l’aide de fichiers CSS personnalisés](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Gérez les formulaires envoyés. (Voir [Gestion du Forms envoyé](/help/forms/developing/handling-submitted-forms.md).)
* Création de Documents PDF avec des données XML envoyées. (Voir [Création de Documents PDF avec des données XML envoyées](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Préremplissage des formulaires. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Documents passés. (Voir [Transmission de Documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calculer les données de formulaire. (Voir [Calcul des données de formulaire](/help/forms/developing/calculating-form-data.md).)
* Optimiser une application. (Voir [Optimisation des performances du service Forms](/help/forms/developing/optimizing-performance-forms-service.md).)

   ***Conseil **: Le site Web Adobe Developer contient l&#39;article suivant qui explique comment créer une application ASP.NET qui appelle le service Forms et effectue le rendu des formulaires. Voir [Création d&#39;applications ASP.NET de rendu de formulaire](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*

