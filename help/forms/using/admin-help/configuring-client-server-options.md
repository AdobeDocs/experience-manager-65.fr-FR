---
title: Configuration des options du client et du serveur
description: Découvrez comment configurer les différentes options du client et du serveur, telles que les paramètres de configuration du serveur, les rôles de Document Security et le contrôle des événements.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '10243'
ht-degree: 23%

---

# Configuration du serveur Document Security {#configure-the-document-security-server}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Configuration du serveur.
1. Configurez les paramètres et cliquez sur OK.

## Paramètres de configuration du serveur {#server-configuration-settings}

**URL de base :** URL de base de Document Security, contenant le nom et le port du serveur. Les informations ajoutées à cette base créent des URL de connexion. Par exemple, la séquence /edc/Main.do est ajoutée pour accéder aux pages Web. Les utilisateurs répondent également aux invitations d’enregistrement des utilisateurs externes par le biais de cette URL.

Si vous utilisez IPv6, saisissez l’URL de base comme nom d’ordinateur ou nom DNS. Si vous utilisez une adresse IP numérique, Acrobat ne parviendra pas à ouvrir les fichiers protégés par une stratégie. Utilisez également une URL HTTP sécurisée (HTTPS) pour votre serveur.

>[!NOTE]
>
>L’URL de base est incorporée dans des fichiers protégés par une stratégie. Les applications clientes utilisent l’URL de base pour se reconnecter au serveur. Les fichiers sécurisés contiendront toujours l’URL de base, même si elle est modifiée ultérieurement. Si vous modifiez l’URL de base, les informations de configuration doivent être mises à jour pour tous les clients qui se connectent.

**Période d’ouverture hors connexion par défaut :** durée par défaut pendant laquelle un utilisateur peut utiliser un document protégé hors connexion. Ce paramètre détermine la valeur de départ de la période d’ouverture hors connexion au moment de la création d’une politique (voir Création et modification de politiques). A l’issue de cette période d’ouverture, le destinataire doit resynchroniser le document pour continuer à l’utiliser.

