---
title: Configurer SSL pour WebSphere Application Server
description: Découvrez comment configurer SSL pour WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 100%

---

# Configurer SSL pour WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

Cette section décrit la procédure permettant de configurer SSL sur IBM WebSphere Application Server.

## Création d’un compte utilisateur local sur WebSphere {#creating-a-local-user-account-on-websphere}

Pour activer SSL, WebSphere doit accéder à un compte utilisateur dans le registre utilisateur du système d’exploitation local, qui soit autorisé à administrer le système :

* (Windows) Créez un utilisateur Windows faisant partie du groupe Administrateurs et ayant le droit d’agir dans le cadre du système d’exploitation. (Voir [Création d’un utilisateur Windows pour WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) L’utilisateur ou l’utilisatrice peut être un utilisateur racine ou un autre utilisateur disposant de droits racine. Lorsque vous activez SSL sur WebSphere, utilisez l’identification du serveur et le mot de passe de cet utilisateur ou de cette utilisatrice.

### Création d’un utilisateur Linux ou UNIX pour WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Connectez-vous en tant qu’utilisateur ou utilisatrice racine.
1. Créez un utilisateur ou une utilisatrice en saisissant la commande suivante dans une invite de commande :

   * (Linux et Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Définissez le mot de passe du nouvel utilisateur en saisissant `passwd` à l’invite de commande.
1. (Linux and Solaris) Créez un fichier de mots de passe cachés en saisissant `pwconv` (sans paramètre) à l’invite de commande.

   >[!NOTE]
   >
   >(Linux et Solaris) pour que le registre de sécurité du système d’exploitation local du serveur d’applications WebSphere soit opérationnel, le fichier des mots de passe cachés doit exister. Ce fichier s’appelle généralement **/etc/shadow** et est basé sur le fichier /etc/passwd. S’il n’existe pas, une erreur se produit après l’activation de la sécurité globale et la configuration du registre de l’utilisateur comme système d’exploitation local.

1. Ouvrez le fichier de groupe du répertoire /etc dans un éditeur de texte.
1. Ajoutez l’utilisateur créé à l’étape 2 au groupe `root`.
1. Enregistrez et fermez le fichier.
1. (UNIX avec SSL activé) Démarrez et arrêtez WebSphere en tant qu’utilisateur ou utilisatrice racine.

### Création d’un utilisateur Windows pour WebSphere {#create-a-windows-user-for-websphere}

1. Connectez-vous à la console d’administration à l’aide d’un compte d’administration.
1. Sélectionnez **Démarrer > Panneau de configuration > Outils d’administration > Gestion de l’ordinateur > Utilisateurs et groupes locaux**.
1. Cliquez avec le bouton droit sur Utilisateurs et sélectionnez **Nouvel utilisateur**.
1. Saisissez un nom d’utilisateur et un mot de passe dans les zones appropriées, puis saisissez les autres informations requises dans les zones restantes.
1. Désélectionnez **L’utilisateur doit modifier le mot de passe lors de sa prochaine connexion**, cliquez sur **Créer**, puis sur **Fermer**.
1. Cliquez sur **Utilisateurs**, cliquez avec le bouton droit sur l’utilisateur que vous avez créé et sélectionnez **Propriétés**.
1. Cliquez sur l’onglet **Member de**, puis sur **Ajouter**.
1. Dans la zone Saisir les noms des objets à sélectionner, saisissez `Administrators`, puis cliquez sur Vérifier les noms pour vous assurer que le nom du groupe est correct.
1. Cliquez sur **OK**, puis de nouveau sur **OK**.
1. Sélectionnez **Démarrer > Panneau de configuration > Outils d’administration > Stratégie de sécurité locale > Stratégies locales**.
1. Cliquez sur Attribution des droits utilisateur, puis cliquez avec le bouton droit sur Agir dans le cadre du système d’exploitation et sélectionnez Propriétés.
1. Cliquez sur **Ajouter un utilisateur ou un groupe**.
1. Dans la zone Entrez les noms des objets à sélectionner, saisissez le nom de l’utilisateur que vous avez créé à l’étape 4, puis cliquez sur **Vérifier les noms** pour vous assurer que le nom est correct, puis cliquez sur **OK**.
1. Cliquez sur **OK** pour fermer la boîte de dialogue Agir dans le cadre des propriétés du système d’exploitation.

### Configuration de WebSphere pour utiliser le nouvel utilisateur en tant qu’administrateur {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Vérifiez que WebSphere est en cours d’exécution.
1. Dans la console d’administration WebSphere, sélectionnez **Sécurité > Sécurité globale**.
1. Dans Sécurité administrative, sélectionnez **Rôles des utilisateurs d’administration**.
1. Cliquez sur Ajouter et procédez comme suit :

   1. Saisissez **&amp;ast;** dans la zone de recherche, puis cliquez sur le bouton de recherche.
   1. Sous les rôles, cliquez sur **Administrateur**.
   1. Ajoutez l’utilisateur que vous venez de créer à Mappé au rôle et mappez-le à l’administrateur.

1. Cliquez sur **OK** pour enregistrer les modifications.
1. Redémarrez le profil WebSphere.

## Activation de la sécurité administrative {#enable-administrative-security}

1. Dans la console d’administration WebSphere, sélectionnez **Sécurité > Sécurité globale**.
1. Cliquez sur **Assistant de configuration de la sécurité**.
1. Assurez-vous de cocher la case **Activation de la sécurité des applications** pour l’activer. Cliquez sur **Suivant**.
1. Sélectionnez **Référentiels fédérés** et cliquez sur **Suivant**.
1. Indiquez les informations d’identification à définir, puis cliquez sur **Suivant**.
1. Cliquez sur **Finish** (Terminer). 
1. Redémarrez le profil WebSphere.

   WebSphere commence à utiliser le KeyStore et le TrustStore par défaut.

## Activation de SSL (TrustStore et clé personnalisée) {#enable-ssl-custom-key-and-truststore}

Il est possible de créer des TrustStores et des KeyStores à l’aide de l’utilitaire ikeyman ou d’Admin Console. Pour que ikeyman fonctionne correctement, assurez-vous que le chemin d’installation de WebSphere ne contient pas de parenthèses.

1. Dans la console d’administration WebSphere, sélectionnez **Sécurité > Gestion des certificats SSL et des clés**.
1. Cliquez sur **KeyStores et certificats** sous Éléments connexes.
1. Dans le menu déroulant **Utilisations des KeyStores**, assurez-vous que l’option **KeyStores SSL** est sélectionnée. Cliquez sur **Nouveau**.
1. Saisissez un nom et une description logiques.
1. Spécifiez le chemin d’accès à l’emplacement où vous souhaitez créer votre KeyStore. Si vous avez déjà créé un KeyStore via ikeyman, indiquez le chemin d’accès au KeyStore.
1. Indiquez et confirmez le mot de passe.
1. Choisissez le type de KeyStore et cliquez sur **Appliquer**.
1. Enregistrez la configuration principale.
1. Cliquez sur **Certificat personnel**.
1. Si vous avez déjà ajouté un KeyStore à l’aide d’ikeyman, votre certificat s’affiche. Dans le cas contraire, vous devez ajouter un nouveau certificat auto-signé en procédant comme suit :

   1. Sélectionnez **Créer > Certificat auto-signé**.
   1. Spécifiez les valeurs appropriées dans le formulaire de certificat. Veillez à conserver Alias et nom commun comme nom de domaine complet de l’ordinateur.
   1. Cliquez sur **Appliquer**.

1. Répétez les étapes 2 à 10 pour créer un TrustStore.

## Appliquer le KeyStore et le TrustStore personnalisés au serveur {#apply-custom-keystore-and-truststore-to-the-server}

1. Dans la console d’administration WebSphere, sélectionnez **Sécurité > Gestion des certificats SSL et des clés**.
1. Cliquez sur **Gestion de la configuration de la sécurité des points d’entrée**. La carte topologique locale s’ouvre.
1. Sous Entrant, sélectionnez l’enfant direct des nœuds.
1. Sous Éléments connexes, sélectionnez **Configurations SSL**.
1. Sélectionnez **NodeDeafultSSLSetting**.
1. Dans les listes déroulantes nom du TrustStore et nom du KeyStore, sélectionnez le TrustStore et le KeyStore personnalisés que vous avez créés.
1. Cliquez sur **Appliquer**.
1. Enregistrez la configuration principale.
1. Redémarrez le profil WebSphere.

   Votre profil s’exécute désormais sur des paramètres SSL personnalisés et votre certificat.

## Activer la prise en charge des formulaires natifs AEM {#enabling-support-for-aem-forms-natives}

1. Dans la console d’administration WebSphere, sélectionnez **Sécurité > Sécurité globale**.
1. Dans la section Authentification, développez **Sécurité RMI/IIOP** et cliquez sur **Communications entrantes CSIv2**.
1. Assurez-vous que **Prise en charge SSL** est sélectionné dans la liste déroulante Transport.
1. Redémarrez le profil WebSphere.

## Configurer WebSphere pour convertir des URL commençant par https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Pour convertir une URL commençant par https, ajoutez un certificat de signataire correspondant à cette URL au serveur WebSphere.

**Créer un certificat de signataire pour un site https**

1. Vérifiez que WebSphere est en cours d’exécution.
1. Dans la console d’administration WebSphere, accédez aux certificats de signataire, puis cliquez sur Sécurité > Gestion des certificats SSL et des clés > KeyStores et certificats > NodeDefaultTrustStore > Certificats de signataire.
1. Cliquez sur Récupérer à partir du port et effectuez les tâches suivantes :

   * Dans le champ Hôte, saisissez l’URL. Par exemple, saisissez `www.paypal.com`.
   * Dans le champ Port, saisissez `443`. Ce port est le port SSL par défaut.
   * Dans la zone Alias, saisissez un alias.

1. Cliquez sur Récupérer les informations de signataire, puis vérifiez que les informations sont récupérées.
1. Cliquez sur Appliquer, puis sur Enregistrer.

La conversion HTML à PDF du site dont le certificat est ajouté fonctionnera désormais à partir du service Generate PDF.

>[!NOTE]
>
>Pour qu’une application se connecte à des sites SSL depuis WebSphere, un certificat de signataire est requis. Il est utilisé par Java Secure Socket Extensions (JSSE) pour valider les certificats envoyés par le côté distant de la connexion lors d’une liaison SSL.

## Configurer des ports dynamiques {#configuring-dynamic-ports}

IBM WebSphere n’autorise pas plusieurs appels à ORB.init() lorsque la sécurité globale est activée. Vous pouvez consulter la restriction permanente à l’adresse https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Effectuez les étapes suivantes pour définir le port pour qu’il soit dynamique et résoudre le problème :

1. Dans la console d’administration WebSphere, sélectionnez **Serveurs** > **Types de serveur** > **Serveur d’applications WebSphere**.
1. Dans la section Préférences, sélectionnez votre serveur.
1. Dans l’onglet **Configuration**, sous la section **Communications**, développez **Ports**, puis cliquez sur **Détails**.
1. Cliquez sur les noms de port suivants, modifiez le **numéro de port** sur 0, puis cliquez sur **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurer le fichier sling.properties {#configure-the-sling-properties-file}

1. Ouvrez le fichier `[aem-forms_root]`\crx-repository\launchpad\sling.properties pour le modifier.
1. Recherchez la propriété `sling.bootdelegation.ibm` et ajoutez `com.ibm.websphere.ssl.*` à son champ de valeur. Le champ mis à jour se présente comme suit :

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Enregistrez le fichier et redémarrez le serveur.
