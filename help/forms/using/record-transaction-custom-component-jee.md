---
title: Enregistrez une transaction pour l’API de composant personnalisé pour AEM Forms on JEE.
description: Utilisez l’API TransactionRecorder pour enregistrer la transaction pour le composant personnalisé.
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Enregistrement d’une transaction pour les API de composant personnalisées pour AEM Forms on JEE {#record-a-transaction-for-custom-components}

Lorsque vous utilisez des API facturables dans votre composant personnalisé, vous pouvez activer la création de rapports de transactions pour le composant. Pour activer le reporting des transactions, modifiez la variable `component.xml` du composant et ajoutez la balise fournie ci-dessous sous l’opération pour laquelle la création de rapports de transaction doit être activée.

**Balise**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Ancienne balise d’opération | Nouvelle balise d’opération |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

S’il est nécessaire de capturer plusieurs transactions pour une API, par exemple dans le cas d’une API par lot où le nombre de transactions peut varier en fonction du nombre d’entrées, dans ces cas, vous devez gérer le nombre de transactions au niveau de l’API. Vous trouverez ci-dessous les étapes données pour enregistrer le nombre de transactions varié :

1. Import, classe `"com.adobe.idp.dsc.InvocationContextStack"` dans le code. La classe fait partie du `adobe-livecycle-client.jar` fichier sdk. Le fichier sdk est disponible à l’adresse `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Mettez à jour le fichier client partagé ci-dessus dans votre projet client avec le nouveau fichier au cas où il serait déjà regroupé.

1. Dans l’API pour laquelle différentes transactions doivent être consignées :
   1. Ajoutez une logique pour stocker le nombre de transactions dans une variable entière, telle que : `transaction_count`.
   1. Lorsque l’opération est réussie, ajoutez `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Articles connexes

* [Activation et affichage du rapport de transaction pour AEM Forms on JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Liste des API facturables pour AEM Forms on JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)


