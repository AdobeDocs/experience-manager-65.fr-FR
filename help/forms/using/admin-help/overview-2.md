---
title: Principes de base de la gestion des certificats et des informations d’identification
seo-title: Principes de base de la gestion des certificats et des informations d’identification
description: Découvrez les bases de la gestion des certificats et des informations d’identification.
seo-description: Découvrez les bases de la gestion des certificats et des informations d’identification.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 86%

---

# Principes de base de la gestion des certificats et des informations d’identification {#basics-of-managing-certificates-and-credentials}

Les *informations d’identification* contiennent les informations de clé privée dont vous avez besoin pour signer ou identifier des documents. Un *certificat* correspond aux informations de clé publique que vous configurez pour l’approbation. AEM forms utilise des certificats et des informations d’identification à plusieurs fins :

* Les extensions d’Acrobat Reader DC utilisent des informations d’identification pour activer les droits Adobe Reader des documents PDF (voir [Configuration des informations d’identification à utiliser avec les extensions d’Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)).
* Vous pouvez configurer Rights Management pour afficher les informations d’identification à utiliser dans Acrobat émanant uniquement des émetteurs autorisés (voir [Configuration des paramètres d’affichage de Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)). Le nom commun ou CN (pour Common Name) doit figurer dans le certificat.
* Le service Signature a accès aux certificats et aux informations d’identification. Pour plus d’informations sur le service Signature, voir le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

**Génération d’une paire de clés**

AEM forms utilise son composant Trust Store pour stocker et gérer les certificats, les informations d’identification ainsi que les listes de révocation des certificats (CRL). Vous pouvez également utiliser un périphérique HSM (Hardware Security Module, module de sécurité matérielle) indépendant pour stocker des clés privées.

AEM forms ne propose pas d’option permettant de générer une paire de clés. Toutefois, vous pouvez le générer à l’aide d’outils, tels que Java keytool, et l’importer dans le composant Trust Store d’AEM forms. Pour plus d’informations sur Java keytool, consultez les articles suivants :

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

Les types de signature suivants sont pris en charge et peuvent être importés dans AEM Forms :

* Signature XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Signatures DSA

**Gestion d’une clé perdue ou compromise**

Si vous pensez que votre clé est perdue ou a été compromise, procédez comme suit :

1. Avertissez l’autorité de certification afin qu’elle ajoute la clé compromise à la liste de révocation de certificats et retire la clé.
1. Demandez une nouvelle clé et ses certificats à l’autorité de certification.
1. Signez de nouveau les documents qui ont été signés avec la clé compromise à l’aide de la nouvelle clé.
