---
title: Enregistrement en tant qu’utilisateur
seo-title: Registering as a User
description: Découvrez comment utiliser les documents protégés par une stratégie que vous recevez d’un utilisateur de Document Security, même si vous êtes externe à l’organisation de l’utilisateur.
seo-description: Learn how you can use policy-protected documents that you receive from an document security user, even if you are external to the user’s organization.
uuid: 4648b358-f545-434f-a3b2-2937e961dc64
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 26e11ef4-9f8f-4b0b-b035-a498fd7d65ef
feature: Document Security
exl-id: 320d8fa4-e200-4993-b018-a9718cddc5c1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 7%

---

# Enregistrement en tant qu’utilisateur {#registering-as-a-user}

Vous pouvez utiliser des documents protégés par une stratégie que vous recevez d’un utilisateur de Document Security, même si vous êtes externe à l’organisation de l’utilisateur. Pour utiliser un document protégé par une stratégie, vous devez vous enregistrer auprès de Document Security. Si vous n’avez pas déjà été invité à vous enregistrer, Document Security lance le processus d’enregistrement lorsque ces événements se produisent :

* Un utilisateur Document Security qui souhaite vous envoyer un document protégé par une stratégie vous ajoute à une stratégie.
* Un administrateur de Document Security crée un compte à votre place.

  Après vous être enregistré et avoir activé votre compte, vous pouvez utiliser des documents protégés par une stratégie que vous êtes autorisé à utiliser par le biais d’une stratégie. Si l’administrateur Document Security active ces fonctionnalités pour les utilisateurs invités, vous pouvez être autorisé à effectuer les tâches suivantes :

* Documents Protect à l’aide de stratégies Document Security.
* Créez vos propres stratégies utilisateur que vous pouvez appliquer à vos documents.
* Invitez d’autres utilisateurs externes à utiliser un document protégé par une stratégie en l’ajoutant à la stratégie.

  En outre, lorsque vous vous enregistrez, il n’est pas nécessaire de vous réenregistrer pour utiliser d’autres documents protégés par une stratégie. Votre compte reste actif jusqu’à ce qu’un administrateur de stratégie le désactive ou le supprime.

>[!NOTE]
>
>Si vous recevez un document protégé par une stratégie, mais ne recevez pas d’invitation par courrier électronique d’enregistrement, contactez la personne qui vous a envoyé le document pour plus d’informations.

## Enregistrement en tant qu’utilisateur invité {#register-as-an-invited-user}

Si vous êtes un utilisateur invité et que vous recevez un message d’enregistrement par courrier électronique de Document Security, vous pouvez vous enregistrer à l’aide de l’URL contenue dans le message pour ouvrir la page d’enregistrement en ligne. Une fois enregistré, vous recevrez un second e-mail concernant l’activation de votre compte.

1. Ouvrez le courrier électronique d’enregistrement de Document Security. L’URL contenue dans le message est un lien vers la page Enregistrement des utilisateurs externes de Document Security.
1. Cliquez sur l’URL ou copiez-la et collez-la dans votre navigateur. La page Enregistrement des utilisateurs externes s’affiche.
1. Saisissez vos nom, numéro de téléphone, adresse, organisation et mot de passe dans les zones appropriées, puis saisissez à nouveau votre mot de passe dans la zone Confirmer le mot de passe . Votre mot de passe peut constituer n’importe quelle combinaison de huit caractères.
1. Cliquez sur Enregistrer. Un message de remerciement s’affiche et vous informe de vérifier que votre email contient un message d’activation. Vous devez maintenant activer votre compte pour terminer le processus d’enregistrement.

## Activation de votre compte d’utilisateur invité {#activate-your-invited-user-account}

Une fois enregistré, Document Security vous envoie un courrier électronique d’activation. Vous devez activer votre compte à l&#39;aide de l&#39;URL contenue dans le message. Vous pouvez ensuite vous connecter à Document Security pour utiliser les documents protégés par une stratégie auxquels vous avez accès. Selon les fonctionnalités activées par l’administrateur pour les utilisateurs externes, vous pouvez être autorisé à créer des stratégies, à appliquer des stratégies à des documents et à ajouter d’autres utilisateurs externes à vos stratégies.

Votre compte reste actif jusqu’à ce que l’administrateur le désactive ou le supprime.

1. Ouvrez l’e-mail de confirmation d’enregistrement de Document Security.
1. Cliquez sur l’URL qui apparaît dans le message. La page d’activation de Document Security s’affiche.
1. Cliquez sur le mot Ici pour accéder à la page de connexion.
1. Dans la zone Nom d’utilisateur, saisissez l’adresse électronique à l’aide de laquelle vous vous êtes enregistré auprès de Document Security. Cette adresse électronique est votre nom d’utilisateur Document Security par défaut.
1. Dans la zone Password, saisissez le mot de passe que vous avez créé lors de votre enregistrement, puis cliquez sur Login.

## Réinitialisation de votre mot de passe {#reset-your-password}

Si vous oubliez votre mot de passe, l’administrateur de stratégie peut le réinitialiser à votre place. La réinitialisation d’un mot de passe génère un courrier électronique qui vous invite à vous connecter à l’aide d’un mot de passe temporaire. Vous pouvez ensuite créer un autre mot de passe.

Pour plus d’informations sur les contacts avec un administrateur de Document Security afin d’obtenir un nouveau mot de passe, vérifiez votre avis par courrier électronique d’activation ou d’autres avis de l’entreprise qui vous a invité à vous enregistrer.

1. Indiquez à l’administrateur de stratégie que vous avez besoin d’un nouveau mot de passe.
1. Lorsque vous recevez le courrier électronique de mot de passe de Document Security, ouvrez-le et obtenez votre nouveau mot de passe temporaire.
1. Connectez-vous à Document Security à l’aide du nouveau mot de passe temporaire.
1. Cliquez sur Options dans le coin supérieur droit de la page. La page Utilisateurs externes s’affiche.
1. Sélectionnez Modifier le mot de passe et saisissez le mot de passe temporaire dans la zone Ancien mot de passe .
1. Dans la zone Nouveau mot de passe, saisissez un nouveau mot de passe, puis saisissez-le à nouveau dans la zone Confirmer le mot de passe .
