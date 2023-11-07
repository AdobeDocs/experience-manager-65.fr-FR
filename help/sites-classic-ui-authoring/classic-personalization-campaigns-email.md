---
title: Marketing par e-mail
description: Le marketing par e-mail (par exemple, les newsletters) est une partie importante de toute campagne marketing, car vous l’utilisez pour envoyer du contenu à vos prospects. Dans AEM, vous pouvez créer des newsletters à partir de contenu AEM existant et ajouter un nouveau contenu, spécifique aux newsletters.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1764'
ht-degree: 92%

---


# Marketing par e-mail{#e-mail-marketing}

>[!NOTE]
>
>Adobe ne prévoit pas de continuer à mettre à jour le suivi des ouvertures et rebonds des e-mails (non livrable) envoyé par le service SMTP AEM.
>Il est recommandé d’utiliser [Adobe Campaign et intégration à AEM](/help/sites-administering/campaign.md).

Le marketing par e-mail (par exemple, les newsletters) est une partie importante de toute campagne marketing, car vous l’utilisez pour envoyer du contenu à vos prospects. Dans AEM, vous pouvez créer des newsletters à partir de contenu AEM existant et ajouter un nouveau contenu, spécifique aux newsletters.

Une fois créées, vous pouvez envoyer les newsletters à des groupes spécifiques d’utilisateurs immédiatement ou à un autre moment planifié (à l’aide d’un workflow). En outre, les utilisateurs et utilisatrices peuvent s’abonner à des newsletters au format de leur choix.

De plus, AEM vous permet d’administrer la fonctionnalité de newsletter, notamment la gestion des thèmes, l’archivage des newsletters et l’affichage des statistiques sur les newsletters.

>[!NOTE]
>
>Dans Geometrixx, le modèle de newsletter ouvre automatiquement l’éditeur d’e-mail. Vous pouvez utiliser l’éditeur d’e-mail dans d’autres modèles dans lesquels vous souhaitez envoyer des e-mails, par exemple des invitations. L’éditeur d’e-mail s’affiche chaque fois qu’une page est héritée de **mcm/components/newsletter/page**.

Ce document décrit les principes de base de la création de newsletters dans AEM. Pour plus d’informations sur l’utilisation du marketing par e-mail, consultez les documents suivants :

