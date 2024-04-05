---
title: Personnalisation du suivi des événements de formulaire
description: Si une personne passe plus de 60 secondes sur un champ, un événement fieldvisit est déclenché et les détails du champ sont envoyés à Adobe SiteCatalyst.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 100%

---

# Personnalisation du suivi des événements de formulaire {#customizing-form-event-tracking}

Les événements suivants sont immédiatement suivis dans un formulaire adaptatif activé pour l’analyse :

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

Dans la configuration par défaut des formulaires AEM, si un utilisateur passe plus de 60 secondes sur un champ, un événement `fieldvisit` est déclenché et les détails du champ sont envoyés à Adobe Analytics. Vous pouvez personnaliser la ligne de base du suivi temporel des champs sous Configuration des rapports d’analyse AEM Forms dans la console de configuration AEM (/system/console/configMgr) afin d’augmenter ou de diminuer le délai d’expiration.

## Personnalisation des événements de suivi {#customizing-the-tracking-events}

Vous pouvez modifier la fonction `trackEvent` disponible dans le fichier `/libs/afanalytics/js/custom.js` afin de personnaliser le suivi des événements. Lorsqu’un événement en cours de suivi se produit dans un formulaire adaptatif, la fonction `trackEvent` est appelée. La fonction `trackEvent` accepte deux paramètres : `eventName` et `variableValueMap`.

Vous pouvez évaluer la valeur des arguments *eventName* et *variableValueMap* pour modifier le comportement du suivi des événements. Par exemple, vous pouvez choisir d’envoyer les informations au serveur d’analyse après un certain nombre d’événements d’erreur. Vous pouvez également choisir d’effectuer l’une des personnalisations suivantes :

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

Dans la configuration d’AEM Forms par défaut, toutes les 60 secondes, l’activité de la fenêtre contenant le formulaire adaptatif est vérifiée. Si la fenêtre est active, un événement `panelVisit` est déclenché dans Adobe Analytics. Cela permet de s’assurer que le document ou le formulaire est actif et de calculer la durée de consultation du formulaire ou du document correspondant.

>[!NOTE]
>
>Le nom d’événement utilisé pour contrôler l’activité et calculer la durée de la visite est « panelVisit ». Cet événement est différent de l’événement de visite de panneau répertorié dans le tableau ci-dessus.

Vous pouvez modifier la fonction scheduleHeartBeatCheck disponible dans le fichier `/libs/afanalytics/js/custom.js` pour modifier ou arrêter cet événement envoyé à Adobe Analytics à intervalles réguliers.
