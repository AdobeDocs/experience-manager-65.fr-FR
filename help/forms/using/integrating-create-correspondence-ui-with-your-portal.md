---
title: Intégration de l’interface utilisateur de création de correspondance dans votre portail personnalisé
seo-title: Intégration de l’interface utilisateur de création de correspondance dans votre portail personnalisé
description: Découvrez comment intégrer l’interface utilisateur de création de correspondance dans votre portail personnalisé
seo-description: Découvrez comment intégrer l’interface utilisateur de création de correspondance dans votre portail personnalisé
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 76%

---

# Intégration de l’interface utilisateur de création de correspondance dans votre portail personnalisé{#integrating-create-correspondence-ui-with-your-custom-portal}

## Présentation {#overview}

Cet article décrit la méthode d’intégration de la solution de création de correspondance dans votre environnement.

## Appel basé sur une URL {#url-based-invocation}

Il est possible d’appeler l’application de création de correspondance à partir d’un portail personnalisé en préparant une URL selon les paramètres de demande suivants :

* l’identifiant du modèle de lettre (à l’aide du paramètre cmLetterId).

* l’URL des données XML extraites à partir de la source de données sélectionnée (à l’aide du paramètre cmDataUrl).

Par exemple, le portail personnalisé prépare l’URL en tant que\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, qui peut être la balise href d’un lien sur le portail.

>[!NOTE]
>
>Cette manière d’appeler l’application n’est pas sûre, car les paramètres nécessaires sont transmis dans le cadre d’une demande GET et affichés (de façon clairement visible) dans l’URL.

>[!NOTE]
>
>Avant d’appeler l’application de création de correspondance, enregistrez et chargez les données d’appel de l’interface utilisateur de création de correspondance au niveau de l’URL de données requise. Cette opération peut être réalisée à partir du portail personnalisé ou à l’aide d’un autre processus différent d’arrière-plan.

## Appel inséré basé sur les données  {#inline-data-based-invocation}

Un autre moyen (plus sécurisé) d’appeler l’application de création de correspondance consiste à accéder simplement à l’URL https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html, tout en envoyant les paramètres et les données pour appeler l’application de création de correspondance en tant que demande de POST (en les cachant de l’utilisateur final). En outre, vous pouvez désormais transmettre les données XML à l’application de création de correspondance en mode POST (dans le cadre de la même demande à l’aide du paramètre cmData), ce qui n’était pas possible (ou idéal) dans l’approche précédente.

### Paramètres de définition de lettre  {#parameters-for-specifying-letter}

| **Nom** | **Type** | **Description** |
|---|---|---|
| cmLetterInstanceId | Chaîne | Identifiant de l’instance de lettre. |
| cmLetterId | Chaîne | Nom du modèle de lettre. |

L’ordre des paramètres du tableau indique la préférence de paramètres utilisés pour le chargement de la lettre.

### Paramètres de définition de la source de données XML  {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td> 
   <td><strong>Type</strong></td> 
   <td><strong>Description</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Données XML à partir d’un fichier source utilisant des protocoles de base, tels que cq, ftp, http ou file.<br />  </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Chaîne</td> 
   <td>Utilisation des données XML disponibles dans l’instance de lettre.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booléen</td> 
   <td>Pour réutiliser les données de test associées au dictionnaire de données.</td> 
  </tr>
 </tbody>
</table>

L’ordre des paramètres du tableau indique la préférence de paramètres utilisés pour le chargement des données XML.

### Autres paramètres {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td> 
   <td><strong>Type</strong></td> 
   <td><strong>Description</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booléen</td> 
   <td>Permet d’ouvrir la lettre en mode aperçu<br /> </td> 
  </tr>
  <tr>
   <td>Aléatoire</td> 
   <td>Horodatage</td> 
   <td>Pour résoudre les problèmes de mise en cache du navigateur.</td> 
  </tr>
 </tbody>
</table>

Si vous utilisez le protocole http ou cq pour cmDataURL, l’URL de http/cq doit être accessible de manière anonyme.
