---
title: Types de certificats utilisés par les extensions d’Acrobat Reader DC
description: Découvrez les types de certificats utilisés par les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '944'
ht-degree: 100%

---

# Types de certificats utilisés par les extensions d’Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

La visionneuse de certificats fournit les informations suivantes sur le certificat :

* Nom « convivial » du certificat
* Profils du certificat
* Période de validité
* Droits d’utilisation des extensions Acrobat Reader DC

## Nom « convivial » du certificat {#certificate-friendly-name}

Le nom « convivial » d’un certificat d’extensions Acrobat Reader DC est une chaîne qui décrit les propriétés du certificat, comme dans l’exemple suivant :

ARE 2D Barcode Full Production V6.1 P8 0002054

La chaîne comprend les éléments suivants :

**Type de certificat :** décrit les modules AEM Forms que le certificat active et le niveau d’activation, par exemple ARE 2D Barcode Full. Pour la liste des types de certificat, reportez-vous à la colonne Type du tableau de la section Profils de certificat.

**Type de déploiement :** indique l’utilisation prévue du certificat, par exemple en mode Production. Cette valeur peut être Evaluation ou Production. Pour la liste des types de déploiement associés à chaque type de certificat, reportez-vous à la colonne Type de déploiement du tableau de la section Profils de certificat.

**Version des droits d’utilisation :** décrit la version de l’algorithme des droits d’utilisation que le certificat peut utiliser, par exemple V6.1. Il ne s’agit cependant pas de la version d’Acrobat ni des extensions Acrobat Reader DC.

**Code de profil :** le code de profil est une description brève des propriétés complètes du certificat (par exemple, P8). Pour la liste des codes de profil associés à chaque type de fichier, reportez-vous à la colonne Profil du tableau de la section Profils de certificat.

**Numéro de série :** un numéro de série est attribué à chaque certificat émis par Adobe, par exemple 0002054. Le support aux entreprises d’Adobe ou un représentant commercial Adobe Enterprise peut utiliser ce numéro de série pour rattacher le certificat à une commande de produit spécifique ou à une relation OEM.

## Profils du certificat {#certificate-profiles}

Le tableau suivant répertorie les différents profils de certificat que vous pouvez rencontrer en analysant des certificats des extensions Acrobat Reader DC.

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
   <td><p>Évaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensions Acrobat Reader DC, Production</p></td>
   <td><p>Max</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensions Acrobat Reader DC, Usage interne d’Adobe</p></td>
   <td><p>2 ans</p></td>
   <td><p>Production</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensions Acrobat Reader DC, Intégration de partenaire</p></td>
   <td><p>2 ans</p></td>
   <td><p>Évaluation et test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensions Acrobat Reader DC, Évaluation</p></td>
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
   <td><p>Adobe Acrobat 7.x, Production</p></td>
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
   <td><p>Autorisations complètes ; peut être utilisé par les OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Production et évaluation</p></td>
  </tr>
 </tbody>
</table>

## Période de validité {#validity-period}

Les certificats d’évaluation sont délivrés aux client et clientes et aux développeurs et développeuses afin qu’ils puissent évaluer et développer des exemples d’applications pour les produits. La période de validité de ces certificats est comprise entre 60 et 90 jours. Ils expirent à la fin du second mois suivant la date d’émission.

Les certificats du type Intégration de partenaire sont fournis aux partenaires commerciaux Adobe pour prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à partir de la date d’émission.

Les certificats du type Usage interne Adobe sont utilisés en interne par Adobe pour prendre en charge le développement, l’intégration, le prototypage et la démonstration de logiciels. Ces certificats sont valables deux ans à partir de la date d’émission.

Les certificats de production sont délivrés aux clients et clientes qui ont acheté les extensions Acrobat Reader DC. Ces certificats sont valides pendant la période maximale autorisée par l’autorité de certification (CA), définie comme « *Max* » dans le tableau Profils de certificat.

## Droits d’utilisation des extensions Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Lorsque vous examinez le certificat des extensions Acrobat Reader DC dans la visionneuse de certificats, vous pouvez sélectionner l’élément des droits d’utilisation dans l’onglet Détails (s’il est configuré) pour afficher une liste détaillée des droits d’utilisation Adobe Reader que le certificat peut activer. Les droits d’utilisation activés sur un document particulier peuvent être un sous-ensemble de ceux activés par le certificat.

Si des commentaires en ligne sont requis dans un environnement non collaboratif, contactez l’assistance Adobe pour plus d’informations. La propriété Mode correspond au type de déploiement et est *production* ou *évaluation*.

Les droits d’utilisation des extensions Acrobat Reader DC autorisés se composent d’un ou de plusieurs éléments spécifiques. Ces éléments sont utilisés dans différentes combinaisons afin d’obtenir diverses fonctionnalités de produit sous licence.

<table>
 <thead>
  <tr>
   <th><p>Élément Droits d’utilisation</p></th>
   <th><p>Fonctionnalité activée dans Adobe Reader lors de l’affichage d’un document PDF dont les droits sont activés</p></th>
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
   <td><p>Envoyer des données par e-mail ou hors ligne à un serveur lorsqu’il n’est pas en cours d’exécution dans une session de navigateur.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Créer des pages à partir des pages de modèle du même formulaire PDF.</p></td>
  </tr>
  <tr>
   <td><p>Signature</p></td>
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
   <td><p>Imprimer un document avec des données de formulaire sous forme de code-barres et non chiffrée qui ne nécessite pas de logiciel de serveur sous licence pour être décodée.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Télécharger des annotations (comme des commentaires) vers et depuis un serveur permettant de réviser et de commenter des documents en ligne.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Se connecter à des services web ou à des bases de données définis dans un formulaire PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifier les objets de fichier incorporés associés au document PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Les droits d’utilisation des extensions Acrobat Reader DC ne peuvent être concédés sous licence que par Adobe dans certaines combinaisons qui fonctionnent ensemble. Il est impossible d’acquérir ces fonctionnalités indépendamment sous licence. Pour plus d’informations sur les combinaisons de droits d’utilisation disponibles, contactez un gestionnaire de compte AEM Forms.
