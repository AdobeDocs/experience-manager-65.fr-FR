---
title: Gestion des informations d’identification HSM
seo-title: Gestion des informations d’identification HSM
description: Découvrez comment gérer vos informations d’identification HSM.
seo-description: Découvrez comment gérer vos informations d’identification HSM.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 99%

---


# Gestion des informations d’identification HSM {#managing-hsm-credentials}

La page Trust Store Management vous permet de gérer des informations d’identification HSM (Hardware Security Module, module de sécurité matérielle). Un HSM est un périphérique PKCS#11 tiers que vous pouvez utiliser pour générer et stocker des clés privées de manière sécurisée. Le HSM protège physiquement l’accès aux certificats et leur utilisation.

Le logiciel client est requis pour communiquer avec le HSM. Le logiciel client HSM doit être installé et configuré sur le même ordinateur qu’AEM Forms.

AEM Forms Digital Signatures peut utiliser les informations d’identification stockées sur un HSM pour appliquer des signatures numériques côté serveur. Suivez les instructions fournies dans cette section et créez un alias pour toutes les informations d’identification HSM utilisées par Digital Signatures. L’alias contient l’ensemble des paramètres requis par le module HSM.

>[!NOTE]
>
>Après avoir modifié votre configuration HSM, redémarrez le serveur AEM Forms.

## Création d’un alias pour des informations d’identification HSM lorsque le périphérique HSM est en ligne {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de Digital Signatures, comme l’opération de saisie du champ de signature.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en grappe, ce chemin d’accès doit être identique pour l’ensemble des serveurs de la grappe.
1. Cliquez sur Tester la connectivité du HSM. Si AEM Forms est en mesure de se connecter au périphérique HSM, un message s’affiche, indiquant que le module HSM est disponible. Cliquez sur Next (Suivant).
1. Utilisez Nom du jeton, ID d’emplacement ou Index de liste d’emplacements pour identifier l’emplacement de stockage des informations d’identification dans le module HSM.

   * **Nom du jeton :** correspond au nom de la partition HSM à utiliser (par exemple, HSMPART1).
   * **ID d’emplacement :** un identifiant d’emplacement de type de données de type Long.
   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index basé sur 0, ce qui signifie que si le client a commencé par s’enregistrer avec la partition HSMPART1, HSMPART1 est ensuite référencée sous la valeur d’index de liste d’emplacements 0.

1. Dans la zone Numéro PIN du jeton, saisissez le mot de passe requis pour accéder à la clé HSM, puis cliquez sur Suivant.
1. Dans la zone Informations d’identification, sélectionnez des informations d’identification. Cliquez sur Enregistrer.

