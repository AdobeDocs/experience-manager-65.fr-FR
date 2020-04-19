---
title: Présentation du site de référence We.Gov
seo-title: Présentation du site de référence We.Gov
description: Utilisez des utilisateurs et des groupes fictifs pour effectuer des  AEM Forms à l’aide du package de démonstration We.Gov.
seo-description: Utilisez des utilisateurs et des groupes fictifs pour effectuer des  AEM Forms à l’aide du package de démonstration We.Gov.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Présentation du site de référence We.Gov{#we-gov-reference-site-walkthrough}

## Conditions préalables {#pre-requisites}

Set up the reference site as described in [Set up and configure We.Gov reference site](../../forms/using/forms-install-configure-gov-reference-site.md).

## Article utilisateur {#user-story}

* AEM Forms

   * Capture de données
   * Intégration de données (MS Dynamics)
   * Adobe Sign

* Workflow
* Communications client

   * Canal d’impression
   * Canal web

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

Le paquet de démonstration We.Gov est fourni avec les utilisateurs fictifs intégrés suivants :

* **Aya Tan**: Citoyens éligibles à un Service d&#39;une agence gouvernementale

![Utilisateur fictif](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Analyste d&#39;affaires de l&#39;agence We.Gov

![Utilisateur fictif](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Directeur CX de l&#39;agence We.Gov

![Utilisateur fictif](/help/forms/using/assets/camila_santos.png)

Les groupes suivants sont également inclus :

* **Utilisateurs de Web.Gov Forms**

   * George Lang (membre)
   * Camila Santos (membre)

* **Utilisateurs Web.Gov**

   * George Lang (membre)
   * Camila Santos (membre)
   * Aya Tan (membre)

### Légende des termes de présentation de la démonstration {#demo-overview-terms-legend}

1. **Impersonate**: Utilisateurs et groupes définis dans la démonstration AEM.
1. **Bouton**: Rectangle coloré ou flèche circulaire pour la navigation.
1. **Cliquez sur**: Pour exécuter une action dans l’article de l’utilisateur.
1. **Liens**: Situé en haut du menu principal du site Web We.Gov.
1. **Instructions** utilisateur : Ensemble d’étapes numériques à suivre lors de la navigation dans l’histoire de l’utilisateur.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **** mobile : utilisateur We.Gov pour répliquer un mobile  avec un navigateur redimensionné.
1. **** de bureau : Utilisateur We.gov à  la démonstration sur un ordinateur portable ou un ordinateur de bureau.
1. **Formulaire** de pré-filtrage : Formulaire sur le  du site Web We.Gov.
1. **Formulaire** adaptatif : Formulaire de demande d&#39;inscription pour la démonstration We.gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Site** Adobe We.Gov : *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe Inbox**: Icône [](assets/bell.svg) Bell située dans la barre de menus supérieure dans le serveur principal AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Client** de messagerie : Moyen privilégié de de vos courriels (Gmail, Outlook)
1. **CTA**: Appel à l&#39;action
1. **Naviguer**: Pour localiser un point de référence spécifique sur la page du navigateur.

## Démonstration  Mobile {#mobile-view-demo}

**Cette section doit être effectuée avant la démonstration.**

**Instructions utilisateur :**

1. Accédez à : *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Connectez-vous avec :

   1. **Utilisateur**: aya.tan
   1. **Mot de passe** : password

1. Redimensionnez la fenêtre du navigateur ou utilisez l’émulateur du navigateur pour reproduire la taille d’un périphérique mobile.

### Aya User Story (site Web We.Gov) {#aya-user-story-we-gov-website}

![Utilisateur fictif](/help/forms/using/assets/aya_tan_new-1.png)

**Cette section**: Aya est une citoyenne. Elle apprend d&#39;une amie qu&#39;elle peut être admissible à recevoir un service d&#39;une agence gouvernementale. Aya accède au site Web We.Gov depuis son téléphone portable pour en savoir plus sur les services auxquels elle a droit.

### Aya User Story (pré-filtre We.Gov) {#aya-user-story-we-gov-pre-screener}

Aya répond à quelques questions pour confirmer son éligibilité en remplissant un court formulaire adaptatif sur son téléphone portable.

**Instructions utilisateur :**

1. Effectuez une sélection dans chaque champ déroulant.

   >[!NOTE]
   >
   >Si l’utilisateur gagne plus de 200 000 $ par an, il n’est pas admissible.

1. Cliquez sur &quot;**Suis-je éligible ?**” button.
1. Cliquez sur le bouton &quot;**Demander ma carte maintenant**&quot; pour continuer.

   ![Lien Appliquer maintenant](/help/forms/using/assets/apply_now_link.png)

### Aya User Story (formulaire adaptatif We.Gov) {#aya-user-story-we-gov-adaptive-form}

Aya découvre qu&#39;elle est éligible et commence à remplir sa demande de service sur son appareil mobile.

Aya a besoin de revoir un à la maison avant de pouvoir remplir la demande de service. Elle enregistre et quitte l&#39;application.

**Instructions utilisateur :**

1. Renseignez les champs d’informations de base, les champs et les listes déroulantes obligatoires suivants :

   1. Informations de base

      1. Prénom
      1. Second prénom
      1. Nom
      1. Nom préféré
      1. DOB
      1. Sexe
   1. Coordonnées

      1. Adresse 
      1. Ville
      1. Numéro de téléphone
      1. Code postal
      1. Courrier électronique
      1. État
   1. État martial

      1. Statut familial



1. Utilisez la logique **** dynamique suivante pour démontrer la fonctionnalité dynamique à l’aide de la liste déroulante État **de la** famille :

   1. **Simple**: Afficher le prochain panneau parent
   1. **Marié**: Afficher le panneau dépendant du mariage
   1. **Divorcé**: Afficher le prochain panneau parent
   1. **Veuf**: Afficher le prochain panneau parent
   1. **Avez-vous des enfants ?**: (Oui/Non) pour afficher le panneau enfant à charge.

      1. (Ajouter/Supprimer) pour ajouter/supprimer plusieurs panneaux enfant dépendants.

1. Cliquez sur la flèche droite dans la barre de menus grise.
1. Cliquez sur le bouton Enregistrer dans la partie inférieure.

   ![Détails du formulaire adaptatif](/help/forms/using/assets/adaptive_form.png)

## Démo de bureau {#desktop-demo}

**Cette section :** De retour chez elle, Aya a trouvé les informations dont elle avait besoin et reprend l&#39;application depuis son bureau. Aya accède au portail de formulaires en ligne pour reprendre sa demande. Avec une personnalisation simple, les agences peuvent également générer automatiquement et envoyer par courrier électronique un lien pour reprendre l&#39;application.

### Aya User Story (suite du formulaire adaptatif) {#aya-user-story-continued-adaptive-form}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Dans la barre de navigation, sélectionnez &quot;Services **en** ligne&quot;.
1. Dans le panneau &quot;Brouillons de formulaires&quot;, sélectionnez l’option existante &quot;Demande d’inscription aux prestations d’assurance maladie&quot;.

   ![Demande d&#39;inscription aux prestations santé](/help/forms/using/assets/enrollment_application.png)

   L&#39;apparence est la même, et elle n&#39;a pas besoin de saisir à nouveau des données.

   **Instructions utilisateur :**

1. Cliquez sur Circle CTA droit pour passer à la section suivante.

   ![Cercle droit CTA](/help/forms/using/assets/right_circle_cta_new.png)

   Le formulaire est renseigné jusqu’au point de la dernière entrée d’Aya. Aya a entré toutes ses informations et est prête à les envoyer.

   ![Envoyer le formulaire adaptatif](/help/forms/using/assets/submit_adaptive_form.png)

   Après avoir envoyé Aya reçoit un courrier électronique qu’elle ouvre et qu’elle est prête à signer électroniquement avec Adobe Sign.

**Instructions utilisateur :**

1. Après envoi, une page de remerciement s’affiche.
1. Accédez à votre client de messagerie et recherchez le courrier électronique Adobe Sign.
1. Cliquez sur le lien vers Adobe Sign.

   ![Lien de signature Adobe](/help/forms/using/assets/adobe_sign_link.png)

**Instructions utilisateur :**

1. Cochez la case &quot;**Je suis d&#39;accord**&quot;.
1. Cliquez sur &quot;**Accepter**&quot;.
1. Faites défiler l’écran jusqu’au bas du  de consulté.
1. Cliquez sur l&#39;onglet jaune surligné pour signer le .

   ![Signez le](/help/forms/using/assets/sign_document_new.png) ![Signez le de test](/help/forms/using/assets/sign_test_document.png)

## Agent du gouvernement (George) {#government-agent-george}

![Agent du gouvernement George](/help/forms/using/assets/george_lang-1.png)

**Cette section :** George est analyste en affaires à l&#39;agence gouvernementale Aya demande un service. George a un seul  où il peut voir toutes les demandes de service qui lui ont été assignées pour examen.

### George User Story (boîte de réception AEM) {#george-user-story-aem-inbox}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l&#39;icône de l&#39;utilisateur (dans le coin supérieur droit) et utilisez l&#39;option de menu &quot;**Se déconnecter**&quot; ou &quot;**Se faire passer pour**&quot; si vous êtes connecté avec un administrateur.

   1. Connectez-vous avec :

      1. **Utilisateur :** george.lang
      1. **Mot de passe :** password
   1. Ou Impersonate :

      1. Tapez &quot;**George**&quot; dans le champ &quot;**Impersonate as**&quot;.

      1. Cliquez sur OK pour vous faire passer.


1. Dans le coin supérieur droit, cliquez sur l’icône Notification (sonnerie).
1. Cliquez sur **tout** pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez le dernier &quot;Examen **des demandes de prestations de** santé&quot;.

   ![Examen des demandes de prestations de santé](/help/forms/using/assets/health_benefits.png)

### George User Story (boîte de réception AEM et MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

Grâce aux intégrations de données et aux  automatisées, l’application Aya apparaît, ainsi qu’un enregistrement CRM qui a été généré automatiquement lors de l’envoi des données.

**Instructions utilisateur :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur le bouton &quot;**Ouvrir MS Dynamics**&quot; pour ouvrir l&#39;enregistrement MS Dynamics dans une nouvelle fenêtre.
1. Dans la gestion de la relation client, toutes les informations peuvent être mises à jour

   1. Vous pouvez également ajouter des notes de révision directement dans Dynamics.

1. Fermez et revenez à la boîte de réception AEM.

   ![Enregistrement MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### George User Story (retour à la boîte de réception AEM) {#george-user-story-back-to-aem-inbox}

George approuve la demande d’Aya et, grâce à un processus automatisé existant, un courrier électronique de confirmation est également envoyé à Aya.

**Instructions utilisateur :**

1. Accédez au coin supérieur gauche et cliquez sur &quot;**Approuver**&quot; pour approuver la demande.
1. Dans le mode modal, vous pouvez laisser un message pour le prospect CX.
1. Cliquez sur Done (Terminé). 
1. (Rôle Citoyen) Ouvrez votre client de messagerie pour du courrier électronique envoyé à Aya.

   ![e-mail envoyé à Aya](/help/forms/using/assets/email_client.png)

## CX Lead (Camila) {#cx-lead-camila}

![Camila (chef CX)](/help/forms/using/assets/camila_santos-1.png)

**Cette section :** Camila, la responsable CX, lance un appel téléphonique de bienvenue avec Aya pour expliquer comment utiliser les services gouvernementaux pour lesquels elle a été approuvée.

### Article pour l’utilisateur de Camila (boîte de réception AEM et MS Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**Instructions utilisateur :**

1. Accédez à *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Cliquez sur l&#39;icône de l&#39;utilisateur (dans le coin supérieur droit) et utilisez l&#39;option de menu &quot;**Se déconnecter**&quot; ou &quot;**Se faire passer pour**&quot; si vous êtes connecté avec un administrateur.

   1. Connectez-vous avec :

      1. **Utilisateur**: camila.santos
      1. **Mot de passe** : password
   1. Ou Impersonate :

      1. Tapez &quot;**Camila**&quot; dans le champ &quot;**Impersonate as**&quot;.

      1. Cliquez sur OK pour vous faire passer.


1. Dans le coin supérieur droit, cliquez sur l’icône Notification (sonnerie).
1. Cliquez sur **tout** pour accéder à la boîte de réception.
1. Dans la boîte de réception, ouvrez le dernier &quot;**Nouvelle approbation** de contact&quot;.

   ![Nouvelle approbation de contact](/help/forms/using/assets/new_contact_approval.png)

   **Instructions utilisateur :**

1. Ouvrez et examinez le formulaire adaptatif en lecture seule.
1. Cliquez sur le bouton &quot;**Ouvrir MS Dynamics**&quot; pour ouvrir l&#39;enregistrement MS Dynamics dans une nouvelle fenêtre.
1. Dans la gestion de la relation client, toutes les informations peuvent être mises à jour

   1. Si vous le souhaitez, ajoutez un nouvel appel  directement dans Dynamics.
   1. Ouvrez la section &quot;****&quot;.
   1. Cliquez sur l&#39;option &quot;**Nouvel appel** téléphonique&quot;.
   1. Ajouter les détails de l&#39;appel téléphonique.
   1. Enregistrez et fermez la fenêtre.

1. De retour dans AEM, accédez au coin supérieur gauche et cliquez sur &quot;**Envoyer**&quot; pour envoyer la demande.
1. Dans le module, vous pouvez laisser un message.
1. Cliquez sur Done (Terminé). 

   ![, onglet](/help/forms/using/assets/activities_tab.png)  de l’ ![Confirmer le nouveau contact](/help/forms/using/assets/confirm_new_contact.png)

## Kit de bienvenue (Aya) {#welcome-kit-citizen-aya}

**Cette section :** Aya reçoit un courriel qui contient un lien vers une communication interactive qui résume ses avantages et inclut des champs de formulaire à remplir. Avec le relevé des avantages PDF joint et le lien vers la lettre de communication interactive dans le courrier (avec le même thème/marque que la communication interactive).

### Aya User Story (client de messagerie) {#aya-user-story-email-client}

**Instructions utilisateur :**

1. Recherchez et ouvrez le courrier électronique du kit de bienvenue.
1. Faites défiler la page jusqu’à la pièce jointe PDF au bas de la page.
1. Cliquez sur pour ouvrir la pièce jointe PDF.
1. Faites défiler votre client de messagerie et cliquez sur &quot;**kit de bienvenue en ligne**&quot;.

   1. Cela ouvrira la version  du Web du même  de.

1. Pour une référence rapide au format PDF directement :

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Pour une référence rapide à IC directement :

   *https://&lt;serveur aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?=web&amp;mode=&amp;wcmmode=disabled*

   ![Guide](/help/forms/using/assets/welcome_benefits_handbook.png) des avantages de bienvenue Lien de communication ![interactif](/help/forms/using/assets/interactive_communication.png)

## Renouvellement du citoyen (Aya) {#renewal-reminder-citizen-aya}

**Cette section :** Camila planifie aussi un rappel de communication un an plus tard. (Etape du flux de travail qui automatise/s’exécute et envoie des courriers électroniques).

### Aya User Story (client de messagerie) {#aya-user-story-email-client-1}

**Instructions utilisateur :**

1. Accédez à votre client de messagerie.
1. Recherchez et ouvrez le courrier électronique Rappel de renouvellement.
1. Cliquez sur le bouton &quot;**Soumettre une nouvelle application**&quot; pour ouvrir le formulaire adaptatif.

   1. Cette section est volontairement laissée vide pour prendre en charge le préremplissage des données dans la phase 2.
   ![Courriel du rappel de renouvellement](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CX Lead (Camila) {#analytics-cx-lead-camila}

**Cette section :** Camila se dirige vers un où elle peut voir à travers les IPC de l&#39;agence, comme le pourcentage de citoyens qui  remplir un formulaire de demande de service et abandonner, la durée moyenne entre la soumission d&#39;une demande et la réponse d&#39;approbation/refus, et les statistiques d&#39;engagement pour les manuels d&#39;avantages qu&#39;elle a envoyés aux citoyens.

### Camila passe en revue les  des sites (We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Accédez à *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Sélectionnez &quot;Site **WebGov d’** AEM Forms&quot; pour les pages du site.
1. Sélectionnez l’une des pages du site (par exemple, Accueil), puis sélectionnez &quot;**Analyses et recommandations**&quot;.

   ![Analytics et recommandation](/help/forms/using/assets/analytics_recommendation.jpg)

1. Sur cette page, vous verrez les informations extraites d’Adobe Analytics qui se rapportent à la page Sites AEM (REMARQUE : par conception, ces informations sont régulièrement actualisées à partir d’Adobe Analytics et ne s’affichent pas en temps réel).

   ![Mesures clés d’Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. De retour sur la page  de de la page (accessible à l’étape 3.), vous pouvez également  les informations de la page en définissant le paramètre d’affichage sur les éléments de la &quot;****--&quot;.
1. Localisez le menu déroulant &quot;****&quot; et sélectionnez &quot;****&quot;.

   ![ dans le menu déroulant  de l’univers](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Dans le même menu, sélectionnez **Paramètres** de  et sélectionnez les colonnes à afficher dans la section &quot;**Analytics**&quot;.

   ![Configuration de l’affichage des colonnes](/help/forms/using/assets/view_setting_analytics.jpg)

1. Cliquez sur &quot;**Mettre à jour**&quot; pour rendre les nouvelles colonnes disponibles.

   ![Rendre les nouvelles colonnes disponibles](/help/forms/using/assets/new_columns_available.jpg)

### Camila passe en revue les  de formulaires (We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Accédez à .

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Sélectionnez le formulaire adaptatif &quot;Demande d’**inscription pour les avantages** pour la santé&quot; et sélectionnez l’option &quot;Rapport **** Analytics&quot;.

   ![Demande d&#39;inscription aux prestations santé](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Patientez jusqu’à ce que la page se charge et les données du rapport Analytics.

   ![Données du rapport Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)

