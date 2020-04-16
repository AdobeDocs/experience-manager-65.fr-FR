---
title: Rendu des formulaires
seo-title: Rendu des formulaires
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Rendu des formulaires {#rendering-forms}

**À propos du service Forms**

Le service Forms vous permet de créer des applications clientes de capture de données interactives qui valident, traitent, transforment et délivrent des formulaires généralement créés dans Designer. Les auteurs de formulaires peuvent développer une conception de formulaire unique que le service Forms rend au format PDF, SWF ou HTML dans divers  de navigateur.

Lorsqu’un utilisateur final demande un formulaire, une application cliente envoie la requête au service Forms, qui renvoie le formulaire dans un format approprié. Dès que le service Forms reçoit une requête, il fusionne les données avec une conception de formulaire, puis livre le formulaire au format souhaité. La sortie du service Form est un formulaire interactif, généralement un  PDF. Un formulaire interactif permet aux utilisateurs de remplir les champs situés sur le formulaire.

Selon le type d’application cliente, vous pouvez écrire le formulaire dans un navigateur Web client ou l’enregistrer dans un fichier PDF. Une application Web peut écrire le formulaire dans un navigateur Web. Une application de bureau peut enregistrer le formulaire au format PDF. Pour démontrer comment écrire dans un navigateur Web et dans un fichier PDF, les  rapides situés dans la section *Rendu des formulaires* sont organisés de la manière suivante :

* Les exemples d’API Java fortement tapées (mode SOAP) sont une servlet Java.
* Les exemples de service Web (Java Base64) sont une servlet Java.
* Les exemples de service Web (MTOM) sont une application de console (tous les rapides n’ont pas d’exemple MTOM).

>[!NOTE]
>
> Pour plus d’informations sur la création d’une application Web qui utilise des servlets java pour appeler le service Forms, voir [Création de   qui Génère des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md).

Vous pouvez transmettre une conception de formulaire (un fichier XDP) ou un PDF au service Forms à l’aide de l’une des deux méthodes suivantes :

* Vous pouvez référencer la conception de formulaire à l’aide d’une valeur d’URL. Cette approche implique l’utilisation d’un `URLSpec` objet. La racine de contenu est transmise au service Forms à l’aide de la `URLSpec` `setContentRootURI` méthode de l’objet. Le nom de la conception de formulaire ( `formQuery`) est transmis en tant que paramètre distinct. Les deux valeurs sont concaténées pour obtenir la référence absolue à la conception de formulaire. (La plupart des  rapides de la section *Rendu des formulaires* utilisent cette approche.)
* Vous pouvez transmettre au service Forms un `com.adobe.idp.Document` qui contient la conception de formulaire. Deux nouvelles méthodes portent le nom `renderPDFForm2` et `renderHTMLForm2` acceptent un `com.adobe.idp.Document` objet contenant une conception de formulaire. (Voir [Transmission de  au service Forms](/help/forms/developing/passing-documents-forms-service.md)

Vous pouvez accomplir ces  de à l’aide du service Forms :

* Générer des formulaires PDF interactifs. (Voir [Rendu de formulaires](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interactifs.)
* Générer des formulaires au niveau du client. (voir [Rendu de formulaires sur le client](/help/forms/developing/rendering-forms-client.md)).
* Rendu des formulaires reposant sur des fragments. (See [Rendering Forms Based on Fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* Générer des formulaires dont les droits sont activés. (Voir [Rendu de formulaires](/help/forms/developing/rendering-rights-enabled-forms.md)prenant en charge les droits.)
* Rendu des formulaires au format HTML. (voir [Rendu de formulaires au format HTML](/help/forms/developing/rendering-forms-html.md)).
* Rendu de formulaires HTML à l’aide de fichiers CSS personnalisés ([Rendu de formulaires HTML à l’aide de fichiers](/help/forms/developing/rendering-html-forms-using-custom.md)CSS personnalisés)
* Gérez les formulaires envoyés. (Voir [Gestion des formulaires](/help/forms/developing/handling-submitted-forms.md)envoyés.)
* Création de  PDF avec des données XML envoyées. (voir [Création d’ PDF avec des données](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML envoyées).
* Préremplissage des formulaires. (Voir [Préremplissage de formulaires avec des mises en page](/help/forms/developing/prepopulating-forms-flowable-layouts.md)à disposition souple.)
*  de passage. (Voir [Transmission de  au service Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calculez les données du formulaire. (Voir [Calcul des données](/help/forms/developing/calculating-form-data.md)de formulaire.)
* Optimisez une application. (voir [Optimisation des performances du service](/help/forms/developing/optimizing-performance-forms-service.md)Forms).

   ***Conseil **: Le site Web Adobe Developer contient l’article suivant qui explique comment créer une application ASP.NET qui appelle le service Forms et génère des formulaires. Voir[Création d&#39;applications](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)ASP.NET de rendu de formulaire.*

