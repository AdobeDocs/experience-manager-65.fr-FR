---
title: Utilisation des pages Web de la sécurité des documents
seo-title: Using the document security webpages
description: Découvrez comment vous connecter, parcourir et utiliser les pages Web de Document Security.
seo-description: Learn how you can login, navigate and use the document security web pages.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 3%

---

# Utilisation des pages Web de la sécurité des documents {#using-the-document-security-webpages}

Les utilisateurs et les administrateurs utilisent les pages Web de Document Security pour créer et gérer des stratégies, gérer des documents protégés par une stratégie et contrôler les événements associés aux documents protégés par une stratégie. Les administrateurs utilisent également les pages web pour créer des jeux de stratégies et désigner des coordinateurs de jeux de stratégies, configurer les paramètres par défaut de Document Security, gérer l’enregistrement et les comptes des utilisateurs invités, ainsi que surveiller et gérer les événements liés au serveur, à la stratégie, à l’utilisateur et aux documents.

>[!NOTE]
>
>Vous pouvez également vous connecter à Document Security par le biais d’Acrobat et d’autres applications clientes à l’aide de votre compte de connexion utilisateur. (Voir [Configuration de l’accès à Document Security à partir d’applications clientes](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Pour ouvrir les pages Web, vous avez besoin d’un navigateur, de l’URL et des informations de connexion à Document Security. L’URL des utilisateurs diffère de celle des administrateurs.

Document Security faisant référence aux répertoires existants de votre entreprise pour obtenir des informations sur l’utilisateur, les informations de connexion à Document Security peuvent être les mêmes que celles que vous utilisez pour vous connecter au réseau et à d’autres applications. Pour obtenir des informations sur votre compte, contactez votre administrateur système ou votre administrateur.

Pour vous connecter en tant qu’administrateur, vous devez disposer du rôle d’administrateur. Vous pouvez utiliser le compte de super-administrateur par défaut créé lors du processus d’installation.

## Connexion aux pages web {#log-in-to-the-web-pages}

Pour vous connecter aux pages web à l’aide d’un navigateur, vous avez besoin de l’URL et d’un compte Document Security. L’URL des utilisateurs diffère de celle des administrateurs. Les administrateurs peuvent également se connecter aux pages utilisateur pour créer des stratégies.

Si vous avez accès à plusieurs installations de Document Security, vous avez besoin de l’URL de l’instance de Document Security à laquelle vous souhaitez accéder. Contactez votre administrateur si vous ne disposez pas de ces informations. L’URL par défaut pour les pages utilisateur est `https://[host]:[port]/edc`. Le numéro de port peut ne pas être requis dans certains cas. Pour plus d’informations, contactez votre administrateur.

L’URL par défaut pour les administrateurs est `https://[host]:[port]/adminui`.

Pour les administrateurs, un compte de super-administrateur par défaut est créé lors de l’installation. Vous pouvez utiliser ce compte pour vous connecter lors de l’installation initiale de Document Security.

>[!NOTE]
>
>Vous pouvez également accéder aux pages web à partir d’Acrobat et d’autres applications clientes. Pour plus d’informations, voir l’ aide d’Acrobat ou l’ aide des extensions Acrobat Reader DC appropriée.

1. Saisissez l’URL dans votre navigateur :

   URL de sécurité des documents : `https://[host]:[port]/edc`

   ou URL de console d’administration : `https://[host]:[port]/adminui`

1. Dans la fenêtre de connexion, saisissez votre nom d’utilisateur et votre mot de passe, puis cliquez sur OK.
1. Dans Administration Console, cliquez sur Services > Document Security.

>[!NOTE]
>
>Lorsque vous utilisez des pages web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette action peut entraîner des problèmes de capture de données et d’affichage de données indésirables.

## Navigation dans les pages web {#navigating-the-web-pages}

Lorsque vous vous connectez aux pages Web utilisateur, vous voyez des liens vers les pages utilisateur Stratégies, Documents et Événements .

Lorsque vous vous connectez à Administration Console et accédez à la page principale de Document Security, vous pouvez également voir un ou deux liens supplémentaires, l’un pour la page Configuration et l’autre pour la page Utilisateurs invités et locaux. La page Utilisateurs invités et locaux s’affiche uniquement si l’enregistrement d’utilisateur invité est activé.

Utilisez ces liens pour accéder aux différentes pages dans lesquelles vous créez et gérez des stratégies et des documents protégés par une stratégie.

**Affichage d’une page**

1. Cliquez sur le nom de la page, par exemple, cliquez sur Stratégies.

**Revenir à la page précédente**

1. Cliquez sur le lien de navigation situé en haut de la page pour la page à laquelle vous souhaitez revenir.

**Actualiser la liste de données sur une page**

1. Sur la page principale, cliquez sur le lien vers la page à actualiser.

>[!NOTE]
>
>Lorsque vous utilisez des pages web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette action peut entraîner des problèmes de capture de données et d’affichage de données indésirables.

## Configuration de l’accès à Document Security à partir d’applications clientes {#setting-up-access-to-document-security-from-client-applications}

Les applications clientes doivent être configurées pour se connecter à Document Security afin de protéger les documents, d’ouvrir des documents protégés par une stratégie et de se connecter aux pages Web de Document Security. Voir *Aide d’Acrobat* ou le *Aide de RightsManagementExtension* pour plus d’informations sur la configuration de la connexion dans l’application cliente.

Document Security est accessible via SSL (Secure Sockets Layer). Installez le certificat du site web dans votre banque de certificats afin que vous puissiez accéder à Document Security par le biais des applications clientes.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Ces instructions sont spécifiques à Internet Explorer, mais vous pouvez installer le certificat à l’aide de n’importe quel navigateur web pris en charge. Pour plus d’informations, voir l’Aide de votre navigateur.

**Installation du certificat du serveur à l’aide d’Internet Explorer**

1. Ouvrez votre navigateur Web et saisissez l’URL de base de Document Security dans la zone Adresse. Par exemple, saisissez `https://[host]:[port]`. Une boîte de dialogue Alertes de sécurité s’affiche.
1. Cliquez sur Afficher le certificat, puis sur Installer le certificat et sélectionnez les paramètres par défaut de l’installation. Le certificat doit être installé dans les autorités de certification racine approuvées.
1. Fermez la session du navigateur.
1. Ouvrez une autre fenêtre de navigateur et saisissez la même URL dans la zone Adresse . Une boîte de dialogue Alertes de sécurité ne doit pas s’afficher. Ce test confirme que le certificat est correctement installé.

## Déconnexion des pages web {#log-out-of-the-web-pages}

Déconnectez-vous une fois que vous avez fini d’utiliser les pages web afin de pouvoir utiliser votre navigateur web en toute sécurité à d’autres fins. Selon la configuration de Document Security, vous devrez peut-être fermer votre navigateur pour vous déconnecter complètement.

1. Dans le coin supérieur droit de la page, cliquez sur Déconnexion.
1. Si un message s’affiche sur la page Déconnexion, fermez la fenêtre du navigateur pour fermer complètement la session. Sinon, vous pouvez continuer à utiliser le navigateur à d’autres fins.
