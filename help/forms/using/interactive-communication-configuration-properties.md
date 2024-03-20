---
title: Propriétés de configuration des communications interactives
description: Modification des propriétés de configuration par défaut des communications interactives
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 48%

---

# Propriétés de configuration des communications interactives{#interactive-communications-configuration-properties}

Les communications interactives incluent les propriétés qui sont configurées automatiquement après l’installation du package du [module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Les auteurs de la communication interactive peuvent modifier ces propriétés de configuration par défaut en utilisant la page de **configuration de la console web d’Adobe Experience Manager**.

Ouvrez la page de **configuration de la console web d’Adobe Experience Manager** à l’aide de l’adresse suivante :

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Les propriétés de configuration incluent :

* [Configuration de fragments de document](#document-fragments-configuration)
* [Configuration de la création de correspondance](#create-correspondence-configuration)
* [Configuration de canal web du formulaire adaptatif et de la communication interactive](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuration des thèmes de canal web du formulaire adaptatif et de la communication interactive](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuration de fragments de document {#document-fragments-configuration}

Sélectionner **Configuration des fragments de document** sur le **Configuration de la console web Adobe Experience Manager** pour afficher les propriétés de configuration des fragments de document.

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Description</td> 
   <td>Valeur par défaut</td> 
   <td>Valeurs acceptables</td> 
  </tr> 
  <tr> 
   <td>Formats d’affichage des données</td> 
   <td>Format d’affichage spécifique aux paramètres régionaux pour les champs, variables et éléments de modèle de données de formulaire disponibles lors de la création d’une communication interactive pour les canaux d’impression et web.</td> 
   <td> 
    <ul> 
     <li>Paramètre régional = en_US, de_DE, fr_FR et ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>Indentation</td> 
   <td>Largeur d’une seule unité de mise en retrait appliquée au texte dans les fragments de document de liste.</td> 
   <td>12,7 mm</td> 
   <td>Nombre</td> 
  </tr> 
  <tr> 
   <td>Largeur minimale (chiffres romains)</td> 
   <td>Largeur minimale à appliquer à la puce ou au champ numérique lors de l’utilisation de chiffres romains dans des fragments de document de liste. </td> 
   <td>12,7 mm</td> 
   <td>Nombre</td> 
  </tr> 
  <tr> 
   <td>Largeur minimale (nombres)</td> 
   <td>Largeur minimale à appliquer à la puce ou au champ numérique lors de l’utilisation de listes numérotées à l’exception des chiffres romains dans des fragments de document de liste.</td> 
   <td>8,0 mm</td> 
   <td>Nombre</td> 
  </tr> 
 </tbody> 
</table>

## Configurer la création de correspondance {#create-correspondence-configuration}

Sélectionner **Configuration de la création de correspondance** sur le **Configuration de la console web Adobe Experience Manager** pour afficher les propriétés de configuration de l’interface utilisateur de l’agent.

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Description</td> 
   <td>Valeur par défaut</td> 
   <td>Valeurs acceptables</td> 
  </tr> 
  <tr> 
   <td>Afficher le contenu résolu pour modification</td> 
   <td>Cochez la case pour afficher le contenu résolu (valeurs réelles au lieu d’espaces réservés) lors de la modification du module de texte dans l’interface utilisateur de l’agent.</td> 
   <td>Non sélectionné</td> 
   <td>Non applicable</td> 
  </tr> 
  <tr> 
   <td>Application d’un filigrane pendant l’aperçu</td> 
   <td>Cochez la case pour appliquer un filigrane au canal d’impression de la communication interactive en mode Aperçu.</td> 
   <td>Non sélectionné</td> 
   <td>Non applicable</td> 
  </tr> 
  <tr> 
   <td>Activer l’incorporation de polices dans un document PDF</td> 
   <td><p>Cochez la case pour activer l’incorporation de polices dans les documents PDF. Après avoir sélectionné cette option, vous pouvez incorporer de nouvelles polices après avoir généré ou prévisualisé des documents PDF à l’aide de l’interface utilisateur de l’agent. Utilisez le canal d’impression de la communication interactive pour générer et prévisualiser des documents PDF.</p> <p>L’incorporation de polices dans un document PDF est utile lorsqu’une police est disponible sur l’ordinateur utilisé pour générer le document PDF et ne l’est pas sur l’ordinateur client qui accède au document PDF.</p> <p>Pour plus d’informations sur l’incorporation de polices, voir <a href="../../forms/using/customize-text-editor.md" target="_blank">Personnaliser l’éditeur de texte</a>.</p> </td> 
   <td>Non sélectionné</td> 
   <td>Non applicable</td> 
  </tr> 
 </tbody> 
</table>

## Configurer le canal web du formulaire adaptatif et de la communication interactive {#adaptive-form-and-interactive-communication-web-channel-configuration}

Sélectionner **Configuration du canal web du formulaire adaptatif et de la communication interactive** sur le **Configuration de la console web Adobe Experience Manager** pour afficher les propriétés de configuration du canal web Forms adaptatif et communications interactives. Le tableau suivant décrit les propriétés liées aux communications interactives :

| Propriété | Description | Valeur par défaut | Valeurs acceptables |
|---|---|---|---|
| Afficher l’espace réservé | Cochez la case pour activer l’affichage des espaces réservés pour les champs inclus dans les formulaires adaptatifs et les communications interactives. | Sélectionné | Non applicable |
| Entrées de cache maximales | Définissez le nombre maximal de formulaires adaptatifs et de communications interactives pouvant être récupérés à l’aide de la mémoire cache. | 100 | Nombre |
| Rendre le nom de fichier unique | Cochez la case pour que les noms des fichiers soient uniques en tant que pièces jointes dans le Forms adaptatif et les communications interactives. | Non sélectionné | Non applicable |

## Configurer les thèmes du canal web du formulaire adaptatif et de la communication interactive {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Sélectionner **Configuration du thème du canal web du formulaire adaptatif et de la communication interactive** sur le **Configuration de la console web Adobe Experience Manager** pour afficher les propriétés de configuration des thèmes de canal web Forms adaptatif et Communications interactives.

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Description</td> 
   <td>Valeur par défaut</td> 
   <td>Valeurs acceptables</td> 
  </tr> 
  <tr> 
   <td>Nom de la liste des polices</td> 
   <td>Liste des polices disponibles lors de la création de Forms adaptatif et de communications interactives.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial black</p> <p>Impact</p> <p>Palatino Linotype</p> </td> 
   <td>Toutes les polices de serveur d’Adobe valides</td> 
  </tr> 
 </tbody> 
</table>
