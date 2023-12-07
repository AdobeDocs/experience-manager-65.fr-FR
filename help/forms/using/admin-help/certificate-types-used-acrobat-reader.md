---
title: Types de certificats utilisés par les extensions d’Acrobat Reader DC
description: Découvrez les types de certificats utilisés par les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 26%

---

# Types de certificats utilisés par les extensions d’Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

La visionneuse de certificats fournit les informations suivantes sur le certificat :

* Nom « convivial » du certificat
* Profils de certificat
* Période de validité
* Droits d’utilisation des extensions Acrobat Reader DC

## Nom « convivial » du certificat {#certificate-friendly-name}

Le nom &quot;convivial&quot; d’un certificat d’extensions Acrobat Reader DC est une chaîne qui décrit les propriétés du certificat, comme dans l’exemple suivant :

ARE Code-barres 2D Full Production V6.1 P8 0002054

La chaîne contient les éléments suivants :

**Type de certificat :** décrit les modules AEM Forms que le certificat active et le niveau d’activation, par exemple ARE 2D Barcode Full. Pour la liste des types de certificat, reportez-vous à la colonne Type du tableau de la section Profils de certificat.

**Type de déploiement :** indique l’utilisation prévue du certificat, par exemple en mode Production. Cette valeur peut être Evaluation ou Production. Pour la liste des types de déploiement associés à chaque type de certificat, reportez-vous à la colonne Type de déploiement du tableau de la section Profils de certificat.

**Version des droits d’utilisation :** décrit la version de l’algorithme des droits d’utilisation que le certificat peut utiliser, par exemple V6.1. Il ne s’agit cependant pas de la version d’Acrobat ni des extensions Acrobat Reader DC.

**Code de profil :** le code de profil est une description brève des propriétés complètes du certificat (par exemple, P8). Pour la liste des codes de profil associés à chaque type de fichier, reportez-vous à la colonne Profil du tableau de la section Profils de certificat.

**Numéro de série :** un numéro de série est attribué à chaque certificat émis par Adobe, par exemple 0002054. Le support aux entreprises d’Adobe ou un représentant commercial Adobe Enterprise peut utiliser ce numéro de série pour rattacher le certificat à une commande de produit spécifique ou à une relation OEM.

## Profils de certificat {#certificate-profiles}

Le tableau suivant répertorie les profils de certificat que vous pouvez rencontrer lors de l’analyse des certificats des extensions Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Code de profil</p></th>
   <th><p>Type</p></th>
   <th><p>Période de validité</p></th>
   <th><p>Type de déploiement</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>Production SAP</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>Test interne SAP</p></td>
   <td><p>2 ans</p></td>
   <td><p>Évaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensions Acrobat Reader DC, production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensions Acrobat Reader DC, utilisation de l’Adobe interne</p></td>
   <td><p>2 ans</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensions Acrobat Reader DC, Intégration de partenaire</p></td>
   <td><p>2 ans</p></td>
   <td><p>Évaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensions Acrobat Reader DC, évaluation</p></td>
   <td><p>60 jours</p></td>
   <td><p>Évaluation</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Signature uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Commentaires hors ligne uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Commentaires uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Autorisations complètes ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
 </tbody>
</table>

## Période de validité {#validity-period}

Les certificats d’évaluation sont délivrés aux clients et aux développeurs afin qu’ils puissent évaluer et développer des exemples d’applications pour les produits. La période de validité de ces certificats est comprise entre 60 et 90 jours. Elles expirent à la fin du deuxième mois suivant les données de l’émission.

Les certificats d’intégration de partenaire sont émis pour Adobe les partenaires commerciaux à prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à compter de la date de publication.

Les certificats à usage interne Adobe sont utilisés dans Adobe pour prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à compter de la date de publication.

Les certificats de production sont délivrés aux clients qui ont acheté des extensions Acrobat Reader DC. Ces certificats sont valides pendant la période maximale autorisée par l’autorité de certification (CA), comme indiqué ci-dessous : *Max* dans la table Profils de certificat .

## Droits d’utilisation des extensions Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Lorsque vous examinez le certificat des extensions Acrobat Reader DC dans la visionneuse de certificats, vous pouvez sélectionner l’élément des droits d’utilisation dans l’onglet Détails (s’il est configuré) pour afficher une liste détaillée des droits d’utilisation Adobe Reader que le certificat peut activer. Les droits d’utilisation activés sur un document particulier peuvent être un sous-ensemble de ceux activés par le certificat.

Si des commentaires en ligne sont requis dans un environnement non collaboratif, contactez l’assistance Adobe pour plus d’informations. La propriété Mode correspond au type de déploiement et est *production* ou *évaluation*.

Les droits d’utilisation des extensions Acrobat Reader DC autorisés se composent d’un ou de plusieurs éléments spécifiques. Ces éléments sont utilisés dans différentes combinaisons afin d’obtenir diverses fonctionnalités de produit sous licence.

<table>
 <thead>
  <tr>
   <th><p>Elément Droits d’utilisation</p></th>
   <th><p>Fonctionnalité activée dans Adobe Reader lors de l’affichage d’un document de PDF dont les droits sont activés</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Renseignez les champs du formulaire et enregistrez les fichiers localement.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importez et exportez des données de formulaire au format FDF, XFDF, XML et XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Ajoutez, modifiez ou supprimez des champs et des propriétés de champ sur le formulaire du PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Envoyez des données, par courrier électronique ou hors ligne, à un serveur lorsqu’il ne s’exécute pas dans une session de navigateur.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Créez des pages à partir de pages de modèle dans le même formulaire de PDF.</p></td>
  </tr>
  <tr>
   <td><p>Signature</p></td>
   <td><p>Signer numériquement et enregistrer des documents de PDF et effacer des signatures numériques.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Créez et modifiez des annotations de document, telles que des commentaires.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Enregistrez les annotations telles que les commentaires dans un fichier de données distinct et chargez les commentaires à partir d’un fichier.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Imprimer un document avec des données de formulaire codées à barres sous une forme non chiffrée qui ne nécessite pas de logiciel de serveur sous licence pour être décodée.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Téléchargez des annotations telles que des commentaires vers et depuis un serveur de révision et de commentaires de documents en ligne.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Connectez-vous à des services web ou à des bases de données définis dans un formulaire de PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifiez les objets de fichier incorporés associés au document du PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Les droits d’utilisation des extensions d’Acrobat Reader DC ne peuvent être concédés sous licence que par Adobe dans certaines combinaisons qui fonctionnent ensemble. Il n’est pas possible d’acquérir ces fonctionnalités indépendamment sous licence. Pour plus d’informations sur les combinaisons de droits d’utilisation disponibles, contactez AEM gestionnaire de compte forms.
