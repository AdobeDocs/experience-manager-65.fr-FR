---
title: Suivi des e-mails rejetés
description: Lorsque vous envoyez une newsletter à de nombreux utilisateurs et utilisatrices, la liste contient généralement des adresses e-mail non valides. L’envoi de newsletters à ces adresses génère un rebond. AEM est en mesure de gérer ces rebonds et d’arrêter l’envoi de newsletters vers ces adresses après le dépassement du compteur de rebonds.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 100%

---

# Suivi des e-mails rejetés{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe ne prévoit pas de continuer à améliorer le suivi des e-mails ouverts et des rebonds envoyés par le service SMTP AEM.
>
>Nous vous recommandons d’[exploiter Adobe Campaign et son intégration AEM](/help/sites-administering/campaign.md).

Lorsque vous envoyez une newsletter à de nombreux utilisateurs et utilisatrices, la liste contient généralement des adresses e-mail non valides. L’envoi de newsletters à ces adresses génère un rebond. AEM est en mesure de gérer ces rebonds et d’arrêter l’envoi de newsletters vers ces adresses après le dépassement du compteur de rebonds. Par défaut, le taux de rebonds est défini sur 3, mais cette valeur est configurable.

Pour qu’AEM effectue le suivi des e-mails rejetés, configurez-le pour qu’il interroge une boîte de messagerie dans laquelle arrivent les messages rejetés. En règle générale, cet emplacement correspond à l’adresse e-mail Expéditeur que vous indiquez pour l’envoi de la newsletter. AEM sonde cette boîte aux lettres et importe tous les messages sous le chemin indiqué dans la configuration de sondage. Un workflow est ensuite déclenché pour rechercher les adresses électroniques rejetées parmi les utilisateurs. La valeur de la propriété bounceCounter de l’utilisateur est mise à jour en conséquence. Une fois le nombre maximal de rebonds configuré dépassé, la personne est supprimée de la liste des newsletters.

## Configurer l’importateur de flux {#configuring-the-feed-importer}

L’importateur de flux vous permet d’importer de manière répétée du contenu provenant de sources externes dans votre référentiel. Avec cette configuration de l’importateur de flux, AEM recherche les mails rejetés dans la boîte de l’expéditeur ou de l’expéditrice.

Pour configurer l’importateur de flux pour le suivi des messages rejetés, procédez comme suit :

1. Dans **Outils**, sélectionnez l’importateur de flux.

1. Cliquez sur **Ajouter** pour créer une configuration.

   ![chlimage_1](assets/chlimage_1a.png)

1. Ajoutez une configuration en sélectionnant le type et en ajoutant des informations à l’URL d’interrogation afin de pouvoir configurer l’hôte et le port. Ajoutez en outre des paramètres spécifiques à l’e-mail et au protocole à la requête d’URL. Définissez la configuration pour qu’elle interroge au moins une fois par jour.

   Toutes les configurations nécessitent des informations sur les éléments suivants dans l’URL d’interrogation :

   `username` : nom d’utilisateur ou d’utilisatrice utilisé pour la connexion.

   `password` : mot de passe utilisé pour la connexion.

   En outre, selon le protocole, vous pouvez configurer certains paramètres.

   **Propriétés de configuration POP3 :**

   `pop3.leave.on.server` : permet d’indiquer si des messages doivent être laissés ou non sur le serveur. Définissez la valeur sur « true » pour laisser les messages sur le serveur et sur « false » dans le cas contraire. La valeur par défaut est « true ».

   **Exemples POP3 :**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Utilisation de pop3 sur SSL pour se connecter à GMail sur le port 995 avec user/secret, pour laisser les messages sur le serveur par défaut. |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propriétés de configuration IMAP :**

   Permet de définir des indicateurs à rechercher.

   `imap.flag.SEEN` :« false » pour les nouveaux messages ou les messages non consultés ; « true » pour les messages déjà lus.

   Voir [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) pour obtenir la liste complète des indicateurs.

   **Exemples IMAP :**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Utilisation d’IMAP sur SSL pour se connecter à GMail sur le port 993 avec user/secret. Obtention de nouveaux messages uniquement par défaut. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Utilisation d’IMAP sur SSL pour se connecter à GMail 993 avec user/secret, pour obtenir uniquement les messages déjà consultés. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Utilisation d’IMAP sur SSL pour se connecter à GMail 993 avec user/secret, pour obtenir des messages déjà lus OU des nouveaux messages. |

1. Enregistrez la configuration.

## Configurer le composant de service de newsletter {#configuring-the-newsletter-service-component}

Une fois que vous avez configuré l’importateur de flux, configurez l’adresse expéditeur et le compteur de rebonds.

Pour configurer le service de newsletter, procédez comme suit :

1. Entrez dans la console OSGi `<host>:<port>/system/console/configMgr` et accédez à **Newsletter MCM**.

1. Configurez le service et enregistrez les modifications une fois cette opération terminée.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   Définissez les configurations suivantes pour ajuster le comportement :

   | Compteur de rebond maximal (max.bounce.count) | Il définit le nombre de rebonds jusqu’à ce qu’une personne utilisatrice soit omise lors de l’envoi d’une newsletter. Définissez cette valeur sur 0 pour désactiver complètement la vérification des rebonds. |
   |---|---|
   | Activité sans cache (sent.activity.nocache) | Elle définit le paramètre de cache à utiliser pour l’activité d’envoi de newsletter. |

   Une fois enregistré, le service de newsletter MCM effectue les opérations suivantes :

   * il écrit une activité dans le flux masqué des personnes utilisatrices lors de l’envoi réussi d’une newsletter ;
   * il écrit une activité si un rebond est détecté et que le compteur de rebonds des personnes utilisatrices change.
