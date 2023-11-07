---
title: Gérer les informations d’identification HSM
description: Découvrez comment gérer les informations d’identification HSM. Vous pouvez gérer HSM à partir de la page Trust Store Management. Vous pouvez afficher, vérifier, mettre à jour, réinitialiser et supprimer des composants HSM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 11%

---

# Gérer les informations d’identification HSM {#managing-hsm-credentials}

Sur la page Trust Store Management, vous pouvez gérer les informations d’identification HSM (Hardware Security Module, module de sécurité matérielle). Un HSM est un périphérique PKCS#11 tiers que vous pouvez utiliser pour générer et stocker des clés privées en toute sécurité. Le HSM protège physiquement l’accès aux clés privées et leur utilisation.

Le logiciel client est nécessaire pour communiquer avec le module HSM. Le logiciel client HSM doit être installé et configuré sur le même ordinateur que AEM forms.

AEM forms Digital Signatures peut utiliser les informations d’identification stockées sur un HSM pour appliquer des signatures numériques côté serveur. Suivez les instructions de cette section pour créer un alias pour chaque identifiant HSM utilisé par Digital Signatures. L’alias contient tous les paramètres requis par le module HSM.

>[!NOTE]
>
>Après avoir modifié votre configuration HSM, redémarrez le serveur d’AEM forms.

## Créer un alias pour les informations d’identification HSM lorsque l’appareil HSM est en ligne {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée comme propriété pour certaines opérations Digital Signatures, telles que l’opération Sign Signature Field.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en grappe, ce chemin d’accès doit être identique pour tous les serveurs de la grappe.
1. Cliquez sur Tester la connectivité HSM. Si AEM forms est en mesure de se connecter à l’appareil HSM, un message s’affiche, indiquant que le HSM est disponible. Cliquez sur Suivant.
1. Utilisez le nom du jeton, l’identifiant d’emplacement ou l’index de liste d’emplacements pour identifier l’emplacement de stockage des informations d’identification sur le HSM.

   * **Nom du jeton :** correspond au nom de la partition HSM à utiliser (par exemple, HSMPART1).
   * **ID d’emplacement :** un identifiant d’emplacement de type de données de type Long.
   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index de base 0, ce qui signifie que si le client est d’abord enregistré avec la partition HSMPART1, HSMPART1 sera référencé à l’aide de la valeur SlotListIndex 0.

1. Dans la zone Token Pin, saisissez le mot de passe requis pour accéder à la clé HSM, puis cliquez sur Next.
1. Dans la zone Informations d’identification, sélectionnez des informations d’identification. Cliquez sur Enregistrer.

## Création d’un alias pour des informations d’identification HSM lorsque l’appareil HSM est hors ligne {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée comme propriété pour certaines opérations Digital Signatures, telles que l’opération Sign Signature Field.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en grappe, ce chemin d’accès doit être identique pour tous les serveurs de la grappe.
1. Cochez la case Création de profil hors ligne . Cliquez sur Suivant.
1. Dans la liste Périphérique HSM, sélectionnez le fabricant de l’appareil HSM sur lequel les informations d’identification sont stockées.
1. Dans la liste Type d’emplacement, sélectionnez Id d’emplacement, Index d’emplacement ou Nom du jeton, puis spécifiez une valeur dans la zone Infos sur l’emplacement. AEM forms utilise ces paramètres pour déterminer l’emplacement de stockage des informations d’identification sur le HSM.

   * **Nom du jeton :** correspond à un nom de partition (par exemple, HSMPART1).
   * **ID d’emplacement :** nombre entier correspondant à l’emplacement, qui correspond à son tour à une partition. Par exemple, le client (serveur Forms) s’est d’abord enregistré avec la partition HSMPART1. Cela mappe l’emplacement 1 à la partition HSMPART1 pour ce client. Etant donné que HSMPART1 est la première partition enregistrée, l’ID d’emplacement est 1 et vous définissez Informations d’emplacement sur 1.

     L’identifiant d’emplacement est défini client par client. Si vous enregistrez une deuxième machine sur une partition différente (par exemple, HSMPART2 sur le même appareil HSM), l’emplacement 1 sera associé à la partition HSMPART2 pour ce client.

   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index de base 0, ce qui signifie que si le client est d’abord enregistré avec la partition HSMPART1, l’emplacement 1 est mappé à HSMPART1 pour ce client. Etant donné que HSMPART1 est la première partition enregistrée, l’index d’emplacement est 0.