* [Création d’une page de destination efficace pour une newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [Gestion des abonnements](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [Publication d’un e-mail sur des services de messagerie](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [Suivi des e-mails rejetés](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>Si vous mettez à jour les fournisseurs de messagerie, effectuez un test en ligne ou envoyez une newsletter. Ces opérations échouent si la newsletter n’est pas publiée au préalable sur l’instance de publication ou si l’instance de publication n’est pas disponible. Veillez à publier votre newsletter et à ce que l’instance de publication soit en cours d’exécution.

## Création d’une expérience de newsletter {#creating-a-newsletter-experience}

>[!NOTE]
>
>Les notifications par e-mail doivent être configurées via la configuration osgi. Voir [Configuration des notifications par e-mail.](/help/sites-administering/notification.md)

1. Sélectionnez votre nouvelle campagne dans le volet de gauche ou double-cliquez dans le volet de droite.

1. Sélectionnez la vue Liste à l’aide de l’icône :

   ![Icône Mode Liste](do-not-localize/mcm_icon_listview-1.png)

1. Cliquez sur **Nouveau...**

   Vous pouvez indiquer le **Titre**, le **Nom** et le type d’expérience à créer ; dans ce cas, Newsletter.

   ![Boîte de dialogue Créer une expérience](assets/mcm_createnewsletter.png)

1. Cliquez sur **Créer**.

1. Une nouvelle boîte de dialogue s’ouvre immédiatement. Vous pouvez y saisir les propriétés de la newsletter.

   **Liste des destinataires par défaut** est un champ obligatoire, dans la mesure où il s’agit du point de contact pour la newsletter (pour plus d’informations sur les listes, voir [Utilisation de listes](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)).

   ![Boîte de dialogue Propriétés de la page](assets/mcm_newnewsletterdialog.png)

   * **Nom de l’expéditeur**
Nom qui doit apparaître comme celui de l’expéditeur de la newsletter.

   * **Adresse de l’expéditeur**
Adresse électronique qui doit apparaître comme celle de l’expéditeur de la newsletter.

   * **Objet**
Objet de la newsletter.

   * **Répondre à**
Adresse électronique pour le traitement des réponses à la newsletter envoyée.

   * **Description**
Description de la newsletter.

   * **Heure d’activation**
Heure d’activation pour l’envoi de la newsletter.

   * **Liste des destinataires par défaut**
Liste par défaut des destinataires qui doivent recevoir la newsletter.

   Elles peuvent être mises à jour ultérieurement à partir de la boîte de dialogue **Propriétés...**.

1. Cliquez sur **OK** pour enregistrer.

## Ajout de contenu aux newsletters {#adding-content-to-newsletters}

Vous pouvez ajouter du contenu, y compris du contenu dynamique, à votre newsletter comme vous le feriez dans n’importe quel composant AEM. Dans Geometrixx, certains composants du modèle de newsletter sont disponibles pour l’ajout et la modification de contenu dans les newsletters.

1. Dans le MCM, cliquez sur l’onglet **Campagnes** et double-cliquez sur la newsletter à laquelle vous souhaitez ajouter du contenu ou que vous souhaitez modifier. La newsletter s’ouvre.

1. Si les composants ne sont pas visibles, accédez à la vue Conception et activez les composants nécessaires (par exemple, les composants Newsletter) avant de commencer la modification.
1. Saisissez le texte, les images ou d’autres composants appropriés. Dans l’exemple de Geometrixx, 4 composants sont disponibles : Texte, Image, En-tête et 2 Colonnes. Votre newsletter peut comporter plus ou moins de composants selon la manière dont vous la configurez.

   >[!NOTE]
   >
   >Vous personnalisez des newsletters à l’aide de variables. Dans la newsletter Geometrixx, les variables sont disponibles dans le composant Texte. Les valeurs des variables sont héritées des informations du profil utilisateur.

   ![Modification du contenu d’une newsletter](assets/mcm_newsletter_content.png)

1. Pour insérer des variables, sélectionnez-en une dans la liste, puis cliquez sur **Insérer**. Les variables sont renseignées à partir du profil.

## Personnalisation des newsletters {#personalizing-newsletters}

Vous personnalisez les newsletters en insérant des variables prédéfinies dans le composant Texte des newsletters dans Geometrixx. Les valeurs des variables sont héritées des informations du profil utilisateur.

Vous pouvez également simuler la manière dont une newsletter est personnalisée en utilisant le contexte client et en chargeant un profil.

Pour personnaliser une newsletter et simuler son aspect :

1. Dans MCM, ouvrez la newsletter dont vous souhaitez personnaliser les paramètres.

1. Ouvrez le composant Texte que vous souhaitez personnaliser.

1. Placez le curseur à l’endroit où vous souhaitez que la variable apparaisse, sélectionnez une variable dans la liste déroulante, puis cliquez sur **Insérer**. Effectuez cette opération pour autant de variables que nécessaire et cliquez sur **OK**.

   ![Ajouter des variables](assets/mcm_newsletter_variables.png)

1. Pour simuler l’aspect de la variable lorsqu’elle est envoyée, appuyez sur CTRL+ALT+c pour ouvrir le contexte client et sélectionnez **Chargement**. Sélectionnez l’utilisateur ou l’utilisatrice dans la liste dont vous souhaitez charger le profil, puis cliquez sur **OK**.

   Les informations du profil que vous avez chargé ont renseigné les variables.

   ![Test des variables](assets/mc_newsletter_testvariables.png)

## Test de newsletters dans divers clients de messagerie électronique {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>Avant d’envoyer des newsletters, vérifiez la configuration OSGi pour l’Externaliseur de lien Day CQ à l’adresse `https://localhost:4502/system/console/configMgr`.
>
>Par défaut, la valeur du paramètre est `localhost:4502` et l’opération ne peut pas être menée à bien en cas de modification du port d’exécution de l’instance.

Basculez entre les clients de messagerie courants pour afficher un aperçu de la newsletter telle qu’elle sera présentée à vos prospects. Par défaut, votre newsletter s’ouvre sans client de messagerie sélectionné.

Actuellement, vous pouvez afficher des newsletters dans les clients de messagerie suivants :

* Yahoo Mail
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple Mail

Pour basculer entre les clients, cliquez sur l’icône correspondante pour afficher la newsletter dans ce client de messagerie :

1. Dans MCM, ouvrez la newsletter dont vous souhaitez personnaliser les paramètres.

1. Cliquez sur un client de messagerie dans la barre supérieure pour voir à quoi ressemblerait la newsletter dans ce client.

   ![Changement de client de messagerie](assets/chlimage_1-119.png)

1. Répétez cette étape pour tout client de messagerie supplémentaire que vous voulez afficher.

   ![Modification des clients de messagerie](assets/chlimage_1-120.png)

## Personnalisation des paramètres de la newsletter {#customizing-newsletter-settings}

Bien que seules les personnes autorisées puissent envoyer une newsletter, vous devez personnaliser les éléments suivants :

* L’objet, pour que les utilisateurs et utilisatrices souhaitent ouvrir votre e-mail et pour s’assurer également que votre newsletter ne sera pas considérée comme un spam.
* L’adresse De, par exemple : `noreply@geometrixx.com`, de sorte que les utilisateurs reçoivent un e-mail d’une adresse spécifiée.

Pour personnaliser les paramètres de la newsletter :

1. Dans MCM, ouvrez la newsletter dont vous souhaitez personnaliser les paramètres.

   ![Ouverture d’une newsletter](assets/mcm_newsletter_open.png)

1. En haut de la newsletter, cliquez sur **Paramètres**.

   ![Modification des paramètres de newsletter](assets/mcm_newsletter_settings.png)
1. Saisissez l’adresse e-mail **De**.

1. Modifiez l’**objet** de l’e-mail, le cas échéant.

1. Sélectionnez une **Liste des destinataires par défaut** dans la liste déroulante.

1. Cliquez sur **OK**.

   Lorsque vous testez ou envoyez la newsletter, les destinataires et destinatrices reçoivent des e-mails avec l’adresse e-mail et l’objet spécifiés.

## Tests en ligne des newsletters {#flight-testing-newsletters}

Bien que les tests en ligne ne soient pas obligatoires, vous pouvez tester une newsletter avant de l’envoyer pour vous assurer qu’elle s’affiche comme vous le souhaitez.

Les tests en ligne permettent d’effectuer les opérations suivantes :

* Consultez la newsletter dans [tous les clients prévus](#testing-newsletters-in-different-e-mail-clients).
* Vérifiez que le serveur de messagerie est correctement configuré.
* Déterminez si votre e-mail est signalé comme spam. (Veillez à vous inclure dans la liste des destinataires ou destinatrices.)

>[!NOTE]
>
>Si vous mettez à jour les fournisseurs de messagerie, effectuez un test en ligne ou envoyez une newsletter. Ces opérations échouent si la newsletter n’est pas publiée au préalable sur l’instance de publication ou si l’instance de publication n’est pas disponible. Veillez à publier votre newsletter et à ce que l’instance de publication soit en cours d’exécution.

Pour tester les newsletters en ligne :

1. Dans MCM, ouvrez la newsletter que vous souhaitez tester et envoyer.

1. Dans la partie supérieure de la newsletter, cliquez sur **Test** pour effectuer un test avant l’envoi.

   ![Paramètres de test d’une newsletter](assets/mcm_newsletter_testsettings.png)

1. Saisissez l’adresse e-mail de test à laquelle vous souhaitez envoyer la newsletter, puis cliquez sur **Envoyer**. Si vous souhaitez modifier le profil, vous chargez un autre profil dans le contexte client. Pour ce faire, appuyez sur CTRL+ALT+c, sélectionnez Charger, puis chargez un profil.

## Envoi de newsletters {#sending-newsletters}

>[!NOTE]
>
>Adobe ne prévoit pas de continuer à mettre à jour le suivi des ouvertures et rebonds des e-mails (non livrable) envoyé par le service SMTP AEM.
>Il est recommandé d’utiliser [Adobe Campaign et intégration à AEM](/help/sites-administering/campaign.md).

Vous pouvez envoyer une newsletter à partir de la newsletter ou de la liste. Les deux procédures sont décrites.

>[!NOTE]
>
>Avant d’envoyer des newsletters, vérifiez la configuration OSGi pour l’Externaliseur de lien Day CQ à l’adresse `https://localhost:4502/system/console/configMgr`.
>
>Par défaut, la valeur du paramètre est `localhost:4502` et l’opération ne peut pas être menée à bien en cas de modification du port d’exécution de l’instance.

>[!NOTE]
>
>Si vous mettez à jour les fournisseurs de messagerie, effectuez un test en ligne ou envoyez une newsletter. Ces opérations échouent si la newsletter n’est pas publiée au préalable sur l’instance de publication ou si l’instance de publication n’est pas disponible. Veillez à publier votre newsletter et à ce que l’instance de publication soit en cours d’exécution.

### Envoi d’une newsletter à partir d’une campagne {#sending-newsletters-from-a-campaign}

Pour envoyer une newsletter à partir d’une campagne :

1. Dans MCM, ouvrez la newsletter à envoyer.

   >[!NOTE]
   >
   >Avant l’envoi, assurez-vous d’avoir personnalisé l’objet de la newsletter et l’adresse électronique de l’expéditeur en [personnalisant ses paramètres](#customizing-newsletter-settings).
   >
   >
   >Il est recommandé d’effectuer un [test envoi](#flight-testing-newsletters) de la newsletter avant de l’envoyer.

1. En haut de la newsletter, cliquez sur **Envoyer**. L’assistant de newsletter s’ouvre.

1. Dans la liste des destinataires et destinatrices, sélectionnez la liste de personnes à laquelle vous souhaitez envoyer la newsletter, puis cliquez sur **Suivant**.

   ![Envoi d’une newsletter](assets/mcm_newslettersend.png)

1. La fin de la configuration est confirmée. Cliquez sur **Envoyer** pour envoyer la newsletter.

   ![Confirmation d’envoi de la newsletter](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >Veillez à être l’un des destinataires ou l’une des destinatrices pour vérifier que la newsletter est bien reçue.

### Envoi de newsletters à partir d’une liste {#sending-newsletters-from-a-list}

Pour envoyer une newsletter à partir d’une liste :

1. Dans MCM, cliquez sur **Listes** dans le volet de gauche.

   >[!NOTE]
   >
   >Avant l’envoi, assurez-vous d’avoir personnalisé l’objet de la newsletter et l’adresse électronique de l’expéditeur en [personnalisant ses paramètres](#customizing-newsletter-settings). Vous ne pouvez pas tester une newsletter si vous l’envoyez à partir de la liste ; vous pouvez la [tester en ligne](#flight-testing-newsletters) si vous l’envoyez à partir de la newsletter.

1. Cochez la case en regard de la liste des prospects auxquels vous souhaitez envoyer la newsletter.

1. Dans le menu **Outils**, sélectionnez **Envoyer la newsletter**. La fenêtre **Envoyer la newsletter** s’ouvre.

   ![Console de newsletter](assets/mcm_newslettersendfromlist.png)

1. Dans le champ **Newsletter**, sélectionnez la newsletter que vous souhaitez envoyer, puis cliquez sur **Suivant**.

   ![Boîte de dialogue Envoyer la newsletter](assets/mcm_newslettersenddialog.png)

1. La fin de la configuration est confirmée. Cliquez sur **Envoyer** pour envoyer la newsletter sélectionnée à la liste spécifiée de prospects.

   ![Envoyer une confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   Votre newsletter est envoyée aux destinataires sélectionnés.

## Abonnement à une newsletter {#subscribing-to-a-newsletter}

Cette section décrit comment s’abonner à une newsletter.

### Abonnement à une newsletter {#subscribing-to-a-newsletter-1}

Pour vous abonner à une newsletter (en utilisant comme exemple le site web de Geometrixx) :

1. Cliquez sur **Sites web**, accédez à la **barre d’outils** Geometrixx et ouvrez-la.

   ![Exemple d&#39;abonnement](assets/chlimage_1-121.png)

1. Dans le champ **S&#39;abonner** de la newsletter Geometrixx, saisissez votre adresse e-mail et cliquez sur **S’abonner**. Votre abonnement à la newsletter est maintenant effectif.
