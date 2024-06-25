---
title: Gérer les informations d’identification HSM
description: Découvrez comment gérer vos informations d’identification HSM. Vous pouvez gérer HSM à partir de la page Trust Store Management. Vous pouvez afficher, vérifier, mettre à jour, réinitialiser et supprimer des composants HSM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 100%

---

# Gérer les informations d’identification HSM {#managing-hsm-credentials}

Sur la page Trust Store Management, vous pouvez gérer les informations d’identification HSM (module de sécurité matérielle). Un module HSM est un périphérique PKCS#11 tiers qui vous permet de générer et de stocker des clés privées en toute sécurité. Le module HSM protège physiquement l’accès aux clés privées et leur utilisation.

Le logiciel client est nécessaire pour communiquer avec le module HSM. Le logiciel client HSM doit être installé et configuré sur le même ordinateur qu’AEM Forms.

AEM Forms Digital Signatures peut utiliser les informations d’identification stockées sur un module HSM pour appliquer des signatures numériques côté serveur. Suivez les instructions de cette section pour créer un alias pour chacune des informations d’identification HSM utilisée par Digital Signatures. L’alias contient tous les paramètres requis par le module HSM.

>[!NOTE]
>
>Une fois la configuration HSM terminée, redémarrez le serveur AEM Forms Server.

## Création d’un alias pour les informations d’identification HSM lorsque le périphérique HSM est en ligne {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis cliquez sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de signatures numériques, comme l’opération de saisie du champ de signature.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en cluster, ce chemin d’accès doit être identique pour tous les serveurs du cluster.
1. Cliquez sur Tester la connectivité HSM. Si AEM Forms est en mesure de se connecter au périphérique HSM, un message s’affiche, indiquant que le module HSM est disponible. Cliquez sur Suivant.
1. Utilisez le nom du jeton, l’ID d’emplacement ou l’index de liste d’emplacements pour identifier l’emplacement de stockage des informations d’identification sur le module HSM.

   * **Nom du jeton :** correspond au nom de la partition HSM à utiliser (par exemple, HSMPART1).
   * **ID d’emplacement :** un identifiant d’emplacement de type de données de type Long.
   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index calculé sur la base 0, ce qui signifie que si le client est d’abord enregistré avec la partition HSMPART1, HSMPART1 sera référencé à l’aide de la valeur SlotListIndex 0.

1. Dans la zone Numéro PIN du jeton, saisissez le mot de passe requis pour accéder à la clé HSM, puis cliquez sur Suivant.
1. Dans la zone Informations d’identification, sélectionnez des informations d’identification. Cliquez sur Enregistrer.

## Création d’un alias pour des informations d’identification HSM lorsque le périphérique HSM est hors ligne {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis cliquez sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de signatures numériques, comme l’opération de saisie du champ de signature.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en cluster, ce chemin d’accès doit être identique pour tous les serveurs du cluster.
1. Cochez la case Création de profil hors connexion. Cliquez sur Suivant.
1. Dans la liste Périphérique HSM, sélectionnez le fabricant du périphérique HSM sur lequel les informations d’identification sont stockées.
1. Dans la liste Type d’emplacement, sélectionnez ID d’emplacement, Index d’emplacement ou Nom du jeton, puis renseignez une valeur dans la zone Informations d’emplacement. AEM Forms utilise ces paramètres pour déterminer l’emplacement de stockage des informations d’identification sur le module HSM.

   * **Nom du jeton :** correspond à un nom de partition (par exemple, HSMPART1).
   * **ID d’emplacement :** nombre entier correspondant à l’emplacement, qui correspond à son tour à une partition. Par exemple, le client (Forms Server) s’est d’abord enregistré avec la partition HSMPART1. L’emplacement 1 est donc associé à la partition HSMPART1 pour ce client. Étant donné que HSMPART1 est la première partition enregistrée, l’ID d’emplacement est 1 et vous définissez Informations d’emplacement sur 1.

     L’ID d’emplacement est défini pour les clients de façon individuelle. Si vous enregistrez une deuxième machine sur une partition différente (par exemple, HSMPART2 sur le même périphérique HSM), l’emplacement 1 sera associé à la partition HSMPART2 pour ce client.

   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index de base 0, ce qui signifie que, si le client est d’abord enregistré avec la partition HSMPART1, l’emplacement 1 est associé à HSMPART1 pour ce client. Étant donné que HSMPART1 est la première partition enregistrée, l’index d’emplacement est 0.

