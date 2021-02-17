---
title: Types de certificats utilisés par les extensions d’Acrobat Reader DC
seo-title: Types de certificats utilisés par les extensions d’Acrobat Reader DC
description: Découvrez les types de certificats utilisés par les extensions Acrobat Reader DC.
seo-description: Découvrez les types de certificats utilisés par les extensions Acrobat Reader DC.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 86%

---


# Types de certificats utilisés par les extensions d’Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

L’afficheur de certificat fournit les informations suivantes sur le certificat :

* Nom « convivial » du certificat
* Profils du certificat
* Période de validité
* Droits d’utilisation des extensions d’Acrobat Reader DC

## Nom « convivial » du certificat {#certificate-friendly-name}

Le nom « convivial » d’un certificat des extensions d’Acrobat Reader DC est une chaîne décrivant les propriétés du certificat, comme dans l’exemple suivant :

ARE Code-barres 2D Complète Production V6.1 P8 0002054

Cette chaîne contient les éléments suivants :

**Type de certificat :** décrit les modules de formulaires AEM activés par le certificat, ainsi que le niveau d’activation, tel que ARE Code à barres 2D Complet. Pour la liste des types de certificat, reportez-vous à la colonne Type du tableau de la section Profils de certificat.

**Type de déploiement :** indique l’utilisation prévue du certificat, telle que Production. Cette valeur peut être Evaluation ou Production. Pour la liste des types de déploiement associés à chaque type de certificat, reportez-vous à la colonne Type de déploiement du tableau de la section Profils de certificat.

**Version des droits d’utilisation :** décrit la version de l’algorithme des droits d’utilisation pour laquelle le certificat peut être utilisé, par exemple V6.1. Cette version ne signifie pas la version des extensions Acrobat ou Acrobat Reader DC.

**Code de profil :** le code de profil est une description abrégée des propriétés complètes du certificat, par exemple, P8. Pour la liste des codes de profil associés à chaque type de fichier, reportez-vous à la colonne Profil du tableau de la section Profils de certificat.

**Numéro de série :** un numéro de série est attribué à chaque certificat émis par l’Adobe, par exemple 0002054. Adobe Enterprise Support ou un représentant du compte Enterprise Adobe peut utiliser ce numéro de série pour tracer le certificat à une commande de produit spécifique ou à une relation OEM.

## Profils du certificat {#certificate-profiles}

Le tableau suivant répertorie les différents profils de certificat que vous pouvez rencontrer en analysant des certificats des extensions d’Acrobat Reader DC.

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
   <td><p>2 ans</p></td>
   <td><p>Evaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensions d’Acrobat Reader DC, Production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensions d’Acrobat Reader DC, Usage interne d’Adobe</p></td>
   <td><p>2 ans</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensions d’Acrobat Reader DC, Intégration de partenaire</p></td>
   <td><p>2 ans</p></td>
   <td><p>Evaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensions d’Acrobat Reader DC, Évaluation</p></td>
   <td><p>60 jours</p></td>
   <td><p>Évaluation</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, Production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, Production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Signature uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Commentaires hors ligne uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Commentaires uniquement ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Droits complets ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
 </tbody>
</table>

## Période de validité  {#validity-period}

Les certificats d’évaluation sont fournis aux clients et aux développeurs pour leur permettre d’évaluer et de développer des exemples d’applications pour les produits. La période de validité de ces certificats est comprise entre 60 et 90 jours. Ils expirent à la fin du second mois suivant la date d’émission.

Les certificats du type Intégration de partenaire sont fournis aux partenaires commerciaux Adobe pour prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à partir de la date d’émission.

Les certificats du type Usage interne Adobe sont utilisés en interne par Adobe pour prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à partir de la date d’émission.

Les certificats du type Production sont fournis aux clients qui ont acheté les extensions d’Acrobat Reader DC. Ces certificats sont valables pendant la durée maximale autorisée par la CA (Certificate Authority, Autorité de certification), définie comme « *Max* » dans le tableau Profils de certificat.

## Droits d’utilisation des extensions d’Acrobat Reader DC  {#acrobat-reader-dc-extensions-usage-rights}

Lorsque vous examinez le certificat des extensions d’Acrobat Reader DC dans l’Afficheur de certificat, sélectionnez l’élément Droits d’utilisation dans l’onglet Détails (s’il est configuré) pour afficher la liste des droits d’utilisation Adobe Reader qui peuvent être activés par le certificat. Les droits d’utilisation activés sur un document particulier peuvent être un sous-ensemble de ceux activés par le certificat.

Si les commentaires en ligne sont requis dans un environnement non collaboratif, contactez le service d’assistance d’Adobe pour obtenir de plus amples informations. La propriété Mode correspond au type de déploiement, soit *production* ou *évaluation*.

Les droits d’utilisation des extensions d’Acrobat Reader DC autorisés comprennent un ou plusieurs éléments spécifiques. Ceux-ci sont utilisés dans différentes combinaisons pour obtenir différentes fonctionnalités de produit sous licence.

<table>
 <thead>
  <tr>
   <th><p>Elément des droits d’utilisation</p></th>
   <th><p>Opérations autorisées dans Adobe Reader en affichant un document PDF dont les droits d’utilisation sont activés</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Remplir des formulaires et enregistrer des fichiers en local.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importer et exporter des données de formulaire aux formats FDF, XFDF, XML et XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Ajouter, modifier ou supprimer des champs et des propriétés de champ dans le formulaire PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Envoyer des données par courrier électronique ou hors ligne à un serveur lorsqu’il n’est pas en cours d’exécution dans une session de navigateur.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Créer des pages à partir des pages de modèle du même formulaire PDF.</p></td>
  </tr>
  <tr>
   <td><p>Signing</p></td>
   <td><p>Signer numériquement et enregistrer des documents PDF et effacer des signatures numériques.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Créer et modifier des annotations de document (comme des commentaires).</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Enregistrer des annotations (comme des commentaires) dans un fichier de données séparé et charger des commentaires depuis un fichier.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Imprimer un document avec des données de formulaire à code-barres sous une forme non chiffrée ne nécessitant pas un logiciel serveur sous licence pour être décodée.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Télécharger des annotations (comme des commentaires) vers et depuis un serveur permettant de réviser et de commenter des documents en ligne.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Se connecter à des services Web ou à des bases de données définis dans un formulaire PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifier les pièces jointes incorporées associées au document PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe ne peut concéder des droits d’utilisation des extensions d’Acrobat Reader DC sous licence que pour certaines combinaisons fonctionnelles. Il est impossible d’obtenir la licence d’utilisation de ces fonctionnalités indépendamment. Pour plus d’informations sur les combinaisons de droits d’utilisation proposées, contactez votre représentant commercial AEM forms.

