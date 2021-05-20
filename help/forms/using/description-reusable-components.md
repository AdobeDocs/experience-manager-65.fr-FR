---
title: Description des composants réutilisables
seo-title: Description des composants réutilisables
description: Liste complète des composants réutilisables, avec les noms de fichier et les dépendances, pour vous permettre d’intégrer le composant espace de travail AEM Forms dans vos applications Web.
seo-description: Liste complète des composants réutilisables, avec les noms de fichier et les dépendances, pour vous permettre d’intégrer le composant espace de travail AEM Forms dans vos applications Web.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 88%

---

# Description des composants réutilisables {#description-of-reusable-components}

L’espace de travail AEM Forms est composé de [composants réutilisables](/help/forms/using/integrating-html-ws-components-web.md) organisés dans une [structure de dossiers](/help/forms/using/folder-structure.md) spécifique dans CRX™. Chaque composant possède des fichiers de modèle, de vue et de contrôleur à l’emplacement spécifié dans la structure de dossiers, des dépendances JavaScript™ à d’autres fichiers de composant, des événements écoutés par le composant et des objets JavaScript qui peuvent déclencher ces événements dans l’espace de travail AEM Forms. La liste complète des composants réutilisables avec leurs noms de fichier et leurs dépendances figure ici.

## TaskList {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>Tâche</p></li>
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle task</p></li>
     <li><p>Modèle teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>filterSelected – modèle tasklist</p></li>
     <li><p>remove – modèle tasklist</p></li>
     <li><p>updateQueue – modèle tasklist</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Ce composant peut être utilisé indépendamment de l’espace de travail AEM Forms, à condition de déclencher l’événement filterSelected pour ce composant depuis l’application personnalisée.

## Tâche {#task}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle tasklist</p></li>
     <li><p>Utilitaire taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>submitComplete – modèle task</p></li>
     <li><p>Reject – modèle task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace appelle la fonction fetchTasks du modèle TaskList afin de créer des modèles Task pour ce composant.

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>fetched – modèle tasklist </p></li>
     <li><p>remove – modèle tasklist </p></li>
     <li><p>updateQueue – modèle tasklist </p></li>
     <li><p>refreshedQueue – modèle tasklist </p></li>
     <li><p>filterSelected – modèle tasklist</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## Filtrer {#filter}

<table>
 <tbody>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td>
    <ul>
     <li><p>Field : queue : {name, qid, isDefault, type}</p> </li>
     <li><p>Field: query: string</p> </li>
     <li><p>Field: parentView: filterlist view</p> </li>
     <li><p>Field: parentModel: tasklist model</p> </li>
     <li><p>Field: utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Evénements écoutés</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>fetched – modèle tasklist </p></li>
     <li><p>remove – modèle tasklist </p></li>
     <li><p>updateQueue – modèle tasklist </p></li>
     <li><p>teamQueuesFetched – modèle tasklist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td>
    <ul>
     <li><p>Extends : filter view</p> </li>
     <li><p>Field : queue : {name, qid, isDefault, type }</p> </li>
     <li><p>Champ : query : string</p> </li>
     <li><p>Champ : parentView : vue filterlist</p> </li>
     <li><p>Champ : parentModel : modèle tasklist</p> </li>
     <li><p>Champ : utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Evénements écoutés</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter obtient l’événement indiquant quelle tâche a été sélectionnée du composant TaskList. Bien que ces composants partagent la même classe de modèle, il n’y a pas d’autre dépendance.

## TaskDetails {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>La plupart des classes d’utilitaires</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>Utilitaire formrendering</p> </li>
     <li><p>Utilitaire notes</p> </li>
     <li><p>Utilitaire attachments</p> </li>
     <li><p>Utilitaire taskactions</p> </li>
     <li><p>Utilitaire history</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>forwarded – modèle task</p> </li>
     <li><p>shared – modèle task</p> </li>
     <li><p>consulted – modèle task</p> </li>
     <li><p>rejected – modèle task</p> </li>
     <li><p>abandoned – modèle task</p> </li>
     <li><p>unlocked – modèle task</p> </li>
     <li><p>locked – modèle task</p> </li>
     <li><p>claimed – modèle task</p> </li>
     <li><p>change:taskselected – modèle tasklist</p> </li>
     <li><p>change:formUrl – modèle task</p> </li>
     <li>attachmentURLFetched - modèle task</li>
    </ul>
    <ul>
     <li>newAttachment - modèle task</li>
     <li><p>taskHistoryFetched – modèle task</p> </li>
     <li>prepareForSubmitComplete - modèle task</li>
     <li><p>submitComplete – modèle task</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>startprocess.html (dans le dossier route)</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>Catégorie</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle favoritecategoryfactory</p></li>
     <li><p>Modèle allcategoryfactory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched – modèle categorylist </p></li>
     <li><p>add – modèle categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ce composant utilise des classes de modèles de certains autres composants tels que StartPointList, StartPoint et Task. Hormis cette dépendance, CategoryList peut être utilisé indépendamment.

