---
title: '"Didacticiel : Test de votre formulaire adaptatif"'
seo-title: '"Didacticiel : Test de votre formulaire adaptatif"'
description: Utilisez les tests automatisés pour tester plusieurs formulaires adaptatifs à la fois.
seo-description: Utilisez les tests automatisés pour tester plusieurs formulaires adaptatifs à la fois.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 10%

---


# Didacticiel : Test de votre formulaire adaptatif {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

Une fois que le formulaire adaptatif est prêt, il est important de le tester avant de le déployer pour les utilisateurs finaux. Vous pouvez tester manuellement (des tests fonctionnels) chaque champ ou automatiser le test de votre formulaire adaptatif. Lorsque vous disposez de plusieurs formulaires adaptatifs, le test manuel de chaque champ de tous les formulaires adaptatifs devient une tâche intimidante.

AEM [!DNL Forms] fournit une structure de test, Calvin, pour automatiser les tests de vos formulaires adaptatifs. Grâce au framework, vous développez et exécutez des tests d’IU directement dans un navigateur Web. La structure fournit des API JavaScript pour la création de tests. Les tests automatisés vous permettent de tester l’expérience de préremplissage d’un formulaire adaptatif, d’envoyer l’expérience d’un formulaire adaptatif, les règles d’expression, depuis les validations, le chargement différé et les interactions de l’interface utilisateur. Ce didacticiel vous guide tout au long des étapes nécessaires pour créer et exécuter des tests automatisés sur un formulaire adaptatif. À la fin de ce didacticiel, vous serez capable de :

* [Créer une suite de tests pour votre formulaire adaptatif](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Création de tests pour votre formulaire adaptatif](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Exécutez la suite de tests et les tests créés pour votre formulaire adaptatif.](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Étape 1 : Créer une suite de tests {#step-create-a-test-suite}

Les suites de tests comportent un ensemble de cas de test. Vous pouvez avoir plusieurs suites de tests. Il est recommandé d’avoir une suite de tests distincte pour chaque formulaire. Pour créer une suite de tests :

1. Connectez-vous à l&#39;instance d&#39;auteur [!DNL Forms] AEM en tant qu&#39;administrateur. Ouvrez [!UICONTROL CRXDE Lite]. Vous pouvez appuyer sur AEM Logo > **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]** ou ouvrir l’URL [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) dans un navigateur pour ouvrir le CRXDE Lite.

1. Accédez à /etc/clientlibs dans [!UICONTROL CRXDE Lite]. Cliquez avec le bouton droit sur le sous-dossier /etc/clientlibs et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un nœud]**. Dans le champ **[!UICONTROL Name]**, saisissez **WeRetailFormTestCases**. Sélectionnez le type **cq:ClientLibraryFolder** et cliquez sur **[!UICONTROL OK]**. Il crée un noeud. Vous pouvez remplacer `WeRetailFormTestCases` par n’importe quel nom.
1. Ajoutez les propriétés suivantes sur le noeud `WeRetailFormTestCases` et appuyez sur **[!UICONTROL Enregistrer TOUT]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Propriété</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Multi</strong></td>
      <td><strong>Valeur</strong></td>
     </tr>
     <tr>
      <td>categories</td>
      <td>Chaîne</td>
      <td>Activé</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dependencies</td>
      <td>Chaîne</td>
      <td>Activé</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   Assurez-vous que chaque propriété est ajoutée à une zone distincte, comme indiqué ci-dessous :

   ![dependencies](assets/dependencies.png)

1. Cliquez avec le bouton droit sur le noeud **[!UICONTROL WeRetailFormTestCases]**, puis cliquez sur **[!UICONTROL Créer]** > **[!UICONTROL Créer un fichier]**. Dans le champ **[!UICONTROL Nom]**, saisissez `js.txt` et cliquez sur **[!UICONTROL OK]**.
1. Ouvrez le fichier js.txt pour le modifier, ajoutez le code suivant, puis enregistrez le fichier :

   ```text
   #base=.
    init.js
   ```

1. Créez un fichier, init.js, dans le `WeRetailFormTestCases`noeud. Ajoutez le code ci-dessous dans le fichier et appuyez sur **[!UICONTROL Enregistrer tout]**.

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   Le code ci-dessus crée une suite de tests nommée **Nous vendons au détail - Tests**.

1. Ouvrez l’interface utilisateur des tests AEM (AEM > **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Tests]**). La suite de tests - **Nous commercialisons - Tests** - est répertoriée dans l’interface utilisateur.

   ![we-commerce-détail-test-suite](assets/we-retail-test-suite.png)

## Étape 2 : Créez un cas de test pour préremplir des valeurs dans un formulaire adaptatif {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Un cas de test est un ensemble d’actions permettant de tester une fonctionnalité spécifique. Par exemple, le préremplissage de tous les champs d’un formulaire et la validation de quelques champs afin de s’assurer que les valeurs correctes sont saisies.

