---
title: Propriétés de configuration de Correspondence Management
description: Cette rubrique explique comment modifier Asset Composer avec des configurations spécifiques à une solution. Cette rubrique décrit les propriétés que vous pouvez modifier, avec leur description, leurs valeurs par défaut et leurs valeurs acceptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 13%

---

# Propriétés de configuration de Correspondence Management {#correspondence-management-configuration-properties}

Pour configurer ces propriétés, ouvrez l’URL suivante dans un navigateur : `https://<server>:<port>/<contextPath>/system/console/configMgr` et sélectionnez **Configurations de Correspondence Management**.

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
   <td><p>12.7mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Number Minimum Width</td>
   <td>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de listes numérotées à l’exception des chiffres romains</td>
   <td>8.0mm</td>
   <td>N’importe quel nombre</td>
  </tr>
  <tr>
   <td><p>Roman Numbers Minimum Width</p> </td>
   <td><p>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de chiffres romains</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Type de rendu</td>
   <td>Type de rendu utilisé par l’application de création de correspondance pour effectuer le rendu de l’aperçu de la lettre. </td>
   <td>Rendu du HTML</td>
   <td>Rendu du HTML / Rendu du PDF</td>
  </tr>
  <tr>
   <td><p>Activation de la mise en surbrillance du PDF CCR</p> </td>
   <td><p>Active la mise en surbrillance sur PDF dans l’application de création de correspondance</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Target Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance de la cible dans l’application de création de correspondance</p> </td>
   <td><p>border</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Target Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance de la cible dans l’application de création de correspondance</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>N’importe quelle couleur RGB au format R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Content Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance du contenu dans l’application de création de correspondance</p> </td>
   <td><p>Remplissage</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Content Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance du contenu dans l’application de création de correspondance</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RGB au format R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Field Highlight Type</p> </td>
   <td><p>Type de mise en surbrillance de champ dans l’application de création de correspondance</p> </td>
   <td><p>fill</p> </td>
   <td><p>border/fill/none</p> </td>
  </tr>
  <tr>
   <td><p>Field Highlight Color</p> </td>
   <td><p>Couleur de mise en surbrillance du champ dans l’application de création de correspondance</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RGB au format R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Application Time Out</p> </td>
   <td><p>Délai d’expiration de l’application en secondes</p> </td>
   <td><p>1200</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td><p>Nom du paramètre de document PDF</p> </td>
   <td><p>Nom de paramètre du document du PDF dans le post-processus</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Tout nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Nom du paramètre de données XML</p> </td>
   <td><p>Nom de paramètre pour le document XML (données) dans le post-processus</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Tout nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>XDP document parameter name</p> </td>
   <td><p>Nom de paramètre du document XDP envoyé au post-processus</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Tout nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Redirect URL parameter name</p> </td>
   <td><p>Nom de paramètre pour l’URL de redirection envoyée à partir du post-traitement Cette valeur peut être n’importe quel nom de variable de chaîne.</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Tout nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Type d’envoi du PDF</p> </td>
   <td><p>Type d’envoi du PDF (type de PDF généré lors de l’envoi à partir de la demande de création de correspondance)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interactif/non interactif</p> </td>
  </tr>
  <tr>
   <td><p>Optimisation de l’instance du dictionnaire de données</p> </td>
   <td><p>Active le transfert optimisé de l’instance du dictionnaire de données entre le serveur et le client</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Auto Correct Inconsistencies </p> </td>
   <td><p>Lorsque cette option est activée, elle gère automatiquement les incohérences possibles dans les affectations de lettre</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Utiliser les formats de données configurés</p> </td>
   <td><p>Contrôle l’utilisation des formats de modification et d’affichage des données configurés</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Formats d’affichage des données</p> </td>
   <td><p>Spécifie le format d’affichage des données spécifique aux paramètres régionaux.</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator= ; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyy; numberDecimalSeparator=,; numberGroupSeparator=; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Format de modification des données</p> </td>
   <td><p>Format de modification des données. Ceci est utilisé lors de l’écriture de données sous forme de chaîne ou de l’analyse de données à partir de chaîne.</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestion des instances de lettre lors de la publication</p> </td>
   <td><p>Active/désactive la fonctionnalité de gestion des lettres (applicable uniquement pour le serveur de publication)</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Enable Audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle. Si la valeur est false, les journaux d’audit de toutes les actions sont désactivés.</p> </td>
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
   <td><p>Active/désactive la fonctionnalité de contrôle pour la mise à jour des ressources</p> </td>
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
   <td><p>Active/désactive la fonctionnalité de contrôle pour les courriers électroniques</p> </td>
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
   <td><p>Active/désactive la fonctionnalité de contrôle pour la diffusion personnalisée de lettres</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Nom du paramètre de documents joints</p> </td>
   <td><p>Nom de paramètre pour les documents en pièce jointe envoyés au post-processus</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Tout nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Racine de l’utilisateur CM</p> </td>
   <td><p>URL du dossier contenant toutes les ressources de l’utilisateur de Correspondence Management.</p> </td>
   <td><p>--</p> </td>
   <td><p>Emplacement de dossier valide</p> </td>
  </tr>
  <tr>
   <td><p>Letter Cache Size</p> </td>
   <td><p>Indiquez le Nombre maximal de lettres à conserver en cache.</p> <p>La modification de cette valeur entraînera le nettoyage de la variable <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Toute valeur numérique</p> </td>
  </tr>
  <tr>
   <td><p>Enable Letter Cache</p> </td>
   <td><p>Active/désactive le cache de lettres.</p> <p>La modification de cette valeur entraînera le nettoyage de la variable <code>in-memory </code> cache.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Commande des éléments de données</p> </td>
   <td><p>Conserve l’ordre des éléments de données dans l’interface de création de correspondance selon leur ordre dans la lettre</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Support Reload</p> </td>
   <td><p>Activez/désactivez la prise en charge du rechargement dans les lettres rendues côté serveur.</p> <p>La désactivation de cette option améliore les performances de rendu de lettre.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Dossier temp </td>
   <td>Emplacement du dossier temporaire.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Remote Save</td>
   <td>Enregistre les instances de lettre sur l’auteur de traitement spécifié.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Options de compatibilité</td>
   <td>Options de compatibilité du format configname:configvalue séparées par une virgule.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Debug Directory </p> <p> </p> </td>
   <td>Emplacement du dossier du système de fichiers pour le débogage. Si le répertoire n’est pas <code>exists</code>, aucun fichier de vidage de débogage ne sera généré.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