## Catégorie {#category}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle categorylist</p></li>
     <li><p>Modèle startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>changed - modèle category </p></li>
     <li><p>childrenFetched – modèle category </p></li>
     <li><p>category:selected – modèle categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>startprocess.html (dans le dossier route)</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle category</p></li>
     <li><p>Modèle favoritecategoryfactory</p></li>
     <li><p>Modèle allcategoryfactory</p></li>
     <li><p>Vue startpoint</p></li>
     <li><p>Modèle startpointlist</p></li>
     <li><p>Modèle startpoint</p></li>
     <li><p>Modèle task</p></li>
     <li><p>Modèle task</p></li>
     <li><p>Modèle tasklist</p></li>
     <li><p>Modèle teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>category:selected – modèle categorylist </p></li>
     <li><p>allStartpointsFetched – modèle categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>les composants StartPointList et CategoryList partagent la même classe de modèle. Le premier dépend donc du second. CategoryList accède aux informations sur la catégorie dont les points de départ sont affichés. Pour utiliser StartPointList indépendamment, simulez le déclencheur d’événement à partir de CategoryList.

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>Modèle task</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td><p>change – modèle startpoint </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td>
    <ul>
     <li><p>La plupart des classes d’utilitaires</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td>
    <ul>
     <li><p>Modèle category</p> </li>
     <li><p>Modèle favoritecategoryfactory</p> </li>
     <li><p>Modèle allcategoryfactory</p> </li>
     <li><p>Utilitaire formrendering</p> </li>
     <li><p>Utilitaire notes</p> </li>
     <li><p>Utilitaire attachments</p> </li>
     <li><p>Utilitaire taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>category:selected – modèle categorylist</p> </li>
     <li><p>change:invokedTask – modèle startpointlist</p> </li>
     <li><p>change:formUrl – modèle task</p> </li>
     <li><p>startpoint:selected – modèle startpointlist</p> </li>
     <li><p>forwarded – modèle task</p> </li>
     <li><p>abandoned – modèle task</p> </li>
     <li><p>unlocked – modèle task</p> </li>
     <li><p>locked – modèle task</p> </li>
     <li>attachmentURLFetched - modèle task</li>
     <li>newAttachment - modèle task</li>
     <li>prepareForSubmitComplete - modèle task </li>
     <li><p>submitComplete – modèle task</p> </li>
     <li><p>allStartpointsFetched – modèle categorylist</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>les composants StartPointList et StartProcess partagent la même classe de modèle. Ce composant devient pertinent lorsqu’un point de départ est sélectionné depuis StartPointList.

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tracking.html (dans le dossier route)</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>Modèle processname</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>add – modèle processnamelist </p></li>
     <li><p>fetched:processnames – modèle processnamelist </p></li>
     <li><p>change - modèle processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList ne dépend pas d’autres composants. Toutefois, en interne, il dépend de la classe de modèles ProcessInstanceList qui, elle, dépend d’autres composants. Par conséquent, ProcessNameList utilise de nombreuses classes de modèles telles que ProcessInstanceList, ProcessInstance, TaskList, Teamtask et Task. Hormis ces dépendances, ProcessNameList peut être utilisé indépendamment.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>processname (dans processnamelist.js)</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>Modèle processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td><p>change – modèle processname </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>tracking.html (dans le dossier route)</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>Modèle processname</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>processname:selected – modèle processnamelist </p></li>
     <li><p>processname:instancesfetched – modèle processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList attend un événement de ProcessNameList indiquant le nom du processus pour récupérer et afficher des instances. Pour utiliser ProcessInstanceList indépendamment, simulez le déclencheur d’événement séparément.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>processname dans processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>Modèle tasklist</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td><p>change – modèle processinstance </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td>
    <ul>
     <li><p>Modèle processname</p></li>
     <li><p>Utilitaire history</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>processname:selected – modèle processnamelist </p></li>
     <li><p>processinstance:selected – modèle processinstancelist </p></li>
     <li><p>tasksFetched – modèle processinstance </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory attend un événement de ProcessInstanceList concernant l’instance de processus dont l’historique doit être affiché. Hormis cette dépendance, le composant peut être utilisé indépendamment.

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>Vue usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched – modèle outofoffice</p> </li>
     <li><p>outOfOfficeSettingsSaved – modèle outofoffice</p> </li>
     <li><p>processesFetched – modèle outofoffice</p> </li>
     <li><p>principalSelected - vue principalsearch</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice peut être utilisé indépendamment.

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>Vue usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modèle sharequeue</p> </li>
     <li><p>queueAccessRequested - modèle sharequeue</p> </li>
     <li><p>grantedUsersFetched - modèle sharequeue</p> </li>
     <li>accessibleUsersFetched - modèle sharequeue</li>
     <li><p>queueAccessRevoked - modèle sharequeue</p> </li>
     <li><p>queueAccessRemoved - modèle sharequeue</p> </li>
     <li><p>principalSelected - vue principalsearch</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue peut être utilisé indépendamment.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched – modèle uisettings </p></li>
     <li><p>settingUpdated – modèle uisettings </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings peut être utilisé indépendamment.

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Evénements écoutés</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation peut être utilisé indépendamment.

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched – modèle userinfo</li>
     <li>sessionRenewed - modèle userinfo  <br /> </li>
     <li>sessionExpired - modèle userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo peut être utilisé indépendamment.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Mode</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Modèle</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p></td>
   <td><p>newWsError – modèle wserror </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modèle principalsearch</li>
     <li>outOfOfficeInfoFetched - modèle usersearch</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>searchtemplate (dans searchtemplatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td><p>templateFetched- modèle searchtemplate</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>tracking.html (dans le dossier route)</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td><p>modèle searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td><p>change - modèle searchtemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Mode</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modèle</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Nécessite les composants</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dépendances JS</p> </td>
   <td>NA<br /> </td>
  </tr>
  <tr>
   <td><p>Événements écoutés (Nom de l’événement - Déclencheur)</p> </td>
   <td><p>searchTemplate:selected - modèle searchtemplate</p> </td>
  </tr>
 </tbody>
</table>
