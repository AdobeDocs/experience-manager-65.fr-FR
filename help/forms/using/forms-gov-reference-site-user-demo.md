---
title: Présentation du site de référence We.Gov et We.Finance
seo-title: Présentation du site de référence We.Gov et We.Finance
description: Utilisez des utilisateurs et des groupes fictifs pour exécuter des tâches AEM Forms à l’aide du module de démonstration We.Gov et We.Finance.
seo-description: Utilisez des utilisateurs et des groupes fictifs pour exécuter des tâches AEM Forms à l’aide du module de démonstration We.Gov et We.Finance.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---

# Présentation du site de référence We.Gov et We.Finance {#we-gov-reference-site-walkthrough}

## Prérequis {#pre-requisites}

Configurez le site de référence comme décrit dans [Configuration du site de référence We.Gov et We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## User Story {#user-story}

* AEM Forms

   * Conversion de formulaires automatisée
   * Création  
   * Modèles de données de formulaire/sources de données

* AEM Forms

   * Capture de données
   * (Facultatif) Intégration de données (MS Dynamics)
   * (Facultatif) Adobe Sign

* Workflow
* Notifications par e-mail
* (Facultatif) Communications client

   * Canal d’impression
   * Canal web

* Adobe Analytics
* Intégrations des sources de données

### Utilisateurs et groupes fictifs {#fictitious-users-and-groups}

Le module de démonstration We.Gov est fourni avec les utilisateurs fictifs intégrés suivants :

* **Aya Tan** : Citoyen éligible à un Service d&#39;une agence gouvernementale

![Un utilisateur fictif](/help/forms/using/assets/aya_tan_new.png)

* **George Lang** : Analyste commercial de l’agence We.Gov

![Un utilisateur fictif](/help/forms/using/assets/george_lang.png)

* **Camila Santos** : Plomb CX de l’agence We.Gov

![Un utilisateur fictif](/help/forms/using/assets/camila_santos.png)

Les groupes suivants sont également inclus :

* **Utilisateurs de Forms We.Gov**

   * George Lang (membre)
   * Camila Santos (membre)

* **Utilisateurs de We.Gov**

   * George Lang (membre)
   * Camila Santos (membre)
   * Aya Tan (membre)

### Légende des termes de présentation de démonstration {#demo-overview-terms-legend}

1. **Emprunter l’identité** : Utilisateurs et groupes définis dans AEM démonstration.
1. **Bouton** : Rectangle coloré ou flèche entourée pour la navigation.
1. **Cliquez sur** : Pour exécuter une action dans l’article de l’utilisateur.
1. **Liens** : Situé dans la partie supérieure du menu principal du site We.Gov.
1. **Instructions** utilisateur : Ensemble d’étapes numériques à suivre lors de la navigation dans l’histoire de l’utilisateur.
1. **Portail Forms** :  *https://&lt;aemserver> : &lt;port>/content/we-gov/formsportal.html*
1. **Vue mobile** : utilisateur We.Gov pour répliquer une vue mobile avec un navigateur redimensionné.
1. **Vue Bureau** : Utilisateur de We.gov pour afficher une démonstration sur un ordinateur portable ou un ordinateur de bureau.
1. **Formulaire de pré-filtrage** : Formulaire sur la page d’accueil du site We.Gov.
1. **Formulaire** adaptatif : Formulaire de demande d’inscription pour la démonstration de We.gov.

   *https://&lt;aemserver> : &lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe du site We.Gov** :  *https://&lt;aemserver> : &lt;port>/content/we-gov/home.html*
1. **Boîte de réception d’Adobe** : Icône de la barre de menu supérieure  [Bell ](assets/bell.svg) dans AEM arrière-plan.

   *https://&lt;aemserver> : &lt;port>/aem/start.html*

1. **Client de messagerie** : Mode d’affichage préféré de vos emails (Gmail, Outlook)
1. **CTA** : Appel à l’action
1. **Naviguez** : Pour localiser un point de référence spécifique sur la page du navigateur.
1. **AFC** : automated forms conversion

## automated forms conversion (Camila) {#automated-forms-conversion}

**Cette section** : Camila the CX Lead dispose d’un formulaire PDF existant qui a été utilisé dans le cadre d’un processus papier. Dans le cadre d’un effort de modernisation, elle souhaite utiliser ce formulaire PDF pour créer automatiquement un nouveau Forms adaptatif moderne.

### automated forms conversion - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Connectez-vous avec :
   * **Utilisateur** : camila.santos
   * **Mot de passe** : password
1. Dans la page principale, sélectionnez Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila télécharge le PDF dans AEM Forms.

   ![Télécharger le formulaire](assets/aftia-upload-form.jpg)

1. Camilla sélectionne ensuite le formulaire PDF et clique sur **Démarrer la conversion automatisée** pour lancer le processus de conversion. Vous devrez peut-être cliquer sur **Remplacer la conversion** si vous avez converti le formulaire.

   >[!NOTE]
   >
   >Notez que les paramètres d’AFC sont préconfigurés pour l’utilisateur final, ce qui signifie qu’ils ne doivent pas être modifiés.

   * **Facultatif** : Si vous souhaitez utiliser le thème Ultramarine accessible, cliquez simplement sur le thème Spécifier un formulaire adaptatif et sélectionnez le thème Ultramarine accessible qui apparaît dans la liste des options.

   ![Commencer la conversion](assets/aftia-start-conversion.jpg)

   ![Thème Ultramarine](assets/aftia-upload-conversion-settings.jpg)

   Le statut de pourcentage terminé s’affiche pendant la conversion. Une fois que l’état affiche **Converted**, cliquez sur le dossier **output**, sélectionnez le formulaire adaptatif et cliquez sur **Modifier** pour ouvrir le formulaire converti.

1. Camilla examine ensuite le formulaire et s’assure que tous les champs sont présents

   ![Conversion des révisions](assets/aftia-review-conversion.jpg)

1. Camilla commence ensuite à éditer le formulaire. Elle sélectionne Panneau racine > Modifier (la clé) > Sélectionner Onglets en haut dans le menu déroulant Disposition du panneau > sélectionne la case à cocher.

   ![Propriétés de révision](assets/aftia-review-properties.jpg)

1. Camilla ajoute ensuite toutes les modifications de champ et CSS nécessaires pour produire le produit final.

   ![Ajouter CSS](assets/aftia-add-css.jpg)

### Modèle de données de formulaire et sources de données (Camila) {#data-sources}

**Cette section** : Une fois le document converti et généré un formulaire adaptatif, Camila doit connecter le formulaire adaptatif à une source de données.

1. Camila ouvre les Propriétés sur le formulaire qui a été converti en [Automated forms conversion - We.Gov](#automated-forms-conversion-wegov).

1. Camila sélectionne ensuite Modèle de formulaire > Sélectionner le modèle de données de formulaire dans la liste déroulante Sélectionner dans > Sélectionner le FDM d’inscription We.gov dans la liste des options.

1. Cliquez sur le bouton Enregistrer et fermer .

   ![Sélection FDM](assets/aftia-select-fdm.jpg)

1. Camila clique sur le dossier **output** , sélectionne le formulaire adaptatif et clique sur **Edit** pour ouvrir le formulaire We.Gov complété.
1. Camila sélectionne un champ de formulaire adaptatif et clique sur ![Icône Configurer](assets/configure-icon.svg). Elle crée une liaison avec les entités de modèle de données de formulaire à l’aide du champ **Référence de liaison**. Elle répète cette étape pour tous les champs du formulaire adaptatif.

### Test d’accessibilité des formulaires (Camila) {#form-accessibility-testing}

Camila confirme également que le contenu créé est construit correctement et entièrement accessible selon les standards de l&#39;entreprise.

1. Camila clique sur le dossier **output** , sélectionne le formulaire adaptatif et clique sur **Aperçu** pour ouvrir le formulaire We.Gov complété.

1. Ouvre l’onglet Audit dans l’outil Chrome Developer.

1. Exécute une vérification d’accessibilité afin de valider le formulaire adaptatif.

   ![Vérification de l’accessibilité](assets/aftia-accessibility.jpg)

## Démonstration de la vue mobile du formulaire adaptatif (Aya) {#mobile-view-demo}

**Cette section doit être effectuée avant la démonstration.**

**Instructions utilisateur :**

1. Accédez à : *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Connectez-vous avec :

   1. **Utilisateur** : aya.tan
   1. **Mot de passe** : password

1. Redimensionnez la fenêtre du navigateur ou utilisez l’émulateur du navigateur pour répliquer la taille d’un appareil mobile.

### Site Web We.Gov (Aya) {#aya-user-story-we-gov-website}

![Un utilisateur fictif](/help/forms/using/assets/aya_tan_new-1.png)

**Cette section** : Aya est une citoyenne. Elle entend d&#39;une amie qu&#39;elle peut être éligible pour recevoir un Service d&#39;une agence gouvernementale. Aya accède au site Web We.Gov à partir de son téléphone mobile pour en savoir plus sur les services auxquels elle est éligible.

### We.Gov Pre-Screener (Aya) {#aya-user-story-we-gov-pre-screener}

Aya répond à quelques questions pour confirmer son éligibilité en remplissant un court formulaire adaptatif sur son téléphone portable.

**Instructions utilisateur :**

1. Effectuez une sélection dans chaque champ de liste déroulante.

   >[!NOTE]
   >
   >Si l’utilisateur gagne plus de 200 000 $ par an, il n’est pas éligible.

1. Cliquez sur &quot;**Suis-je éligible ?**” button.
1. Cliquez sur le bouton &quot;**Appliquer maintenant**&quot; pour continuer.

   ![Lien Appliquer maintenant](/help/forms/using/assets/apply_now_link.png)

### Formulaire Adaptatif We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya découvre qu’elle est éligible et commence à remplir sa demande pour demander le service sur son appareil mobile.

Aya doit consulter certains documents à la maison avant de pouvoir remplir la demande de service. Elle enregistre et quitte l’application à partir de son appareil mobile.

**Instructions utilisateur :**

1. Renseignez les champs Informations de base , les champs et listes déroulantes suivants sont obligatoires :

   1. Informations de base

      1. Prénom
      1. Nom
      1. DDN
      1. E-mail

1. Utilisez la **logique dynamique** suivante pour démontrer la fonctionnalité dynamique à l’aide de la liste déroulante **État de la famille** :

   1. **Simple** : Afficher en regard du panneau parent
   1. **Marié** : Afficher le panneau dépendant du mariage
   1. **Divorcé** : Afficher en regard du panneau parent
   1. **veuve** : Afficher en regard du panneau parent
   1. **Avez-vous des enfants ?**: Bouton radio (Oui/Non) pour afficher le panneau enfant à charge.

      1. (Ajouter/Supprimer) pour ajouter/supprimer plusieurs panneaux enfant dépendants.

1. Cliquez sur la flèche droite dans la barre de menus grise.
1. Cliquez sur le bouton Enregistrer en bas de la page.

   ![Détails du formulaire adaptatif](/help/forms/using/assets/adaptive_form.png)

## Démonstration de l’appli de bureau {#desktop-demo}

**Cette section :** De retour à la maison, Aya a trouvé les informations dont elle avait besoin et reprend la demande depuis son bureau. Aya accède au portail de formulaires en ligne pour reprendre sa demande. Avec une personnalisation simple, les agences peuvent également générer automatiquement et envoyer par courrier électronique un lien pour reprendre l’application.

### Suite du formulaire adaptatif (Aya) {#aya-user-story-continued-adaptive-form}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Dans la barre de navigation, sélectionnez &quot;**Services en ligne**&quot;.
1. Dans le panneau &quot;Version préliminaire de Forms&quot;, sélectionnez la demande d’inscription existante pour les prestations d’intégrité.

   ![Demande d’inscription pour les prestations de santé](/help/forms/using/assets/enrollment_application.png)

   L’apparence est la même, et elle n’a pas besoin de saisir à nouveau des données.

   **Instructions utilisateur :**

1. Cliquez sur Circle CTA droit pour passer à la section suivante.

   ![CTA du cercle droit](/help/forms/using/assets/right_circle_cta_new.png)

   Le formulaire est renseigné jusqu’au point de la dernière entrée d’Aya. Aya a saisi toutes ses informations et est prête à les envoyer.

   ![Envoyer le formulaire adaptatif](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Lorsqu’Aya remplit le champ du numéro de téléphone, elle doit le remplir sous la forme d’un nombre à 11 chiffres au fil de l’eau, sans tirets, espaces ou tirets.

   Après l’envoi, Aya reçoit une page de remerciement. Elle peut également recevoir un courrier électronique qu’elle peut ouvrir pour signer électroniquement le document d’enregistrement avec Adobe Sign.

### Facultatif : Adobe Sign (Aya) {#adobe-sign}

**Instructions utilisateur :**

1. Accédez à votre client de messagerie et recherchez l’adresse électronique Adobe Sign.
1. Cliquez sur le lien vers Adobe Sign.

   ![Lien de signature d’Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instructions utilisateur :**

1. Cochez la case &quot;**J’accepte**&quot;.
1. Cliquez sur &quot;**Accepter**&quot;.
1. Faites défiler jusqu’au bas du document révisé.
1. Cliquez sur l’onglet jaune en surbrillance pour signer le document.

   ![Signer le ](/help/forms/using/assets/sign_document_new.png) ![documentSigner le document de test](/help/forms/using/assets/sign_test_document.png)

## Agent du gouvernement (George) {#government-agent-george}

![Agent du gouvernement George](/help/forms/using/assets/george_lang-1.png)

**Cette section :** George est un analyste des affaires de l&#39;agence gouvernementale Aya est un demandeur de service. George dispose d’un seul tableau de bord où il peut voir toutes les demandes de service qui lui ont été affectées pour révision.

### AEM Boîte de réception (George) {#george-user-story-aem-inbox}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l’icône de l’utilisateur (coin supérieur droit) et utilisez l’option de menu &quot;**Se déconnecter**&quot; ou &quot;**Se faire passer pour**&quot; si vous êtes actuellement connecté avec un utilisateur administrateur.

   1. Connectez-vous avec :

      1. **Utilisateur :** george.lang
      1. **Mot de passe :** password
   1. Ou emprunter l’identité :

      1. Saisissez &quot;**George**&quot; dans le champ &quot;**Emprunter l’identité de**&quot;.

      1. Cliquez sur OK pour emprunter l’identité.


1. Dans le coin supérieur droit, cliquez sur l’icône Notification (cloche) .
1. Cliquez sur &quot;**Afficher tout**&quot; pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez la dernière tâche &quot;**Health Avantages Application Review**&quot;.

   ![Examen des demandes d’avantages sociaux](/help/forms/using/assets/health_benefits.png)

### Facultatif : AEM Boîte de réception et MS Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Grâce aux intégrations de données et aux workflows automatisés, l’application Aya apparaît, ainsi qu’un enregistrement CRM qui a été généré automatiquement lors de l’envoi des données.

**Instructions utilisateur :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur le bouton &quot;**Ouvrir MS Dynamics**&quot; pour ouvrir l’enregistrement MS Dynamics dans une nouvelle fenêtre.
1. Dans le CRM, toutes les informations peuvent être mises à jour.

   1. Vous pouvez éventuellement ajouter des notes de révision directement dans Dynamics.

1. Fermez et revenez à AEM boîte de réception.

   ![Enregistrement MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Retour à AEM Boîte de réception (George) {#george-user-story-back-to-aem-inbox}

George approuve la demande d’Aya et, grâce à un workflow automatisé existant, un email de confirmation est également envoyé à Aya.

**Instructions utilisateur :**

1. Accédez au coin supérieur gauche et cliquez sur &quot;**Approve**&quot; (Approuver) pour approuver la demande.
1. Dans le modal, vous pouvez laisser un message pour le prospect CX.
1. Cliquez sur Terminé.
1. (Rôle citoyen) Ouvrez votre client de messagerie pour afficher l’e-mail envoyé à Aya.

   ![Afficher l&#39;email envoyé à Aya](/help/forms/using/assets/email_client.png)

## CX Lead (Camila) {#cx-lead-camila}

![Camila (chef CX)](/help/forms/using/assets/camila_santos-1.png)

**Cette section :** Camila the CX lance un appel téléphonique de bienvenue avec Aya pour expliquer comment utiliser les services publics pour lesquels elle a reçu l&#39;autorisation de service.

### (Facultatif) AEM Boîte de réception et MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l’icône de l’utilisateur (coin supérieur droit) et utilisez l’option de menu &quot;**Se déconnecter**&quot; ou &quot;**Se faire passer pour**&quot; si vous êtes actuellement connecté avec un utilisateur administrateur.

   1. Connectez-vous avec :

      1. **Utilisateur** : camila.santos
      1. **Mot de passe** : password
   1. Ou emprunter l’identité :

      1. Saisissez &quot;**Camila**&quot; dans le champ &quot;**Emprunter l’identité de**&quot;.

      1. Cliquez sur OK pour emprunter l’identité.


1. Dans le coin supérieur droit, cliquez sur l’icône Notification (cloche) .
1. Cliquez sur &quot;**Afficher tout**&quot; pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez la dernière tâche &quot;**Nouvelle approbation de contact**&quot;.

![Nouvelle approbation de contact](/help/forms/using/assets/new_contact_approval.png)

**(Facultatif) Instructions utilisateur :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur le bouton &quot;**Ouvrir MS Dynamics**&quot; pour ouvrir l’enregistrement MS Dynamics dans une nouvelle fenêtre.
1. Dans le CRM, toutes les informations peuvent être mises à jour.

   1. Vous pouvez éventuellement ajouter une nouvelle activité d’appel directement dans Dynamics.
   1. Ouvrez la section &quot;**Activités**&quot;.
   1. Cliquez sur l’option &quot;**Nouvel appel téléphonique**&quot;.
   1. Ajoutez les détails de l’appel téléphonique.
   1. Enregistrez la fenêtre, puis fermez-la.

1. De retour dans AEM, accédez au coin supérieur gauche et cliquez sur &quot;**Submit**&quot; pour envoyer la demande.
1. Dans le modal, vous pouvez laisser un message.
1. Cliquez sur Terminé.

   ![Onglet Activités ](/help/forms/using/assets/activities_tab.png) ![Confirmer nouveau contact](/help/forms/using/assets/confirm_new_contact.png)

## (Facultatif) Kit de bienvenue Citoyen (Aya) {#welcome-kit-citizen-aya}

**Cette section :** Aya reçoit un courrier électronique contenant un lien vers une communication interactive qui résume ses avantages et inclut également des champs de formulaire à remplir. Une instruction d’avantages PDF est jointe et un lien vers une lettre de communication interactive dans le courrier (avec le même thème/marque que la communication interactive).

### Notification Client Par Courrier Électronique (Aya) {#aya-user-story-email-client}

**Instructions utilisateur :**

1. Recherchez et ouvrez le courrier électronique du kit de bienvenue.
1. Faites défiler la page jusqu’à la pièce jointe PDF.
1. Cliquez sur pour ouvrir la pièce jointe PDF.
1. Faites défiler l’écran vers le haut dans votre client de messagerie et cliquez sur &quot;**Afficher le kit de bienvenue en ligne**&quot;.

   1. Cette opération ouvre la version du canal web du même document.

1. Pour une référence rapide à PDF directement :

   *https://&lt;aemserver> :&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Pour une référence rapide à IC directement :

   *https://&lt;aemserver>: &lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Welcome Avantages ](/help/forms/using/assets/welcome_benefits_handbook.png) ![ManualInteractive Communication Link](/help/forms/using/assets/interactive_communication.png)

## Renouvellement du citoyen (Aya) {#renewal-reminder-citizen-aya}

**Cette section :** Camila planifie également un rappel de communication un an plus tard. (Étape de workflow qui automatise/exécute et envoie électronique).

### Notification Client Par Courrier Électronique (Aya) {#aya-user-story-email-client-updated}

**Instructions utilisateur :**

1. Accédez à votre client de messagerie.
1. Recherchez et ouvrez l’e-mail Rappel de renouvellement .
1. Cliquez sur le bouton &quot;**Submit a1/>&quot; pour ouvrir le formulaire adaptatif.**

   1. Cette section est délibérément laissée vide pour prendre en charge le préremplissage de données lors de la phase 2.

   ![Courrier électronique de rappel de renouvellement](/help/forms/using/assets/renewal_reminder_email.png)

## (Facultatif) Modèle de données de formulaire (Camila) {#form-data-model}

**Cette section** : Camila accède aux intégrations de données AEM Forms où elle peut exécuter un test rapide pour vérifier que les informations envoyées à la source de données externe via l’intégration du modèle de données de formulaire sont bien présentes.

### Modèle de données de formulaire (Camila) {#form-data-model-camila}

**Cette section** : Camila accède à la page Sources de données pour valider les données que le serveur a répliquées dans la base de données Derby.

1. Une fois l’expérience utilisateur terminée et l’envoi de l’utilisateur terminé, Camila accède à l’onglet Sources de données dans AEM Forms (**Forms** > **Intégrations de données**).

1. Camila sélectionne ensuite AEM Forms **We.gov FDM**, puis édite le **FDM d’inscription We.gov**.

1. Camila sélectionne ensuite le **Contact** > **Service de lecture** à tester.

   ![Service de lecture des contacts](assets/aftia-contact-read-service.jpg)

1. Camila fournit ensuite au service de test un ID de contact, puis clique sur le bouton Tester. Par exemple, 1 ou 2, si vous avez envoyé le formulaire. Si vous n’avez pas envoyé le formulaire, aucune donnée n’est renvoyée.

   ![Service de lecture des contacts](assets/aftia-test-service.jpg)

1. Camila peut ensuite vérifier que les données ont bien été insérées dans la source de données.

   * Les données du Derby DS ressemblent au format suivant :

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

**Cette section :** Camila accède à un tableau de bord où elle peut voir les IPC de l’agence, tels que le pourcentage de citoyens qui commencent à remplir un formulaire de demande de service et abandonnent, la durée moyenne entre l’envoi d’une demande et la réponse d’approbation/refus, et les statistiques d’engagement pour les manuels d’avantages qu’elle a envoyés aux citoyens.

### Rapports Adobe Analytics Sites (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Accédez à *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Sélectionnez &quot;**AEM Forms We.Gov Site**&quot; pour afficher les pages du site.
1. Sélectionnez l’une des pages du site (par exemple Accueil), puis &quot;**Analytics et Recommendations**&quot;.

   ![Analytics et recommandation](/help/forms/using/assets/analytics_recommendation.jpg)

1. Sur cette page, vous verrez les informations récupérées d’Adobe Analytics qui se rapportent à la page AEM Sites (REMARQUE : par conception, ces informations sont régulièrement actualisées à partir d’Adobe Analytics et ne s’affichent pas en temps réel).

   ![Mesures clés Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De retour sur la page vue (accessible à l’étape 3.), vous pouvez également afficher les informations de page vue en modifiant le paramètre d’affichage pour afficher les éléments dans le &quot;**mode Liste**&quot;.
1. Recherchez le menu déroulant &quot;**Afficher**&quot; et sélectionnez &quot;**Mode Liste**&quot;.

   ![Mode Liste dans le menu déroulant Affichage](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Dans le même menu, sélectionnez &quot;**Paramètre d’affichage**&quot; et sélectionnez les colonnes à afficher dans la section &quot;**Analytics**&quot;.

   ![Configurer l&#39;affichage des colonnes](/help/forms/using/assets/view_setting_analytics.jpg)

1. Cliquez sur &quot;**Mettre à jour**&quot; pour rendre les nouvelles colonnes disponibles.

   ![Mettre de nouvelles colonnes à disposition](/help/forms/using/assets/new_columns_available.jpg)

### Rapports Adobe Analytics Forms (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accédez à . 

   *https://&lt;aemserver> :&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Sélectionnez le formulaire adaptatif &quot;**Demande d’inscription pour les prestations de santé**&quot; et sélectionnez l’option &quot;**Rapport d’analyse**&quot;.

   ![Demande d’inscription pour les prestations de santé](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Patientez jusqu’au chargement de la page et affichez les données du rapport Analytics.

   ![Données du rapport Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
