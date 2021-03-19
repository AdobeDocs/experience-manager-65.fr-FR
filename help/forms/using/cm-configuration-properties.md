---
title: Propriétés de configuration de Correspondence Management
seo-title: Propriétés de configuration de Correspondence Management
description: Cette rubrique explique comment modifier Asset Composer avec des configurations propres à cette solution. Cette rubrique détaille les propriétés que vous pouvez modifier, avec leur description, leurs valeurs par défaut et leurs valeurs acceptables.
seo-description: Cette rubrique explique comment modifier Asset Composer avec des configurations propres à cette solution. Cette rubrique détaille les propriétés que vous pouvez modifier, avec leur description, leurs valeurs par défaut et leurs valeurs acceptables.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 97%

---


# Propriétés de configuration de Correspondence Management {#correspondence-management-configuration-properties}

Pour configurer ces propriétés, ouvrez l’URL suivante dans un navigateur : `https://<server>:<port>/<contextPath>/system/console/configMgr` et sélectionnez **Configurations de Correspondence Management**.

Correspondence Management possède les propriétés de configuration suivantes :

<table>
 <tbody>
  <tr>
   <th><p><strong>Propriété</strong></p> </th>
   <th><p><strong>Description</strong></p> </th>
   <th><p><strong>Valeur par défaut</strong></p> </th>
   <th><p><strong>Valeurs acceptables</strong></p> </th>
  </tr>
  <tr>
   <td><p>Indentation</p> </td>
   <td>Retrait sur les modules<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Number Minimum Width</td>
   <td>Largeur minimale à appliquer au champ de puce/nombre, lors de l’utilisation de listes numérotées, à l’exception des chiffres romains.</td>
   <td>8,0 mm</td>
   <td>N’importe quel nombre</td>
  </tr>
  <tr>
   <td><p>Roman Numbers Minimum Width</p> </td>
   <td><p>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de chiffres romains</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Type de rendu</td>
   <td>Type de rendu que l’application de création de correspondance utilise pour restituer l’aperçu de lettre </td>
   <td>Rendu HTML</td>
   <td>Rendu HTML/Rendu PDF</td>
  </tr>
  <tr>
   <td><p>Enable CCR PDF highlight</p> </td>
   <td><p>Active la surbrillance sur PDF dans l’application de création de correspondance</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Target Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance de la cible dans l’application de création de correspondance</p> </td>
   <td><p>bordure</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Target Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance de la cible dans l’application de création de correspondance</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Content Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance du contenu dans l’application de création de correspondance</p> </td>
   <td><p>Fill</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Content Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance du contenu dans l’application de création de correspondance</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Field Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance de champ dans l’application de création de correspondance</p> </td>
   <td><p>fill</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Field Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance de champ dans l’application de création de correspondance</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Application Time Out</p> </td>
   <td><p>Délai d’expiration de l’application en secondes</p> </td>
   <td><p>1200</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td><p>PDF document parameter name</p> </td>
   <td><p>Nom de paramètre pour un document PDF dans le post-processus</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>N’importe quel nom de variable de type chaîne</p> </td>
  </tr>
  <tr>
   <td><p>XML data parameter name</p> </td>
   <td><p>Nom de paramètre pour un document XML (données) dans le post-processus</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>N’importe quel nom de variable de type chaîne</p> </td>
  </tr>
  <tr>
   <td><p>XDP document parameter name</p> </td>
   <td><p>Nom de paramètre pour un document XDP envoyé au post-processus</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>N’importe quel nom de variable de type chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Redirect URL parameter name</p> </td>
   <td><p>Nom de paramètre pour une URL de redirection envoyée depuis le post-processus. Cette valeur peut être n’importe quel nom de variable de type chaîne.</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>N’importe quel nom de variable de type chaîne</p> </td>
  </tr>
  <tr>
   <td><p>PDF Submit Type</p> </td>
   <td><p>Type d’envoi de PDF (type de fichier PDF généré lors de l’envoi depuis l’application de création de correspondance)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interactive/non-interactive</p> </td>
  </tr>
  <tr>
   <td><p>Optimize Data Dictionary Instance</p> </td>
   <td><p>Active le transfert de données optimisé de l’instance du dictionnaire de données entre le serveur et le client</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Auto Correct Inconsistencies </p> </td>
   <td><p>Lorsque cette propriété est activée, elle gère automatiquement les incohérences possibles dans les affectations de lettre</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Use Configured Data Formats</p> </td>
   <td><p>Contrôle l’utilisation des formats de modification et d’affichage des données configurés.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Data Display Formats</p> </td>
   <td><p>Spécifie le format d’affichage des données spécifique des paramètres régionaux.</p> </td>
   <td><p>locale=en_US ; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=de_DE ; dateFormat=dd-MM-yyyy; numberDecimalSeparator= ; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Data Edit Format</p> </td>
   <td><p>Format de modification des données. Cette propriété est utilisée lors de l’écriture de données en tant que chaîne ou de l’analyse des données à partir d’une chaîne.</p> </td>
   <td><p>locale=en_US ; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Manage Letter Instances on Publish</p> </td>
   <td><p>Active/désactive la fonctionnalité de gestion des lettres (applicable uniquement pour le serveur de publication)</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle. Lorsque cette propriété est définie sur false, les journaux de contrôle de toutes les actions sont désactivés.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Read Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour les lectures de ressources</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Create Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour la création de ressources</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Update Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour la mise à jour de ressources</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Revert Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour le rétablissement de ressources</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Publish Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour la publication de ressources</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable SaveAsDraft Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour l’enregistrement des brouillons de lettre</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Submit Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour l’envoi de lettres</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Email Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour les envois de lettres par courrier électronique</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Print Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour l’impression de lettres</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Custom Delivery Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle pour la livraison de lettres personnalisée</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Attachment documents parameter name</p> </td>
   <td><p>Nom de paramètre pour les documents en pièce jointe envoyés au post-processus</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>N’importe quel nom de variable de type chaîne</p> </td>
  </tr>
  <tr>
   <td><p>CM User Root</p> </td>
   <td><p>URL du dossier contenant tous les actifs utilisateur de Correspondence Management</p> </td>
   <td><p>—</p> </td>
   <td><p>Emplacement de dossier valide</p> </td>
  </tr>
  <tr>
   <td><p>Letter Cache Size</p> </td>
   <td><p>Spécifie le nombre maximal de lettres à conserver dans le cache.</p> <p>La modification de cette valeur entraînera le nettoyage du cache en  <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Toute valeur numérique</p> </td>
  </tr>
  <tr>
   <td><p>Enable Letter Cache</p> </td>
   <td><p>Active/désactive le cache de lettres.</p> <p>La modification de cette valeur entraînera le nettoyage du cache en   <code>in-memory </code> cache.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Data Elements Ordering</p> </td>
   <td><p>Conserve le même ordre des éléments de données dans l’interface de création de correspondance que dans la lettre</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Support Reload</p> </td>
   <td><p>Active/désactive la prise en charge du rechargement pour le rendu de lettres côté serveur.</p> <p>La désactivation améliore le rendu de lettres.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Dossier temp   </td>
   <td>Emplacement du dossier temporaire.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Remote Save</td>
   <td>Enregistre les instances de lettre sur l’auteur de traitement spécifique.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Compatibility Options</td>
   <td>Options de compatibilité du format configname:configvalue séparées par une virgule.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Debug Directory </p> <p> </p> </td>
   <td>Recherche du dossier du système de fichiers pour le débogage. Si le répertoire n’existe  <code>exists</code>, aucun fichier de vidage de débogage ne sera généré.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
