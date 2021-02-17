---
title: Gestion de certificats
seo-title: Gestion de certificats
description: Découvrez comment importer et exporter un certificat et modifier ses paramètres d’approbation.
seo-description: Découvrez comment importer et exporter un certificat et modifier ses paramètres d’approbation.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 83%

---


# Gestion de certificats {#managing-certificates}

Trust Store Management vous permet d’importer, de modifier et de supprimer des certificats de confiance sur le serveur pour valider des signatures numériques et l’authentification de certificats. Vous pouvez en importer et en exporter autant que vous le souhaitez. Une fois qu’un certificat a été importé, vous pouvez modifier les paramètres d’approbation et le type de Trust Store. Pensez aux options suivantes lorsque vous combinez des types de Trust Store :

* **Approbation de l’authentification de certificats avec l’autorité de certification :** pour la validation de CRL, sélectionnez également Approbation d’identité.
* **Approbation de l’authentification de certificats avec l’ICA :** sélectionnez uniquement Approbation d’identité.. Un ICA ne doit pas être approuvé pour l’authentification de certificats. Si vous approuvez l’ICA pour l’authentification de certificats, l’ICA devient une autorité de certification pour la création de chemins. Si l’ICA est approuvé pour l’authentification de certificats et l’identité, le certificat du fournisseur de l’autorité de certification est ignoré car l’ICA devient l’autorité de certification.
* **Approbation du serveur OCSP avec HTTPS :** si le serveur du répondant OSCP réside sur un site HTTPS, vous devez également sélectionner Approbation de connexions SSL. Si le répondant OSCP requiert une validation CRL, vérifiez que vous sélectionnez également Approbation d’identité.
* **Racine Adobe :** ne sélectionnez ni Connexions SSL ni Types de Trust Store du serveur OCSP. Racine Adobe n’est pas approuvé pour les connexions SSL et le serveur OCSP. Adobe n’émet pas de certificats OCSP et SSL. Racine Adobe est implicitement approuvé avec l’alias « ADOBEROOT ».

Seuls les certificats X509v3 sont pris en charge. Ce type de certificat peut être fourni dans un fichier codé DER binaire (fichier .cer) ou un fichier texte qui contient une version codée Base64 du même certificat codé DER (y compris des certificats X509 au format PEM (Privacy Enhanced Mail)).

Les certificats requis pour vérifier des signatures doivent résider au même emplacement de stockage (module HSM ou base de données).

Vous pouvez également importer et supprimer des certificats à l’aide de l’API Trust Manager. Pour plus d’informations, reportez-vous aux sections « Importation des certificats à l’aide de l’API Trust Manager » et « Suppression des certificats à l’aide de l’API Trust Manager » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importation d’un certificat {#import-a-certificate}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Trust Store Management > Certificats]**.
1. Cliquez sur Importer, puis, sous Type de Trust Store, sélectionnez l’une des options suivantes :

   * **Approbation de connexions SSL :** indique qu’AEM Forms peut utiliser des certificats pour établir une connexion à des systèmes externes via SSL.
   * **Approbation de certification de signature :** indique que des certificats sont approuvés dans des opérations de signature de document pour certifier les signatures numériques d’auteurs.
   * **Approbation de signature :** indique que des certificats sont approuvés dans des opérations de signature de document pour les signatures numériques de non-auteurs.
   * **Approbation d’authentification de certificats :** indique que des certificats sont utilisés par AEM forms pour authentifier des utilisateurs par le biais d’une authentification de certificat ou de carte à puce.
   * **Approbation de serveur OCSP :** indique qu’AEM forms peut utiliser des certificats pour établir une connexion à des répondeurs OCSP externes.
   * **Approbation d’identité :** indique que des certificats peuvent être utilisés pour approuver des types d’informations autres que ceux indiqués ci-dessus.

   >[!NOTE]
   >
   >un certificat racine Adobe est implicitement approuvé par le Trust Store pour l’authentification de certificat, la signature, la certification de signature et l’identité.

1. Dans la zone Alias, saisissez l’identificateur du certificat.
1. Cliquez sur **[!UICONTROL Parcourir]** pour localiser le certificat, puis sur **[!UICONTROL OK]**.

## Exportation d’un certificat {#export-a-certificate}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Trust Store Management > Certificats]**.
1. Cliquez sur le nom d’alias du certificat à exporter. La page **[!UICONTROL Détails du certificat]** s&#39;affiche.
1. Cliquez sur **[!UICONTROL Exporter]**, suivez les instructions pour exporter le certificat, puis cliquez sur **[!UICONTROL OK]**.

## Modification des paramètres d’approbation et du type de Trust Store d’un certificat {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Trust Store Management > Certificats]**.
1. Cliquez sur le nom d’alias du certificat à modifier.
1. Cliquez sur **[!UICONTROL Mettre à jour le certificat]**.
1. Pour modifier le nom d’alias du certificat, saisissez en un nouveau dans la zone Alias.
1. Pour mettre à jour le type de Trust Store du certificat, sélectionnez le type de Trust Store approprié.
1. Pour mettre à jour les restrictions de stratégie, dans la zone Stratégies de certificat, saisissez les informations de stratégie, puis cliquez sur **[!UICONTROL OK]**.

## Suppression d’un certificat {#delete-a-certificate}

1. Dans Administration Console, cliquez sur **[!UICONTROL Paramètres > Trust Store Management > Certificats]**.
1. Cochez les cases correspondant aux certificats à supprimer, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL OK]**.

