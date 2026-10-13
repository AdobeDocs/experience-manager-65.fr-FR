---
title: Enregistrer une transaction pour les implémentations personnalisées
description: Utilisez l’API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas automatiquement comptabilisées comme des transactions.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
feature: Transaction Reports
exl-id: b0c4f72a-e65f-453a-af66-5d9f98a9d6df
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
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
source-wordcount: '286'
ht-degree: 94%
---
# Enregistrer une transaction pour les implémentations personnalisées pour AEM Forms sur OSGi {#record-a-transaction-for-custom-implementations}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquer ici](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/record-transaction-custom-implementation) |
| AEM 6.5 | Cet article |

Utilisez l’API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas automatiquement comptabilisées comme des transactions

Vous pouvez utiliser du code personnalisé pour envoyer un formulaire PDF ou pour envoyer aux utilisateurs finaux et utilisatrices finales une URL d’aperçu de l’interface utilisateur de l’agent afin de prévisualiser une communication interactive. Vous pouvez également envoyer un formulaire à l’aide de méthodes personnalisées au lieu d’utiliser des méthodes d’envoi fournies avec AEM Forms. Toutes les actions mentionnées précédemment et les implémentations personnalisées des API AEM Forms ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API, [TransactionRecorder](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), pour enregistrer de telles actions en tant que transactions.

Pour enregistrer une transaction, écrivez le [servlet sling standard](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=fr) et appelez le servlet d’un client pour enregistrer une transaction. Vous pouvez appeler le servlet à l’aide d’AJAX ou de toute autre méthode standard.

## Exemple de code côté serveur {#sample-server-sided-code}

Vous pouvez utiliser l’exemple de code ci-dessous pour exécuter l’API TransactionRecorder à partir d’une classe Java™ à l’aide d’un bundle OSGi personnalisé.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Exemple de code côté client {#sample-client-side-code}

Vous pouvez utiliser l’exemple de code ci-dessous pour appeler la servlet qui contient l’API `TransactionRecorder`.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Articles connexes {#related-articles}

* [Vue d’ensemble des rapports de transaction pour AEM Forms sur OSGi](/help/forms/using/transaction-reports-overview.md)
* [Afficher et comprendre les rapports de transaction pour AEM Forms sur OSGi](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables pour les rapports de transaction pour AEM Forms sur OSGi](/help/forms/using/transaction-reports-billable-apis.md)
