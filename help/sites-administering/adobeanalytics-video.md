---
title: Configuration du suivi vidéo pour Adobe Analytics
seo-title: Configuration du suivi vidéo pour Adobe Analytics
description: Familiarisez-vous avec la configuration du suivi vidéo pour SiteCatalyst.
seo-description: Familiarisez-vous avec la configuration du suivi vidéo pour SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 43%

---

# Configuration du suivi vidéo pour Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Il existe différentes méthodes pour assurer le suivi des événements vidéo, dont deux sont des options héritées de versions précédentes d’Adobe Analytics. Ces options existantes sont : Jalons hérités et Secondes héritées.

>[!NOTE]
>
>Avant de poursuivre, assurez-vous qu’une **vidéo lisible** est chargée dans AEM.
>
>Pour vous assurer que vos vidéos sont lisibles dans la page, consultez **[ce didacticiel](/help/sites-authoring/default-components-foundation.md#video)** pour plus d’informations sur le transcodage de fichiers vidéo dans AEM.

Appliquez la procédure ci-dessous pour configurer une structure pour le suivi des vidéos à l’aide de chaque méthode.

>[!NOTE]
>
>Pour les nouvelles mises en œuvre, il est recommandé de **ne pas utiliser** les options héritées pour le suivi vidéo. Utilisez plutôt la méthode **Jalons**.

## Étapes communes {#common-steps}

1. Configurez une page web en faisant glisser un **composant vidéo** à partir du sidekick et en ajoutant une **vidéo comme ressource** lisible pour le composant.

1. [Créez une configuration et une structure Adobe Analytics](/help/sites-administering/adobeanalytics.md).

   * Les exemples des sections qui suivent utilisent le nom **my-sc-configuration** pour la configuration et **videofw** pour la structure.

1. Sur la page de structure, sélectionnez un RSID et définissez l’utilisation sur tous. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. Dans la catégorie Général du sidekick, faites glisser le composant vidéo dans la structure.
1. Sélectionnez une méthode de suivi :

   * [Jalons](/help/sites-administering/adobeanalytics.md)
   * [Jalons non hérités](/help/sites-administering/adobeanalytics.md)
   * [Jalons hérités](/help/sites-administering/adobeanalytics.md)
   * [Secondes héritées](/help/sites-administering/adobeanalytics.md)

1. Lorsque vous sélectionnez une méthode de suivi, la liste de variables CQ change en conséquence. Pour plus d’informations sur la configuration du composant et le mappage des variables CQ avec les propriétés Adobe Analytics, reportez-vous aux sections suivantes.

## Jalons {#milestones}

La méthode Jalons suit la plupart des informations sur la vidéo. Elle est hautement personnalisable et facile à configurer.

Pour utiliser la méthode Jalons, spécifiez les décalages de suivi temporels afin de définir les jalons. Lorsqu’une lecture vidéo franchit un jalon, la page appelle Adobe Analytics pour effectuer le suivi de l’événement. Pour chaque jalon que vous définissez, le composant crée une variable CQ que vous pouvez mapper à une propriété Adobe Analytics. Le format du nom de ces variables CQ est le suivant :

```shell
eventdata.events.milestoneXX
```

Le suffixe XX correspond au décalage de suivi, qui définit le jalon. Par exemple, la spécification des décalages de suivi de 4, 8, 16, 20 et 28 secondes génère les variables CQ suivantes :

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

Le tableau ci-dessous décrit les variables CQ par défaut fournies pour la méthode Jalons :

<table>
 <tbody>
  <tr>
   <th>Variables CQ</th>
   <th>Propriétés Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>Les variables mappées à cette propriété contiennent le nom <strong>convivial</strong> (<strong>Titre</strong>) de la vidéo s’il est défini dans la gestion des ressources numériques ; si cette valeur n’est pas définie, le <strong>nom de fichier</strong> de la vidéo sera envoyé à la place. Envoyée une seule fois, au début de la lecture d’une vidéo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Les variables mappées à cette propriété contiennent le nom du fichier. Envoyé uniquement avec eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Les variables mappées à cette propriété contiennent le chemin d’accès au fichier sur le serveur. Envoyé uniquement avec eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Envoyé chaque fois qu’un jalon de segment est franchi </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Envoyé chaque fois qu’un jalon est déclenché, le nombre de secondes passées par l’utilisateur à regarder le segment donné est également envoyé avec cet événement. par exemple, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Envoyé lors de l’initialisation de la vue vidéo</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Envoyé lorsque la lecture de la vidéo est terminée<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Envoyé lorsque le jalon donné est franchi, X correspond à la seconde où le jalon est déclenché à <br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Envoyé à chaque jalon ; apparaît en tant que pev3 dans l’appel Adobe Analytics, généralement envoyé en tant que "video"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Correspond exactement à eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contient des informations sur le segment qui a été consulté ; par exemple, 2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez définir le nom **convivial** d’une vidéo en ouvrant la vidéo pour modification dans la gestion des ressources numériques et en définissant le champ de métadonnées **Titre** sur le nom souhaité.

1. Après avoir sélectionné les jalons comme méthode de suivi, dans la boîte de dialogue des décalages de suivi, saisissez une liste de décalages de suivi, exprimés en secondes, séparés par des virgules. Par exemple, la valeur ci-dessous définit des jalons 4, 8, 16, 20 et 28 secondes après le début de la vidéo :

   ```xml
   4,8,16,20,24
   ```

   Les valeurs de décalage doivent être des entiers supérieurs à 0. La valeur par défaut est `10,25,50,75`.

1. Pour mapper les variables CQ aux propriétés Adobe Analytics, faites glisser les propriétés Adobe Analytics de ContentFinder en regard de la variable CQ sur le composant.

   Pour plus d’informations sur l’optimisation des mappages, consultez le guide [Mesure vidéo dans Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) .

1. [Ajoutez le ](/help/sites-administering/adobeanalytics.md) cadre à la page.
1. Pour tester la configuration en **mode Aperçu**, lisez la vidéo pour que les appels Adobe Analytics se déclenchent.

Les exemples de données de suivi Adobe Analytics suivants s’appliquent au suivi Milestone à l’aide des décalages de suivi de 4,8,16,20 et 24, ainsi que les mappages suivants pour les variables CQ :

<table>
 <tbody>
  <tr>
   <th>Variable CQ</th>
   <th>Propriété Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar 1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

Dans cet exemple, le composant Vidéo s’affiche comme suit dans la page de la structure :

![video1](assets/video1.png)

>[!NOTE]
>
>Pour voir les appels effectués vers Adobe Analytics, utilisez un outil approprié, tel que DigitalPulse Debugger ou Fiddler.

Les appels vers Adobe Analytics à l’aide de l’exemple fourni doivent ressembler à ceci lorsqu’ils sont affichés avec le DigitalPulse Debugger :

![chlimage_1-128](assets/chlimage_1-128.png)

*Il s’agit du **premier**appel effectué à Adobe Analytics contenant les valeurs suivantes :*

* *prop1 et eVar1 pour eventdata.a.media.name,*
* *props2-4, avec eVar2 et eVar3 contenant contentType (vidéo) et segment (1:O:1-4)*
* *event3 mappé à eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

***Troisième appel**vers Adobe Analytics :*

* *prop1 et eVar1 contiennent a.media.name ;*
* *event1 car un segment a été visionné ;* 
* *event2 envoyé avec un temps de lecture = 4 ;*
* *event11 envoyé car eventdata.events.milestone8 a été atteint ;* 
* *prop2 à 4 ne sont pas envoyés (car eventdata.events.a.media.view n’a pas été déclenché).* 

## Jalons non hérités {#non-legacy-milestones}

La méthode Jalons non hérités est similaire à la méthode Jalons, excepté que les jalons sont définis à l’aide de pourcentages de la durée du suivi. Les points communs sont les suivants :

* Lorsqu’une lecture vidéo franchit un jalon, la page appelle Adobe Analytics pour effectuer le suivi de l’événement.
* [ensemble statique de variables CQ](#cqvars) définies pour le mappage avec des propriétés Adobe Analytics.
* Pour chaque jalon que vous définissez, le composant crée une variable CQ que vous pouvez mapper à une propriété Adobe Analytics.

Le format du nom de ces variables CQ est le suivant :

Le suffixe XX correspond au pourcentage de la durée du suivi, qui définit le jalon. Par exemple, la spécification des pourcentages de 10, 25, 50 et 75 secondes génère les variables CQ suivantes :

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Après avoir sélectionné la méthode de suivi Jalons non hérités, dans la zone Décalage de suivi, saisissez une liste de pourcentages de durée du suivi séparés par des virgules. Par exemple, la valeur par défaut ci-dessous définit des jalons à 10 %, 25 %, 50 % et 75 % de la durée du suivi :

   ```xml
   10,25,50,75
   ```

   Les valeurs de décalage doivent être des entiers supérieurs à 0.

1. Pour mapper les variables CQ aux propriétés Adobe Analytics, faites glisser les propriétés Adobe Analytics de ContentFinder en regard de la variable CQ sur le composant.

   Pour plus d’informations sur l’optimisation des mappages, consultez le guide [Mesure vidéo dans Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) .

1. [Ajoutez le ](/help/sites-administering/adobeanalytics.md) cadre à la page.
1. Pour tester la configuration en **mode Aperçu**, lisez la vidéo pour que les appels Adobe Analytics se déclenchent.

## Jalons hérités {#legacy-milestones}

Cette méthode est similaire à la méthode Jalons, excepté que les jalons spécifiés dans le champ *Décalage de suivi* sont des pourcentages et non des points définis dans la vidéo.

>[!NOTE]
>
>Le champ Décalage de suivi accepte uniquement des nombres entiers compris entre 1 et 100, séparés par des virgules.

1. Définissez le décalage de suivi.

   * Par exemple, 10, 50, 75, 100

   En outre, les informations envoyées à Adobe Analytics sont moins personnalisables ; seules 3 variables sont disponibles pour le mappage :

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Les variables mappées à cette propriété contiennent le nom <strong>convivial</strong> (<strong>Titre</strong>) de la vidéo s’il est défini dans la gestion des ressources numériques ; si le titre n’est pas défini, le <strong>nom de fichier</strong> de la vidéo sera envoyé à la place. Envoyée une seule fois, au début de la lecture d’une vidéo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Les variables mappées à cette propriété contiennent le nom du fichier. Envoyée une seule fois, au début de la lecture d’une vidéo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable mappée à cette propriété contient le chemin d’accès au fichier sur le serveur. Envoyée une seule fois, au début de la lecture d’une vidéo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez définir le nom **convivial** d’une vidéo en ouvrant la vidéo pour modification dans la gestion des ressources numériques et en définissant le champ de métadonnées **Titre** sur le nom souhaité. Vous devez également enregistrer les modifications apportées une fois l’opération terminée.

1. Mappez ces variables aux variables props 1 à 3.

   Le **reste des informations** pertinentes dans l’appel sera envoyé concaténé dans la variable **one** nommée **pev3**.

   **Les exemples d’** appels vers Adobe Analytics à l’aide de l’exemple fourni doivent ressembler à ceci lorsqu’ils sont affichés avec DigitalPulse Debugger :

   ![lmilestones1](assets/lmilestones1.png)

   *La variable **pev3**envoyée dans l’appel contient les informations suivantes :*

   * *Nom*  : nom du fichier vidéo (*film.avi*).

   * *Longueur*  : durée du fichier vidéo, en secondes (*100*).

   * *Nom du lecteur*  : lecteur vidéo utilisé pour lire le fichier vidéo (*vidéo HTML5*)

   * *Total des secondes lues*  : nombre total de secondes pendant lesquelles la vidéo a été lue (*25*)

   * *Horodatage de début*  : horodatage qui identifie le moment auquel la lecture vidéo a commencé (*1331035567*)

   * *Session de lecture*  : détails de la session de lecture. Ce champ indique comment l’utilisateur a interagi avec la vidéo. Cela peut inclure des données telles que l’emplacement où ils ont commencé la lecture de la vidéo, s’ils ont utilisé le curseur vidéo pour avancer dans la vidéo et l’emplacement où ils ont arrêté la lecture de la vidéo (*L10E24S58L58 - la vidéo a été arrêtée à la seconde. 25 de la section L10, puis avance rapide jusqu’à la seconde 48*)

## Secondes héritées {#legacy-seconds}

Lors de l’utilisation de la méthode **secondes héritées**, les appels Adobe Analytics sont déclenchés toutes les N secondes, où N est spécifié dans le champ Décalage de suivi.

1. Définissez le décalage de suivi sur n’importe quel nombre de secondes,

   * Par exemple, 6.
   >[!NOTE]
   >
   >Le champ Décalage de suivi accepte uniquement des entiers supérieurs à 0.

   Les informations envoyées à Adobe Analytics sont moins personnalisables. Seules 3 variables sont disponibles pour le mappage :

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Les variables mappées à cette propriété contiennent le nom <strong>convivial</strong> (<strong>Titre</strong>) de la vidéo s’il est défini dans la gestion des ressources numériques ; si le titre n’est pas défini, le <strong>nom de fichier</strong> de la vidéo sera envoyé à la place. Envoyée une seule fois, au début de la lecture d’une vidéo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>La variable mappée à cette propriété contient le nom du fichier. Envoyée une seule fois, au début de la lecture d’une vidéo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable mappée à cette propriété contient le chemin d’accès au fichier sur le serveur. Envoyée une seule fois, au début de la lecture d’une vidéo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez définir le nom **convivial** d’une vidéo en ouvrant la vidéo pour modification dans la gestion des ressources numériques et en définissant le champ de métadonnées **Titre** sur le nom souhaité. Vous devez également enregistrer les modifications apportées une fois l’opération terminée.

1. Mappez ces variables à prop1, prop2 et prop3.

   Le **reste des informations pertinentes** dans l’appel sera envoyé sous forme concaténée dans **une** variable nommée **pev3**.

   Les appels vers Adobe Analytics à l’aide de l’exemple fourni doivent ressembler à ceci lorsqu’ils sont affichés avec le DigitalPulse Debugger :

   ![lseconds](assets/lseconds.png)

   *L’appel est similaire à l’appel Jalons hérités ci-dessus. Consultez les informations sur pev3 **[fournies ici](/help/sites-administering/adobeanalytics.md)**.*

**Références utilisées dans ce didacticiel :**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
