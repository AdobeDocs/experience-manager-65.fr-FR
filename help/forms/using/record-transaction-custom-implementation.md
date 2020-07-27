---
title: Enregistrer une transaction pour les implémentations personnalisées
seo-title: Enregistrer une transaction pour les implémentations personnalisées
description: Utilisez l'API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas comptabilisées comme des transactions
seo-description: Utilisez l'API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas comptabilisées comme des transactions
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Enregistrer une transaction pour les implémentations personnalisées {#record-a-transaction-for-custom-implementations}

Utilisez l&#39;API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas comptabilisées comme des transactions

Vous pouvez utiliser un code personnalisé pour envoyer un formulaire PDF, pour envoyer l’URL de prévisualisation de l’interface utilisateur de l’agent aux utilisateurs finaux afin de prévisualisation une communication interactive ou pour envoyer un formulaire à l’aide de méthodes personnalisées plutôt que d’utiliser des méthodes d’envoi fournies avec des AEM Forms. Toutes les actions mentionnées précédemment et les implémentations personnalisées des API AEM Forms ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API, [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), pour enregistrer des actions telles que des transactions.

Pour enregistrer une transaction, écrivez la servlet [sling](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) standard et appelez la servlet d&#39;un client pour enregistrer une transaction. Vous pouvez appeler la servlet à l’aide d’AJAX ou de toute autre méthode standard.

## Exemple de code côté serveur {#sample-server-sided-code}

Vous pouvez utiliser l’exemple de code ci-dessous pour exécuter l’API TransactionRecorder à partir d’une classe JAVA à l’aide d’un lot OSGi personnalisé.

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

Vous pouvez utiliser l’exemple de code ci-dessous pour appeler la servlet contenant l’ `TransactionRecorder`API.

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

## Related Articles {#related-articles}

* [Présentation des rapports sur les transactions](/help/forms/using/transaction-reports-overview.md)
* [Affichage et compréhension des rapports sur les transactions](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables des rapports de transaction](/help/forms/using/transaction-reports-billable-apis.md)

