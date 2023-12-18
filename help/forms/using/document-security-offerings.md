---
title: Offres Document Security
description: Découvrez les différents outils et fonctionnalités d’AEM Document Security.
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: ht
source-wordcount: '1216'
ht-degree: 100%

---

# Offres Document Security{#document-security-offerings}

La sécurité des documents Adobe Experience Manager Forms garantit que seuls les utilisateurs et utilisatrices autorisés peuvent utiliser vos documents. Document Security vous permet de distribuer en toute sécurité toute information enregistrée sous un format pris en charge. Les formats de fichiers pris en charge sont Adobe Portable Document Format (PDF) et Microsoft® Word, Excel et PowerPoint.

Vous pouvez protéger les documents à l’aide de politiques. Les paramètres de confidentialité que vous spécifiez dans une politique déterminent la mesure dans laquelle un destinataire ou une destinatrice peut utiliser un document auquel vous appliquez cette politique. Par exemple, vous pouvez spécifier si les destinataires et destinatrices sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés.

Les stratégies sont stockées sur le serveur Document Security. Vous appliquez les politiques aux documents par le biais de votre application cliente. Lorsque vous appliquez une politique à un document, les paramètres de confidentialité spécifiés dans la politique protègent les informations que le document contient. Vous pouvez distribuer le document protégé par une politique aux destinataires et destinatrices autorisés par la politique.

Le diagramme suivant illustre l’architecture standard pour AEM Forms Document Security :

![Document Security : architecture recommandée](do-not-localize/document_security_architecture.png)

## Clients Document Security {#document-security-clients}

Document Security fournit divers clients pour protéger les documents, afficher et modifier les documents protégés et les indexeurs afin d’activer la recherche de texte intégral sur les documents protégés. Vous pouvez choisir un client en fonction de vos besoins et des capacités de ce client.

Le serveur Document Security est le composant central par l’intermédiaire duquel Document Security effectue des transactions telles que l’authentification des utilisateurs, la gestion en temps réel des politiques et l’application de la confidentialité. Le serveur joue également le rôle de référentiel central pour les politiques, les enregistrements d’audit et d’autres informations associées.

Le serveur Document Security fournit une interface web (page web) pour créer des politiques, gérer des documents protégés par une politique et surveiller les événements associés aux documents protégés par une politque. Les administrateurs et administratrices peuvent également configurer des options globales, telles que l’authentification des utilisateurs et utilisatrices, la vérification et l’envoi de messages aux utilisateurs et utilisatrices invités et la gestion des comptes des utilisateurs et utilisatrices invités.

Le serveur est inclus dans l’offre de module complémentaire Document Security d’AEM Forms. Vous pouvez contacter l’[équipe commerciale](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG?lang=fr) d’AEM Forms pour acheter le module complémentaire Document Security.

### Protéger les documents {#protect-documents}

Document Security d’AEM Forms fournit divers outils pour appliquer des politiques de sécurité. Vous pouvez choisir un outil en fonction de vos besoins et de vos spécifications.

![document-security-offerings](assets/document-security-offerings.png)

Vous pouvez utiliser SDK Document Security, Adobe Acrobat, Document Security Extension for Microsoft® Office ou la bibliothèque portable de protection pour appliquer et suivre les politiques de sécurité :

