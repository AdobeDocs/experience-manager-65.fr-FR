---
title: '« Tutoriel : tester votre formulaire adaptatif »'
seo-title: 'Tutorial: Testing your adaptive form'
description: Grâce aux tests automatisés, vous pouvez tester plusieurs formulaires adaptatifs en même temps.
seo-description: Use automated testing to test multiple adaptive forms at once.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: Adaptive Forms
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '951'
ht-degree: 100%

---

# Tutoriel : tester votre formulaire adaptatif {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

Une fois le formulaire adaptatif prêt, il est important de le tester avant de le déployer auprès des utilisateurs finaux. Vous pouvez choisir de tester manuellement (tests fonctionnels) chaque champ ou dʼautomatiser le test de votre formulaire adaptatif. Si vous disposez de plusieurs formulaires adaptatifs et que vous souhaitez tester chaque champ de tous les formulaires adaptatifs, vous devrez vous armer de courage.

AEM [!DNL Forms] propose un framework, Calvin, permettant dʼautomatiser les tests des formulaires adaptatifs. Grâce au framework, vous développez et exécutez des tests d’IU directement dans un navigateur Web. Ce framework fournit des API Javascript dédiés à la création de tests. Les tests automatisés vous permettent de tester le préremplissage ainsi que lʼenvoi d’un formulaire adaptatif, les règles d’expression, les validations, le chargement différé et les interactions avec l’interface utilisateur. Ce tutoriel vous guide tout au long des étapes nécessaires à la création et à l’exécution de tests automatisés sur un formulaire adaptatif. À la fin de ce didacticiel, vous serez capable de :

* [Créer une suite de tests pour votre formulaire adaptatif](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Créez des tests pour votre formulaire adaptatif.](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Exécutez la suite de tests et les tests créés pour votre formulaire adaptatif.](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Étape 1 : créer une suite de tests {#step-create-a-test-suite}

Les suites de tests comportent plusieurs cas de test. Il est possible de disposer de plusieurs suites de tests. Il est recommandé de disposer d’une suite de tests distincte pour chaque formulaire. Pour exécuter une suite de tests, procédez comme suit :

1. Connectez-vous à l’instance dʼauteur AEM [!DNL Forms] en tant qu’administrateur. Ouvrez [!UICONTROL CRXDE Lite]. Pour ouvrir CRXDE Lite, vous pouvez sélectionner le logo AEM > **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]** ou saisir lʼadresse [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) dans un navigateur.

1. Accédez à /etc/clientlibs dans [!UICONTROL CRXDE Lite]. Cliquez avec le bouton droit sur le sous-dossier /etc/clientlibs et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un nœud]**. Dans le champ **[!UICONTROL Nom]**, saisissez **WeRetailFormTestCases**. Sélectionnez le type comme **cq:ClientLibraryFolder**, puis cliquez sur **[!UICONTROL OK]**. afin de créer un nœud. Vous pouvez utiliser le nom de votre choix à la place de `WeRetailFormTestCases`.
1. Ajoutez les propriétés suivantes au nœud `WeRetailFormTestCases` et cliquez sur **[!UICONTROL Enregistrer TOUT]**.

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

   Veillez à ce que chaque propriété soit ajoutée dans une zone de texte distincte, comme illustré ci-dessous :

   ![dependencies](assets/dependencies.png)

1. Cliquez avec le bouton droit sur le nœud **[!UICONTROL WeRetailFormTestCases]** et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un fichier]**. Dans le champ **[!UICONTROL Nom]**, saisissez `js.txt`, puis cliquez sur **[!UICONTROL OK]**.
1. Ouvrez le fichier js.txt pour le modifier, saisissez le code suivant, puis enregistrez le fichier :

   ```text
   #base=.
    init.js
   ```

1. Créez un fichier nommé init.js dans le nœud `WeRetailFormTestCases`. Ajoutez le code ci-dessous au fichier et appuyez sur **[!UICONTROL Enregistrer tout]**.

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

   Le code ci-dessus crée une suite de tests nommée **We retail - Tests**.

1. Ouvrez l’interface utilisateur des tests dʼAEM (AEM > **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Tests]**). La suite de tests nommée **We retail - Tests** est répertoriée dans l’interface utilisateur.

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## Étape 2 : créer un cas de test pour préremplir des valeurs dans un formulaire adaptatif {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Un cas de test est un ensemble d’actions visant à tester une fonctionnalité spécifique. Par exemple, le préremplissage de tous les champs d’un formulaire et la validation de quelques champs pour sʼassurer que des valeurs correctes sont saisies.

