---
title: Qu’est-ce que Document Security ?
description: Découvrez comment vous pouvez facilement créer, stocker et appliquer des paramètres de confidentialité prédéfinis et répartir vos informations en toute sécurité à l’aide de Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: 0cdc9ee3-0172-43be-9b62-ed768534c074
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '3219'
ht-degree: 100%

---

# À propos de Document Security {#about-document-security}

Grâce à Document Security, seuls les utilisateurs et utilisatrices autorisés peuvent utiliser vos documents. Document Security vous permet de distribuer en toute sécurité toute information enregistrée sous un format pris en charge. Les formats de fichiers pris en charge sont :

* Les fichiers Adobe PDF
* Les fichiers Microsoft® Word, Excel et PowerPoint

Pour plus d’informations sur la façon dont les politiques protègent les types de fichiers pris en charge, consultez la section [Informations complémentaires sur Document Security](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-security/document-security-offerings.html?lang=fr).

Avec Document Security, vous pouvez facilement créer, stocker et appliquer des paramètres de confidentialité prédéfinis à vos documents. Pour empêcher toute diffusion incontrôlée d’informations, vous pouvez également vérifier et contrôler la façon dont les destinataires et destinatrices utilisent les documents que vous leur avez distribués.

Vous pouvez protéger les documents à l’aide de politiques. Une *politique* est un groupe d’informations comprenant des paramètres de confidentialité et une liste d’utilisateurs et utilisatrices autorisés. Les paramètres de confidentialité que vous spécifiez dans une politique déterminent la mesure dans laquelle un destinataire ou une destinatrice peut utiliser un document auquel vous appliquez cette politique. Par exemple, vous pouvez spécifier si les destinataires et destinatrices sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés.

Les utilisateurs et utilisatrices de Document Security créent des politiques à l’aide de pages Web destinées aux utilisateurs et utilisatrices finaux. Les administrateurs et administratrices utilisent les pages Web de Document Security pour créer des jeux de politiques contenant des politiques partagées, accessibles à tous les utilisateurs et utilisatrices autorisés.

Bien que les politiques soient stockées dans Document Security, vous les appliquez aux documents par le biais de votre application cliente. Les modalités d’application des politiques aux documents PDF sont décrites en détail dans l’*Aide d’Acrobat*. L’application de politiques à l’aide d’autres applications, telles que Microsoft® Office, est décrite dans l’*Aide des extensions Acrobat Reader DC* de l’application.

Lorsque vous appliquez une politique à un document, les paramètres de confidentialité spécifiés dans la politique protègent les informations que le document contient. Les paramètres de confidentialité protègent également tout fichier (texte, audio ou vidéo) contenu dans un document PDF. Vous pouvez distribuer le document protégé par une politique aux destinataires et destinatrices autorisés par la politique.

**Contrôle d’accès aux documents et vérification des documents**

En utilisant une politique pour protéger un document, vous maintenez un contrôle continu sur le document, même après sa distribution. Vous pouvez contrôler le document, modifier la politique, empêcher des utilisateurs et utilisatrices d’accéder au document et changer la politique appliquée au document.

Grâce à Document Security, vous pouvez contrôler les documents protégés par une politique et assurer le suivi des événements, comme lorsqu’un utilisateur ou une utilisatrice autorisé ou non tente d’ouvrir le document.

**Composants**

Document Security se compose d’un serveur et d’une interface utilisateur :

**Serveur :** composant central par l’intermédiaire duquel Document Security effectue des transactions telles que l’authentification des utilisateurs et utilisatrices, la gestion en temps réel des politiques et l’application de la confidentialité. Le serveur joue également le rôle de référentiel central pour les politiques, les enregistrements d’audit et d’autres informations associées.

