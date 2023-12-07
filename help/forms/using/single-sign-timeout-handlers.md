---
title: Authentification unique et gestionnaires de temporisation
description: Comment définir la valeur de délai d’expiration de session pour l’espace de travail AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 40%

---

# Authentification unique et gestionnaires de temporisation {#single-sign-on-and-timeout-handlers}

L’espace de travail AEM Forms est SSO activé. Si un utilisateur s’est connecté à une application AEM Forms telle que Forms Manager ou l’interface utilisateur du PDF Generator et a accès à l’espace de travail AEM Forms dans la même session de navigateur, il est alors connecté à l’espace de travail AEM Forms et inversement.

## Gestion du délai d’expiration du serveur dans l’espace de travail AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Le délai d’expiration de la session d’un utilisateur peut être configuré dans Administration Console.

Pour définir le délai d’expiration, connectez-vous à `https://'[server]:[port]'/adminui`, accédez à **Paramètres > User Management > Configuration > Configurer les attributs système avancés**, puis sélectionnez les paramètres souhaités.

Dans l’espace de travail AEM Forms, le délai d’expiration correspond à :

* la durée de disponibilité d’une session utilisateur en réponse à l’appel de commande `initialize` qui initialise la session utilisateur.
* Une boîte de dialogue contextuelle avertit l’utilisateur que la session est sur le point d’expirer, 15 secondes avant l’expiration de la session.

Dans cette boîte de dialogue contextuelle :

* Cliquez sur OK pour terminer la session utilisateur.
* Cliquez sur Annuler pour réinitialiser la session utilisateur.

>[!NOTE]
>
>Si l’utilisateur ne réagit pas, il est automatiquement déconnecté de l’espace de travail AEM Forms trois secondes avant expiration de la session.
