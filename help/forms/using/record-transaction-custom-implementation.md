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
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 100%

---

# Enregistrer une transaction pour les implémentations personnalisées pour AEM Forms sur OSGi {#record-a-transaction-for-custom-implementations}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/record-transaction-custom-implementation) |
| AEM 6.5 | Cet article |

Utilisez l’API TransactionRecorder pour enregistrer automatiquement les actions qui ne sont pas automatiquement comptabilisées comme des transactions

Vous pouvez utiliser du code personnalisé pour envoyer un formulaire PDF ou pour envoyer aux utilisateurs finaux et utilisatrices finales une URL d’aperçu de l’interface utilisateur de l’agent afin de prévisualiser une communication interactive. Vous pouvez également envoyer un formulaire à l’aide de méthodes personnalisées au lieu d’utiliser des méthodes d’envoi fournies avec AEM Forms. Toutes les actions mentionnées précédemment et les implémentations personnalisées des API AEM Forms ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API, [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html?lang=fr), pour enregistrer de telles actions en tant que transactions.

Pour enregistrer une transaction, écrivez le [servlet sling standard](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=fr) et appelez le servlet d’un client pour enregistrer une transaction. Vous pouvez appeler le servlet à l’aide d’AJAX ou de toute autre méthode standard.

## Exemple de code côté serveur {#sample-server-sided-code}

Vous pouvez utiliser l’exemple de code ci-dessous pour exécuter l’API TransactionRecorder à partir d’une classe Java™ à l’aide d’un lot OSGi personnalisé.

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
