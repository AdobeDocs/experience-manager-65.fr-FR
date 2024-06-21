---
title: Authentification unique et gestionnaires de temporisation
description: Comment définir la valeur de délai d’expiration de session pour l’espace de travail AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# Authentification unique et gestionnaires de temporisation {#single-sign-on-and-timeout-handlers}

L’authentification unique est activée sur l’espace de travail AEM Forms. Si une personne s’est connectée à une application AEM Forms telle que Forms Manager ou l’interface utilisateur de PDF Generator, puis accède à l’espace de travail AEM Forms dans la même session de navigateur, alors elle est connectée à l’espace de travail AEM Forms et vice versa.

## Gestion des délais d’expiration du serveur dans l’espace de travail AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Le délai d’expiration de la session d’une personne peut être configuré dans la console d’administration.

Pour définir le délai d’expiration, connectez-vous à `https://'[server]:[port]'/adminui`, accédez à **Paramètres > User Management > Configuration > Configurer les attributs système avancés**, puis sélectionnez les paramètres souhaités.

Dans l’espace de travail AEM Forms, le délai d’expiration correspond à :

* la durée de disponibilité d’une session utilisateur en réponse à l’appel de commande `initialize` qui initialise la session utilisateur.
* Une boîte de dialogue contextuelle avertit la personne que la session est sur le point d’expirer, 15 secondes avant qu’elle n’expire.

Dans cette boîte de dialogue contextuelle :

* Cliquez sur OK pour terminer la session de la personne.
* Cliquez sur Annuler pour réinitialiser la session de la personne.

>[!NOTE]
>
>Si l’utilisateur ne réagit pas, il est automatiquement déconnecté de l’espace de travail AEM Forms trois secondes avant expiration de la session.