Une action est une activité spécifique sur un formulaire adaptatif, telle qu’un clic sur un bouton. Pour créer un cas de test et des actions permettant de valider les données utilisateur pour chaque champ de formulaire adaptatif :

1. Dans [!UICONTROL CRXDE Lite], accédez au dossier `/content/forms/af/create-first-adaptive-form`. Cliquez avec le bouton droit sur le noeud de dossier **[!UICONTROL create-first-adaptive-form]** et cliquez sur **[!UICONTROL Créer]** **[!UICONTROL Créer un fichier]**. Dans le champ **[!UICONTROL Nom]**, saisissez `prefill.xml` et cliquez sur **[!UICONTROL OK]**. Ajoutez le code suivant au fichier 

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. Accédez à `/etc/clientlibs`. Cliquez avec le bouton droit sur le sous-dossier `/etc/clientlibs` et cliquez sur **[!UICONTROL Créer]** **[!UICONTROL Créer un noeud]**.

   Dans le champ **[!UICONTROL Nom]**, saisissez `WeRetailFormTests`. Sélectionnez le type `cq:ClientLibraryFolder` et cliquez sur **[!UICONTROL OK]**.

1. Ajoutez les propriétés suivantes au noeud **[!UICONTROL WeRetailFormTests]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Propriété</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Multi</strong></td>
      <td><strong>Valeur</strong></td>
     </tr>
     <tr>
      <td>catégories</td>
      <td>Chaîne</td>
      <td>Activé</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dépendances</td>
      <td>Chaîne</td>
      <td>Activé</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. Créez un fichier, js.txt, dans le noeud **[!UICONTROL WeRetailFormTests]**. Ajoutez les éléments suivants dans le fichier :

   ```shell
   #base=.
   prefillTest.js
   ```

   Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Créez un fichier, `prefillTest.js`, dans le noeud **[!UICONTROL WeRetailFormTests]**. Ajoutez le code ci-dessous dans le fichier. Le code crée un cas de test. Le cas de test préremplit tous les champs d’un formulaire et valide certains champs pour s’assurer que les valeurs sont saisies correctement.

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   Le cas de test est créé et prêt à être exécuté. Vous pouvez créer des cas de test pour valider divers aspects d’un formulaire adaptatif, tels que la vérification de l’exécution du script de calcul, la validation de modèles et la validation de l’expérience d’envoi d’un formulaire adaptatif. Pour plus d’informations sur divers aspects du test des formulaires adaptatifs, voir Test automatisé des formulaires adaptatifs.

## Étape 3 : Exécuter tous les tests dans une suite ou des cas de tests individuels {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Une suite de tests peut comporter plusieurs cas de test. Vous pouvez exécuter tous les cas de test dans une suite de tests en une seule fois ou individuellement. Lorsque vous exécutez un test, les icônes indiquent les résultats :

* Une icône en forme de coche indique un test réussi : ![save_icon](assets/save_icon.svg)
* Une icône &quot;X&quot; indique un test qui a échoué : ![icône de fermeture](assets/close-icon.svg)

1. Accédez à l&#39;icône AEM > **[!UICONTROL Outils]** **[!UICONTROL Opérations&lt;a3/&quot;**[!UICONTROL  Tests ]**]**
1. Pour exécuter tous les tests de la suite de tests :

   1. Dans le panneau [!UICONTROL Tests], appuyez sur **[!UICONTROL Nous vendons au détail - Tests (1)]**. Il La suite se développe pour afficher la liste de test.
   1. Appuyez sur le bouton **[!UICONTROL Exécuter les tests]**. La zone vierge sur le côté droit de l’écran est remplacée par le formulaire adaptatif au fur et à mesure que le test s’exécute.

      ![exécution-tout-test](assets/run-all-test.png)

1. Pour exécuter un seul test à partir de la suite de tests :

   1. Dans le panneau Tests, appuyez sur **[!UICONTROL Nous vendons au détail - Tests (1)]**. Il La suite se développe pour afficher la liste de test.
   1. Appuyez sur **[!UICONTROL Test de préremplissage]** et sur le bouton **[!UICONTROL Exécuter les tests]**. La zone vierge sur le côté droit de l’écran est remplacée par le formulaire adaptatif au fur et à mesure que le test s’exécute.

1. Appuyez sur le nom du test, Test de préremplissage, pour examiner les résultats du test. Il ouvre le panneau [!UICONTROL Résultat]. Appuyez sur le nom de votre cas de test dans le panneau [!UICONTROL Résultat] pour vue tous les détails du test.

   ![révision-résultats](assets/review-results.png)

Désormais, le formulaire adaptatif est prêt pour la publication.
