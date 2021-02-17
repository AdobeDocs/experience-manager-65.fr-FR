---
title: Propriétés de configuration des communications interactives
seo-title: Propriétés de configuration de la communication interactive
description: Modifier les propriétés de configuration par défaut des communications interactives
seo-description: Modifier les propriétés de configuration par défaut des communications interactives
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 60%

---


# Propriétés de configuration des communications interactives{#interactive-communications-configuration-properties}

Les communications interactives incluent les propriétés qui sont configurées automatiquement après l’installation du package du [module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Les auteurs de la communication interactive peuvent modifier ces propriétés de configuration par défaut en utilisant la page de **configuration de la console web d’Adobe Experience Manager**.

Ouvrez la page **Configuration de la console Web de Adobe Experience Manager** à l’aide de l’URL suivante :

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Les propriétés de configuration incluent :

* [Configuration de fragments de document](#document-fragments-configuration)
* [Configuration de la création de correspondance](#create-correspondence-configuration)
* [Configuration de canal web du formulaire adaptatif et de la communication interactive](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuration des thèmes de canal web du formulaire adaptatif et de la communication interactive](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuration de fragments de document {#document-fragments-configuration}

Appuyez sur **Configuration des fragments de Document** dans la page **Configuration de la console Web de Adobe Experience Manager** pour vue les propriétés de configuration des fragments de document.

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Description</td> 
   <td>Valeur par défaut</td> 
   <td>Valeurs acceptables</td> 
  </tr> 
  <tr> 
   <td>Data Display Formats</td> 
   <td>Format d’affichage spécifique aux paramètres régionaux pour les champs, variables et éléments de modèle de données de formulaire disponibles lors de la création d’une communication interactive pour l’impression et les canaux Web.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR et ja_JP</li> 
     <li>dateFormat = jj-MM-aaaa</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Indentation</td> 
   <td>Largeur de l’unité unique de mise en retrait appliquée au texte dans des fragments de document de liste.</td> 
   <td>12,7 mm</td> 
   <td>Nombre</td> 
  </tr> 
  <tr> 
   <td>Roman Numbers Minimum Width</td> 
   <td>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de chiffres romains dans des fragments de document de liste. </td> 
   <td>12,7 mm</td> 
   <td>Nombre</td> 
  </tr> 
  <tr> 
   <td>Number Minimum Width</td> 
   <td>Largeur minimale à appliquer à la puce/au champ numérique lors de l’utilisation de listes numérotées à l’exception des chiffres romains dans des fragments de document de liste.</td> 
   <td>8,0 mm</td> 
   <td>Nombre</td> 
  </tr> 
 </tbody> 
</table>

## Configuration de la création de correspondance  {#create-correspondence-configuration}

Appuyez sur **Créer la configuration de correspondance** dans la page **Configuration de la console Web de Adobe Experience Manager** pour vue les propriétés de configuration de l&#39;interface utilisateur de l&#39;agent.

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
   <td>Cochez la case pour afficher le contenu résolu (valeurs réelles au lieu d’espaces réservés) lors de la modification du module de texte sur l’interface utilisateur de l’agent.</td> 
   <td>Non sélectionné</td> 
   <td>Non applicable</td> 
  </tr> 
  <tr> 
   <td>Appliquer un filigrane lors de l’aperçu</td> 
   <td>Cochez la case pour appliquer un filigrane au canal d’impression de la communication interactive en mode Aperçu.</td> 
   <td>Non sélectionné</td> 
   <td>Non applicable</td> 
  </tr> 
  <tr> 
   <td>Activer l’incorporation de polices dans le PDF</td> 
   <td><p>Cochez la case pour activer l’incorporation de polices dans les documents PDF. Après avoir sélectionné cette option, vous pouvez incorporer de nouvelles polices après avoir généré ou prévisualisé les documents PDF à l’aide de l’interface utilisateur de l’agent. Utilisez le canal d’impression de la communication interactive pour générer et prévisualisation des documents PDF.</p> <p>L’incorporation de polices dans un document PDF s’avère utile si une police est disponible sur un ordinateur utilisé pour générer le PDF et n’est pas disponible sur l’ordinateur client qui accède au PDF.</p> <p>Pour plus d’informations sur l’incorporation de polices, voir <a href="../../forms/using/customize-text-editor.md" target="_blank">Personnaliser l’éditeur de texte</a>.</p> </td> 
   <td>Non sélectionné</td> 
   <td>Ne s’applique pas</td> 
  </tr> 
 </tbody> 
</table>

## Configuration de canal web du formulaire adaptatif et de la communication interactive  {#adaptive-form-and-interactive-communication-web-channel-configuration}

Appuyez sur **Configuration du Canal Web de formulaire adaptatif et de communication interactive** dans la page **Configuration de la console Web de Adobe Experience Manager** pour vue les propriétés de configuration pour le canal Web Adaptive Forms and Interactive Communications. Le tableau suivant décrit les propriétés liées aux communications interactives :

| Propriété | Description | Valeur par défaut | Valeurs acceptables |
|---|---|---|---|
| Afficher l’espace réservé | Cochez la case pour activer l’affichage des espaces réservés pour les champs inclus dans les formulaires adaptatifs et les communications interactives. | Sélectionné | Non applicable |
| Nombre maximal d’entrées de cache | Définissez le nombre maximal de formulaires adaptatifs et de communications interactives pouvant être récupérés à l’aide de la mémoire cache. | 100 | Nombre |
| Rendre le nom de fichier unique | Cochez la case pour attribuer des noms uniques aux fichiers en tant que pièces jointes dans les formulaires adaptatifs et les communications interactives. | Non sélectionné | Ne s’applique pas |

## Configuration des thèmes de canal web du formulaire adaptatif et de la communication interactive  {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Appuyez sur **Configuration du thème du Canal Web de formulaire adaptatif et de communication interactive** dans la page **Configuration de la console Web de Adobe Experience Manager** pour vue les propriétés de configuration des thèmes de canal Web de Forms et de communications interactives.

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Description</td> 
   <td>Valeur par défaut</td> 
   <td>Valeurs acceptables</td> 
  </tr> 
  <tr> 
   <td>Nom de la liste de polices</td> 
   <td>Liste des polices pouvant être utilisées lors de la création de formulaires adaptatifs et de communications interactives.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial black</p> <p>Impact</p> <p>Palatino Linotype</p> </td> 
   <td>Toutes les polices valides du serveur Adobe</td> 
  </tr> 
 </tbody> 
</table>