Pour plus d’informations sur le fonctionnement de la synchronisation et de l’ouverture hors connexion, reportez-vous à la section [Primer on configuring offline lease and synchronization](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Période de synchronisation hors connexion par défaut :** durée maximale pendant laquelle un document peut être utilisé hors connexion lors de la mise en place de sa protection.

**Délai d’expiration de la session client :** durée (en minutes) à l’issue de laquelle Document Security se déconnecte si un utilisateur connecté par le biais d’une application cliente n’interagit pas avec Document Security.

**Autoriser l’accès d’utilisateurs anonymes :** sélectionnez cette option pour permettre de créer des politiques partagées et personnelles autorisant les utilisateurs anonymes à ouvrir des documents protégés par une politique. (les utilisateurs qui ne possèdent pas de compte peuvent accéder au document, mais ils ne peuvent pas ouvrir de session Document Security ni utiliser d’autres documents protégés par une politique).

**Désactiver l’accès aux clients version 7 :** indique si les utilisateurs peuvent se connecter au serveur via Acrobat ou Reader 7.0. Lorsque cette option est sélectionnée, les utilisateurs doivent utiliser Acrobat ou Reader 8.0 et versions ultérieures pour effectuer des opérations Document Security sur des documents PDF. Si les stratégies exigent qu’Acrobat ou Reader 8.0 et versions ultérieures s’exécutent en mode certifié lors de l’ouverture de documents protégés par une stratégie, désactivez l’accès à Acrobat ou au Reader 7. (voir Spécification des droits de documents pour les utilisateurs et les groupes).

**Autoriser l’accès hors connexion par document :** cette option permet de spécifier l’accès hors connexion par document. Si ce paramètre est activé, l’utilisateur aura accès en mode hors connexion uniquement aux documents qu’il a ouverts en ligne au moins une fois.

**Autoriser l’authentification du mot de passe de l’utilisateur :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat du client :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification de certificat lors de la connexion au serveur.

**Autoriser une authentification étendue :** sélectionnez cette option pour activer l’authentification étendue, puis saisissez l’URL d’accueil de l’authentification étendue.

La sélection de cette option permet aux applications clientes d’utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisés et différentes options d’authentification configurées sur le serveur d’AEM forms. Par exemple, les utilisateurs peuvent désormais tester l’authentification SAML au lieu d’AEM nom d’utilisateur/mot de passe des formulaires, à partir d’Acrobat et du client Reader. Par défaut, l&#39;URL d&#39;entrée contient *localhost* comme nom du serveur. Remplacez le nom du serveur par un nom d’hôte complet. Le nom d’hôte dans l’URL d’entrée est automatiquement renseigné à partir de l’URL de base, si l’authentification étendue n’est pas encore activée. Voir [Ajout du fournisseur d’authentification étendue](configuring-client-server-options.md#add-the-extended-authentication-provider).

***Remarque ** : l’authentification étendue est prise en charge sur Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.*

**Largeur de la commande HTML préférée pour l’authentification étendue :** indiquez la largeur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

**Hauteur de la commande HTML préférée pour l’authentification étendue :** indiquez la hauteur de la boîte de dialogue d’authentification étendue qui s’ouvre dans Acrobat pour la saisie des informations d’identification de l’utilisateur.

***Remarque ** : les limites de la largeur et la hauteur de cette boîte de dialogue sont les suivantes :*
Largeur : minimum = 400, maximum = 900

Hauteur : minimum = 450 ; maximum = 800

**Activer la mise en cache des informations d’identification du client :** sélectionnez cette option pour permettre aux utilisateurs de mettre en cache leurs informations d’identification (nom d’utilisateur et mot de passe). Lorsque les informations d’identification des utilisateurs sont mises en cache, il n’est pas nécessaire de les saisir à chaque ouverture d’un document ou lorsqu’ils cliquent sur le bouton Actualiser de la page Gérer les stratégies de sécurité dans Adobe Acrobat. Vous pouvez spécifier le nombre de jours avant que les utilisateurs ne doivent à nouveau fournir leurs informations d’identification. Si vous définissez le nombre de jours sur 0, les informations d’identification peuvent être mises en cache indéfiniment.

## Configuration des utilisateurs et des administrateurs de Document Security {#configuring-document-security-users-and-administrators}

### Attribution de rôles Document Security aux administrateurs {#assigning-document-security-roles-to-administrators}

Votre environnement d’AEM forms contient un ou plusieurs utilisateurs administrateurs disposant des privilèges appropriés pour créer des utilisateurs et des groupes. Si votre entreprise utilise Document Security, au moins un administrateur doit également disposer du droit de gestion des utilisateurs invités et locaux.

Les administrateurs doivent également disposer du rôle Utilisateur dans la console d’administration pour accéder à Administration Console. (Voir [Création et configuration des rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuration des utilisateurs et des groupes visibles {#configuring-visible-users-and-groups}

Pour afficher les utilisateurs et les groupes dans les domaines sélectionnés lors des recherches d’utilisateurs de stratégies, un super-administrateur ou un administrateur de jeux de stratégies doit sélectionner et ajouter des domaines (créés dans User Management) à la liste des utilisateurs et des groupes visibles pour chaque jeu de stratégies.

La liste des utilisateurs et des groupes visibles est visible par le coordinateur de jeux de stratégies. Elle permet de restreindre les domaines que l’utilisateur final peut parcourir lorsqu’il choisit des utilisateurs ou des groupes à ajouter aux stratégies. Si cette tâche n’est pas effectuée, le coordinateur de jeux de stratégies ne trouvera aucun utilisateur ou groupe à ajouter à la stratégie. Il peut y avoir plusieurs coordinateurs de jeux de stratégies pour un jeu donné.

1. Après avoir installé et configuré votre environnement d’AEM forms avec Document Security, configurez tous les domaines appropriés dans User Management. <!-- Fix broken link (See Setting up and managing domains) -->

   ***Remarque ** : vous devez commencer par créer les domaines avant de pouvoir créer des politiques.*

1. Dans Administration Console, cliquez sur Services > Gestion des documents > Stratégies, puis sur l’onglet Jeux de stratégies.
1. Sélectionnez Jeu de stratégies global, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter un(s) domaine(s) et ajoutez des domaines existants selon les besoins.
1. Accédez à Services > Document Security > Configuration > Mes stratégies, puis cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Cliquez sur Ajouter un(s) domaine(s) et ajoutez des domaines existants selon les besoins.

## Ajout du fournisseur d’authentification étendue {#add-the-extended-authentication-provider}

AEM forms fournit un exemple de configuration que vous pouvez personnaliser pour votre environnement. Exécutez les étapes suivantes :

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X avec Adobe Acrobat version 11.0.6 et ultérieure.

1. Procurez-vous l’exemple de fichier WAR pour le déployer. Consultez le guide d’installation approprié à votre serveur d’applications.
1. Assurez-vous que le serveur Forms dispose d’un nom complet plutôt que d’adresses IP comme URL de base et qu’il s’agit d’une URL HTTPS. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Activez l’authentification étendue à partir de la page Configuration du serveur . Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).
1. Ajoutez les URL de redirection d’authentification unique requises dans le fichier de configuration de User Management. Voir [Ajout d’URL de redirection d’authentification unique pour l’authentification étendue](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Ajout d’URL de redirection d’authentification unique pour l’authentification étendue {#add-sso-redirect-urls-for-extended-authentication}

Une fois l’authentification étendue activée, les utilisateurs qui ouvrent un document protégé par une stratégie dans Acrobat XI ou le Reader XI reçoivent une boîte de dialogue d’authentification. Cette boîte de dialogue charge la page de HTML que vous avez spécifiée comme URL d’accueil de l’authentification étendue dans les paramètres du serveur Document Security. Voir [Paramètres de configuration du serveur](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X avec Adobe Acrobat version 11.0.6 et ultérieure.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter et enregistrez le fichier de configuration sur votre disque.
1. Ouvrez le fichier dans un éditeur et recherchez le noeud AllowedUrls .
1. Dans le nœud `AllowedUrls`, ajoutez les lignes suivantes : `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Enregistrez le fichier, puis importez le fichier mis à jour à partir de la page Configuration manuelle : dans la Console d’administration, cliquez sur Paramètres > User Management > Configuration > Importer et exporter les fichiers de configuration.

## Configuration de la sécurité hors ligne {#configuring-offline-security}

Document Security permet d’utiliser hors connexion des documents protégés par une stratégie sans connexion Internet ou réseau. Cette fonctionnalité nécessite que la stratégie autorise l’accès hors ligne, comme décrit dans la section [Spécification des autorisations de document pour les utilisateurs et les groupes](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Avant qu’un document doté d’une telle stratégie puisse être utilisé hors ligne, le destinataire doit ouvrir le document en ligne et activer l’accès hors ligne, en cliquant sur Oui lorsque vous y êtes invité. Le destinataire peut également être invité à s’authentifier. Le destinataire peut alors utiliser les documents hors connexion pendant la durée de la période d’ouverture hors connexion spécifiée dans la stratégie.

A la fin de la période d’ouverture hors connexion, le destinataire doit à nouveau se synchroniser avec Document Security soit en ouvrant un document en ligne, soit en utilisant une commande de menu Acrobat ou Acrobat Reader DC extensions pour se synchroniser. (Voir *Aide d’Acrobat* ou le *Aide sur les extensions d’Acrobat Reader DC*.)

Étant donné que les documents qui autorisent un accès hors connexion nécessitent la mise en cache du matériel clé sur l’ordinateur où les fichiers sont stockés hors connexion, le fichier peut être compromis si un utilisateur non autorisé peut obtenir le matériel clé. Pour pallier ce risque, des options de roulement manuel et planifié des clés sont fournies. Vous pouvez les configurer pour empêcher une personne non autorisée d’utiliser la clé pour accéder au document.

### Définir une période d’ouverture hors connexion par défaut {#set-a-default-offline-lease-period}

Les destinataires des documents protégés par une stratégie peuvent les mettre hors ligne pendant le nombre de jours spécifié dans la stratégie. Après la synchronisation initiale du document avec Document Security, le destinataire peut l’utiliser hors connexion jusqu’à l’expiration de la période d’ouverture hors connexion. Lorsque la période d’ouverture expire, le destinataire doit mettre le document en ligne et se connecter pour se synchroniser avec Document Security afin de continuer à l’utiliser.

Vous pouvez configurer une période d’ouverture hors connexion par défaut. La période d’ouverture peut être modifiée à partir de la valeur par défaut lorsque quelqu’un crée ou modifie une stratégie.

1. Dans la page Document Security, cliquez sur Configuration > Configuration du serveur.
1. Dans la zone Période d’ouverture hors connexion par défaut, indiquez le nombre de jours pendant la période d’ouverture hors connexion.
1. Cliquez sur OK.

### Gestion des roulements de clés {#manage-key-rollovers}

Document Security utilise des algorithmes de chiffrement et des licences pour protéger les documents. Lorsqu’il chiffre un document, Document Security génère et gère une clé de déchiffrement appelée *DocKey* qu’il transmet à l’application cliente. Si la stratégie qui protège un document autorise l’accès hors connexion, une clé hors connexion appelée *clé principale* est également généré pour chaque utilisateur disposant d’un accès hors ligne au document.

>[!NOTE]
>
>Si aucune clé principale n’existe, Document Security en génère une pour protéger un document.

Pour ouvrir hors connexion un document protégé par une stratégie, l’ordinateur de l’utilisateur doit disposer de la clé principale appropriée. L’ordinateur obtient la clé principale lorsque l’utilisateur se synchronise avec Document Security (ouvre un document protégé en ligne). Si cette clé principale est compromise, tout document auquel l’utilisateur a un accès hors ligne peut également être compromis.

L’une des manières de réduire la menace envers les documents hors ligne consiste à éviter d’autoriser l’accès hors ligne à des documents particulièrement sensibles. Une autre méthode consiste à rouler périodiquement sur les clés principales. Lorsque Document Security place la clé au-dessus, les clés existantes ne peuvent plus accéder aux documents protégés par une stratégie. Par exemple, si un auteur obtient une clé principale à partir d’un ordinateur portable volé, cette clé ne peut pas être utilisée pour accéder aux documents protégés après le survol. Si vous pensez qu’une clé principale spécifique a été compromise, vous pouvez la survoler manuellement.

Cependant, vous devez également savoir qu’un roulement de clés affecte toutes les clés principales, et non une seule. Cela réduit également l’évolutivité du système, car les clients doivent stocker plus de clés pour l’accès hors ligne. La fréquence de roulement des clés par défaut est de 20 jours. Il est recommandé de ne pas définir cette valeur sur 14 jours, car les personnes peuvent ne pas pouvoir afficher les documents hors ligne et les performances du système peuvent être affectées.

Dans l’exemple suivant, Clé1 est la plus ancienne des deux clés principales et Clé2 la plus récente. Lorsque vous cliquez pour la première fois sur le bouton Exécuter le roulement des clés maintenant , Clé1 n’est plus valide et une clé principale plus récente et valide (Clé3) est générée. Les utilisateurs obtiendront Key3 lorsqu’ils se synchronisent avec Document Security, généralement en ouvrant un document protégé en ligne. Toutefois, les utilisateurs ne sont pas obligés de se synchroniser avec Document Security tant qu’ils n’ont pas atteint la période d’ouverture hors connexion maximale spécifiée dans une stratégie. Après le premier roulement de clés, les utilisateurs qui restent hors ligne peuvent toujours ouvrir des documents hors ligne, y compris ceux protégés par Clé3, jusqu’à ce qu’ils atteignent la période d’ouverture hors ligne maximale. Lorsque vous cliquez une seconde fois sur le bouton Exécuter le roulement des clés maintenant , Clé2 n’est plus valide et Clé4 est créée. Les utilisateurs qui restent hors ligne pendant les deux roulements de clés ne peuvent pas ouvrir les documents protégés par Clé3 ou Clé4 tant qu’ils ne se synchronisent pas avec Document Security.

**Modification de la fréquence de roulement des clés**

À des fins de confidentialité, lorsque vous utilisez des documents hors ligne, Document Security propose une option de roulement automatique des clés avec une fréquence par défaut de 20 jours. Vous pouvez modifier la fréquence de roulement. Toutefois, évitez de définir une valeur inférieure à 14 jours, car les personnes peuvent ne pas pouvoir afficher les documents hors ligne et les performances du système peuvent être affectées.

1. Dans la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Dans le champ Fréquence de roulement des clés, indiquez le nombre de jours pendant la période de roulement.
1. Cliquez sur OK.

**Roulement manuel des clés principales**

Pour préserver la confidentialité des documents hors ligne, vous pouvez effectuer un roulement manuel des clés principales. Il peut s’avérer nécessaire de rouler manuellement une clé (par exemple, si elle est compromise par une personne qui l’obtient à partir d’un ordinateur sur lequel elle est mise en cache pour activer l’accès hors ligne à un document).

>[!NOTE]
>
>Évitez d’utiliser fréquemment le roulement manuel, car il entraîne le roulement de toutes les clés principales, et non d’une seule, et peut temporairement empêcher les utilisateurs d’afficher les nouveaux documents hors ligne.

Les clés principales doivent être roulées deux fois avant que les clés existantes sur les ordinateurs clients ne soient invalidées. Les ordinateurs clients qui ont invalidé les clés principales doivent se resynchroniser avec le service Document Security pour acquérir les nouvelles clés principales.

1. Dans la page Document Security, cliquez sur Configuration > Gestion des clés.
1. Cliquez sur Exécuter le roulement des clés maintenant, puis sur OK.
1. Attends environ 10 minutes. Le message suivant s’affiche dans le fichier-journal du serveur : `Done RightsManagement key rollover for`*N* `principals`. Où *N* est le nombre d’utilisateurs dans le système Document Security.
1. Cliquez sur Exécuter le roulement des clés maintenant, puis sur OK.
1. Attends environ 10 minutes.

## Configuration des paramètres de contrôle et de confidentialité des événements {#configuring-event-auditing-and-privacy-settings}

Document Security peut contrôler et enregistrer des informations sur les événements liés à l’interaction avec des documents protégés par une stratégie, des stratégies, des administrateurs et le serveur. Vous pouvez configurer le contrôle des événements et spécifier les types d’événements à contrôler. Pour contrôler les événements d’un document particulier, l’option de contrôle de la stratégie doit également être activée.

Lorsque le contrôle est activé, vous pouvez afficher les détails des événements contrôlés sur la page Événements . les utilisateurs de Document Security peuvent également afficher les événements relatifs aux documents protégés par une stratégie qu’ils utilisent ou créent.

Vous pouvez sélectionner les types d’événements suivants pour le contrôle :

* Événements de document protégés par une stratégie, tels que les tentatives d’ouverture de documents par des utilisateurs autorisés ou non
* événements de stratégie, tels que la création, la modification, la suppression, l’activation et la désactivation de stratégies
* Événements d’utilisateur, tels que les invitations et enregistrements d’utilisateurs externes, les comptes d’utilisateurs activés et désactivés, les modifications des mots de passe utilisateur et les mises à jour de profil
* AEM événements de formulaires, tels que les versions incohérentes, le serveur d’annuaire et les fournisseurs d’autorisations indisponibles, ainsi que les modifications de configuration du serveur

### Activation ou désactivation du contrôle des événements {#enable-or-disable-event-auditing}

Vous pouvez activer et désactiver le contrôle des événements liés au serveur, aux documents protégés par une stratégie, aux stratégies, aux jeux de stratégies et aux utilisateurs. Lorsque vous activez le contrôle des événements, vous pouvez choisir de contrôler tous les événements possibles ou sélectionner des événements spécifiques à contrôler.

Lorsque vous activez le contrôle du serveur, vous pouvez afficher les événements contrôlés sur la page Événements .

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le contrôle du serveur, sélectionnez Oui ou Non sous Activer le contrôle du serveur.
1. Si vous avez sélectionné Oui, effectuez l’une des opérations suivantes sous chaque catégorie d’événement pour sélectionner les options à contrôler :

   * Pour contrôler tous les événements de la catégorie, sélectionnez Tous.
   * Pour contrôler certains événements uniquement, désélectionnez Tous, puis cochez les cases en regard des événements à contrôler.

     (Voir [Options de contrôle des événements](configuring-client-server-options.md#event-auditing-options).)

1. Cliquez sur OK.

>[!NOTE]
>
>Lorsque vous travaillez sur des pages web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que la flèche Précédent ou Précédent, car cette action peut entraîner des problèmes de capture de données et d’affichage de données indésirables.

### Activation ou désactivation de la notification de confidentialité {#enable-or-disable-privacy-notification}

Vous pouvez activer et désactiver un message de notification de confidentialité. Lorsque vous activez la notification de confidentialité, un message s’affiche lorsqu’un destinataire tente d’ouvrir un document protégé par une stratégie. L’avis informe l’utilisateur que l’utilisation du document fait l’objet d’un contrôle. Vous pouvez également spécifier une URL que l’utilisateur peut utiliser pour afficher votre page de politique de confidentialité, le cas échéant.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer la notification de confidentialité, sélectionnez Oui ou Non sous Activer la notification de confidentialité.

   Si la stratégie associée à un document autorise l’accès anonyme des utilisateurs et que l’option Activer la notification de confidentialité est définie sur Non, l’utilisateur n’est pas invité à se connecter et le message de notification de confidentialité n’est pas affiché.

   Si la stratégie associée à un document n’autorise pas l’accès anonyme, l’utilisateur voit le message de notification de confidentialité.

1. Le cas échéant, dans la zone URL de confidentialité, saisissez l’URL vers la page de votre politique de confidentialité. Si la zone URL de confidentialité n’est pas renseignée, la page de confidentialité de adobe.com s’affiche.
1. Cliquez sur OK.

>[!NOTE]
>
>La désactivation de la notification de confidentialité ne désactive pas le contrôle de l’utilisation du document. Les actions d’audit prêtes à l’emploi et les actions personnalisées prises en charge par le suivi de l’utilisation étendue peuvent toujours collecter des informations sur le comportement des utilisateurs.

### Importation d’un type d’événement de contrôle personnalisé {#import-a-custom-audit-event-type}

Si vous utilisez une application compatible Document Security qui prend en charge le contrôle d’événements supplémentaires, tels que des événements spécifiques à un certain type de fichier, un partenaire d’Adobe peut vous fournir des événements de contrôle personnalisés que vous pouvez importer dans Document Security. Utilisez cette fonction uniquement si un partenaire d’Adobe vous a fourni des types d’événement personnalisés.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Cliquez sur Parcourir pour accéder au fichier XML à importer, puis sur Importer.
1. L’importation remplace les types d’événements de contrôle personnalisés existants sur le serveur si des combinaisons de code d’événement et d’espace de noms identiques sont trouvées.
1. Cliquez sur OK.

### Suppression d’un type d’événement de contrôle personnalisé {#delete-a-custom-audit-event-type}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Cochez la case en regard du type d’événement de contrôle personnalisé à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK.

### Exportation des événements de contrôle {#export-audit-events}

Vous pouvez exporter des événements de contrôle vers un fichier à des fins d’archivage.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Modifiez les paramètres sous Exporter les événements de contrôle selon les besoins. Vous pouvez préciser :

   * âge minimum des événements de contrôle à exporter
   * le nombre maximal d’événements de contrôle à inclure dans un seul fichier. Le serveur génère un ou plusieurs fichiers en fonction de cette valeur.
   * dossier dans lequel le fichier sera créé. Ce dossier se trouve sur le serveur Forms. Si le chemin du dossier est relatif, il est relatif au répertoire racine du serveur d’applications.
   * le préfixe de fichier à utiliser pour les fichiers d’événements de contrôle ;
   * le format du fichier, soit un fichier CSV (valeurs séparées par des virgules) compatible avec Microsoft Excel, soit un fichier XML.

1. Cliquez sur Exporter. Si vous souhaitez annuler l’exportation, cliquez sur Annuler l’exportation. Si un autre utilisateur a planifié une exportation, le bouton Annuler l’exportation n’est pas disponible tant que l’exportation n’est pas terminée. Le bouton Annuler l’exportation n’est pas disponible si un autre utilisateur a planifié une exportation. Pour vérifier si une exportation ou une suppression planifiée a commencé ou s’est terminée, cliquez sur Actualiser.

### Suppression d’événements de contrôle {#delete-audit-events}

Vous pouvez supprimer les événements de contrôle dont la date est antérieure à un nombre spécifié de jours.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Gestion des événements.
1. Sous Supprimer les événements de contrôle, indiquez le nombre de jours dans la zone Supprimer les événements de contrôle antérieurs à .
1. Cliquez sur Supprimer. Cliquez sur Exporter. Si vous souhaitez annuler la suppression, cliquez sur Annuler la suppression. Si un autre utilisateur a planifié une suppression, le bouton Annuler la suppression n’est pas disponible tant que l’exportation n’est pas terminée. Le bouton Annuler la suppression n’est pas disponible si un autre utilisateur a planifié une exportation. Pour vérifier si une suppression planifiée a commencé ou s’est terminée, cliquez sur Actualiser.

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

**Utilisateur supprimé :** un administrateur supprime un compte utilisateur.

**Enregistrer un utilisateur invité :** un utilisateur externe s’enregistre auprès de la Sécurité des documents.

**Ouverture de session réussie :** tentatives d’ouverture de session réussies par des administrateurs ou des utilisateurs. 

**Utilisateurs invités :** la Sécurité des documents invite un utilisateur à s’enregistrer.

**Utilisateurs activés :** des utilisateurs externes activent leur compte à l’aide de l’URL mentionnée dans le courrier électronique d’activation ou un administrateur active un compte.

**Modifier le mot de passe :** des utilisateurs invités changent leur mot de passe ou un administrateur réinitialise le mot de passe d’un utilisateur local.

**Echec de l’ouverture de session :** échec des tentatives d’ouverture de session par des administrateurs ou des utilisateurs.

**Utilisateurs désactivés :** un administrateur supprime un compte utilisateur local.

**Mise à jour du profil :** des utilisateurs invités modifient leur nom, le nom de leur entreprise et leur mot de passe.

**Compte verrouillé :** Un administrateur verrouille un compte.

**Evénements de jeu de politique**

**Jeu 

de politiques créé :** un administrateur ou un coordinateur de jeux de politiques crée un jeu de politiques.

**Jeu de politiques supprimé :** un administrateur ou un coordinateur de jeux de politiques supprime un jeu de politiques.

**Jeu de politiques modifié :** un administrateur ou un coordinateur de jeux de politiques modifie un jeu de politiques.

**Evénements de système**

**Synchronisation 
des annuaires terminée :** ces informations ne sont pas disponibles à partir de la page Événements. Les informations actuelles sur la synchronisation des annuaires, notamment l’état actuel de la synchronisation et l’heure de la dernière synchronisation, s’affichent sur la page Gestion des domaines. Pour accéder à la page Gestion des domaines dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.

**Client Activez l’accès hors ligne :** Un utilisateur a activé l’accès hors ligne aux documents sécurisés sur le serveur sur l’ordinateur de l’utilisateur.

**Client synchronisé** : l’application cliente doit synchroniser les informations avec le serveur pour autoriser l’accès hors connexion.

**Version incohérente :** une version du SDK d’AEM forms incompatible avec le serveur a tenté de se connecter à ce dernier.

**Informations sur la synchronisation des annuaires :** ces informations ne sont pas disponibles à partir de la page Événements. Les informations actuelles sur la synchronisation des annuaires, notamment l’état actuel de la synchronisation et l’heure de la dernière synchronisation, s’affichent sur la page Gestion des domaines. Pour accéder à la page Gestion des domaines dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.

**Modification de la configuration du serveur :** modifications apportées à la configuration du serveur soit par l’intermédiaire des pages Web soit par importation manuelle d’un fichier config.xml. Cela inclut les modifications apportées à l’URL de base, aux délais d’expiration de session, aux verrouillages de connexion, aux paramètres d’annuaire, aux roulements de clés, aux paramètres du serveur SMTP pour l’enregistrement externe, à la configuration des filigranes, aux options d’affichage, etc.

## Configuration du suivi des utilisations étendues {#configuring-extended-usage-tracking}

Document Security peut effectuer le suivi de divers événements personnalisés pouvant être effectués sur un document protégé. Vous pouvez activer le suivi des événements à partir du serveur Document Security au niveau global ou au niveau des stratégies. Vous pouvez ensuite configurer un script JavaScript pour capturer les actions spécifiques effectuées dans le document de PDF protégé, comme cliquer sur un bouton ou enregistrer le document. Ces données d’utilisation sont envoyées sous forme de fichier XML dans des paires clé-valeur, que vous pouvez utiliser pour une analyse plus approfondie. Les utilisateurs finaux qui accèdent aux documents protégés peuvent autoriser ou refuser ce suivi à partir de l’application cliente.

Si le suivi est activé au niveau global, vous pouvez remplacer ce paramètre au niveau de la stratégie et le désactiver pour une stratégie spécifique. Le remplacement au niveau de la stratégie n’est pas possible si le suivi est désactivé au niveau global. La liste des événements suivis est automatiquement envoyée au serveur lorsque le nombre d’événements atteint 25 ou lorsque le document est fermé. Vous pouvez également configurer votre script pour envoyer explicitement la liste d’événements selon vos besoins. Vous pouvez personnaliser le suivi des événements en accédant aux propriétés et aux méthodes de l’objet Document Security.

Une fois le suivi activé, le suivi est activé par défaut pour toutes les stratégies créées ultérieurement. Les stratégies créées avant l’activation du suivi sur le serveur devront être mises à jour manuellement.

### Activation ou désactivation du suivi des utilisations étendues {#enable-or-disable-extended-usage-tracking}

Avant de commencer, assurez-vous que le contrôle du serveur est activé. Voir [Configuration des paramètres de contrôle et de confidentialité des événements](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) pour plus d’informations sur le contrôle.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Paramètres de contrôle et de confidentialité.
1. Pour configurer le suivi des utilisations étendues, sous Activer le suivi, sélectionnez Oui ou Non.
1. Pour définir la sélection de la case à cocher Autoriser la collecte de données d’utilisation détaillées sur la page de connexion, sous Activer le suivi par défaut, sélectionnez Oui ou Non.

Pour afficher les événements suivis, vous pouvez utiliser le filtre Evénements de document sur la page Événements . Les événements suivis à l’aide de JavaScript sont étiquetés comme Suivi détaillé de l’utilisation. Voir [Surveillance des événements](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) pour plus d’informations sur les événements.

## Configuration des paramètres d’affichage de Document Security {#configure-document-security-display-settings}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Options d’affichage.
1. Configurez les paramètres et cliquez sur OK.

### Paramètres d’affichage {#display-settings}

**Lignes à afficher pour les résultats de la recherche :** nombre de lignes qui apparaissent sur une page lors des recherches.

**Personnalisation de la boîte de dialogue de connexion client**

Ces paramètres contrôlent le texte affiché dans l’invite de connexion qui s’affiche lorsqu’un utilisateur se connecte à Document Security via une application cliente.

**Texte de bienvenue :** texte du message de bienvenue, par exemple « Veuillez vous connecter à l’aide de votre nom d’utilisateur et de votre mot de passe. ». Le texte du message de bienvenue doit contenir des informations sur la connexion à Document Security et sur la manière de contacter un administrateur ou une autre personne désignée du service d’assistance pour obtenir de l’aide. Par exemple, des utilisateurs externes peuvent avoir besoin de contacter un administrateur s’ils oublient leurs mots de passe ou s’ils ont besoin d’aide pour l’enregistrement ou le processus de connexion. La longueur maximale du texte de bienvenue est de 512 caractères.

**Texte du nom d’utilisateur :** libellé de texte de la zone de nom d’utilisateur.

**Texte du mot de passe :** libellé de texte de la zone du mot de passe.

**Personnalisation de la boîte de dialogue d’authentification de certificat client**

Ces paramètres contrôlent le texte affiché dans la boîte de dialogue d’authentification de certificat.

**Choisir 
le texte du type d’authentification :** texte affiché pour demander à un utilisateur de sélectionner un type d’authentification.

**Choisir le texte de certificat :** texte affiché pour demander à un utilisateur de sélectionner un type de certificat.

**Texte d’erreur Certificats non disponibles :** message de 512 caractères maximum à afficher lorsque le certificat sélectionné n’est pas disponible.

**Personnalisation de l’affichage du certificat client**

**Afficher uniquement les informations d’identification de confiance :** lorsque cette option est sélectionnée, l’application cliente ne présente à l’utilisateur que les certificats des émetteurs d’informations d’identification de confiance pour lesquels AEM Forms est configuré (voir Gérer des certificats et des informations d’identification). Lorsque cette option n’est pas sélectionnée, la liste de tous les certificats figurant sur le système de l’utilisateur s’affiche pour l’utilisateur.

## Configuration des filigranes dynamiques {#configure-dynamic-watermarks}

Document Security vous permet de configurer les paramètres par défaut de l’option de filigrane dynamique que vous pouvez appliquer lors de la création de stratégies. A *filigrane* est une image superposée au texte du document. Il est utile pour le suivi du contenu d’un document et peut aider à identifier l’utilisation illégale du contenu.

Un filigrane dynamique peut être constitué de texte constitué de variables définies, telles que l’ID utilisateur et la date et le texte personnalisé, ou de contenu enrichi dans un PDF. Vous pouvez configurer des filigranes avec plusieurs éléments, chacun ayant son propre positionnement et formatage.

Les filigranes ne sont pas modifiables et constituent donc une méthode plus sécurisée pour garantir la confidentialité du contenu du document. Les filigranes dynamiques garantissent également qu’un filigrane affiche suffisamment d’informations spécifiques à l’utilisateur pour empêcher toute diffusion ultérieure du document.

Le filigrane spécifié par une stratégie apparaît dans le document protégé par une stratégie lorsqu’un destinataire affiche ou imprime le document. Contrairement aux filigranes permanents, un filigrane dynamique n’est jamais enregistré dans le document, ce qui offre la flexibilité nécessaire lors du déploiement d’un document dans un environnement intranet pour s’assurer que l’application d’affichage affiche l’identité de l’utilisateur spécifique. En outre, si un document comporte plusieurs utilisateurs, l’utilisation du filigrane dynamique signifie que vous pouvez utiliser un document au lieu de plusieurs versions, chacune avec un filigrane différent. Le filigrane qui s’affiche indique l’identité de l’utilisateur actuel.

Notez que les filigranes dynamiques sont différents des filigranes que les utilisateurs peuvent ajouter directement au document dans Acrobat. Par conséquent, vous pouvez avoir deux filigranes dans un document protégé par une stratégie.

### Remarques concernant la création de filigranes {#considerations-when-creating-watermarks}

Vous pouvez créer des filigranes dynamiques avec plusieurs éléments de filigrane, chacun étant défini comme texte ou PDF. Vous pouvez inclure jusqu’à cinq éléments dans un filigrane.

Si vous choisissez un filigrane textuel, vous pouvez spécifier plusieurs éléments dans le filigrane avec plusieurs entrées de texte et spécifier la position de chaque élément. Attribuez des noms significatifs à ces éléments, tels que l’en-tête, le pied de page, etc.

Par exemple, si vous souhaitez spécifier un texte différent dans l’en-tête, le pied de page, dans les marges et dans le document en tant que filigrane, créez plusieurs éléments de filigrane et indiquez leur position. Si vous souhaitez que l’identifiant utilisateur et la date actuelle d’accès au document s’affichent dans l’en-tête, que le nom de la politique soit indiqué dans la marge de droite et qu’un texte personnalisé indiquant « CONFIDENTIEL » apparaissent en diagonale sur le document, définissez des éléments de filigrane différents de type texte et précisez leur formatage et leur emplacement. Lorsque le filigrane est appliqué à un document, tous les éléments du filigrane sont appliqués simultanément au document, dans l’ordre dans lequel ils sont ajoutés au filigrane.

En règle générale, vous utilisez des filigranes basés sur un PDF pour inclure des contenus graphiques tels que des logos ou des symboles spéciaux tels que les droits d’auteur ou les marques enregistrées.

Vous pouvez modifier les limites du nombre d’éléments de filigrane et la taille de fichier du PDF en modifiant le fichier de configuration de Document Security. Voir [Modification des paramètres de configuration du filigrane](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Lorsque vous configurez des filigranes, tenez compte des points suivants :

* Vous ne pouvez pas utiliser un document de PDF protégé par mot de passe comme élément de filigrane. Cependant, si le filigrane que vous créez contient d’autres éléments qui ne sont pas protégés par mot de passe, ils seront appliqués dans le cadre du filigrane.
* Vous pouvez modifier la taille maximale du fichier de PDF que vous souhaitez utiliser comme élément de filigrane. Cependant, les documents PDF volumineux utilisés comme filigranes dégradent les performances lors de la synchronisation hors ligne des documents appliqués avec ces filigranes. Voir [Modification des paramètres de configuration du filigrane](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Seule la première page du PDF sélectionné est utilisée comme filigrane. Assurez-vous que les informations que vous souhaitez afficher en tant que filigrane sont disponibles sur la première page elle-même.
* Bien que vous puissiez spécifier la mise à l’échelle du document du PDF, tenez compte de la taille et de la mise en page du PDF si vous prévoyez de l’utiliser comme filigrane dans l’en-tête, le pied de page ou les marges.
* Lorsque vous spécifiez le nom de la police, saisissez le nom correctement. AEM forms remplace la police que vous avez spécifiée si elle n’est pas présente sur l’ordinateur client sur lequel le document est ouvert.
* Si vous avez sélectionné le texte comme filigrane, la définition de l’option de mise à l’échelle sur Page entière ne fonctionne pas pour les pages dont la largeur est différente.
* Lorsque vous définissez le positionnement des éléments du filigrane, assurez-vous qu’aucun élément n’a le même positionnement. Si deux éléments de filigrane ont le même emplacement, tels que le centre, ils apparaissent recouverts sur le document et dans l’ordre dans lequel ils ont été ajoutés au filigrane.
* Lors de la spécification de la taille et du type de police, assurez-vous que la longueur du texte est entièrement visible dans la page. Le contenu textuel s’étend sur de nouvelles lignes, de sorte que le contenu du filigrane que vous souhaitez voir apparaître dans les marges peut se chevaucher dans les zones de contenu des pages. Cependant, si le document est ouvert dans Acrobat 9, le texte au-delà de la ligne unique est tronqué.

### Limites des filigranes dynamiques {#limitations-of-dynamic-watermarks}

Certaines applications clientes peuvent ne pas prendre en charge les filigranes dynamiques. Voir l’aide des extensions d’Acrobat Reader DC appropriée. En outre, gardez à l’esprit les points suivants concernant les versions d’Acrobat qui prennent en charge les filigranes dynamiques :

* Vous ne pouvez pas utiliser un document de PDF protégé par mot de passe comme élément de filigrane.
* Les versions d’Acrobat et d’Adobe Reader antérieures à la version 10 ne prennent pas en charge les fonctionnalités de filigrane suivantes :

   * filigranes PDF
   * Plusieurs éléments dans le filigrane (texte/PDF)
   * Options avancées telles que la plage de pages ou les options d’affichage
   * Options de mise en forme du texte, telles que la police, le nom et la couleur spécifiés. Toutefois, les versions antérieures d’Acrobat et de Reader affichent le contenu du texte dans la police et la couleur par défaut.

* Acrobat 9.0 et versions antérieures : Acrobat 9.0 et versions antérieures ne prennent pas en charge les noms de stratégie dans les filigranes dynamiques. Si Acrobat 9.0 ouvre un document protégé par une stratégie avec un filigrane dynamique qui comprend un nom de stratégie et d’autres données dynamiques, le filigrane s’affiche sans le nom de la stratégie. Si le filigrane dynamique ne contient que le nom de la stratégie, Acrobat affiche un message d’erreur.

### Ajout d’un modèle de filigrane dynamique {#add-a-dynamic-watermark-template}

Vous pouvez créer des modèles de filigrane dynamiques. Ces modèles restent disponibles en tant qu’option de configuration pour les stratégies créées par les administrateurs ou les utilisateurs.

>[!NOTE]
>
>Les informations de configuration des filigranes dynamiques ne sont pas capturées avec les autres informations de configuration lors de l’exportation d’un fichier de configuration.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cliquez sur Nouveau.
1. Dans la zone Nom, saisissez le nom du nouveau filigrane.

   ***Remarque ** : certains caractères spéciaux ne peuvent être utilisés dans le nom ou la description des filigranes ou des éléments de filigrane. Voir les restrictions répertoriées dans la section [Considérations relatives à la modification de stratégies](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Sous Nom, en regard du signe plus, saisissez un nom significatif pour l’élément de filigrane, tel que En-tête, ajoutez une description, puis développez le signe plus pour afficher les options.
1. Sous Source, sélectionnez le type de filigrane Texte ou PDF.
1. Si vous avez sélectionné Texte, procédez comme suit :

   * Sélectionnez les types de filigrane à inclure. Si vous sélectionnez Texte personnalisé, saisissez le texte à afficher pour le filigrane dans la zone adjacente. Gardez à l’esprit la longueur du texte qui apparaîtra en filigrane.
   * Spécifiez les propriétés de mise en forme du texte, telles que le nom de la police, la taille de la police, la couleur de premier plan et la couleur d’arrière-plan pour le contenu du texte du filigrane. Spécifiez les couleurs de premier plan et d’arrière-plan en tant que valeurs hexadécimales.

     ***Remarque ** : si vous définissez le cadrage sur Page entière, vous ne pouvez pas modifier la taille de la police.*

1. Si vous sélectionnez le format PDF pour les options de filigrane riches, cliquez sur **Parcourir**, à côté de Sélectionner le PDF du filigrane, pour sélectionner le document PDF que vous voulez utiliser en filigrane.

   ***Remarque ** : n’utilisez pas de document PDF protégé par mot de passe. Si vous spécifiez un PDF protégé par mot de passe comme élément de filigrane, le filigrane n’est pas appliqué.*

1. Sous Utiliser comme arrière-plan, sélectionnez Oui ou Non.

   **Remarque** : le filigrane apparaît au premier plan, quelle que soit l’option sélectionnée pour ce paramètre. 

1. Pour contrôler l’emplacement d’affichage du filigrane dans le document, configurez les options Alignement vertical et Alignement horizontal .
1. Sélectionnez Ajuster à la page ou % et saisissez un pourcentage dans la zone. La valeur doit être un nombre entier, pas une fraction. Pour configurer la taille du filigrane, vous pouvez utiliser une valeur qui correspond au pourcentage de la page ou définir le filigrane en fonction de la taille de la page.
1. Dans la zone Rotation, saisissez les degrés de rotation du filigrane. La plage est comprise entre -180 et 180. Utilisez une valeur négative pour faire pivoter le filigrane dans le sens inverse des aiguilles d’une montre. La valeur doit être un nombre entier, pas une fraction.
1. Dans la zone Opacité, saisissez un pourcentage. Utilisez un nombre entier, pas une fraction.
1. Sous Options avancées, définissez les options suivantes :

   **Options d’étendue de page**

   Définissez la plage de pages où le filigrane doit s’afficher. Définissez la page de début sur 1 et la page de fin sur -1 pour que toutes les pages soient marquées avec le filigrane.

   **Options d’affichage**

   Sélectionnez l’emplacement où doit apparaître le filigrane. Par défaut, le filigrane apparaît à la fois sur la copie (en ligne) et sur la copie (papier).

1. Cliquez sur **Nouveau** sous Eléments de filigrane pour ajouter d’autres éléments de filigrane si nécessaire.
1. Cliquez sur OK.

### Modification d’un modèle de filigrane dynamique {#edit-a-dynamic-watermark-template}

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cliquez sur le filigrane approprié dans la liste.
1. Sur la page Modifier les filigranes , modifiez les paramètres selon les besoins.
1. Cliquez sur OK.

### Suppression d’un modèle de filigrane dynamique {#delete-a-dynamic-watermark-template}

Lorsque vous supprimez un filigrane dynamique, il ne peut plus être ajouté à une nouvelle stratégie. Cependant, le filigrane reste sur les stratégies existantes qui l’utilisent et les documents actuellement protégés par la stratégie continuent à afficher le filigrane dynamique jusqu’à ce que vous ou un utilisateur modifiez la stratégie qui contient le filigrane supprimé. Une fois la stratégie modifiée, le filigrane n’est plus appliqué. Un message s’affiche, indiquant que le filigrane existant est supprimé dans la stratégie et que l’utilisateur peut en sélectionner un autre pour le remplacer.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Filigranes.
1. Cochez la case en regard du filigrane approprié, puis cliquez sur Supprimer.
1. Cliquez sur OK.

## Configuration de l’enregistrement d’utilisateur invité {#configuring-invited-user-registration}

Les utilisateurs externes à votre entreprise peuvent s’enregistrer auprès de Document Security. Les utilisateurs invités qui s’enregistrent et activent leur compte peuvent se connecter à Document Security à l’aide de leur adresse électronique et du mot de passe qu’ils créent lors de leur enregistrement. Les utilisateurs invités enregistrés peuvent utiliser des documents protégés par une stratégie pour lesquels ils disposent d’autorisations.

Lorsque les utilisateurs invités sont activés, ils deviennent des utilisateurs locaux. Les utilisateurs locaux peuvent être configurés et gérés à l’aide des zones Utilisateurs invités et locaux . (Voir [Gestion des comptes d’utilisateurs invités et locaux](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

Selon les fonctionnalités que vous activez pour les utilisateurs invités, ils peuvent également utiliser les fonctionnalités de Document Security suivantes :

* Application de stratégies à des documents
* Créer des politiques
* Ajout d’utilisateurs invités à des stratégies

Document Security génère automatiquement un courrier électronique d’invitation à l’enregistrement lorsque les événements suivants se produisent, sauf si l’utilisateur figure déjà dans l’annuaire LDAP source ou a déjà été invité à s’enregistrer :

* un utilisateur existant ajoute un utilisateur invité à une stratégie ;
* Un administrateur ajoute un compte utilisateur invité sur la page Enregistrement d’utilisateur invité

Le courrier électronique d’enregistrement contient un lien vers une page d’enregistrement et des informations sur la façon de s’enregistrer. Une fois l’utilisateur invité enregistré, Document Security émet un courrier électronique d’activation contenant un lien vers une page d’activation. Une fois activé, le compte reste valide jusqu’à ce que vous le désactivez ou le supprimiez.

Si vous activez l’enregistrement intégré, vous spécifiez une seule fois votre serveur SMTP, les détails des courriers électroniques d’enregistrement, les fonctionnalités d’accès et réinitialisez les informations de courrier électronique de mot de passe. Avant d’activer l’enregistrement intégré, vérifiez que vous avez créé un domaine local dans User Management et que le rôle « Utilisateur invité de Document Security » a été attribué aux utilisateurs, utilisatrices et groupes appropriés de votre organisation. (Voir [Ajouter un domaine local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) et [Création et configuration des rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Si vous n’utilisez pas l’enregistrement intégré, votre propre système d’enregistrement d’utilisateur doit être créé à l’aide du SDK d’AEM forms. Consultez l’aide de la section « Développement de SPI pour AEM Forms » dans [Programmation avec AEM Forms](/help/forms/developing/introducing-java-api-soap-quick.md). Si vous n’utilisez pas l’option Enregistrement intégré, il est recommandé de configurer un message dans l’e-mail d’activation et dans l’écran de connexion du client afin d’informer les utilisateurs de la manière de contacter l’administrateur pour obtenir un nouveau mot de passe ou d’autres informations.

**Activation et configuration de l’enregistrement d’un utilisateur invité**

Par défaut, le processus d’enregistrement des utilisateurs invités est désactivé. Vous pouvez activer et désactiver l’enregistrement des utilisateurs invités pour Document Security, selon les besoins.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Enregistrement d’utilisateur invité.
1. Sélectionnez Activer l’enregistrement d’utilisateur invité.
1. (Facultatif) Mettez à jour les paramètres d’enregistrement de l’utilisateur invité selon les besoins :

   * [Exclusion ou inclusion d’un utilisateur ou d’un groupe externe](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Paramètres des comptes d’enregistrement et du serveur](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Paramètres des courriers électroniques d’invitation à effectuer un enregistrement](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Paramètres des courriers électroniques d’activation](configuring-client-server-options.md#activation-email-settings)
   * [Configuration d’un courrier électronique de réinitialisation de mot de passe](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Facultatif) Sous Enregistrement intégré, sélectionnez Oui pour activer cette option. Si vous n’activez pas l’enregistrement intégré, vous devez configurer votre propre système d’enregistrement des utilisateurs.
1. Cliquez sur OK.

### Exclure ou inclure un utilisateur ou un groupe externe {#exclude-or-include-an-external-user-or-group}

Vous pouvez restreindre l’enregistrement auprès de Document Security à certains utilisateurs ou groupes d’utilisateurs externes. Cette option est utile, par exemple, pour autoriser l’accès à un certain groupe d’utilisateurs, mais exclure des individus spécifiques qui font partie du groupe.

Les paramètres suivants se trouvent dans la zone Filtre de restriction de courrier électronique de la page Enregistrement d’utilisateur invité.

**Exclusion :** saisissez l’adresse électronique d’un utilisateur ou d’un groupe à exclure. Pour exclure plusieurs utilisateurs ou groupes, saisissez chaque adresse électronique sur une nouvelle ligne. Pour exclure tous les utilisateurs appartenant à un domaine particulier, saisissez un caractère générique et le nom de domaine. Par exemple, pour exclure tous les utilisateurs du domaine example.com, saisissez &amp;.example.com.

**Inclusion :** saisissez l’adresse électronique d’un utilisateur ou d’un groupe à inclure. Pour inclure plusieurs utilisateurs ou groupes, saisissez chaque adresse électronique sur une nouvelle ligne. Pour inclure tous les utilisateurs appartenant à un domaine particulier, saisissez un caractère générique et le nom de domaine. Par exemple, pour inclure tous les utilisateurs du domaine example.com, saisissez &amp;.example.com.

### Paramètres des comptes d’enregistrement et du serveur {#server-and-registration-account-parameters}

Les paramètres suivants se trouvent dans la zone Paramètres généraux de la page Enregistrement d’utilisateur invité .

**Hôte SMTP :** le nom d’hôte du serveur SMTP. Le serveur SMTP gère les e-mails sortants pour enregistrer et activer les comptes d’utilisateurs invités.

Si l’hôte SMTP vous l’exige, saisissez les informations requises dans les zones SMTP Server Account Name et SMTP Server Account Password pour vous connecter au serveur SMTP. Certaines organisations n’appliquent pas cette exigence. Si vous avez besoin d’informations, contactez votre administrateur système.

**Nom de la classe de socket du serveur SMTP :** Nom de la classe de socket pour le serveur SMTP. Par exemple, javax.net.ssl.SSLSocketFactory.

**Type de contenu d’email :** Type MIME accepté comme text/plain ou text/html.

**Codage d’email :** format de codage à utiliser pour l’envoi d’un email. Vous pouvez spécifier tout codage, par exemple UTF-8 pour Unicode ou ISO-8859-1 pour Latin. La valeur par défaut est UTF-8.

**Rediriger l’adresse e-mail :** lorsque vous indiquez une adresse e-mail pour ce paramètre, toute nouvelle invitation est envoyée à l’adresse fournie. Ce paramètre peut être utile pour l’exécution de tests.

**Utiliser des domaines locaux :** sélectionnez le domaine approprié. Dans une nouvelle installation, assurez-vous que vous avez créé le domaine à l’aide de User Management. S’il s’agit d’une mise à niveau, un domaine utilisateur externe a été créé lors de la mise à niveau et peut être utilisé.

**Utiliser SSL pour le serveur SMTP :** sélectionnez cette option pour activer SSL pour le serveur SMTP.

**Afficher le lien de connexion sur la page d’inscription :** affiche un lien de connexion sur la page d’enregistrement affichée pour les utilisateurs invités.

**Pour activer le protocole TLS (Transport Layer Security) pour le serveur SMTP**

1. Ouvrez Administration Console.

   L’emplacement par défaut de la console d’administration est le suivant : `https://<server>:<port>/adminui`.

1. Accédez à Accueil > Services > Document Security > Configuration > Enregistrement d’utilisateur invité.
1. Dans Enregistrement d’utilisateur invité, spécifiez tous les paramètres de configuration, puis cliquez sur OK.

   >[!NOTE]
   >
   >Si vous utilisez Microsoft Office 365 comme serveur SMTP afin d’envoyer les invitations d’enregistrement des utilisateurs, utilisez les paramètres suivants :
   >
   >**Hôte SMTP :** smtp.office365.com.
   >**Port :** 587.

1. Vous devez ensuite mettre à jour le fichier config.xml. Voir [Configuration pour activer SMTP pour Transport Layer Security (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Si vous apportez des modifications aux options Enregistrement d’utilisateur invité, le fichier config.xml est remplacé et TLS est désactivé. Si vous écrasez les modifications, vous devez effectuer l’étape ci-dessus pour réactiver la prise en charge du protocole TLS pour l’enregistrement d’utilisateur invité.

### Paramètres des courriers électroniques d’invitation à l’enregistrement {#registration-invitation-email-settings}

Document Security envoie automatiquement un courrier électronique d’invitation à l’enregistrement lorsque vous créez un compte d’utilisateur invité ou lorsqu’un utilisateur existant ajoute un destinataire externe qui ne s’est pas encore enregistré ou qui a été invité à s’enregistrer dans une stratégie. L&#39;email contient un lien que le destinataire peut utiliser pour accéder à la page d&#39;enregistrement et saisir des informations de compte personnelles, notamment son nom d&#39;utilisateur et son mot de passe. Le mot de passe peut être n’importe quelle combinaison de huit caractères.

Lorsque le destinataire active le compte, il devient un utilisateur local.

Les paramètres suivants se trouvent dans la zone Configuration du courrier électronique d’invitation de la page Enregistrement d’utilisateur invité .

**De :** adresse e-mail à partir de laquelle l’e-mail d’invitation est envoyé. Le format par défaut de l’adresse e-mail d’expédition est postmaster@[[votre_domaine_d’installation]].com.

**Objet :** objet par défaut de l’e-mail d’invitation.

**Délai d’expiration :** nombre de jours à l’issue duquel l’invitation à l’enregistrement expire si l’utilisateur externe ne s’enregistre pas. La valeur par défaut est de 30 jours.

**Message :** texte qui apparaît dans le corps du message, invitant l’utilisateur à s’enregistrer.

### Paramètres des courriers électroniques d’activation {#activation-email-settings}

Une fois les utilisateurs invités enregistrés, Document Security envoie un courrier électronique d’activation. L’e-mail d’activation contient un lien vers la page d’activation du compte dans laquelle les utilisateurs peuvent activer leur compte. Lorsque les comptes sont activés, les utilisateurs peuvent se connecter à Document Security à l’aide de leur adresse électronique et du mot de passe qu’ils ont créés lorsqu’ils se sont enregistrés.

Lorsque le destinataire active le compte utilisateur, celui-ci devient un utilisateur local.

Les paramètres suivants se trouvent dans la zone Configuration du courrier électronique d’activation de la page Enregistrement d’utilisateur invité.

>[!NOTE]
>
>Il est également recommandé de configurer un message dans l’écran de connexion afin de conseiller aux utilisateurs externes de contacter leur administrateur pour obtenir un nouveau mot de passe ou d’autres informations.

**De :** adresse e-mail à partir de laquelle l’e-mail d’activation est envoyé. Cette adresse email reçoit les avis d’échec de diffusion de la part de l’hôte de messagerie du destinataire ainsi que tous les messages que ce dernier envoie en réponse à l’email d’enregistrement. Le format par défaut de l’adresse e-mail d’expédition est postmaster@[[votre_domaine_d’installation]].com.

**Objet :** objet par défaut de l’e-mail d’activation.

**Délai d’expiration :** nombre de jours à l’issue duquel l’invitation à l’activation expire si l’utilisateur externe n’active pas le compte. La valeur par défaut est de 30 jours.

**Message :** Le texte qui apparaît dans le corps du message et qui indique que le compte utilisateur du destinataire doit être activé. Vous pouvez également inclure des informations telles que la manière de contacter un administrateur pour obtenir un nouveau mot de passe.

### Configurer un courrier électronique de réinitialisation de mot de passe {#configure-a-password-reset-email}

Si vous devez réinitialiser le mot de passe d’un utilisateur invité, un email de confirmation est généré, invitant l’utilisateur à choisir un nouveau mot de passe. Le mot de passe d’un utilisateur ne peut pas être déterminé ; si l’utilisateur l’oublie, vous devez le réinitialiser.

Les paramètres suivants se trouvent dans la zone Réinitialiser le message électronique de mot de passe de la page Enregistrement d’utilisateur invité .

**De :** l’adresse électronique à partir de laquelle l’e-mail de réinitialisation du mot de passe est envoyé. Le format par défaut de l’adresse électronique d’expédition est postmaster@[your_installation_domain].com.

**Objet :** objet par défaut pour l’e-mail de réinitialisation.

**Message :** Le texte qui apparaît dans le corps du message, un message indiquant que le mot de passe utilisateur externe du destinataire est réinitialisé.

## Activation des utilisateurs et des groupes pour créer des stratégies {#enable-users-and-groups-to-create-policies}

La page Configuration comporte un lien vers la page Mes stratégies, dans laquelle vous spécifiez les utilisateurs finaux autorisés à créer mes stratégies, ainsi que les utilisateurs et groupes visibles dans les résultats de recherche. La page Mes stratégies comporte deux onglets :

**Onglet Créer des politiques :** permet de configurer les autorisations des utilisateurs pour créer des politiques personnalisées.

**Onglet Utilisateurs et groupes visibles :** permet de contrôler quels utilisateurs et groupes sont visibles dans les résultats de recherche des utilisateurs. Le super-utilisateur ou l’administrateur de jeux de stratégies doit sélectionner et ajouter des domaines, créés dans User Management, à l’utilisateur et au groupe visible pour chaque jeu de stratégies. Cette liste est visible par le coordinateur de jeux de stratégies et permet de limiter les domaines que le coordinateur de jeux de stratégies peut parcourir lors du choix des utilisateurs à ajouter aux stratégies.

Avant d’autoriser les utilisateurs à créer des stratégies personnalisées, déterminez le niveau d’accès ou de contrôle que vous souhaitez que les utilisateurs individuels disposent. De plus, déterminez l’exposition de vos utilisateurs et groupes lorsque vous les rendez visibles pour les recherches.

### Spécification des utilisateurs et groupes autorisés à créer des stratégies {#specify-users-and-groups-who-can-create-policies}

En tant qu’administrateur, spécifiez les utilisateurs et les groupes autorisés à créer des stratégies personnalisées. Cette autorisation peut être définie au niveau de l’utilisateur et du groupe. La fonctionnalité de recherche les utilisateurs et les groupes dans la base de données User Management.

1. Dans Administration Console, cliquez sur Services > Document Security > Configuration > Mes stratégies.
1. Sur la page Mes stratégies, cliquez sur l’onglet Créer des stratégies, puis sur Ajouter des utilisateurs et des groupes.
1. Dans la zone Rechercher, saisissez le nom ou l’adresse électronique de l’utilisateur ou du groupe que vous recherchez. Si vous ne disposez pas de ces informations, laissez la zone vide. Vous pouvez également saisir un nom ou une adresse électronique partielle, par exemple lorsque vous ne connaissez que les deux premières lettres d’un nom d’utilisateur.
1. Dans la liste Utilisation, sélectionnez vos paramètres de recherche Nom ou Adresse électronique.
1. Dans la liste Type, sélectionnez Groupe ou Utilisateur pour affiner votre recherche.
1. Dans la liste Dans, sélectionnez le domaine à rechercher. Si vous ne connaissez pas le domaine de l’utilisateur ou du groupe, sélectionnez Tous les domaines.
1. Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page, puis cliquez sur Rechercher.
1. Pour ajouter des utilisateurs et des groupes Mes stratégies, cochez la case correspondant à chaque utilisateur et groupe à ajouter.
1. Cliquez sur Ajouter, puis sur OK.

Les utilisateurs et groupes sélectionnés sont désormais autorisés à créer des stratégies personnalisées.

### Suppression de l’autorisation de création de stratégies personnalisées d’un utilisateur ou d’un groupe {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Dans la page Document Security, cliquez sur Configuration > Mes stratégies.
1. Dans la page Mes stratégies, cliquez sur l’onglet Créer des stratégies . Les utilisateurs et les groupes autorisés à créer des stratégies personnalisées s’affichent.
1. Cochez la case en regard des utilisateurs et des groupes à supprimer de cette autorisation.
1. Cliquez sur Supprimer, puis sur OK.

### Spécification des utilisateurs et groupes visibles dans les recherches {#specify-users-and-groups-that-are-visible-in-searches}

Lorsque les utilisateurs gèrent leurs stratégies personnalisées, ils peuvent rechercher des utilisateurs et des groupes à ajouter à leurs stratégies. Vous devez indiquer les domaines à partir desquels les utilisateurs et les groupes sont visibles dans ces recherches.

1. Dans la page Document Security, cliquez sur Configuration > Mes stratégies.
1. Sur la page Mes stratégies, cliquez sur l’onglet Utilisateurs et groupes visibles.
1. Pour rendre visibles les utilisateurs et les groupes d’un domaine, cliquez sur Ajouter des domaines, sélectionnez les domaines, puis cliquez sur Ajouter. Pour supprimer un domaine, cochez la case en regard de son nom, puis cliquez sur Supprimer.

## Modification manuelle du fichier de configuration de Document Security {#manually-editing-the-document-security-configuration-file}

Vous pouvez importer et exporter les informations de configuration stockées dans la base de données Document Security. Par exemple, vous pouvez effectuer une copie de sauvegarde des informations de configuration lorsque vous passez d’un environnement intermédiaire à un environnement de production, ou vous pouvez modifier des options avancées qui ne peuvent être configurées que lors de la modification de ce fichier.

Vous pouvez effectuer les modifications suivantes à l’aide du fichier de configuration :

[Affichage des autorisations CATIA lors de la création et de la modification de stratégies](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Définition d’un délai d’expiration pour la synchronisation hors ligne](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Refus d’accès aux services Document Security pour des applications spécifiques](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Modification des paramètres de configuration des filigranes](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Désactivation des liens externes](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>L’importation du fichier de configuration reconfigure votre système en fonction des informations contenues dans le fichier. Les exceptions sont les informations de configuration de filigrane dynamique et d’événements personnalisés, qui ne sont pas enregistrées avec le fichier de configuration exporté. Vous devez configurer ces informations manuellement dans votre nouveau système. Seul un administrateur système ou un consultant en services professionnels qui connaît Document Security et XML doit modifier le contenu d’un fichier de configuration, par exemple pour reconfigurer un paramètre corrompu ou pour régler les paramètres d’un scénario de déploiement d’entreprise particulier.

**Exporter un fichier de configuration**

1. Dans Administration Console, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Exporter et enregistrez le fichier de configuration à un autre emplacement. Le nom de fichier par défaut est config.xml.
1. Cliquez sur OK.
1. Avant de modifier le fichier de configuration, effectuez une copie de sauvegarde au cas où vous auriez besoin d’effectuer un rétablissement.

**Importation d’un fichier de configuration**

1. Dans Administration Console, cliquez sur Services > Document Security 11 > Configuration > Configuration manuelle.
1. Cliquez sur Parcourir pour accéder au fichier de configuration, puis sur Importer. Vous ne pouvez pas saisir le chemin directement dans la zone Nom du fichier .
1. Cliquez sur OK.

### Définition d’un délai d’expiration pour la synchronisation hors ligne {#specify-a-timeout-period-for-offline-synchronization}

Document Security permet aux utilisateurs d’ouvrir et d’utiliser des documents protégés lorsqu’ils ne sont pas connectés au serveur Document Security. L’application cliente de l’utilisateur doit régulièrement se synchroniser avec le serveur pour que les documents restent valides pour une utilisation hors ligne. La première fois que les utilisateurs ouvrent un document protégé, ils sont invités à indiquer à leur ordinateur s’il doit être autorisé à effectuer une synchronisation périodique des clients.

Par défaut, la synchronisation a lieu automatiquement toutes les quatre heures et selon les besoins lorsqu’un utilisateur est connecté au serveur Document Security. Si la période hors ligne d’un document expire pendant que l’utilisateur est hors ligne, l’utilisateur doit se reconnecter au serveur pour permettre à l’application cliente de se synchroniser avec le serveur.

Dans le fichier de configuration de Document Security, vous pouvez définir la fréquence par défaut de la synchronisation automatique en arrière-plan. Ce paramètre agit comme le délai d’expiration par défaut des applications client, sauf si le client définit explicitement sa propre valeur de délai d’expiration.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `PolicyServer`. Sous ce nœud, recherchez le nœud `ServerSettings`.
1. Dans le nœud `ServerSettings`, ajoutez l’entrée suivante, puis enregistrez le fichier :

   `<entry key="BackgroundSyncFrequency" value="`*durée* `"/>`

   où *time* correspond au nombre de secondes entre les synchronisations automatiques en arrière-plan. Si vous définissez cette valeur sur `0`, la synchronisation a lieu en continu. La valeur par défaut est `14400` secondes (toutes les quatre heures).

1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Refuser l’accès aux services Document Security pour des applications spécifiques {#denying-document-security-services-for-specific-applications}

Vous pouvez configurer Document Security pour refuser des services aux applications qui répondent à des critères spécifiques. Les critères peuvent spécifier un attribut unique, tel qu’un nom de plateforme, ou spécifier plusieurs jeux d’attributs. Cette fonctionnalité peut vous aider à contrôler les requêtes que Document Security doit traiter. Voici quelques applications de cette fonctionnalité :

* **Protection des revenus :** vous pouvez refuser l’accès à toute application cliente ne prenant pas en charge vos conventions de revenus.
* **Compatibilité des applications :** certaines applications peuvent être incompatibles avec les politiques ou le comportement de votre serveur Document Security.

Lorsque des applications clientes tentent d’établir un lien avec Document Security, elles fournissent des informations sur l’application, la version et la plateforme. Document Security compare ces informations aux paramètres de refus qu’il obtient à partir du fichier de configuration de Document Security.

Les paramètres de refus peuvent contenir plusieurs jeux de conditions de refus. Si tous les attributs d’un jeu correspondent, l’application qui demande ne peut pas accéder aux services Document Security.

La fonctionnalité de refus de service requiert que les applications clientes utilisent le SDK client C++ Document Security version 8.2 ou ultérieure. Les produits Adobe suivants fournissent des informations sur les produits lors de la demande de services Document Security :

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard et versions ultérieures
* Adobe Reader 9.0 et versions ultérieures
* Extensions Acrobat Reader DC pour Microsoft Office 8.2 et versions ultérieures

Les applications clientes utilisent l’API cliente du SDK client C++ Document Security pour demander des services à Document Security. Les demandes de l’API client incluent des informations sur la plateforme et la version du SDK (précompilées dans l’API client) ainsi que des informations sur les produits obtenues à partir de l’application cliente.

Les applications clientes ou les plug-ins fournissent des informations sur les produits dans leur mise en oeuvre d’une fonction de rappel. L’application fournit les informations suivantes :

* Nom de l’intégrateur
* Version de l’intégrateur
* Famille d’applications
* Nom de l’application
* Version de l’application

Si des informations ne sont pas applicables, l’application cliente laisse le champ correspondant vide.

Plusieurs applications Adobe incluent des informations sur les produits lors de la demande de services Document Security, notamment Acrobat, Adobe Reader et les extensions Acrobat Reader DC pour Microsoft Office.

**Acrobat et Adobe Reader**

Lorsque Acrobat ou Adobe Reader demande un service auprès de Document Security, il fournit les informations suivantes sur les produits :

* **Intégrateur :** Adobe Systems, Inc.
* **Version de l’intégrateur :** 1.0
* **Famille de l’application :** Acrobat
* **Nom de l’application :** Acrobat
* **Version de l’application :** 9.0.0

**Extensions Acrobat Reader DC pour Microsoft Office**

Les extensions Acrobat Reader DC pour Microsoft Office sont un module externe utilisé avec les produits Microsoft Office : Microsoft Word, Microsoft Excel et Microsoft PowerPoint. Lorsqu’il demande un service, il fournit les informations suivantes :

* **Intégrateur :** Adobe Systems Incorporated
* **Version de l’intégrateur :** 8.2
* **Famille d’applications :** Extensions d’Acrobat Reader DC pour Microsoft Office
* **Nom de l’application :** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Version de l’application :** 2003 ou 2007

**Configuration de Document Security pour le refus de services pour des applications spécifiques**

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
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

   `SDKPlatforms` indique la plateforme hébergeant l’application cliente. Les valeurs possibles sont les suivantes :

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` indique la version de l’API Client C++ de Document Security utilisée par l’application cliente. Par exemple, `"8.2"`.

   `APPFamilies` est défini par l’API Client.

   `AppName`indique le nom de l’application cliente. Les virgules sont utilisées comme séparateurs de nom. Pour inclure une virgule dans un nom, ajoutez une barre oblique inverse (\) en guise d’échappement. Par exemple : *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` indique la version de l’application cliente.

   `Integrators` indique le nom de la société ou du groupe ayant développé le module supplémentaire ou l’application intégrée.

   `IntegratorVersions` correspond à la version du module supplémentaire ou de l’application intégrée.

1. Pour chaque jeu supplémentaire de données de refus, ajoutez un autre *MyEntryName* élément .
1. Enregistrez le fichier de configuration.
1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Exemples**

Dans cet exemple, tous les clients Windows se voient refuser l’accès.

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

Dans cet exemple, l’accès à My Application version 3.0 et My Other Application version 2.0 est refusé. La même URL d’information de refus est utilisée quelle que soit la raison du refus.

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

Dans cet exemple, toutes les demandes provenant d’une installation Microsoft PowerPoint 2007 ou Microsoft PowerPoint 2010 d’Acrobat Reader DC extensions pour Microsoft Office sont refusées.

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

Par défaut, vous pouvez spécifier un maximum de cinq éléments dans un filigrane. En outre, la taille de fichier maximale du document du PDF que vous souhaitez utiliser comme filigrane est limitée à 100 Ko. Vous pouvez modifier ces paramètres dans le fichier config.xml .

***Remarque ** : si vous modifiez ces paramètres, faites-le avec précaution.*

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `ServerSettings`.
1. Dans le nœud `ServerSettings`, ajoutez les entrées suivantes, puis enregistrez le fichier : `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`.

   La première entrée, *taille de fichier maximale* est la taille de fichier maximale (en Ko) qui est autorisée pour un élément de filigrane en format PDF. La valeur par défaut est de 100 Ko.

   la seconde entrée, *éléments max* est le nombre maximal d’éléments autorisés dans un filigrane. La valeur par défaut est 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Désactiver les liens externes {#disabling-external-links}

De nombreux utilisateurs de Document Security n’ont pas accès aux liens externes tels que **www.adobe.com** pendant qu’ils utilisent les interfaces utilisateur de Rights Management :

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Les modifications suivantes apportées au fichier config.xml désactivent tous les liens externes des interfaces utilisateur de Rights Management.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. Pour désactiver tous les liens externes, dans le nœud `DisplaySettings`, ajoutez l’entrée suivante, puis enregistrez le fichier : `<entry key="ExternalLinksAllowed" value="false"/>`.

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configuration pour activer SMTP pour Transport Layer Security (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Les modifications suivantes apportées au fichier config.xml activent la prise en charge de TLS pour la fonction Enregistrement d’utilisateur invité.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud `DisplaySettings`.
1. Localisez le nœud suivant : `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Définissez la valeur de la clé `SmtpUseTls` du nœud `ExternalUser` sur **true**.
1. Définissez la valeur de la clé `SmtpUseSsl` du nœud `ExternalUser` sur **false**.
1. Enregistrez le fichier `config.xml`.
1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Désactivation des points de fin SOAP pour les documents Document Security {#disable-soap-endpoints-for-document-security-documents}

Les modifications suivantes apportées au fichier config.xml désactivent les points de fin SOAP pour les documents Document Security.

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le noeud suivant : `<node name="DRM">`

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
1. Importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Évolutivité croissante du serveur Document Security {#increasingscalability}

Par défaut, lors de la synchronisation d’un document pour une utilisation hors ligne, ainsi que des informations relatives au document actif, les clients Document Security récupèrent les informations de mise à jour des stratégies, filigranes, licences et de révocation pour tous les autres documents auxquels l’utilisateur a accès. Si ces mises à jour et informations ne sont pas synchronisées avec le client, un document ouvert en mode hors ligne peut toujours s’ouvrir avec des informations de stratégie, de filigrane et de révocation plus anciennes.

Vous pouvez augmenter l’évolutivité du serveur Document Security en limitant les informations envoyées au client. La réduction de la quantité d’informations envoyées au client entraîne une évolutivité améliorée, un temps de réponse réduit et de meilleures performances du serveur. Effectuez les étapes suivantes pour augmenter l’évolutivité :

1. Exportez le fichier de configuration de Document Security. (Voir [Modification manuelle du fichier de configuration de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Ouvrez le fichier de configuration dans un éditeur et recherchez le nœud ServerSettings.
1. Dans le nœud ServerSettings, définissez la valeur de la propriété `DisableGlobalOfflineSynchronizationData` sur `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Lorsque la valeur est définie sur true, le serveur Document Security envoie des informations uniquement pour le document actif tandis que les informations relatives aux documents restants (les autres documents auxquels un utilisateur a accès) ne sont pas envoyées au client.

   >[!NOTE]
   >
   >Par défaut, la valeur de la clé `DisableGlobalOfflineSynchronizationData` est définie sur `false`.

1. Enregistrez et importez le fichier de configuration. (Voir [Modification manuelle du fichier de configuration de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
