---
title: Configuration des options du client et du serveur
seo-title: Configuration des options du client et du serveur
description: Découvrez comment vous pouvez configurer les différentes options de client et de serveur, telles que les paramètres de configuration du serveur, les rôles de sécurité des documents et le contrôle des événements.
seo-description: Découvrez comment vous pouvez configurer les différentes options de client et de serveur, telles que les paramètres de configuration du serveur, les rôles de sécurité des documents et le contrôle des événements.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '10273'
ht-degree: 85%

---


# Configuration du serveur Document Security {#configure-the-document-security-server}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Configuration du serveur.
1. Configurez les paramètres et cliquez sur OK.

## Paramètres de configuration du serveur {#server-configuration-settings}

**URL de base :** URL de base de la sécurité du document, contenant le nom et le port du serveur. Les informations ajoutées à cette base créent des URL de connexion. Par exemple, la séquence /edc/Main.do est ajoutée pour accéder aux pages Web. Les utilisateurs externes répondent également aux demandes d’enregistrement qui leur sont adressées au moyen de cette URL.

Si vous utilisez IPv6, vous devez saisir l’URL de base sous la forme du nom de machine ou du nom DNS. Si vous utilisez une adresse IP numérique, Acrobat ne parviendra pas à ouvrir les fichiers protégés par une stratégie. Par ailleurs, utilisez une URL HTTP sécurisée (HTTPS) sur votre serveur.

>[!NOTE]
>
>l’URL de base est incorporée dans des fichiers protégés par une stratégie. Les applications clientes utilisent l’URL de base pour se reconnecter au serveur. Les fichiers protégés contiennent toujours l’URL de base, même si elle est modifiée par la suite. Si vous modifiez l’URL de base, les informations de configuration doivent être mises à jour pour tous les clients qui se connectent.

**Période de location hors connexion par défaut :** Durée par défaut pendant laquelle un utilisateur peut utiliser un document protégé hors connexion. Ce paramètre détermine la valeur de départ de la période d’ouverture hors connexion au moment de la création d’une stratégie (voir Création et modification de stratégies). A l’issue de cette période d’ouverture, le destinataire doit resynchroniser le document pour continuer à l’utiliser.

