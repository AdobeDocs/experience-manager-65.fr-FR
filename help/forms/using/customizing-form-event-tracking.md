---
title: Personnalisation du suivi des événements de formulaire
seo-title: Customizing form event tracking
description: Si un utilisateur passe plus de 60 secondes sur un champ, un événement fieldvisit est déclenché et les détails du champ sont envoyés à Adobe SiteCatalyst.
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '446'
ht-degree: 100%

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

Vous pouvez modifier la fonction `trackEvent` disponible dans le fichier `/libs/afanalytics/js/custom.js` afin de personnaliser le suivi des événements. Lorsqu’un événement en cours de suivi se produit dans un formulaire adaptatif, la fonction `trackEvent` est appelée. La fonction `trackEvent` accepte deux paramètres : `eventName` et `variableValueMap`.

Vous pouvez évaluer la valeur des arguments *eventName* et *variableValueMap* pour modifier le comportement du suivi des événements. Vous pouvez, par exemple, choisir d’envoyer les informations au serveur d’analyse après un certain nombre d’événements d’erreur. Il est également possible d’exécuter l’une des personnalisations suivantes :

* Vous pouvez définir un temps limite avant l’envoi de l’événement.
* Vous pouvez conserver un état afin de déterminer l’action à entreprendre, par exemple *fieldVisit* diffuse un événement factice en fonction de la date et de l’heure du dernier événement.
* Vous pouvez utiliser la fonction `pushEvent` pour envoyer l’événement au serveur d’analyse *.*

* Vous pouvez choisir de ne pas diffuser l’événement au serveur d’analyse.

### Échantillon {#sample}

Dans l’exemple suivant, l’état de l’événement *error* de chaque attribut *fieldName* est conservé. L’événement n’est envoyé au serveur d’analyse que si une erreur se produit.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personnalisation de l’événement panelvisit {#customizing-the-panelvisit-event}

Dans la configuration d’AEM Forms par défaut, toutes les 60 secondes, l’activité de la fenêtre contenant le formulaire adaptatif est vérifiée. Si la fenêtre est active, un événement `panelVisit` est déclenché dans Adobe Analytics. Il permet d’assurer que le document ou le formulaire est actif et de calculer la durée de consultation du formulaire ou du document correspondant.

>[!NOTE]
>
>Le nom d’événement utilisé assurer l’activité et calculer la durée de consultation est « panelVisit ». Cet événement est différent de l’événement Visite de panneau répertorié dans le tableau ci-dessus.

Vous pouvez modifier la fonction scheduleHeartBeatCheck disponible dans le fichier `/libs/afanalytics/js/custom.js` pour modifier ou arrêter cet événement envoyé à Adobe Analytics à intervalles réguliers.