**Pages Web :** interface vous permettant de créer des politiques, de gérer vos documents protégés par une politique et de contrôler les événements associés aux documents protégés par une politique. Les administrateurs et administratrices peuvent également configurer des options globales, telles que l’authentification des utilisateurs et utilisatrices, la vérification et l’envoi de messages aux utilisateurs et utilisatrices invités et la gestion des comptes d’utilisateurs invités.

![rm_psworkflow](assets/rm_psworkflow.png)

Étapes représentées dans le schéma :

1. Le ou la propriétaire du document crée des politiques à l’aide des pages Web. Les propriétaires de documents peuvent créer des politiques personnelles auxquelles ils sont les seuls à avoir accès. Les administrateurs et administratrices et les coordinateurs et coordinatrices de jeux de politiques peuvent créer des politiques partagées dans les jeux de politiques qui sont accessibles aux utilisateurs et utilisatrices autorisés.
1. Le ou la propriétaire du document applique la politique, puis enregistre et diffuse le document. Le document peut être distribué par e-mail, via un dossier réseau ou sur un site Web.
1. Le destinataire ou la destinatrice ouvre le document dans l’application cliente appropriée. Il ou elle peut utiliser le document conformément à sa politique.
1. Le ou la propriétaire du document, le coordinateur ou la coordinatrice de jeux de politiques ou l’administrateur ou l’administratrice peut suivre les documents et modifier l’accès à ces derniers à l’aide des pages Web.

## À propos des utilisateurs et utilisatrices de Document Security {#about-document-security-users}

Divers types d’utilisateurs et utilisatrices recourent à Document Security pour accomplir différentes tâches :

* L’administrateur ou administratrice système ou un informaticien ou une informaticienne installe et configure Document Security. Cette personne peut également être chargée de la configuration des paramètres généraux du serveur, des pages Web, des politiques et des documents.

  Ces options peuvent notamment inclure l’URL de base de Document Security, les notifications de contrôle et de confidentialité, les notifications d’enregistrement des utilisateurs et utilisatrices invités et les périodes d’ouverture hors connexion par défaut.

