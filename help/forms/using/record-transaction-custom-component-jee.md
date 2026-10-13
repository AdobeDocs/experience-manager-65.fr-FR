---
title: Enregistrement d’une transaction de l’API de composant personnalisé pour AEM Forms sur JEE
description: Découvrez comment utiliser l’API TransactionRecorder pour enregistrer les transactions d’un composant personnalisé.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: bcb3e79d-a57e-59a4-ad50-e03803c9f153
    internal-label: Transaction Reports
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%
---
# Enregistrement d’une transaction pour les API de composant personnalisées pour AEM Forms sur OSGi {#record-a-transaction-for-custom-components}

Lorsque vous utilisez des API facturables dans votre composant personnalisé, vous pouvez activer le reporting des transactions pour le composant. Pour activer la création de rapports de transactions, modifiez le fichier `component.xml` du composant et ajoutez la balise donnée ci-dessous sous l’opération pour laquelle la création de rapports de transactions doit être activée.

**Balise** : `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Ancienne balise d’opération | Nouvelle balise d’opération |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Si vous devez capturer plusieurs transactions pour une API, par exemple une API par lot où le nombre de transactions varie en fonction du nombre d’entrées, gérez le nombre de transactions au niveau de l’API.

**Pour enregistrer le nombre des différentes transactions, procédez comme suit :**

1. Importez la classe `"com.adobe.idp.dsc.InvocationContextStack"` dans le code. La classe fait partie du fichier sdk `adobe-livecycle-client.jar`. Le fichier sdk est disponible dans `<AEM_Forms_JEE_Install>\sdk\client-libs\common`.

   >[!NOTE]
   > Mettez à jour le fichier client partagé ci-dessus dans votre projet client avec le nouveau fichier au cas où il serait déjà regroupé.

1. Dans l’API pour laquelle différentes transactions doivent être consignées, procédez comme suit :
   1. Ajoutez une logique afin de pouvoir stocker le nombre de transactions dans une variable entière, telle que `transaction_count`.
   1. Une fois l’opération réussie, ajoutez `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--
For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.
-->

## Articles connexes

* [Activation et affichage des rapports de transaction pour AEM Forms sur JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Liste des API facturables pour AEM Forms sur JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
