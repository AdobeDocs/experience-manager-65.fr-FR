---
title: Configuration des points d’entrée de courrier électronique
description: Découvrez comment configurer des points de fin de courrier électronique. Les points de fin de courrier électronique vous permettent d’appeler un service en envoyant un ou plusieurs documents à un compte de messagerie spécifié.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
exl-id: 33583a12-4f20-4146-baa4-c9854e454bbf
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '3775'
ht-degree: 53%

---

# Configuration des points d’entrée de courrier électronique {#configuring-email-endpoints}

Les points de fin de courrier électronique permettent aux utilisateurs d’appeler un service en envoyant un ou plusieurs documents (en tant que pièces jointes à un courrier électronique spécifique). La boîte de réception du courrier électronique sert de point de collecte pour les pièces jointes. Le service surveille la boîte de réception et traite les pièces jointes. Les résultats de la conversion sont transférés à l’utilisateur défini dans le point de terminaison .

Pour un point de fin de courrier électronique, les utilisateurs autorisés peuvent appeler un processus en envoyant des fichiers par courrier électronique au compte approprié. Les résultats sont renvoyés à l’utilisateur qui envoie (par défaut) ou à l’utilisateur défini dans les paramètres des points de fin.

Avant de configurer un point de fin de courrier électronique, créez un compte de courrier électronique POP3 ou IMAP à utiliser par le point de fin. Configurez un compte distinct pour chaque type de conversion. Par exemple, un compte peut être configuré pour générer des documents PDF standard à partir de pièces jointes entrantes, et un autre compte peut être configuré pour générer des documents PDF sécurisés.

>[!NOTE]
>
>Chaque adresse électronique ne doit correspondre qu’à un seul point de fin de courrier électronique. Vous ne pouvez pas configurer plusieurs points de fin de courrier électronique sur une seule adresse, même si les points de fin de courrier électronique supplémentaires sont désactivés.

Tous les points de fin de courrier électronique sont configurés avec un nom d’utilisateur et un mot de passe autorisés pour la boîte de réception, qui sont requis lors de l’appel du service. Le compte de messagerie est protégé par le système de serveur de messagerie sur lequel il est configuré.

Si vos utilisateurs envoient des documents dont les noms et les chemins de conversion contiennent des caractères d’alphabet des langues de l’Europe occidentale, ils doivent utiliser une application d’e-mail prenant en charge les types d’encodage requis (Latin1 [ISO-8859-1], Langues de l’Europe occidentale [Windows] ou UTF-8). Pour plus d’informations, consultez le document *Installation et déploiement d’AEM forms* correspondant à votre serveur d’applications.

