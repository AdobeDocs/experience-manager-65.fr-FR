---
title: Présentation du site de référence de recrutement des employé(e)s
description: Le site de référence AEM Forms explique comment les entreprises peuvent utiliser les fonctionnalités AEM Forms pour mettre en oeuvre le processus de recrutement des employés.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 20%

---

# Présentation du site de référence de recrutement des employé(e)s {#employee-recruitment-reference-site-walkthrough}

## Présentation {#overview}

We.Finance est une organisation qui permet aux candidats de postuler pour un emploi via le portail du site de référence. L’entreprise utilise également le portail pour gérer la planification et l’affichage des entretiens des candidats, et la communication interne. Le site gère les éléments suivants :

* Les candidats recherchent et postulent des emplois
* Sélection et présélection des candidats
* Processus d’entretien
* Collecte des détails des candidats
* Vérification de l&#39;arrière-plan du candidat
* Déploiement des offres sur les candidats sélectionnés

>[!NOTE]
>
>Des cas pratiques de recrutement d’employés sont disponibles sur les sites de référence We.Finance et We.Gov . Les exemples, images et descriptions utilisés dans les présentations WebFix utilisent le site de référence We.Finance. Cependant, vous pouvez également exécuter ces cas d’utilisation et examiner les artefacts à l’aide de We.Gov. Pour ce faire, remplacez **we-finance** avec **we-gov** dans les URL mentionnées.

### Modèles de workflow impliqués {#workflow-models-involved}

Le cas d’utilisation du recrutement des employés implique deux workflows :

* Avant l’entretien : processus de recrutement des employés We Finance
* Avant l’entretien : processus après l’entretien de recrutement des employés We Finance

Ces entretiens sont créés dans AEM et sont disponibles à l’adresse :

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### Workflow de recrutement des employés We Finance {#we-finance-employee-recruiting-workflow}

Voici le modèle du processus de recrutement des employés We Finance suivi dans ce document.

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### Processus de post-entretien de recrutement des employés We Finance {#we-finance-employee-recruiting-post-interview-workflow}

Voici le modèle du processus de recrutement après entretien des employés de We Finance suivi dans ce document.