* **SDK Document Security :** le SDK est un client riche en fonctionnalités. Vous pouvez utiliser SDK Document Security pour accéder aux fonctionnalités du serveur de documents, ouvrir des documents protégés par une politique et développer des extensions personnalisées, des modules complémentaires ou des applications. Par exemple, vous pouvez développer des extensions pour protéger les formats de fichiers personnalisés ou intégrer le SDK avec les solutions de prévention de perte de données (DLP). Les extensions, applications et modules complémentaires sont développés à l’aide du SDK Document Security pour envoyer des documents au serveur AEM Forms désigné et les politiques sont appliquées sur le serveur. Le SDK client Document Security d’AEM Forms (CSDK) ne peut pas annuler la protection des documents protégés à l’aide de la bibliothèque portable de protection (PPL) et inversement.

  Le SDK Document Security est disponible pour Java™ et C++. Le SDK Java™ est inclus dans l’offre AEM Forms Document Security et il est installé sur le déploiement d’AEM forms on JEE. Contactez l’[Assistance clientèle AEM](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support) pour obtenir le SDK C++. Le SDK C++ peut être compilé avec Microsoft® Visual Studio 2013. Visitez le site de la [documentation de l’API Document Security](https://help.adobe.com/fr_FR/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) où vous pouvez apprendre et utiliser les fonctionnalités du SDK.

* **Adobe Acrobat :** vous pouvez utiliser Adobe Acrobat pour appliquer la politique de sécurité à des documents PDF créés à l’aide d’applications de bureau courantes, telles que Microsoft® Office, des navigateurs web ou toute application prenant en charge l’impression au format PDF.

  Vous pouvez acheter et télécharger Adobe Acrobat sur le [site web d’Adobe](https://www.adobe.com/fr/acrobat/free-trial-download.html). L’article Adobe Acrobat concernant la [configuration des politiques de sécurité pour les fichiers PDF](https://helpx.adobe.com/fr/acrobat/using/setting-security-policies-pdfs.html) contient des informations détaillées sur la création et l’application de politiques dans Adobe Acrobat.

* **Document Security Extension for Microsoft® Office** : vous pouvez utiliser Document Security Extension for Microsoft® Office pour appliquer des politiques prédéfinies à vos fichiers Microsoft® Office à partir des programmes Microsoft® Office. L’extension garantit que seules les personnes autorisées puissent utiliser des fichiers Microsoft® Word, Excel et PowerPoint protégés par une politique. Seuls les personnes autorisées ayant installé le module complémentaire peuvent utiliser les fichiers protégés par une politique.

  L’extension Document Security est disponible sous forme de plug-in de Microsoft® Office. Contactez l’[Assistance clientèle AEM](https://helpx.adobe.com/fr/marketing-cloud/contact-support.html) pour obtenir l&#39;extension. Ultérieurement, vous pourrez consulter [Document Security Extension for Microsoft® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=fr) pour découvrir comment installer, configurer et utiliser l’extension.

* **Bibliothèque portable de protection :** la PPL protège un document localement, sans l’envoyer au serveur AEM Forms. Seuls les détails de politiques et les informations d’identification de sécurité transitent sur le réseau. La PPL vous permet également de limiter l’accès à la récupération de la politique aux seuls utilisateurs ou utilisatrices connectés. Vous pouvez récupérer des politiques avec le contexte de l’utilisateur ou l’utilisatrice connecté à l’utilisateur ou l’utilisatrice AEM.

  En plus de ce qui est mentionné ci-dessus, la PPL possède toutes les fonctionnalités du SDK Document Security. Vous pouvez utiliser SDK Document Security pour accéder aux fonctionnalités du serveur de documents, ouvrir des documents protégés par une politique et développer des extensions personnalisées, des modules complémentaires ou des applications. La PPL ne peut pas annuler la protection du SDK client Document Security AEM Forms (CSDK) et inversement.

  La PPL est disponible pour les langues dJava™ et C++ dans les versions 32 bits et 64 bits. Elle est également disponible en tant que bundle OSGi pour AEM Forms on OSGi. La PPL C++ peut être compilée avec Microsoft® Visual Studio 2013. Si vous possédez un module complémentaire Document Security AEM Forms sous licence, vous pouvez contacter l’équipe d’assistance de [Document Security AEM Forms](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support) pour accéder à la PPL. Ultérieurement, vous pouvez utiliser l’aide de la PPL (fournie avec la bibliothèque) pour installer et utiliser la PPL.

### Afficher ou modifier des documents protégés {#view-or-edit-protected-documents}

* Pour les **documents PDF**, vous pouvez utiliser Adobe Acrobat DC, Acrobat Reader et Acrobat Reader Mobile pour afficher les documents PDF protégés. Acrobat Reader est souvent déjà installé sur le périphérique de la plupart des utilisateurs et des utilisatrices, qui n’ont donc pas besoin d’obtenir ou d’apprendre un nouveau logiciel pour afficher les documents protégés. Vous pouvez également télécharger Acrobat Reader à partir du [site web de téléchargement d’Acrobat Reader](https://get.adobe.com/fr/reader/).

* Pour les **documents Microsoft® Office**, vous devez disposer de Microsoft® Office et de l’extension Document Security for Microsoft® Office AEM Forms. L’extension Document Security est disponible sous forme de plug-in de Microsoft® Office. Vous pouvez télécharger l’extension depuis le site Web d’Adobe.

### Indexer les documents protégés {#index-protected-documents}

Les moteurs de recherche de texte intégral de Microsoft® Windows (serveur SharePoint Index) et Adobe Experience Manager (AEM) peuvent effectuer une recherche de texte intégral dans les formats de document courants tels que les fichiers texte brut, les documents Microsoft® Office et les fichiers PDF. Vous pouvez utiliser des indexeurs Document Security pour permettre aux moteurs de recherche de texte intégral de rechercher les documents PDF protégés :

* **Indexeur iFilter :** vous pouvez utiliser l’indexeur iFilter pour indexer des documents PDF protégés et permettre aux moteurs de recherche de texte intégral de Microsoft® Windows (service d’indexation de bureau et serveur SharePoint Index) de rechercher les documents PDF protégés. Pour plus d’informations, reportez-vous à [AEM SharePoint IFilter pour documents protégés](assets/sharepoint-ifilter-doc-security.pdf).

* **Indexeur de Document Security AEM Forms :** vous pouvez utiliser l’indexeur de Document Security AEM Forms pour indexer des documents PDF protégés et permettre à Adobe Experience Manager de rechercher les documents PDF protégés. Les indexeurs font partie de l’offre de Document Security AEM Forms. Ils sont inclus dans les programmes d’installation AEM Forms on JEE.
