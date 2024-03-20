---
title: Publier un e-mail sur des services de messagerie
description: Vous pouvez diffuser des newsletters sur des services de messagerie, tels qu’ExactTarget et Silverpop Engage.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 97%

---

# Publier un e-mail sur des services de messagerie{#publishing-an-email-to-email-service-providers}

Vous pouvez diffuser des newsletters sur des services de messagerie, tels qu’ExactTarget et Silverpop Engage. Ce document décrit comment configurer AEM pour publier une newsletter sur ces services de messagerie.

>[!NOTE]
>
>Vous devez configurer le fournisseur de services avant de créer et de publier un e-mail. Consultez [Configuration d’ExactTarget](/help/sites-administering/exacttarget.md) et [Configuration de Silverpop Engage](/help/sites-administering/silverpop.md) pour plus d’informations.

Pour publier votre e-mail auprès du fournisseur de services de messagerie, vous devez effectuer les étapes suivantes :

1. Créez un e-mail.
1. Appliquez la configuration du service de messagerie à cet e-mail. 
1. Publiez l&#39;e-mail.

>[!NOTE]
>
>Si vous mettez à jour les fournisseurs de messagerie, effectuez un test en ligne ou envoyez une newsletter. Ces opérations échouent si la newsletter n’est pas publiée au préalable sur l’instance de publication ou si l’instance de publication n’est pas disponible. Veillez à publier votre newsletter et à ce que l’instance de publication soit en cours d’exécution.

## Créer un e-mail {#creating-an-email}