* Les administrateurs et administratrices de Document Security créent des politiques et des jeux de politiques, et gèrent les documents protégés par une politique pour les utilisateurs et utilisatrices, selon les besoins. Ils et elles créent également des comptes d’utilisateur ou utilisatrice invité et contrôlent les événements concernant le système, les documents, les utilisateurs et utilisatrices, les politiques, les jeux de politiques, ainsi que les événements personnalisés. Ils et elles peuvent également être responsables de la configuration des paramètres généraux du serveur, des pages Web et des politiques, avec un administrateur ou une administratrice système.

  Les administrateurs et administratrices peuvent affecter les rôles ci-après aux utilisateurs et utilisatrices dans la zone User Management de la console d’administration. Les utilisateurs et utilisatrices dotés de ces rôles exécutent leurs tâches dans la zone de l’interface utilisateur Document Security de la console d’administration.

  **Super-administrateur ou administratrice de Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle ont accès à tous les paramètres Document Security dans la console d’administration. Ces autorisations sont associées au rôle :

   * Gestion de la configuration
   * Gestion de la politique
   * Gestion des jeux de politiques
   * Gestion des documents
   * Gestion des éditeurs et éditrices
   * Gestion des utilisateurs et utilisatrices invités et locaux
   * Affichage des événements
   * Déléguer
   * Invitation d’utilisateurs et utilisatrices externes

  **Administrateur ou administratrice de Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle peuvent configurer le serveur Document Security à l’aide de la page Configuration de la section Document Security de la console d’administration. Cette autorisation est associée au rôle Gestion de la configuration.

  >[!NOTE]
  >
  >Les utilisateurs et utilisatrices bénéficiant de ce rôle doivent également disposer du rôle Utilisateur de la console d’administration pour être à même de se connecter à la console et de modifier les paramètres relatifs à la configuration.

  **Administrateur ou administratrice de jeux de politiques Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle peuvent utiliser la section Document Security de la console d’administration pour modifier d’autres politiques d’utilisateurs et utilisatrices ainsi que pour créer, modifier et supprimer des jeux de politiques. Lorsqu’un administrateur ou une administratrice de jeux de politiques crée un jeu de politiques, il ou elle peut affecter un coordinateur ou une coordinatrice à ce jeu de politiques. Ces autorisations sont associées au rôle :

   * Gestion de la politique
   * Gestion des jeux de politiques
   * Gestion des documents
   * Gestion des éditeurs et éditrices
   * Affichage des événements
   * Déléguer

  >[!NOTE]
  >
  >Les utilisateurs et utilisatrices bénéficiant de ce rôle doivent également disposer du rôle Utilisateur de la console d’administration pour être à même de se connecter à la console et de modifier les paramètres relatifs à la configuration.

  **Gestion des utilisateurs invités et locaux Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle peuvent exécuter les tâches requises pour gérer l’ensemble des utilisateurs et utilisatrices invités et locaux dans les pages Web Document Security appropriées. Ces autorisations sont associées au rôle :

   * Gestion des utilisateurs et utilisatrices invités et locaux
   * Invitation d’utilisateurs et utilisatrices externes
   * Accès aux pages Web destinées aux utilisateurs et utilisatrices finaux

  >[!NOTE]
  >
  >Les utilisateurs et utilisatrices bénéficiant de ce rôle doivent également disposer du rôle Utilisateur de la console d’administration pour être à même de se connecter à la console et de modifier les paramètres relatifs à la configuration.

  **Invitation d’un utilisateur ou d’une utilisatrice de Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle peuvent inviter des utilisateurs et utilisatrices. Ces autorisations sont associées au rôle :

   * Invitation d’utilisateurs et utilisatrices externes
   * Accès aux pages Web destinées aux utilisateurs et utilisatrices finaux

  **Utilisateur ou utilisatrice final de Document Security**

  Les utilisateurs et utilisatrices bénéficiant de ce rôle peuvent accéder aux pages Web Document Security destinées aux utilisateurs et utilisatrices finaux. Ce rôle peut également être attribué aux administrateurs et administratrices pour leur permettre de créer des politiques à l’aide des pages destinées aux utilisateurs et utilisatrices finaux. Cette autorisation est associée au rôle avec le rôle Accès aux pages Web destinées aux utilisateurs et utilisatrices finaux.

* Les utilisateurs et utilisatrices de l’entreprise qui possèdent des comptes Document Security valides créent leurs propres politiques et utilisent des politiques pour protéger des documents, contrôler et gérer leurs documents protégés par une politique et contrôler les événements concernant leurs documents.
* Les coordinateurs et coordinatrices de jeux de politiques gèrent les documents, affichent les événements et gèrent d’autres coordinateurs et coordinatrices de jeux de politiques (selon leurs autorisations). Les administrateurs et administratrices désignent, parmi les utilisateurs et utilisatrices, des coordinateurs et coordinatrices pour certains jeux de politiques.
* Les utilisateurs et utilisatrices externes à l’entreprise (partenaires commerciaux, par exemple) peuvent utiliser les documents protégés par une politique s’ils et elles figurent dans l’annuaire de Document Security, si l’administrateur ou l’administratrice leur crée un compte ou s’ils et elles s’enregistrent dans Document Security par l’intermédiaire d’un processus automatisé d’invitation par e-mail. Selon le mode choisi par l’administrateur ou l’administratrice pour activer les paramètres d’accès, les utilisateurs et utilisatrices invités peuvent également être autorisés à appliquer des politiques à des documents, à créer, modifier et supprimer leurs politiques, et à inviter d’autres utilisateurs et utilisatrices externes à utiliser leurs documents protégés par une politique.
* Les développeurs utilisent le SDK d’AEM Forms pour intégrer des applications personnalisées à Document Security.

Les administrateurs et administratrices de Document Security peuvent créer des rôles personnalisés à l’aide des autorisations ci-après dans User Management :

