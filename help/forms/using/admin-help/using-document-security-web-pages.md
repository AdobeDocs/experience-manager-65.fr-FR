---
title: Utilisation des pages Web de la sécurité des documents
description: Découvrez comment vous connecter et parcourir et utiliser les pages web de Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '921'
ht-degree: 100%

---

# Utilisation des pages Web de la sécurité des documents {#using-the-document-security-webpages}

Les utilisateurs et utilisatrices et les équipes d’administration utilisent les pages web de Document Security pour créer et gérer des politiques, gérer des documents protégés par une politique et contrôler les événements associés aux documents protégés par une politique. Les équipes d’administration utilisent également les pages web pour créer des jeux de politiques et désigner des coordinateurs et coordinatrices de jeux de politiques, configurer les paramètres par défaut de Document Security, gérer l’enregistrement et les comptes des utilisateurs et utilisatrices invités, ainsi que surveiller et gérer les événements liés au serveur, à la politique, à l’utilisateur ou l’utilisatrice et aux documents.

>[!NOTE]
>
>Vous pouvez également vous connecter à Document Security par le biais d’Acrobat et d’autres applications clientes à l’aide de votre compte de connexion d’utilisateur ou d’utilisatrice. (Voir [Configurer l’accès à Document Security à partir d’applications clientes](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Pour ouvrir les pages web, vous avez besoin d’un navigateur, de l’URL et des informations de connexion à Document Security. L’URL des utilisateurs et utilisatrices diffère de celle de l’équipe d’administration.

Document Security faisant référence aux répertoires existants de votre organisation pour obtenir des informations sur l’utilisateur ou l’utilisatrice, les informations de connexion à Document Security peuvent être les mêmes que celles que vous utilisez pour vous connecter au réseau et à d’autres applications. Pour obtenir des informations sur votre compte, contactez votre équipe d’administration système ou votre administrateur ou administratrice.

Pour vous connecter en tant qu’administrateur ou administratrice, vous devez disposer du rôle d’administrateur ou d’administratrice. Vous pouvez utiliser le compte de super-administrateur ou super-administratrice par défaut créé lors du processus d’installation.

## Se connecter aux pages web {#log-in-to-the-web-pages}

Pour vous connecter aux pages web à l’aide d’un navigateur, vous avez besoin de l’URL et d’un compte Document Security. L’URL des utilisateurs et utilisatrices diffère de celle de l’équipe d’administration. Les administrateurs et administratrices peuvent également se connecter aux pages utilisateur pour créer des politiques.

Si vous avez accès à plusieurs installations de Document Security, vous avez besoin de l’URL de l’instance de Document Security à laquelle vous souhaitez accéder. Contactez votre administrateur ou administratrice si vous ne disposez pas de ces informations. L’URL par défaut pour les pages utilisateur est `https://[host]:[port]/edc`. Le numéro de port peut ne pas être requis dans certains cas. Pour plus d’informations, contactez votre administrateur ou administratrice.

L’URL par défaut pour les administrateurs est `https://[host]:[port]/adminui`.

Pour les équipes d’administration, un compte de super-administrateur ou super-administratrice par défaut est créé lors de l’installation. Vous pouvez utiliser ce compte pour vous connecter lors de la première installation de Document Security.

>[!NOTE]
>
>Vous pouvez également accéder aux pages web à partir d’Acrobat et d’autres applications clientes. Pour plus dʼinformations, consultez l’Aide d’Acrobat ou l’Aide des extensions Acrobat Reader DC appropriée.

1. Saisissez l’URL dans votre navigateur :

   URL de sécurité des documents : `https://[host]:[port]/edc`

   ou URL de console d’administration : `https://[host]:[port]/adminui`

1. Dans la fenêtre de connexion, saisissez votre nom d’utilisateur ou d’utilisatrice et votre mot de passe, puis cliquez sur OK.
1. Dans la console d’administration, cliquez sur Services > Document Security.

>[!NOTE]
>
>Lorsque vous utilisez des pages web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette action peut entraîner des problèmes de capture de données et d’affichage de données indésirables.

## Naviguer dans les pages web {#navigating-the-web-pages}

Lorsque vous vous connectez aux pages web d’utilisateur ou d’utilisatrice, vous voyez des liens vers les pages utilisateur Politiques, Documents et Événements.

Lorsque vous vous connectez à la console d’administration et accédez à la page principale de Document Security, vous pouvez également voir un ou deux liens supplémentaires, l’un pour la page Configuration et l’autre pour la page Utilisateurs et utilisatrices invités et locaux. La page Utilisateurs et utilisatrices invités et locaux s’affiche uniquement si l’enregistrement de l’utilisateur ou l’utilisatrice invité est activé.

Utilisez ces liens pour accéder aux différentes pages dans lesquelles vous créez et gérez des politiques et des documents protégés par une politique.

**Afficher une page**

1. Cliquez sur le nom de la page, par exemple, cliquez sur Politiques.

**Revenir à la page précédente**

1. Cliquez sur le lien de navigation situé en haut de la page à laquelle vous souhaitez revenir.

**Actualiser la liste de données sur une page**

1. Sur la page principale, cliquez sur le lien vers la page à actualiser.

>[!NOTE]
>
>Lorsque vous utilisez des pages web, évitez de cliquer sur les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette action peut entraîner des problèmes de capture de données et d’affichage de données indésirables.

## Configurer l’accès à Document Security à partir d’applications clientes {#setting-up-access-to-document-security-from-client-applications}

Les applications clientes doivent être configurées pour se connecter à Document Security afin de protéger les documents, d’ouvrir des documents protégés par une politique et de se connecter aux pages web de Document Security. Voir l’*Aide d’Acrobat* ou l’*Aide de RightsManagementExtension* qui convient pour plus d’informations sur la configuration de la connexion dans l’application cliente.

Document Security est accessible via SSL (Secure Sockets Layer). Installez le certificat du site Web dans votre banque de certificats afin que vous puissiez accéder à Document Security par le biais des applications clientes.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Ces instructions sont spécifiques à Internet Explorer, mais vous pouvez installer le certificat à l’aide de n’importe quel navigateur web pris en charge. Pour plus d’informations, voir l’Aide de votre navigateur.

**Installation du certificat du serveur à l’aide d’Internet Explorer.**

1. Ouvrez votre navigateur web et saisissez l’URL de base de Document Security dans la zone Adresse. Par exemple, saisissez `https://[host]:[port]`. Une boîte de dialogue Alertes de sécurité s’affiche.
1. Cliquez sur Afficher le certificat, puis sur Installer le certificat et sélectionnez les paramètres par défaut de l’installation. Le certificat doit être installé dans les autorités de certification racine approuvées.
1. Fermez la session du navigateur.
1. Ouvrez une autre fenêtre de navigateur et saisissez la même URL dans la zone Adresse. Une boîte de dialogue Alertes de sécurité ne doit pas s’afficher. Ce test confirme que le certificat est correctement installé.

## Se déconnecter des pages web {#log-out-of-the-web-pages}

Déconnectez-vous une fois que vous avez fini d’utiliser les pages web afin de pouvoir utiliser votre navigateur web en toute sécurité à d’autres fins. Selon la configuration de Document Security, vous devrez peut-être fermer votre navigateur pour vous déconnecter complètement.

1. Dans le coin supérieur droit de la page, cliquez sur Déconnexion.
1. Si un message s’affiche sur la page Déconnexion, fermez la fenêtre du navigateur pour fermer complètement la session. Sinon, vous pouvez continuer à utiliser le navigateur à d’autres fins.
