---
title: Configuration des options du client et du serveur
description: Découvrez comment configurer les différentes options du client et du serveur, telles que les paramètres de configuration du serveur, les rôles de Document Security et le contrôle des événements.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '10278'
ht-degree: 98%

---

# Configurer le serveur Document Security {#configure-the-document-security-server}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Configuration du serveur.
1. Configurez les paramètres et cliquez sur OK.

## Paramètres de configuration du serveur {#server-configuration-settings}

**URL de base :** URL de base de Document Security, contenant le nom et le port du serveur. Les informations ajoutées à cette base créent des URL de connexion. Par exemple, la séquence /edc/Main.do est ajoutée pour accéder aux pages Web. Les utilisateurs et utilisatrices répondent également aux invitations d’enregistrement des utilisateurs et utilisatrices externes par le biais de cette URL.

Si vous utilisez IPv6, saisissez l’URL de base comme nom d’ordinateur ou nom DNS. Si vous utilisez une adresse IP numérique, Acrobat ne parviendra pas à ouvrir les fichiers protégés par une politique. Utilisez également une URL HTTP sécurisée (HTTPS) pour votre serveur.

>[!NOTE]
>
>L’URL de base est incorporée dans des fichiers protégés par une politique. Les applications clientes utilisent l’URL de base pour se reconnecter au serveur. Les fichiers sécurisés contiendront toujours l’URL de base, même si elle est modifiée ultérieurement. Si vous modifiez l’URL de base, les informations de configuration doivent être mises à jour pour l’ensemble des clientes et des clients qui se connectent.

**Période d’ouverture hors connexion par défaut :** durée par défaut pendant laquelle un utilisateur peut utiliser un document protégé hors connexion. Ce paramètre détermine la valeur de départ de la période d’ouverture hors connexion au moment de la création d’une politique (Consultez la section Créer et modifier des politiques). À l’expiration de cette période d’ouverture, le ou la destinataire doit resynchroniser le document pour continuer à l’utiliser.