* Gestion de la configuration de Document Security
* Gestion des utilisateurs et utilisatrices invités et locaux de Document Security
* Gestion des jeux de politiques Document Security
* Gestion des jeux de politiques Document Security
* Affichage des événements du serveur Document Security
* Modification du ou de la propriétaire d’une politique Document Security

## Politiques et documents protégés par une politique {#policies-and-policy-protected-documents}

Une *politique* définit un jeu de paramètres de confidentialité et les utilisateurs et utilisatrices habilités à accéder au document auquel la politique est appliquée. De plus, une politique permet de modifier dynamiquement les autorisations sur un document. Elle permet à la personne qui sécurise le document de modifier les paramètres de confidentialité, de révoquer l’accès au document ou de changer de politique.

La protection d’une politique peut être appliquée à un document PDF à l’aide d’Acrobat® Pro et d’Adobe Acrobat Standard. La protection de politique peut également être appliquée à d’autres types de fichiers, tels que Microsoft® Word, Excel et PowerPoint par le biais de l’application cliente, à condition que les Extensions Acrobat Reader DC appropriées soient installées.

### Fonctionnement des politiques {#how-policies-work}

Les politiques contiennent des informations sur les utilisateurs et utilisatrices autorisés et les paramètres de confidentialité à appliquer aux documents. Les utilisateurs et utilisatrices peuvent être des membres de votre entreprise, ainsi que des personnes extérieures qui possèdent un compte. Si l’administrateur ou administratrice active la fonction d’invitation d’utilisateur ou utilisatrice, il est même possible d’ajouter de nouveaux utilisateurs ou utilisatrices aux politiques et de déclencher le processus d’envoi par e-mail d’une invitation à l’enregistrement.

Les paramètres de confidentialité d’une politique déterminent dans quelle mesure les destinataires et destinatrices peuvent utiliser le document. Par exemple, vous pouvez spécifier si les destinataires et destinatrices sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés. Une même politique peut également spécifier différents paramètres de confidentialité pour des utilisateurs et utilisatrices spécifiques.

>[!NOTE]
>
>Les paramètres de confidentialité appliqués par l’intermédiaire d’une politique ont priorité sur ceux qui peuvent avoir été appliqués à un document PDF dans Acrobat en utilisant les options de mot de passe ou de certificat. (Voir l’aide d’Acrobat pour plus d’informations).

Les utilisateurs et utilisatrices et les administrateurs et administratrices créent des politiques par l’intermédiaire des pages Web de Document Security. Une seule politique à la fois peut être appliquée à un document. Les deux méthodes suivantes permettent d’appliquer une politique :

* Ouvrez le document dans Acrobat ou une autre application cliente et sélectionnez une politique pour protéger le document.
* Envoyez un document en tant que pièce jointe d’un courrier électronique dans Microsoft Outlook. Dans ce cas, vous pouvez sélectionner une politique dans la liste des politiques. Ou, vous pouvez choisir une politique générée automatiquement et créée par Acrobat avec un jeu de paramètres de confidentialité par défaut afin de ne protéger le document que pour les destinataires et destinatrices de l’e-mail.

Vous pouvez supprimer une politique d’un document à l’aide de l’application cliente.

![rm_psonline_policy](assets/rm_psonline_policy.png)

Les étapes du diagramme sont les suivantes :

1. Le ou la propriétaire du document sécurise le document à partir d’une application cliente prise en charge avec une politique qui autorise l’utilisation en ligne.
1. Document Security crée une licence de document ainsi que des clés de document, et chiffre la politique. La licence de document, la politique chiffrée et la clé du document sont renvoyées à l’application cliente.
1. Le document est chiffré avec la clé du document et cette dernière est abandonnée. Le document intègre alors la licence et la politique. Ces tâches sont effectuées dans l’application cliente prise en charge.

