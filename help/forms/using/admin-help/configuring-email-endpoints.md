---
title: Configuration des points de fin de courrier électronique
seo-title: Configuration des points de fin de courrier électronique
description: Découvrez comment configurer les points de fin de courrier électronique.
seo-description: Découvrez comment configurer les points de fin de courrier électronique.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '3766'
ht-degree: 60%

---


# Configuration des points de fin de courrier électronique {#configuring-email-endpoints}

Les points de fin de courrier électronique permettent à un utilisateur d’appeler un service en envoyant un ou plusieurs documents (en tant que pièces jointes de courrier électronique) à un compte de messagerie spécifié. La boîte de réception du courrier électronique collecte les pièces jointes. Le service contrôle la boîte de réception et traite les pièces jointes. Le résultat de la conversion est transmis à l’utilisateur désigné dans le point de fin.

Avec un point de fin de courrier électronique, les utilisateurs autorisés peuvent lancer un processus en envoyant des fichiers au compte approprié. Les résultats sont renvoyés à l’expéditeur (par défaut) ou à l’utilisateur défini dans les paramètres du point de fin.

Avant de configurer un point de fin de courrier électronique, créez un compte de messagerie POP3 ou IMAP qui sera utilisé par le point de fin. Créez un compte distinct pour chaque type de conversion. Par exemple, vous pouvez configurer un compte pour la création de documents PDF standard à partir des fichiers reçus en pièce jointe, et un autre compte pour la création de documents PDF sécurisés.

>[!NOTE]
>
>chaque adresse électronique doit correspondre à un seul point de fin de courrier électronique. Vous ne pouvez pas configurer plusieurs points de fin de courrier électronique sur une seule adresse de messagerie, même si les points de fin supplémentaires de courrier électronique sont désactivés.

Tous les points de fin de courrier électronique sont configurés avec un nom d’utilisateur et un mot de passe, qui sont requis pour exécuter le service. Le compte de courrier électronique est protégé par le serveur de messagerie sur lequel il est configuré.

Si vos utilisateurs envoient des documents avec des caractères d’Europe occidentale dans des noms de fichier et de chemin de conversion, ils doivent utiliser une application de messagerie qui prend en charge les types de codage requis (Latin1 [ISO-8859-1], Western European [Windows] ou UTF-8). Pour plus d’informations, consultez le document *Installation et déploiement d&#39;AEM forms* correspondant à votre serveur d’applications.