## Création d’un alias pour des informations d’identification HSM lorsque le périphérique HSM est hors ligne  {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification HSM, puis sur Ajouter.
1. Dans la zone Nom du profil, saisissez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de Digital Signatures, comme l’opération de saisie du champ de signature.
1. Dans la zone Bibliothèque PKCS11, saisissez le chemin d’accès complet à votre bibliothèque cliente HSM sur le serveur. Par exemple, `c:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en grappe, ce chemin d’accès doit être identique pour l’ensemble des serveurs de la grappe.
1. Activez la case à cocher Création de profil hors connexion. Cliquez sur Next (Suivant).
1. Dans la liste Périphérique HSM, sélectionnez l’éditeur du périphérique HSM dans lequel les informations d’identification sont stockées.
1. Dans la liste Type d’emplacement, sélectionnez Id d’emplacement, Index d’emplacement ou Nom du jeton et indiquez une valeur dans le champ Informations d’emplacement. AEM Forms utilise ces paramètres pour déterminer à quel endroit les informations d’identification sont stockées sur le HSM.

   * **Nom du jeton :** correspond à un nom de partition (par exemple, HSMPART1).
   * **ID d’emplacement :** nombre entier correspondant à l’emplacement, qui correspond à son tour à une partition. Par exemple, le client (serveur Forms) commence par s’enregistrer avec la partition HSMPART1. Cette opération associe l’emplacement 1 à la partition HSMPART1 pour ce client. Etant donné que HSMPART1 est la première partition enregistrée, l’ID d’emplacement est 1 et vous devez placer Informations d’emplacement sur 1.

      L’ID d’emplacement est défini pour les clients de façon individuelle. Si vous enregistrez un second ordinateur sur une partition différente (par exemple, HSMPART2 sur le même périphérique HSM), l’emplacement 1 sera alors associé à la partition HSMPART2 pour ce client.

   * **Index d’emplacement :** si vous sélectionnez Index d’emplacement, définissez Informations d’emplacement sur un nombre entier correspondant à l’emplacement. Il s’agit d’un index basé sur 0, ce qui signifie que si le client a commencé par s’enregistrer avec la partition HSMPART1, l’emplacement 1 est associé à HSMPART1 pour ce client. Etant donné que HSMPART1 est la première partition enregistrée, l’Index d’emplacement est 0.

1. Sélectionnez l’une de ces options et indiquez le chemin :

   * **Certificat**  : (non requis si vous utilisez SHA1) cliquez sur Parcourir et localisez le chemin d’accès à la clé publique correspondant aux informations d’identification utilisées.
   * **Certificat SHA1 :** (non requis si vous utilisez un certificat physique) saisissez la valeur SHA1 (empreinte numérique) du fichier de clé publique (.cer) pour les informations d’identification utilisées. Veillez à ce que la valeur SHA1 ne contienne aucun espace.

1. Dans la zone Mot de passe, saisissez le mot de passe requis pour accéder à la clé HSM correspondant aux informations d’emplacement données, puis cliquez sur Enregistrer.

## Affichage des propriétés d’alias d’informations d’identification HSM  {#view-hsm-credential-alias-properties}

1. Dans Administration Console, cliquez sur Paramètres > Gestion de Trust Store > Informations d’identification HSM.
1. Cliquez sur le nom d’alias des informations d’identification pour en afficher les propriétés, puis cliquez sur OK.

## Vérification de l’état des informations d’identification HSM  {#check-the-status-of-an-hsm-credential}

1. Dans Administration Console, cliquez sur Paramètres > Gestion de Trust Store > Informations d’identification HSM.
1. Sélectionnez la case à cocher située en regard des informations d’identification à vérifier, puis cliquez sur Vérifier l’état.

La colonne Etat indique l’état actuel des informations d’identification. En cas d’échec, une croix (X) rouge s’affiche dans cette colonne. Placez votre souris sur le X afin d’afficher une info-bulle expliquant la raison de l’échec.

## Mise à jour des propriétés d’alias d’informations d’identification HSM  {#update-hsm-credential-alias-properties}

1. Dans Administration Console, cliquez sur Paramètres > Gestion de Trust Store > Informations d’identification HSM.
1. Cliquez sur le nom de l’alias des informations d’identification.
1. Cliquez sur Mettre à jour les informations d’identification, puis mettez à jour les paramètres si nécessaire.

## Réinitialisation de toutes les connexions HSM  {#reset-all-hsm-connections}

Réinitialisez les connexions ouvertes à un périphérique HSM après toute interruption de la session réseau entre le serveur Forms et le périphérique HSM. Par exemple, des interruptions peuvent survenir à la suite d’une panne de réseau ou lorsque le périphérique HSM est mis hors ligne pendant une mise à jour de logiciel. Après une interruption, les connexions existantes sont caduques et toutes les demandes de signature relatives à ces connexions échouent. L’option Réinitialiser toutes les connexions HSM permet d’effacer les anciennes connexions.

1. Dans Administration Console, cliquez sur Paramètres > Gestion de Trust Store > Informations d’identification HSM.
1. Cliquez sur Réinitialiser toutes les connexions HSM.

## Suppression d’un alias d’informations d’identification HSM  {#delete-an-hsm-credential-alias}

1. Dans Administration Console, cliquez sur Paramètres > Gestion de Trust Store > Informations d’identification HSM.
1. Cochez les cases correspondant aux informations d’identification HSM à supprimer, cliquez sur Supprimer, puis sur OK.

## Configuration de la prise en charge HSM à distance  {#configure-remote-hsm-support}

AEM Forms utilise un mécanisme IPC/RPC basé sur les services Web. Ce mécanisme permet à AEM Forms d’utiliser un HSM installé sur un ordinateur distant. Pour utiliser cette fonctionnalité, installez le service Web sur l’ordinateur distant où HSM est installé. Pour plus d’informations, consultez [Configuration de la prise en charge HSM pour AEM Forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html).

Ce mécanisme ne prend pas en charge la création en ligne de profils HSM ou les vérifications d’état. Toutefois, il existe deux façons de créer des profils HSM et d’effectuer des vérifications d’état :

* Créez des informations d’identification client pour AEM Forms en lui transmettant le certificat du signataire. Suivez les étapes mentionnées dans la rubrique [Configuration de la prise en charge HSM pour AEM Forms ES à l’aide du JDK Sun sur une plateforme Windows 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html) pour plus d’informations. L’emplacement du service Web est transmise sous forme de propriété des informations d’identification. Les profils HSM créés à l’aide d’un certificat DER ou d’un certificat SHA-1 hex sont également pris en charge. Toutefois, si vous avez effectué la mise à niveau vers AEM forms à partir d’une version antérieure d’AEM forms, effectuez les modifications de client car les informations d’identification portent des données de certificat et de service Web.
* L’emplacement du service Web est spécifié dans Administration Console pour le service Signature (voir [Paramètres du service Signature](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)). Ici, le client porte uniquement l’alias du profil HSM dans le Trust Store. Vous pouvez utiliser cette option directement sans modifications de client, même si vous avez effectué la mise à niveau vers AEM Forms à partir d’une version antérieure d’AEM Forms. Cette option ne prend pas en charge les profils HSM créés à l’aide d’un certificat SHA-1.