Lorsque vous appliquez une politique à un document, les informations contenues dans le document, dont les fichiers (texte, audio ou vidéo) enregistrés dans le document PDF, sont protégées par les paramètres de confidentialité spécifiés dans la politique. Document Security génère une licence et des informations de chiffrement qui sont ensuite intégrées dans le document. Lorsque vous distribuez le document, Document Security peut authentifier les destinataires et destinatrices qui tentent d’ouvrir le document et autoriser l’accès en fonction des privilèges spécifiés dans la politique.

Si l’utilisation hors ligne est autorisée, les destinataires et destinatrices peuvent également utiliser hors connexion (sans être connectés à Internet ou au réseau) des documents protégés par une politique, pendant la période spécifiée dans la politique.

### Fonctionnement des documents protégés par une politique {#how-policy-protected-documents-work}

Pour ouvrir et utiliser des documents protégés par une politique, cette dernière doit inclure votre nom en tant que destinataire ou destinatrice et vous devez disposer d’un compte Document Security valide. Pour les documents PDF, vous avez besoin d’Acrobat ou d’Adobe Reader®. Pour les autres types de fichiers, vous devez disposer de l’application voulue et des extensions Acrobat Reader DC déjà installées.

Lorsque vous tentez d’ouvrir un document protégé par une politique, Acrobat, Adobe Reader ou les extensions Acrobat Reader DC se connectent à Document Security pour vous authentifier. Vous pouvez ensuite vous connecter. Si l’utilisation du document fait l’objet d’un audit, un message de notification s’affiche. Une fois que Document Security a déterminé les autorisations à accorder, il gère le déchiffrement du document. Vous pouvez ensuite utiliser le document en fonction des paramètres de confidentialité de la politique.

![rm_psopen_online](assets/rm_psopen_online.png)

Les étapes du diagramme sont les suivantes :

1. L’utilisateur ou l’utilisatrice du document ouvre le document dans une application cliente prise en charge et s’authentifie auprès du serveur. L’identifiant du document est envoyé au serveur Document Security.
1. Document Security authentifie les utilisateurs et utilisatrices, vérifie les autorisations de la politique et crée un bon. Le bon (qui contient la clé de document et les autorisations) est renvoyé à l’application cliente.
1. Le document est déchiffré à l’aide de la clé de document et celle-ci est ignorée. Le document peut ensuite être utilisé conformément aux paramètres de confidentialité de la politique. Ces tâches sont effectuées dans l’application cliente prise en charge.

Vous pouvez continuer à utiliser un document dans les conditions suivantes :

* indéfiniment ou pendant la période de validité spécifiée dans la politique ;
* jusqu’à ce que l’administrateur/administratrice ou la personne ayant appliqué la politique révoque l’accès au fichier ou modifie la politique.

Vous pouvez également utiliser hors ligne (sans connexion Internet ou réseau) des documents protégés par une politique, dans la mesure où la politique autorise l’accès hors ligne. Connectez-vous d’abord à Document Security pour synchroniser le document. Vous pouvez ensuite utiliser le document pendant la période d’ouverture hors connexion spécifiée dans la politique.

Une fois la période d’ouverture hors connexion terminée, resynchronisez le document avec Document Security, soit en le mettant en ligne et en ouvrant un document protégé par une politique, soit en utilisant une commande dans l’application cliente. (Pour plus dʼinformations, consultez l’*Aide d’Acrobat* ou l’*Aide des extensions Acrobat Reader DC* appropriée).

Si vous enregistrez une copie d’un document protégé par une politique à l’aide de la commande de menu Enregistrer ou Enregistrer sous, la politique est automatiquement appliquée au nouveau document. Les événements tels que les tentatives d’ouverture du nouveau fichier sont également contrôlés et enregistrés pour le document d’origine.

## Jeux de politiques {#policy-sets}

Les *jeux de politiques* regroupent plusieurs politiques ayant une finalité commune. Ces jeux de politiques sont ensuite rendus accessibles à un sous-ensemble d’utilisateurs et utilisatrices du système.

