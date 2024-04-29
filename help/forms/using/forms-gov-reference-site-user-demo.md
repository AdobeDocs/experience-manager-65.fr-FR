---
title: Présentation du site de référence We.Gov et We.Finance
description: Utilisez des utilisateurs et des groupes fictifs pour exécuter des tâches AEM Forms à l’aide du package de démonstration We.Gov et We.Finance.
contentOwner: anujkapo
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '2478'
ht-degree: 100%

---

# Présentation du site de référence We.Gov et We.Finance {#we-gov-reference-site-walkthrough}

## Prérequis {#pre-requisites}

Configurez le site de référence comme décrit dans la section [Installation et configuration du site de référence We.Gov et We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Scénario utilisateur {#user-story}

* AEM Forms

   * Conversion de formulaires automatisée
   * Création
   * Modèles de données de formulaire/Sources de données

* AEM Forms

   * Capture de données
   * (Facultatif) Intégration de données (MS® Dynamics)
   * (Facultatif) Adobe Sign

* Workflow
* Notifications par e-mail
* (Facultatif) Communications client

   * Canal d’impression
   * Canal web

* Adobe Analytics
* Intégrations des sources de données

### Utilisateurs et groupes fictifs {#fictitious-users-and-groups}

Le package de démonstration We.Gov est fourni avec les utilisateurs fictifs intégrés suivants :

* **Aya Tan** : citoyenne éligible à un Service d’une agence gouvernementale

![Un utilisateur fictif](/help/forms/using/assets/aya_tan_new.png)

* **George Lang** : analyste commercial de l’agence We.Gov

![Un utilisateur fictif](/help/forms/using/assets/george_lang.png)

* **Camila Santos** : Responsable expérience client de l’agence We.Gov

![Un utilisateur fictif](/help/forms/using/assets/camila_santos.png)

Les groupes suivants sont également inclus :

* **Utilisateurs We.Gov Forms**

   * George Lang (membre)
   * Camila Santos (membre)

* **Utilisateurs We.Gov**

   * George Lang (membre)
   * Camila Santos (membre)
   * Aya Tan (membre)

### Légende des termes de présentation de démonstration {#demo-overview-terms-legend}

1. **Emprunter l’identité** : utilisateurs et groupes définis dans la démonstration d’AEM.
1. **Bouton** : rectangle coloré ou flèche entourée pour la navigation.
1. **Clic** : pour exécuter une action dans le scénario de l’utilisateur ou l’utilisatrice.
1. **Liens** : dans la partie supérieure du menu principal du site We.Gov.
1. **Instructions utilisateur** : ensemble d’étapes numériques à suivre lors de la navigation dans le scénario de l’utilisateur.
1. **Portail Forms** : *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Vue mobile** : utilisateur ou utilisatrice We.Gov pour répliquer une vue mobile avec un navigateur redimensionné.
1. **Vue ordinateur de bureau** : utilisateur de We.gov pour afficher une démonstration sur un ordinateur portable ou un ordinateur de bureau.
1. **Formulaire de pré-filtrage** : formulaire sur la page d’accueil du site We.Gov.
1. **Formulaire adaptatif** : formulaire de demande d’inscription pour la démonstration de We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Site Adobe We.Gov** : *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Boîte de réception Adobe** : dans la barre de menu supérieure, [Icône cloche](assets/bell.svg) du serveur principal d’AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Client de messagerie** : mode d’affichage préféré de vos courriers électroniques (Gmail, Outlook)
1. **CTA** : Call to action (appel à l’action)
1. **Naviguer** : pour localiser un point de référence spécifique sur la page du navigateur.
1. **AFC**: Automated Forms Conversion (conversion automatisée de formulaires)

## Automated Forms Conversion (Camila) {#automated-forms-conversion}

**La présente section** : Camila (Responsable de l’expérience client) dispose d’un formulaire basé un PDF existant qui a été utilisé dans le cadre d’un processus papier. Dans le cadre d’un effort de modernisation, Camila souhaite utiliser ce formulaire PDF pour créer automatiquement un nouveau formulaire adaptatif moderne.

### Automated Forms Conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Connectez-vous avec :
   * **Utilisateur** : camila.santos
   * **Mot de passe** : password
1. Dans la page principale, sélectionnez Formulaires > Formulaires et documents > Formulaires AEM Forms We.gov > AFC.
1. Camila télécharge le PDF vers AEM Forms.

   ![Télécharger le formulaire](assets/aftia-upload-form.jpg)

1. Camilla sélectionne ensuite le formulaire PDF et clique sur **Démarrer la conversion automatisée** pour lancer le processus de conversion. Vous devrez peut-être cliquer sur **Remplacer la conversion** si vous avez déjà converti le formulaire.

   >[!NOTE]
   >
   >Les paramètres d’AFC sont préconfigurés pour l’utilisateur final ou l’utilisatrice finale, ce qui signifie qu’ils ne doivent pas être modifiés.

   * **Facultatif** : si vous souhaitez utiliser le thème Ultramarine accessible, cliquez simplement sur le thème Spécifier un formulaire adaptatif et sélectionnez le thème Ultramarine accessible qui apparaît dans la liste des options.

   ![Démarrer la conversion](assets/aftia-start-conversion.jpg)

   ![Thème Ultramarine](assets/aftia-upload-conversion-settings.jpg)

   Le pourcentage de la barre de progression s’affiche pendant la conversion. Une fois l’état **Converti** affiché, cliquez sur le dossier **de sortie**, sélectionnez le formulaire adaptatif et cliquez sur **Modifier** pour ouvrir le formulaire converti.

1. Camilla examine ensuite le formulaire et s’assure que tous les champs sont présents

   ![Vérifier la conversion](assets/aftia-review-conversion.jpg)

1. Camilla commence ensuite à modifier le formulaire et sélectionne Panneau racine > Modifier (icône de clé à molette) > Onglets en haut dans le menu déroulant Disposition du panneau > la case à cocher.

   ![Propriétés de révision](assets/aftia-review-properties.jpg)

1. Camilla ajoute ensuite toutes les modifications de champ et CSS nécessaires pour générer le produit final.

   ![Ajouter CSS](assets/aftia-add-css.jpg)

### Modèle de données de formulaire et sources de données (Camila) {#data-sources}

**Cette section** : une fois le document converti et le formulaire adaptatif généré, Camila doit connecter le formulaire adaptatif à une source de données.

1. Camila ouvre les Propriétés sur le formulaire qui a été converti grâce à [Automated Forms Conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila sélectionne ensuite Modèle de formulaire, sélectionne le modèle de données de formulaire dans la liste déroulante Sélectionner parmi et sélectionne le modèle de données du formulaire d’inscription à We.gov dans la liste des options.

1. Cliquez sur Enregistrer et fermer.

   ![Sélection FDM](assets/aftia-select-fdm.jpg)

1. Camila clique sur le dossier **de sortie**, sélectionne le formulaire adaptatif et clique sur **Modifier** pour ouvrir le formulaire We.Gov complété.
1. Camila sélectionne un champ de formulaire adaptatif et clique sur l’![Icône Configurer](assets/configure-icon.svg) et crée une liaison avec les entités de modèle de données de formulaire à l’aide du champ **Référence de liaison**. Camila répète cette étape pour tous les champs du formulaire adaptatif.

### Test d’accessibilité des formulaires (Camila) {#form-accessibility-testing}

Camila confirme également que le contenu créé est construit correctement et entièrement accessible selon les standards de l’entreprise.

1. Camila clique sur le dossier **de sortie**, sélectionne le formulaire adaptatif et clique sur **Prévisualisation** pour ouvrir le formulaire We.Gov complété.

1. Ouvre l’onglet Audit dans l’outil Chrome Developer.

1. Exécute une vérification d’accessibilité afin de valider le formulaire adaptatif.

   ![Vérification de l’accessibilité](assets/aftia-accessibility.jpg)

## Démo d’affichage mobile de formulaire adaptatif (Aya) {#mobile-view-demo}

**Cette section doit être effectuée avant la démonstration.**

**Instructions utilisateur :**

1. Accédez à : *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Connectez-vous avec :

   1. **Utilisateur** : aya.tan
   1. **Mot de passe** : password

1. Redimensionnez la fenêtre du navigateur ou utilisez l’émulateur du navigateur pour répliquer la taille d’un appareil mobile.

### Site web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Un utilisateur fictif](/help/forms/using/assets/aya_tan_new-1.png)

**Cette section** : Aya est une citoyenne et a appris qu’elle peut recevoir un Service d’une agence gouvernementale. Aya accède au site web We.Gov à partir de son téléphone mobile pour en savoir plus sur les services auxquels elle est éligible.

### Présélection We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya répond à quelques questions pour confirmer son éligibilité en remplissant un court formulaire adaptatif sur son téléphone portable.

**Instructions utilisateur :**

1. Effectuez une sélection dans chaque champ de la liste déroulante.

   >[!NOTE]
   >
   >Si l’utilisateur ou l’utilisatrice gagne plus de 200 000 $ par an, il ou elle n’est pas éligible.

1. Cliquez sur « **Suis-je éligible ?** ».
1. Cliquez sur le bouton **Déposer une candidature maintenant** pour continuer.

   ![Lien Déposer une candidature maintenant](/help/forms/using/assets/apply_now_link.png)

### Formulaire adaptatif We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya découvre qu’elle est éligible et commence à remplir sa demande pour demander le service sur son appareil mobile.

Aya doit consulter certains documents à la maison avant de pouvoir remplir la demande de service. Elle enregistre et quitte l’application à partir de son appareil mobile.

**Instructions utilisateur :**

1. Renseignez les champs d’informations de base. Les champs et listes déroulantes suivants sont obligatoires :

   1. Informations de base

      1. Prénom
      1. Nom
      1. DDN
      1. E-mail

1. Utilisez la **logique dynamique** suivante pour démontrer la fonctionnalité dynamique à l’aide de la liste déroulante **Statut de la famille** :

   1. **Célibataire** : afficher le panneau des proches parents
   1. **Marié.e** : afficher le panneau relatif au mariage
   1. **Divorcé.e** : afficher le panneau des proches parents
   1. **Veuf.ve** : afficher le panneau des proches parents
   1. **Avez-vous des enfants ?** : bouton radio (Oui/Non) pour afficher le panneau des enfants à charge.

      1. Bouton (Ajouter/Supprimer) pour ajouter/supprimer plusieurs panneaux d’enfants à charge.

1. Cliquez sur la flèche droite dans la barre de menus grise.
1. Cliquez sur le bouton Enregistrer en bas de la page.

   ![Détails du formulaire adaptatif](/help/forms/using/assets/adaptive_form.png)

## Démonstration ordinateur de bureau {#desktop-demo}

**La présente section :** de retour à la maison, Aya a trouvé les informations dont elle avait besoin et reprend l’application depuis son ordinateur de bureau. Aya accède au portail Formulaires en ligne pour reprendre sa candidature. Avec une personnalisation simple, les agences peuvent également générer automatiquement et envoyer par courrier électronique un lien pour reprendre la demande de candidature.

### Suite du formulaire adaptatif (Aya) {#aya-user-story-continued-adaptive-form}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Dans la barre de navigation,sélectionnez **Services en ligne**.
1. Dans le panneau « Brouillons de formulaires », sélectionnez la « Demande d’inscription pour les prestations de santé » existante.

   ![Demande d’inscription aux prestations de santé](/help/forms/using/assets/enrollment_application.png)

   L’apparence est la même, et elle n’a pas besoin de saisir à nouveau des données.

   **Instructions utilisateur :**

1. Faites un clic droit sur Circle CTA pour passer à la section suivante.

   ![Right circle CTA](/help/forms/using/assets/right_circle_cta_new.png)

   Le formulaire est renseigné jusqu’au point de la dernière entrée d’Aya. Aya a saisi toutes ses informations et est prête à les envoyer.

   ![Envoyer le formulaire adaptatif](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Lorsqu’Aya remplit le champ du numéro de téléphone, elle doit le remplir sous la forme d’un nombre à 11 chiffres sans tirets, espaces ou traits d’union.

   Après l’envoi, Aya reçoit une page de remerciement. Aya peut également recevoir un e-mail qu’elle peut ouvrir pour signer électroniquement le document d’enregistrement avec Adobe Sign.

### Facultatif : Adobe Sign (Aya) {#adobe-sign}

**Instructions utilisateur :**

1. Accédez à votre client de messagerie électronique et recherchez l’adresse Adobe Sign.
1. Cliquez sur le lien vers Adobe Sign.

   ![Lien Adobe Sign](/help/forms/using/assets/adobe_sign_link.png)

**Instructions utilisateur :**

1. Cochez la case **J’accepte**.
1. Cliquez sur **Accepter**.
1. Faites défiler jusqu’en bas du document révisé.
1. Cliquez sur l’onglet jaune surligné pour signer le document.

   ![Signez le document](/help/forms/using/assets/sign_document_new.png) ![Signez le document test](/help/forms/using/assets/sign_test_document.png)

## Agent du gouvernement (George) {#government-agent-george}

![Agent du gouvernement George](/help/forms/using/assets/george_lang-1.png)

**Cette section :** George est un analyste des affaires de l’agence gouvernementale à qui Aya demande un service. George dispose d’un seul tableau de bord où il peut voir toutes les demandes de service qui lui ont été affectées pour révision.

### Boîte de réception AEM (George) {#george-user-story-aem-inbox}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l’icône de l’utilisateur ou de l’utilisatrice (coin supérieur droit) et utilisez l’option du menu **Se déconnecter** ou **Se faire passer pour** si vous êtes actuellement connecté avec un utilisateur administrateur ou une utilisatrice administratrice.

   1. Connectez-vous avec :

      1. **Utilisateur :** george.lang
      1. **Mot de passe :** password

   1. Ou empruntez l’identité :

      1. Saisissez `George` dans le champ **Se faire passer pour**.

      1. Cliquez sur OK pour emprunter l’identité.

1. Dans le coin supérieur droit, cliquez sur l’icône Notification (cloche).
1. Cliquez sur **Afficher tout** pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez la dernière tâche **Demande d’inscription aux prestations de santé**.

   ![Examen de la demande relative aux prestations de santé](/help/forms/using/assets/health_benefits.png)

### Facultatif : Boîte de réception AEM et MS® Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Grâce aux intégrations de données et aux workflows automatisés, la demande d’Aya apparaît, ainsi qu’un enregistrement CRM qui a été généré automatiquement lors de l’envoi des données.

**Instructions utilisateur :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur le bouton **Ouvrir MS® Dynamics** pour ouvrir l’enregistrement MS® Dynamics dans une nouvelle fenêtre.
1. Dans le CRM, vous voyez toutes les informations pouvant être mises à jour.

   1. Vous pouvez éventuellement ajouter des notes de révision directement dans Dynamics.

1. Fermez et revenez à la boîte de réception AEM.

   ![Enregistrement MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Retour à la boîte de réception d’AEM (George) {#george-user-story-back-to-aem-inbox}

George approuve la demande d’Aya et, grâce à un workflow automatisé existant, un e-mail de confirmation est également envoyé à Aya.

**Instructions utilisateur :**

1. Accédez au coin supérieur gauche et cliquez sur **Approuver** pour approuver la demande.
1. Dans la fenêtre modale, vous pouvez laisser un message pour le responsable Expérience Client.
1. Cliquez sur Terminé.
1. (Rôle citoyen) Ouvrez votre client de messagerie pour afficher l’e-mail envoyé à Aya.

   ![Affichez l’email envoyé à Aya](/help/forms/using/assets/email_client.png)

## Responsable Expérience Client (Camila) {#cx-lead-camila}

![Camila (Responsable Expérience Client)](/help/forms/using/assets/camila_santos-1.png)

**Cette section :** Camila, la responsable Expérience Client, a mis en place un appel téléphonique de bienvenue avec Aya pour lui expliquer comment utiliser les services administratifs pour lesquels elle a reçu l’autorisation de travailler.

### (Facultatif) Boîte de réception AEM et MS® Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l’icône de l’utilisateur ou de l’utilisatrice (coin supérieur droit) et utilisez l’option du menu **Se déconnecter** ou **Se faire passer pour** si vous êtes actuellement connecté avec un utilisateur administrateur ou une utilisatrice administratrice.

   1. Connectez-vous avec :

      1. **Utilisateur** : camila.santos
      1. **Mot de passe** : password

   1. Ou empruntez l’identité :

      1. Saisissez `Camila` dans le champ **Se faire passer pour**.

      1. Cliquez sur OK pour emprunter l’identité.

1. Dans le coin supérieur droit, cliquez sur l’icône Notification (cloche).
1. Cliquez sur **Afficher tout** pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez la dernière tâche **Nouvelle approbation de contact**.

![Nouvelle approbation de contact](/help/forms/using/assets/new_contact_approval.png)

**(Facultatif) Instructions d’utilisation :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur **Ouvrir MS® Dynamics** pour ouvrir l’enregistrement MS® Dynamics dans une nouvelle fenêtre.
1. Dans le CRM, vous pouvez voir toutes les informations pouvant être mises à jour.

   1. Vous pouvez éventuellement ajouter une nouvelle activité d’appel directement dans Dynamics.
   1. Ouvrez la section **Activités**.
   1. Cliquez sur **Nouvel appel téléphonique**.
   1. Ajoutez les détails de l’appel téléphonique.
   1. Enregistrez le fichier, puis fermez la fenêtre.

1. De retour dans AEM, accédez au coin supérieur gauche et cliquez sur **Envoyer** pour envoyer la demande.
1. Dans la fenêtre modale, vous pouvez laisser un message.
1. Cliquez sur Terminé.

   ![Onglet Activités](/help/forms/using/assets/activities_tab.png) ![Confirmer le nouveau contact](/help/forms/using/assets/confirm_new_contact.png)

## (Facultatif) Kit de bienvenue citoyen (Aya) {#welcome-kit-citizen-aya}

**Cette section :** Aya reçoit un courrier électronique contenant un lien vers une communication interactive qui résume ses avantages et inclut également des champs de formulaire à remplir. Une déclaration d’avantages au format PDF est jointe ainsi qu’un lien vers la lettre de communication interactive dans le courrier (avec le même thème/marque que la communication interactive).

### Notification client par courrier électronique (Aya) {#aya-user-story-email-client}

**Instructions d’utilisation :**

1. Recherchez et ouvrez le courrier électronique du kit de bienvenue.
1. Faites défiler la page jusqu’à la pièce jointe PDF.
1. Cliquez pour ouvrir la pièce jointe PDF.
1. Faites défiler l’écran vers le haut dans votre client de messagerie et cliquez sur **Afficher le kit de bienvenue en ligne**.

   1. Cette opération ouvre la version du canal web du même document.

1. Pour une référence rapide au PDF directement :

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Pour une référence rapide à IC directement :

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manuel des avantages de bienvenue](/help/forms/using/assets/welcome_benefits_handbook.png) ![Lien de communication interactive](/help/forms/using/assets/interactive_communication.png)

## Rappel de renouvellement citoyen (Aya) {#renewal-reminder-citizen-aya}

**Cette section :** Camila organise aussi un rappel de communication un an plus tard. (Étape de workflow qui automatise/exécute et envoie électroniquement).

### Notification client par courrier électronique (Aya) {#aya-user-story-email-client-updated}

**Instructions utilisateur :**

1. Accédez à votre client de messagerie.
1. Recherchez et ouvrez le courrier électronique Rappel de renouvellement.
1. Cliquez sur **Envoyer une nouvelle demande** pour ouvrir le formulaire adaptatif.

   1. Cette section est délibérément laissée vide pour prendre en charge le pré-remplissage de données lors de la phase 2.

   ![Courrier électronique de rappel de renouvellement](/help/forms/using/assets/renewal_reminder_email.png)

## (Facultatif) Modèle de données de formulaire (Camila) {#form-data-model}

**La présente section** : Camila accède aux intégrations de données AEM Forms où elle peut exécuter un test rapide pour vérifier que les informations envoyées à la source de données externe via l’intégration du modèle de données de formulaire sont bien présentes.

### Modèle de données de formulaire (Camila) {#form-data-model-camila}

**La présente section** : Camila accède à la page Sources de données pour valider les données que le serveur a répliquées dans la base de données Derby.

1. Une fois l’expérience client et l’envoi terminés, Camila accède à l’onglet Sources de données dans AEM Forms (**Formulaires** > **Intégrations de données**)

1. Camila sélectionne ensuite le FDM We.gov d’AEM Forms puis modifie le **FDM d’inscription We.gov**.

1. Camila sélectionne ensuite le **Contact** > **Service de lecture** à tester.

   ![Service de lecture des contacts](assets/aftia-contact-read-service.jpg)

1. Camila fournit ensuite au service de test un ID de contact, puis clique sur **Tester**. Par exemple 1 ou 2, si vous avez envoyé le formulaire. Si vous n’avez pas envoyé le formulaire, aucune donnée n’est renvoyée.

   ![Service de lecture des contacts](assets/aftia-test-service.jpg)

1. Camila peut ensuite vérifier que les données ont bien été insérées dans la source de données.

   * Les données du Derby DS ressemblent au format suivant :

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Facultatif) Analytics (Camila) {#analytics-cx-lead-camila}

**Cette section :** Camila accède à un tableau de bord où elle peut voir les KPI de l’administration, tels que le pourcentage de citoyens et citoyennes qui commencent à remplir un formulaire de demande de service et abandonnent, la durée moyenne de la soumission de la demande à la réponse d’approbation/refus, et les statistiques d’engagement pour les manuels de prestations envoyés.

### Rapports sur les sites Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Accédez à *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Sélectionnez le **Site We.Gov d’AEM Forms** pour afficher les pages du site.
1. Sélectionnez l’une des pages du site (par exemple Accueil), puis choisissez **Analytics et Recommendations**.

   ![Analytics et Recommandations](/help/forms/using/assets/analytics_recommendation.jpg)

1. Sur cette page, vous verrez les informations récupérées d’Adobe Analytics qui se rapportent à la page AEM Sites (REMARQUE : par conception, ces informations sont périodiquement actualisées à partir d’Adobe Analytics et ne s’affichent pas en temps réel).

   ![Mesures clés Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De retour sur la page vue (accessible à l’étape 3), vous pouvez également afficher les informations de la page vue en modifiant le paramètre d’affichage afin d’afficher les éléments dans la **Vue Liste**.
1. Recherchez le menu déroulant **Affichage** et sélectionnez **Vue Liste**.

   ![Vue Liste dans le menu déroulant Affichage](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Dans le même menu, sélectionnez **Paramètre d’affichage**, puis les colonnes que vous souhaitez afficher dans la section **Analytics**.

   ![Configurer l’affichage des colonnes](/help/forms/using/assets/view_setting_analytics.jpg)

1. Cliquez sur **Mettre à jour** pour rendre les nouvelles colonnes disponibles.

   ![Mettre de nouvelles colonnes à disposition](/help/forms/using/assets/new_columns_available.jpg)

### Rapports Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accédez à

   *https://&lt;serveur_AEM>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Sélectionnez le formulaire adaptatif **Demande d’inscription pour les prestations de santé** et sélectionnez le **Rapport Analytics**.

   ![Demande d’inscription pour les prestations de santé](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Patientez jusqu’au chargement de la page et affichez les données du rapport Analytics.

   ![Données du rapport Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