Avant de configurer un point de fin de courrier électronique, configurez le service Email. (Voir [Configuration des paramètres par défaut des points de fin de courrier électronique](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) Les paramètres de configuration du service Email ont deux objectifs :

* Pour configurer les attributs communs à tous les points de fin de courrier électronique
* Pour fournir des valeurs par défaut pour tous les points de fin de courrier électronique

## Configuration du protocole SSL pour un point de fin de courrier électronique {#configure-ssl-for-an-email-endpoint}

Vous pouvez configurer les protocoles POP3, IMAP ou SMTP pour utiliser le protocole SSL (Secure Sockets Layer) pour un point de fin de courrier électronique.

1. Sur le serveur de messagerie, activez SSL pour POP3, IMAP ou SMTP, conformément à la documentation du fabricant.
1. Exportez un certificat client à partir du serveur de messagerie.
1. Utilisez le programme keytool pour importer le fichier du certificat client dans la boutique de certificats de la machine virtuelle Java (JVM) du serveur d’applications. La procédure de cette étape dépend de la JVM et des chemins d’installation du client.

   Par exemple, si vous utilisez une installation WebLogic Server par défaut avec JDK 1.5.0 sous Microsoft Windows Server® 2003, saisissez le texte suivant dans une invite de commande :

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. A l’invite, spécifiez votre mot de passe (pour Java, le mot de passe par défaut est « `changeit` »). Vous recevrez un message indiquant que le certificat a bien été importé.
1. Utilisez Administration Console pour ajouter le point de fin de courrier électronique au service.
1. Créez le point de fin de courrier électronique dans Administration Console. Lors de la configuration des paramètres des points de fin, sélectionnez SSL POP3/IMAP activé pour les messages entrants et SSL SMTP activé pour les messages sortants, puis modifiez les propriétés du port en conséquence.

>[!NOTE]
>
>Conseil : Si vous rencontrez des problèmes lors de l’utilisation de SSL, utilisez un client de messagerie tel que Microsoft Outlook pour vérifier s’il peut accéder au serveur de messagerie à l’aide de SSL. Si le client de messagerie ne peut pas accéder au serveur de messagerie, le problème est lié à la configuration de votre certificat ou de votre serveur de messagerie.

## Configuration des paramètres par défaut des points de fin de courrier électronique {#configure-default-email-endpoint-settings}

Vous pouvez utiliser la page Gestion des services pour configurer les attributs communs à tous les points de fin de courrier électronique et fournir les valeurs par défaut de tous les points de fin de courrier électronique.

Pour que le processus des formulaires reçoive et traite les courriers électroniques entrants envoyés par les utilisateurs, vous devez créer un point de fin de courrier électronique pour le service Complete Task. Ce point de fin de courrier électronique nécessite des paramètres supplémentaires, comme décrit dans la section [Création d’un point de fin de courrier électronique pour le service Complete Task](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Modification des valeurs par défaut des points de fin de courrier électronique {#change-the-default-values-for-email-endpoints}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Sur la page Gestion des services, cliquez sur Email: 1.0 (l’ID de composant est com.adobe.idp.dsc.provider.service.email.Email).
1. Dans l’onglet Configuration , spécifiez les paramètres par défaut des points de fin de courrier électronique, puis cliquez sur Enregistrer.

### Paramètres des points de fin de courrier électronique par défaut {#default-email-endpoint-settings}

**Expression Cron :** expression Cron utilisée par Quartz pour planifier l’interrogation du répertoire d’entrée.

**Intervalle de répétitions :** nombre de répétitions de l’interrogation du répertoire d’entrée. L’intervalle de répétition par défaut est exprimé en secondes si cette valeur n’est pas spécifiée dans la configuration des points d’entrée. La valeur par défaut est 10. Cette valeur ne peut pas être inférieure à 10.

**Nombre de répétitions :** nombre d’interrogations du répertoire d’entrée. Nombre de répétitions par défaut à utiliser si cette valeur n’est pas spécifiée dans la configuration du point de terminaison. La valeur -1 indique une analyse indéfinie du répertoire. La valeur par défaut est -1.

**Retard au début d’une tâche :** valeur par défaut (en secondes) du retard au début de l’analyse du point d’entrée. La valeur par défaut est 0.

**Taille du lot :** nombre d’e-mails que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 indique tous les emails. La valeur par défaut est 2.

**Asynchrone :** identifie le type d’invocation comme étant asynchrone ou synchrone. Les processus provisoires et synchrones peuvent être appelés uniquement de façon synchrone. La valeur par défaut est asynchrone.

**Modèle de domaine :** modèle de nom de domaine servant à filtrer les e-mails entrants. Par exemple, si le domaine adobe.com est utilisé, seuls les messages électroniques de ce domaine sont traités ; ceux provenant d’autres domaines sont ignorés.

**Modèle de fichier :** indique les modèles de pièce jointe de fichier entrant acceptés par le fournisseur. Les fichiers portant des extensions particulières (*.dat, *.xml), des noms spécifiques (data) et contenant des expressions composites dans leur nom et leur extension (.[dD][aA]&#39;port&#39;). La valeur par défaut est &amp;ast;.&amp;ast;.

**Destinataires de tâches réussies :** une ou plusieurs adresses e-mails utilisées pour envoyer des e-mails afin d’indiquer les tâches réussies. Par défaut, un message de tâche réussi est toujours envoyé à l’expéditeur de la tâche initiale. Jusqu’à 100 destinataires sont pris en charge. Pour désactiver ce paramètre, laissez ce champ vide.

**Destinataires de tâches échouées :** une ou plusieurs adresses e-mails utilisées pour envoyer des e-mails afin d’indiquer les tâches ayant échoué. Par défaut, un message de tâche en échec est toujours envoyé à l’expéditeur qui a envoyé la tâche initiale. Jusqu’à 100 destinataires sont pris en charge. Pour désactiver ce paramètre, laissez ce champ vide.

**Hôte de boîte de réception :** nom ou adresse IP de l’hôte de boîte de réception du fournisseur de messagerie électronique à analyser.

**Port de boîte de réception :** numéro de port de boîte de réception que le fournisseur de messagerie électronique doit analyser. Si la valeur est 0, le port IMAP ou POP3 par défaut est utilisé.

**Protocole de boîte de réception :** protocole utilisé par le point d’entrée d’e-mail pour analyser la boîte de réception. Les choix possibles sont IMAP ou POP3. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.

**Délai d’expiration de la boîte de réception :** indique le délai d’expiration du point d’entrée pour annuler une tentative de connexion à la boîte de réception. Si une connexion n’est pas établie avant que cette valeur ne soit atteinte, la boîte de réception n’est pas interrogée.

**Utilisateur de la boîte de réception :** nom d’utilisateur requis pour se connecter au compte e-mail. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’adresse électronique ou de l’adresse électronique complète.

**Mot de passe de la boîte de réception :** mot de passe de l’utilisateur de la boîte de réception.

**SSL POP3/IMAP activé :** lorsque cette option est sélectionnée, SSL est activé.

**Hôte SMTP :** nom d’hôte du serveur de messagerie par lequel le fournisseur de messagerie électronique envoie les résultats et les messages d’erreur. Par exemple, mail.example.com.

**Port SMTP :** port utilisé pour la connexion au serveur de messagerie. La valeur par défaut est 25.

**Utilisateur SMTP** : compte d’utilisateur que le fournisseur d’e-mail doit utiliser pour envoyer des résultats et des erreurs par e-mail.

**Mot de passe SMTP :** mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.

**Envoyé par :** adresse e-mail (utilisateur@entreprise.com, par exemple) utilisée pour envoyer des notifications par e-mail de résultats et d’erreurs. Si vous ne spécifiez pas de valeur Send From, le serveur de messagerie tente de déterminer l’adresse électronique en combinant la valeur spécifiée dans le paramètre SMTP User avec un domaine par défaut configuré sur le serveur de messagerie. Si votre serveur de messagerie n’a pas de domaine par défaut et que vous ne spécifiez pas de valeur pour l’option De, des erreurs peuvent se produire. Pour vous assurer que les courriers électroniques auront la bonne adresse d’envoi De, indiquez une valeur pour le paramètre De.

**SMTP SSL activé :** lorsque cette option est sélectionnée, SSL via SMTP est activé.

**Incluez Le Corps De L&#39;Email D&#39;Origine En Pièce Jointe :** Par défaut, lorsque vous envoyez un email au serveur Forms, le texte d’origine du message est inclus dans le corps du message. Pour inclure ce texte en pièce jointe à la place, sélectionnez cette option.

**Utiliser la ligne d’objet originelle pour les e-mails de résultat :** par défaut, le serveur Forms utilise les valeurs spécifiées dans les paramètres d’objet des e-mails de succès et d’erreur en tant qu’objet des e-mails de résultat envoyés. Pour que l’objet des messages électroniques de résultat soit le même que l’objet du message électronique original envoyé au serveur, sélectionnez cette option.

**Success Email Subject :** Une fois que vous avez envoyé un courrier électronique à un point de fin de courrier électronique pour démarrer ou continuer un processus, vous recevez un courrier électronique de retour du serveur AEM Forms. Si votre email réussit, vous recevez un message de réussite. Si votre email échoue, vous recevez un message d’échec vous informant de son échec. Ce paramètre vous permet de spécifier l’objet des messages électroniques de réussite envoyés pour ce point de terminaison.

**Corps de l’e-mail de succès :** permet de spécifier le corps de texte des e-mails de succès envoyés pour ce point d’entrée.

**Préfixe d’objet des e-mails d’erreurs :** permet de spécifier le préfixe utilisé au début de l’objet des e-mails d’erreur envoyés pour ce point d’entrée.

**Objet de l’e-mail d’erreur :** permet de spécifier l’objet des e-mails d’erreur envoyés pour ce point d’entrée. Ce texte est affichée après le préfixe de l’objet des messages électroniques d’erreur.

**Corps des e-mails d’erreur :** permet de spécifier la première ligne du corps du texte des e-mails d’erreur envoyés pour ce point d’entrée.

**Email Summary Info :** Chaque message de succès ou d’échec comprend une section contenant le texte du courrier électronique d’origine que vous avez envoyé au serveur Forms. Ce paramètre spécifie le texte qui apparaît au-dessus cette section.

**Validez La Boîte De Réception Avant De Créer/Mettre À Jour Ce Point De Terminaison :** Lorsque cette option est sélectionnée, le serveur Forms vérifie que vos paramètres SMTP/POP3 sont corrects avant de créer le point de terminaison. Lorsque vous cliquez sur Ajouter, un message s’affiche, indiquant si le compte de boîte de réception est valide. Si cette option n’est pas sélectionnée, le serveur AEM Forms crée le point de terminaison sans valider la boîte de réception.

**Encodage du jeu de caractères :** format de codage à utiliser pour l’e-mail. La valeur par défaut est UTF-8, que la plupart des utilisateurs en dehors du Japon utiliseront. Les utilisateurs d’un environnement japonais peuvent choisir ISO2022-JP.

**Dossier Échec d’envoi de l’e-mail :** spécifie un répertoire dans lequel stocker les résultats en cas de non-fonctionnement du serveur de courrier SMTP.

## Paramètres des points d’entrée de courrier électronique {#email-endpoint-settings}

Utilisez les paramètres suivants pour configurer un point de fin de courrier électronique.

**Nom :** paramètre obligatoire qui identifie le point d’entrée. N’incluez pas de caractère&lt;, car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point d’entrée, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**Description :** description du point d’entrée. N’incluez pas de caractère &lt;, car la description affichée dans Workspace serait tronquée.

**Expression Cron :** saisissez une expression Cron si l’e-mail doit être programmé en utilisant une expression de ce type.

**Nombre de répétitions :** nombre de fois que le point d’entrée de l’e-mail analyse le dossier ou le répertoire. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.

**Intervalle de répétition :** taux d’analyse que le destinataire utilise pour vérifier le courrier entrant.

**Délai de début de la tâche :** temps d’attente d’analyse une fois le planificateur démarré.

**Taille du lot :** nombre d’emails que le destinataire traite par analyse pour obtenir des performances optimales. La valeur -1 indique tous les emails. La valeur par défaut est 2.

**Nom d’utilisateur :** paramètre obligatoire correspondant au nom d’utilisateur utilisé lors de l’appel d’un service cible à partir de l’e-mail. La valeur par défaut est SuperAdmin.

**Nom de domaine :** paramètre obligatoire correspondant au domaine de l’utilisateur. La valeur par défaut est DefaultDom.

**Modèle de domaine :** spécifie les modèles de domaine d’e-mail entrant qui sont acceptés par le fournisseur. Par exemple, si le domaine adobe.com est utilisé, seuls les messages électroniques de ce domaine sont traités ; ceux provenant d’autres domaines sont ignorés.

**Modèle de fichier :** indique les modèles de pièce jointe de fichier entrant qui sont acceptés par le fournisseur. Cela inclut les fichiers ayant des extensions spécifiques (&amp;ast;.dat, &amp;ast;.xml), des noms spécifiques (data) ou des expressions composites dans le nom et l’extension (&amp;ast;.[dD][aA]&#39;port&#39;).

**Destinataires des tâches effectuées :** adresse e-mail à laquelle sont envoyés les messages pour signaler les tâches effectuées. Par défaut, un message de travail effectué est toujours envoyé à l’expéditeur. Si vous saisissez sender, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses électroniques séparées par des virgules (,).

Pour désactiver ce paramètre, laissez le paramètre vide. Dans certains cas, vous souhaitez déclencher un processus et ne souhaitez pas recevoir de notification par courrier électronique du résultat.

**Destinataires des tâches en échec :** adresse e-mail à laquelle sont envoyés les messages pour signaler les travaux ayant échoué. Par défaut, un message de travail ayant échoué est toujours envoyé à l’expéditeur. Si vous saisissez sender, les résultats des messages électroniques sont envoyés à l’expéditeur. Jusqu’à 100 destinataires sont pris en charge. Spécifiez d’autres destinataires avec des adresses électroniques séparées par des virgules (,).

Pour désactiver ce paramètre, laissez le paramètre vide. Dans certains cas, vous souhaitez déclencher un processus et ne souhaitez pas recevoir de notification par courrier électronique du résultat.

**Hôte de la boîte de réception :** nom ou adresse IP de l’hôte de la boîte de réception du fournisseur de messagerie électronique à analyser.

**Port de la boîte de réception :** port utilisé par le serveur de messagerie. La valeur POP3 par défaut est 110 et la valeur IMAP par défaut est 143. Si le protocole SSL est activé, la valeur POP3 par défaut est 995 et la valeur IMAP par défaut est 993.

**Protocole de la boîte de réception :** protocole utilisé par le point d’entrée d’e-mail pour analyser la boîte de réception. Les valeurs sont IMAP ou POP3. Le serveur de messagerie de l’hôte boîte de réception doit prendre en charge ces protocoles.

**Délai d’attente de la boîte de réception :** délai (en secondes) pendant lequel le fournisseur d’e-mail attend les réponses de la boîte de réception.

**Utilisateur de la boîte de réception :** nom d’utilisateur requis pour se connecter au compte e-mail. En fonction du serveur de messagerie et de la configuration, il peut s’agir uniquement de la partie nom d’utilisateur de l’adresse électronique ou de l’adresse électronique complète.

**Mot de passe de la boîte de réception :** mot de passe de l’utilisateur de la boîte de réception.

**POP3/IMAP SSL activé :** sélectionnez ce paramètre pour forcer le fournisseur d’e-mail à utiliser le protocole SSL pour analyser la boîte de réception. Vérifiez que le serveur de messagerie prend en charge le protocole SSL.

**Hôte SMTP :** nom d’hôte du serveur de messagerie auquel le fournisseur d’e-mail envoie les résultats et les messages d’erreur.

**Port SMTP :** la valeur par défaut du port SMTP est 25.

**Utilisateur SMTP** : compte d’utilisateur que le fournisseur d’e-mail doit utiliser lorsqu’il envoie des e-mails pour signaler des résultats et des erreurs.

**Mot de passe SMTP :** mot de passe du compte SMTP. Certains serveurs de messagerie ne nécessitent pas de mot de passe SMTP.

**Envoyé par :** adresse e-mail (utilisateur@entreprise.com, par exemple) utilisée pour envoyer des notifications par e-mail de résultats et d’erreurs. Si vous ne spécifiez pas de valeur Send From, le serveur de messagerie tente de déterminer l’adresse électronique en combinant la valeur spécifiée dans le paramètre SMTP User avec un domaine par défaut configuré sur le serveur de messagerie. Si votre serveur de messagerie n’a pas de domaine par défaut et que vous ne spécifiez pas de valeur pour l’option De, des erreurs peuvent se produire. Pour vous assurer que les courriers électroniques auront la bonne adresse d’envoi De, indiquez une valeur pour le paramètre De.

**SMTP SSL activé :** sélectionnez ce paramètre pour forcer le fournisseur d’e-mail à utiliser le protocole SSL pour analyser la boîte de réception. Vérifiez que le serveur de messagerie prend en charge le protocole SSL.

**Dossier Échec d’envoi d’e-mail :** spécifie un répertoire dans lequel stocker les résultats en cas de non-fonctionnement du serveur de courrier SMTP.

**asynchrone :** lorsque l’option est définie sur synchrone, tous les documents d’entrée sont traités, puis une seule réponse est renvoyée. Lorsqu’elle est définie sur asynchrone, une réponse est envoyée pour chaque document traité.

Par exemple, un point de fin de courrier électronique est créé pour un service qui utilise un seul document Word et renvoie ce document en tant que fichier PDF. Un courrier électronique peut être envoyé à la boîte de réception du point de fin qui contient plusieurs (3) documents Word. Lorsque les trois documents sont traités, si le point de fin est configuré comme synchrone, un seul message électronique de réponse est envoyé avec les trois documents joints. Si le point de fin est asynchrone, un courrier électronique de réponse est envoyé une fois que chaque document Word a été converti en PDF. Il en résulte trois emails, chacun avec une pièce jointe de PDF unique.

La valeur par défaut est asynchrone.

**Insérez le corps du courrier électronique d’origine en tant que pièce jointe :** Par défaut, lorsque vous envoyez un email au serveur Forms, le texte d’origine du message est inclus dans le corps du message. Pour inclure ce texte en pièce jointe à la place, sélectionnez cette option.

**Utiliser la ligne d’objet d’origine pour les e-mails de résultats :** par défaut, le serveur Forms utilise les valeurs spécifiées dans les paramètres d’objet des e-mails de réussite et d’erreur en tant qu’objet des e-mails de résultat envoyés. Pour que l’objet des messages électroniques de résultat soit le même que l’objet du message électronique original envoyé au serveur, sélectionnez cette option.

**Success Email Subject :** Une fois que vous avez envoyé un courrier électronique à un point de fin de courrier électronique pour démarrer ou continuer un processus, vous recevez un courrier électronique de retour du serveur AEM Forms. Si votre email réussit, vous recevez un message de réussite. Si votre email échoue, vous recevez un message d’échec vous informant de son échec. Ce paramètre vous permet de spécifier l’objet des messages électroniques de réussite envoyés pour ce point de terminaison.

**Corps de l’e-mail de succès :** permet de spécifier le corps de texte des e-mails de succès envoyés pour ce point d’entrée.

**Préfixe d’objet des e-mails d’erreurs :** permet de spécifier le préfixe utilisé au début de l’objet des e-mails d’erreur envoyés pour ce point d’entrée.

**Objet de l’e-mail d’erreur :** permet de spécifier l’objet des e-mails d’erreur envoyés pour ce point d’entrée. Ce texte est affichée après le préfixe de l’objet des messages électroniques d’erreur.

**Corps des e-mails d’erreur :** permet de spécifier la première ligne du corps du texte des e-mails d’erreur envoyés pour ce point d’entrée.

**Email Summary Info :** Chaque message de succès ou d’échec comprend une section contenant le texte du courrier électronique d’origine que vous avez envoyé au serveur Forms. Ce paramètre spécifie le texte qui apparaît au-dessus cette section.

**Validez la boîte de réception avant de créer/mettre à jour ce point de terminaison :** Lorsque cette option est sélectionnée, le serveur Forms vérifie que vos paramètres SMTP/POP3 sont corrects avant de créer le point de terminaison. Lorsque vous cliquez sur Ajouter, un message s’affiche, indiquant si le compte de boîte de réception est valide. Si cette option n’est pas sélectionnée, le serveur AEM Forms crée le point de terminaison sans valider la boîte de réception.

**Nom de l’opération :** ce paramètre est obligatoire. Liste des opérations pouvant être affectées au point de fin de courrier électronique. L’opération que vous sélectionnez ici détermine les champs affichés dans les sections Mappages des paramètres d’entrée et Mappages des paramètres de sortie .

**Mappage du paramètre d’entrée :** permet de configurer l’entrée requise pour traiter le service et l’opération. Il existe deux types d’entrées : littéral et variable.

**Littéral :** l’e-mail utilise la valeur saisie dans le champ telle qu’elle est affichée.

**Variable :** vous pouvez associer une chaîne à l’objet, au corps, à l’en-tête ou à l’adresse e-mail de l’expéditeur de l’e-mail. Pour ce faire, utilisez l’un des mots-clés suivants : %SUBJECT%, %BODY%, %HEADER% ou %SENDER%. Par exemple, si vous utilisez %SUBJECT%, le contenu de l’objet de l’email est utilisé comme paramètre d’entrée. Pour sélectionner des pièces jointes, saisissez un modèle de fichier que le point de fin de courrier électronique peut utiliser pour sélectionner les documents joints. Par exemple, le fait de saisir &amp;ast;.pdf sélectionne tout document joint dont l’extension est .pdf. La saisie de « &amp;ast; » sélectionne tout document joint. Saisir exemple.pdf sélectionne tout document joint dont le nom est example.pdf.

**Mappage du paramètre de sortie :** permet de configurer les sorties du service et de l’opération. Les caractères suivants indiqués dans les valeurs de mappage des paramètres de sortie sont développés dans le nom du fichier de la pièce jointe :

**%F** représente le nom du fichier source (extension non incluse).

**%E** représente l’extension du fichier source.

Toute occurrence de la barre oblique inverse (\) est remplacée par %%.

***Remarque ** : si le message de demande de service comprend plusieurs fichiers joints, vous ne pouvez pas utiliser les paramètres %F et %E dans des valeurs pour la propriété Mappages des paramètres de sortie du point d’entrée. Si la réponse du service renvoie plusieurs pièces jointes, vous ne pouvez pas spécifier le même nom de fichier pour plusieurs pièces jointes. Si vous ne suivez pas ces recommandations, le service appelé crée les noms des fichiers renvoyés et les noms ne sont pas prévisibles.*

Les valeurs suivantes sont disponibles :

**Objet unique :** le fournisseur de messagerie électronique n’a pas la destination du dossier source. Les résultats sont renvoyés en tant que pièces jointes. Le modèle est Result/%F.ps et renvoie Result%%nom_fichier_source.ps comme pièce jointe du nom du fichier.

**Liste :** le modèle est Result/%F/ et renvoie Result%%sourcefilename%%file1 comme pièce jointe du nom de fichier.

**Mappage :** le modèle est Result/%F/ et la destination de la source est Result%%sourcefilename%%file1 et Result%%sourcefilename%%file2. Si cette option contient plusieurs objets et que le modèle est Result/%F.ps, les pièces jointes de réponse sont Result%%nom_fichier_source1.ps (sortie1) et Result%%nom_fichier_source2.ps (sortie2).

## Création d’un point de fin de courrier électronique pour le service Complete Task {#create-an-email-endpoint-for-the-complete-task-service}

Pour que le processus des formulaires reçoive et traite les courriers électroniques entrants envoyés par les utilisateurs, vous devez créer un point de fin de courrier électronique pour le service Complete Task.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, cliquez sur le service Complete Task.
1. Dans l’onglet Points de fin, sélectionnez Email dans la liste déroulante, puis cliquez sur Ajouter.
1. Dans le champ Inbox Host, saisissez le nom d’hôte ou l’adresse IP du serveur de messagerie.
1. Dans la boîte de réception User, saisissez le nom d’utilisateur requis pour vous connecter au compte de messagerie que vous avez créé afin de gérer les envois de formulaire. Selon le serveur de messagerie et la configuration, ce nom peut être uniquement la partie nom d’utilisateur de l’e-mail ou l’adresse électronique complète.
1. Dans la zone Inbox Password, saisissez le mot de passe de l’utilisateur de la boîte de réception.
1. Dans la zone SMTP Host, saisissez le nom d’hôte ou l’adresse IP du serveur de messagerie à partir duquel le fournisseur de messagerie envoie les résultats et les messages d’erreur.
1. Dans la zone SMTP User, saisissez le compte utilisateur que le fournisseur de messagerie électronique doit utiliser lorsqu’il envoie un courrier électronique pour signaler des résultats et des erreurs. Ce compte utilisateur peut être la même valeur que celle utilisée pour l’utilisateur de la boîte de réception.
1. Dans la zone SMTP Password, saisissez le mot de passe du compte SMTP.
1. Dans la liste Operation Name, sélectionnez invoke.
1. Dans la liste attachmentMap, sélectionnez Variable et saisissez `*.*` dans le champ adjacent. Toutes les pièces jointes des messages électroniques entrants sont alors envoyées vers une variable map pour le processus Terminer la tâche.
1. Dans la liste mailBody, sélectionnez Variable et saisissez `%BODY%` dans le champ adjacent.
1. Dans la liste mailFrom, sélectionnez Variable et saisissez `%SENDER%` dans le champ adjacent. L’adresse de l’expéditeur est alors mise en correspondance avec les données du processus Terminer la tâche.
1. Dans la zone des résultats, saisissez `results`. Cela entraîne le renvoi d’une chaîne de résultat par l’option Terminer la tâche ou Processus de démarrage .
1. Cliquez sur Ajouter.