Un e-mail ou une newsletter que vous souhaitez diffuser sur un service de messagerie, tel qu’ExactTarget, peut être créé(e) sous une campagne, à l’aide du modèle **Newsletter Geometrixx**. Vous pouvez également utiliser le modèle **E-mail Geometrixx Outdoors**. L’exemple d’e-mail ou de newsletter basé sur le modèle **E-mail Geometrixx Outdoors** est disponible à l’adresse suivante : `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

Pour créer un email publié sur le service de messagerie configuré :

1. Sélectionnez **Sites web**, puis **Campagnes**. Sélectionnez une campagne.
1. Cliquez sur **Nouveau** pour ouvrir la fenêtre **Créer une page**.
1. Saisissez le titre, le nom et sélectionnez le modèle **Newsletter Geometrixx** dans la liste des modèles disponibles.
1. Cliquez sur **Créer**.
1. Ouvrez l&#39;e-mail créé.
1. Basculez vers le mode de conception pour sélectionner les composants à afficher dans le sidekick.
1. Basculez en mode d’édition et commencez à ajouter du contenu (texte, images, [outils de messagerie électronique](#adding-exacttarget-email-tools-to-your-email), [variables de personnalisation](#adding-text-and-personalization-tool-to-your-e-mail), etc.) à votre e-mail.

### Ajout d’outils de messagerie ExactTarget à votre e-mail {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>Cette section est spécifique au service ExactTarget.

Le composant **Outils de messagerie électronique** pour ExactTarget permet d’ajouter des fonctionnalités de messagerie à votre e-mail ou votre newsletter.

1. Ouvrez un e-mail à publier sur ExactTarget.
1. Ajoutez le composant **ET – Outils de messagerie électronique** à votre page à l’aide du sidekick. Ouvrez le composant en mode d’édition.

   ![chlimage_1](assets/chlimage_1.gif)

1. Sélectionnez une option dans le menu **Options** :

<table>
 <tbody>
  <tr>
   <td>Adresse postale physique (requise)</td>
   <td>Ce composant insère l’adresse postale physique de votre organisation dans l’e-mail.</td>
  </tr>
  <tr>
   <td>Centre de profils (requis)</td>
   <td>Le centre de profils est une page web où les personnes abonnées peuvent saisir et gérer les informations personnelles que vous conservez à leur sujet.</td>
  </tr>
  <tr>
   <td>Afficher l’e-mail sous forme d’une page web</td>
   <td>Ce composant permet à l’utilisateur ou l’utilisatrice d’afficher l’e-mail sous la forme d’une page web.</td>
  </tr>
  <tr>
   <td>Politique de confidentialité</td>
   <td>Ce composant insère le lien vers votre politique de confidentialité dans l'e-mail.<br /> </td>
  </tr>
  <tr>
   <td>Centre de désabonnement</td>
   <td>Permet à l’utilisateur ou l’utilisatrice de se désabonner de votre liste de publipostage.</td>
  </tr>
  <tr>
   <td>Centre d’abonnement</td>
   <td>Un centre d’abonnement est une page Web dans laquelle les abonnés peuvent contrôler les messages qu’ils reçoivent de votre entreprise.</td>
  </tr>
  <tr>
   <td>Suivre les ouvertures d’e-mail</td>
   <td>Composant masqué qui vous permet d’utiliser la fonctionnalité de suivi d’ExactTarget.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Des valeurs ne sont renseignées dans le menu déroulant **Options** que si la configuration d’ExactTarget est appliquée à l’e-mail. Consultez [Application de la configuration de service de messagerie aux paramètres d’e-mail](#applying-e-mail-service-configuration-to-e-mail-settings) pour plus d’informations.

1. Publiez l&#39;e-mail sur ExactTarget.

   L&#39;e-mail contenant les outils de messagerie peut être utilisé dans le compte ExactTarget configuré.

>[!NOTE]
>
>* Les URL renseignées dans les outils de messagerie sont remplacées (dans l’e-mail reçu) par leurs valeurs réelles seulement si l’e-mail est envoyé à l’aide de l’option **Envoi simple** ou **Envoi guidé**, mais pas **Envoi de test**.
>
>* Deux des outils de messagerie sont requis : **Adresse postale physique (requise)** et **Centre de profils (requis)**. Lorsque l&#39;e-mail est publié sur ExactTarget, ces deux outils de messagerie sont ajoutés par défaut au bas de chaque message.
>

### Ajout de l’outil Texte et personnalisation à votre e-mail {#adding-text-and-personalization-tool-to-your-e-mail}

Vous pouvez ajouter des champs personnalisés dans un e-mail en ajoutant le composant **Texte et personnalisation** à la page :

1. Ouvrez l’e-mail à publier sur votre service de messagerie.
1. Pour activer le champ de personnalisation de votre service de messagerie, ajoutez la configuration du framework lors de la configuration du service de messagerie. Consultez [Configuration de Silverpop Engage](/help/sites-administering/silverpop.md) et [Configuration d’ExactTarget](/help/sites-administering/exacttarget.md) pour plus d’informations.
1. Ajoutez le composant **Texte et personnalisation** à partir du sidekick. Ce composant fait partie du groupe de newsletter. Ouvrez ce composant en mode d’édition.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. Ajoutez au texte le champ personnalisé nécessaire en le sélectionnant dans le menu contextuel et en cliquant sur **Insérer**.
1. Cliquez sur **OK** pour terminer.

## Application de la configuration du service de messagerie aux paramètres d’e-mail {#applying-e-mail-service-configuration-to-e-mail-settings}

Pour appliquer la configuration de votre service de messagerie à une newsletter :

1. Créez une configuration de service de messagerie.
1. Ouvrez votre e-mail ou newsletter.
1. Ouvrez les paramètres de l’e-mail ou de la newsletter en cliquant sur **Paramètres** ou sur **Propriétés de page** dans le sidekick.
1. Cliquez sur **Ajouter un service** dans l&#39;onglet **Services cloud**. La liste des services s’affiche. Sélectionnez la configuration requise, **ExactTarget** ou **Silverpop**, dans le menu déroulant.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. Cliquez sur **OK**.

## Publication d’e-mails sur le service de messagerie {#publishing-emails-to-email-service}

Les e-mails/newsletters peuvent être publiés sur votre service de messagerie en procédant comme suit :

1. Ouvrez l&#39;e-mail.
1. Avant de publier un e-mail, vérifiez que vous avez appliqué la configuration correcte à celui-ci.
1. Cliquez sur **Publier**. Vous accédez alors à la fenêtre **Publier la newsletter dans le fournisseur de service d’e-mail**.
1. Renseignez le champ **Nom de la newsletter** L&#39;e-mail et la newsletter sont publiés sur le fournisseur de services de messagerie avec ce nom. Si aucun nom n’est indiqué, l’e-mail est publié avec le nom de la page de la newsletter défini dans AEM.
1. Cliquez sur **Publier**. 

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   Si la publication se déroule correctement, AEM confirme que vous pouvez afficher l’e-mail dans ExactTarget ou Engagement Silverpop.

   S’il existe ExactTarget, l’email publié peut être consulté en cliquant sur **Afficher le courrier électronique publié**. Vous accédez alors directement à la newsletter publiée dans ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/).).

>[!NOTE]
>
>Si un e-mail et une newsletter sont publiés avec le même nom que celui d’un e-mail et d’une newsletter déjà publiés, l&#39;e-mail et la newsletter précédents ne sont pas remplacés. Au lieu de cela, un nouvel e-mail et une nouvelle newsletter sont créés avec le même nom (les identifiants de deux newsletters seront toutefois différents).
>
>La publication de l&#39;e-mail et de la newsletter sur le fournisseur de services de messagerie les publie également sur l’instance de publication AEM.
>

### Mise à jour d’un e-mail publié {#updating-a-published-e-mail}

Le bouton **Mise à jour** de la boîte de dialogue Publier vous permet de mettre à jour une newsletter déjà publiée sur un service de messagerie. Si la newsletter n’est pas encore publiée et que vous cliquez sur le bouton **Mise à jour**, un message **Newsletter non publiée** s’affiche.

Pour mettre à jour un e-mail publié :

1. Ouvrez l’e-mail ou la newsletter déjà publié(e) sur un service de messagerie que vous souhaitez republier après l’avoir mis(e) à jour.
1. Cliquez sur **Publier**. La fenêtre **Publier la newsletter dans le fournisseur de service d’e-mail** s’ouvre. Cliquez sur **Mettre à jour**.

   Pour vérifier si la newsletter a été mise à jour dans ExactTarget, cliquez sur le bouton **Afficher l’e-mail publié**. Vous accédez alors à l&#39;e-mail publié dans ExactTarget.

   Pour vérifier si l&#39;e-mai et la newsletter ont été mis à jour sur le service de messagerie Silverpop, rendez-vous sur le site Silverpop Engage.