Chaque jeu de politiques peut être associé à un ou plusieurs coordinateurs et coordinatrices de jeux de politiques. Le coordinateur de jeux de politiques est un administrateur ou un utilisateur possédant des autorisations supplémentaires. Au sein de l’organisation, *le coordinateur/la coordinatrice de jeux de politiques* est généralement la personne la plus à même de créer des politiques dans un jeu donné.

Les coordinateurs et coordinatrices de jeux de politiques peuvent effectuer les tâches suivantes :

* Créer des politiques
* Modifier et supprimer une politique dans le jeu de politiques
* Modifier des paramètres de jeux de politiques
* Ajouter et supprimer des coordinateurs de jeux de politiques
* Afficher des événements de politique et de document pour n’importe quel document ou politique du jeu de politiques
* Révoquer l’accès aux documents
* Changer de politiques pour le document

>[!NOTE]
>
>Vous pouvez récupérer un maximum de 1 000 noms de jeux de politiques dans la base de données à l’aide d’API `getAllPolicysetnames()`.

Les jeux de politiques sont créés et supprimés dans les pages web d’administration de Document Security par les administrateurs et administratrices et les coordinateurs et coordinatrices de jeux de politiques bénéficiant des autorisations requises.

Les jeux de politiques sont généralement rendus accessibles à un nombre limité d’utilisateurs et d’utilisatrices, en spécifiant quels utilisateurs et utilisatrices et groupes d’un domaine sont autorisés à se servir des politiques du jeu de politiques défini pour protéger des documents.

L’installation de Document Security crée un jeu de politiques par défaut appelé *Jeu de politiques global*. L’administrateur ou l’administratrice qui a installé le logiciel gère ce jeu de politiques.

## Bonnes pratiques {#best-practices}

Les politiques sont des jeux réutilisables d’autorisations et de groupes d’utilisateurs qui peuvent être appliqués à divers documents. Pour les documents protégés. Ces politiques garantissent que seuls les utilisateurs autorisés peuvent utiliser les fonctionnalités spécifiées. En règle générale, le nombre de politiques sʼaccroît et reflète lʼaugmentation des différents rôles dʼutilisateurs et des documents au sein d’un même service. Pour créer et gérer des politiques, voici quelques considérations et bonnes pratiques :

* **Créer des politiques réutilisables :** Adobe recommande de réutiliser les politiques dans plusieurs documents. Cela permet de réduire au maximum le nombre de politiques, d’offrir des performances optimales et de faciliter la gestion des politiques. Pour créer une politique réutilisable, procédez comme suit :

1. Identifiez et définissez les exigences en matière de contrôle d’accès au niveau des services et de l’organisation.

1. Créez des groupes d’utilisateurs et ajoutez des utilisateurs à ces groupes.

1. Création d’un jeu de politiques.

1. Ouvrez le jeu de politiques et créez une politique. Ajoutez des groupes d’utilisateurs et définissez les paramètres de confidentialité (contrôle d’accès) pour la politique.

Ajoutez des groupes dʼutilisateurs aux politiques au lieu dʼutilisateurs individuels. Cela facilite la gestion et l’application des politiques à de nombreux utilisateurs et utilisatrices.

* **Créer des jeux de politiques personnalisés :** un jeu de politiques combine plusieurs politiques en une entité gérable. Créez des jeux de politiques personnalisés pour votre organisation ou votre service, utilisez-les pour regrouper les politiques connexes et mettez-les à la disposition dʼun sous-ensemble d’utilisateurs du système.

  Grâce aux jeux de politiques, l’affectation et la gestion de politiques connexes à des utilisateurs spécifiques d’une organisation ou d’un service est plus facile. Par exemple, des jeux de politiques distincts pour le service des finances et celui des ressources humaines peuvent faciliter la gestion et l’application de politiques connexes aux documents destinés aux services correspondants.

