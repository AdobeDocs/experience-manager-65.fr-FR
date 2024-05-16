---
title: Présentation de la loi sur l’accès à l’information pour le site de référence We.Gov
description: Consultez la présentation du site de référence pour comprendre comment AEM Forms aide les administrations à recevoir et donner les informations demandées par les utilisateurs et utilisatrices dans le cadre de la loi sur l’accès à l’information.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '842'
ht-degree: 100%

---

# Présentation de la loi sur l’accès à l’information pour le site de référence We.Gov {#we-gov-reference-site-foia-walkthrough}

## Scénario de la loi sur l’accès à l’information pour le site de référence {#reference-site-freedom-of-information-act-scenario}

We.Gov est un organisme dépendant de l’État qui permet aux parents adoptifs de s’inscrire pour obtenir une allocation familiale s’ils ont adopté un enfant. We.Gov permet également aux parents de demander des informations auprès des ministères suivants en vertu de la loi sur l’accès à l’information :

* Agence DLA (Defense Logistics Agency)
* Ministère de la Défense, bureau de l’Inspecteur général
* Ministère de la Justice, bureau de la politique de l’information
* Département de la Marine
* Agence de protection de l’environnement

Pour plus d’informations à propos de la loi sur l’accès à l’information, voir [https://www.foia.gov/](https://www.foia.gov).

Le scénario implique les personnages suivants :

* Sarah Rose, personne demandant des informations
* John Jacobs, la personne qui gère la demande et la fait suivre au service approprié.
* Gloria Rios, la fonctionnaire du gouvernement qui fournit les informations de la demande.

## Sarah lance la demande d’informations dans le cadre de la loi sur l’accès à l’information. {#sarah-initiates-request-for-information-under-foia}

Dans le cadre de la loi sur l’accès à l’information, Sarah demande une copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016. Sarah envoie cette demande au bureau de la politique de l’information du ministère de la Justice et indique également qu’elle est prête à payer jusqu’à 100 dollars américains pour les frais d’impression et d’envoi.

### Fonctionnement {#how-it-works}

### Démonstration {#see-it-yourself}

Dans votre navigateur, ouvrez `https://<hostname>:<PublishPort>/wegov`. Sur le site We.Gov, sélectionnez Applications> Toutes les applications. Dans la page Toutes les applications, sélectionnez Appliquer sous Application dans le cadre de la loi sur l’accès à l’information.

## Sarah commence sa demande d’informations dans le cadre de la loi sur l’accès à l’information {#sarah-starts-her-application-for-information-under-foia}

Sarah clique sur **Appliquer** et sur la page Formulaire de demande dans le cadre de la Loi sur l’accès à l’information, Sarah saisit les informations suivantes :

* **Agence** : Sarah précise l’agence à laquelle la demande a été adressée : Ministère de la Justice - Bureau de la politique de l’information.

* **Versera jusqu’à** : Sarah indique qu’elle est prête à payer jusqu’à 100 dollars américains pour les frais d’impression et d’envoi.
* **Décrire la demande en détail** : Sarah indique « Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016. »

![Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016](assets/sarahfiosform.png)

Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016

À tout moment, Sarah peut sélectionner **Enregistrer** pour enregistrer le brouillon du formulaire et y revenir plus tard pour remplir le formulaire et l’envoyer. Sarah envoie le formulaire.

>[!NOTE]
>
>Le workflow de reprise à partir d’un e-mail fonctionne uniquement avec les utilisateurs et utilisatrices connectés. Dans le scénario du site de référence, assurez-vous que l’utilisatrice Sarah Rose est ajoutée. Les informations de connexion de Sarah sont `srose/password`.

## John Jacobs reçoit et approuve la demande. {#john-jacobs-receives-and-approves-the-application}

John Jacobs reçoit la demande et la fait suivre à la bonne personne. La boîte de réception AEM lui permet de voir toutes les demandes envoyées dans un seul emplacement.

### Fonctionnement {#how-it-works-1}

Lorsque Sarah remplit et envoie la demande dans le cadre de la loi sur l’accès à l’information, un enregistrement de la demande est envoyé dans la boîte de réception John Jacobs. John Jacobs peut afficher la demande envoyée et l’accepter ou la refuser.

### Démonstration {#see-it-yourself-1}

Vous pouvez accéder à la boîte de réception AEM à l’adresse https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Connectez-vous à la boîte de réception AEM, en utilisant jjacobs/password comme nom d’utilisateur/mot de passe pour John Jacobs, et consultez la demande dans le cadre de la loi sur l’accès à l’information. Pour plus d’informations sur l’utilisation de la boîte de réception AEM pour les tâches du workflow relatives aux formulaires, voir [Gérer des applications et des tâches Forms dans la boîte de réception AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs peut voir, approuver ou refuser la demande à partir du tableau de bord des demandes. John Jacobs sélectionne et ouvre les détails de la demande et, après avoir examiné la demande, l’approuve.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah reçoit un e-mail d’accusé de réception.</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Une fois que John Jacobs approuve la demande, Sarah reçoit une confirmation par e-mail provenant du site We.Gov. Sarah est informée des frais et du temps requis pour le traitement de sa demande. L&#39;e-mail contient également des informations (adresse e-mail et téléphone) que Sarah peut utiliser pour obtenir des mises à jour sur sa demande.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria reçoit demande dans le cadre de la loi sur l’accès à l’information pour le second niveau d’approbation. {#gloria-receives-the-foia-request-for-second-level-approval}

Une fois que John Jacobs a complété les informations requises et a approuvé la demande de Sarah, la demande est envoyée à Gloria Rios pour l’approbation finale. Gloria consulte le document joint de l’enregistrement et approuve la demande.

![gloriariosinbox](assets/gloriariosinbox.png)

### Fonctionnement {#how-it-works-2}

Lorsque John Jacobs approuve la demande dans le cadre de la loi sur l’accès à l’information, un document PDF ou un document d’enregistrement de la demande est créé et envoyé dans la boîte de réception de Gloria Rios. Gloria peut afficher la demande envoyée et l’accepter ou la refuser.

### Jugez-en par vous-même {#see-for-yourself}

Vous pouvez accéder à la boîte de réception AEM à l’adresse https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Connectez-vous à la boîte de réception AEM à l’aide de grios/password en tant que nom d’utilisateur/mot de passe pour Gloria Rios et consultez la demande dans le cadre de la loi sur l’accès à l’information.

Gloria ouvre la demande et examine les détails de la demande dans le cadre de la loi sur l’accès à l’information. Après avoir consulté les détails de la demande et vérifié la possibilité de fournir les documents requis, Gloria approuve la demande.

![gloriariosapprove](assets/gloriariosapproves.png)

## Sarah reçoit la notification que sa demande est approuvée. {#sarah-receives-notification-that-her-request-is-approved}

Après que Gloria ait approuvé la demande dans le cadre de la loi sur l’accès à l’information, Sarah reçoit un e-mail l’informant que sa demande est approuvée. L&#39;e-mail comprend également des informations sur le délai d’attente attendu pour la fourniture du document et des coordonnées pour le suivi de la demande.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
