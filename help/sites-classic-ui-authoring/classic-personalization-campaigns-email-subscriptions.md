---
title: Gérer les abonnements
description: Les utilisateurs et utilisatrices peuvent être invités à s’abonner à des listes de diffusion de fournisseurs de services de messagerie à l’aide du composant Formulaire utilisé sur une page Web AEM. Pour préparer une page AEM avec un formulaire d’abonnement à des listes de diffusion d’un service de messagerie, appliquez la configuration de service correspondante à la page AEM que consultera l’abonné(e) potentiel(le).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 52%

---

# Gérer les abonnements{#managing-subscriptions}

>[!NOTE]
>
>Adobe ne prévoit pas d’optimiser cette fonctionnalité (Gestion des prospects et des listes).
>Il est recommandé d’utiliser [Adobe Campaign et son intégration AEM](/help/sites-administering/campaign.md).

Les utilisateurs peuvent être invités à s’abonner à des listes de publipostage de **fournisseurs de services de messagerie** à l’aide du composant **Formulaire** utilisé sur une page Web AEM. Pour préparer une page AEM avec un formulaire d’abonnement à des listes de diffusion d’un service de messagerie, appliquez la configuration de service correspondante à la page AEM que consultera l’abonné potentiel.

## Application de la configuration du service de messagerie à une page {#applying-email-service-configuration-to-a-page}

Pour configurer une page AEM :

1. Accédez au **Sites web** .
1. Sélectionnez la page qui doit être configurée pour le service. Cliquez sur la page avec le bouton droit de la souris et sélectionnez **Propriétés**.

1. Sélectionnez **Services cloud**, puis **Ajouter un service**. Sélectionnez une configuration dans la liste des configurations disponibles.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Cliquez sur **OK**.

## Création d’un formulaire d’inscription sur une page AEM pour s’abonner/se désabonner à des listes {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Pour créer un formulaire d’inscription et le configurer pour les abonnements aux listes de messagerie du fournisseur de services de messagerie :

1. Ouvrez la page AEM que l’utilisateur va consulter.
1. Appliquez la configuration du fournisseur de services de messagerie à la page.

