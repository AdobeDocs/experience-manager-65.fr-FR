---
title: Créer et gérer des politiques
description: Une politique définit un jeu de paramètres de confidentialité et les utilisateurs et utilisatrices habilités à accéder au document auquel la politique est appliquée. Vous pouvez créer et gérer différents types de politiques à l’aide d’AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 5e57451c-1a89-442c-8404-841e95d5ceff
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '4713'
ht-degree: 100%

---

# Créer et gérer des politiques {#creating-and-managing-policies}

Une *politique* définit un jeu de paramètres de confidentialité et les utilisateurs et utilisatrices habilités à accéder au document auquel la politique est appliquée. Les *jeux de politiques* regroupent plusieurs politiques ayant une finalité métier commune. Ces jeux de politiques sont ensuite rendus accessibles à un sous-ensemble d’utilisateurs et d’utilisatrices du système. Pour plus d’informations sur les politiques, voir [Politiques et documents protégés par une politique](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Types de politiques {#types-of-policies}

Document Security fournit les types de politiques suivants.

**Politiques personnelles**

Les utilisateurs et utilisatrices peuvent créer, modifier, copier, supprimer et appliquer leurs propres politiques avec des paramètres appropriés à une situation donnée. Seules la personne qui crée une politique et l’équipe d’administration peuvent accéder à cette politique personnelle. Les politiques personnelles apparaissent dans l’onglet Mes politiques de la page Politiques.

Les utilisateurs et utilisatrices invités peuvent également créer, copier et supprimer des politiques personnelles si l’équipe d’administration active cette fonctionnalité.

**Politiques partagées**

Les équipes d’administration et de coordination des jeux de politiques créent des politiques partagées en fonction des exigences de confidentialité que votre organisation identifie pour différents types de documents et d’utilisateurs et utilisatrices. Les politiques partagées sont contenues dans des jeux de politiques et sont disponibles pour tous les utilisateurs et utilisatrices autorisés (équipes d’édition, de coordination de jeux de politiques et destinataires de documents) pour un jeu de politiques particulier. Les équipes d’administration et de coordination de jeux de politiques peuvent activer et désactiver des politiques partagées. Les politiques partagées apparaissent dans les jeux de politiques, sous l’onglet Jeux de politiques de la page Politiques.

Lors de sa première installation, Document Security contient une politique partagée nommée *Limiter à toutes les entités*. Lorsque cette politique est appliquée à un document, un utilisateur ou une utilisatrice qui peut se connecter à Document Security peut accéder au document. Cette politique figure dans le jeu de politiques nommé *Jeu de politiques global*. Par défaut, cette politique n’est pas activée. Vous pouvez l’activer si elle correspond aux besoins de votre organisation.

**Politiques générées automatiquement par Microsoft® Outlook**

Acrobat vous permet d’appliquer des politiques aux documents que vous envoyez en tant que pièces jointes d’e-mail dans Microsoft® Outlook. Dans Outlook, vous pouvez protéger un document à l’aide d’une politique existante. Vous pouvez également utiliser une politique générée automatiquement par Acrobat avec des paramètres de confidentialité par défaut et l’appliquer au document joint à un e-mail. (Voir *[Aide d’Acrobat](https://help.adobe.com/fr_FR/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Pour qu’une politique soit disponible dans Outlook, vous devez la définir comme favori dans Acrobat. Toutes les autres politiques, y compris celles pour lesquelles vous êtes Éditeur, ne s’affichent pas dans Outlook.

## Personnes habilitées à créer et à gérer des politiques et des jeux de politiques {#who-can-create-and-manage-policies-and-policy-sets}

La manière dont vous interagissez avec les politiques et les jeux de politiques dépend de votre rôle au sein de l’organisation :

**Utilisateurs :** les utilisateurs peuvent créer, modifier et supprimer leurs politiques personnelles. Les utilisateurs invités peuvent également créer des politiques personnelles si l’administrateur active cette fonctionnalité.

**Coordinateurs de jeux de politiques :** les coordinateurs de jeux de politiques peuvent créer et gérer les politiques partagées figurant dans les jeux de politiques pour lesquels ils ont été désignés en tant que coordinateur. Au sein de l’organisation, c’est généralement la personne la plus à même de créer des politiques dans un jeu donné.

**Administrateurs et administratrices :** les équipes d’administration peuvent modifier les politiques personnelles de n’importe quel utilisateur ou n’importe quelle utilisatrice. Elles peuvent créer des politiques partagées. Elles peuvent également créer, modifier et supprimer des jeux de politiques, et désigner des coordinateurs et coordinatrices de jeux de politiques.

Pour plus d’informations sur les différents rôles de Document Security, consultez la section [À propos des utilisateurs de Document Security](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Créer et modifier des politiques {#creating-and-editing-policies}

Les utilisateurs et utilisatrices peuvent créer ou modifier des politiques personnelles pour leur propre usage. Les équipes d’administration et de coordination de jeux de politiques peuvent créer ou modifier des politiques partagées pour votre organisation.

### Considérations relatives à la modification des politiques {#considerations-for-editing-policies}

Lorsque vous modifiez une politique, les modifications affectent les documents actuellement protégés par cette dernière, ainsi que ceux qui le seront. Par exemple, si vous supprimez des destinataires d’une politique appliquée à un document, ces destinataires ne peuvent plus ouvrir le document.

Le statut du document détermine le moment où la modification prend effet :

* Si le document est en ligne, les modifications sont appliquées immédiatement, sauf si l’utilisateur ou l’utilisatrice l’a ouvert. Dans ce cas, l’utilisateur ou l’utilisatrice doit fermer le document pour que les modifications soient prises en compte.
* Si un destinataire utilise le document hors ligne (par exemple, sur un ordinateur portable), les modifications prennent effet lorsque le ou la destinataire remet le document en ligne. Il se synchronise ensuite avec Document Security en ouvrant un document protégé par une politique.

>[!NOTE]
>
>Les politiques générées automatiquement par Acrobat pour les destinataires des documents joints aux e-mails dans Microsoft® Outlook n’apparaissent pas dans la liste des politiques. Vous ne pouvez afficher ces politiques qu’en ouvrant la page Détails du document correspondant au document associé.

Lorsque vous modifiez des politiques, ces restrictions s’appliquent :

* Les personnes invitées ne peuvent modifier des politiques que si l’administrateur ou l’administratrice active cette fonctionnalité. Si vous ne pouvez pas modifier de politiques, l’option Modifier n’est pas disponible.
* Les coordinateurs et coordinatrices de jeux de politiques ne peuvent modifier les politiques des jeux de politiques que s’ils disposent des autorisations appropriées. Ces autorisations sont définies par le super-utilisateur ou la super-utilisatrice ou l’administrateur ou administratrice de jeux de politiques dans l’interface d’administration de Document Security.
* Si un filigrane est configuré pour la politique et que l’administrateur ou l’administratrice l’a supprimé depuis la création de la politique, ce filigrane ne sera plus appliqué aux documents si vous modifiez et enregistrez la politique. Les filigranes supprimés restent en vigueur uniquement pour les politiques existantes tant que vous ne modifiez pas la politique. Si vous modifiez la politique, vous devez sélectionner un autre filigrane pour remplacer celui qui a été supprimé.
* Vous ne pouvez pas accorder l’accès anonyme à un document en modifiant la politique appliquée. Si vous modifiez la politique, les utilisateurs et utilisatrices doivent toujours ouvrir une session pour accéder au document. Pour autoriser un accès anonyme à ce document, vous devez commencer par supprimer la politique dans l’application cliente, puis appliquer une autre politique autorisant l’accès anonyme.
* Les politiques générées automatiquement par Adobe pour les destinataires d’un document joint à un e-mail dans Microsoft Outlook n’apparaissent pas dans la liste des politiques. Pour accéder à cette politique, recherchez le document dans la page Documents, ouvrez la page Détails du document et cliquez sur le nom de la politique dans la liste des détails du document.

**Création ou modification d’une politique**

1. Dans la page Document Security, cliquez sur Politiques puis sur l’un des onglets suivants :

   * Pour créer ou modifier une politique personnelle, cliquez sur l’onglet Ma politique.
   * Pour créer ou modifier une politique partagée, cliquez sur l’onglet Jeux de politiques si vous en avez l’autorisation, puis sur le nom du jeu de politiques approprié, et enfin sur l’onglet Politiques.

1. Cliquez sur Nouveau ou sélectionnez la politique à modifier dans la liste.
1. Dans la zone Nom, saisissez un nom qui identifie de manière unique la politique. Dans la zone Description, décrivez le rôle de la politique et ses conditions d’utilisation. Si la politique se trouve dans un jeu de politiques, le nom et la description s’affichent dans la liste des politiques pour tous les les utilisateurs et utilisatrices spécifiés. Les politiques personnelles sont disponibles uniquement pour les utilisateurs et utilisatrices et les administrateurs et administratrices.

   Les caractères suivants ne peuvent pas être utilisés dans le nom ou la description :

   * Signe inférieur à (&lt;)
   * Signe supérieur à (>)
   * Esperluette (&amp;)
   * Apostrophe droite (&#39;)
   * Guillemet anglais (&quot;)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous avez utilisé le caractère suivant dans le nom ou la description, il est converti en espaces :

   * Retour chariot (caractère ASCII 13)
   * Saut de ligne (caractère ASCII 10).

   >[!NOTE]
   >
   >Vous pouvez créer un nom de politique qui contient des caractères étendus. Cependant, en cas de comparaison entre deux chaînes, aucune différence n’est faite entre les caractères accentués et non accentués (« e » et « é », par exemple). Lorsqu’une personne crée une politique, une comparaison est effectuée pour vérifier s’il existe une politique portant le même nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. La politique étant considérée comme existante dans la base de données, aucun ajout n’est possible.

1. Ajoutez des utilisateurs et utilisatrices et des groupes à la politique et définissez les autorisations appropriées. (Voir [Utilisateurs et utilisatrices et groupes](creating-policies.md#users-and-groups).)
1. Sous Paramètres généraux, sélectionnez les options appropriées. (Voir [Paramètres généraux](creating-policies.md#general-settings)).
1. (Facultatif) Le cas échéant, sélectionnez un fournisseur d’autorisations externe et indiquez ses propriétés. Si vous ne souhaitez pas utiliser de fournisseur d’autorisations externe, cliquez sur Supprimer le fournisseur par défaut.

   Un fournisseur d’autorisations externe est utilisé pour configurer des propriétés dans la politique. Lorsqu’il est sélectionné, le fournisseur d’autorisations externe utilise ces informations pour évaluer la politique. Les propriétés disponibles sont configurées par l’administrateur ou l’administratrice et la personne qui installe le logiciel.

1. Sous Paramètres avancés, sélectionnez les options appropriées. (Voir [Paramètres avancés](creating-policies.md#advanced-settings).)
1. Sous Paramètres avancés non modifiables, sélectionnez les options appropriées. (Voir [Paramètres avancés non modifiables](creating-policies.md#unchangeable-advanced-settings).)
1. Cliquez sur Enregistrer. La politique apparaît dans la liste des politiques. Une icône en forme de cercle rouge apparaît en regard de la nouvelle politique, indiquant qu’elle est toujours désactivée.

   Pour mettre la politique à la disposition des utilisateurs et des utilisatrices, activez-la. (Voir [Activation ou désactivation de politiques partagées](creating-policies.md#enable-or-disable-shared-policies).)

### Utilisateurs et groupes  {#users-and-groups}

Dans la zone Utilisateurs et utilisatrices et groupes, vous spécifiez les utilisateurs et utilisatrices ayant accès aux documents protégés par la politique. Pour chaque utilisateur ou utilisatrice ou groupe que vous spécifiez, vous définissez également les privilèges d’utilisation du document.

>[!NOTE]
>
>L’éditeur ou l’éditrice est la personne qui protège le document avec la politique. Cette personne est toujours incluse par défaut dans une politique, avec des droits d’accès complets, notamment des fonctionnalités de révocation et de changement de politique. Toutefois, les administrateurs et administratrices peuvent modifier les droits d’accès de l’éditeur ou de l’éditrice pour les politiques partagées. Par exemple, l’administrateur ou l’administratrice peut empêcher l’éditeur ou l’éditrice de révoquer l’accès au document ou de changer de politique.

**Ajouter un utilisateur ou une utilisatrice ou un groupe :** pour ajouter un utilisateur ou une utilisatrice ou un groupe d’utilisateurs et d’utilisatrices, cliquez sur Ajouter un utilisateur ou une utilisatrice ou un groupe, puis sur Recherche avancée pour trouver des utilisateurs et utilisatrices ou des groupes. Les utilisateurs et utilisatrices incluent les utilisateurs et utilisatrices internes de votre entreprise et les utilisateurs et utilisatrices invités qui se sont enregistrés auprès de Document Security. Lorsque vous sélectionnez cette option, la page Ajouter un utilisateur ou une utilisatrice ou un groupe s’affiche :

* Dans la zone Rechercher, saisissez le nom ou l’adresse électronique de l’utilisateur ou de l’utilisatrice ou du groupe.
* Dans la liste Utilisation, sélectionnez Nom ou E-mail.
* Dans la liste Type, sélectionnez Utilisateur ou utilisatrice ou Groupe.
* Sélectionnez le domaine dans lequel effectuer la recherche dans la liste Dans, puis cliquez sur Rechercher.
* Lorsque les résultats sont renvoyés, sélectionnez l’utilisateur ou l’utilisatrice ou le groupe à ajouter, puis cliquez sur Ajouter.

>[!NOTE]
>
>Si vous saisissez un nom de personne invitée ou une adresse e-mail correcte et qu’aucun résultat n’est renvoyé, la personne n’est peut-être pas encore enregistrée ou le compte peut être supprimé. Vous pouvez essayer d’ajouter l’utilisateur ou l’utilisatrice en tant que personne invitée ou contacter votre administrateur ou administratrice.

**Inviter un nouvel utilisateur ou une nouvelle utilisatrice :** pour ajouter une personne invitée, cliquez sur Inviter un nouvel utilisateur ou une nouvelle utilisatrice, entrez l’adresse e-mail de la personne dans la zone qui s’affiche, puis cliquez sur Inviter. Cette option est disponible uniquement si l’administrateur ou l’administratrice l’a activée. Lorsque vous ajoutez de nouvelles personnes invitées à une politique, Document Security envoie un e-mail d’invitation à s’enregistrer si cela n’a pas été déjà fait. Les personnes doivent utiliser le lien contenu dans l’e-mail pour créer un compte, puis activer le compte.

Après leur enregistrement, les personnes invitées peuvent utiliser les documents protégés par une politique pour lesquels elles disposent d’une autorisation. Selon les fonctionnalités activées par l’administrateur ou l’administratrice, les utilisateurs et utilisatrices externes peuvent être autorisés à appliquer des politiques à des documents, à créer, à modifier et à supprimer des politiques et à ajouter d’autres utilisateurs et utilisatrices externes aux politiques.

**Ajouter un utilisateur anonyme :** pour autoriser l’accès d’un utilisateur anonyme, cliquez sur Ajouter un utilisateur anonyme. Cette option n’est disponible que si l’administrateur a activé l’accès Utilisateur anonyme à Document Security (voir Configuration du serveur Document Security). Cette option permet à l’ensemble des utilisateurs et des utilisatrices d’accéder aux documents protégés par cette politique, qu’ils disposent ou non d’un compte Document Security. Si vous sélectionnez cette option, vous ne pouvez pas ajouter d’autres types d’utilisateurs et d’utilisatrices à la politique.

>[!NOTE]
>
>Pour autoriser l’accès anonyme à un document protégé par une politique qui ne permet pas ce type d’accès, supprimez la politique existante, puis appliquez une politique qui autorise l’accès anonyme. Si vous changez de politique ou si vous la modifiez, les utilisateurs et utilisatrices doivent toujours se connecter pour accéder au document.

#### Spécification des droits de documents pour les utilisateurs, les utilisatrices et les groupes {#specify-the-document-permissions-for-users-and-groups}

Vous pouvez spécifier des autorisations de document pour un utilisateur, une utilisatrice ou un groupe à la fois, ou sélectionner plusieurs utilisateurs et utilisatrices et groupes dans la liste et modifier leurs autorisations à l’aide des options de la zone des en-têtes de colonne.

Par défaut, tous les documents protégés par une politique disposent d’une autorisation qui permet aux utilisateurs et utilisatrices de les ouvrir en ligne.

Les onglets Droits et Options s’affichent dans Document Security.

Ces droits de document sont disponibles dans l’onglet Droits. Vous pouvez les appliquer aux fichiers PDF, PTC Pro/E et Microsoft Office.

**Imprimer :** autorise l’utilisateur à imprimer un document protégé par cette politique. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Imprimer pour autoriser l’impression ou la décocher pour empêcher l’impression. Si vous cochez la case Afficher les droits personnalisés pour PDF, vous pouvez choisir l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à imprimer le PDF.

**Autorisé :** l’utilisateur est autorisé à imprimer le PDF.

**Basse résolution seulement :** l’utilisateur est autorisé à imprimer le PDF en basse résolution.

**Modifier :** autorise l’utilisateur à modifier un document protégé par cette politique. Pour les fichiers Office et Pro/E, vous pouvez cocher la case Modifier pour autoriser les modifications, ou la décocher dans le cas contraire. Si vous cochez la case Afficher les droits personnalisés pour PDF, vous pouvez choisir l’une des options suivantes :

**Non autorisé :** l’utilisateur n’est pas autorisé à modifier le PDF.

**Autorisé :** l’utilisateur peut modifier le PDF.

**Collaborer :** l’utilisateur est autorisé à collaborer avec d’autres utilisateurs, en utilisant les options de collaboration d’Adobe Acrobat. Cette autorisation permet à l’utilisateur de copier les données d’un formulaire, même si l’autorisation Copier n’est pas explicitement donnée dans la politique.

**Modifier les pages :** l’utilisateur est autorisé à ajouter et à supprimer des pages, ainsi qu’à modifier du contenu dans le PDF.

**Remplir et signer :** l’utilisateur est autorisé à remplir les champs de formulaire du PDF et à le signer.

**Copier :** autorise l’utilisateur à copier du texte d’un document protégé par cette politique.

**Lecteur d’écran :** cette autorisation s’affiche si vous cochez la case Afficher les droits personnalisés pour PDF. Lorsque cette option est sélectionnée, Adobe Acrobat a l’autorisation d’ajouter des balises temporaires sur le PDF pour améliorer sa lisibilité sur un lecteur d’écrans.

Ces droits de document sont disponibles dans l’onglet Options. Vous pouvez les appliquer aux fichiers PDF, PTC Pro/E et Microsoft Office :

**Hors ligne :** autorise l’utilisateur à afficher hors ligne un document protégé par cette politique.

**Validité des autorisations :** sélectionnez Autorisations toujours valables ou définissez une période de validité pour les autorisations du document. Si vous sélectionnez une période de validité, cliquez sur les icônes de calendrier pour sélectionner une date et utilisez les flèches pour spécifier l’heure au format 24 heures.

Pour les politiques partagées, les administrateurs et les administratrices peuvent désactiver les privilèges de l’éditeur ou de l’éditrice (l’utilisateur ou l’utilisatrice qui applique la politique à un document) ci-dessous :

**Révoquer :** autorise l’éditeur du document à révoquer les privilèges d’accès au document.

**Changer :** autorise l’éditeur du document à changer les privilèges des politiques.

### Paramètres généraux {#general-settings}

La zone Paramètres généraux contient les paramètres suivants :

**Période de validité :** période pendant laquelle le document protégé par une politique est accessible aux destinataires autorisés. Plusieurs périodes de validité sont proposées :

**Le document ne sera pas valide après :** le document est accessible pendant le nombre de jours spécifié à partir du moment où il a été protégé.

**Le document ne sera pas valide après cette date :** le document est valide à partir de la date d’application de la politique au document jusqu’à la date de fin spécifiée.

**Valide de, jusqu’à :** le document est valide pendant les dates que vous avez spécifiées. Le cas échéant, vous pouvez utiliser le calendrier pour sélectionner une date. Pour ce faire, cliquez sur l’icône de calendrier.

**Document toujours valide :** la période de validité du document n’expire pas.

>[!NOTE]
>
>les dates de validité reposent sur le fuseau horaire du système Document Security, et non sur celui de votre ordinateur local.

**Réaliser un audit :** permet d’activer ou de désactiver la réalisation d’un audit des événements associés à un document protégé par une politique. Par exemple, Document Security peut enregistrer des événements tels que les tentatives d’ouverture d’un document. Les événements contrôlés sont répertoriés dans la liste de la page Evénements. Si vous ne sélectionnez pas cette option, Document Security n’enregistre pas les événements concernant les documents associés à cette politique.

>[!NOTE]
>
>L’administrateur ou l’administratrice doit également activer le contrôle du serveur dans la page de configuration Options de contrôle et de confidentialité.

**Suivi des utilisations étendues :** activez ou désactivez le suivi des utilisations étendues. Document Security prend en charge le suivi des événements utilisateur associés à diverses opérations effectuées sur un fichier PDF. Vous pouvez accéder à l’objet Document Security à l’aide d’un script Java. Le fait de cliquer sur un bouton, un fichier multimédia en cours de lecture ou l’enregistrement d’un fichier sont quelques exemples d’événements pouvant être envoyés par un fichier PDF protégé par une politique. À l’aide de l’objet Document Security, vous pouvez également récupérer des informations sur l’utilisateur ou l’utilisatrice. Le suivi des événements peut être activé sur le serveur Document Security au niveau global ou au niveau de la politique.

**Période d’ouverture hors ligne :** nombre maximum de jours pendant lesquels le destinataire peut utiliser le document protégé par une politique hors ligne (c’est-à-dire sans être connecté à Internet ou à un réseau). À l’issue de cette période d’ouverture, le ou la destinataire doit resynchroniser le document pour continuer à l’utiliser.

### Fournisseurs d’autorisations externes {#external-authorization-providers}

Sélectionnez les fournisseurs d’authentification externes si vous en avez déjà configuré. Les fournisseurs disponibles sont répertoriés.

### Paramètres d’authentification {#authentication-settings}

Vous pouvez remplacer les paramètres d’authentification que vous avez configurés sur le serveur et spécifier les options d’authentification pertinentes pour cette politique. Sélectionnez Remplacer les paramètres d’authentification globaux, puis sélectionnez les options d’authentification pertinentes pour cette politique. Les options d’authentification suivantes sont disponibles :

**Autoriser l’authentification par nom d’utilisateur ou d’utilisatrice/mot de passe :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification par nom d’utilisateur ou d’utilisatrice/mot de passe lors de la connexion au serveur.

**Autoriser l’authentification Kerberos :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification Kerberos lors de la connexion au serveur.

**Autoriser l’authentification de certificat client :** sélectionnez cette option pour permettre aux applications clientes d’utiliser l’authentification de certificat lors de la connexion au serveur.

**Autoriser l’authentification étendue :** sélectionnez cette option pour activer l’authentification étendue. La sélection de cette option permet aux applications clientes d’utiliser l’authentification étendue. L’authentification étendue fournit des processus d’authentification personnalisés et différentes options d’authentification configurées sur le serveur Document Security.

Si vous remplacez les paramètres d’authentification globaux, vous pouvez choisir les options d’authentification pertinentes pour cette politique. Par exemple, si vous avez activé trois options d’authentification (nom d’utilisateur ou d’utilisatrice et mot de passe, certificat client et authentification étendue) sur le serveur, vous pouvez remplacer ce paramètre global et sélectionner uniquement l’authentification étendue pour cette politique. Assurez-vous que l’option d’authentification que vous sélectionnez ici est déjà configurée sur le serveur. Dans cet exemple, vous ne pouvez pas sélectionner Kerberos comme option d’authentification, car elle n’est pas configurée sur le serveur.

>[!NOTE]
>
>L’authentification étendue est prise en charge sur Apple Mac OS X doté de la version 11.0.6 d’Adobe Acrobat et ultérieure.

### Paramètres avancés {#advanced-settings}

La zone Paramètres avancés contient les paramètres suivants :

**Filigrane dynamique :** sélectionnez un filigrane à afficher dynamiquement dans les pages d’un document (par exemple lorsqu’un destinataire imprime le document). Les filigranes dynamiques identifient de manière unique un document, ce qui permet d’assurer la confidentialité de ce dernier et d’empêcher toute violation du copyright. Par exemple, l’administrateur ou l’administratrice peut configurer un filigrane dynamique qui affiche la date actuelle, le nom d’utilisateur ou d’utilisatrice ou l’identifiant de la personne qui utilise le document. Ou le nom de la politique utilisée pour protéger le document. Un filigrane peut également afficher du texte ou des éléments graphiques personnalisés, s’ils sont configurés. Les administrateurs et administratrices configurent les options de filigrane, et tout comme les utilisateurs et utilisatrices, peuvent les appliquer à des politiques.

(Voir [Configuration des filigranes dynamiques](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Si vous modifiez une politique et que l’administrateur ou l’administratrice a supprimé un filigrane configuré que vous aviez sélectionné pour cette politique, un message s’affiche dans la page Modifier la politique. Dans ce cas, si vous enregistrez le document modifié, sélectionnez un nouveau filigrane si vous souhaitez qu’il apparaisse sur le document.

>[!NOTE]
>
>Pour les politiques qui autorisent les accès anonymes, le nom d’utilisateur ou d’utilisatrice et l’identifiant d’un utilisateur ou d’une utilisatrice anonyme ne s’affichent pas en filigrane, même si vous sélectionnez ce type de filigrane.

**N’utiliser que des modules externes Acrobat certifiés pour PDF :** lorsque cette option est sélectionnée pour une politique, elle spécifie qu’Acrobat version 8.0 ou ultérieure doit s’exécuter en mode certifié lors de l’ouverture de documents sécurisés par cette politique. Lorsqu’Acrobat s’exécute en mode certifié, il ne charge aucun plug-in tiers.

Sélectionnez cette option si une personne destinataire d’un document crée un plug-in susceptible de contourner les protections de documents dans Acrobat 8.0 et versions ultérieures. Ne la sélectionnez pas si les personnes destinataires du document doivent utiliser des plug-ins tiers dans Acrobat pour interagir avec les documents.

Cette option active uniquement le mode certifié dans Acrobat 8.0 ou version ultérieure ; l’administrateur ou l’administratrice doit désactiver l’accès pour Acrobat 7.0.

(Voir [Configuration du serveur Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Cette option ne s’applique pas à Adobe Reader.

**Message d’erreur « Accès refusé » :** message qui s’affiche lorsqu’un utilisateur non autorisé tente d’ouvrir un document protégé par une politique. Ce message apparaît dans Acrobat. Les clients qui ne peuvent pas afficher ce message affichent un message par défaut pour indiquer que l’accès est refusé.

### Paramètres avancés non modifiables {#unchangeable-advanced-settings}

La zone Paramètres avancés non modifiables contient les paramètres suivants : Vous ne pouvez pas modifier ces paramètres une fois la politique enregistrée.

**Algorithme de chiffrement et longueur de la clé :** utilisé pour protéger vos documents. Faites votre choix parmi les options suivantes :

* AES 128 bits
* AES 256 bits. Cette option est uniquement prise en charge par Acrobat 9.0 et versions ultérieures. Pour utiliser le chiffrement AES 256 pour les fichiers PDF, récupérez et installez les fichiers Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Ces fichiers remplacent les fichiers local_policy.jar et US_export_policy.jar dans le dossier [JAVE_HOME]/lib/security. Par exemple, si vous utilisez Sun JDK 1.6, copiez les fichiers téléchargés dans le dossier [racine_déploiement]/Java/jdk1.6.0_26/lib/security. Vous pouvez télécharger ces fichiers à partir de [Téléchargements de Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Aucun chiffrement. Cette option est actuellement prise en charge par Acrobat 9.0 et versions ultérieures. Si vous sélectionnez cette option, les options Restrictions du document sont désactivées. Cette option peut s’avérer utile si vous souhaitez recourir à Document Security pour le contrôle de documents ou la gestion de versions sans chiffrer le document.

**Restrictions du document :** sélectionnez les composants du document PDF à chiffrer. D’autres applications clientes chiffrent l’intégralité du document, mais pas les fichiers liés ou incorporés. Faites votre choix parmi les options suivantes :

* L’intégralité du document, avec ses pièces jointes et ses métadonnées. Les *métadonnées* décrivent le document et son contenu, et vous pouvez les consulter dans la boîte de dialogue Propriétés du document ou à partir du menu avancé d’Acrobat. Dans Acrobat, vous pouvez joindre des fichiers de différents types (fichiers texte, audio et vidéo, par exemple) à des documents PDF.
* Le document et ses pièces jointes, mais pas ses métadonnées.
* Uniquement les pièces jointes du document. Vous pouvez chiffrer les pièces d’un fichier PDF sans chiffrer le contenu du document.

## Activation ou désactivation de politiques partagées {#enable-or-disable-shared-policies}

Pour qu’une politique partagée soit disponible, l’administrateur ou l’administratrice, ou le coordinateur ou la coordinatrice de jeux de politiques doit l’activer. Vous pouvez activer de nouvelles politiques ou des politiques qui ont été désactivées. Une politique partagée que vous désactivez s’applique toujours aux documents qui sont protégés par celle-ci.

Une croix (X) rouge apparaît en regard d’une politique désactivée.

>[!NOTE]
>
>Les administrateurs et les administratrices ne peuvent pas désactiver les politiques personnelles, et les utilisateurs et utilisatrices ne peuvent pas activer ni désactiver leurs propres politiques.

1. Dans la page Document Security, cliquez sur Politiques, puis sur l’onglet Jeux de politiques.
1. Cliquez sur le nom du jeu de politiques approprié, puis sur l’onglet Politiques.
1. Cochez la case située en regard de la politique appropriée, cliquez sur Activer ou sur Désactiver, puis sur OK.

## Affichage des informations sur une politique {#view-information-about-a-policy}

L’onglet Mes politiques vous permet de rechercher des politiques personnelles.

Les jeux de politiques créés par les administrateurs et les administratrices sont répertoriés dans l’onglet Jeux de politiques de la page Politiques. Ils contiennent des informations sur le jeu de politiques, notamment son nom, la date de création et de modification, ainsi qu’une description. Cliquez sur le nom d’un jeu de politiques pour en afficher les détails. Les coordinateurs et les coordinatrices de jeux de politiques autorisés à gérer les politiques peuvent créer des politiques partagées au sein d’un jeu de politiques spécifique.

Lorsque vous créez ou modifiez une politique, une page apparaît dans laquelle vous pouvez configurer le nom de la politique, les autorisations, les paramètres de confidentialité et les destinataires à inclure dans la politique.

L’administrateur ou l’administratrice peut configurer les paramètres de confidentialité suivants pour une politique :

* les options de confidentialité générales, comme la période de validité et la période d’ouverture hors connexion des documents ;
* les utilisateurs et les utilisatrices autorisés, ainsi que les restrictions et privilèges de document pour ces utilisateurs et utilisatrices ;
* les options de confidentialité avancées, notamment les filigranes dynamiques et le chiffrement de document.

Les utilisateurs et les utilisatrices peuvent afficher les politiques créées et celles partagées auxquelles ils ont accès. Les administrateurs et les administratrices peuvent afficher toutes les politiques partagées et personnelles dans Document Security.

Vous pouvez afficher d’autres informations plus détaillées sur une politique de la liste, notamment les utilisateurs et les utilisatrices, ou les groupes inclus dans la politique et les paramètres de confidentialité spécifiés pour ces utilisateurs et utilisatrices.

>[!NOTE]
>
>Les politiques générées automatiquement par Acrobat pour les destinataires d’un document joint à un e-mail dans Microsoft Outlook n’apparaissent pas dans la liste des politiques. Vous ne pouvez afficher ces politiques qu’en ouvrant la page Détails du document correspondant au document associé.

1. Dans la page Document Security, cliquez sur Politiques, puis sur l’onglet Mes politiques.
1. Remplissez les informations de recherche pour rechercher des politiques personnelles.
1. Sélectionnez la politique appropriée dans la liste.
1. Sur la page Détails de la politique, vous pouvez afficher les détails se rapportant à la politique, la modifier ou afficher les événements liés à cette politique.

## Recherche de politiques {#search-for-policies}

Les administrateurs et les administratrices peuvent rechercher des politiques partagées, ainsi que des politiques personnelles créées par d’autres utilisateurs ou utilisatrices.

1. Pour rechercher une politique partagée, cliquez sur Politiques, puis sur l’onglet Jeux de politiques. Cliquez sur un jeu de politiques dans la liste, puis sur l’onglet Politiques.

   Pour rechercher une politique personnelle, dans la page Document Security, cliquez sur Politiques, puis sur l’onglet Mes politiques.

1. Dans la liste Rechercher, sélectionnez l’une des options suivantes :

   **ID de politique :** numéro d’identification de politique généré lors de la création de la politique par l’utilisateur. Saisissez l’ID de politique exact.

   **Nom de la politique :** nom de la politique. Vous pouvez rechercher une partie ou la totalité du nom de la politique.

1. Dans la zone de texte, saisissez la valeur correspondante. Par exemple, si vous avez sélectionné Nom de la politique, saisissez le nom de la politique que vous recherchez.
1. Dans la liste Afficher, indiquez le nombre d’éléments à afficher, puis cliquez sur Rechercher. Les résultats de la recherche s’affichent.
1. (Facultatif) Pour afficher les détails de la politique, cliquez dessus.

## Copie d’une politique {#copy-a-policy}

Vous pouvez copier une politique existante et l’enregistrer avec un nouveau nom et une nouvelle description. La copie de politiques est un moyen efficace de créer des politiques à l’aide de paramètres existants.

Les utilisateurs et utilisatrices externes ne peuvent copier des politiques que si l’administrateur ou l’administratrice active cette fonctionnalité. Si vous ne pouvez pas créer de politiques, l’option Copier n’est pas disponible.

1. Dans la page Document Security, cliquez sur Politiques, puis sur l’onglet Ma politique.
1. Sélectionnez la politique appropriée dans la liste.
1. Sur la page Détails de la politique, cliquez sur Copier.
1. Dans la zone Nom de la nouvelle politique, saisissez le nouveau nom de la politique. Vous pouvez également saisir une nouvelle description.

   Les caractères suivants ne peuvent pas être utilisés dans le nom ou la description :

   * Signe inférieur à (&lt;)
   * Signe supérieur à (>)
   * Esperluette (&amp;)
   * Apostrophe droite (&#39;)
   * Guillemet anglais (&quot;)
   * barre oblique inverse (\)
   * Barre oblique (/)

   Si vous avez utilisé le caractère suivant dans le nom ou la description, il est converti en espaces :

   * Retour chariot (caractère ASCII 13)
   * Saut de ligne (caractère ASCII 10).

   >[!NOTE]
   >
   >Vous pouvez créer un nom de politique qui contient des caractères étendus. Cependant, en cas de comparaison entre deux chaînes, aucune différence n’est faite entre les caractères accentués et non accentués (« e » et « é », par exemple). Lorsqu’une personne crée une politique, une comparaison est effectuée pour vérifier s’il existe une politique portant le même nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. La politique étant considérée comme existante dans la base de données, aucun ajout n’est possible.

1. Cliquez sur OK.

## Suppression d’une politique {#delete-a-policy}

Vous pouvez supprimer les politiques que vous avez créées. Les administrateurs et administratrices peuvent supprimer les politiques créées par n’importe quelle personne. Les coordinateurs et coordinatrices de jeux de politiques peuvent supprimer des politiques dans leurs jeux de politiques. Une politique que vous supprimez continue à s’appliquer aux documents protégés par celle-ci. Vous pouvez supprimer plusieurs politiques à la fois.

Les personnes invitées ne peuvent supprimer des politiques que si l’administrateur ou l’administratrice active cette fonctionnalité. Si vous ne pouvez pas supprimer de politiques, l’option de suppression n’est pas disponible.

1. Dans la page Document Security, cliquez sur Politiques.
1. Cliquez sur l’onglet Ma politique.
1. Pour supprimer une politique partagée, cliquez sur l’onglet Jeux de politiques, puis sur le nom du jeu de politiques approprié.
1. Cochez la case située en regard de l’utilisateur ou de l’utilisatrice, cliquez sur Supprimer, puis sur OK.

>[!NOTE]
>
>Utilisez l’application cliente pour supprimer des politiques de documents. (Consultez l’aide d’Acrobat ou l’aide des extensions Acrobat Reader DC appropriée.)

## Trie de la liste des politiques {#sort-the-policy-list}

Pour faciliter la recherche de politiques, vous pouvez en trier la liste par en-tête de colonne. Une icône en forme de triangle située en regard de l’en-tête de colonne indique la colonne triée. Lorsque le triangle est dirigé vers le haut, l’ordre de tri est croissant et lorsqu’il est dirigé vers le bas, l’ordre de tri est décroissant.

1. Dans la page Document Security, cliquez sur Politiques, puis sur l’onglet Jeu de politiques.
1. Sélectionnez un jeu de politiques, puis cliquez sur l’onglet Politiques.
1. Cliquez sur l’en-tête de colonne approprié.
1. Pour modifier l’ordre de tri, cliquez de nouveau sur la colonne.
