---
title: Rendu de Forms
seo-title: Rendu de Forms
description: Utilisez le service Forms pour créer des applications clientes interactives de capture de données qui valident, traitent, transforment et diffusent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms effectue au format PDF, SWF ou HTML dans différents environnements de navigateur.
seo-description: Utilisez le service Forms pour créer des applications clientes interactives de capture de données qui valident, traitent, transforment et diffusent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms effectue au format PDF, SWF ou HTML dans différents environnements de navigateur.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Rendu du Forms {#rendering-forms}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service Forms**

Le service Forms permet de créer des applications clientes interactives de capture de données qui valident, traitent, transforment et diffusent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms effectue au format PDF, SWF ou HTML dans différents environnements de navigateur.

Lorsqu’un utilisateur final demande un formulaire, une application client envoie la demande au service Forms, qui renvoie le formulaire dans un format approprié. Dès que le service Forms reçoit une demande, il fusionne les données avec une conception de formulaire, puis transmet le formulaire au format souhaité. La sortie du service Form est un formulaire interactif, généralement un document PDF. Un formulaire interactif permet aux utilisateurs de remplir les champs situés sur le formulaire.

Selon le type d’application cliente, vous pouvez écrire le formulaire dans un navigateur Web client ou l’enregistrer en tant que fichier PDF. Une application web peut écrire le formulaire dans un navigateur web. Une application de bureau peut enregistrer le formulaire au format PDF. Pour expliquer comment écrire dans un navigateur web et un fichier PDF, les démarrages rapides situés dans la section *Rendering Forms* sont organisés comme suit :

* Les exemples d’API Java fortement typées (mode SOAP) sont un servlet Java.
* Les exemples de service Web (Java Base64) sont un servlet Java.
* Les exemples de service Web (MTOM) sont une application de console (tous les démarrages rapides n’ont pas un exemple de MTOM).

>[!NOTE]
>
>Pour plus d’informations sur la création d’une application web qui utilise des servlets Java pour appeler le service Forms, voir [Création d’applications web qui renvoient Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Vous pouvez transmettre une conception de formulaire (un fichier XDP) ou un document PDF au service Forms en utilisant l’une des deux méthodes suivantes :

* Vous pouvez référencer la conception de formulaire à l’aide d’une valeur URL. Cette approche implique l’utilisation d’un objet `URLSpec`. La racine du contenu est transmise au service Forms à l’aide de la méthode `setContentRootURI` de l’objet `URLSpec`. Le nom de la conception de formulaire ( `formQuery`) est transmis en tant que paramètre distinct. Les deux valeurs sont concaténées afin d’obtenir la référence absolue à la conception de formulaire. (La plupart des démarrages rapides situés dans la section *Rendering Forms* utilisent cette approche.)
* Vous pouvez transmettre au service Forms une balise `com.adobe.idp.Document` contenant la conception de formulaire. Deux nouvelles méthodes nommées `renderPDFForm2` et `renderHTMLForm2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire. (Voir [Transmission de documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)

Vous pouvez accomplir ces tâches à l’aide du service Forms :

* Rendu des PDF forms interactifs. (Voir [Rendu des PDF forms interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Rendu des formulaires au niveau du client. (Voir [Rendu de Forms sur le client](/help/forms/developing/rendering-forms-client.md).)
* Rendu des formulaires reposant sur des fragments. (Voir [Rendu de Forms basé sur des fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* Rendu des formulaires dont les droits sont activés. (Voir [Rendu de Forms prenant en charge les droits](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Rendu des formulaires au format HTML. (Voir [Rendu de Forms au format HTML](/help/forms/developing/rendering-forms-html.md).)
* Rendu de Forms HTML à l’aide de fichiers CSS personnalisés ([Rendu de Forms HTML à l’aide de fichiers CSS personnalisés](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Gérer les formulaires envoyés. (Voir [Gestion des Forms envoyées](/help/forms/developing/handling-submitted-forms.md).)
* Création de documents PDF avec des données XML envoyées. (Voir [Création de documents PDF avec des données XML envoyées](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Préremplir les formulaires. (Voir [Préremplissage de Forms avec des dispositions souple](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Transmission de documents. (Voir [Transmission de documents au service Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcul des données de formulaire. (Voir [Calcul des données de formulaire](/help/forms/developing/calculating-form-data.md).)
* Optimisez une application. (Voir [Optimisation des performances du service Forms](/help/forms/developing/optimizing-performance-forms-service.md).)

   ***Conseil **: Le site web Adobe Developer contient l’article suivant qui explique comment créer une application ASP.NET qui appelle le service Forms et effectue le rendu des formulaires. Voir [Création d’applications de rendu de formulaire ASP.NET](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*