1. Ajoutez un composant **Formulaire** à la page en le faisant glisser à partir du sidekick. Si le composant n’est pas disponible, basculez en mode de conception et activez le groupe **Formulaire**.
1. Cliquez sur **Modifier** dans la barre **Début du formulaire** et accédez à l’onglet **Avancé**.
1. Dans le menu déroulant **Formulaire**, sélectionnez **Service de messagerie électronique : créer un abonné** et l’ajouter à la liste.
1. Au bas de la boîte de dialogue, ouvrez le **Configuration d’action** qui permet de sélectionner une ou plusieurs listes d&#39;abonnements.
1. Dans la liste **Sélectionner, choisissez la liste** à laquelle vous souhaitez que les utilisateurs s’abonnent. Vous pouvez ajouter plusieurs listes à l’aide du bouton plus (**Ajouter un élément**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >Votre boîte de dialogue peut varier en fonction du fournisseur de services de messagerie.

1. Dans le **Formulaire** sélectionnez la page de remerciement à laquelle doivent accéder les utilisateurs après avoir envoyé le formulaire (si rien n’est indiqué, le formulaire s’affiche de nouveau lors de l’envoi.) Cliquez sur **OK**. Un **Email id** s’affiche dans le formulaire, ce qui vous permet de créer un formulaire dans lequel les utilisateurs peuvent envoyer leurs adresses électroniques pour s’abonner ou se désabonner d’une liste de diffusion.
1. Ajoutez le composant de bouton **Envoyer** dans la section **Formulaire** du sidekick.

   Le formulaire est prêt. Publiez la page configurée dans les étapes ci-dessus avec le **merci** vers l’instance de publication. Tout abonné potentiel qui consulte la page peut remplir le formulaire et s’abonner à la liste fournie dans la configuration.

   >[!NOTE]
   >
   >Pour que l&#39;abonnement au formulaire fonctionne correctement, [les clés de chiffrement de l’auteur doivent être exportées et importées sur l’instance de publication.](#exporting-keys-from-author-and-importing-on-publish).

## Exportation de clés à partir de l’auteur et importation sur publication {#exporting-keys-from-author-and-importing-on-publish}

Pour que l’abonnement et le désabonnement au service de messagerie fonctionnent via le formulaire d’inscription sur l’instance de publication, vous devez procéder comme suit :

1. Sur l’instance d’auteur, accédez au gestionnaire de modules.
1. Créez un package. Définissez le filtre en tant que `/etc/key`.
1. Créez et téléchargez le package.
1. Accédez au gestionnaire de modules sur l’instance de publication et téléchargez ce module.
1. Accédez à la console Publier OSGi et redémarrez le lot nommé **Prise en charge du chiffrement Adobe**.

## Désabonnement des utilisateurs des listes {#unsubscribing-users-from-lists}

Pour désabonner les utilisateurs des listes :

1. Ouvrez les propriétés de page de la page AEM qui comporte le formulaire d’inscription pour désabonner une piste.
1. Appliquez la configuration du service à la page.
1. Créez un formulaire d’inscription sur la page.
1. Pendant la configuration du composant, sélectionnez l’action **Service de messagerie électronique** : **désabonner l’utilisateur de la liste.**
1. Dans le menu déroulant, sélectionnez la liste de laquelle l’utilisateur sera supprimé lors du désabonnement.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exportez les clés de l’instance de création vers l’instance de publication.

## Configuration des messages de répondeur automatique pour le service de messagerie {#configuring-auto-responder-emails-for-email-service}

Pour configurer un message de répondeur automatique pour un abonné :

1. Ouvrez la page des propriétés de la page AEM qui contient le formulaire d’inscription pour configurer le répondeur automatique pour un prospect.
1. Appliquez la configuration ExactTarget à la page.

1. Ajoutez un composant **Formulaire** à la page en le faisant glisser à partir du sidekick. Si le composant n’est pas disponible, basculez vers le mode de conception et activez le groupe **Formulaire**.
1. Cliquez sur **Modifier** dans la barre **Début du formulaire** et accédez à l’onglet **Avancé**.
1. Dans le menu déroulant **Formulaire**, sélectionnez **Service de messagerie électronique : envoyer un message de répondeur automatique.**
1. **Sélectionnez un e-mail** (il s’agit de l’e-mail envoyé en tant que message de répondeur automatique).

1. **Sélectionnez une classification** (cette classification est utilisée pour envoyer le e-mail).
1. Sélectionnez la page de **remerciement** (il s’agit de la page vers laquelle les utilisateurs sont redirigés après avoir envoyé le formulaire).

   Dans l’onglet **Formulaire**, sélectionnez la page de remerciement à laquelle doivent accéder les utilisateurs après avoir envoyé le formulaire. (Si aucune donnée n’est saisie, le formulaire s’affiche à nouveau lors de l’envoi.) Cliquez sur **OK**.

1. Exportez les clés de l’instance de création vers l’instance de publication.
1. Ajoutez le composant de bouton **Envoyer** dans la section **Formulaire** du sidekick.

   Le formulaire d’inscription est prêt. Publiez la page configurée dans les étapes ci-dessus avec le **merci** vers l’instance de publication. Tout abonné potentiel qui consulte la page peut remplir le formulaire et, lors de l’envoi du formulaire, le visiteur recevra un message de répondeur automatique sur l’ID de message électronique renseigné dans le formulaire.

   >[!NOTE]
   >
   >Pour que l&#39;abonnement au formulaire d&#39;inscription fonctionne correctement, [les clés de chiffrement de l’auteur doivent être exportées et importées sur l’instance de publication.](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