![we-finance-employee-recruiting-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### Personas {#personas}

Le scénario implique les personnages suivants :

* Sarah Rose, la candidate qui demande un emploi dans l’organisation
* John Jacobs, le recruteur
* Gloria Rios, la responsable des recrutements
* John Doe, le responsable des ressources humaines

## Sarah demande un emploi {#sarah-applies-for-a-job}

Sarah Rose recherche une opportunité d’emploi dans l’entreprise. Elle visite son portail web et explore les offres d’emploi répertoriées sur la page Carrières. Elle trouve une liste d&#39;emplois correspondante et fait une demande pour celle-ci.

![home-page](assets/home-page.png)

Page d’accueil de We.Finance

![career-page](assets/career-page.png)

Page de carrière We.Finance

Sarah clique sur Demander sur une publication de tâche. Le formulaire de demande de traitement s’ouvre. Elle remplit tous les détails de la demande et l’envoie.

![job-application-form](assets/job-application-form.png)

### Fonctionnement {#how-it-works}

La page d’accueil et la page Carrières de We.Finance sont des pages d’AEM Sites. La page de carrière incorpore un formulaire adaptatif, qui utilise un panneau répétable pour récupérer les offres d’emploi à l’aide d’un service et les répertorier sur la page. Vous pouvez consulter le formulaire adaptatif à l’adresse `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### Démonstration {#see-it-yourself}

Accédez à `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` et cliquez sur **[!UICONTROL Carrière]**. Cliquez sur **[!UICONTROL Rechercher]** afin que vous renseignez la liste des tâches, puis cliquez sur **[!UICONTROL Appliquer]** pour un travail. Renseignez les détails du formulaire et envoyez la demande.

Assurez-vous de spécifier un ID de courrier électronique valide dans l’application, car toute communication par le biais de cette procédure pas à pas est envoyée à l’ID de courrier électronique spécifié.

## John Jacobs présélectionne le profil de Sarah Rose pour la sélection du responsable de l’embauche {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

L’entreprise reçoit la demande d’emploi envoyée par Sarah. John Jacobs, un recruteur, se voit attribuer la tâche de révision du profil de Sarah. John examine la tâche dans sa boîte de réception AEM, trouve le profil correspondant aux exigences de la tâche et clique sur Raccourci. Le profil de Sarah est transmis à Gloria Rios, la responsable des recrutements, pour approbation.

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

Boîte de réception AEM de John

![candidate-shortlist](assets/candidate-shortlist.png)

John Jacobs présélectionne le profil de Sarah Rose pour la sélection du responsable de l’embauche

**Fonctionnement**

L’action d’envoi dans le formulaire de demande de tâche déclenche un processus qui crée une tâche dans la boîte de réception de John Jacob pour examiner la demande. Lorsque John examine et préséllise la demande, le processus crée une tâche dans la boîte de réception de Gloria, responsable de l’embauche.

### Démonstration {#see-it-yourself-1}

Accédez à `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`et connectez-vous en utilisant jjacobs/password comme nom d’utilisateur/mot de passe pour John Jacobs. Ouvrez la tâche de consultation du profil de candidat(e) et sélectionnez le ou la candidat(e).

## Gloria examine la demande et approuve le demandeur pour un entretien {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

Gloria, la responsable de l’embauche, reçoit le profil présélectionné comme tâche dans sa boîte de réception d’AEM. Elle la examine et approuve la candidate, Sarah Rose, pour l&#39;entretien.

![gloriainbox](assets/gloriainbox.png)

Boîte de réception d’AEM de Gloria

![gloriaschedulesentretien](assets/gloriaschedulesinterview.png)

Gloria approuve Sarah Rose pour un entretien

**Fonctionnement**

Lorsque Gloria approuve le candidat pour un entretien, le processus crée une tâche dans la boîte de réception AEM de John Doe, qui est un recruteur pour We.Finance.

### Démonstration {#see-it-yourself-2}

Accédez à `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` et connectez-vous en utilisant jjacobs/password comme nom d’utilisateur/mot de passe pour John Jacobs. Ouvrez la tâche de consultation du profil du candidat et sélectionnez le candidat.

Accédez à sur `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` et connectez-vous en utilisant grios/password comme nom d’utilisateur/mot de passe pour Gloria Rios. Ouvrez la tâche de révision du profil du candidat et cliquez sur Planifier l’entretien.

## John Doe planifie un entretien {#john-doe-schedules-an-interview}

John Doe reçoit la tâche de planifier une entrevue dans sa boîte de réception. John Doe sélectionne et ouvre la tâche, et corrige la date et l’heure de l’entretien, le lieu et la personne responsable de l’entretien comme John Jacob. John Doe clique sur Envoyer un courrier électronique d’invitation. Un courrier électronique est envoyé à Sarah et une tâche est affectée à Gloria, la responsable des recrutements, pour l’entretien avec Sarah.

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

Boîte de réception AEM de John Doe

![johndoescheduleinterviewer](assets/johndoescheduleinterview.png)

John Doe planifie l’entretien et envoie les détails à Sarah Rose

## Sarah Rose reçoit le courrier électronique avec la planification de l’entretien {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose reçoit le courrier électronique avec la planification de l’entretien, le lieu et d’autres détails. Sarah clique sur Accepter pour indiquer qu’elle respecte le calendrier et le lieu de l’entretien. En fonction des informations précises, Sarah parvient aux interviews.

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose reçoit la planification de l’entretien

## Après les entretiens, le responsable des recrutements présélectionne Sarah Rose {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Une fois que Sarah Rose a passé les entretiens et les a effacés, Gloria Rios, la responsable des recrutements, ouvre la tâche Sélection de candidat dans sa boîte de réception et clique sur Sélectionner. La décision de Gloria Rios est transmise à la personne des ressources humaines, John Doe, pour qu&#39;elle soit traitée plus avant.

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Boîte de réception d’AEM de Gloria

![gloriariosselectcandidate](assets/gloriariosselectcandidate.png)

Gloria Rios sélectionne Sarah Rose après les interviews

## John Doe demande plus d’informations {#john-doe-requests-more-information}

Avant de demander à un candidat de rejoindre l’organisation, l’arrière-plan de Sarah doit être vérifié. John Doe ouvre et examine les détails de la candidate sélectionnée et constate que certains de ses détails sur l&#39;emploi et la formation ne sont pas encore remplis. John Doe clique sur Besoin de plus d’informations.

![johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe demande plus d’informations à Sarah Rose sur ses études et son expérience professionnelle.

## Sarah Rose reçoit un courrier électronique lui demandant des informations supplémentaires {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose reçoit un courrier électronique l’informant que des informations supplémentaires sont requises pour traiter sa demande d’emploi. Le courrier électronique comprend un lien vers le formulaire pour remplir les informations requises.

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose reçoit un courrier électronique l’informant que des informations supplémentaires sont requises pour traiter sa demande d’emploi.

Sarah clique sur le lien Fournir des détails dans le courrier électronique. Un formulaire s’affiche. Sarah remplit les informations requises sur la formation et l’emploi comme demandé par John Doe et clique sur Envoyer.

![additionalinformation1](assets/additionalinformation1.png)

Sarah ouvre le formulaire d’informations supplémentaires en cliquant sur le lien dans le courrier électronique

![additionalinformation2](assets/additionalinformation2.png)

Sarah remplit des informations supplémentaires comme demandé par John Doe et clique sur Envoyer

## John Doe examine le profil du candidat sélectionné pour obtenir les informations supplémentaires fournies {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe sélectionne la demande de révision du candidat et l’ouvre. John Doe trouve que Sarah a rempli toutes les informations selon les besoins. Après avoir examiné la demande, John Doe clique sur Approuver. Une fois approuvée par John Doe, la demande d’exécution d’une vérification d’arrière-plan sur Sarah Rose est transmise à John Jacobs.

![johndoeadditionainformationinbox](assets/johndoeadditionainformationinbox.png)

Boîte de réception AEM de John Doe

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe examine les informations supplémentaires fournies par Sarah et les approuve

## John Jacobs reçoit une demande de vérification d’arrière-plan {#john-jacobs-receives-a-background-check-request}

John Jacobs voit la demande de vérification en arrière-plan dans sa boîte de réception. John Jacobs ouvre la tâche et examine les informations fournies par Sarah Rose. Après avoir effectué une vérification d’arrière-plan, John Jacobs clique sur Aller de l’avant pour indiquer que la vérification d’arrière-plan a réussi.

![johnjacobsbackgroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

Boîte de réception AEM de John Jacobs

![johnjacobsbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

Après avoir effectué la vérification de l’arrière-plan, John Jacobs clique sur Aller de l’avant

## John Doe envoie la lettre de recrutement à Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe reçoit une demande dans sa boîte de réception AEM pour envoyer la lettre de recrutement. John ouvre la requête et affiche les détails. John Doe joint le PDF de lettre de recrutement, puis clique sur Joindre et envoyer la lettre de recrutement.

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

Boîte de réception AEM de John Doe

![johndoejoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe envoie la lettre de recrutement pour signature

## Sarah Rose reçoit et signe la lettre de recrutement {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose reçoit la lettre de recrutement pour signature. Sarah clique sur Cliquez ici pour consulter et signer la lettre de recrutement. Le fichier PDF de lettre de recrutement s’ouvre avec un champ pour signer le document.

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose reçoit la lettre de recrutement pour signature.

Sarah peut choisir d’entrer, d’utiliser l’option Dessiner pour écrire à la main, d’insérer une image de signature ou d’utiliser l’écran tactile de son mobile pour dessiner sa signature. Sarah saisit son nom, clique sur Cliquer pour signer et télécharge la copie signée de la lettre de recrutement.

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah saisit son nom pour signer la lettre de recrutement

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah clique sur Cliquer pour signer pour terminer la procédure de signature de la lettre de recrutement
