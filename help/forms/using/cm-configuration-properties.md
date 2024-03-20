---
title: Propriétés de configuration de Correspondence Management
description: Cette rubrique explique comment modifier Asset Composer avec des configurations propres à cette solution. Cette rubrique détaille les propriétés que vous pouvez modifier, avec leur description, leurs valeurs par défaut et leurs valeurs acceptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 100%

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
   <td>Mise en retrait sur les modules<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Largeur minimale (nombres)</td>
   <td>Largeur minimale à appliquer au champ de puce/nombre, lors de l’utilisation de listes numérotées, à l’exception des chiffres romains.</td>
   <td>8,0 mm</td>
   <td>N’importe quel nombre</td>
  </tr>
  <tr>
   <td><p>Largeur minimale (chiffres romains)</p> </td>
   <td><p>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de chiffres romains.</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td>Type de rendu</td>
   <td>Type de rendu que l’application de création de correspondance utilise pour restituer l’aperçu de lettre. </td>
   <td>Rendu HTML</td>
   <td>Rendu HTMLou rendu PDF.</td>
  </tr>
  <tr>
   <td><p>Activation de la surbrillance du PDF dans CCR</p> </td>
   <td><p>Active la surbrillance du PDF dans l’application de création de correspondance.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Type de surbrillance de la cible</p> </td>
   <td><p>Type de mise en surbrillance de la cible dans l’application de création de correspondance.</p> </td>
   <td><p>border</p> </td>
   <td><p>bord/remplissage/aucun</p> </td>
  </tr>
  <tr>
   <td><p>Couleur de surbrillance de la cible</p> </td>
   <td><p>Couleur de surbrillance de la cible dans l’application de création de correspondance.</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Type de surbrillance du contenu</p> </td>
   <td><p>Type de surbrillance du contenu dans l’application de création de correspondance.</p> </td>
   <td><p>Remplissage</p> </td>
   <td><p>bord/remplissage/aucun</p> </td>
  </tr>
  <tr>
   <td><p>Couleur de surbrillance du contenu</p> </td>
   <td><p>Couleur de surbrillance du contenu dans l’application de création de correspondance.</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Type de surbrillance du champ</p> </td>
   <td><p>Type de surbrillance du champ dans l’application de création de correspondance.</p> </td>
   <td><p>Remplissage</p> </td>
   <td><p>bord/remplissage/aucun</p> </td>
  </tr>
  <tr>
   <td><p>Couleur de surbrillance du champ</p> </td>
   <td><p>Couleur de surbrillance du champ dans l’application de création de correspondance.</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>N’importe quelle couleur RVB au format R;V;B</p> </td>
  </tr>
  <tr>
   <td><p>Délai d’expiration de l’application</p> </td>
   <td><p>Délai d’expiration de l’application en secondes.</p> </td>
   <td><p>1200</p> </td>
   <td><p>N’importe quel nombre</p> </td>
  </tr>
  <tr>
   <td><p>Nom de paramètre du document PDF</p> </td>
   <td><p>Nom de paramètre pour un document PDF en post-traitement.</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>N’importe quel nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Nom de paramètre de données XML</p> </td>
   <td><p>Nom de paramètre pour un document XML (données) en post-traitement.</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>N’importe quel nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Nom de paramètre du document XDP</p> </td>
   <td><p>Nom de paramètre pour un document XDP envoyé au post-traitement.</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>N’importe quel nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Nom de paramètre de l’URL de redirection</p> </td>
   <td><p>Nom de paramètre pour une URL de redirection envoyée depuis le post-traitement. Cette valeur peut être n’importe quel nom de variable de chaîne.</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>N’importe quel nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Type d’envoi de PDF</p> </td>
   <td><p>Type d’envoi de PDF (type de fichier PDF généré lors de l’envoi depuis l’application de création de correspondance).</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interactif/non interactif</p> </td>
  </tr>
  <tr>
   <td><p>Optimisation de l’instance du dictionnaire de données</p> </td>
   <td><p>Active le transfert de données optimisé de l’instance du dictionnaire de données entre le serveur et le client ou la cliente.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Auto Correct Inconsistencies </p> </td>
   <td><p>Lorsque cette propriété est activée, elle gère automatiquement les incohérences possibles dans les affectations de lettre.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Utilisation des formats de données configurés</p> </td>
   <td><p>Contrôle l’utilisation des formats de modification et d’affichage des données configurés.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Formats d’affichage des données</p> </td>
   <td><p>Spécifie le format d’affichage des données spécifique des paramètres régionaux.</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator= ; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>Format de modification des données</p> </td>
   <td><p>Format de modification des données. Cette propriété est utilisée lors de l’écriture de données en tant que chaîne ou de l’analyse des données à partir d’une chaîne.</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestion des instances de lettre lors de la publication</p> </td>
   <td><p>Active/désactive la fonctionnalité de gestion des lettres (applicable uniquement pour le serveur de publication).</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit</p> </td>
   <td><p>Active/désactive la fonctionnalité de contrôle. Lorsque cette propriété est définie sur false, les journaux d’audit de toutes les actions sont désactivés.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de lecture</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour les lectures de ressources.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de création</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour la création de ressources.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de mise à jour</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour la mise à jour de ressources.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de rétablissement</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour le rétablissement de ressources.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de publication</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour la publication de ressources.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit d’enregistrement en tant que brouillon</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour l’enregistrement des brouillons de lettre.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit d’envoi</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour l’envoi de lettres.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit d’e-mail</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour les envois de lettres par e-mail.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit d’impression</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour l’impression de lettres.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Activation de l’audit de diffusion personnalisée</p> </td>
   <td><p>Active/désactive la fonctionnalité d’audit pour la diffusion de lettres personnalisée.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Nom du paramètre de documents joints</p> </td>
   <td><p>Nom de paramètre pour les documents en pièce jointe envoyés au post-traitement.</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>N’importe quel nom de variable de chaîne</p> </td>
  </tr>
  <tr>
   <td><p>Racine de l’utilisateur CM</p> </td>
   <td><p>URL du dossier contenant toutes les ressources de l’utilisateur de Correspondence Management.</p> </td>
   <td><p>--</p> </td>
   <td><p>Emplacement de dossier valide</p> </td>
  </tr>
  <tr>
   <td><p>Taille du cache de lettres</p> </td>
   <td><p>Spécifie le nombre maximal de lettres à conserver dans le cache.</p> <p>La modification de cette valeur entraînera le nettoyage du cache <code>in-memory</code>.</p> </td>
   <td><p>100</p> </td>
   <td><p>N’importe quelle valeur numérique</p> </td>
  </tr>
  <tr>
   <td><p>Activation du cache de lettres</p> </td>
   <td><p>Active/désactive le cache de lettres.</p> <p>La modification de cette valeur entraînera le nettoyage du cache <code>in-memory </code>.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Commande des éléments de données</p> </td>
   <td><p>Conserve le même ordre des éléments de données dans l’interface de création de correspondance que dans la lettre.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Prise en charge du rechargement</p> </td>
   <td><p>Active/désactive la prise en charge du rechargement pour le rendu de lettres côté serveur.</p> <p>La désactivation améliore le rendu de lettres.</p> </td>
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
   <td>Enregistrement à distance</td>
   <td>Enregistre les instances de lettre sur l’auteur ou l’autrice de traitement spécifique.</td>
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
   <td>Recherche du dossier du système de fichiers pour le débogage. Si ce répertoire ne <code>exists</code> pas, aucun fichier de vidage de débogage ne sera généré.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