* **Utiliser un agent d’autorisation externe pour appliquer les autorisations de manière dynamique :** vous pouvez utiliser un [agent d’autorisation externe](https://help.adobe.com/fr_FR/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html) pour évaluer et appliquer dynamiquement les autorisations en fonction de conditions externes. Lorsque les autorisations sont évaluées de manière dynamique, en fonction de conditions externes, les actions suivantes sont disponibles :

   * Assurez un contrôle dʼaccès centralisé aux documents de votre organisation.

   * Contrôlez l’accès aux documents protégés par une politique en déterminant de manière dynamique si un utilisateur peut accéder à un document protégé par une politique. Par exemple, décidez de manière dynamique si un utilisateur peut imprimer un document protégé par une politique.

   * Utilisez un mécanisme de contrôle d’accès que votre système de gestion de contenu utilise, en plus du processus standard d’évaluation des politiques. Par exemple, lorsque le service détermine si un utilisateur ou une utilisatrice peut imprimer un document protégé par une politique, il peut utiliser le processus d’évaluation de politique standard. Il peut également utiliser le mécanisme de contrôle d’accès utilisé par votre système de gestion de contenu.

  Bien qu’il soit possible de remplacer complètement le processus d’évaluation des politiques de Document Security par un gestionnaire d’autorisation externe, il est recommandé d’utiliser le processus d’évaluation des politiques en plus dʼun gestionnaire d’autorisation externe. De cette façon, l’accès aux documents peut être contrôlé par le même mécanisme de contrôle que celui utilisé par votre système de gestion de contenu. Par exemple, lorsque le service Document Security détermine si un utilisateur ou une utilisatrice peut imprimer un document protégé par une politique, il utilise le processus d’évaluation de politique standard. Il utilise également le mécanisme de contrôle d’accès utilisé par votre système de gestion de contenu. Pour plus d’informations, consultez la section [Créer des gestionnaires d’autorisation externes](https://help.adobe.com/fr_FR/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html).

* **Réduire les jeux de politiques à un nombre limité :** lʼaugmentation constante des politiques et des jeux de politiques est imputable à de nombreux facteurs. Les plus courants sont les suivants :

   * Augmentation des rôles utilisateur, des services et des documents au sein d’une organisation sur une période donnée.
   * Les services dʼune organisation travaillent de manière autonome et exercent un contrôle strict sur les politiques qui leur sont propres. Cela conduit à des politiques identiques au sein d’une organisation.

  Adobe recommande de limiter au maximum le nombre de politiques et de jeux de politiques. Cela permet de gérer plus facilement les politiques et les jeux de politiques et d’offrir de meilleures performances. Pour réduire au maximum le nombre de stratégies, procédez comme suit :

   * Créez des politiques réutilisables. Elles peuvent être partagées dans plusieurs services.
   * Pensez à créer des jeux de politiques à l’échelle de l’organisation. Au lieu de créer un jeu de politiques individuel pour chaque service, créez des politiques qui s’appliquent à plusieurs services.
   * Regroupez les politiques liées dans un jeu de politiques. Ne créez pas de jeu de politiques distinct pour chaque politique.
   * Utilisez un agent d’autorisation externe pour contrôler de manière dynamique les autorisations utilisateur.

  >[!NOTE]
  >
  >Vous pouvez utiliser lʼAPI [getAllPolicysetnames()](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/PolicyManager.html) pour récupérer, au maximum, 1 000 noms de jeux de politiques. En interne, l’API récupère un maximum de 1 000 politiques pour lesquelles le demandeur de l’API dispose de l’autorisation d’éditeur de document, puis crée et renvoie une liste de noms de jeux de politiques uniques associés aux politiques récupérées. Par exemple, lorsque l’API récupère 1 000 politiques et que les politiques récupérées sont associées à 200 jeux de politiques au total, l’API renvoie uniquement 200 noms de jeux de politiques.