Pour plus d’informations sur le fonctionnement de la synchronisation et de l’ouverture hors connexion, reportez-vous à la section [Primer on configuring offline lease and synchronization](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Période de synchronisation hors connexion par défaut :** durée maximale pendant laquelle un document peut être utilisé hors connexion lors de la mise en place de sa protection.

**Délai d’expiration de la session client :** durée (en minutes) à l’issue de laquelle Document Security se déconnecte si un utilisateur connecté par le biais d’une application cliente n’interagit pas avec Document Security.

**Autoriser l’accès d’utilisateurs anonymes :** sélectionnez cette option pour permettre de créer des politiques partagées et personnelles autorisant les utilisateurs anonymes à ouvrir des documents protégés par une politique. (les utilisateurs qui ne possèdent pas de compte peuvent accéder au document, mais ils ne peuvent pas ouvrir de session Document Security ni utiliser d’autres documents protégés par une politique).

**Désactiver l’accès aux clients version 7 :** indique si les utilisateurs peuvent se connecter au serveur via Acrobat ou Reader 7.0. Lorsque cette option est sélectionnée, les utilisateurs et utilisatrices doivent utiliser Acrobat ou Reader 8.0 et versions ultérieures pour effectuer des opérations Document Security sur des documents PDF. Si les politiques exigent qu’Acrobat ou Reader 8.0 et versions ultérieures s’exécutent en mode certifié lors de l’ouverture de documents protégés par une politique, désactivez l’accès à Acrobat ou à Reader 7. (voir Spécification des droits de documents pour les utilisateurs et les groupes).

**Autoriser l’accès hors connexion par document :** cette option permet de spécifier l’accès hors connexion par document. Si ce paramètre est activé, l’utilisateur aura accès en mode hors connexion uniquement aux documents qu’il a ouverts en ligne au moins une fois.

**Autoriser l’authentification du mot de passe de l’utilisateur :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat du client :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification de certificat lors de la connexion au serveur.

**Autoriser une authentification étendue :** sélectionnez cette option pour activer l’authentification étendue, puis saisissez l’URL d’accueil de l’authentification étendue.

La sélection de cette option permet aux applications clientes d’utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisés et différentes options d’authentification configurées sur le serveur AEM Forms. Par exemple, les utilisateurs et utilisatrices peuvent désormais tester l’authentification SAML au lieu du nom d’utilisateur ou d’utilisatrice/mot de passe d’AEM Forms, à partir d’Acrobat et du client Reader. Par défaut, l’URL d’entrée contient *localhost* comme nom du serveur. Remplacez le nom du serveur par un nom d’hôte complet. Le nom d’hôte dans l’URL de destination est automatiquement renseigné à partir de l’URL de base, si l’authentification étendue n’est pas encore activée. Voir [Ajouter le fournisseur d’authentification étendue](configuring-client-server-options.md#add-the-extended-authentication-provider).

***Remarque ** : l’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.*

**Largeur de la commande HTML préférée pour l’authentification étendue :** indiquez la largeur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

**Hauteur de la commande HTML préférée pour l’authentification étendue :** indiquez la hauteur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

***Remarque ** : les limites de la largeur et la hauteur de cette boîte de dialogue sont les suivantes :*
Largeur : minimum = 400, maximum = 900

Hauteur : minimum = 450 ; maximum = 800

**Activer la mise en cache des informations d’identification du client :** sélectionnez cette option pour permettre aux utilisateurs de mettre en cache leurs informations d’identification (nom d’utilisateur et mot de passe). Lorsque les informations d’identification des utilisateurs et utilisatrices sont mises en cache, ils ou elles n’ont pas besoin de saisir leurs informations d’identification après avoir ouvert un document ou cliqué sur le bouton Actualiser de la page Gérer les politiques de sécurité dans Adobe Acrobat. Vous pouvez spécifier le nombre de jours avant que les utilisateurs ou utilisatrices aient à fournir à nouveau leurs informations d’identification. Définir le nombre de jours sur 0 permet de mettre les informations d’identification en cache indéfiniment.

## Configuration des utilisateurs utilisatrices, et des administrateurs et administratrices de Document Security {#configuring-document-security-users-and-administrators}

### Attribution des rôles de Document Security aux administrateurs et administratrices {#assigning-document-security-roles-to-administrators}

Votre environnement AEM Forms contient un ou plusieurs utilisateurs administrateurs ou utilisatrices administratrices disposant des privilèges appropriés pour créer des utilisateurs et utilisatrices, et des groupes. Si votre organisation utilise Document Security, au moins un administrateur ou une administrice doit également disposer du privilège nécessaire pour gérer les utilisateurs et utilisatrices invités et locaux.

Les administrateurs et administratrices doivent également disposer du rôle Utilisateur de la console d’administration pour accéder à la console d’administration. (Voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuration des utilisateurs et utilisatrices, et des groupes visibles {#configuring-visible-users-and-groups}

Pour afficher les utilisateurs et utilisatrices, et les groupes des domaines sélectionnés lors des recherches d’utilisateurs de politiques, un super-administrateur ou une super-administratrice ou un administrateur ou administratrice de jeux de politiques doit sélectionner et ajouter des domaines (créés dans User Management) à la liste des utilisateurs et utilisatrices, et groupes visibles pour chaque jeu de politiques créé.

La liste des utilisateurs, des utilisatrices et des groupes est visible par la personne coordinatrice de jeux de politiques. Elle permet de restreindre les domaines que l’utilisateur ou l’utilisatrice peut parcourir lorsqu’il ou elle choisit des utilisateurs, des utilisatrices ou des groupes à ajouter aux politiques. Si cette tâche n’est pas effectuée, la personne coordinatrice de jeux de politiques ne trouvera aucun utilisateur, utilisatrice ou groupe à ajouter à la politique. Un jeu de politiques peut avoir plusieurs personnes coordinatrices.

1. Après avoir installé et configuré votre environnement d’AEM Forms avec Document Security, configurez tous les domaines appropriés dans User Management. <!-- Fix broken link (See Setting up and managing domains) -->

   ***Remarque ** : vous devez commencer par créer les domaines avant de pouvoir créer des politiques.*

1. Dans la console d’administration, cliquez sur Services > Document Management > Politiques et cliquez sur l’onglet Jeux de politiques.
1. Sélectionnez Jeu de politiques global, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter un ou des domaine(s) et ajoutez des domaines existants selon les besoins.
1. Accédez à Services > Document Security > Configuration > Mes politiques et cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter un ou des domaine(s) et ajoutez des domaines existants selon les besoins.

## Ajouter le fournisseur d’authentification étendue {#add-the-extended-authentication-provider}

AEM Forms fournit un exemple de configuration que vous pouvez personnaliser pour votre environnement. Exécutez les étapes suivantes :

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

1. Obtenez l’exemple de fichier WAR et déployez-le. Consultez le guide d’installation adapté à votre serveur d’applications.
1. Assurez-vous que le serveur Forms possède un nom complet au lieu d’adresses IP comme URL de base et qu’il s’agit d’une URL HTTPS. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Activez l’authentification étendue à partir de la page Configuration du serveur. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Ajoutez les URL de redirection SSO requises dans le fichier de configuration User Management. Voir [Ajouter des URL de redirection SSO pour une authentification étendue](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Ajouter des URL de redirection SSO pour une authentification étendue {#add-sso-redirect-urls-for-extended-authentication}

Lorsque l’authentification étendue est activée, les utilisateurs et utilisatrices ouvrant un document protégé par une politique dans Acrobat XI ou Reader XI voient une boîte de dialogue d’authentification. Cette boîte de dialogue charge la page HTML que vous avez spécifiée comme URL de destination d’authentification étendue dans les paramètres du serveur Document Security. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter et enregistrez le fichier de configuration sur votre disque.
1. Ouvrez le fichier dans un éditeur et recherchez le nœud AllowedUrls.
1. Dans le nœud `AllowedUrls`, ajoutez les lignes suivantes : `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Enregistrez le fichier, puis importez le fichier mis à jour à partir de la page Configuration manuelle : dans la Console d’administration, cliquez sur Paramètres > User Management > Configuration > Importer et exporter les fichiers de configuration.

## Configuration de la sécurité hors ligne {#configuring-offline-security}

Document Security offre la possibilité d’utiliser des documents protégés par une politique hors ligne, sans connexion Internet ou réseau. Cette capacité nécessite que la politique autorise l’accès hors ligne, comme décrit dans [Spécifier les autorisations de document pour les utilisateurs et utilisatrices, et les groupes](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Avant qu’un document doté d’une telle politique puisse être utilisé hors ligne, les destinataires doivent ouvrir le document en ligne et activer l’accès hors ligne en cliquant sur Oui lorsque l’invite apparaît. Il peut également être demandé aux destinataires d’authentifier leurs identités. Les destinataires peuvent ensuite utiliser les documents hors ligne pendant la durée de la période d’ouverture hors ligne spécifiée dans la politique.

À la fin de la période d’ouverture hors ligne, les destinataires doivent se synchroniser à nouveau avec Document Security soit en ouvrant un document en ligne, soit en utilisant une commande de menu d’extensions Acrobat ou Acrobat Reader DC pour effectuer la synchronisation. (voir l’*Aide d’Acrobat* ou l’*Aide des extensions Acrobat Reader DC* appropriée).

Étant donné que les documents permettant un accès hors ligne nécessitent la mise en cache du matériel clé sur l’ordinateur sur lequel les fichiers sont stockés localement, le fichier peut potentiellement être compromis si un utilisateur ou une utilisatrice sans autorisation peut obtenir le matériel clé. Pour compenser cette éventualité, des options de basculement de clé planifiées et manuelles vous sont proposées et vous pouvez les configurer pour empêcher une personne non autorisée d’utiliser la clé pour accéder au document.

### Définir une période de location hors ligne par défaut {#set-a-default-offline-lease-period}

Les destinataires de documents protégés par une politique peuvent mettre les documents hors ligne pendant le nombre de jours spécifié dans la politique. Après avoir initialement synchronisé le document avec Document Security, le ou la destinataire peut utiliser le document hors ligne jusqu’à l’expiration de la période de location hors ligne. À l’expiration de la période de location, le ou la destinataire doit mettre le document en ligne et se connecter pour synchroniser le document avec Document Security afin de continuer à l’utiliser.

Vous pouvez configurer une période de location hors ligne par défaut. La durée de la location peut être modifiée par défaut lorsque quelqu’un crée ou modifie une politique.

1. Sur la page Document Security, cliquez sur Configuration > Configuration du serveur.
1. Dans la zone Période de location hors ligne par défaut, saisissez le nombre de jours pour la période de location hors ligne.
1. Cliquez sur OK.

### Gérer les changements de clés {#manage-key-rollovers}

Document Security utilise des algorithmes de chiffrement et des licences pour protéger les documents. Lorsqu’un document est chiffré, Document Security génère et gère une clé de déchiffrement appelée *DocKey* transmise à l’application cliente. Si la politique qui protège un document autorise l’accès hors ligne, une clé hors ligne appelée *clé principale* est également générée pour chaque utilisateur ou utilisatrice ayant un accès hors ligne au document.

>[!NOTE]
>
>Si une clé principale n’existe pas, Document Security en génère une pour sécuriser un document.

Pour ouvrir un document protégé par une politique hors ligne, l’ordinateur de l’utilisateur ou de l’utilisatrice doit disposer de la clé principale appropriée. L’ordinateur obtient la clé principale lorsque l’utilisateur ou l’utilisatrice se synchronise avec Document Security (ouvre un document protégé en ligne). Si cette clé principale est compromise, tout document auquel l’utilisateur ou l’utilisatrice a accès hors ligne peut également être compromis.

Pour réduire la menace pesant sur les documents hors ligne, il vaut mieux éviter d’autoriser l’accès hors ligne à des documents particulièrement sensibles. Vous pouvez également renouveler périodiquement les clés principales. Lorsque Document Security renouvelle la clé, les clés existantes ne peuvent plus accéder aux documents protégés par la politique. Par exemple, si un intrus récupère une clé principale sur un ordinateur portable volé, cette clé ne lui permet pas d’accéder aux documents protégés après le changement. Si vous pensez qu’une clé principale spécifique a été compromise, vous pouvez la remplacer manuellement.

Cependant, un changement de clé affecte toutes les clés principales, pas une seule. Cela limite également l’évolutivité du système, car les clientes et les clients doivent stocker davantage de clés pour l’accès hors connexion. La fréquence de changement des clés par défaut est de 20 jours. Il est recommandé de ne pas définir une valeur inférieure à 14 jours, car les utilisateurs et les utilisatrices ne pourront plus consulter des documents hors connexion et les performances du système peuvent en pâtir.

Dans l’exemple suivant, Clé1 est la plus ancienne des deux clés principales et Clé2 est la plus récente. Lorsque vous cliquez pour la première fois sur le bouton Exécuter le changement des clés maintenant, Clé1 devient non valide et une clé principale plus récente et valide (Clé3) est générée. Les utilisateurs et les utilisatrices obtiendront Clé3 lors de la synchronisation avec Document Security, généralement en ouvrant un document protégé en ligne. Néanmoins, les utilisateurs et les utilisatrices ne sont pas obligés d’effectuer la synchronisation avec Document Security avant d’avoir atteint la période de location hors connexion maximale indiquée par une politique. Après le premier changement de clés, les utilisateurs et les utilisatrices qui restent hors ligne peuvent continuer à ouvrir des documents hors ligne, dont ceux protégés par Clé3, jusqu’à expiration de la période de location hors ligne maximale. Lorsque vous cliquez une deuxième fois sur le bouton Exécuter le changement de clés maintenant, Clé2 devient non valide et Clé4 est créée. Les utilisateurs et les utilisatrices qui restent hors ligne pendant les deux changements de clé ne peuvent pas ouvrir les documents protégés par Clé3 ou Clé4 jusqu’à ce qu’ils soient synchronisés avec Document Security.

**Modifier la fréquence de changement des clés**

Pour des raisons de confidentialité, lorsque vous utilisez des documents hors ligne, Document Security propose une option de changement automatique des clés avec une période de fréquence par défaut de 20 jours. Vous pouvez modifier la fréquence de changement ; toutefois, évitez de définir une valeur inférieure à 14 jours, car les utilisateurs et les utilisatrices pourraient ne pas pouvoir consulter les documents hors ligne et les performances du système pourraient être affectées.

1. Sur la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Dans la zone Fréquence de changement des clés, saisissez le nombre de jours correspondant à la période de changement.
1. Cliquez sur OK.

**Procéder au changement manuel des clés principales**

Pour préserver la confidentialité des documents hors ligne, vous pouvez effectuer un changement manuel des clés principales. Vous devrez peut-être effectuer le changement manuel d’une clé (par exemple, si la clé est compromise par quelqu’un qui l’obtient à partir d’un ordinateur sur lequel elle est mise en cache pour permettre l’accès hors ligne à un document).

>[!NOTE]
>
>Évitez d’utiliser fréquemment le changement manuel, car cela entraîne le changement de toutes les clés principales, et non d’une seule, et peut empêcher temporairement les utilisateurs et les utilisatrices de visualiser de nouveaux documents hors ligne.

Les clés principales doivent être renouvelées deux fois avant que les clés précédemment existantes sur les ordinateurs clients ne soient invalidées. Les ordinateurs clients qui ont des clés principales invalidées doivent se resynchroniser avec Document Security pour acquérir les nouvelles clés principales.

1. Sur la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Cliquez sur Exécuter le changement des clés maintenant, puis cliquez sur OK.
1. Attendez environ 10 minutes. Le message suivant s’affiche dans le fichier-journal du serveur : `Done RightsManagement key rollover for`*N* `principals`. Où *N* est le nombre d’utilisateurs et d’utilisatrices dans le système de Document Security.
1. Cliquez sur Exécuter le changement des clés maintenant, puis cliquez sur OK.
1. Attendez environ 10 minutes.

## Configurer le contrôle des événements et les paramètres de confidentialité {#configuring-event-auditing-and-privacy-settings}

Document Security peut contrôler et enregistrer des informations sur les événements liés à l’interaction avec les documents protégés par une politique, les politiques, les administrateurs et administratrices et le serveur. Vous pouvez configurer le contrôle des événements et spécifier les types d’événements à contrôler. Pour contrôler les événements d’un document particulier, l’option de contrôle sur la politique doit également être activée.

Lorsque le contrôle est activé, vous pouvez afficher les détails des événements audités sur la page Événements. Les utilisateurs et utilisatrices de Document Security peuvent également afficher les événements spécifiquement liés aux documents protégés par une politique qu’ils utilisent ou créent.

Vous pouvez sélectionner ces types d’événements pour le contrôle :

* Événements de documents protégés par une politique, tels que les tentatives d’utilisateurs et utilisatrices autorisés ou non autorisés à ouvrir des documents
* Événements de politique, tels que la création, la modification, la suppression, l’activation et la désactivation de politiques
* Événements utilisateur, tels que les invitations et inscriptions d’utilisateurs ou utilisatrices externes, les comptes d’utilisateurs ou d’utilisatrices activés et désactivés, les modifications des mots de passe des utilisateurs et utilisatrices et les mises à jour de profil.
* Événements AEM Forms, tels que les incompatibilités de version, l’indisponibilité du serveur de répertoire et des fournisseurs d’autorisation et les modifications de configuration du serveur

### Activer ou désactiver le contrôle des événements {#enable-or-disable-event-auditing}

Vous pouvez activer et désactiver le contrôle des événements liés au serveur, aux documents protégés par une politique, aux politiques, aux ensembles de politiques et aux utilisateurs et utilisatrices. Lorsque vous activez le contrôle des événements, vous pouvez choisir de contrôler tous les événements possibles ou de sélectionner des événements spécifiques à contrôler.

Lorsque vous activez le contrôle du serveur, vous pouvez afficher les événements contrôlés sur la page Événements.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le contrôle du serveur, sous Activer le contrôle du serveur, sélectionnez Oui ou Non.
1. Si vous avez sélectionné Oui, sous chaque catégorie d’événement, effectuez l’une des actions suivantes pour sélectionner les options à contrôler :

   * Pour contrôler tous les événements de la catégorie, sélectionnez Tous.
   * Pour contrôler uniquement certains événements, désélectionnez Tous, puis cochez les cases en regard des événements que vous souhaitez contrôler.

     (Voir [Options de contrôle d’événements](configuring-client-server-options.md#event-auditing-options).)

1. Cliquez sur OK.

>[!NOTE]
>
>Lorsque vous travaillez avec des pages web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser et les flèches Précédent ou Suivant, car une telle action peut entraîner des problèmes indésirables de capture et d’affichage des données.

### Activer ou désactiver la notification de confidentialité {#enable-or-disable-privacy-notification}

Vous pouvez activer et désactiver un message de notification de confidentialité. Lorsque vous activez la notification de confidentialité, un message apparaît lorsqu’un ou une destinataire tente d’ouvrir un document protégé par une politique. L’avis informe la personne que l’utilisation du document est en cours de contrôle. Vous pouvez également spécifier une URL que la personne peut utiliser pour afficher votre page de politique de confidentialité, le cas échéant.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer la notification de confidentialité, sous Activer l’avis de confidentialité, sélectionnez Oui ou Non.

   Si la politique jointe à un document autorise l’accès des utilisateurs et utilisatrices anonymes et que l’option Activer la notification de confidentialité est définie sur Non, la personne n’est pas invitée à se connecter et le message de notification de confidentialité ne s’affiche pas.

   Si la politique jointe à un document n’autorise pas l’accès des utilisateurs et utilisatrices anonymes, la personne verra le message de notification de confidentialité.

1. Le cas échéant, dans la zone URL de confidentialité, saisissez l’URL de votre page de politique de confidentialité. Si la zone URL de confidentialité reste vide, la page de confidentialité d’Adobe.com s’affiche.
1. Cliquez sur OK.

>[!NOTE]
>
>La désactivation de l’avis de confidentialité ne désactive pas le contrôle de l’utilisation des documents. Les actions de contrôle prêtes à l’emploi et les actions personnalisées prises en charge via le suivi d’utilisation étendue peuvent toujours collecter des informations sur le comportement des utilisateurs et des utilisatrices.

### Importer un type d’événement de contrôle personnalisé {#import-a-custom-audit-event-type}

Si vous utilisez une application compatible avec Document Security qui prend en charge le contrôle d’événements supplémentaires, tels que des événements spécifiques à un certain type de fichier, un partenaire Adobe peut vous fournir des événements de contrôle personnalisés que vous pouvez importer dans Document Security. Utilisez cette fonctionnalité uniquement si des types d’événements personnalisés vous ont été fournis par un partenaire Adobe.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Cliquez sur Parcourir pour accéder au fichier XML à importer et cliquez sur Importer.
1. L’import écrase les types d’événements de contrôle personnalisés existants sur le serveur si des combinaisons identiques de code d’événement et d’espace de noms sont trouvées.
1. Cliquez sur OK.

### Supprimer un type d’événement de contrôle personnalisé {#delete-a-custom-audit-event-type}

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Cochez la case en regard du type d’événement de contrôle personnalisé à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK.

### Exporter les événements de contrôle {#export-audit-events}

Vous pouvez exporter des événements de contrôle vers un fichier à des fins d’archivage.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Modifiez les paramètres sous Exporter les événements de contrôle selon vos besoins. Vous pouvez préciser :

   * l’âge minimum des événements de contrôle à exporter ;
   * le nombre maximum d’événements de contrôle à inclure dans un seul fichier. Le serveur génère un ou plusieurs fichiers, en fonction de cette valeur ;
   * le dossier dans lequel le fichier sera créé. Ce dossier se trouve sur le serveur Forms. Si le chemin du dossier est relatif, il est relatif au répertoire racine de votre serveur d’applications.
   * le préfixe de fichier à utiliser pour les fichiers d&#39;événements de contrôle ;
   * le format du fichier, soit un fichier CSV (valeurs séparées par des virgules) compatible avec Microsoft Excel, soit un fichier XML.

1. Cliquez sur Exporter. Si vous souhaitez annuler l’export, cliquez sur Annuler l’export. Si un autre utilisateur ou une autre utilisatrice a planifié un export, le bouton Annuler l’export n’est pas disponible tant que cet export n’est pas terminé. Le bouton Annuler l’export n’est pas disponible si un autre utilisateur ou une autre utilisatrice a planifié un export. Pour vérifier si un export planifié ou une suppression a commencé ou est terminé, cliquez sur Actualiser.

### Supprimer les événements de contrôle {#delete-audit-events}

Vous pouvez supprimer les événements de contrôle antérieurs à un nombre de jours spécifié.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Sous Supprimer les événements de contrôle, spécifiez le nombre de jours dans la zone Supprimer les événements de contrôle plus anciens que.
1. Cliquez sur Supprimer. Cliquez sur Exporter. Si vous souhaitez annuler la suppression, cliquez sur Annuler la suppression. Si un autre utilisateur ou une autre utilisatrice a programmé une suppression, le bouton Annuler la suppression n’est pas disponible tant que l’export n’est pas terminé. Le bouton Annuler la suppression n’est pas disponible si un autre utilisateur ou une autre utilisatrice a planifié un export. Pour vérifier si une suppression planifiée a commencé ou est terminée, cliquez sur Actualiser.

### Options de contrôle des événements {#event-auditing-options}

Vous pouvez activer et désactiver le contrôle des événements et spécifier les types d’événements à contrôler.

**Événements de document**

**Afficher le document :** un destinataire affiche un document protégé par une politique.

**Fermer le document :** un destinataire ferme un document protégé par une politique.

**Imprimer en basse résolution** : un destinataire imprime un document protégé par une politique avec l’option de basse résolution spécifiée.

**Imprimer en haute résolution :** un destinataire imprime un document protégé par une politique avec l’option de haute résolution spécifiée.

**Ajouter une annotation au document :** un destinataire ajoute une annotation à un document PDF.

**Révoquer le document :** un utilisateur ou un administrateur révoque l’accès à un document protégé par une politique.

**Annuler la révocation du document :** un utilisateur ou un administrateur rétablit l’accès à un document protégé par une politique.

**Remplir le formulaire :** un destinataire saisit des informations dans un document PDF qui est un formulaire à remplir.

**Politique supprimée :** un éditeur supprime une politique d’un document pour retirer les protections de sécurité.

**Modifier l’URL de révocation du document :** un appel au niveau de l’API modifie une URL de révocation spécifiée pour accéder à un nouveau document qui remplace un document révoqué.

**Modifier le document :** un destinataire modifie le contenu d’un document protégé par une politique.

**Signer le document :** un destinataire signe un document.

**Sécuriser un nouveau document :** un utilisateur applique une politique pour protéger un document.

**Changer de politique pour le document :** un utilisateur ou un administrateur change la politique associée à un document.

**Publier le document en tant que :** un nouveau document dont les propriétés nomdedocument et licence sont identiques à un document existant est enregistré sur le serveur ; les documents n’ont pas de relation parent-enfant. Cet événement peut être déclenché à l’aide du SDK d’AEM forms.

**Itérer le document :** un nouveau document dont les propriétés nomdedocument et licence sont identiques à un document existant est enregistré sur le serveur ; les documents ont une relation parent-enfant. Cet événement peut être déclenché à l’aide du SDK d’AEM forms.

**Evénements de politique**

**Politique créée :** un utilisateur ou un administrateur crée une politique.

**Politique activée :** un administrateur rend une politique disponible.

**Politique modifiée :** un utilisateur ou un administrateur modifie une politique.

**Politique désactivée :** un administrateur rend une politique indisponible.

**Politique supprimée :** un utilisateur ou un administrateur supprime une politique.

**Modifier le propriétaire de la politique :** un appel au niveau de l’API modifie le propriétaire de la politique.

**Evénements d’utilisateur**

**Utilisateur supprimé** : un administrateur ou une administratrice supprime un compte d’utilisateur.

**Enregistrer un utilisateur invité :** un utilisateur externe s’enregistre auprès de la Sécurité des documents.

**Ouverture de session réussie :** tentatives d’ouverture de session réussies par des administrateurs ou des utilisateurs. 

**Utilisateurs invités :** la Sécurité des documents invite un utilisateur à s’enregistrer.

**Utilisateurs activés :** des utilisateurs externes activent leur compte à l’aide de l’URL mentionnée dans le courrier électronique d’activation ou un administrateur active un compte.

**Modifier le mot de passe :** des utilisateurs invités changent leur mot de passe ou un administrateur réinitialise le mot de passe d’un utilisateur local.

**Echec de l’ouverture de session :** échec des tentatives d’ouverture de session par des administrateurs ou des utilisateurs.

**Utilisateurs désactivés** : un administrateur ou une administratrice supprime un compte d’utilisateur local.

**Mise à jour du profil :** des utilisateurs invités modifient leur nom, le nom de leur entreprise et leur mot de passe.

**Compte verrouillé :** Un administrateur verrouille un compte.

**Evénements de jeu de politique**

**Jeu 

de politiques créé :** un administrateur ou un coordinateur de jeux de politiques crée un jeu de politiques.

**Jeu de politiques supprimé :** un administrateur ou un coordinateur de jeux de politiques supprime un jeu de politiques.

**Jeu de politiques modifié :** un administrateur ou un coordinateur de jeux de politiques modifie un jeu de politiques.

**Evénements de système**

**Synchronisation 
des annuaires terminée :** ces informations ne sont pas disponibles à partir de la page Événements. Les informations actuelles de synchronisation de répertoire, y compris l’état de synchronisation actuel et l’heure de la dernière synchronisation, sont affichées sur la page Gestion de domaine. Pour accéder à la page Gestion de domaine dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs et utilisatrices > Gestion de domaine.

**Activation d’accès client hors connexion :** une personne a activé l’accès hors connexion à des documents sécurisés par le serveur sur l’ordinateur de l’utilisateur ou de l’utilisatrice.

**Client synchronisé** : l’application cliente doit synchroniser les informations avec le serveur pour autoriser l’accès hors connexion.

**Version incohérente :** une version du SDK d’AEM forms incompatible avec le serveur a tenté de se connecter à ce dernier.

**Informations sur la synchronisation des annuaires :** ces informations ne sont pas disponibles à partir de la page Événements. Les informations actuelles de synchronisation de répertoire, y compris l’état de synchronisation actuel et l’heure de la dernière synchronisation, sont affichées sur la page Gestion de domaine. Pour accéder à la page Gestion de domaine dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs et utilisatrices > Gestion de domaine.

**Modification de la configuration du serveur :** modifications apportées à la configuration du serveur soit par l’intermédiaire des pages Web soit par importation manuelle d’un fichier config.xml. Cela inclut les modifications apportées à l’URL de base, les délais d’expiration de session, les verrouillages de connexion, les paramètres de répertoire, les changements de clés, les paramètres du serveur SMTP pour l’enregistrement externe, la configuration du filigrane, les options d’affichage, etc.

## Configurer le suivi d’utilisation étendu {#configuring-extended-usage-tracking}

Document Security peut suivre divers événements personnalisés pouvant être effectués sur un document protégé. Vous pouvez activer le suivi des événements du serveur Document Security au niveau global ou au niveau de la politique. Vous pouvez ensuite configurer un JavaScript pour capturer des actions spécifiques effectuées dans le document PDF protégé, comme cliquer sur un bouton ou enregistrer le document. Ces données d’utilisation sont envoyées sous forme de fichier XML en tant que paires clé-valeur, que vous pouvez utiliser pour une analyse plus approfondie. Les utilisateurs et utilisatrices finaux qui accèdent aux documents protégés peuvent autoriser ou refuser un tel suivi depuis l’application cliente.

Si le suivi est activé au niveau global, vous pouvez remplacer ce paramètre au niveau de la politique et le désactiver pour une politique particulière. Le remplacement au niveau de la politique n’est pas possible si le suivi est désactivé au niveau global. La liste des événements suivis est automatiquement transmise au serveur lorsque le nombre d’événements atteint 25 ou lorsque le document est fermé. Vous pouvez également configurer votre script pour envoyer explicitement la liste d’événements selon vos besoins. Vous pouvez personnaliser le suivi des événements en accédant aux propriétés et méthodes de l’objet Document Security.

Une fois le suivi activé, il le sera par défaut pour toutes les politiques créées par la suite. Les politiques créées avant l’activation du suivi sur le serveur nécessiteront des mises à jour manuelles.

### Activer ou désactiver le suivi d’utilisation étendu {#enable-or-disable-extended-usage-tracking}

Avant de commencer, assurez-vous que l’audit du serveur est activé. Voir [Configuration de l’audit des événements et des paramètres de confidentialité](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) pour plus d’informations sur l’audit.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le suivi d’utilisation étendu, sous Activer le suivi, sélectionnez Oui ou Non.
1. Pour définir la sélection de la case à cocher Autoriser la collecte de données d’utilisation détaillées sur la page de connexion, sous Activer le suivi par défaut, sélectionnez Oui ou Non.

Pour afficher les événements suivis, vous pouvez utiliser le filtre Événements de document sur la page Événements. Les événements suivis à l’aide de JavaScript sont étiquetés comme suivi détaillé de l’utilisation. Consultez [Surveillance des événements](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) pour plus d’informations sur les événements.

## Configurer les paramètres d’affichage de Document Security {#configure-document-security-display-settings}

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Options d’affichage.
1. Configurez les paramètres et cliquez sur OK.

### Paramètres d’affichage {#display-settings}

**Lignes à afficher pour les résultats de la recherche :** nombre de lignes qui apparaissent sur une page lors des recherches.

**Personnalisation de la boîte de dialogue de connexion cliente**

Ces paramètres contrôlent le texte affiché dans l’invite de connexion qui apparaît lorsqu’une personne se connecte à Document Security via une application cliente.

**Texte de bienvenue :** texte du message de bienvenue, par exemple « Veuillez vous connecter à l’aide de votre nom d’utilisateur et de votre mot de passe. ». Le texte du message de bienvenue doit contenir des informations sur la manière de se connecter à Document Security et de contacter un administrateur ou une administratrice ou une autre personne désignée dans votre organisation pour obtenir de l’aide. Par exemple, les utilisateurs et les utilisatrices externes peuvent avoir besoin de contacter un administrateur ou une administratrice s’ils oublient leur mot de passe ou ont besoin d’aide pour le processus d’inscription ou de connexion. La longueur maximale du texte de bienvenue est de 512 caractères.

**Texte du nom d’utilisateur :** libellé de texte de la zone de nom d’utilisateur.

**Texte du mot de passe :** libellé de texte de la zone du mot de passe.

**Personnalisation de la boîte de dialogue d’authentification du certificat client**

Ces paramètres contrôlent le texte affiché dans la boîte de dialogue d’authentification du certificat.

**Choisir 
le texte du type d’authentification :** texte affiché pour demander à un utilisateur de sélectionner un type d’authentification.

**Choisir le texte de certificat :** texte affiché pour demander à un utilisateur de sélectionner un type de certificat.

**Texte d’erreur Certificats non disponibles :** message de 512 caractères maximum à afficher lorsque le certificat sélectionné n’est pas disponible.

**Personnalisation de l’affichage du certificat client**

**Afficher uniquement les informations d’identification de confiance :** lorsque cette option est sélectionnée, l’application cliente ne présente à l’utilisateur que les certificats des émetteurs d’informations d’identification de confiance pour lesquels AEM forms est configuré (voir Gestion des certificats et des informations d’identification). Lorsque cette option n’est pas sélectionnée, l’utilisateur voit s’afficher une liste de tous les certificats du système de l’utilisateur.

## Configurer les filigranes dynamiques {#configure-dynamic-watermarks}

À l’aide de Document Security, vous pouvez configurer les paramètres par défaut de l’option de filigrane dynamique que vous pouvez appliquer lorsque vous créez des politiques. Un *filigrane* est une image superposée au texte du document. Il est utile pour suivre le contenu d’un document et peut aider à identifier une utilisation illégale du contenu.

Un filigrane dynamique peut être constitué soit de texte composé de variables définies telles que l’ID de l’utilisateur ou de l’utilisatrice, la date et le texte personnalisé, soit de contenu riche dans un PDF. Vous pouvez configurer des filigranes avec plusieurs éléments, chacun avec son propre positionnement et sa propre mise en forme.

Les filigranes ne sont pas modifiables et constituent donc une méthode plus sécurisée pour garantir la confidentialité du contenu du document. Les filigranes dynamiques garantissent également qu’un filigrane affiche suffisamment d’informations spécifiques à l’utilisateur ou à l’utilisatrice pour dissuader la diffusion ultérieure du document.

Le filigrane spécifié par une politique apparaît dans le document protégé par une politique lorsqu’une personne destinataire affiche ou imprime le document. Contrairement aux filigranes permanents, un filigrane dynamique n’est jamais enregistré dans le document, ce qui offre la flexibilité nécessaire lors du déploiement d’un document dans un environnement intranet pour garantir que l’application de visualisation affiche l’identité de l’utilisateur ou de l’utilisatrice spécifique. De plus, si un document a plusieurs utilisateurs ou utilisatrices, l’utilisation du filigrane dynamique signifie que vous pouvez utiliser un seul document au lieu de plusieurs versions, chacune avec un filigrane différent. Le filigrane qui apparaît reflète l’identité de l’utilisatrice ou de l’utilisateur actuel.

Notez que les filigranes dynamiques sont différents des filigranes que les utilisateurs et utilisatrices peuvent ajouter directement au document dans Acrobat. Le résultat est que vous pouvez avoir deux filigranes dans un document protégé par une politique.

### Points à prendre en compte lors de la création de filigranes {#considerations-when-creating-watermarks}

Vous pouvez créer des filigranes dynamiques avec plusieurs éléments de filigrane, chaque élément étant spécifié sous forme de texte ou de PDF. Vous pouvez inclure jusqu’à cinq éléments dans un filigrane.

Si vous choisissez un filigrane basé sur du texte, vous pouvez spécifier plusieurs éléments dans le filigrane avec plusieurs entrées de texte et spécifier le positionnement de chaque élément. Attribuez des noms significatifs à ces éléments, tels que l’en-tête, le pied de page, etc.

Par exemple, si vous souhaitez spécifier un texte différent dans l’en-tête, le pied de page, dans les marges et dans le document sous forme de filigrane, vous créez plusieurs éléments de filigrane et spécifier leur position. Si vous souhaitez que l’identifiant utilisateur et la date actuelle d’accès au document s’affichent dans l’en-tête, que le nom de la politique soit indiqué dans la marge de droite et qu’un texte personnalisé indiquant « CONFIDENTIEL » apparaissent en diagonale sur le document, définissez des éléments de filigrane différents de type texte et précisez leur formatage et leur emplacement. Lorsque le filigrane est appliqué à un document, tous les éléments de celui-ci sont appliqués au document en même temps, dans l’ordre dans lequel ils sont ajoutés au filigrane.

En règle générale, vous utilisez des filigranes PDF pour inclure du contenu graphique tel que des logos ou des symboles spéciaux comme un copyright ou une marque déposée.

Vous pouvez modifier les limites du nombre d’éléments de filigrane et de la taille du fichier PDF en modifiant le fichier de configuration de Document Security. Voir [Modifier les paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Gardez à l’esprit les points suivants lorsque vous configurez les filigranes :

* Vous ne pouvez pas utiliser un document PDF protégé par mot de passe comme élément de filigrane. Toutefois, si le filigrane que vous créez contient d’autres éléments qui ne sont pas protégés par mot de passe, ils seront appliqués en tant que partie du filigrane.
* Vous pouvez modifier la taille maximale du fichier PDF que vous souhaitez utiliser comme élément de filigrane. Cependant, les documents PDF volumineux utilisés comme filigranes dégradent les performances lors de la synchronisation hors ligne des documents auxquels de tels filigranes sont appliqués. Voir [Modifier les paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Seule la première page du PDF sélectionné est utilisée comme filigrane. Assurez-vous que les informations que vous souhaitez afficher sous forme de filigrane sont disponibles sur la première page elle-même.
* Même si vous pouvez spécifier la mise à l’échelle du document PDF, tenez compte de la taille de la page et de la disposition du PDF si vous envisagez de l’utiliser comme filigrane dans l’en-tête, le pied de page ou les marges.
* Lorsque vous spécifiez le nom de la police, saisissez-le correctement. AEM Forms remplace la police que vous avez spécifiée si elle n’est pas présente sur l’ordinateur client sur lequel le document est ouvert.
* Si vous avez sélectionné du texte comme contenu du filigrane, la spécification de l’option de mise à l’échelle sur Ajuster à la page ne fonctionne pas pour les pages dont la largeur est différente.
* Lorsque vous spécifiez le positionnement des éléments du filigrane, assurez-vous qu’un seul élément au maximum a le même positionnement. Si deux éléments de filigrane ont le même positionnement, par exemple au centre, ils apparaissent superposés sur le document et dans l’ordre dans lequel ils ont été ajoutés au filigrane.
* Lorsque vous spécifiez la taille et le type de police, assurez-vous que le texte est entièrement visible sur la page. Le contenu du texte est reporté sur de nouvelles lignes, de sorte que le contenu du filigrane que vous souhaitiez voir apparaître dans les marges peut empiéter sur les zones de contenu des pages. Toutefois, si le document est ouvert dans Acrobat 9, le texte au-delà d’une seule ligne est tronqué.

### Limites des filigranes dynamiques {#limitations-of-dynamic-watermarks}

Certaines applications clientes peuvent ne pas prendre en charge les filigranes dynamiques. Consultez l’aide appropriée des Extensions Acrobat Reader DC. De plus, gardez à l’esprit les points suivants concernant les versions d’Acrobat qui prennent en charge les filigranes dynamiques :

* Vous ne pouvez pas utiliser un document PDF protégé par mot de passe comme élément de filigrane.
* Les versions d’Acrobat et d’Adobe Reader antérieures à la version 10 ne prennent pas en charge les fonctionnalités de filigrane suivantes :

   * Filigranes PDF
   * Éléments multiples dans le filigrane (Texte/PDF)
   * Options avancées telles que la plage de pages ou les options d’affichage
   * Options de mise en forme du texte telles que la police, le nom de la police et la couleur spécifiés. Cependant, les versions antérieures d’Acrobat et de Reader afficheront le contenu du texte dans la police et la couleur par défaut.

* Acrobat 9.0 et versions antérieures : Acrobat 9.0 et les versions antérieures ne prennent pas en charge les noms de politique dans les filigranes dynamiques. Si Acrobat 9.0 ouvre un document protégé par une politique avec un filigrane dynamique qui inclut un nom de politique et d’autres données dynamiques, le filigrane s’affiche sans le nom de la politique. Si le filigrane dynamique inclut uniquement le nom de la politique, Acrobat affiche un message d’erreur.

### Ajouter un modèle de filigrane dynamique {#add-a-dynamic-watermark-template}

Vous pouvez créer des modèles de filigrane dynamique. Ces modèles restent disponibles en tant qu’option de configuration pour les politiques créées par les administrateurs et administratrices ou les utilisateurs et utilisatrices.

>[!NOTE]
>
>Les informations de configuration de filigrane dynamique ne sont pas capturées avec les autres informations de configuration lorsque vous exportez un fichier de configuration.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cliquez sur Nouveau.
1. Dans la zone Nom, saisissez le nom du nouveau filigrane.

   ***Remarque ** : certains caractères spéciaux ne peuvent être utilisés dans le nom ou la description des filigranes ou des éléments de filigrane. Reportez-vous aux restrictions répertoriées dans [Considérations relatives à la modification des politiques](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Sous Nom, à côté du signe plus, saisissez un nom significatif pour l’élément de filigrane, tel que En-tête, ajoutez une description, puis développez le signe plus pour afficher les options.
1. Sous Source, sélectionnez le type de filigrane : Texte ou PDF.
1. Si vous avez sélectionné Texte, procédez comme suit :

   * Sélectionnez les types de filigranes à inclure. Si vous sélectionnez Texte personnalisé, dans la zone adjacente, saisissez le texte à afficher pour le filigrane. Gardez à l’esprit la longueur du texte qui apparaîtra en filigrane.
   * Spécifiez les propriétés de mise en forme du texte telles que le nom de la police, la taille de la police, la couleur de premier plan et la couleur d&#39;arrière-plan pour le contenu du texte du filigrane. Spécifiez la couleur de premier plan et d’arrière-plan sous forme de valeurs hexadécimales.

     ***Remarque ** : si vous définissez le cadrage sur Page entière, vous ne pouvez pas modifier la taille de la police.*

1. Si vous sélectionnez le format PDF pour les options de filigrane riches, cliquez sur **Parcourir**, à côté de Sélectionner le PDF du filigrane, pour sélectionner le document PDF que vous voulez utiliser en filigrane.

   ***Remarque ** : n’utilisez pas de document PDF protégé par mot de passe. Si vous spécifiez un PDF protégé par mot de passe comme élément de filigrane, le filigrane n’est pas appliqué.*

1. Sous Utiliser comme arrière-plan, sélectionnez Oui ou Non.

   **Remarque** : le filigrane apparaît au premier plan, quelle que soit l’option sélectionnée pour ce paramètre. 

1. Pour contrôler l’endroit où le filigrane s’affiche sur le document, configurez les options Alignement vertical et Alignement horizontal.
1. Sélectionnez Ajuster à la page ou sélectionnez % et saisissez un pourcentage dans la zone. La valeur doit être un nombre entier et non une fraction. Pour configurer la taille du filigrane, vous pouvez utiliser une valeur correspondant au pourcentage de la page ou définir le filigrane pour qu’il s&#39;adapte à la taille de la page.
1. Dans la zone Rotation, saisissez les degrés de rotation du filigrane. La plage va de -180 à 180. Utilisez une valeur négative pour faire pivoter le filigrane dans le sens inverse des aiguilles d’une montre. La valeur doit être un nombre entier et non une fraction.
1. Dans la zone Opacité, saisissez un pourcentage. Utilisez un nombre entier et non une fraction.
1. Sous Options avancées, définissez les éléments suivants :

   **Options de plage de pages**

   Définissez la plage de pages sur lesquelles le filigrane doit être affiché. Entrez la page de début comme 1 et la page de fin comme -1 pour que toutes les pages soient marquées avec le filigrane.

   **Options d’affichage**

   Sélectionnez l’endroit où vous souhaitez que le filigrane apparaisse. Par défaut, le filigrane apparaît à la fois sur la copie électronique (en ligne) et sur la copie papier (impression).

1. Cliquez sur **Nouveau** sous Éléments de filigrane pour ajouter d’autres éléments de filigrane si nécessaire.
1. Cliquez sur OK.

### Modifier un modèle de filigrane dynamique {#edit-a-dynamic-watermark-template}

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cliquez sur le filigrane approprié dans la liste.
1. Dans la page Modifier les filigranes, modifiez les paramètres selon les besoins.
1. Cliquez sur OK.

### Supprimer un modèle de filigrane dynamique {#delete-a-dynamic-watermark-template}

Lorsque vous supprimez un filigrane dynamique, il n’est plus possible de l’ajouter à une nouvelle politique. Toutefois, le filigrane reste sur les politiques existantes qui l’utilisent actuellement. Les documents que la politique protège actuellement continuent d’afficher le filigrane dynamique jusqu’à ce que vous, un utilisateur ou une utilisatrice modifiiez la politique qui contient le filigrane supprimé. Une fois la politique modifiée, le filigrane n’est plus appliqué. Un message apparaît, indiquant que le filigrane existant est supprimé sur la politique et que l’utilisateur ou l’utilisatrice peut en sélectionner un autre pour le remplacer.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cochez la case à côté du filigrane approprié et cliquez sur Supprimer.
1. Cliquez sur OK.

## Configuration de l’inscription des utilisatrices et des utilisateurs invités {#configuring-invited-user-registration}

Les utilisateurs et les utilisatrices externes à votre organisation peuvent s’inscrire auprès de Document Security. Les utilisatrices et utilisateurs invités qui s’inscrivent et activent leur compte peuvent se connecter à Document Security en utilisant leur adresse e-mail et le mot de passe créé lors de leur inscription. Les utilisatrices et les utilisateurs invités enregistrés peuvent utiliser les documents protégés par une politique pour lesquels ils disposent d’autorisations.

Lorsque les utilisatrices et les utilisateurs invités sont activés, ils deviennent des utilisateurs locaux. Les utilisateurs et utilisatrices locaux peuvent être configurés et gérés à l’aide de la zone Utilisateurs et utilisatrices invités et locaux. (Voir [Gestion des comptes d’utilisatrices et d’utilisateurs invités et locaux](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)).

Selon les fonctionnalités que vous activez pour les utilisateurs et utilisatrices invités, ils peuvent également utiliser ces fonctionnalités de Document Security :

* Appliquer des politiques à des documents
* Créer des politiques
* Ajouter des utilisatrices et des utilisateurs invités aux politiques

Document Security génère automatiquement un e-mail d’invitation à l’enregistrement lorsque les événements suivants se produisent, sauf si l’utilisateur ou l’utilisatrice se trouve déjà dans l’annuaire LDAP source ou a déjà reçu une invitation d’enregistrement :

* Une personne existante ajoute une personne invitée à une politique.
* Un administrateur ou une administratrice ajoute un compte d’utilisateur invité sur la page d’enregistrement des utilisateurs et utilisatrices invités.

L’e-mail d’enregistrement contient un lien vers une page d’enregistrement et des informations sur les modalités d’enregistrement. Une fois la personne invitée enregistrée, Document Security envoie un e-mail d’activation comportant un lien vers une page d’activation. Une fois activé, le compte reste valide jusqu’à ce que vous le désactiviez ou le supprimiez.

Si vous activez l’enregistrement intégré, vous spécifiez une seule fois votre serveur SMTP, les détails de l’e-mail d’enregistrement, les capacités d’accès et les informations de réinitialisation du mot de passe de l’e-mail. Avant d’activer l’enregistrement intégré, vérifiez que vous avez créé un domaine local dans User Management et que le rôle « Utilisateur invité de Document Security » a été attribué aux utilisateurs, utilisatrices et groupes appropriés de votre organisation. (Voir [Ajout d’un domaine local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) et [Création et configuration des rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Si vous n’utilisez pas l’enregistrement intégré, vous devez disposer de votre propre système d’enregistrement des utilisateurs créé à l’aide d’AEM forms SDK. Consultez l’aide de la section « Développement de SPI pour AEM Forms » dans [Programmation avec AEM Forms](/help/forms/developing/introducing-java-api-soap-quick.md). Si vous n’utilisez pas l’option d’enregistrement intégré, il est recommandé de configurer un message dans l’e-mail d’activation et sur l’écran de connexion du client pour informer les utilisateurs et les utilisatrices sur la façon de contacter l’administration pour obtenir un nouveau mot de passe ou d’autres informations.

**Activer et configurer l’enregistrement des utilisateurs et utilisatrices invités**

Par défaut, le processus d’enregistrement des utilisateurs et utilisatrices invités est désactivé. Vous pouvez activer et désactiver l’enregistrement des utilisateurs et des utilisatrices invités pour Document Security, selon vos besoins.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Enregistrement des utilisateurs et des utilisatrices invités.
1. Sélectionnez Activer l’enregistrement des utilisateurs et des utilisatrices invités.
1. (Facultatif) Mettez à jour les paramètres d’enregistrement des utilisateurs et utilisatrices invités si nécessaire :

   * [Exclusion ou inclusion d’un utilisateur ou d’un groupe externe](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Paramètres des comptes d’enregistrement et du serveur](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Paramètres des courriers électroniques d’invitation à effectuer un enregistrement](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Paramètres des courriers électroniques d’activation](configuring-client-server-options.md#activation-email-settings)
   * [Configuration d’un courrier électronique de réinitialisation de mot de passe](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facultatif) Sous Enregistrement intégré, sélectionnez Oui pour activer cette option. Si vous n’activez pas l’enregistrement intégré, vous devez configurer votre propre système d’enregistrement des utilisateurs et utilisatrices.
1. Cliquez sur OK.

### Exclure ou inclure un utilisateur ou un groupe externe {#exclude-or-include-an-external-user-or-group}

Vous pouvez restreindre l’enregistrement auprès de Document Security pour certains utilisateurs, utilisatrices ou groupes d’utilisateurs et d’utilisatrices externes. Cette option s’avère utile, par exemple, pour autoriser l’accès à un certain groupe d’utilisateurs et d’utilisatrices mais exclure des personnes spécifiques faisant partie du groupe.

Les paramètres suivants se trouvent dans la zone Filtre de restriction des e-mails de la page Enregistrement des utilisateurs et utilisatrices invités.

**Exclusion :** saisissez l’adresse électronique d’un utilisateur ou d’un groupe à exclure. Pour exclure plusieurs utilisateurs et utilisatrices ou groupes, saisissez chaque adresse e-mail sur une nouvelle ligne. Pour exclure tous les utilisateurs et utilisatrices appartenant à un domaine particulier, entrez un caractère générique et le nom de domaine. Par exemple, pour exclure tous les utilisateurs du domaine example.com, saisissez &amp;.example.com.

**Inclusion :** saisissez l’adresse électronique d’un utilisateur ou d’un groupe à inclure. Pour inclure plusieurs utilisateurs et utilisatrices ou groupes, saisissez chaque adresse e-mail sur une nouvelle ligne. Pour inclure tous les utilisateurs et utilisatrices appartenant à un domaine particulier, entrez un caractère générique et le nom de domaine. Par exemple, pour inclure tous les utilisateurs du domaine example.com, saisissez &amp;.example.com.

### Paramètres des comptes d’enregistrement et du serveur {#server-and-registration-account-parameters}

Les paramètres suivants se trouvent dans la zone Paramètres généraux de la page d’enregistrement des utilisateurs et utilisatrices invités.

**Hôte SMTP :** le nom d’hôte du serveur SMTP. Le serveur SMTP gère les notifications par e-mail sortantes pour enregistrer et activer les comptes d’utilisateurs et utilisatrices invités.

Si votre hôte SMTP l’exige, saisissez les informations requises dans les zones Nom du compte du serveur SMTP et Mot de passe du compte du serveur SMTP pour vous connecter au serveur SMTP. Certaines organisations n’appliquent pas cette exigence. Si vous avez besoin d’informations, consultez votre administrateur ou administratrice système.

**Nom de la classe de socket du serveur SMTP :** Nom de la classe de socket pour le serveur SMTP. Par exemple, javax.net.ssl.SSLSocketFactory.

**Type de contenu d’email :** Type MIME accepté comme text/plain ou text/html.

**Codage d’email :** format de codage à utiliser pour l’envoi d’un email. Vous pouvez spécifier n’importe quel codage, par exemple UTF-8 pour Unicode ou ISO-8859-1 pour Latin. La valeur par défaut est UTF-8.

**Rediriger l’adresse e-mail :** lorsque vous indiquez une adresse e-mail pour ce paramètre, toute nouvelle invitation est envoyée à l’adresse fournie. Ce paramètre peut être utile pour l’exécution de tests.

**Utiliser des domaines locaux :** sélectionnez le domaine approprié. Lors d’une nouvelle installation, assurez-vous d’avoir créé le domaine à l’aide de User Management. S’il s’agit d’une mise à niveau, un domaine utilisateur externe a été créé lors de la mise à niveau et peut être utilisé.

**Utiliser SSL pour le serveur SMTP :** sélectionnez cette option pour activer SSL pour le serveur SMTP.

**Afficher le lien de connexion sur la page d’inscription :** affiche un lien de connexion sur la page d’enregistrement affichée pour les utilisateurs invités.

**Pour activer Transport Layer Security (TLS) pour le serveur SMTP**

1. Ouvrez la console d’administration.

   L’emplacement par défaut de la console d’administration est le suivant : `https://<server>:<port>/adminui`.

1. Accédez à Accueil > Services >Document Security > Configuration > Enregistrement des utilisateurs invités.
1. Dans Enregistrement des utilisateurs invités, spécifiez tous les paramètres de configuration, puis cliquez sur OK.

   >[!NOTE]
   >
   >Si vous utilisez Microsoft Office 365 comme serveur SMTP afin d’envoyer les invitations d’enregistrement des utilisateurs, utilisez les paramètres suivants :
   >
   >**Hôte SMTP :** smtp.office365.com.
   >**Port :** 587.

1. Ensuite, vous devez mettre à jour le fichier config.xml. Voir [Configuration pour activer SMTP pour Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Si vous apportez des modifications aux options d&#39;enregistrement des personnes invitées, le fichier config.xml est écrasé et TLS est désactivé. Si vous écrasez les modifications, vous devez effectuer l’étape ci-dessus pour réactiver la prise en charge de TLS pour l’enregistrement des personnes invitées.

### Paramètres des courriers électroniques d’invitation à l’enregistrement {#registration-invitation-email-settings}

Document Security émet automatiquement un e-mail d’invitation à l’enregistrement lorsque vous créez un compte de personne invitée ou lorsqu’un utilisateur ou une utilisatrice existant ajoute un ou une destinataire externe qui ne s’est pas encore enregistré ou n&#39;a pas été invité à s’enregistrer à une politique. L’e-mail contient un lien que le ou la destinataire peut utiliser pour accéder à la page d’enregistrement et saisir les informations de son compte personnel, notamment son nom d’utilisateur et son mot de passe. Votre mot de passe peut constituer n’importe quelle combinaison de huit caractères.

Lorsque le ou la destinataire active le compte, l’utilisateur ou l’utilisatrice devient un utilisateur ou une utilisatrice local.

Les paramètres suivants se trouvent dans la zone Configuration de l’e-mail d’invitation de la page Enregistrement des utilisateurs invités.

**De :** adresse e-mail à partir de laquelle l’e-mail d’invitation est envoyé. Le format par défaut de l’adresse e-mail d’expédition est postmaster@[[votre_domaine_d’installation]].com.

**Objet :** objet par défaut de l’e-mail d’invitation.

**Délai d’expiration :** nombre de jours à l’issue duquel l’invitation à l’enregistrement expire si l’utilisateur externe ne s’enregistre pas. La valeur par défaut est de 30 jours.

**Message :** texte qui apparaît dans le corps du message, invitant l’utilisateur à s’enregistrer.

### Paramètres des courriers électroniques d’activation {#activation-email-settings}

Une fois les personnes invitées enregistrées, Document Security envoie un e-mail d’activation. L’e-mail d’activation contient un lien vers la page d’activation du compte où les utilisateurs et utilisatrices peuvent activer leur compte. Lorsque les comptes sont activés, les utilisateurs et utilisatrices peuvent se connecter à Document Security en utilisant leur adresse e-mail et le mot de passe créés lors de leur enregistrement.

Lorsque le ou la destinataire active le compte d’utilisateur, l’utilisateur ou l’utilisatrice devient un utilisateur local ou une utilisatrice locale.

Les paramètres suivants se trouvent dans la zone Configuration de l’e-mail d’activation de la page Enregistrement des utilisateurs invités.

>[!NOTE]
>
>Il est également recommandé de configurer un message sur l’écran de connexion pour indiquer aux utilisateurs et utilisatrices externes comment contacter leur administrateur ou administratrice pour un nouveau mot de passe ou pour d’autres informations.

**De :** adresse e-mail à partir de laquelle l’e-mail d’activation est envoyé. Cette adresse e-mail reçoit les avis de non-acheminement envoyés par l’hôte de messagerie des utilisateurs et utilisatrices qui s’enregistrent, ainsi que les messages renvoyés par le ou la destinataire suite à l’email d’enregistrement. Le format par défaut de l’adresse e-mail d’expédition est postmaster@[[votre_domaine_d’installation]].com.

**Objet :** objet par défaut de l’e-mail d’activation.

**Délai d’expiration :** nombre de jours à l’issue duquel l’invitation à l’activation expire si l’utilisateur externe n’active pas le compte. La valeur par défaut est de 30 jours.

**Message :** texte qui apparaît dans le corps du message pour indiquer que le compte d’utilisateur des destinataires doit être activé. Vous souhaiterez peut-être également inclure des informations telles que la manière de contacter un administrateur ou une administratrice pour obtenir un nouveau mot de passe.

### Configurer un courrier électronique de réinitialisation de mot de passe {#configure-a-password-reset-email}

Si vous devez réinitialiser le mot de passe d’une personne invitée, un e-mail de confirmation est généré qui invite l’utilisateur ou l’utilisatrice à choisir un nouveau mot de passe. Le mot de passe d’un utilisateur ou une utilisatrice ne peut pas être déterminé. Si la personne l’oublie, vous devez le réinitialiser.

Les paramètres suivants se trouvent dans la zone E-mail de réinitialisation du mot de passe de la page d’enregistrement des utilisateurs et utilisatrices invités.

**De :** l’adresse électronique à partir de laquelle l’e-mail de réinitialisation du mot de passe est envoyé. Le format par défaut de l’adresse électronique d’expédition est postmaster@[your_installation_domain].com.

**Objet :** objet par défaut pour l’e-mail de réinitialisation.

**Message :** le texte qui apparaît dans le corps d’un message, indiquant que le mot de passe de l’utilisateur ou l’utilisatrice externe du destinataire a été réinitialisé.

## Permettre aux utilisateurs, aux utilisatrices et aux groupes de créer des politiques {#enable-users-and-groups-to-create-policies}

La page Configuration contient un lien vers la page Mes politiques, où vous spécifiez les utilisateurs finaux et utilisatrices finales qui pourront créer mes politiques, ainsi que les utilisateurs, utilisatrices et groupes qui sont visibles dans les résultats de recherche. La page Mes politiques comporte deux onglets :

**Onglet Créer des politiques :** permet de configurer les autorisations des utilisateurs pour créer des politiques personnalisées.

**Onglet Utilisateurs et groupes visibles :** permet de contrôler quels utilisateurs et groupes sont visibles dans les résultats de recherche des utilisateurs. Le superutilisateur ou la superutilisatrice ou l’équipe d’administration de l’ensemble de politiques doit sélectionner et ajouter des domaines, créés dans User Management, pour l’utilisateur, l’utilisatrice et le groupe visibles pour chaque ensemble de politiques. Cette liste est visible par le coordinateur ou la coordinatrice de l’ensemble de politiques et est utilisée pour limiter les domaines que le coordinateur ou la coordinatrice de l’ensemble de politiques peut parcourir lors du choix des personnes à ajouter aux politiques.

Avant d’autoriser les utilisateurs et utilisatrices à créer des politiques personnalisées, réfléchissez au niveau d’accès ou de contrôle que vous souhaitez accorder à chaque personne. De plus, réfléchissez au degré d’exposition que vous souhaitez donner à vos utilisateurs, utilisatrices et groupes lorsque vous les rendez visibles dans les recherches.

### Spécifier les utilisateurs, utilisatrices et groupes qui peuvent créer des politiques {#specify-users-and-groups-who-can-create-policies}

En tant qu’administrateur ou administratrice, spécifiez les personnes et les groupes qui peuvent créer des politiques personnalisées. Cette autorisation peut être définie au niveau de l’utilisateur, de l’utilisatrice et du groupe. La fonctionnalité de recherche les utilisateurs et les groupes dans la base de données User Management.

1. Dans la console d’administration, cliquez sur Services > Document Security > Configuration > Mes politiques.
1. Sur la page Mes politiques, cliquez sur l’onglet Créer des politiques, puis cliquez sur Ajouter des utilisateurs, des utilisatrices et des groupes.
1. Dans la zone Rechercher, saisissez le nom d’utilisateur ou d’utilisatrice ou l’adresse e-mail de la personne ou du groupe que vous recherchez. Si vous ne possédez pas ces informations, laissez la case vide. Vous pouvez également saisir un nom ou une adresse e-mail partiel, par exemple lorsque vous ne connaissez que les deux premières lettres d’un nom d’utilisateur ou d’utilisatrice.
1. Dans la liste Utilisation, sélectionnez vos paramètres de recherche Nom ou E-mail.
1. Dans la liste Type, sélectionnez Groupe ou Utilisateur ou utilisatrice pour affiner votre recherche.
1. Dans la liste Dans, sélectionnez le domaine à rechercher. Si vous ne connaissez pas le domaine de l’utilisateur ou utilisatrice ou du groupe, sélectionnez Tous les domaines.
1. Dans la liste Afficher, spécifiez le nombre de résultats de recherche à afficher par page, puis cliquez sur Rechercher.
1. Pour ajouter des utilisateurs, des utilisatrices et des groupes à Mes politiques, cochez la case pour chaque personne et groupe à ajouter.
1. Cliquez sur Ajouter, puis sur OK.

Les utilisateurs, utilisatrices et groupes sélectionnés sont désormais autorisés à créer des politiques personnalisées.

### Supprimer l’autorisation de création de politiques personnalisées d’un utilisateur, d’une utilisatrice ou d’un groupe {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Sur la page de Document Security, cliquez sur Configuration > Mes politiques.
1. Sur la page Mes politiques, cliquez sur l’onglet Créer des politiques. Les utilisateurs, les utilisatrices et les groupes disposant des autorisations nécessaires pour créer des politiques personnalisées sont affichés.
1. Cochez la case en regard des utilisateurs, utilisatrices et groupes à supprimer de cette autorisation.
1. Cliquez sur Supprimer, puis sur OK.

### Spécifier les utilisateurs, utilisatrices et groupes visibles dans les recherches {#specify-users-and-groups-that-are-visible-in-searches}

Lorsque les utilisateurs et utilisatrices gèrent leurs politiques personnalisées, ils peuvent rechercher des personnes et des groupes à y ajouter. Spécifiez les domaines à partir desquels les utilisateurs, utilisatrices et groupes sont visibles dans ces recherches.

1. Sur la page de Document Security, cliquez sur Configuration > Mes politiques.
1. Sur la page Mes politiques, cliquez sur l’onglet Utilisateurs, utilisatrices et groupes visibles.
1. Pour rendre visibles les utilisateurs, les utilisatrices et les groupes d’un domaine, cliquez sur Ajouter des domaines, sélectionnez les domaines, puis cliquez sur Ajouter. Pour supprimer un domaine, cochez la case en regard du nom de domaine et cliquez sur Supprimer.

## Modifier manuellement le fichier de configuration de Document Security {#manually-editing-the-document-security-configuration-file}

Vous pouvez importer et exporter les informations de configuration stockées dans la base de données de Document Security. Par exemple, vous souhaiterez peut-être réaliser une copie de sauvegarde des informations de configuration lorsque vous passez d’un environnement d’évaluation à un environnement de production, ou vous souhaiterez peut-être modifier les options avancées qui ne peuvent être configurées qu’en modifiant ce fichier.

Vous pouvez apporter les modifications suivantes à l’aide du fichier de configuration :

[Afficher les autorisations CATIA lors de la création et de la modification des politiques](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Spécifier un délai d’expiration pour la synchronisation hors ligne](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Refus d’accès aux services Document Security pour des applications spécifiques](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modification des paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Désactivation des liens externes](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L’import du fichier de configuration reconfigure votre système en fonction des informations contenues dans le fichier. Les exceptions concernent la configuration du filigrane dynamique et les informations sur les événements personnalisés, qui ne sont pas enregistrées avec le fichier de configuration exporté. Configurez ces informations manuellement dans votre nouveau système. Seul un consultant ou une consultante en services professionnels ou une équipe d’administration système connaissant Document Security et XML doit modifier le contenu d’un fichier de configuration, par exemple pour reconfigurer un paramètre corrompu ou pour ajuster les paramètres pour un scénario de déploiement d’entreprise particulier.

**Exporter un fichier de configuration**

1. Dans la console d’administration, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Exporter et enregistrez le fichier de configuration dans un autre emplacement. Le nom de fichier par défaut est config.xml.
1. Cliquez sur OK.
1. Avant de modifier le fichier de configuration, effectuez une copie de sauvegarde, au cas où vous auriez besoin de revenir en arrière.

**Importation d’un fichier de configuration**

1. Dans la console d’administration, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Parcourir pour accéder au fichier de configuration, puis sur Importer. Vous ne pouvez pas saisir le chemin directement dans la case Nom du fichier.
1. Cliquez sur OK.

### Spécifier un délai d’expiration pour la synchronisation hors ligne {#specify-a-timeout-period-for-offline-synchronization}

Document Security permet aux utilisateurs et utilisatrices d’ouvrir et d’utiliser un document protégé lorsqu’ils ne sont pas connectés au serveur Document Security. L’application cliente de l’utilisateur ou l’utilisatrice doit régulièrement se synchroniser avec le serveur pour que les documents restent valides pour une utilisation hors ligne. Lorsqu’un utilisateur ou une utilisatrice ouvre un document protégé pour la première fois, il lui est demandé si son ordinateur doit être autorisé à effectuer une synchronisation cliente périodique.

Par défaut, la synchronisation s’effectue automatiquement toutes les quatre heures et selon les besoins lorsqu’une personne est connectée au serveur Document Security. Si la période hors ligne d’un document expire alors que l’utilisateur ou l’utilisatrice est hors ligne, la personne doit se reconnecter au serveur pour permettre à l’application cliente de se synchroniser avec le serveur.

Dans le fichier de configuration Document Security, vous pouvez spécifier la fréquence par défaut de la synchronisation automatique en arrière-plan. Ce paramètre fait office de délai d’expiration par défaut pour les applications clientes, à moins que le client ou la cliente ne définisse explicitement sa propre valeur de délai d’expiration.

1. Exportez le fichier de configuration de Document Security. (Voir [Modifier manuellement le fichier de configuration Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `PolicyServer`. Sous ce nœud, recherchez le nœud `ServerSettings`.
1. Dans le nœud `ServerSettings`, ajoutez l’entrée suivante, puis enregistrez le fichier :

   `<entry key="BackgroundSyncFrequency" value="`*durée* `"/>`

   où *time* correspond au nombre de secondes entre les synchronisations automatiques en arrière-plan. Si vous définissez cette valeur sur `0`, la synchronisation a lieu en continu. La valeur par défaut est `14400` secondes (toutes les quatre heures).

1. Importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Refuser l’accès aux services Document Security pour des applications spécifiques {#denying-document-security-services-for-specific-applications}

Vous pouvez configurer Document Security de façon à ce qu’il refuse des services aux applications qui répondent à des critères spécifiques. Les critères peuvent spécifier un seul attribut, tel qu’un nom de plateforme, ou plusieurs ensembles d’attributs. Cette fonctionnalité peut vous aider à contrôler les demandes que doit traiter Document Security. Vous trouverez ci-dessous quelques applications de cette fonctionnalité :

* **Protection des revenus :** vous pouvez refuser l’accès à toute application cliente ne prenant pas en charge vos conventions de revenus.
* **Compatibilité des applications :** certaines applications peuvent être incompatibles avec les politiques ou le comportement de votre serveur Document Security.

Lorsque les applications clientes tentent d’établir un lien avec Document Security, elles fournissent des informations sur l’application, la version et la plateforme. Document Security compare ces informations aux paramètres de refus obtenus à partir de son fichier de configuration.

Les paramètres Refus peuvent contenir plusieurs ensembles de conditions de refus. Si tous les attributs d’un ensemble donné correspondent, l’application requérante se voit refuser l’accès aux services Document Security.

La fonctionnalité de refus de service nécessite que les applications clientes utilisent le SDK client C++ de Document Security version 8.2 ou ultérieure. Les produits Adobe suivants fournissent des informations produit lors de la demande de services de Document Security :

* Adobe Acrobat 9.0 Professionnel/Acrobat 9.0 Standard et versions ultérieures
* Adobe Reader 9.0 et versions ultérieures
* Extensions Acrobat Reader DC pour Microsoft Office 8.2 et versions ultérieures

Les applications clientes utilisent l’API cliente du SDK client C++ de Document Security pour demander des services à Document Security. Les requêtes de l’API cliente incluent des informations sur la plateforme et la version du SDK (précompilées dans l’API cliente) et des informations sur le produit obtenues à partir de l’application cliente.

Les applications clientes ou plug-ins clients fournissent des informations sur le produit dans leur implémentation d’une fonction de rappel. L’application contient les informations suivantes :

* Nom de l’intégrateur
* Version de l’intégrateur
* Famille d’application
* Nom d’application
* Version de l’application

Si des informations ne sont pas applicables, l’application cliente laisse le champ correspondant vide.

Plusieurs applications Adobe incluent des informations sur le produit lors de la demande de services de Document Security, notamment les extensions Acrobat, Adobe Reader et Acrobat Reader DC pour Microsoft Office.

**Acrobat et Adobe Reader**

Lorsqu’Acrobat ou Adobe Reader demandent un service de Document Security, il fournit les informations produit suivantes :

* **Intégrateur :** Adobe Systems, Inc.
* **Version de l’intégrateur :** 1.0
* **Famille de l’application :** Acrobat
* **Nom de l’application :** Acrobat
* **Version de l’application :** 9.0.0

**Extensions Acrobat Reader DC pour Microsoft Office**

Les extensions Acrobat Reader DC pour Microsoft Office sont un plug-in utilisé avec les produits Microsoft Word, Microsoft Excel et Microsoft PowerPoint de Microsoft Office. Lorsqu’il demande un service, il fournit les informations suivantes :

* **Intégrateur :** Adobe Systems Incorporated
* **Version de l’intégrateur :** 8.2
* **Famille d’applications :** Extensions d’Acrobat Reader DC pour Microsoft Office
* **Nom de l’application :** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Version de l’application :** 2003 ou 2007

**Configurer Document Security pour refuser les services pour des applications spécifiques**

1. Exportez le fichier de configuration de Document Security. (Voir [Modifier manuellement le fichier de configuration Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `PolicyServer`. Ajoutez un nœud `ClientVersionRules` comme enfant immédiat du nœud `PolicyServer`, s’il existe :

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   où :

   `SDKPlatforms` indique la plateforme hébergeant l’application cliente. Les valeurs possibles sont les suivantes :

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` indique la version de l’API Client C++ de Document Security utilisée par l’application cliente. Par exemple, `"8.2"`.

   `APPFamilies` est défini par l’API Client.

   `AppName`indique le nom de l’application cliente. Les virgules sont utilisées comme séparateurs de noms. Pour inclure une virgule dans un nom, utilisez la barre oblique inverse (\) comme caractère d’échappement. Par exemple, *« Adobe Systems\, Inc. »*.

   `AppVersions` indique la version de l’application cliente.

   `Integrators` indique le nom de la société ou du groupe ayant développé le module supplémentaire ou l’application intégrée.

   `IntegratorVersions` correspond à la version du module supplémentaire ou de l’application intégrée.

1. Pour chaque ensemble supplémentaire de données de refus, ajoutez un autre élément *MyEntryName*.
1. Enregistrez le fichier de configuration.
1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Exemples**

Dans cet exemple, l’accès est refusé à l’ensemble des clientes et des clients Windows.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

Dans cet exemple, Mon application version 3.0 et Mon autre application version 2.0 se voient refuser l’accès. La même URL d’informations sur les refus est utilisée quelle que soit la raison du refus.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

Dans cet exemple, toutes les demandes provenant d’une installation Microsoft PowerPoint 2007 ou Microsoft PowerPoint 2010 des extensions Acrobat Reader DC pour Microsoft Office sont refusées.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### Modifier les paramètres de configuration des filigranes {#change-the-watermark-configuration-parameters}

Par défaut, vous pouvez spécifier un maximum de cinq éléments dans un filigrane. De plus, la taille maximale du document PDF que vous souhaitez utiliser comme filigrane est limitée à 100 Ko. Vous pouvez modifier ces paramètres dans le fichier config.xml.

***Remarque ** : si vous modifiez ces paramètres, faites-le avec précaution.*

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `ServerSettings`.
1. Dans le nœud `ServerSettings`, ajoutez les entrées suivantes, puis enregistrez le fichier : `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`.

   La première entrée, *taille de fichier maximale* est la taille de fichier maximale (en Ko) qui est autorisée pour un élément de filigrane en format PDF. La valeur par défaut est 100 Ko.

   La deuxième entrée, *éléments maximum*, est le nombre maximum d’éléments autorisés dans un filigrane. La valeur par défaut est 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Désactiver les liens externes {#disabling-external-links}

De nombreux utilisateurs et utilisatrices de Document Security n’ont pas accès aux liens externes tels que **www.adobe.com** lorsqu’ils utilisent les interfaces utilisateur de Right Management :

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Les modifications suivantes apportées au fichier config.xml désactivent tous les liens externes des interfaces utilisateur Right Management.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. Pour désactiver tous les liens externes, dans le nœud `DisplaySettings`, ajoutez l’entrée suivante, puis enregistrez le fichier : `<entry key="ExternalLinksAllowed" value="false"/>`.

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configuration pour activer SMTP pour TSL (Transport Layer Security) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Les modifications suivantes apportées au fichier config.xml activent la prise en charge TLS pour la fonctionnalité d’enregistrement des utilisateurs et utilisatrices invités.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. Localisez le nœud suivant : `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Définissez la valeur de la clé `SmtpUseTls` du nœud `ExternalUser` sur **true**.
1. Définissez la valeur de la clé `SmtpUseSsl` du nœud `ExternalUser` sur **false**.
1. Enregistrez le fichier `config.xml`.
1. Importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Désactiver les points d’entrée SOAP pour les documents Document Security {#disable-soap-endpoints-for-document-security-documents}

Les modifications suivantes sont apportées au fichier config.xml pour désactiver les points d’entrée SOAP pour les documents de Document Security.

1. Exportez le fichier de configuration de Document Security. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et accédez au nœud suivant : `<node name="DRM">`.

   ```xml
   <node name="DRM">
   ```

1. Dans le nœud DRM, recherchez le nœud `entry` :

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Pour désactiver les points d’entrée SOAP pour les documents Document Security, définissez l’attribut de valeur sur **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Enregistrez le `config.xml`.
1. Importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Augmenter l’évolutivité du serveur de Document Security {#increasingscalability}

Par défaut, lors de la synchronisation d’un document pour une utilisation hors ligne, ainsi que des informations sur le document actuel, les clients de Document Security récupèrent les informations sur les politiques, les filigranes, les licences et les mises à jour de révocation pour tous les autres documents auxquels la personne a accès. Si ces mises à jour et informations ne sont pas synchronisées avec le client, un document ouvert en mode hors ligne peut toujours s’ouvrir avec des informations de politique, de filigrane et de révocation plus anciennes.

Vous pouvez augmenter l’évolutivité du serveur Document Security en limitant les informations envoyées au client. La réduction de la quantité d’informations envoyées au client entraîne une amélioration de l’évolutivité, une réduction du temps de réponse et de meilleures performances du serveur. Effectuez les étapes suivantes pour augmenter l’évolutivité :

1. Exportez le fichier de configuration de Document Security. (Voir [Modifier manuellement le fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud ServerSettings.
1. Dans le nœud ServerSettings, définissez la valeur de la propriété `DisableGlobalOfflineSynchronizationData` sur `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Lorsque la valeur est définie sur true, le serveur Document Security envoie des informations uniquement pour le document actif tandis que les informations relatives aux documents restants (les autres documents auxquels un utilisateur a accès) ne sont pas envoyées au client.

   >[!NOTE]
   >
   >Par défaut, la valeur de la clé `DisableGlobalOfflineSynchronizationData` est définie sur `false`.

1. Enregistrez et importez le fichier de configuration. (Voir [Modifier manuellement le fichier de configuration de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