Pour plus d’informations sur le fonctionnement de la synchronisation et de l’ouverture hors connexion, reportez-vous à la section [Primer on configuring offline lease and synchronization](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Période de synchronisation hors connexion par défaut :** durée maximale pendant laquelle un document peut être utilisé hors connexion à partir du moment où il est initialement protégé.

**Délai d’expiration de la session client :** durée, en minutes, après laquelle la sécurité du document se déconnecte si un utilisateur connecté par le biais d’une application cliente n’interagit pas avec la sécurité du document.

**Autoriser l’accès des utilisateurs anonymes :** Sélectionnez cette option pour permettre la création de stratégies partagées et personnelles permettant aux utilisateurs anonymes d’ouvrir des documents protégés par une stratégie. (les utilisateurs qui ne possèdent pas de compte peuvent accéder au document, mais ils ne peuvent pas ouvrir de session Document Security ni utiliser d’autres documents protégés par une stratégie).

**Désactivation de l’accès aux clients de la version 7 :** Indique si les utilisateurs peuvent utiliser Acrobat ou Reader 7.0 pour se connecter au serveur. Lorsque cette option est sélectionnée, les utilisateurs doivent utiliser Acrobat ou Reader 8.0 et versions ultérieures pour exécuter des opérations Document Security sur des documents PDF. Si certaines stratégies exigent l’exécution d’Acrobat ou de Reader 8.0 et versions ultérieures en mode certifié lors de l’ouverture de documents protégés par une stratégie, désactivez l’accès à Acrobat ou Reader 7 (voir Spécification des droits de documents pour les utilisateurs et les groupes).

**Autoriser l’accès hors connexion par document** Sélectionnez cette option pour spécifier l’accès hors connexion par document. Si ce paramètre est activé, l’utilisateur aura accès en mode hors connexion uniquement aux documents qu’il a ouverts en ligne au moins une fois.

**Autoriser l’authentification du mot de passe du nom d’utilisateur :** Sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** Sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat client :** Sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par certificat lors de la connexion au serveur.

**Autoriser l’authentification** étendue Sélectionnez cette option pour activer l’authentification étendue, puis entrez l’URL d’entrée d’authentification étendue.

Le fait de sélectionner cette option autorise les applications clientes à utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisée et différentes options d’authentification configurées sur le serveur AEM forms. Par exemple, les utilisateurs peuvent désormais utiliser l’authentification SAML au lieu du nom d’utilisateur/mot de passe AEM forms, à partir des clients Acrobat et Reader. Par défaut, l’URL d’accueil contient *localhost* comme nom de serveur. Remplacer le nom du serveur par un nom d’hôte complet. Le nom d’hôte dans l’URL d’acceuil est automatiquement rempli à partir de l’URL de base si l’authentification étendue n’est pas encore activée. Voir [Ajout du fournisseur d’authentification étendue](configuring-client-server-options.md#add-the-extended-authentication-provider).

***Remarque ** : l’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.*

**Largeur de contrôle HTML préférée pour l’authentification** étendue Spécifiez la largeur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

**Hauteur de contrôle HTML préférée pour l’authentification** étendue Spécifiez la hauteur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

***remarque **: Les limites de largeur et de hauteur de cette boîte de dialogue sont les suivantes :*Largeur : Minimum = 400, maximum = 900

Hauteur : minimum = 450 ; maximum = 800

**Activer la mise en cache des informations d’identification client :** Sélectionnez cette option pour permettre aux utilisateurs de mettre en cache leurs informations d’identification (nom d’utilisateur et mot de passe). Lorsque les informations d’identification d’un utilisateur sont mises en cache, il n’a plus à les saisir à chaque fois qu’il ouvre un document ou lorsqu’il clique sur le bouton Actualiser de la page de gestion des stratégies de sécurité dans Adobe Acrobat. Vous pouvez spécifier le nombre de jours à l’issue duquel les utilisateurs doivent à nouveau fournir ces informations. Si le nombre de jours est fixé à 0, les informations sont mises en cache indéfiniment.

## Configuration des utilisateurs et administrateurs de Document Security {#configuring-document-security-users-and-administrators}

### Attribution de rôles Document Security aux administrateurs {#assigning-document-security-roles-to-administrators}

Votre environnement AEM forms contient un ou plusieurs administrateurs disposant des droits appropriés pour créer des utilisateurs et des groupes. Si votre entreprise utilise Document Security, au moins un administrateur doit également disposer du droit de gestion des utilisateurs invités et locaux.

Les administrateurs doivent également bénéficier du rôle Utilisateur dans Administration Console pour pouvoir accéder à Administration Console (voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).

### Configuration des utilisateurs et des groupes visibles {#configuring-visible-users-and-groups}

Pour afficher les utilisateurs et les groupes des domaines sélectionnés lors des recherches d’utilisateurs de stratégies, un super-administrateur ou un administrateur de jeux de stratégies doit sélectionner et ajouter des domaines (créés dans User Management) à la liste des utilisateurs et groupes visibles pour chaque jeu de stratégies créé.

La liste des utilisateurs et des groupes visibles est accessible au coordinateur des jeux de stratégies. Elle permet de restreindre les domaines que ce dernier peut consulter lorsqu’il choisit les utilisateurs ou les groupes à ajouter aux stratégies. Si cette tâche n’est pas effectuée, le coordinateur des jeux de stratégies ne trouvera aucun utilisateur ni aucun groupe à ajouter aux stratégies. Un jeu de stratégies peut avoir plusieurs coordinateurs.

1. Après avoir installé et configuré l’environnement AEM forms avec Document Security, définissez tous les domaines appropriés dans Gestion des utilisateurs <!-- Fix broken link (See Setting up and managing domains) -->

   ***Remarque ** : vous devez commencer par créer les domaines avant de pouvoir créer des stratégies.*

1. Dans Administration Console, cliquez sur Services > Gestion des documents > Stratégies et cliquez sur l’onglet Jeux de stratégies.
1. Sélectionnez Jeu de stratégies global, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter des domaines et ajoutez les domaines nécessaires.
1. Naviguez jusqu’à Services > Document Security > Configuration > Mes stratégies et cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter des domaines et ajoutez les domaines nécessaires.

## Ajout du fournisseur d’authentification étendue {#add-the-extended-authentication-provider}

AEM forms fournit un exemple de configuration que vous pouvez personnaliser en fonction de votre environnement. Exécutez les étapes suivantes :

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

1. Obtention et déploiement du fichier WAR. Voir le guide d’installation approprié pour votre serveur d’applications.
1. Vérification que le serveur Forms dispose d’un nom complet au lieu d’adresses IP en tant qu’URL de base et que l’URL est sécurisée (HTTPS). Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Activation de l’authentification étendue à partir de la page de configuration du serveur. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Ajout d’URL obligatoire de redirection d’authentification unique dans le fichier de configuration de User Management. Voir [Ajout d’URL de redirection d’authentification unique pour l’authentification étendue](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Ajout d’URL de redirection d’authentification unique pour l’authentification étendue {#add-sso-redirect-urls-for-extended-authentication}

Lorsque l’authentification étendue est activée, une boîte de dialogue d’authentification s’affiche pour les utilisateurs qui ouvrent un document protégé par une stratégie dans Acrobat XI ou Reader XI. Cette boîte de dialogue charge la page HTML que vous avez indiquée comme URL d’accueil de l’authentification étendue dans les paramètres du serveur Document Security. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter et enregistrez le fichier de configuration sur votre disque.
1. Ouvrez le fichier dans un éditeur et recherchez le nœud AllowedUrls.
1. In the `AllowedUrls` node, add the following lines: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Enregistrez le fichier, puis importez le fichier mis à jour depuis la page Configuration manuelle : Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.

## Configuration de la sécurité hors connexion {#configuring-offline-security}

Document Security permet d’utiliser des documents protégés par une stratégie sans être connecté à Internet ou à un réseau. Cette fonction requiert que la stratégie autorise l’accès hors connexion, comme décrit dans [Spécification des droits de documents pour les utilisateurs et les groupes](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Avant qu’un document protégé par une telle stratégie puisse être utilisé hors connexion, le destinataire doit ouvrir ce dernier pendant qu’il est connecté et activer l’accès hors connexion en cliquant sur Oui lorsqu’il y est invité. Le destinataire doit parfois s’authentifier. Il peut alors utiliser le document hors connexion pendant la période d’ouverture hors connexion spécifiée dans la stratégie.

A l’issue de la période d’ouverture hors connexion, le destinataire doit resynchroniser le document avec Document Security, soit en ouvrant le document en ligne, soit en utilisant une commande de resynchronisation d’Acrobat ou du menu des extensions d’Acrobat Reader DC (voir l’*Aide d’Acrobat* ou l’*Aide des extensions d’Acrobat Reader DC* appropriée).

Comme les documents qui autorisent un accès hors connexion utilisent également une clé de chiffrement mise en cache sur l’ordinateur sur lequel les fichiers sont stockés hors connexion, les documents peuvent être compromis si un utilisateur non autorisé se procure la clé. Pour vous protéger contre ce risque, des options de roulement manuel et programmé des clés sont fournies. Il vous suffit de les configurer pour empêcher un utilisateur non autorisé d’accéder au document.

### Définition d’une période d’ouverture hors connexion par défaut {#set-a-default-offline-lease-period}

Les destinataires de documents protégés par une stratégie peuvent mettre ces documents hors connexion pendant le nombre de jours spécifiés dans la stratégie. Après la synchronisation initiale du document avec Document Security, le destinataire peut l’utiliser hors connexion jusqu’à la fin de la période d’ouverture hors connexion. A l’issue de cette période, il doit remettre le document en ligne et ouvrir une session pour le synchroniser avec Document Security et continuer à l’utiliser.

Vous pouvez configurer une période d’ouverture hors connexion par défaut. Cette période par défaut peut être modifiée lors de la création ou de la modification d’une stratégie.

1. Dans la page Document Security, cliquez sur Configuration > Configuration du serveur.
1. Dans le champ Période d’ouverture hors connexion par défaut, indiquez un nombre de jours.
1. Cliquez sur OK.

### Gestion des roulements de clés {#manage-key-rollovers}

Document Security protège les documents à l’aide d’algorithmes de chiffrement et de licences. Lorsqu’il chiffre un document, Document Security génère et gère une clé de déchiffrement, appelée *DocKey*, qu’il transmet à l’application cliente. Si la stratégie qui protège un document autorise un accès hors connexion, une clé hors connexion, appelée *clé principale*, est également générée pour chaque utilisateur disposant d’un accès hors connexion au document.

>[!NOTE]
>
>Si aucune clé principale n’existe, Document Security en génère une pour protéger un document.

Pour ouvrir un document hors connexion protégé par une stratégie, l’ordinateur de l’utilisateur doit posséder la clé principale appropriée. Il doit obtenir la clé principale lorsque l’utilisateur se synchronise avec Document Security (ouvre un document protégé en ligne). Si cette clé principale est compromise, tout document pour lequel l’utilisateur dispose d’un accès hors connexion est également compromis.

L’un des moyens permettant de réduire la menace portant sur les documents hors connexion consiste à refuser l’accès hors connexion à certains documents sensibles. Une autre méthode consiste à procéder à un roulement régulier des clés principales. Lorsque Document Security effectue un roulement de clés, les clés existantes n’ont plus accès aux documents protégés par une stratégie. Par exemple, si un intrus récupère une clé principale sur un ordinateur portable volé, cette clé ne lui permet pas d’accéder aux documents protégés après le roulement. De plus, si vous pensez qu’une clé principale a été compromise, vous pouvez effectuer un roulement manuel de cette clé.

Gardez cependant à l’esprit qu’un roulement de clés modifie toutes les clés principales, et non une seule. Il limite également l’évolutivité du système car les clients doivent stocker davantage de clés pour l’accès hors connexion. La fréquence de roulement par défaut des clés est de 20 jours. Il est recommandé de ne pas définir une valeur inférieure à 14 jours car certains utilisateurs ne pourront plus consulter des documents hors connexion et les performances du système peuvent en pâtir.

Dans l’exemple suivant, Clé1 est la plus ancienne des deux clés principales, et Clé2 la plus récente. Lorsque vous cliquez sur le bouton Exécuter le roulement des clés maintenant pour la première fois, Clé1 est invalidée et une nouvelle clé principale valide (Clé3) est générée. Les utilisateurs peuvent obtenir Clé3 en synchronisant Document Security, généralement en ouvrant un document protégé en ligne. Néanmoins, les utilisateurs ne sont pas obligés d’effectuer la synchronisation avec Document Security avant d’avoir atteint la période d’ouverture hors connexion maximale indiquée par une stratégie. Après le premier roulement de clés, les utilisateurs qui restent hors connexion peuvent continuer à ouvrir des documents hors connexion, dont ceux protégés par Clé3, jusqu’à expiration de la période d’ouverture hors connexion maximale. Lorsque vous cliquez sur le bouton Exécuter le roulement des clés maintenant pour la seconde fois, Clé2 est invalidée et une nouvelle clé, Clé4, est générée. Les utilisateurs qui restent hors connexion durant les deux roulements de clés ne peuvent pas ouvrir les documents protégés par Clé3 et Clé4 avant leur synchronisation avec Document Security.

**Modification de la fréquence de roulement des clés**

Pour des raisons de confidentialité, lorsque vous utilisez des documents hors connexion, Document Security fournit une option de roulement automatique des clés avec une fréquence par défaut de 20 jours. Vous pouvez modifier cette fréquence de roulement, mais évitez de définir une valeur inférieure à 14 jours car certains utilisateurs ne pourront plus consulter des documents hors connexion et les performances du système peuvent en pâtir.

1. Dans la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Dans le champ Fréquence de roulement des clés, indiquez la durée en jours de la période de roulement.
1. Cliquez sur OK.

**Roulement manuel des clés principales**

Pour garantir la confidentialité des documents hors connexion, vous pouvez effectuer un roulement manuel des clés principales. Vous pouvez être contraint d’effectuer cette opération, notamment si la clé est compromise par une personne qui se l’est procurée sur un ordinateur sur lequel cette clé est mise en cache pour autoriser l’accès hors connexion à un document.

>[!NOTE]
>
>évitez les roulements manuels fréquents car ils modifient toutes les clés principales (et non une seule) et peuvent temporairement empêcher les utilisateurs d’afficher les nouveaux documents en ligne.

Vous devez rouler deux fois les clés principales avant que les clés précédentes sur les ordinateurs client soient invalidées. Les ordinateurs clients ayant invalidé des clés principales doivent se resynchroniser avec le service Document Security afin d’obtenir les nouvelles clés principales.

1. Dans la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Cliquez sur Exécuter le roulement des clés maintenant, puis sur OK.
1. Attendez 10 minutes environ. The following log message appears in the server log: `Done RightsManagement key rollover for`*N *`principals`. Dans ce message, la lettre* N *correspond au nombre d’utilisateurs du système Document Security.
1. Cliquez sur Exécuter le roulement des clés maintenant, puis sur OK.
1. Attendez 10 minutes environ.

## Configuration des options de contrôle et de confidentialité des événements {#configuring-event-auditing-and-privacy-settings}

Document Security peut contrôler et enregistrer des informations sur les événements liés aux interactions avec des documents protégés par une stratégie, des stratégies, des administrateurs et le serveur. Vous pouvez configurer le contrôle des événements et spécifier les types d’événements à contrôler. Pour contrôler les événements d’un document particulier, l’option de contrôle doit également être activée dans la stratégie.

Lorsque le contrôle est activé, vous pouvez afficher les détails des événements contrôlés dans la page Evénements. Les utilisateurs de Document Security peuvent également afficher les événements concernant les documents protégés par une stratégie qu’ils utilisent ou qu’ils créent.

Les événements qu’il est possible de contrôler sont les suivants :

* les événements concernant les documents protégés par une stratégie, tels que les tentatives d’ouverture de documents par des utilisateurs autorisés ou non ;
* les événements concernant les stratégies, comme la création, la modification, la suppression, l’activation et la désactivation de stratégies ;
* les événements concernant les utilisateurs, comme les invitations et les enregistrements d’utilisateurs externes, les comptes d’utilisateurs activés et désactivés, les modifications des mots de passe et les mises à jour de profils ;
* les événements AEM forms, tels que les versions incohérentes, le serveur d’annuaire et les fournisseurs d’autorisations indisponibles, et les modifications apportées à la configuration du serveur.

### Activation ou désactivation du contrôle des événements {#enable-or-disable-event-auditing}

Vous pouvez activer et désactiver le contrôle des événements concernant le serveur, les documents protégés par une stratégie, les stratégies, les jeux de stratégies et les utilisateurs. Lorsque vous activez le contrôle des événements, vous pouvez choisir de contrôler tous les événements ou sélectionner certains événements à contrôler.

Lorsque vous activez le contrôle du serveur, vous pouvez afficher les éléments contrôlés dans la page Evénements.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le contrôle du serveur, sélectionnez Oui ou Non sous Activer le contrôle du serveur.
1. Si vous avez sélectionné Oui, effectuez l’une des opérations ci-après sous chacune des catégories d’événements pour sélectionner les options à contrôler :

   * Sélectionnez Tous pour contrôler tous les événements figurant dans la catégorie.
   * Pour contrôler certains événements seulement, désélectionnez Tous, puis cochez les cases en regard des événements à contrôler

      (voir [Options de contrôle des événements](configuring-client-server-options.md#event-auditing-options)).

1. Cliquez sur OK.

>[!NOTE]
>
>lorsque vous travaillez sur des pages Web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette opération risque de capturer des données non souhaitées et d’entraîner des problèmes d’affichage.

### Activation ou désactivation de la notification de confidentialité {#enable-or-disable-privacy-notification}

Vous pouvez activer ou désactiver le message de la notification de confidentialité. Lorsque vous activez la notification de confidentialité, un message apparaît lorsqu’un destinataire tente d’ouvrir un document protégé par une stratégie. Cette notification informe l’utilisateur que le document fait l’objet d’un contrôle. Vous pouvez également spécifier une URL permettant à l’utilisateur d’afficher la page de votre stratégie de confidentialité si elle est disponible.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer la notification de confidentialité, sélectionnez Oui ou Non sous Activer la notification de confidentialité.

   Si la stratégie liée à un document permet aux utilisateurs de se connecter anonymement et que l’option Activer la notification de confidentialité est définie sur Non, l’utilisateur n’est pas invité à se connecter et le message de notification de confidentialité ne s’affiche pas.

   Si la stratégie liée à un document ne permet pas aux utilisateurs de se connecter anonymement, l’utilisateur peut voir le message de notification de confidentialité.

1. Le cas échéant, dans la zone URL de confidentialité, saisissez l’URL pointant vers la page de votre stratégie de confidentialité. Si la zone URL de confidentialité est laissée vide, la page de confidentialité de adobe.com s’affiche.
1. Cliquez sur OK.

>[!NOTE]
>
>La désactivation de la notification de confidentialité ne désactive pas le contrôle d’utilisation du document. Des actions de contrôle hors champ et des actions personnalisées gérées via le suivi des utilisations étendues peuvent toujours collecter des informations sur le comportement des utilisateurs.

### Importation d’un type d’événement de contrôle personnalisé {#import-a-custom-audit-event-type}

Si vous utilisez une application compatible Document Security qui gère le contrôle d’événements supplémentaires, tels que les événements propres à un certain type de fichier, un partenaire Adobe peut vous fournir des événements de contrôle personnalisés à importer dans Document Security. N’utilisez cette fonction que si un partenaire Adobe vous a fourni des types d’événements personnalisés.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Cliquez sur Parcourir pour trouver le fichier XML à importer, puis cliquez sur Importer.
1. L’importation remplace les types d’événements de contrôle personnalisés existant sur le serveur si des combinaisons d’espace de nom et de code d’événement identiques sont détectées.
1. Cliquez sur OK.

### Suppression d’un type d’événement de contrôle personnalisé {#delete-a-custom-audit-event-type}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Désélectionnez la case à cocher correspondant au type d’événement de contrôle personnalisé à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK.

### Exportation d’événements de contrôle {#export-audit-events}

Vous pouvez exporter des événements de contrôle vers un fichier dans un but d’archivage.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Modifiez les paramètres de la section Exporter les événements de contrôle selon les besoins. Vous pouvez préciser les points suivants :

   * L’âge minimum des événements de contrôle à exporter.
   * Le nombre maximum d’événements de contrôle à inclure dans un seul fichier. Le serveur génère un ou plusieurs fichiers en fonction de cette valeur.
   * Le dossier dans lequel le fichier est créé. Ce dossier se trouve sur le serveur Forms. Si le chemin d’accès au dossier est relatif, il est alors relatif au répertoire racine du serveur d’applications.
   * Le préfixe de fichier à utiliser pour les fichiers d’événements de contrôle.
   * Le format du fichier, soit un fichier CSV (valeurs séparées par des virgules) compatible avec Microsoft Excel, soit un fichier XML.

1. Cliquez sur Exporter. Si vous souhaitez annuler l’exportation, cliquez sur Annuler l’exportation. Si un autre utilisateur a planifié une exportation, le bouton Annuler l’exportation n’est pas disponible avant la fin de l’exportation. Le bouton Annuler l’exportation n’est pas disponible si un autre utilisateur a planifié une exportation. Pour vérifier si une opération d’exportation ou de suppression planifiée a démarré ou est terminée, cliquez sur Actualiser.

### Suppression d’événements de contrôle {#delete-audit-events}

Vous pouvez supprimer les événements de contrôle dont la date est antérieure au nombre de jours spécifié.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Sous Supprimer les événements de contrôle, indiquez le nombre de jours dans la zone Supprimer les événements de contrôle antérieurs à.
1. Cliquez sur Supprimer. Cliquez sur Exporter. Si vous souhaitez annuler la suppression, cliquez sur Annuler la suppression. Si un autre utilisateur a planifié une suppression, le bouton Annuler la suppression n’est pas disponible avant la fin de l’exportation. Le bouton Annuler la suppression n’est pas disponible si un autre utilisateur a planifié une exportation. Pour vérifier si une opération de suppression planifiée a démarré ou est terminée, cliquez sur Actualiser.

### Options de contrôle des événements {#event-auditing-options}

Vous pouvez activer et désactiver le contrôle des événements et spécifier les types d’événements à contrôler.

**Evénements de document**

**Document de Vue :** Un destinataire vue un document protégé par une stratégie.

**Document de fermeture :** Un destinataire ferme un document protégé par une stratégie.

**Imprimer en basse résolution** Un destinataire imprime un document protégé par une stratégie avec l’option de basse résolution spécifiée.

**Imprimer en haute résolution :** Un destinataire imprime un document protégé par une stratégie avec l’option haute résolution spécifiée.

**Ajouter l&#39;annotation au Document :** Un destinataire ajoute une annotation à un document PDF.

**Révoquer le Document :** un utilisateur ou un administrateur révoque l’accès à un document protégé par une stratégie.

**Annuler la révocation du Document :** Un utilisateur ou un administrateur rétablit l’accès à un document protégé par une stratégie.

**Remplissage du formulaire :** Un destinataire saisit des informations dans un document PDF qui est un formulaire à remplir.

**Stratégie supprimée :** Un éditeur supprime une stratégie d’un document pour retirer les protections de sécurité.

**Modifier l’URL de révocation du Document :** Un appel au niveau de l’API modifie l’URL de révocation spécifiée afin d’accéder à un nouveau document qui remplace un document révoqué.

**Modifier le Document :** Un destinataire modifie le contenu d’un document protégé par une stratégie.

**Signer le Document :** Un destinataire signe un document.

**Protéger un nouveau Document :** Un utilisateur applique une stratégie pour protéger un document.

**Changer de stratégie en Document :** Un utilisateur ou un administrateur change la stratégie associée à un document.

**Publier le Document sous :** Un nouveau document dont le nom de document et la licence sont identiques à un document existant est enregistré sur le serveur et les documents n’ont pas de relation parent-enfant. Cet événement peut être déclenché à l’aide du SDK d’AEM forms.

**Document d&#39;itération :** Un nouveau document dont le nom de document et la licence sont identiques à un document existant est enregistré sur le serveur et les documents ont une relation parent-enfant. Cet événement peut être déclenché à l’aide du SDK d’AEM forms.

**Evénements de stratégie**

**Stratégie créée :** un utilisateur ou un administrateur crée une stratégie.

**Stratégie activée :** un administrateur rend une stratégie disponible.

**Stratégie modifiée :** un utilisateur ou un administrateur modifie une stratégie.

**Stratégie désactivée :** un administrateur rend une stratégie indisponible.

**Stratégie supprimée :** un utilisateur ou un administrateur supprime une stratégie.

**Modifier le propriétaire de la stratégie :** Un appel au niveau de l’API modifie le propriétaire de la stratégie.

**Evénements d’utilisateur**

**Utilisateur supprimé :** Un administrateur supprime un compte utilisateur.

**Enregistrer un utilisateur invité :** Un utilisateur externe s’enregistre avec document security.

**Connexion réussie :** Tentatives de connexion réussies des administrateurs ou des utilisateurs.

**Utilisateurs invités :** Document security invite un utilisateur à s’enregistrer.

**Utilisateurs activés :** Les utilisateurs externes activent leurs comptes à l’aide de l’URL figurant dans le courrier électronique de l’activation, ou un administrateur active un compte.

**Modifier le mot de passe :** Les utilisateurs invités modifient leur mot de passe ou un administrateur réinitialise un mot de passe pour un utilisateur local.

**Échec de la connexion :** Échec des tentatives de connexion des administrateurs ou des utilisateurs.

**Utilisateurs désactivés :** Un administrateur désactive un compte d’utilisateur local.

**Mise à jour du Profil :** Les utilisateurs invités modifient leur nom, nom d’organisation et mot de passe.

**Compte verrouillé :** un administrateur verrouille un compte.

**Evénements de jeu de stratégie**

**CreatedPolicy Set :** Un administrateur ou un coordinateur de jeux de stratégies crée un jeu de stratégies.

**Jeu de stratégies supprimé :** un administrateur ou un coordinateur de jeux de stratégies supprime un jeu de stratégies.

**Jeu de stratégies modifié :** un administrateur ou un coordinateur de jeux de stratégies modifie un jeu de stratégies.

**Evénements de système**

**Synchronisation des annuaires terminée :** Ces informations ne sont pas disponibles sur la page Événements. Les informations actuelles sur la synchronisation des annuaires, notamment l’état de synchronisation actuel et la date de la dernière synchronisation, s’affichent sur la page Gestion des domaines. Pour atteindre la page Gestion des domaines dans Administration Console, cliquez sur Paramètres > Gestion des domaines > Gestion des domaines.

**Activation de l&#39;accès hors connexion du client :** Un utilisateur a activé l’accès hors connexion aux documents sécurisés par rapport au serveur sur l’ordinateur de l’utilisateur.

**L’application cliente** synchronisée doit synchroniser les informations avec le serveur pour autoriser l’accès hors connexion.

**Version incohérente :** Une version du SDK AEM forms incompatible avec le serveur a tenté de se connecter au serveur.

**Informations sur la synchronisation des annuaires :** Ces informations ne sont pas disponibles sur la page Événements. Les informations actuelles sur la synchronisation des annuaires, notamment l’état de synchronisation actuel et la date de la dernière synchronisation, s’affichent sur la page Gestion des domaines. Pour atteindre la page Gestion des domaines dans Administration Console, cliquez sur Paramètres > Gestion des domaines > Gestion des domaines.

**Modification de la configuration du serveur :** Modifications apportées à la configuration du serveur par le biais des pages Web ou manuellement en important un fichier config.xml. Ceci inclut les modifications de l’URL de base, les délais d’expiration des sessions, les ouvertures de session verrouillées, les paramètres d’annuaire, les roulements de clés, les paramètres du serveur SMTP pour l’enregistrement externe, la configuration des filigranes, les options d’affichage, etc.

## Configuration du suivi de l’utilisation étendue {#configuring-extended-usage-tracking}

Document Security peut suivre divers événements personnalisés qui peuvent survenir sur un document protégé. Vous pouvez activer le suivi des événements depuis le serveur Document Security au niveau global ou au niveau stratégique. Vous pouvez ensuite configurer un JavaScript pour capturer les actions spécifiques effectuées dans un fichier PDF protégé tel qu’un clic sur un bouton ou l’enregistrement du document. Ces données d’utilisation sont envoyées sous la forme d’un fichier XML de paires clé/valeur, que vous pouvez utiliser pour une analyse ultérieure. Les utilisateurs finaux accédant aux documents protégés peuvent autoriser ou refuser un tel suivi à partir de l’application cliente.

Si le suivi est activé au niveau global, vous pouvez remplacer ce paramètre au niveau stratégique et le désactiver pour une stratégie particulière. Le remplacement au niveau stratégique n’est pas possible si le suivi est désactivé au niveau global. La liste du suivi des événements est automatiquement envoyée vers le serveur lorsque le nombre d’événements atteint 25 ou lorsque le document est fermé. Vous pouvez également configurer votre script pour envoyer la liste des événements de manière explicite selon vos besoins. Vous pouvez personnaliser le suivi des événement en accédant aux propriétés des objets et aux méthodes Document Security.

Une fois que vous avez activé le suivi, l’ensemble des stratégies créées par la suite comporteront cette option activée par défaut. Les stratégies créées avant l’activation du suivi sur le serveur doivent être mises à jour manuellement.

### Activation ou désactivation du suivi des utilisations étendues {#enable-or-disable-extended-usage-tracking}

Avant de commencer, assurez-vous que le contrôle du serveur est activé. Voir [Configuration des options de contrôle et de confidentialité des événements](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) pour plus d’informations sur le contrôle.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le suivi des utilisations étendues, dans la zone Activation du suivi, sélectionnez Oui ou Non.
1. Pour définir la sélection de la caser à cocher Permettre la collecte des données d’utilisation détaillées sur la page de connexion, dans la zone Activation du suivi par défaut, sélectionnez Oui ou Non.

Pour afficher les événements suivis vous pouvez utiliser le filtre des événements de document sur la page Evénements. Les événements faisant l’objet d’un suivi à l’aide de JavaScript sont étiquetés comme faisant l’objet d’un suivi détaillé de l’utilisation. Voir [Contrôle des événements](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) pour plus d’informations sur les événements.

## Configuration des paramètres d’affichage de Document Security {#configure-document-security-display-settings}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Options d’affichage.
1. Configurez les paramètres et cliquez sur OK.

### Paramètres d’affichage {#display-settings}

**Lignes à afficher pour les résultats de la recherche :** Nombre de lignes qui apparaissent sur une page lorsque des recherches sont effectuées.

**Personnalisation de la boîte de dialogue d’ouverture de session client**

Ces paramètres contrôlent le texte affiché dans l’invite d’ouverture de session qui apparaît lorsqu’un utilisateur se connecte à Document Security par le biais d’une application cliente.

**Texte de bienvenue :** texte du message de bienvenue, tel que &quot;Veuillez vous connecter avec votre nom d’utilisateur et votre mot de passe&quot;. Le message de bienvenue doit contenir des informations sur la marche à suivre pour ouvrir une session Document Security et pour contacter un administrateur ou une autre personne chargée du support dans votre entreprise. Par exemple, des utilisateurs externes peuvent être amenés à contacter un administrateur s’ils ont oublié leur mot de passe ou qu’ils ont besoin d’aide pour ouvrir une session ou pour s’enregistrer. Le texte de bienvenue peut contenir un maximum de 512 caractères.

**Texte du nom d’utilisateur :** Libellé de texte de la zone de nom d’utilisateur.

**Texte du mot de passe :** Libellé de texte de la zone de mot de passe.

**Personnalisation de la boîte de dialogue d’authentification de certificat client**

Ces paramètres contrôlent le texte affiché dans la boîte de dialogue d’authentification de certificat.

**Choisir le type d&#39;authentification Texte :** Texte affiché pour demander à un utilisateur de sélectionner un type d’authentification.

**Choisir le texte du certificat :** Texte affiché pour demander à un utilisateur de sélectionner un type de certificat.

**Texte d&#39;erreur Certificats non disponibles :** Message contenant jusqu’à 512 caractères à afficher lorsque le certificat sélectionné n’est pas disponible.

**Personnalisation de l’affichage du certificat client**

**Afficher uniquement les informations d’identification approuvées :** Lorsque cette option est sélectionnée, l’application cliente ne présente à l’utilisateur que les certificats des émetteurs d’informations d’identification pour lesquels AEM forms est configuré pour faire confiance (voir Gestion des certificats et des informations d’identification). Lorsque cette option n’est pas sélectionnée, l’utilisateur voit apparaître la liste de tous les certificats présents sur le système de l’utilisateur.

## Configuration des filigranes dynamiques {#configure-dynamic-watermarks}

Document Security vous permet de configurer les paramètres par défaut des filigranes dynamiques que vous appliquez lors de la création des stratégies. Un *filigrane* est une image qui se superpose au texte d’un document. Il permet d’assurer le suivi du contenu d’un document et de détecter une utilisation illégale de ce contenu.

Un filigrane dynamique peut consister en du texte inventé de variables définies, telles que l’ID utilisateur, une date ou du texte personnalisé, ou en du contenu riche d’un fichier PDF. Vous pouvez configurer les filigranes avec plusieurs éléments, chacun d’entre eux ayant leur propre format et positionnement.

Les filigranes ne sont pas modifiables et optimisent la confidentialité du contenu du document. Les filigranes dynamiques garantissent également l’affichage d’un nombre suffisant d’informations concernant l’utilisateur pour décourager toute diffusion abusive du document.

Le filigrane spécifié par une stratégie apparaît dans le document protégé par une stratégie lorsqu’un destinataire affiche ou imprime le document. Contrairement aux filigranes permanents, un filigrane dynamique n’est jamais enregistré dans le document, offrant ainsi la souplesse nécessaire lors du déploiement d’un document dans un environnement d’intranet pour garantir l’affichage de l’identité de l’utilisateur par l’application utilisée. De plus, si un document a plusieurs utilisateurs, l’emploi du filigrane dynamique signifie que vous pouvez utiliser un seul document au lieu de plusieurs versions, chacune avec un filigrane différent. Le filigrane qui apparaît indique l’identité de l’utilisateur courant.

Notez que les filigranes dynamiques diffèrent des filigranes que les utilisateurs peuvent ajouter directement au document dans Acrobat. Un document protégé par une stratégie peut donc contenir deux filigranes.

### Remarques concernant la création de filigranes {#considerations-when-creating-watermarks}

Vous pouvez créer un filigrane dynamique avec plusieurs éléments de filigrane, chaque élément étant défini au format texte ou PDF. Vous pouvez inclure jusqu’à cinq éléments dans un filigrane.

Si vous choisissez un filigrane au format texte, vous pouvez définir plusieurs éléments dans le filigrane, comportant plusieurs entrées de texte, et vous pouvez également définir l’emplacement de chaque élément. Donnez des noms significatifs à ces éléments, tels en-tête, pied de page, etc.

Par exemple, si vous souhaitez définir un texte différent pour les en-têtes, les pieds de page et autres marges, dans l’ensemble du document en tant que filigrane, créez plusieurs éléments de filigrane et précisez leur emplacement. Si vous souhaitez que l’ID utilisateur et la date actuelle d’accès au document apparaissent dans l’en-tête, que le nom de la police soit indiqué dans la marge de droite et qu’un texte personnalisé indiquant « CONFIDENTIEL » apparaissent en diagonale sur le document, définissez des éléments de filigrane différents de type texte et précisez leur formatage et leur emplacement. Lorsque le filigrane est appliqué à un document, tous les éléments du filigrane sont appliqués en même temps à ce document, dans l’ordre dans lequel ils ont été ajoutés au filigrane.

En règle générale, les filigranes au format PDF sont utilisés pour ajouter du contenu graphique, tel que des logos, ou des symboles spéciaux, tels que le symbole de droits d’auteur ou celui de marque déposée.

Vous pouvez changer les limites de nombre d’éléments de filigrane, ainsi que la taille du fichier PDF en modifiant le fichier de configuration de Document Security (voir [Modification des paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters)).

Lorsque vous configurez un filigrane, tenez compte des points suivants :

* Vous ne pouvez pas utiliser de document PDF protégé par un mot de passe en tant qu’élément de filigrane. Toutefois, si le filigrane que vous créez contient d’autres éléments qui ne sont pas protégée par mot de passe, ils seront appliqués en tant que partie intégrante du filigrane.
* Vous pouvez modifier la taille maximum d’un fichier PDF que vous souhaitez utiliser comme élément de filigrane. Toutefois, les documents PDF volumineux utilisés comme filigranes dégradent les performances lors de la synchronisation hors connexion de documents appliqué avec lesdits filigranes (voir [Modification des paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters)).
* Seule la première page du fichier PDF sélectionné est utilisée par le filigrane. Assurez-vous donc que les informations que vous souhaitez que le filigrane prenne en compte se trouvent à la première page du fichier PDF.
* Même si vous pouvez définir le cadrage du document PDF, faites attention au format de page ainsi qu’à la mise en page du PDF lorsque vous envisagez de l’utiliser en tant que filigrane pour les en-têtes, les pieds de page ou les marges.
* Lorsque vous définissez le nom de la police, assurez-vous de saisir son nom correctement. AEM forms remplace la police que vous avez spécifiée si celle-ci n’existe pas dans l’ordinateur client sur lequel le document est ouvert.
* Si vous avez choisi un filigrane au format texte, définir le cadrage sur Page entière ne fonctionne pas pour les pages dont la largeur est différente.
* Lorsque vous définissez l’emplacement des éléments du filigrane, assurez-vous qu’à chaque élément correspond un emplacement différent. Si deux éléments de filigrane ont le même emplacement (centre par exemple), ils apparaîtront l’un sur l’autre dans le document, dans l’ordre auquel ils ont été ajoutés au filigrane.
* Lorsque vous définissez la taille et le type de police, assurez-vous que tout le texte apparaît dans la page. Le texte est restructuré en de nouvelles lignes, donc il est possible que le contenu du filigrane que vous souhaitez voir apparaître dans les marges chevauche la zone de texte dans certaines pages. Toutefois, si le document est ouvert à l’aide d’Acrobat 9, le texte allant au-delà d’une ligne est tronqué.

### Limite des filigranes dynamiques {#limitations-of-dynamic-watermarks}

Certaines applications clientes ne gèrent pas les filigranes dynamiques Consultez l’Aide des extensions d’Acrobat Reader DC appropriée. En outre, gardez à l’esprit les points suivants concernant les versions d’Acrobat prenant en charge en charge les filigranes dynamiques :

* Vous ne pouvez pas utiliser de document PDF protégé par un mot de passe en tant qu’élément de filigrane.
* Les versions d’Acrobat et d’Adobe antérieures à la version 10 ne prennent pas en charge les fonctionnalités de filigrane suivantes :

   * Les filigranes au format PDF
   * Des éléments multiples dans un filigrane (texte/PDF)
   * Les options avancées telles que l’étendue de page ou les options d’affichage
   * Les options de formatage de texte telles qu’une police, ou une couleur ou un nom de police Cependant, des versions antérieures d’Acrobat et de Reader affichent le contenu de texte dans la police et la couleur par défaut.

* Acrobat 9.0 et versions antérieures : Acrobat 9.0 et les versions antérieures ne prennent pas en charge les noms de stratégie dans les filigranes dynamiques. Si Acrobat 9.0 ouvre un document protégé par une stratégie avec un filigrane dynamique qui contient un nom de stratégie et d’autres données dynamiques, le filigrane est affiché sans le nom de la stratégie. Si le filigrane dynamique inclut uniquement le nom de la stratégie, Acrobat affiche un message d’erreur

### Ajout d’un modèle de filigrane dynamique {#add-a-dynamic-watermark-template}

Vous pouvez créer des modèles de filigrane dynamique. Ces modèles restent disponibles comme options de configuration pour les stratégies que les administrateurs ou les utilisateurs créent.

>[!NOTE]
>
>les informations de configuration des filigranes dynamiques ne sont pas capturées avec les autres informations de configuration lorsque vous exportez un fichier de configuration.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cliquez sur Nouveau.
1. Dans la zone Nom, saisissez le nom du nouveau filigrane.

   ***Remarque ** : certains caractères spéciaux ne peuvent être utilisés dans le nom ou la description des filigranes ou des éléments de filigrane. (voir les limites listées dans[Eléments à prendre en compte concernant la modification de stratégies](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)).*

1. Dans le champ Nom, à côté du signe plus, saisissez un nom significatif pour l’élément de filigrane, comme en-tête par exemple, ajoutez une description, puis cliquez sur le signe plus pour afficher les options.
1. Dans Source, sélectionnez le type de filigrane souhaité : texte ou PDF.
1. Si vous sélectionnez Texte, effectuez les étapes suivantes :

   * Sélectionnez les types de filigrane à inclure. Si vous sélectionnez Texte personnalisé, saisissez dans le champ adjacent le texte à afficher en filigrane. Gardez à l’esprit la longueur du texte qui apparaîtra en filigrane.
   * Indiquez les propriétés de mise en forme du texte devant apparaître en filigrane, à savoir le nom et la taille de la police, la couleur de premier plan et celle d’arrière-plan. Spécifiez les couleurs de premier plan et d’arrière-plan en tant que valeurs hexadécimales.

      ***Remarque ** : si vous définissez le cadrage sur Page entière, vous ne pouvez pas modifier la taille de la police.*

1. Si vous sélectionnez le format PDF pour les options de filigrane riches, cliquez sur **Parcourir**, à côté de Sélectionner le PDF du filigrane, pour sélectionner le document PDF que vous voulez utiliser en filigrane.

   ***Remarque ** : n’utilisez pas de document PDF protégé par mot de passe. Si vous spécifiez un PDF protégé par mot de passe PDF comme élément de filigrane, le filigrane n’est pas appliqué.*

1. Sous Utiliser comme arrière-plan, sélectionnez Oui ou Non.

   **Remarque** : le filigrane apparaît au premier plan, quelle que soit l’option sélectionnée pour ce paramètre. 

1. Pour contrôler l’emplacement d’affichage du filigrane dans le document, configurez les options d’alignement vertical et horizontal.
1. Sélectionnez Page entière ou % et saisissez un pourcentage dans la zone. Cette valeur doit être un nombre entier, et non une fraction. Pour configurer la taille du filigrane, utilisez une valeur correspondant à un pourcentage de la page ou ajustez le filigrane au format de la page.
1. Dans le champ Rotation, indiquez le nombre de degrés de rotation du filigrane. Les valeurs autorisées vont de -180 à 180. Vous devez donc spécifier une valeur négative pour faire pivoter le filigrane dans le sens contraire des aiguilles d’une montre. Cette valeur doit être un nombre entier, et non une fraction.
1. Dans le champ Opacité, indiquez un pourcentage. Utilisez un nombre entier, pas de fraction.
1. Dans Options avancées, définissez les options suivantes :

   **Options d’étendue de page :**

   définissez l’étendue de page où le filigrane doit apparaître. Définissez la première page sur 1 et la dernière sur -1 pour que toutes les pages soient marquées dans le filigrane.

   **Options d’affichage :**

   sélectionnez l’emplacement où vous souhaitez que le filigrane apparaisse. Par défaut, le filigrane apparaît à la fois sur à l’écran (en ligne) et sur papier (impression).

1. Dans Eléments du filigrane, cliquez sur **Nouveau** pour ajouter un élément de filigrane le cas échéant.
1. Cliquez sur OK.

### Modification d’un modèle de filigrane dynamique {#edit-a-dynamic-watermark-template}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Sélectionnez le filigrane approprié dans la liste.
1. Dans la page Modifier filigranes, modifiez les paramètres.
1. Cliquez sur OK.

### Suppression d’un modèle de filigrane dynamique {#delete-a-dynamic-watermark-template}

Lorsque vous supprimez un filigrane dynamique, il n’est plus disponible et ne peut plus être ajouté à une nouvelle stratégie. Toutefois, il est conservé sur les stratégies existantes qui l’utilisent et les documents qui sont actuellement protégés par cette stratégie continuent à afficher le filigrane dynamique jusqu’à ce que vous ou un utilisateur modifiez la stratégie qui contient le filigrane supprimé. Après la modification de la stratégie, le filigrane n’est plus appliqué. Un message s’affiche alors pour signaler que le filigrane existant a été supprimé de la stratégie et qu’il est possible d’en sélectionner un autre.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Sélectionnez la case à cocher correspondant au filigrane approprié, puis cliquez sur Supprimer.
1. Cliquez sur OK.

## Configuration de l’enregistrement d’utilisateur invité {#configuring-invited-user-registration}

Les utilisateurs externes à votre entreprise peuvent s’enregistrer dans Document Security. Les utilisateurs invités qui s’enregistrent et activent leur compte peuvent ouvrir une session dans Document Security en indiquant l’adresse électronique et le mot de passe qu’ils ont créés lors de l’enregistrement. Les utilisateurs invités enregistrés peuvent utiliser les documents protégés par une stratégie pour lesquels ils disposent d’autorisations.

Lorsqu’un utilisateur invité est activé, il devient un utilisateur local. La zone Utilisateurs invités et locaux permet de configurer et de gérer les utilisateurs locaux (voir [Gestion des comptes d’utilisateurs invités et locaux](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)).

Selon les paramètres que vous activez pour les utilisateurs invités, ces derniers peuvent également utiliser les fonctionnalités Document Security suivantes :

* application de stratégies à des documents ;
* création de stratégies ;
* ajout d’utilisateurs invités à des stratégies.

Document Security génère automatiquement un courrier électronique d’invitation à l’enregistrement lorsque les événements suivants ont lieu, excepté si l’utilisateur figure déjà dans l’annuaire LDAP source ou a déjà été invité à s’enregistrer :

* un utilisateur existant ajoute un utilisateur invité à une stratégie ;
* un administrateur ajoute un compte d’utilisateur invité dans la page Enregistrement d’utilisateur invité.

Le courrier électronique d’enregistrement contient un lien permettant d’accéder à une page d’enregistrement et décrit la marche à suivre pour s’enregistrer. Une fois l’utilisateur invité enregistré, Document Security envoie un courrier électronique contenant un lien vers une page d’activation. Un compte reste activé tant que vous ne le désactivez pas ou que vous ne le supprimez pas.

L’activation de l’enregistrement intégré vous permet de ne spécifier votre serveur SMTP, les détails du courrier électronique d’enregistrement, les droits d’accès et le courrier électronique de réinitialisation du mot de passe qu’une seule et unique fois. Avant d’activer l’enregistrement intégré, vérifiez que vous avez créé un domaine local dans Gestion des utilisateurs et que le rôle Invitation d’un utilisateur de Document Security a été affecté aux utilisateurs et groupes appropriés de votre entreprise (voir [Ajout d’un domaine local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) et [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)). Si vous n’utilisez pas l’enregistrement intégré, vous devez disposer de votre propre système d’enregistrement d’utilisateurs créé à l’aide du SDK d’AEM forms. Consultez l’aide de la section « Développement d’interfaces SPI pour AEM Forms » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn-aemforms-programming-63). Si vous n’utilisez pas l’option d’enregistrement intégré, il est conseillé de configurer un message dans le courrier électronique d’activation, ainsi que dans l’écran d’ouverture de session du client, pour expliquer aux utilisateurs comment contacter l’administrateur et lui demander un nouveau mot de passe ou d’autres informations.

**Activation et configuration de l’enregistrement d’un utilisateur invité**

Par défaut, le processus d’enregistrement des utilisateurs invités est désactivé. Vous pouvez activer ou désactiver l’enregistrement des utilisateurs invités dans Document Security, à votre convenance.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Enregistrement d’utilisateur invité.
1. Sélectionnez la case à cocher Activer l’enregistrement de l’utilisateur invité.
1. (Facultatif) Mettez à jour les paramètres d’enregistrement des utilisateurs invités selon les besoins :

   * [Exclusion ou inclusion d’un utilisateur ou d’un groupe externe](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Paramètres des comptes d’enregistrement et du serveur](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Paramètres des courriers électroniques d’invitation à effectuer un enregistrement](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Paramètres des courriers électroniques d’activation](configuring-client-server-options.md#activation-email-settings)
   * [Configuration d’un courrier électronique de réinitialisation de mot de passe](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facultatif) Pour activer l’Enregistrement intégré, sélectionnez Oui. Si vous n’activez pas l’enregistrement intégré, vous devez configurer votre propre système d’enregistrement des utilisateurs.
1. Cliquez sur OK.

### Exclusion ou inclusion d’un utilisateur ou d’un groupe externe {#exclude-or-include-an-external-user-or-group}

Vous pouvez limiter la possibilité d’enregistrement dans Document Security à certains utilisateurs ou groupes d’utilisateurs externes. Cette option se révèle notamment utile si vous souhaitez autoriser l’accès à un groupe d’utilisateurs, mais exclure certains membres de ce groupe.

Les paramètres suivants se trouvent dans la zone Filtre de restriction de message électronique de la page Enregistrement d’utilisateur invité.

**Exclusion :** Tapez l&#39;adresse électronique d&#39;un utilisateur ou d&#39;un groupe à exclure. Pour exclure plusieurs utilisateurs ou groupes, saisissez chaque adresse électronique sur une nouvelle ligne. Pour exclure tous les utilisateurs appartenant à un domaine précis, saisissez un caractère générique et le nom de domaine. Par exemple, pour exclure tous les utilisateurs du domaine exemple.com, saisissez &amp;ast;.example.com.

**Inclusion :** Entrez l’adresse électronique d’un utilisateur ou d’un groupe à inclure. Pour inclure plusieurs utilisateurs ou groupes, saisissez chaque adresse électronique sur une nouvelle ligne. Pour inclure tous les utilisateurs appartenant à un domaine précis, saisissez un caractère générique et le nom de domaine. Par exemple, pour inclure tous les utilisateurs dans le domaine exemple.com, saisissez &amp;ast;.example.com.

### Paramètres des comptes d’enregistrement et du serveur {#server-and-registration-account-parameters}

Les paramètres suivants se trouvent dans la zone Paramètres généraux de la page Enregistrement d’utilisateur invité.

**Hôte SMTP :** Nom d’hôte du serveur SMTP. Le serveur SMTP gère les courriers électroniques sortants concernant l’enregistrement et l’activation des comptes d’utilisateurs invités.

Si votre hôte SMTP vous y invite, saisissez les informations requises dans les zones Nom du compte de serveur SMTP et Mot de passe du compte de serveur SMTP pour vous connecter au serveur SMTP. Certaines entreprises n’exigent pas ces informations. Pour plus d’informations, contactez votre administrateur système.

**Nom de classe de socket du serveur SMTP :** Nom de la classe de socket pour le serveur SMTP. Par exemple, javax.net.ssl.SSLSocketFactory.

**Type de contenu du courriel :** Type MIME accepté tel que text/plain ou text/html.

**Encodage du courrier électronique :** Format de codage à utiliser lors de l’envoi de messages électroniques. Vous pouvez préciser l’encodage de votre choix, par exemple UTF-8 pour Unicode ou ISO-8859-1 pour Latin. La valeur par défaut est UTF-8.

**Rediriger l&#39;adresse électronique :** Lorsque vous spécifiez une adresse électronique pour ce paramètre, toute nouvelle invitation est envoyée à l’adresse fournie. Ce paramètre peut être utile pour l’exécution de tests.

**Utiliser des domaines locaux :** Sélectionnez le domaine approprié. Dans une nouvelle installation, vérifiez que vous avez créé le domaine en utilisant User Management. S’il s’agit d’une mise à niveau, vous pouvez utiliser le domaine d’utilisateur externe créé lors de la mise à niveau.

**Utiliser SSL pour le serveur SMTP :** Sélectionnez cette option pour activer SSL pour le serveur SMTP.

**Afficher le lien de connexion sur la page d&#39;inscription :** Affiche un lien de connexion sur la page d’enregistrement affichée pour les utilisateurs invités.

**Pour activer le protocole TLS (Transport Layer Security) pour le serveur SMTP**

1. Ouvrez Administration Console.

   L’emplacement par défaut de la console d’administration est `https://<server>:<port>/adminui`.

1. Accédez à Accueil > Services > Document Security > Configuration > Enregistrement d’utilisateur invité.
1. Dans Enregistrement d’utilisateur invité, spécifiez tous les paramètres de configuration, puis cliquez sur OK.

   >[!NOTE]
   >
   >Si vous utilisez Microsoft Office 365 en tant que serveur SMTP pour envoyer les invitations à l’enregistrement des utilisateurs, utilisez les paramètres suivants :
   >
   >**Hôte SMTP :** smtp.office365.com
   >**Port :** 587

1. Vous devez ensuite mettre à jour le fichier config.xml. Voir [Configuration d’activation du protocole TLS (Transport Layer Security)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls).

>[!NOTE]
>
>si vous modifiez l’option Enregistrement d’utilisateur invité, le fichier config.xml est remplacé et le protocole TLS est désactivé. Si vous écrasez les modifications, vous devez exécuter l’étape précédente pour activer à nouveau la prise en charge du protocole TLS de l’option Enregistrement d’utilisateur invité.

### Paramètres des courriers électroniques d’invitation à effectuer un enregistrement {#registration-invitation-email-settings}

Document Security envoie automatiquement un courrier électronique d’invitation à l’enregistrement lorsque vous créez un compte d’utilisateur invité ou lorsqu’un utilisateur existant ajoute à une stratégie un destinataire externe qui n’est pas encore enregistré ou qui a été invité à s’enregistrer. Ce courrier électronique contient un lien permettant au destinataire d’accéder à la page d’enregistrement et de saisir les références de son compte, telles que son nom d’utilisateur et son mot de passe. Le mot de passe doit contenir huit caractères, quels qu’ils soient.

Lorsque le destinataire active son compte, il devient un utilisateur local.

Les paramètres suivants se trouvent dans la zone Configuration de message électronique d’invitation de la page Enregistrement d’utilisateur invité.

**De :** adresse électronique à partir de laquelle le courrier électronique d’invitation est envoyé. The default format of the From email address is postmaster@[your_installation_domain].com.

**Objet :** Objet par défaut du message électronique d’invitation.

**Délai d’expiration :** Nombre de jours après lesquels l’invitation à l’enregistrement expire si l’utilisateur externe ne s’enregistre pas. La valeur par défaut est de 30 jours.

**Message :** texte qui s’affiche dans le corps du message invitant l’utilisateur à s’enregistrer.

### Paramètres des courriers électroniques d’activation {#activation-email-settings}

Une fois les utilisateurs invités enregistrés, Document Security envoie un courrier électronique d’activation. Ce courrier contient un lien vers la page d’activation permettant aux utilisateurs d’activer leur compte. Après avoir activé leur compte, les utilisateurs peuvent ouvrir une session Document Security en spécifiant l’adresse électronique et le mot de passe qu’ils ont créés lorsqu’ils se sont enregistrés.

Lorsque le destinataire active son compte, il devient un utilisateur local.

Les paramètres suivants se trouvent dans la zone Configuration du message électronique d’activation de la page Enregistrement d’utilisateur invité.

>[!NOTE]
>
>il est également conseillé de configurer un message qui s’affiche dans l’écran d’ouverture de session pour expliquer aux utilisateurs externes comment contacter leur administrateur afin de demander un nouveau mot de passe ou d’autres informations.

**De :** Adresse électronique à partir de laquelle le courrier électronique d’activation est envoyé. Cette adresse électronique reçoit les avis de non-acheminement envoyés par l’hôte de messagerie des utilisateurs qui s’enregistrent, ainsi que les messages renvoyés par le destinataire suite au courrier électronique d’enregistrement. The default format of the From email address is postmaster@[your_installation_domain].com.

**Objet :** Objet par défaut du message électronique d’activation.

**Délai d’expiration :** Nombre de jours après lesquels l’invitation à l’activation expire si l’utilisateur n’active pas le compte. La valeur par défaut est de 30 jours.

**Message :** texte qui apparaît dans le corps du message pour indiquer que le compte utilisateur du destinataire doit être activé. Vous pouvez également inclure d’autres informations, comme la marche à suivre pour contacter un administrateur afin d’obtenir un nouveau mot de passe.

### Configuration d’un courrier électronique de réinitialisation de mot de passe {#configure-a-password-reset-email}

Si vous devez réinitialiser le mot de passe d’un utilisateur invité, un courrier électronique invitant l’utilisateur à choisir un nouveau mot de passe est généré. Il n’existe aucun moyen de récupérer le mot de passe d’un utilisateur. Si l’utilisateur l’oublie, vous devez le réinitialiser.

Les paramètres suivants se trouvent dans la zone Message électronique de réinitialisation de mot de passe de la page Enregistrement d’utilisateur invité.

**De :** adresse électronique à partir de laquelle le courrier électronique de réinitialisation de mot de passe est envoyé. The default format of the From email address is postmaster@[your_installation_domain].com.

**Objet :** Objet par défaut du message électronique de réinitialisation.

**Message :** texte qui apparaît dans le corps du message et qui indique que le mot de passe utilisateur externe du destinataire est réinitialisé.

## Capacité pour les utilisateurs et les groupes à créer des stratégies {#enable-users-and-groups-to-create-policies}

La page Configuration comprend un lien vers la page Mes stratégies, à partir de laquelle vous identifiez les utilisateurs finaux autorisés à créer des stratégies Mes stratégies, ainsi que les utilisateurs et groupes visibles dans les résultats de recherche. La page Mes stratégies comporte deux onglets :

**Onglet Créer des stratégies :** Permet de configurer les autorisations d’utilisateur pour créer des stratégies personnalisées.

**Onglet Utilisateurs et groupes visibles :** Permet de contrôler quels utilisateurs et groupes sont visibles dans les résultats de recherche des utilisateurs. Le super-utilisateur ou l’administrateur de jeux de stratégies doit sélectionner et ajouter les domaines créés dans User Management pour l’utilisateur et le groupe visible pour chacun des jeux de stratégies. Cette liste est accessible au coordinateur de jeux de stratégies et permet de restreindre les domaines que ce dernier peut consulter lorsqu’il choisit les utilisateurs à ajouter aux stratégies.

Avant d’octroyer aux utilisateurs l’autorisation de créer des stratégies personnalisées, déterminez le niveau d’accès ou de contrôle que vous souhaitez accorder à chaque utilisateur. Déterminez également le niveau d’exposition de vos utilisateurs et groupes lorsqu’ils sont visibles dans les recherches.

### Désignation des utilisateurs et groupes autorisés à créer des stratégies {#specify-users-and-groups-who-can-create-policies}

En tant qu’administrateur, vous déterminez les utilisateurs et les groupes autorisés à créer des stratégies personnalisées. Cette autorisation peut être configurée au niveau de l’utilisateur et au niveau du groupe. La fonctionnalité de recherche recherche les utilisateurs et les groupes dans la base de données User Management.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Mes stratégies.
1. Dans la page Mes stratégies, cliquez sur l’onglet Créer des stratégies, puis sur Ajouter des utilisateurs ou des groupes.
1. Dans le champ Rechercher, indiquez le nom ou l’adresse électronique de l’utilisateur ou du groupe que vous recherchez. Si vous ne connaissez pas ces informations, laissez le champ vide. Vous pouvez également saisir un nom incomplet ou une adresse électronique partielle, notamment lorsque vous ne connaissez que les deux premières lettres du nom d’un utilisateur.
1. Dans la liste Utilisation, sélectionnez les paramètres de recherche Nom ou Adresse électronique.
1. Dans la liste Type, restreignez votre recherche en sélectionnant Groupe ou Utilisateur,
1. Dans la liste Dans, sélectionnez le domaine dans lequel effectuer la recherche. Si vous ne connaissez pas le domaine de l’utilisateur ou du groupe, sélectionnez Tous les domaines.
1. Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page, puis cliquez sur Rechercher.
1. Pour ajouter des utilisateurs et des groupes dans Mes stratégies, sélectionnez la case à cocher en regard de chaque utilisateur et groupe à ajouter.
1. Cliquez sur Ajouter puis sur OK.

Les utilisateurs et groupes sélectionnés sont alors autorisés à créer des stratégies personnalisées.

### Retrait de l’autorisation à créer des stratégies personnalisées pour un utilisateur ou un groupe {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Dans la page Document Security, cliquez sur Configuration > Mes stratégies.
1. Dans la page Mes stratégies, cliquez sur l’onglet Créer des stratégies, Les utilisateurs et les groupes qui possèdent l’autorisation de créer des stratégies personnalisées sont affichés.
1. Cochez les cases correspondant aux utilisateurs et groupes pour lesquels vous souhaitez supprimer cette autorisation.
1. Cliquez sur Supprimer, puis sur OK.

### Désignation des utilisateurs et des groupes visibles dans les recherches {#specify-users-and-groups-that-are-visible-in-searches}

Pour gérer leurs stratégies personnalisées, les utilisateurs peuvent rechercher des utilisateurs et des groupes à ajouter à leurs stratégies. Vous devez spécifier les domaines à partir desquels les utilisateurs et les groupes sont visibles dans ces recherches.

1. Dans la page Document Security, cliquez sur Configuration > Mes stratégies.
1. Dans la page Mes stratégies, cliquez sur l’onglet Utilisateurs et groupes visibles,
1. Pour rendre les utilisateurs et les groupes d’un domaine visibles, cliquez sur Ajouter des domaines, sélectionnez les domaines, puis cliquez sur Ajouter. Pour supprimer un domaine, cochez la case en regard du nom de domaine, puis cliquez sur Supprimer.

## Modification manuelle du fichier de configuration de Document Security {#manually-editing-the-document-security-configuration-file}

Vous pouvez importer et exporter les informations de configuration stockées dans la base de données Document Security. Vous pouvez par exemple effectuer cette opération si vous souhaitez procéder à une copie de sauvegarde des informations de configuration lorsque vous passez d’un environnement d’installation à un environnement de production ou si vous souhaitez modifier des options avancées qui ne peuvent être configurées qu’en modifiant ce fichier.

Vous pouvez procéder aux modifications suivantes dans le fichier de configuration :

[Affichage des autorisations CATIA lors de la création et de la modification de stratégies](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Définition d’un délai d’expiration pour la synchronisation hors connexion](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Refus d&#39;accès aux services Document Security pour des applications spécifiques](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modification des paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Désactivation des liens externes](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>en important le fichier de configuration, vous reconfigurez votre système en fonction des informations contenues dans le fichier. Les exceptions à cette règle sont les informations de configuration des filigranes dynamiques et les informations d’événements personnalisés, qui ne sont pas enregistrées dans le fichier de configuration exporté. Vous devez configurer ces informations manuellement dans le nouveau système. Seul un administrateur système ou un consultant spécialiste de Document Security et du langage XML est habilité à modifier le contenu d’un fichier de configuration, notamment pour reconfigurer un paramètre corrompu ou pour affiner les paramètres d’un exemple de déploiement spécifique d’une entreprise.

**Exportation d’un fichier de configuration**

1. Dans Administration Console, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Exporter, puis enregistrez le fichier de configuration à un autre emplacement. Le nom de fichier par défaut est config.xml.
1. Cliquez sur OK.
1. Avant de modifier le fichier de configuration, effectuez une copie de sauvegarde à rétablir en cas de besoin.

**Importation d’un fichier de configuration**

1. Dans Administration Console, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Parcourir pour trouver le fichier de configuration, puis cliquez sur Importer. Vous ne pouvez pas directement saisir le chemin dans le champ Nom du fichier.
1. Cliquez sur OK.

### Définition d’un délai d’expiration pour la synchronisation hors connexion {#specify-a-timeout-period-for-offline-synchronization}

Document Security permet aux utilisateurs d’ouvrir et d’utiliser un document protégé lorsqu’ils sont connectés au serveur Document Security. L’application cliente de l’utilisateur doit régulièrement se synchroniser avec le serveur pour que les documents soient toujours valides pour une utilisation hors connexion. La première fois qu’un utilisateur ouvre un document protégé, il lui est demandé si sa machine doit être autorisée à effectuer une synchronisation périodique avec le client.

Par défaut, la synchronisation a lieu automatiquement toutes les quatre heures et en fonction des besoins lorsqu’un utilisateur est connecté au serveur Document Security. Si la période hors connexion d’un document expire pendant que l’utilisateur est hors ligne, il doit se reconnecter au serveur pour permettre à l’application cliente de se synchroniser avec le serveur.

Dans le fichier de configuration de Document Security, vous pouvez définir la fréquence par défaut de la synchronisation automatique. Ce paramètre sert de délai d’expiration par défaut pour les applications clientes, sauf si le client définit explicitement son propre délai d’expiration.

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `PolicyServer`. Sous ce nœud, recherchez le nœud `ServerSettings`.
1. Dans le nœud `ServerSettings`, ajoutez l’entrée suivante, puis enregistrez le fichier :

   `<entry key="BackgroundSyncFrequency" value="`*durée *`"/>`

   où *time* correspond au nombre de secondes entre les synchronisations automatiques en arrière-plan. Si vous définissez cette valeur sur `0`, la synchronisation a lieu en continu. The default value is `14400` seconds (every four hours).

1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Refus d’accès aux services Document Security pour des applications spécifiques {#denying-document-security-services-for-specific-applications}

Vous pouvez configurer Document Security pour que l’accès aux services soit refusé à des applications répondant à des critères précis. Les critères peuvent préciser un attribut unique, comme le nom d’une plateforme, ou plusieurs jeux d’attributs. Cette fonction peut vous aider à contrôler les demandes traitées par Document Security. Voici quelques exemples d’application de cette fonction :

* **Protection des revenus :** vous pouvez refuser l’accès à toute application cliente ne prenant pas en charge vos conventions de revenus.
* **Compatibilité des applications :** certaines applications peuvent être incompatibles avec les stratégies ou le comportement de votre serveur Document Security.

Lorsque des applications clientes tentent d’établir un lien avec Document Security, elles fournissent des informations d’application, de version et de plateforme. Document Security compare ces informations aux paramètres de refus obtenus grâce au fichier de configuration de Document Security.

Les paramètres de refus peuvent contenir plusieurs jeux de conditions de refus. Si tous les attributs d’un jeu correspondent, l’application effectuant la demande n’obtient pas l’autorisation d’accéder aux services Document Security.

La fonction de refus de service exige que les applications clientes utilisent le SDK Client C++ de Document Security, version 8.2 ou ultérieure. Les produits Adobe suivants fournissent des informations de produit dans le cadre de la demande d’accès aux services Document Security :

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard et versions ultérieures
* Adobe Reader 9.0 et versions ultérieures
* Extensions d’Acrobat Reader DC pour Microsoft Office 8.2 et versions ultérieures

Les applications clientes utilisent l’API Client du SDK Client C++ de Document Security pour demander l’accès aux services de Document Security. Les demandes de l’API Client incluent les informations de plateforme et de version du SDK (précompilation dans l’API Client) ainsi que des informations de produit obtenues par le biais de l’application cliente.

Les applications clientes ou les modules supplémentaires fournissent des informations de produit dans leur mise en œuvre d’une fonction de rappel. L’application fournit les informations suivantes :

* Nom de l’intégrateur
* Version de l’intégrateur
* Famille d’applications
* Nom de l’application
* Version de l’application

Si des informations ne sont pas applicables, l’application cliente laisse le champ correspondant vide.

Plusieurs applications Adobe fournissent des informations de produit dans le cadre de la demande d’accès aux services Document Security, notamment Acrobat, Adobe Reader et les extensions d’Acrobat Reader DC pour Microsoft Office.

**Acrobat et Acrobat Reader**

Lorsque Acrobat ou Adobe Reader demande l’accès à un service depuis Document Security, il fournit les informations de produit suivantes :

* **Intégrateur :** Adobe Systems, Inc.
* **Version de l’intégrateur :** 1.0
* **Famille de l’application :** Acrobat
* **Nom de l’application :** Acrobat
* **Version de l’application :** 9.0.0

**Extensions d’Acrobat Reader DC pour Microsoft Office**

Les extensions d’Acrobat Reader DC pour Microsoft Office sont un module supplémentaire utilisé avec les produits Microsoft Office (Microsoft Word, Microsoft Excel et Microsoft PowerPoint). Dans le cadre d’une demande d’accès à un service, les informations suivantes sont fournies :

* **Intégrateur :** Adobe Systems Incorporated
* **Version de l’intégrateur :** 8.2
* **Famille d’applications :** Extensions d’Acrobat Reader DC pour Microsoft Office
* **Nom de l’application :** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Version de l’application :** 2003 ou 2007

**Configuration de Document Security pour le refus de services à des applications spécifiques**

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
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
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` indique la version de l’API Client C++ de Document Security utilisée par l’application cliente. Par exemple, `"8.2"`.

   `APPFamilies` est défini par l’API Client.

   `AppName`indique le nom de l’application cliente. Les virgules sont utilisées pour séparer les noms. Pour inclure une virgule dans un nom, définissez une séquence de caractères d’échappement avec la barre oblique inverse (\). Par exemple : *Adobe Systems, Inc.*

   `AppVersions` indique la version de l’application cliente.

   `Integrators` indique le nom de la société ou du groupe ayant développé le module supplémentaire ou l’application intégrée.

   `IntegratorVersions` correspond à la version du module supplémentaire ou de l’application intégrée.

1. Pour chaque jeu supplémentaire de données de refus, ajoutez un autre élément *MyEntryName*.
1. Enregistrez le fichier de configuration.
1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

**Exemples**

Dans cet exemple, l’accès est refusé pour tous les clients Windows.

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

Dans cet exemple, l’accès est refusé pour My Application version 3.0 et My Other Application version 2.0. La même URL d’informations de refus est utilisée quel que soit le motif du refus.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

Dans cet exemple, toutes les requêtes émanant d’une installation Microsoft PowerPoint 2007 ou Microsoft PowerPoint 2010 des extension d’Acrobat Reader DC pour Microsoft Office sont refusées.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

### Modification des paramètres de configuration des filigranes {#change-the-watermark-configuration-parameters}

Par défaut, vous pouvez définir un maximum de cinq éléments dans un filigrane. Par ailleurs, la taille maximale des documents PDF que vous voulez utiliser en filigrane est de 100 Ko. Vous pouvez modifier ces paramètres dans le fichier config.xml.

***Remarque ** : si vous modifiez ces paramètres, faites-le avec précaution.*

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `ServerSettings`.
1. In the `ServerSettings` node, add the following entries and then save the file: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La première entrée, *taille de fichier maximale* est la taille de fichier maximale (en Ko) qui est autorisée pour un élément de filigrane en format PDF. La valeur par défaut est 100 Ko.

   La deuxième entrée, *nombre maximal d’éléments* est le nombre maximal d’éléments qui est autorisée dans un filigrane. La valeur par défaut est 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Désactivation des liens externes {#disabling-external-links}

De nombreux utilisateurs de Document Security n’ont pas accès aux liens externes, tels que **www.adobe.com**, lorsqu’ils utilisent les interfaces utilisateur de Rights Management :

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Les modifications suivantes apportées au fichier config.xml désactivent tous les liens externes des interfaces utilisateur de Rights Management.

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. To disable all external links, in the `DisplaySettings` node, add the following entry and then save the file: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Configuration d’activation du protocole TLS (Transport Layer Security). {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Les modifications suivantes apportées au fichier config.xml activent la prise en charge du protocole TLS pour la fonction Enregistrement d’utilisateur invité.

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. Locate the following node: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Définissez la valeur de la clé `SmtpUseTls` du nœud `ExternalUser` sur **true**.
1. Définissez la valeur de la clé `SmtpUseSsl` du nœud `ExternalUser` sur **false**.
1. Enregistrez le `config.xml`.
1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Désactivation des points de fin SOAP pour les documents Document Security {#disable-soap-endpoints-for-document-security-documents}

Les modifications suivantes apportées au fichier config.xml désactivent les points de fin SOAP pour les documents Document Security.

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et localisez le nœud suivant : `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. Dans le nœud DRM, recherchez le nœud `entry` :

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Pour désactiver les points de fin SOAP pour les documents Document Security, définissez l’attribut de valeur sur **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Enregistrez le `config.xml`.
1. Importez le fichier de configuration (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Évolutivité croissante du serveur Document Security {#increasingscalability}

Par défaut, lors de la synchronisation d’un document pour une utilisation en mode hors connexion, en plus des informations du document actif, les clients Document Security récupèrent des informations de mise à jour des stratégies, filigranes, licences et de révocation pour tous les autres documents auquel l’utilisateur a accès. Si ces mises à jour et informations ne sont pas synchronisées avec le client, un document ouvert en mode hors connexion peut toujours s’ouvrir avec des informations de stratégie, filigrane et révocation antérieures.

Vous pouvez accroître l’évolutivité du serveur Document Security en limitant les informations envoyées au client. La réduction du volume d’informations envoyé au client entraîne une évolutivité améliorée, un temps de réponse réduit et une meilleure performance du serveur. Effectuez les étapes suivantes pour augmenter l’évolutivité :

1. Exportez le fichier de configuration de Document Security (voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud ServerSettings.
1. Dans le nœud ServerSettings, définissez la valeur de la propriété `DisableGlobalOfflineSynchronizationData` sur `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Lorsque la valeur est définie sur true, le serveur Document Security envoie des informations uniquement pour le document actif tandis que les informations relatives aux documents restants (les autres documents auxquels un utilisateur a accès) ne sont pas envoyées au client.

   >[!NOTE]
   >
   >Par défaut, la valeur de la clé `DisableGlobalOfflineSynchronizationData` est définie sur `false`.

1. Enregistrez et importez le fichier de configuration. (voir [Modification manuelle du fichier de configuration de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