Une action est une activité spécifique effectuée sur un formulaire adaptatif. Par exemple, un clic sur un bouton. Pour créer un cas de test et des actions permettant de valider la saisie de l’utilisateur pour chaque champ de formulaire adaptatif, procédez comme suit :

1. Dans [!UICONTROL CRXDE Lite], accédez au dossier `/content/forms/af/create-first-adaptive-form`. Cliquez avec le bouton droit sur le nœud du dossier **[!UICONTROL create-first-adaptive-form]** et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un fichier]**. Dans le champ **[!UICONTROL Nom]**, saisissez `prefill.xml`, puis cliquez sur **[!UICONTROL OK]**. Ajoutez le code suivant au fichier :

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

1. Accédez à `/etc/clientlibs`. Cliquez avec le bouton droit sur le sous-dossier `/etc/clientlibs` et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un nœud]**.

   Dans le champ **[!UICONTROL Nom]**, saisissez `WeRetailFormTests`. Sélectionnez le type `cq:ClientLibraryFolder` et cliquez sur **[!UICONTROL OK]**.

1. Ajoutez les propriétés suivantes au nœud **[!UICONTROL WeRetailFormTests]**.

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
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dependencies</td>
      <td>Chaîne</td>
      <td>Activé</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. Créez un fichier nommé js.txt dans le nœud **[!UICONTROL WeRetailFormTests]**. Ajoutez le suivant au fichier :

   ```shell
   #base=.
   prefillTest.js
   ```

   Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Créez un fichier nommé `prefillTest.js` dans le nœud **[!UICONTROL WeRetailFormTests]**. Ajoutez le code suivant au fichier : Le code permet de créer un cas de test. Le cas de test préremplit tous les champs d’un formulaire et en valide certains pour s’assurer que des valeurs correctes sont saisies.

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

   Le cas de test est créé et prêt à être exécuté. Les cas de test permettent de valider différents aspects dʼun formulaire adaptatif, comme la vérification de l’exécution du script de calcul, la validation des modèles et la validation du processus d’envoi d’un formulaire adaptatif. Pour plus d’informations sur les tests des différents aspects des formulaires adaptatifs, consultez la section Automatiser les tests des formulaires adaptatifs.

## Étape 3 : exécuter tous les tests dans une suite ou des cas de tests individuels {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Une suite de tests peut comporter plusieurs cas de test. Vous pouvez exécuter tous les cas de test dʼune suite de tests en même temps ou individuellement. Lorsque vous exécutez un test, les icônes indiquent les résultats :

* Une icône en forme de coche indique un test réussi : ![save_icon](assets/save_icon.svg)
* Une icône « X » indique l’échec d’un test : ![close-icon](assets/close-icon.svg).

1. Accédez à l’icône AEM > **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Tests]**.
1. Pour exécuter tous les tests de la suite de tests :

   1. Dans le panneau [!UICONTROL Tests], appuyez sur **[!UICONTROL We retail - Tests (1)]**. La suite se développe pour afficher la liste des tests.
   1. Appuyez sur le bouton **[!UICONTROL Exécuter les tests]**. La zone vierge sur le côté droit de l’écran est remplacée par un formulaire adaptatif lors de l’exécution du test.

      ![exécuter-tous-les--tests](assets/run-all-test.png)

1. Pour exécuter un seul test à partir de la suite de tests :

   1. Dans le panneau Tests, appuyez sur **[!UICONTROL We retail - Tests (1)]**. La suite se développe pour afficher la liste des tests.
   1. Appuyez sur le bouton **[!UICONTROL Test de préremplissage]** et sur **[!UICONTROL Exécuter les tests]**. La zone vierge sur le côté droit de l’écran est remplacée par un formulaire adaptatif lors de l’exécution du test.

1. Appuyez sur le nom du test, Test de préremplissage, pour examiner les résultats du cas de test. Cela ouvre le panneau des [!UICONTROL Résultats]. Appuyez sur le nom de votre cas de test dans le panneau des [!UICONTROL Résultats] pour afficher tous les détails du test.

   ![examiner-les-résultats](assets/review-results.png)

Le formulaire adaptatif est maintenant prêt pour la publication.
