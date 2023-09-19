---
title: Présentation de la loi sur l’accès à l’information pour le site de référence We.Gov
description: Consultez la présentation du site de référence We.Gov afin de comprendre comment AEM Forms aide les gouvernements à recevoir et à transmettre des informations demandées par des personnes en vertu de la loi sur l'accès à l'information.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 24%

---

# Présentation de la loi sur l’accès à l’information pour le site de référence We.Gov {#we-gov-reference-site-foia-walkthrough}

## Scénario du site de référence &quot;Freedom of Information Act&quot; {#reference-site-freedom-of-information-act-scenario}

We.Gov est une organisation gérée par l&#39;État qui permet aux parents adoptifs de s&#39;inscrire à une allocation familiale s&#39;ils ont adopté un enfant. We.Gov permet également aux parents de demander des informations aux services gouvernementaux suivants en vertu de la loi sur la liberté d&#39;information :

* Defense Logistics Agency
* Ministère de la Défense Bureau de l&#39;Inspecteur général
* Ministère de la Justice - Bureau de la politique de l&#39;information
* Département de la Marine
* Agence de protection de l&#39;environnement

Pour plus d’informations sur la loi sur l’accès à l’information, voir [https://www.foia.gov/](https://www.foia.gov).

Le scénario implique les personnages suivants :

* Sarah Rose, personne demandant des informations
* John Jacobs, la personne qui gère la demande la transfère au service approprié.
* Gloria Rios, la fonctionnaire du gouvernement qui fournit les informations conformément à la demande

## Sarah lance une demande d’informations sous FOIA {#sarah-initiates-request-for-information-under-foia}

En vertu de la loi sur l’accès à l’information, Sarah demande une copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016. Sarah envoie cette demande au Ministère de la Justice - Bureau de la politique de l’information et indique également qu’elle peut payer jusqu’à 100 USD pour les frais d’impression et de poste.

### Fonctionnement {#how-it-works}

### Démonstration {#see-it-yourself}

Dans votre navigateur, ouvrez `https://<hostname>:<PublishPort>/wegov`. Sur le site We.Gov, appuyez sur Applications> Toutes les applications. Dans la page Toutes les applications, appuyez sur Appliquer sous Application dans le cadre de la loi sur l’accès à l’information.

## Sarah commence sa demande d’informations dans le cadre de la loi sur l’accès à l’information {#sarah-starts-her-application-for-information-under-foia}

Sarah clique sur **Appliquer** et sur la page Formulaire de demande dans le cadre de la Loi sur l’accès à l’information, Sarah saisit les informations suivantes :

* **Agence** : Sarah précise l’agence à laquelle la demande a été adressée : Ministère de la Justice - Bureau de la politique de l’information.

* **Payera jusqu&#39;à**: Sarah indique qu’elle est prête à payer jusqu’à 100 USD pour les frais d’impression et de poste.
* **Décrire la demande en détail** : Sarah indique « Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016. »

![Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016](assets/sarahfiosform.png)

Demande de copie des registres des cas de l’Administration pour les enfants et les familles pour les années 2013 à 2016

Sarah peut appuyer à tout moment **Enregistrer** pour enregistrer un brouillon du formulaire et y revenir ultérieurement pour remplir le formulaire et l’envoyer. Sarah envoie le formulaire.

>[!NOTE]
>
>Le workflow de reprise à partir d’un courrier électronique fonctionne uniquement avec les utilisateurs connectés. Dans le scénario du site de référence, assurez-vous que l’utilisateur Sarah Rose est ajouté. Les informations de connexion de Sarah sont `srose/password`.

## John Jacobs reçoit et approuve la demande {#john-jacobs-receives-and-approves-the-application}

John Jacobs reçoit la demande et l’achemine vers la bonne personne. AEM Boîte de réception permet à John d’afficher toutes les demandes envoyées au même endroit.

### Fonctionnement {#how-it-works-1}

Lorsque Sarah remplit et envoie la demande d’accès à l’information, un enregistrement de la demande est envoyé à la boîte de réception de John Jacobs. John Jacobs peut afficher la demande envoyée et l’accepter ou la refuser.

### Démonstration {#see-it-yourself-1}

Vous pouvez accéder à AEM boîte de réception à l’adresse https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Connectez-vous à la boîte de réception d’AEM, à l’aide de jjacobs/password comme nom d’utilisateur/mot de passe pour John Jacobs, et consultez l’application FOIA. Pour plus d’informations sur l’utilisation de la boîte de réception AEM pour les tâches du workflow relatives aux formulaires, voir [Gérer des applications et des tâches Forms dans la boîte de réception AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs peut voir, approuver ou rejeter la demande depuis le tableau de bord de la demande. John Jacobs sélectionne et ouvre les détails de la demande, puis, après avoir examiné la demande, l’approuve.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah reçoit un courrier électronique d’acquittement</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Une fois que John Jacobs a approuvé la demande, Sarah reçoit un courrier électronique d’accusé de réception du site We.Gov. Sarah est informée des frais et du temps requis pour traiter sa demande. Le courrier électronique contient également les informations par courrier électronique et par téléphone que Sarah peut contacter pour obtenir des informations sur sa demande.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria reçoit la demande d’approbation de second niveau de la loi sur l’accès à l’information {#gloria-receives-the-foia-request-for-second-level-approval}

Une fois que John Jacobs a rempli les informations requises et approuvé la demande de Sarah, elle est envoyée à Gloria Rios pour l’approbation finale. Gloria examine le document d’enregistrement joint et approuve la demande.

![gloriariosinbox](assets/gloriariosinbox.png)

### Fonctionnement {#how-it-works-2}

Lorsque John Jacobs approuve la demande de la loi sur l’accès à l’information, un PDF ou un document d’enregistrement de la demande est créé et envoyé à la boîte de réception de Gloria Rios. Gloria peut afficher la demande envoyée et l’accepter ou la refuser.

### Jugez-en par vous-même {#see-for-yourself}

Vous pouvez accéder à AEM boîte de réception à l’adresse https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Connectez-vous à la boîte de réception AEM à l’aide de grios/password (nom d’utilisateur/mot de passe) pour Gloria Rios, puis consultez la demande FOIS.

Gloria ouvre la demande et examine les détails de la demande de la loi sur l’accès à l’information. Après avoir examiné les détails de la demande et vérifié la faisabilité de la remise des documents requis, Gloria approuve la demande.

![gloriariosapprove](assets/gloriariosapproves.png)

## Sarah reçoit une notification l’informant que sa demande est approuvée {#sarah-receives-notification-that-her-request-is-approved}

Après que Gloria a approuvé la demande d’accès à l’information, Sarah reçoit un courrier électronique l’informant que sa demande est approuvée. Le courrier électronique contient également des informations sur le calendrier provisoire de remise du document et les coordonnées de contact pour le suivi de la demande.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