1. Sélectionnez l’une de ces options et indiquez le chemin d’accès :

   * **Certificat** : (non requis si vous utilisez SHA1) cliquez sur Parcourir et localisez le chemin d’accès à la clé publique correspondant aux informations d’identification utilisées.
   * **Certificat SHA1 :** (non requis si vous utilisez un certificat physique) saisissez la valeur SHA1 (empreinte numérique) du fichier de clé publique (.cer) pour les informations d’identification que vous utilisez. Veillez à ce que la valeur SHA1 ne contienne aucun espace.

1. Dans la zone Mot de passe, saisissez le mot de passe requis pour accéder à la clé HSM correspondant aux informations d’emplacement données, puis cliquez sur Enregistrer.

## Affichage des propriétés d’alias d’informations d’identification HSM {#view-hsm-credential-alias-properties}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur le nom d’alias des informations d’identification pour en afficher les propriétés, puis sur OK.

## Vérification du statut d’informations d’identification HSM {#check-the-status-of-an-hsm-credential}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cochez la case en regard des informations d’identification à vérifier, puis cliquez sur Vérifier le statut.

La colonne Statut indique le statut actuel des informations d’identification. En cas d’échec, un X rouge s’affiche dans la colonne Statut. Placez la souris sur le X pour afficher une info-bulle contenant la raison de l’échec.

## Mise à jour des propriétés d’alias d’identification HSM {#update-hsm-credential-alias-properties}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur le nom de l’alias des informations d’identification.
1. Cliquez sur Mettre à jour les informations d’identification et mettez à jour les paramètres suivant les besoins.

## Réinitialisation de toutes les connexions HSM {#reset-all-hsm-connections}

Réinitialisez les connexions ouvertes à un périphérique HSM après toute interruption de la session réseau entre le serveur Forms Server et le périphérique HSM. Par exemple, des interruptions peuvent survenir en raison d’une panne du réseau ou de la mise hors ligne du périphérique HSM pour une mise à jour du logiciel. Après une interruption, les connexions existantes sont obsolètes et toutes les demandes de signature sur ces connexions échouent. L’option Réinitialiser toutes les connexions HSM efface les anciennes connexions.

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur Réinitialiser toutes les connexions HSM.

## Suppression d’un alias d’informations d’identification HSM {#delete-an-hsm-credential-alias}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cochez les cases correspondant aux informations d’identification HSM à supprimer et cliquez sur Supprimer, puis sur OK.

## Configuration de la prise en charge HSM à distance {#configure-remote-hsm-support}

AEM Forms utilise un mécanisme IPC/RPC basé sur les services web. Ce mécanisme permet à AEM Forms d’utiliser un HSM installé sur un ordinateur distant. Pour utiliser cette fonctionnalité, installez le service web sur l’ordinateur distant sur lequel HSM est installé. Pour plus d’informations, consultez [Configuration de la prise en charge HSM pour AEM Forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://helpx.adobe.com/fr/livecycle/kb/configuring-hsm-support-using-sun.html).

Ce mécanisme ne prend pas en charge la création en ligne de profils HSM ni les vérifications de statut. Toutefois, il existe deux façons de créer des profils HSM et d’effectuer des vérifications de statut :

* Créez des informations d’identification client pour AEM Forms en lui transmettant le certificat du ou de la signataire. Suivez les étapes mentionnées dans la rubrique [Configuration de la prise en charge HSM pour AEM Forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://helpx.adobe.com/fr/livecycle/kb/configuring-hsm-support-using-sun.html) pour plus d’informations. L’emplacement du service web est transmis en tant que propriété Credential. La création de profils HSM hors ligne à l’aide du certificat der ou du certificat SHA-1 hex est également prise en charge. Cependant, si vous avez effectué une mise à niveau vers AEM Forms à partir d’une version antérieure, apportez des modifications au client car les informations d’identification comportaient des informations de certificat et de service web.
* L’emplacement du service web est spécifié dans la console d’administration pour le service Signature. (Voir [Paramètres du service Signature](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) Ici, le client ne transportait que l’alias du profil HSM dans le Trust Store. Vous pouvez facilement utiliser cette option sans aucune modification du client, même si vous avez effectué une mise à niveau vers AEM Forms à partir d’une version antérieure d’AEM Forms. Cette option ne prend pas en charge les profils HSM utilisant le certificat SHA-1.