Avant de configurer un point de fin de courrier électronique, configurez le service Email. Voir [Configuration des paramètres par défaut des points de fin du courrier électronique](configuring-email-endpoints.md#configure-default-email-endpoint-settings). Les paramètres de configuration du service Email ont deux objectifs :

* configurer les attributs communs à tous les points de fin de courrier électronique ;
* fournir des valeurs par défaut à tous les points de fin de courrier électronique.

## Configuration de SSL sur un point de fin de courrier électronique  {#configure-ssl-for-an-email-endpoint}

Vous pouvez configurer les paramètres POP3, IMAP ou SMTP pour utiliser SSL (Secure Sockets Layer) sur un point de fin de courrier électronique.

1. Sur le serveur de messagerie, activez SSL pour POP3, IMAP ou SMTP, en vous reportant à la documentation de l’éditeur du logiciel.
1. Exportez un certificat de client depuis le serveur de courrier électronique.
1. Utilisez le programme keytool pour importer le fichier du certificat client dans le de stock des certificats Java Virtual Machine (JVM) du serveur d’applications. La marche à suivre pour cette étape varie selon la version de la JVM installée et les chemins d’installation du client.

   Par exemple, si vous utilisez une installation Oracle WebLogic Server par défaut avec JDK 1.5.0 sous Microsoft Windows Server® 2003, saisissez la commande suivante après une invite de commande :

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. A l’invite, spécifiez votre mot de passe (pour Java, le mot de passe par défaut est « `changeit` »). Une fois le certificat importé, un message vous est envoyé confirmant la réussite de l’opération.
1. Ajoutez un point de fin de courrier électronique au service à l’aide d’Administration Console.
1. Créez le point de fin de courrier électronique dans Administration Console. Lors de la configuration des paramètres d’un point de fin, sélectionnez SSL POP3/IMAP activé pour les messages entrants et SSL SMTP activé pour les messages sortants, puis modifiez les propriétés de port en conséquence.

>[!NOTE]
>
>Conseil : si vous rencontrez des problèmes pour utiliser SSL, vérifiez qu’un client de courrier électronique tel que Microsoft Outlook a accès au serveur de courrier électronique à l’aide de SSL. Si le client de courrier électronique ne parvient pas à accéder au serveur de courrier électronique, le problème tient à la configuration du certificat ou du serveur de courrier électronique.

## Configuration des paramètres par défaut des points de fin du courrier électronique  {#configure-default-email-endpoint-settings}

Vous pouvez utiliser la page Gestion des services pour configurer des attributs communs à tous les points de fin de courrier électronique et fournir des valeurs par défaut pour tous ces points de fin.

Pour que le processus des formulaires reçoive et traite les courriers électroniques entrants envoyés par des utilisateurs, vous devez créer un point de fin de courrier électronique pour le service Complete Task. Ce point de fin de courrier électronique exige des paramètres supplémentaires, décrits dans [Création d’un point de fin de courrier électronique pour le service Complete Task](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Modification des valeurs par défaut pour tous les points de fin de courrier électronique  {#change-the-default-values-for-email-endpoints}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, cliquez sur Email: 1.0 (l’ID de composant est com.adobe.idp.dsc.provider.service.email.Email).
1. Dans l’onglet Configuration, spécifiez les paramètres par défaut des points de fin de courrier électronique et cliquez sur Enregistrer.

### Paramètres par défaut des points de fin de courrier électronique  {#default-email-endpoint-settings}

**Expression cron :** expression cron utilisée par quartz pour planifier l’interrogation du répertoire d’entrée.

**Intervalle de répétition :** nombre de répétitions de l’interrogation d’annuaire. L’intervalle de répétition par défaut est exprimé en secondes si cette valeur n’est pas spécifiée dans la configuration des points de fin. La valeur par défaut est 10. Cette valeur ne peut pas être inférieure à 10.

**Nombre de répétitions :** nombre de fois où le répertoire d’entrée est interrogé. Nombre de répétitions par défaut à utiliser si cette valeur n’est pas spécifiée dans la configuration des points de fin. La valeur -1 indique une analyse indéfinie du répertoire. La valeur par défaut est -1.

**Délai d’analyse des débuts de la tâche : valeur par défaut, en secondes, du délai avant que le début de la tâche n’analyse le point de terminaison.** La valeur par défaut est 0.

**Taille du lot :** nombre de messages électroniques que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 désigne tous les messages électroniques. La valeur par défaut est 2.

**Asynchrone :** identifie le type d’appel comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est asynchrone.

**Modèle de domaine : modèle** de nom de domaine utilisé pour filtrer les courriers électroniques entrants. Par exemple, si le domaine adobe.com est utilisé, seuls les messages électroniques de ce domaine sont traités ; ceux provenant d’autres domaines sont ignorés.

**Modèle de fichier :** modèles de pièces jointes entrantes que le fournisseur accepte. Cela inclut les fichiers qui comportent des extensions spécifiques (&amp;amp ; ast ; .dat, &amp;amp ; ast ; .xml), des noms spécifiques (data) et des expressions composites dans le nom et l’extension (.[dD][aA]&#39;port&#39;). La valeur par défaut est &amp;ast;.&amp;ast;.

**Destinataires de la tâche réussie :** une ou plusieurs adresses électroniques utilisées pour envoyer des courriers électroniques afin d’indiquer les tâches réussies. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur du travail d’origine. Jusqu’à 100 destinataires sont pris en charge. Pour désactiver ce paramètre, ne renseignez pas ce champ.

**Destinataires de la tâche en échec :** une ou plusieurs adresses électroniques utilisées pour envoyer des courriers électroniques afin d’indiquer les tâches ayant échoué. Par défaut, un message de travail ayant échoué est toujours envoyé à l’expéditeur du travail d’origine. Jusqu’à 100 destinataires sont pris en charge. Pour désactiver ce paramètre, ne renseignez pas ce champ.

**Hôte de la boîte de réception :** nom d’hôte de la boîte de réception ou adresse IP du fournisseur de messagerie électronique à analyser.

**Port de boîte de réception :** numéro de port de boîte de réception que le fournisseur de messagerie électronique doit analyser. Avec la valeur 0, le port IMAP ou POP3 par défaut est utilisé.

**Protocole de boîte de réception : protocole** de messagerie que le point de terminaison de courrier électronique doit utiliser pour analyser la boîte de réception. Les protocoles proposés sont les protocoles IMAP ou POP3. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.

**Délai d’expiration de la boîte de réception :** indique le délai d’attente du point de terminaison avant l’annulation lors de la tentative de connexion à la boîte de réception. Si une connexion n’est pas établie avant que cette valeur ne soit atteinte, la boîte de réception n’est pas interrogée.

**Utilisateur de la boîte de réception :** nom d’utilisateur requis pour se connecter au compte de messagerie. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’adresse électronique ou de l’adresse électronique complète.

**Mot de passe de la boîte de réception :** mot de passe de l’utilisateur de la boîte de réception.

**SSL POP3/IMAP activé :** lorsqu’il est sélectionné, SSL est activé.

**Hôte SMTP : nom d’hôte** du serveur de messagerie que le fournisseur de messagerie électronique utilise pour envoyer les résultats et les messages d’erreur. Par exemple, mail.corp.exemple.com.

**Port SMTP : port** utilisé pour la connexion au serveur de messagerie. La valeur par défaut est 25.

**Utilisateur SMTP : compte utilisateur** que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie un courrier électronique pour signaler des résultats et des erreurs.

**Mot de passe SMTP :** mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.

**Envoyer depuis :** adresse électronique (par exemple, user@company.com) utilisée pour envoyer des notifications par courrier électronique des résultats et des erreurs. Si vous n’indiquez pas de valeur pour l’élément De, le serveur de messagerie tentera de déterminer l’adresse électronique en combinant la valeur spécifiée dans le paramètre Utilisateur SMTP avec un domaine par défaut configuré sur le serveur de messagerie. Si votre serveur de messagerie n’a pas de domaine par défaut et que vous n’indiquez pas de valeur pour l’élément De, des erreurs peuvent se produire. Pour vous assurer que les courriers électroniques auront la bonne adresse d’envoi De, indiquez une valeur pour le paramètre De.

**SSL SMTP activé :** lorsque cette option est sélectionnée, SSL sur SMTP est activé.

**Inclure le corps du message d’origine comme pièce jointe :** Par défaut, lorsque vous envoyez un message électronique au serveur Forms, le texte original du message est inclus dans le corps du message. Pour inclure ce texte en pièce jointe à la place, sélectionnez cette option.

**Utiliser la ligne d’objet d’origine pour les messages électroniques de résultats :** Par défaut, le serveur Forms utilise les valeurs spécifiées dans les paramètres Objet du message de réussite et Objet du message d’erreur comme ligne d’objet lors de l’envoi des messages électroniques de résultat. Pour que l’objet des messages électroniques de résultat soit le même que l’objet du message électronique original envoyé au serveur, sélectionnez cette option.

**Sujet du message électronique de réussite :** après avoir envoyé un message électronique à un point de terminaison de courrier électronique au début ou si vous avez poursuivi le processus, vous recevez un message électronique de retour du serveur AEM forms. Si votre message électronique est fructueux, vous recevez un message de réussite. Si votre message électronique échoue, vous recevez un message d’erreur expliquant les raisons de cet échec. Ce paramètre vous permet de spécifier l’objet d’un message électronique de réussite envoyé pour ce point de fin.

**Corps du message électronique de réussite :** permet de spécifier le corps du texte des messages électroniques de réussite envoyés pour ce point de terminaison.

**Error Email Subject Prefix :** permet de spécifier le texte utilisé au début de l’objet des messages électroniques d’erreur envoyés pour ce point de terminaison.

**Objet du message d’erreur :** permet de spécifier l’objet des messages électroniques d’erreur envoyés pour ce point de terminaison. Ce texte est affichée après le préfixe de l’objet des messages électroniques d’erreur.

**Corps du message d’erreur :** permet de spécifier la première ligne du corps du texte des messages électroniques d’erreur envoyés pour ce point de terminaison.

**Informations de résumé du courrier électronique :** chaque message de réussite ou d’échec comprend une section contenant le texte du message électronique d’origine que vous avez envoyé au serveur Forms. Ce paramètre spécifie le texte qui apparaît au-dessus cette section.

**Valider la boîte de réception avant de créer/mettre à jour ce point de terminaison :** lorsque cette option est sélectionnée, le serveur Forms vérifie si vos paramètres SMTP/POP3 sont corrects avant de créer le point de terminaison. Lorsque vous cliquez sur Ajouter, un message s’affiche pour indiquer si le compte de boîte de réception est valide ou non. Si cette option n’est pas sélectionnée, le serveur AEM forms crée le point de fin, sans vérifier la validité du compte de boîte de réception.

**Encodage du jeu de caractères :** format de codage à utiliser pour le message électronique. Le format par défaut UTF-8 est utilisé par la plupart des utilisateurs, exception faite du Japon. Les utilisateurs d’un environnement japonais utilisent généralement le format ISO2022-JP.

**Echec de l’envoi du dossier de courrier électronique :** indique un répertoire dans lequel stocker les résultats si le serveur de messagerie SMTP n’est pas opérationnel.

## Paramètres des points de fin de courrier électronique {#email-endpoint-settings}

Définissez les paramètres suivants pour configurer un point de fin de courrier électronique.

**Nom : paramètre obligatoire** qui identifie le point de terminaison. N’incluez pas de caractère&lt;, car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point de fin, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**Description : description** du point de terminaison. N’incluez pas de caractère &lt;, car la description affichée dans Workspace serait tronquée.

**Expression cron :** saisissez une expression cron si le courrier électronique doit être planifié à l’aide d’une expression cron.

**Nombre de répétitions :** nombre de fois où le point de terminaison du courrier électronique analyse le dossier ou le répertoire. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.

**Intervalle de répétition :** taux d&#39;analyse utilisé par le destinataire pour vérifier le courrier entrant.

**Délai de début de la tâche :** délai d’attente pour l’analyse après les débuts du Planificateur.

**Taille du lot :** nombre de messages électroniques que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 désigne tous les messages électroniques. La valeur par défaut est 2.

**Nom d’utilisateur : paramètre obligatoire** qui correspond au nom d’utilisateur utilisé lors de l’appel d’un service de cible par courrier électronique. La valeur par défaut est SuperAdmin.

**Nom de domaine :** paramètre obligatoire, qui correspond au domaine de l’utilisateur. La valeur par défaut est DefaultDom.

**Modèle de domaine :** indique les modèles de domaine du courrier électronique entrant que le fournisseur accepte. Par exemple, si le domaine adobe.com est utilisé, seuls les messages électroniques de ce domaine sont traités ; ceux provenant d’autres domaines sont ignorés.

**Modèle de fichier :** indique les modèles de pièces jointes entrantes que le fournisseur accepte. Cela inclut les fichiers qui ont des extensions spécifiques (&amp;amp ; ast ; .dat, &amp;amp ; ast ; .xml), des noms spécifiques (data) ou des expressions composites dans le nom et l’extension (&amp;amp ; ast ; .[dD][aA]&#39;port&#39;).

**Destinataires de la tâche réussie :** adresse électronique à laquelle des messages sont envoyés pour indiquer les tâches réussies. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur. Si vous saisissez sender, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires et leurs adresses électroniques en les séparant par des virgules (,).

Pour désactiver ce paramètre, laissez-le vide. Dans certains cas, il se peut que vous souhaitiez déclencher un processus et ne pas recevoir de courrier électronique de notification du résultat.

**Destinataires de la tâche en échec :** adresse électronique à laquelle des messages sont envoyés pour indiquer les tâches ayant échoué. Par défaut, un message de travail ayant échoué est toujours envoyé à l’expéditeur. Si vous saisissez sender, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires et leurs adresses électroniques en les séparant par des virgules (,).

Pour désactiver ce paramètre, laissez-le vide. Dans certains cas, il se peut que vous souhaitiez déclencher un processus et ne pas recevoir de courrier électronique de notification du résultat.

**Hôte de la boîte de réception :** nom d’hôte de la boîte de réception ou adresse IP du fournisseur de messagerie électronique à analyser.

**Port de boîte de réception :** port utilisé par le serveur de messagerie. La valeur POP3 par défaut est 110 et la valeur IMAP par défaut est 143. Si le protocole SSL est activé, la valeur POP3 par défaut est 995 et la valeur IMAP par défaut est 993.

**Protocole de boîte de réception : protocole** de messagerie que le point de terminaison de courrier électronique doit utiliser pour analyser la boîte de réception. Les valeurs proposées sont les protocoles IMAP ou POP3. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.

**Délai d’expiration de** la boîte de réception : délai d’expiration, en secondes, pendant lequel le fournisseur de messagerie électronique attend les réponses de la boîte de réception.

**Utilisateur de la boîte de réception :** nom d’utilisateur requis pour se connecter au compte de messagerie. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’adresse électronique ou de l’adresse électronique complète.

**Mot de passe de la boîte de réception :** mot de passe de l’utilisateur de la boîte de réception.

**SSL POP3/IMAP activé :** sélectionnez ce paramètre pour forcer le fournisseur de messagerie électronique à utiliser SSL pour analyser la boîte de réception. Vérifiez que le serveur de messagerie prend en charge le protocole SSL.

**Hôte SMTP : nom d’hôte** du serveur de messagerie que le fournisseur de messagerie électronique utilise pour envoyer les résultats et les messages d’erreur.

**Port SMTP :** la valeur par défaut du port SMTP est 25.

**Utilisateur SMTP : compte utilisateur** que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie des notifications électroniques de résultats et d’erreurs.

**Mot de passe SMTP :** mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.

**Envoyer depuis :** adresse électronique (par exemple, user@company.com) utilisée pour envoyer des notifications par courrier électronique des résultats et des erreurs. Si vous n’indiquez pas de valeur pour l’élément De, le serveur de messagerie tentera de déterminer l’adresse électronique en combinant la valeur spécifiée dans le paramètre Utilisateur SMTP avec un domaine par défaut configuré sur le serveur de messagerie. Si votre serveur de messagerie n’a pas de domaine par défaut et que vous n’indiquez pas de valeur pour l’élément De, des erreurs peuvent se produire. Pour vous assurer que les courriers électroniques auront la bonne adresse d’envoi De, indiquez une valeur pour le paramètre De.

**SSL SMTP activé :** sélectionnez ce paramètre pour forcer le fournisseur de messagerie électronique à utiliser SSL pour analyser la boîte de réception. Vérifiez que le serveur de messagerie prend en charge le protocole SSL.

**Echec de l’envoi du dossier de courrier électronique :** indique un répertoire dans lequel stocker les résultats si le serveur de messagerie SMTP n’est pas opérationnel.

**asynchrone :** lorsqu’elle est définie sur synchrone, tous les documents d’entrée sont traités et une seule réponse est renvoyée. Lorsque l’option est définie sur asynchrone, une réponse est envoyée pour chaque document traité.

Par exemple, un point de fin de courrier électronique est créé pour un service qui utilise un seul document Word et le renvoie sous forme de fichier PDF. Un message électronique peut être envoyé vers la boîte de réception des points de fin qui contient plusieurs (3) documents Word. Une fois que les trois documents sont traités, si le point de fin est configuré comme étant synchrone, un seul message électronique de réponse est envoyé avec les trois documents joints. Si le point de fin est asynchrone, un message électronique de réponse est envoyé une fois que chaque document Word a été converti en document PDF. Trois messages électroniques sont envoyés avec une pièce jointe au format PDF.

La valeur par défaut est asynchrone.

**Inclure le corps du message électronique d’origine comme pièce jointe :** Par défaut, lorsque vous envoyez un message électronique au serveur Forms, le texte original du message est inclus dans le corps du message. Pour inclure ce texte en pièce jointe à la place, sélectionnez cette option.

**Utiliser l’objet d’origine pour les courriers électroniques de résultats :** Par défaut, le serveur Forms utilise les valeurs spécifiées dans les paramètres Objet du message de réussite et Objet du message d’erreur comme objet lors de l’envoi des messages électroniques de résultats. Pour que l’objet des messages électroniques de résultat soit le même que l’objet du message électronique original envoyé au serveur, sélectionnez cette option.

**Sujet du message électronique de réussite :** après avoir envoyé un message électronique à un point de terminaison de courrier électronique au début ou si vous avez poursuivi le processus, vous recevez un message électronique de retour du serveur AEM forms. Si votre message électronique est fructueux, vous recevez un message de réussite. Si votre message électronique échoue, vous recevez un message d’erreur expliquant les raisons de cet échec. Ce paramètre vous permet de spécifier l’objet d’un message électronique de réussite envoyé pour ce point de fin.

**Corps du message électronique de réussite :** permet de spécifier le corps du texte des messages électroniques de réussite envoyés pour ce point de terminaison.

**Error Email Subject Prefix :** permet de spécifier le texte utilisé au début de l’objet des messages électroniques d’erreur envoyés pour ce point de terminaison.

**Objet du message d’erreur :** permet de spécifier l’objet des messages électroniques d’erreur envoyés pour ce point de terminaison. Ce texte est affichée après le préfixe de l’objet des messages électroniques d’erreur.

**Corps du message d’erreur :** permet de spécifier la première ligne du corps du texte des messages électroniques d’erreur envoyés pour ce point de terminaison.

**Informations de résumé du courrier électronique :** chaque message de réussite ou d’échec comprend une section contenant le texte du message électronique d’origine que vous avez envoyé au serveur Forms. Ce paramètre spécifie le texte qui apparaît au-dessus cette section.

**Valider la boîte de réception avant de créer/mettre à jour ce point de terminaison :** lorsque cette option est sélectionnée, le serveur Forms vérifie si vos paramètres SMTP/POP3 sont corrects avant de créer le point de terminaison. Lorsque vous cliquez sur Ajouter, un message s’affiche pour indiquer si le compte de boîte de réception est valide ou non. Si cette option n’est pas sélectionnée, le serveur AEM forms crée le point de fin, sans vérifier la validité du compte de boîte de réception.

**Nom de l’opération :** ce paramètre est obligatoire. Liste des opérations pouvant être attribuées au point de fin de courrier électronique. L’opération sélectionnée ici détermine les champs affichés dans les sections Mappages des paramètres d’entrée et Mappages des paramètres de sortie.

**Mappages des paramètres d’entrée :** permet de configurer l’entrée nécessaire au traitement du service et de l’opération. Il existe deux types d’entrées : littéral et variable.

**Littéral :** le courrier électronique utilise la valeur saisie dans le champ telle qu’elle est affichée.

**Variable :** vous pouvez mapper une chaîne à partir de l’objet, du corps, de l’en-tête ou de l’adresse électronique de l’expéditeur du courrier électronique. Pour ce faire, utilisez l’un des mots-clés suivants : %SUBJECT%, %BODY%, %HEADER% ou %SENDER%. Par exemple, si vous utilisez %SUBJECT%, le contenu de l’objet du message électronique est utilisé comme paramètre d’entrée. Pour sélectionner des pièces jointes, spécifiez un modèle de fichier que le point de fin de courrier électronique peut utiliser pour sélectionner les documents en pièce jointe. Par exemple, la saisie de &amp;ast;.pdf sélectionne tout document joint dont l’extension est .pdf. Saisir &amp;ast; sélectionne tout document joint. Saisir exemple.pdf sélectionne tout document joint dont le nom est example.pdf.

**Mappages des paramètres de sortie :** permet de configurer la sortie du service et de l’opération. Les caractères suivants indiqués dans les valeurs de mappage des paramètres de sortie sont développés dans le nom du fichier de la pièce jointe :

**%** FRreprésente le nom de fichier du fichier source (sans extension).

**%** ERreprésente l&#39;extension du fichier source.

Toute occurrence de la barre oblique inverse (\) est remplacée par %%.

***Remarque ** : si le message de demande de service comprend plusieurs fichiers joints, vous ne pouvez pas utiliser les paramètres %F et %E dans des valeurs pour la propriété Mappages des paramètres de sortie du point de fin. Si la réponse du service renvoie plusieurs fichiers joints, vous ne pouvez pas spécifier le même nom de fichier pour plusieurs pièces jointes. Si vous ne suivez pas ces recommandations, le service appelé crée les noms des fichiers renvoyés, et les noms ne sont pas prévisibles.*

Les valeurs suivantes sont disponibles :

**Objet unique :** le fournisseur de messagerie électronique ne dispose pas de la destination du dossier source ; les résultats sont renvoyés sous forme de pièces jointes. Le modèle est Result/%F.ps et renvoie Result%%nom_fichier_source.ps comme pièce jointe du nom du fichier.

**Liste :** Le modèle est Result/%F/ et renvoie Result%%nom_fichier_source%%file1 comme pièce jointe du nom de fichier.

**Carte :** le modèle est Result/%F/ et la destination source est Result%%nom_fichier_source%%file1 et Result%%nom_fichier_source%%file2. Si cette option contient plusieurs objets et que le modèle est Result/%F.ps, les pièces jointes de réponse sont Result%%nom_fichier_source1.ps (sortie1) et Result%%nom_fichier_source2.ps (sortie2).

## Création d’un point de fin de courrier électronique pour le service Complete Task {#create-an-email-endpoint-for-the-complete-task-service}

Pour que le processus des formulaires reçoive et traite les courriers électroniques entrants envoyés par des utilisateurs, vous devez créer un point de fin de courrier électronique pour le service Complete Task.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, cliquez sur le service Complete Task.
1. Dans l’onglet Points de fin, sélectionnez Adresse électronique dans la liste déroulante et cliquez sur Ajouter.
1. Dans le champ Hôte de la boîte de réception, saisissez le nom d’hôte ou l’adresse IP du serveur de messagerie.
1. Dans le champ Utilisateur de la boîte de réception, saisissez le nom d’utilisateur requis pour se connecter au compte de messagerie créé pour le traitement des soumissions de formulaires. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’adresse électronique ou de l’adresse électronique complète.
1. Dans le champ Mot de passe de la boîte de réception, saisissez le mot de passe de l’utilisateur de la boîte de réception.
1. Dans le champ Hôte SMTP, saisissez le nom d’hôte ou l’adresse IP du serveur de messagerie à partir duquel le fournisseur de messagerie envoie les résultats et les messages d’erreur.
1. Dans le champ Utilisateur SMTP, saisissez le compte utilisateur que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie des messages électroniques pour signaler des résultats et des erreurs. Ce champ peut prendre la même valeur que le champ Utilisateur de la boîte de réception.
1. Dans le champ Mot de passe SMTP, saisissez le mot de passe du compte SMTP.
1. Dans la liste Nom de l’opération, sélectionnez appel.
1. Dans la liste attachementMap, sélectionnez Variable et saisissez `*.*` dans la zone adjacente. Toutes les pièces jointes des messages électroniques entrants sont alors envoyées vers une variable map pour le processus Terminer la tâche.
1. Dans la liste mailBody, sélectionnez variable et saisissez `%BODY%` dans la zone adjacente.
1. Dans la liste mailFrom, sélectionnez Variable et saisissez `%SENDER%` dans la zone adjacente. L’adresse de l’expéditeur est alors mise en correspondance avec les données du processus Terminer la tâche.
1. Dans la zone des résultats, saisissez `results`. Le processus Terminer la tâche (Complete Task) ou Démarrer le processus (Start Process) renvoie alors une chaîne de résultat.
1. Cliquez sur Ajouter.