1. Sélectionnez l’une de ces options et indiquez le chemin d’accès :

   * **Certificat** : (non requis si vous utilisez SHA1) cliquez sur Parcourir et localisez le chemin d’accès à la clé publique correspondant aux informations d’identification utilisées.
   * **Certificat SHA1 :** (Non requis si vous utilisez un certificat physique) Saisissez la valeur SHA1 (empreinte numérique) du fichier de clé publique (.cer) pour les informations d’identification que vous utilisez. Assurez-vous qu’aucun espace n’est utilisé dans la valeur SHA1.

1. Dans la zone Mot de passe, saisissez le mot de passe requis pour accéder à la clé HSM correspondant aux informations d’emplacement données, puis cliquez sur Enregistrer.

## Affichage des propriétés d’alias d’identification HSM {#view-hsm-credential-alias-properties}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur le nom de l’alias des informations d’identification pour afficher les propriétés, puis cliquez sur OK.

## Vérification de l’état des informations d’identification HSM {#check-the-status-of-an-hsm-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cochez la case en regard des informations d’identification à vérifier, puis cliquez sur Vérifier l’état.

La colonne État reflète l’état actuel des informations d’identification. En cas d’échec, un X rouge s’affiche dans la colonne État. Passez la souris sur le X pour afficher une info-bulle contenant la raison de l’échec.

## Mise à jour des propriétés d’alias d’identification HSM {#update-hsm-credential-alias-properties}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur le nom de l’alias des informations d’identification.
1. Cliquez sur Mettre à jour les informations d’identification et mettez à jour les paramètres suivant les besoins.

## Réinitialiser toutes les connexions HSM {#reset-all-hsm-connections}

Réinitialisez les connexions ouvertes à un périphérique HSM après toute interruption de la session réseau entre le serveur Forms et le périphérique HSM. Par exemple, des interruptions peuvent survenir en raison d’une panne du réseau ou de la mise hors ligne du périphérique HSM pour une mise à jour du logiciel. Après une interruption, les connexions existantes sont obsolètes et toutes les demandes de signature de ces connexions échouent. L’option Réinitialiser toutes les connexions HSM efface les anciennes connexions.

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cliquez sur Réinitialiser toutes les connexions HSM.

## Suppression d’un alias d’informations d’identification HSM {#delete-an-hsm-credential-alias}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM.
1. Cochez les cases correspondant aux informations d’identification HSM à supprimer, cliquez sur Supprimer, puis sur OK.

## Configuration de la prise en charge HSM distante {#configure-remote-hsm-support}

AEM forms utilise un mécanisme IPC/RPC basé sur les services Web. Ce mécanisme permet à AEM forms d’utiliser un HSM installé sur un ordinateur distant. Pour utiliser cette fonctionnalité, installez le service Web sur l’ordinateur distant sur lequel HSM est installé. Voir [Configuration de la prise en charge HSM pour AEM forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://helpx.adobe.com/fr/livecycle/kb/configuring-hsm-support-using-sun.html)pour plus d’informations.

Ce mécanisme ne prend pas en charge la création en ligne de profils HSM ou les vérifications d’état. Toutefois, il existe deux façons de créer des profils HSM et d’effectuer des vérifications d’état :

* Créez des informations d’identification client d’AEM forms en lui transmettant le certificat du signataire. Suivez les étapes décrites dans la section [Configuration de la prise en charge HSM pour AEM forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://helpx.adobe.com/fr/livecycle/kb/configuring-hsm-support-using-sun.html). L’emplacement du service Web est transmis en tant que propriété Credential. Les profils HSM hors ligne créés à l’aide du certificat der ou du certificat SHA-1 hex sont également pris en charge. Cependant, si vous avez effectué une mise à niveau vers AEM forms à partir d’une version antérieure d’AEM forms, apportez des modifications au client car les informations d’identification portaient des informations de certificat et de service Web.
* L’emplacement du service Web est spécifié dans Administration Console pour le service Signature. (Voir [Paramètres du service Signature](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) Ici, le client ne transportait que l’alias du profil HSM dans le trust store. Vous pouvez utiliser cette option sans aucune modification du client, même si vous avez effectué une mise à niveau vers AEM forms à partir d’une version antérieure d’AEM forms. Cette option ne prend pas en charge les profils HSM utilisant le certificat SHA-1.
