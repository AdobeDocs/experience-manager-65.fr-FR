---
title: Personnalisation du suivi des événements de formulaire
seo-title: Personnalisation du suivi des événements de formulaire
description: Si un utilisateur passe plus de 60 secondes sur un champ, un événement fieldvisit est déclenché et les détails du champ sont envoyés à Adobe SiteCatalyst.
seo-description: Si un utilisateur passe plus de 60 secondes sur un champ, un événement fieldvisit est déclenché et les détails du champ sont envoyés à Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 77%

---


# Personnalisation du suivi des événements de formulaire {#customizing-form-event-tracking}

Les événements suivants sont immédiatement suivis dans un formulaire adaptatif activé par analyse :

<table>
 <tbody>
  <tr>
   <th>Événement</th>
   <th>Variables disponibles</th>
  </tr>
  <tr>
   <td>render</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>abandon</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>erreur</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>help</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## Personnalisation du délai d’événement de visite de champ {#customizing-the-field-visit-event-timeout}

Dans la configuration par défaut des formulaires AEM, si un utilisateur passe plus de 60 secondes sur un champ, un événement `fieldvisit` est déclenché et les détails du champ sont envoyés à Adobe Analytics. Vous pouvez personnaliser la Ligne de base de suivi du temps passé sur le champ sous Configuration des rapports d’analyse AEM Forms dans la console de configuration d’AEM (/system/console/configMgr) pour augmenter ou réduire la limite du délai.

## Personnalisation des événements de suivi {#customizing-the-tracking-events}

You can modify the `trackEvent`function available in `/libs/afanalytics/js/custom.js` file to customize the event tracking. Lorsqu’un événement en cours de suivi se produit dans un formulaire adaptatif, la fonction `trackEvent` est appelée. The `trackEvent` function accepts two parameters: `eventName`and `variableValueMap`.

You can evaluate value of *eventName* and *variableValueMap* arguments to change the tracking behavior of events. Vous pouvez, par exemple, choisir d’envoyer les informations au serveur d’analyse après un certain nombre d’événements d’erreur. Il est également possible d’exécuter l’une des personnalisations suivantes :

* Vous pouvez définir un temps limite avant l’envoi de l’événement.
* You can maintain a state to decide action, for example, *fieldVisit* pushes a dummy event based on the timestamp of the last event.
* Vous pouvez utiliser la fonction `pushEvent` pour envoyer l’événement au serveur d’analyse *.*

* Vous pouvez choisir de ne pas diffuser l’événement au serveur d’analyse.

### Échantillon {#sample}

In the following example, state for the *error* event of each *fieldName* attribute is maintained. L’événement n’est envoyé au serveur d’analyse que si une erreur se produit.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personnalisation de l’événement panelvisit {#customizing-the-panelvisit-event}

Dans la configuration d’AEM Forms par défaut, toutes les 60 secondes, l’activité de la fenêtre contenant le formulaire adaptatif est vérifiée. If the window is active, a `panelVisit`event is triggered to Adobe Analytics. Il permet d’assurer que le document ou le formulaire est actif et de calculer la durée de consultation du formulaire ou du document correspondant.

>[!NOTE]
>
>Le nom d’événement utilisé assurer l’activité et calculer la durée de consultation est « panelVisit ». Cet événement est différent de l’événement Visite de panneau répertorié dans le tableau ci-dessus.

You can modify the scheduleHeartBeatCheck function available in the `/libs/afanalytics/js/custom.js` file to change or stop this event sent to Adobe Analytics at a regular interval.
