---
title: Gérer des certificats
description: Découvrez comment importer et exporter un certificat et modifier ses paramètres d’approbation.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 100%

---

# Gérer des certificats {#managing-certificates}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Trust Store Management vous permet d’importer, de modifier et de supprimer des certificats de confiance sur le serveur pour valider des signatures numériques et l’authentification de certificats. Vous pouvez en importer et en exporter autant que vous le souhaitez. Une fois qu’un certificat a été importé, vous pouvez modifier les paramètres d’approbation et le type de Trust Store. Pensez aux options suivantes lorsque vous combinez des types de Trust Store :

* **Approbation de l’authentification de certificats avec l’autorité de certification :** pour la validation de CRL, sélectionnez également Approbation d’identité.
* **Approbation de l’authentification de certificats avec l’ICA :** sélectionnez uniquement Approbation d’identité.. Un ICA ne doit pas être approuvé pour l’authentification de certificats. Si vous approuvez l’ICA pour l’authentification de certificats, l’ICA devient une autorité de certification pour la création de chemins. Si l’ICA est approuvé pour l’authentification de certificats et l’identité, le certificat du fournisseur de l’autorité de certification est ignoré car l’ICA devient l’autorité de certification.
* **Approbation du serveur OCSP avec HTTPS :** si le serveur du répondant OSCP réside sur un site HTTPS, vous devez également sélectionner Approbation de connexions SSL. Si le répondant OSCP requiert une validation CRL, vérifiez que vous sélectionnez également Approbation d’identité.
* **Racine Adobe :** ne sélectionnez ni Connexions SSL ni Types de Trust Store du serveur OCSP. Adobe Root n’est pas approuvé pour les connexions SSL et le serveur OCSP. Adobe n’émet pas de certificats OCSP et SSL. Adobe Root est implicitement approuvé avec l’alias « ADOBEROOT ».

Seuls les certificats X509v3 sont pris en charge. Ce type de certificat peut être fourni dans un fichier codé DER binaire (fichier .cer) ou un fichier texte contenant une version codée Base64 du même certificat codé DER (y compris les certificats X509 au format PEM (Privacy Enhanced Mail)).

Les certificats requis pour effectuer une vérification de signature doivent se trouver dans le même magasin (HSM ou base de données).

Vous pouvez également importer et supprimer des certificats à l’aide de l’API Trust Manager. Pour plus d’informations, reportez-vous aux sections « Importation des certificats à l’aide de l’API Trust Manager » et « Suppression des certificats à l’aide de l’API Trust Manager » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).

## Importer un certificat {#import-a-certificate}

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > Gestion de Trust Store > Certificats]**.
1. Cliquez sur Importer, puis, sous Type de Trust Store, sélectionnez l’une des options suivantes :

   * **Approbation de connexions SSL :** indique qu’AEM Forms peut utiliser des certificats pour établir une connexion à des systèmes externes via SSL.
   * **Approbation de certification de signature :** indique que des certificats sont approuvés dans des opérations de signature de document pour certifier les signatures numériques d’auteurs.
   * **Approbation de signature :** indique que des certificats sont approuvés dans des opérations de signature de document pour les signatures numériques de non-auteurs.
   * **Approbation d’authentification de certificats :** indique que des certificats sont utilisés par AEM forms pour authentifier des utilisateurs par le biais d’une authentification de certificat ou de carte à puce.
   * **Approbation de serveur OCSP :** indique qu’AEM forms peut utiliser des certificats pour établir une connexion à des répondeurs OCSP externes.
   * **Approbation d’identité :** indique que des certificats peuvent être utilisés pour approuver des types d’informations autres que ceux indiqués ci-dessus.

   >[!NOTE]
   >
   >Un certificat Adobe Root est implicitement approuvé par le Trust Store pour l’authentification de certificat, la signature, la certification de signature et l’identité.

1. Dans la zone Alias, saisissez l’identifiant du certificat.
1. Cliquez sur **[!UICONTROL Parcourir]** pour localiser le certificat, puis sur **[!UICONTROL OK]**.

## Exportation d’un certificat {#export-a-certificate}

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > Gestion de Trust Store > Certificats]**.
1. Cliquez sur le nom d’alias du certificat à exporter. La page **[!UICONTROL Détails du certificat]** s’affiche.
1. Cliquez sur **[!UICONTROL Exporter]**, suivez les instructions pour exporter le certificat, puis cliquez sur **[!UICONTROL OK]**.

## Modification des paramètres d’approbation et du type de Trust Store d’un certificat {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > Gestion de Trust Store > Certificats]**.
1. Cliquez sur le nom d’alias du certificat à modifier.
1. Cliquez sur **[!UICONTROL Mettre à jour le certificat]**.
1. Pour modifier le nom de l’alias du certificat, saisissez un nouveau nom dans la zone Alias.
1. Pour mettre à jour le type de Trust Store du certificat, sélectionnez le type de Trust Store approprié.
1. Pour mettre à jour les restrictions de la politique, dans la zone Politiques des certificats, saisissez les informations de politique, puis cliquez sur **[!UICONTROL OK]**.

## Suppression d’un certificat {#delete-a-certificate}

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > Gestion de Trust Store > Certificats]**.
1. Cochez les cases des certificats à supprimer, cliquez sur **[!UICONTROL Supprimer]**, puis sur **[!UICONTROL OK]**.
