---
title: Référence sur les étapes du processus basé sur l’utilisation de Forms on OSGi
seo-title: Référence sur les étapes du processus basé sur l’utilisation de Forms on OSGi
description: Les étapes du processus basé sur l’utilisation de Forms on OSGi vous permettent de créer rapidement des formulaires adaptatifs basés sur des processus.
seo-description: Les étapes du processus basé sur l’utilisation de Forms on OSGi vous permettent de créer rapidement des formulaires adaptatifs basés sur des processus.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
source-git-commit: aaafda59c63ea47c67ec974263013ead468df9cc
workflow-type: tm+mt
source-wordcount: '7268'
ht-degree: 64%

---

# Référence sur les étapes du processus basé sur l’utilisation de Forms on OSGi{#forms-centric-workflow-on-osgi-step-reference}

## Étapes de processus Forms {#forms-workflow-steps}

Les étapes de processus Forms effectuent des opérations spécifiques à AEM Forms dans un processus AEM. Ces étapes vous permettent de créer rapidement des formulaires adaptatifs à partir de processus basés sur l’utilisation de Forms on OSGi. Ces workflows peuvent être utilisés pour développer des processus de révision et d’approbation de base, des processus métier internes et entre pare-feu. Vous pouvez également utiliser les étapes de processus Forms pour lancer les services de document, les intégrer au processus de signature Adobe Sign et effectuer d’autres opérations AEM Forms. Un [module complémentaire AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) est nécessaire pour utiliser ces étapes dans un processus.

## Étape Affecter une tâche {#assign-task-step}

L’étape Affecter une tâche crée une tâche et l’affecte à un utilisateur ou un groupe. Lors de l’affectation de la tâche, le composant spécifie également le formulaire adaptatif ou le fichier PDF non interactif de la tâche. Le formulaire adaptatif est requis pour accepter une saisie des utilisateurs et un fichier PDF non interactif ou un formulaire adaptatif en lecture seule est utilisé pour les processus de révision uniquement.

Vous pouvez également utiliser le composant pour contrôler le comportement de la tâche. Par exemple : lors de la création d’un document d’enregistrement automatique, lors de l’affectation de la tâche à un utilisateur ou un groupe spécifique, lors de l’indication du chemin d’accès des données envoyées, lors de l’indication du chemin d’accès des données pré-renseignées et des actions par défaut. L’étape Affecter une tâche possède les propriétés suivantes :

* **Titre :** titre de la tâche. Le titre s’affiche dans la boîte de réception AEM.
* **Description :** description des opérations en cours dans la tâche. Ces informations sont utiles pour d’autres développeurs de processus lorsque vous travaillez dans un environnement de développement partagé.

* **Chemin d’accès de la miniature :** chemin d’accès de la miniature de la tâche. Si aucun chemin n’est spécifié, une miniature par défaut s’affiche pour un formulaire adaptatif et une icône par défaut s’affiche pour un document d’enregistrement.
* **Phase de processus :** un processus peut se composer de plusieurs phases. Ces phases sont affichées dans la boîte de réception AEM. Vous pouvez définir ces phases dans les propriétés du modèle (Sidekick > Page > Propriétés de la page > Phases).
* **Priorité :** la priorité sélectionnée s’affiche dans la boîte de réception AEM. Les options disponibles sont les suivantes : Élevée, Moyenne et Faible. La valeur par défaut est Moyenne.
* **Date d’expiration :** spécifiez le nombre de jours ou d’heures restant avant que la tâche soit affichée comme En retard. Si vous sélectionnez **Désactivé**, la tâche n’est jamais marquée comme En retard. Vous pouvez également spécifier un gestionnaire de dépassement de délai pour effectuer des tâches spécifiées dès que la tâche est marquée comme En retard.

* **Jours :** le nombre de jours restants pour terminer la tâche. Le nombre de jours est calculé à partir du jour de l’affectation de la tâche à un utilisateur. Si cette option est sélectionnée, si une tâche n’est pas terminée et dépasse le nombre de jours spécifié dans le champ Jours, un gestionnaire de dépassement de délai est déclenché après la date d’expiration.
* **Heures :** le nombre d’heures restantes pour terminer la tâche. Le nombre d’heures est calculé à partir de l’heure de l’affectation de la tâche à un utilisateur. Si cette option est sélectionnée, si une tâche n’est pas terminée et dépasse le nombre d’heures spécifié dans le champ Heures, un gestionnaire de dépassement de délai est déclenché après l’heure de l’expiration.
* **Expiration après l’échéance :** sélectionnez cette option pour activer le champ Sélection du gestionnaire de dépassement de délai.
* **Gestionnaire de dépassement de délai :** sélectionnez le script à exécuter lorsque l’étape Affecter une tâche dépasse l’échéance. Les scripts placés dans le référentiel CRX à l’emplacement [apps]/fd/dashboard/scripts/timeoutHandler peuvent être sélectionnés. Le chemin spécifié n’existe pas dans le référentiel CRX. Un administrateur crée le chemin d’accès avant de l’utiliser.
* **Sélectionner l’action et ajouter un commentaire depuis la dernière tâche dans Détails de la tâche :** sélectionnez cette option pour afficher la dernière action qui a été effectuée et le dernier commentaire reçu dans la section Détails de la tâche.
* **Type :** sélectionnez le type de document à remplir lors du lancement du processus. Vous pouvez choisir un formulaire adaptatif, un formulaire adaptatif en lecture seule, un document PDF non interactif, l’interface utilisateur de l’agent de communication interactive ou un document de canal web de communication interactive.
* **Utiliser le formulaire adaptatif :** indiquez la méthode pour localiser le formulaire adaptatif d’entrée. Cette option est disponible si vous sélectionnez Formulaire adaptatif ou Formulaire adaptatif en lecture seule dans la liste déroulante Type . Vous pouvez utiliser le formulaire adaptatif envoyé au workflow, disponible à un chemin d’accès absolu ou disponible à un chemin d’accès dans une variable. Vous pouvez utiliser une variable de type chaîne pour spécifier le chemin d’accès.\
   Vous pouvez associer plusieurs formulaires adaptatifs à un workflow. Par conséquent, vous pouvez spécifier un formulaire adaptatif au moment de l’exécution à l’aide des méthodes d’entrée disponibles.

* **Utiliser la communication interactive :** indiquez la méthode pour localiser la communication interactive d’entrée. Vous pouvez utiliser la communication interactive envoyée au workflow, disponible à un chemin absolu ou disponible à un chemin dans une variable. Vous pouvez utiliser une variable de type chaîne pour spécifier le chemin d’accès. Cette option est disponible si vous sélectionnez Interface utilisateur de l’agent de communication interactive ou Document de canal web de communication interactive dans la liste déroulante Type .

>[!NOTE]
>
>Vous devez disposer de cm-agent-users et d’affectations de groupe workflow-users pour accéder à l’interface utilisateur de l’agent de communication interactive dans AEM boîte de réception.

* **Formulaire adaptatif ou chemin de communication interactive** : Spécifiez le chemin d’accès du formulaire adaptatif ou de la communication interactive. Vous pouvez utiliser le formulaire adaptatif ou la communication interactive envoyé au workflow, disponible à un chemin d’accès absolu, ou récupérer le formulaire adaptatif à partir d’un chemin d’accès stocké dans une variable de type de données string.
* **Sélectionner le PDF d’entrée à l’aide de :** spécifiez le chemin d’accès d’un document PDF non interactif. Le champ apparaît lorsque vous sélectionnez un document PDF non interactif dans le champ Type. Vous pouvez sélectionner le fichier PDF d’entrée à l’aide du chemin d’accès relatif à la charge utile, enregistré à un chemin absolu ou à l’aide d’une variable de type de données Document. Par exemple, [Répertoire_Charge_utile]/Workflow/PDF/credit-card.pdf. Le chemin n’existe pas dans le référentiel CRX. Un administrateur crée le chemin d’accès avant de l’utiliser. Vous devez activer l’option Document d’enregistrement ou posséder des formulaires adaptatifs basés sur un modèle de formulaire pour utiliser l’option Chemin d’accès du fichier PDF.
* **Une fois la tâche terminée, effectuer le rendu du formulaire adaptatif en tant que** : lorsqu’une tâche est marquée comme terminée, vous pouvez effectuer le rendu du formulaire adaptatif en tant que formulaire adaptatif en lecture seule ou document PDF. Vous devez activer l’option Document d’enregistrement ou posséder des formulaires adaptatifs basés sur un modèle de formulaire pour effectuer le rendu du formulaire adaptatif en tant que Document d’enregistrement.
* **Pré-renseigné :**  les champs suivants ci-dessous servent d’entrées à la tâche :

   * **Sélectionnez le fichier de données d’entrée à l’aide de :** Chemin du fichier de données d’entrée (.json,). xml, .doc ou modèle de données de formulaire). Vous pouvez récupérer le fichier de données d’entrée à l’aide d’un chemin d’accès relatif à la charge utile ou récupérer le fichier stocké dans une variable de type de données Document, XML ou JSON. Par exemple, le fichier contient les données envoyées pour le formulaire via une application de boîte de réception AEM. Voici un exemple de chemin d’accès : [Répertoire_Charge_utile]/workflow/data.
   * **Sélectionner les pièces jointes d’entrée à l’aide de :** les pièces jointes disponibles à l’emplacement sont jointes au formulaire associé à la tâche. Le chemin d’accès est toujours relatif à la charge. Voici un exemple de chemin d’accès : [Répertoire_Charge_utile]/attachments/
   * **Choisissez JSON d’entrée :** sélectionnez un fichier JSON d’entrée à l’aide d’un chemin d’accès relatif à la charge utile ou stocké dans une variable de type de données Document, JSON ou Form Data Model. Cette option est disponible si vous sélectionnez Interface utilisateur de l’agent de communication interactive ou Document de canal web de communication interactive dans la liste déroulante Type .
   * **Choisir un service de préremplissage personnalisé :** sélectionnez le service de préremplissage pour récupérer les données et préremplissez le document du canal web de communication interactive ou l’interface utilisateur de l’agent.

   * **Utiliser le service de préremplissage de la communication interactive sélectionnée ci-dessus :**  utilisez cette option pour utiliser le service de préremplissage de la communication interactive définie dans la liste déroulante Utiliser la communication interactive .
   * **Mappage des attributs de requête :** utilisez la section Mappage des attributs de requête pour définir le  [nom et la valeur de l’attribut de requête](../../forms/using/work-with-form-data-model.md#bindargument). Récupérez les détails de la source de données en fonction du nom d’attribut et de la valeur spécifiés dans la requête. Vous pouvez définir une valeur d’attribut de requête à l’aide d’une valeur littérale ou d’une variable de type de données Chaîne.\
      Les options de mappage de service de préremplissage et d’attribut de requête ne sont disponibles que si vous sélectionnez Interface utilisateur de l’agent de communication interactive ou Document de canal web de communication interactive dans la liste déroulante Type .

* **Informations envoyées :** les champs répertoriés ci-dessous servent d’emplacement de sortie pour la tâche :

   * **Enregistrez le fichier de données de sortie à l’aide de :** enregistrez le fichier de données (.json,). xml, .doc ou modèle de données de formulaire). Le fichier de données contient des informations envoyées via le formulaire associé. Vous pouvez enregistrer le fichier de données de sortie à l’aide d’un chemin d’accès relatif à la charge utile ou le stocker dans une variable de type de données Document, XML ou JSON. Par exemple, [Répertoire_Charge_utile]/Workflow/data, où les données correspondent à un fichier.
   * **Enregistrer les pièces jointes à l’aide de :** enregistrez les pièces jointes de formulaire fournies dans une tâche. Vous pouvez enregistrer les pièces jointes à l’aide d’un chemin relatif à la charge utile ou le stocker dans une variable de tableau de type de données Document .
   * **Enregistrer le document d’enregistrement à l’aide de :** chemin d’accès pour enregistrer un fichier de document d’enregistrement. Par exemple,[ Répertoire_Charge_utile]/DocumentofRecord/credit-card.pdf. Vous pouvez enregistrer le document d’enregistrement à l’aide d’un chemin d’accès relatif à la charge utile ou le stocker dans une variable de type de données Document. Si vous sélectionnez l’option **Relatif à la charge utile**, le document d’enregistrement n’est pas généré si le champ de chemin d’accès est laissé vide. Cette option est disponible uniquement si vous sélectionnez Formulaire adaptatif dans la liste déroulante Type .

   * **Enregistrer les données du canal web à l’aide de :** enregistrez le fichier de données du canal web à l’aide d’un chemin relatif à la charge utile ou stockez-le dans une variable de type de données Document, JSON ou Form Data Model. Cette option est disponible uniquement si vous sélectionnez Interface utilisateur de l’agent de communication interactive dans la liste déroulante Type .
   * **Enregistrer le document PDF à l’aide de :** enregistrez le document PDF à l’aide d’un chemin relatif à la charge utile ou stockez-le dans une variable de type de données Document. Cette option est disponible uniquement si vous sélectionnez Interface utilisateur de l’agent de communication interactive dans la liste déroulante Type .
   * **Enregistrer le modèle de mise en page à l’aide de :** enregistrez le modèle de mise en page à l’aide d’un chemin relatif à la payload ou stockez-le dans une variable de type de données Document. Le [modèle de mise en page](../../forms/using/layout-design-details.md) fait référence à un fichier XDP que vous créez à l’aide de Forms Designer. Cette option est disponible uniquement si vous sélectionnez Interface utilisateur de l’agent de communication interactive dans la liste déroulante Type .

* **Cessionnaire > Options d’affectation :** spécifiez la méthode d’affectation de la tâche à un utilisateur. Vous pouvez affecter la tâche de manière dynamique à un utilisateur ou un groupe à l’aide du script Programme de sélection des participants ou affecter la tâche à un utilisateur ou à un groupe AEM spécifique.
* **Programme de sélection des participants :** cette option est disponible lorsque l’option **Sélectionner de manière dynamique un utilisateur ou un groupe** est activée dans le champ Options d’affectation. Vous pouvez utiliser un script ECMAScript ou un service pour sélectionner de manière dynamique un utilisateur ou un groupe. Pour plus d’informations, voir [Affecter de manière dynamique un processus à des utilisateurs](https://helpx.adobe.com/fr/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) et [Création d’une étape Participant dynamique Adobe Experience Manager personnalisé.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr&amp;CID=RedirectAEMCommunityKautuk)

* **Participants :** le champ est disponible lorsque l’option **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]****est sélectionnée dans le champ Programme de sélection des participants.** Le champ vous permet de sélectionner des utilisateurs ou des groupes pour l’option RandomParticipantChooser.

* **Cessionnaire :** le champ est disponible lorsque  **[!UICONTROL com.adobe.fd.workspace.step.service.]** VariableParticipantChooserest sélectionné dans le champ  **Programme de sélection des** participants. Ce champ vous permet de sélectionner une variable de type Chaîne pour définir la personne désignée.

* **Arguments :** le champ est disponible lorsqu’un script autre que le script RandomParticipantChoose est sélectionné dans le champ Programme de sélection des participants. Le champ vous permet de fournir une liste d’arguments séparés par des virgules pour le script sélectionné dans le champ Programme de sélection des participants.

* **Utilisateur ou groupe :** la tâche est affectée à l’utilisateur ou au groupe sélectionné. Cette option est disponible lorsque l’option **À un utilisateur ou un groupe spécifique** est activée dans le champ **Options d’affectation**. Le champ répertorie tous les utilisateurs et groupes du groupe d’utilisateurs du processus.\
   Le menu déroulant **Utilisateur ou groupe** répertorie les utilisateurs et les groupes auxquels l’utilisateur connecté a accès. L’affichage du nom d’utilisateur dépend des autorisations d’accès sur le nœud **users** dans crx-repository pour cet utilisateur particulier.

* **[!UICONTROL Envoyer une notification par e-mail :]** sélectionnez cette option pour envoyer des notifications par e-mail à la personne désignée. Ces notifications sont envoyées lorsqu’une tâche est affectée à un utilisateur ou à un groupe. Vous pouvez utiliser l’option **[!UICONTROL Adresse électronique du destinataire]** pour spécifier le mécanisme de récupération de l’adresse électronique.

* **[!UICONTROL Adresse électronique du destinataire :]** vous pouvez stocker l’adresse électronique dans une variable, utiliser un littéral pour spécifier une adresse électronique permanente ou utiliser l’adresse électronique par défaut de la personne désignée spécifiée dans son profil. Vous pouvez utiliser le littéral ou une variable pour spécifier l’adresse électronique d’un groupe. L’option de variable permet de récupérer et d’utiliser de manière dynamique une adresse électronique. L’option **[!UICONTROL Utiliser l’adresse électronique par défaut de la personne désignée]** n’est destinée qu’à une seule personne désignée. Dans ce cas, l’adresse électronique stockée dans le profil utilisateur de la personne désignée est utilisée.

* **Modèle de courrier électronique HTML** : sélectionnez un modèle de courrier électronique pour la notification électronique. Pour modifier un modèle, modifiez le fichier situé à l’emplacement /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt dans le référentiel CRX.
* **Autoriser la délégation à :** la boîte de réception AEM permet à l’utilisateur connecté de déléguer le processus affecté à un autre utilisateur. Vous pouvez déléguer la tâche au sein du même groupe ou à l’utilisateur du processus d’un autre groupe. Si la tâche est affectée à un utilisateur unique et que l’option **Autoriser la délégation aux membres du groupe désigné** est sélectionnée, vous ne pouvez pas déléguer la tâche à un utilisateur ou à un autre groupe.
* **Paramètres de partage :**  AEM boîte de réception propose des options pour partager une ou toutes les tâches de la boîte de réception avec d’autres utilisateurs :
   * Lorsque l’option **Autoriser les personnes désignées à partager explicitement dans la boîte de réception** est sélectionnée, l’utilisateur peut cliquer sur la tâche et la partager avec un autre utilisateur AEM.
   * Lorsque l’option **Autoriser les personnes désignées à partager par l’intermédiaire de la boîte de réception** est sélectionnée et qu’un utilisateur partage ses éléments de boîte de réception ou permet à d’autres utilisateurs d’accéder à ses éléments de boîte de réception, seules les tâches avec l’option ci-dessus activée sont partagées avec d’autres utilisateurs.

* **Actions > Actions par défaut :** les actions d’usine, Envoyer, Enregistrer et Réinitialiser sont disponibles. Par défaut, toutes les actions par défaut sont activées.
* **Variable d’itinéraire :** nom de la variable d’itinéraire. La variable d’itinéraire capture les actions personnalisées qu’un utilisateur sélectionne dans la boîte de réception AEM.
* **Itinéraires :** une tâche peut se composer de plusieurs itinéraires. Lorsque cette option est sélectionnée dans la boîte de réception AEM, l’itinéraire renvoie une valeur et les branches du processus en fonction de l’itinéraire sélectionné. Vous pouvez stocker des itinéraires dans une variable de tableau de type de données Chaîne ou sélectionner **Littéral** pour ajouter manuellement des itinéraires.

* **Titre** : Indiquez le titre de l’itinéraire. Il s’affiche dans la boîte de réception AEM.
* **Icône Corail** : indiquez l’attribut HTML d’une icône corail. La bibliothèque Adobe CoralUI fournit un vaste ensemble d’icônes tactiles. Vous pouvez sélectionner et utiliser une icône pour l’itinéraire. Elle s’affiche avec le titre dans la boîte de réception AEM. Si vous stockez les itinéraires dans une variable, ils utilisent une icône de corail Balises par défaut.
* **Autoriser la personne désignée à ajouter des commentaires** : sélectionnez cette option pour activer les commentaires pour la tâche. Une personne désignée peut ajouter des commentaires à partir de la boîte de réception AEM au moment de l’envoi de la tâche.
* **Enregistrer le commentaire dans la variable :** enregistrez le commentaire dans une variable de type de données String. Cette option s’affiche uniquement si vous cochez la case **Autoriser la personne désignée à ajouter un commentaire**.

* **Autoriser la personne désignée à ajouter des pièces jointes à la tâche** : sélectionnez cette option pour activer les pièces jointes pour la tâche. Une personne désignée peut ajouter des pièces jointes à partir de la boîte de réception AEM au moment de l’envoi de la tâche.
* **Enregistrez les pièces jointes de la tâche de sortie en utilisant** : spécifiez l’emplacement du dossier des pièces jointes. Vous pouvez enregistrer les pièces jointes de la tâche de sortie à l’aide d’un chemin d’accès relatif à la charge utile ou dans une variable de tableau de type de données Document. Cette option s’affiche uniquement si vous cochez la case **Autoriser la personne désignée à ajouter des pièces jointes à la tâche** et sélectionnez **Formulaire adaptatif**, **Formulaire adaptatif en lecture seule** ou **Document PDF non interactif** dans la liste déroulante **Type** l’onglet **Form/Document**.

>[!NOTE]
>
>Utilisez l’onglet Pièces jointes de l’interface utilisateur de l’agent au moment de l’exécution pour associer les pièces jointes à une communication interactive. Les pièces jointes associées s’affichent en tant que pièces jointes de tâche dans le sidekick après l’ouverture de l’élément de travail à l’état Terminé.

* **Utiliser des métadonnées personnalisées :** sélectionnez cette option pour activer le champ de métadonnées personnalisées. Les métadonnées personnalisées sont utilisées dans les modèles de courrier électronique.
* **Métadonnées personnalisées :** sélectionnez une métadonnée personnalisée pour les modèles de courrier électronique. La métadonnée personnalisée est disponible dans le référentiel CRX à l’emplacement apps/fd/dashboard/scripts/metadataScripts. Le chemin spécifié n’existe pas dans le référentiel CRX. Un administrateur crée le chemin d’accès avant de l’utiliser. Vous pouvez également utiliser un service pour les métadonnées personnalisées. Vous pouvez également étendre l’interface WorkitemUserMetadataService pour fournir des métadonnées personnalisées.
* **Afficher les données des étapes précédentes** : sélectionnez cette option pour permettre aux personnes désignées d’afficher les personnes désignées précédentes, les actions déjà effectuées sur la tâche, les commentaires ajoutés à la tâche et le document d’enregistrement de la tâche terminée, le cas échéant.
* **Afficher les données des étapes suivantes :** sélectionnez cette option pour permettre à la personne actuellement désignée d’afficher l’action effectuée et les commentaires ajoutés à la tâche par les personnes désignées suivantes. Cette option permet également à la personne actuellement désignée d’afficher un document d’enregistrement de la tâche terminée, le cas échéant.
* **Visibilité du type de données :** par défaut, une personne désignée peut afficher un document d’enregistrement, des personnes désignées, une action effectuée et les commentaires des personnes désignées précédentes et suivantes qui ont été ajoutés. Utilisez l’option de visibilité du type de données pour limiter le type de données visibles pour les personnes désignées.

## Etape Envoyer un courrier électronique {#send-email-step}

Utilisez l’étape Envoyer un courrier électronique pour, par exemple, envoyer un courrier électronique avec un document d’enregistrement, un lien d’un formulaire adaptatif, un lien d’une communication interactive ou avec un document PDF joint. L’étape Envoyer un courrier électronique prend en charge [le courrier électronique HTML](https://en.wikipedia.org/wiki/HTML_email). Les courriers électroniques HTML sont réactifs et s’adaptent à différents clients de messagerie et tailles d’écran. Vous pouvez utiliser un modèle de courrier électronique HTML pour définir l’aspect, le modèle de couleurs et le comportement du courrier électronique.

L’étape Envoyer un courrier électronique utilise le service de messagerie Day CQ pour envoyer des messages. Avant d’utiliser l’étape Envoyer un courrier électronique, assurez-vous que [le service de messagerie](../../forms/using/aem-forms-workflow.md) est configuré. L’étape Envoyer un courrier électronique possède les propriétés suivantes :

**Titre :** le titre de l’étape permet d’identifier l’étape dans l’éditeur du processus.

**Description :** la description est utile pour d’autres développeurs de processus lorsque vous travaillez dans un environnement de développement partagé.

**Objet du message :** l’objet peut être récupéré à partir des métadonnées d’un workflow, spécifié manuellement ou récupéré à partir de la valeur stockée dans une variable. Faites votre choix parmi les options suivantes :

* **Littéral :** spécifiez manuellement un objet.
* **Récupérer à partir des métadonnées du processus** : récupérez l’objet d’une propriété de métadonnées.
* **Variable** : récupérez l’objet de la valeur stockée dans une variable de type de données Chaîne.

**Modèle de courrier électronique HTML** : modèle HTML pour le courrier électronique. Vous pouvez spécifier des variables dans un modèle de courrier électronique. L’étape Envoyer un courrier électronique extrait et affiche toutes les variables incluses dans un modèle pour les entrées.

**Métadonnées du modèle de courrier électronique :**  la valeur des variables du modèle de courrier électronique peut être une valeur spécifiée par l’utilisateur, le chemin d’accès d’une ressource sur le serveur de création ou de publication, une image ou une propriété de métadonnées de workflow.

* **Littéral** : utilisez cette option lorsque vous connaissez la valeur exacte à spécifier. Par exemple, [example@example.com](mailto:example@example.com).

* **Métadonnées de processus :** utilisez cette option lorsque la valeur à utiliser est enregistrée dans une propriété de métadonnées de processus. Après avoir sélectionné cette option, saisissez le nom de la propriété des métadonnées dans la zone de texte vide en dessous de l’option Métadonnées de processus. Par exemple, emailAddress.
* **URL de la ressource :** utilisez cette option pour incorporer un lien web d’une communication interactive dans l’email. Après avoir sélectionné l’option, recherchez et sélectionnez la communication interactive à incorporer. Un actif peut résider sur le serveur de création ou de publication.
* **Image :** utilisez cette option pour inclure une image au courrier électronique. Après avoir sélectionné cette option, recherchez et sélectionnez l’image. L’option image est uniquement disponible pour les balises d’image (&lt;img src=&quot;*&quot;/>) disponibles dans le modèle du courrier électronique.

**Adresse électronique de l’expéditeur/du destinataire :** sélectionnez l’option  **** Littéralité pour spécifier manuellement une adresse électronique ou sélectionnez l’option  **Récupérer à partir des** métadonnées de workflow pour récupérer l’adresse électronique à partir d’une propriété de métadonnées. Vous pouvez également spécifier une liste de tableaux de propriété de métadonnées pour l’option **Récupérez à partir des métadonnées de processus**. Sélectionnez l’option **Variable** pour récupérer l’adresse électronique à partir de la valeur stockée dans une variable de type de données Chaîne.

**Pièce jointe :** la ressource disponible à l’emplacement spécifié est jointe au courrier électronique. Le chemin d’accès de l’actif peut être lié à la charge utile ou au chemin d’accès absolu. Voici un exemple de chemin d’accès : [Répertoire_Charge_utile]/attachments/.

Sélectionnez l’option **Variable** pour récupérer le fichier joint stocké dans une variable de type de données Document, XML ou JSON.

**Nom de fichier :** nom du fichier de la pièce jointe au courrier électronique. L’étape Envoyer un courrier électronique remplace le nom de fichier original de la pièce jointe par le nom de fichier spécifié. Le nom peut être spécifié manuellement ou récupéré à partir d’une propriété de métadonnées de processus ou d’une variable. Utilisez l’option **Littéral** lorsque vous connaissez la valeur exacte à spécifier. Utilisez l’option **Variable** pour récupérer le nom du fichier à partir de la valeur stockée dans une variable de type de données Chaîne. Utilisez l’option **Récupérer à partir des métadonnées de processus** lorsque la valeur à utiliser est enregistrée dans une propriété de métadonnées de processus.

## Etape Générer un document d’enregistrement {#generate-document-of-record-step}

Lorsqu’un formulaire est rempli ou envoyé, vous pouvez conserver un enregistrement du formulaire, au format imprimé ou au format de document. On parle ici de document d’enregistrement (DOR). Vous pouvez utiliser l’étape Générer un document d’enregistrement pour créer une version PDF interactive ou en lecture seule d’un formulaire adaptatif. La version PDF contient des informations remplies dans le formulaire avec la mise en page du formulaire adaptatif.

L’étape Document d’enregistrement possède les propriétés suivantes :

**Utiliser le formulaire** adaptatif : Spécifiez la méthode pour localiser le formulaire adaptatif d’entrée. Vous pouvez utiliser le formulaire adaptatif envoyé au workflow, disponible à un chemin d’accès absolu ou disponible à un chemin d’accès dans une variable. Vous pouvez utiliser une variable de type de données Chaîne pour spécifier le chemin d’accès dans le champ **Sélectionner la variable à résoudre**.\
Vous pouvez associer plusieurs formulaires adaptatifs à un workflow. Par conséquent, vous pouvez spécifier un formulaire adaptatif au moment de l’exécution à l’aide des méthodes d’entrée disponibles.

**Chemin d’accès du formulaire adaptatif** : indiquez le chemin d’accès du formulaire adaptatif. Le champ est disponible lorsque vous sélectionnez l’option **Disponible à un chemin d’accès absolu** dans le champ **Utiliser le formulaire adaptatif**.

**Sélectionnez Input data using :** chemin des données d’entrée pour le formulaire adaptatif. Vous pouvez conserver les données à un emplacement relatif à la charge utile, spécifier un chemin d’accès absolu aux données ou récupérer les données stockées dans une variable de type Document, JSON ou XML. Les données d’entrée sont fusionnées avec le formulaire adaptatif pour créer un document d’enregistrement.

**Sélectionnez Input attachment path using:** Chemin d’accès des pièces jointes. Ces pièces jointes sont incluses dans le document d’enregistrement. Vous pouvez conserver les pièces jointes à un emplacement relatif à la charge utile, spécifier un chemin absolu pour les pièces jointes ou récupérer les pièces jointes stockées dans une variable de tableau de type de données Document.

Si vous spécifiez le chemin d’accès d’un dossier (des pièces jointes, par exemple), tous les fichiers directement disponibles dans le dossier sont joints au document d’enregistrement. Si des fichiers sont présents dans les dossiers directement disponibles dans le chemin d’accès de la pièce jointe spécifiée, les fichiers sont inclus dans le document d’enregistrement en tant que pièces jointes. Les dossiers présents dans les dossiers directement disponibles sont ignorés.

**Enregistrer le document d’enregistrement généré à l’aide des options ci-dessous :** spécifiez l’emplacement de conservation d’un fichier de document d’enregistrement. Vous pouvez choisir de remplacer le dossier de charge utile, de placer le document d’enregistrement à un emplacement dans le répertoire de charge utile ou de stocker le document d’enregistrement dans une variable de type de données Document .

**Paramètre régional** : spécifiez la langue du document d’enregistrement. Sélectionnez **Littéral** pour sélectionner le paramètre régional dans une liste déroulante ou **Variable** pour récupérer le paramètre régional à partir de la valeur stockée dans une variable de type de données Chaîne. Vous devez définir le code de la langue lors du stockage de la valeur de la langue dans une variable. Par exemple, spécifiez **en_US** pour l’anglais et **fr_FR** pour le français.

## Etape Invoquer le service de modèle de données de formulaire {#invoke-form-data-model-service-step}

Vous pouvez utiliser l’[intégration de données AEM Forms](../../forms/using/data-integration.md) pour configurer des sources de données disparates et vous y connecter. Ces sources de données peuvent être une base de données, un service Web, un service REST, un service OData et une solution CRM. L’intégration de données AEM Forms vous permet de créer un modèle de données de formulaire regroupant plusieurs services afin d’effectuer des opérations de récupération, d’ajout et de mise à jour de données sur la base de données configurée. Vous pouvez utiliser **l’étape Invoquer le service de modèle de données de formulaire** pour sélectionner un modèle de données de formulaire (FDM) et utiliser les services du FDM pour récupérer, mettre à jour ou ajouter des données aux sources de données disparates.

Pour mieux comprendre les entrées des champs de l’étape, la table de base de données et le fichier JSON suivants sont utilisés à titre d’exemple :

**Exemple de table CustomerDetails**

<table>
 <tbody> 
  <tr> 
   <td>Propriété</td> 
   <td>Valeur<br /> </td> 
  </tr> 
  <tr> 
   <td>Prénom<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Nom de famille</td> 
   <td>Rose</td> 
  </tr> 
  <tr> 
   <td>ID de client</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Adresse électronique<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**Exemple de fichier JSON**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

L’étape Invoquer le service de modèle de données de formulaire contient les champs suivants pour faciliter les opérations du modèle de données de formulaire :

* **Titre :** titre de l’étape. Il permet d’identifier l’étape dans l’éditeur du processus.
* **Description :** la description est utile pour d’autres développeurs de processus lorsque vous travaillez dans un environnement de développement partagé.

* **Chemin d’accès du modèle de données de formulaire** : recherchez et sélectionnez un modèle de données de formulaire présent sur le serveur.

* **Service** : liste des services fournit par le modèle de données de formulaire sélectionné.
* **Entrée des services > Fournir des données d’entrée à l’aide d’un fichier JSON, de l’option Littéral,d’une variable, de métadonnées de processus** : un service peut avoir plusieurs arguments. Sélectionnez cette option pour obtenir la valeur des arguments de service à partir d’une propriété de métadonnées de processus, d’un objet JSON ou d’une variable, ou saisissez directement la valeur dans la zone prévue à cet effet :

   * **Littéral** : utilisez cette option lorsque vous connaissez la valeur exacte à spécifier. Par exemple, srose@we.info.
   * **Variable :** utilisez l’option pour récupérer la valeur stockée dans une variable.
   * **Récupérer à partir des métadonnées de processus :** utilisez cette option lorsque la valeur à utiliser est enregistrée dans une propriété de métadonnées de processus. Par exemple, emailAddress.
   * **[!UICONTROL Relatif à la charge utile]** : Utilisez l’option pour récupérer la pièce jointe de fichier enregistrée à un chemin d’accès relatif à la charge utile. Sélectionnez l’option et indiquez le nom du dossier contenant la pièce jointe ou indiquez le nom de la pièce jointe dans la zone de texte.

      Par exemple, si le dossier Relatif à la charge utile dans le référentiel CRX inclut une pièce jointe à l’emplacement `attachment\attachment-folder` , spécifiez `attachment\attachment-folder` dans la zone de texte après avoir sélectionné l’option **[!UICONTROL Relative à la charge utile]** .
   * **JSON Dot Notation :** utilisez cette option lorsque la valeur à utiliser figure dans un fichier JSON. Par exemple, insurance.customerDetails.emailAddress. L’option JSON Dot Notation n’est disponible que si l’option Mapper les champs de saisie de l’entrée JSON est sélectionnée.
   * **Mapper les champs de saisie depuis le fichier JSON d’entrée :** spécifiez le chemin d’accès d’un fichier JSON pour obtenir la valeur d’entrée des arguments de service à partir du fichier JSON. Le chemin d’accès du fichier JSON peut être relatif à la charge utile, un chemin absolu, ou vous pouvez sélectionner un document JSON d’entrée à l’aide d’une variable de type JSON ou Modèle de données de formulaire.

* **Entrée pour les services > Fournir des données d’entrée à l’aide d’une variable ou d’un fichier JSON :** sélectionnez l’option permettant d’obtenir des valeurs pour tous les arguments à partir d’un fichier JSON enregistré à un chemin absolu, à un chemin relatif à la charge utile ou dans une variable.
* **Sélectionnez le document JSON d’entrée en utilisant** : fichier JSON contenant des valeurs pour tous les arguments de service. Le chemin d’accès du fichier JSON peut être **relatif à la charge utile** ou à un **chemin d’accès absolu.** Vous pouvez également récupérer le document JSON d’entrée à l’aide d’une variable de type de données JSON ou Modèle de données de formulaire.

* **JSON Dot Notation :** laissez le champ vide pour utiliser tous les objets du fichier JSON spécifié en tant qu’entrée pour les arguments de service. Pour lire un objet JSON spécifique à partir du fichier JSON spécifié en tant qu’entrée pour des arguments de service, spécifiez la notation par point pour l’objet JSON. Par exemple, si vous avez un fichier JSON identique à l’un des fichiers indiqué au début de la section, spécifiez insurance.customerDetails pour fournir tous les détails d’un client en tant qu’entrée du service.
* **Sortie de service > Mapper et écrire les valeurs de sortie dans une variable ou une métadonnée :** sélectionnez l’option pour enregistrer les valeurs de sortie en tant que propriétés du noeud de métadonnées de l’instance de workflow dans le référentiel crx-repository. Spécifiez le nom de la propriété de métadonnées et sélectionnez l’attribut de sortie de service correspondant à mapper avec la propriété de métadonnées, par exemple, mappez la valeur numéro_de_téléphone renvoyé par le service de sortie avec la propriété numéro_de_téléphone des métadonnées du processus. De même, vous pouvez stocker la sortie dans une variable de type données Long. Lorsque vous sélectionnez une propriété pour l’attribut **[!UICONTROL Service output à mapper]**, seules les variables capables de stocker les données de la propriété sélectionnée sont renseignées pour l’option **[!UICONTROL Save the output to]**.

* **Sortie de service > Enregistrer la sortie dans une variable ou un fichier JSON :**  sélectionnez l’option permettant d’enregistrer les valeurs de sortie dans un fichier JSON à un chemin d’accès absolu, à un chemin d’accès relatif à la charge utile ou dans une variable .
* **Enregistrez le document JSON de sortie à l’aide des options ci-dessous :** enregistrez le fichier JSON de sortie. Le chemin d’accès du fichier JSON peut être relatif à la charge utile ou à un chemin d’accès absolu. Vous pouvez également enregistrer le fichier JSON de sortie à l’aide d’une variable de type de données JSON ou Modèle de données de formulaire.

## Etape Signer le document {#sign-document-step}

L’étape Signer le document vous permet d’utiliser Adobe Sign pour signer des documents. L’étape Signer le document possède les propriétés suivantes :

* **Nom du contrat :** indiquez le titre du contrat. Le nom du contrat devient une partie de l’objet et du corps du courrier électronique envoyé aux signataires. Vous pouvez soit stocker le nom dans une variable de type de données Chaîne, soit sélectionner **Littéral** pour l’ajouter manuellement.

* **Paramètre régional :** spécifiez la langue pour les options de messagerie et de vérification. Vous pouvez stocker le paramètre régional dans une variable de type de données Chaîne ou sélectionner **Littéral** pour choisir le paramètre régional dans la liste des options disponibles. Vous devez définir le code de la langue lors du stockage de la valeur de la langue dans une variable. Par exemple, spécifiez **en_US** pour l’anglais et **fr_FR** pour le français.

* **Configuration cloud Adobe Sign** : sélectionnez une configuration cloud Adobe Sign. Si vous n’avez pas configuré Adobe Sign pour AEM Forms, voir [Intégrer Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Sélectionner le document à signer à l’aide :**  vous pouvez choisir un document à partir d’un emplacement relatif à la charge utile, utiliser la charge utile comme document, spécifier un chemin d’accès absolu du document ou récupérer le document stocké dans une variable de type de données Document.
* **Jours avant l’échéance :** un document est marqué comme dû (délai expiré) lorsqu’il n’y a plus aucune activité sur la tâche pour le nombre de jours spécifié dans le champ **Jours avant l’échéance.** Le nombre de jours est calculé à partir du jour de l’affectation du document à un utilisateur pour signature.
* **Fréquence des messages de rappel :** vous pouvez envoyer un message de rappel à intervalle quotidien ou hebdomadaire. La semaine est calculée à compter du jour de l’affectation du document à un utilisateur pour signature.
* **Processus de signature :** vous pouvez signer un document dans un ordre séquentiel ou parallèle. Dans un ordre séquentiel, un signataire à la fois reçoit le document à signer. Une fois que le premier signataire a terminé la signature du document, il est envoyé au signataire suivant, et ainsi de suite. Dans l’ordre parallèle, plusieurs signataires signent un document en même temps.
* **URL de redirection :** spécifiez une URL de redirection. Une fois le document signé, vous pouvez rediriger la personne désignée vers une URL. En général, cette URL contient un message de remerciement ou des instructions supplémentaires.
* **Phase de processus :** un processus peut se composer de plusieurs phases. Ces phases sont affichées dans la boîte de réception AEM. Vous pouvez définir ces phases dans les propriétés du modèle (Sidekick > Page > Propriétés de la page > Phases).
* **Sélectionner les signataires :** indiquez la méthode utilisée pour sélectionner des signataires pour le document. Vous pouvez affecter de manière dynamique le processus à un utilisateur ou à un groupe ou ajouter manuellement les informations d’un signataire.
* **Script ou service pour sélectionner les signataires :** cette option est disponible uniquement si l’option De manière dynamique est sélectionnée dans le champ Sélectionner les signataires. Vous pouvez spécifier un script ECMAScript ou un service pour sélectionner des signataires et des options de vérification pour un document.
* **Détails du signataire :** cette option est disponible uniquement si l’option Manuellement est sélectionnée dans le champ Sélectionner les signataires. Indiquez l’adresse électronique et choisissez une méthode de vérification facultative. Avant de sélectionner une méthode de vérification en 2 étapes, assurez-vous que l’option de vérification correspondante est activée pour le compte Adobe Sign configuré. Vous pouvez utiliser une variable de type String pour définir des valeurs pour les champs **[!UICONTROL Email]**, **[!UICONTROL Code pays]** et **[!UICONTROL Numéro de téléphone]**. Les champs **[!UICONTROL Code pays]** et **[!UICONTROL Numéro de téléphone]** s’affichent uniquement si vous sélectionnez **[!UICONTROL Vérification de téléphone]** dans la liste déroulante **[!UICONTROL Vérification en 2 étapes]**.
* **Variable d’état :** un document activé par Adobe Sign stocke l’état de signature du document dans une variable de type de données String. Spécifiez le nom de la variable d’état (adobeSignStatus). Une variable d’état d’une instance est disponible dans CRXDE à l’adresse /etc/workflow/instances/&lt;serveur>/&lt;date-time>/&lt;instance du modèle de processus>/workItems/&lt;noeud>/metaData contient l’état d’une variable.
* **Enregistrer le document signé à l’aide des options ci-dessous :** spécifiez l’emplacement de conservation des documents signés. Vous pouvez choisir de remplacer le fichier de charge utile, de placer le document signé à un emplacement dans le répertoire de charge utile ou de stocker le document signé dans une variable de type Document .

## Etapes Services de document {#document-services-steps}

Les services de document AEM sont un ensemble de services permettant de créer, d’assembler et de sécuriser des documents PDF. AEM Forms fournit une étape AEM processus distincte pour chaque service de document.

Comme pour d’autres étapes de processus AEM Forms, telles que Affecter une tâche, Envoyer un courrier électronique et Signer un document, vous pouvez utiliser des variables dans toutes les étapes AEM Document Services. Pour plus d’informations sur la création et la gestion des variables, voir [Variables dans AEM workflows](../../forms/using/variable-in-aem-workflows.md).

### Étape Appliquer l’horodatage du document {#apply-document-time-stamp-step}

Ajoute un horodatage à un document. Indiquez les détails du document, tels que le chemin d’accès du document d’entrée, le nom du document d’entrée, l’emplacement de stockage des données exportées. Vous pouvez choisir de remplacer un fichier de charge utile existant, de choisir un nom de fichier différent pour stocker les données dans un autre fichier sous le dossier de charge utile, de fournir un chemin d’accès absolu aux données ou de stocker les données dans une variable de type de données Document .

### Etape Convertir en image {#convert-to-image-step}

Convertit un document PDF en liste d’images. Les formats d’image pris en charge sont JPEG, JPEG2000, PNG et TIFF. Les informations suivantes s’appliquent aux conversions en images TIFF :

* Un fichier TIFF de plusieurs pages est généré.
* Certaines annotations ne sont pas incluses dans les images TIFF. Les annotations requises par Acrobat pour générer leur aspect ne sont pas incluses.

### Etape Convertir en PDF/A {#convert-to-pdf-a-step}

Convertit un document PDF au format PDF/A à l’aide des options fournies. La version PDF/A du format PDF (Portable Document Format) est réservée à l’archivage et la conservation des documents à long terme.

### Etape Convertir en PS {#convert-to-ps-step}

Convertir des documents PDF en PostScript. Lors d’une conversion au format PostScript, vous pouvez indiquer le document source et choisir entre une conversion vers PostScript niveau 2 ou 3. Le document PDF à convertir en fichier PostScript ne doit pas être interactif.

### Etape Créer le PDF depuis le type spécifié {#create-pdf-from-specified-type-step}

Génère un document PDF à partir d’un fichier d’entrée. Le document d’entrée peut être relatif à la charge utile, comporter un chemin d’accès absolu, une charge utile elle-même ou être stocké dans une variable de type de données Document .

### Etape Créer un fichier PDF depuis l’URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Génère un document PDF à partir de l’URL fournie ou du fichier HTML et ZIP.

### Etape Exporter des données {#export-data-step}

Exporte des données à partir d’un formulaire PDF ou d’un XDP. Vous devez saisir le chemin d’accès du document d’entrée et le format d’exportation des données. Les options Exporter le format de données sont Auto, XDP et XmlData.

### Etape Exporter un PDF vers le type spécifié {#export-pdf-to-specified-type-step}

Convertit un document PDF au format sélectionné.

### Etape Générer un PDF non interactif {#generatenoninteractive}

Génère un PDF non interactif. Cette étape comprend différentes options de personnalisation.

>[!NOTE]
>
>Vous pouvez utiliser des variables pour spécifier le fichier de modèle pour les documents d’entrée. Conservez le chemin d’accès du fichier de modèle dans une variable de type Données de chaîne .

### Etape Importer des données {#import-data-step}

Fusionne les données de formulaire dans un formulaire PDF. Vous pouvez importer les données de formulaire dans un formulaire au format PDF.

### Etape Invoquer DDX {#invokeddx}

Exécute le fichier DDX sur la carte spécifiée des documents d’entrée et renvoie les documents PDF ayant fait l’objet d’une manipulation.

>[!NOTE]
>
>Vous pouvez utiliser des variables pour spécifier le fichier DDX pour les documents d’entrée. Stockez le fichier DDX dans une variable de type Document ou Données XML.

### Etape Optimiser un PDF {#optimize-pdf-step}

Optimise les fichiers PDF en réduisant leur taille. Le résultat de cette conversion est un fichier PDF qui peut être plus petit que ses versions d’origine. Cette opération permet également de convertir des documents PDF vers la version PDF spécifiée dans les paramètres d’optimisation.

Les paramètres d’optimisation spécifient le mode d’optimisation des fichiers. Voici des exemples de paramètres :

* Version PDF cible
* Ignorer les objets tels que les actions JavaScript et les miniatures de page incorporées
* Ignorer les données utilisateur telles que les commentaires et les pièces jointes
* Ignorer les paramètres non valides ou inutilisés
* Compression de données non compressées ou utilisation d’algorithmes de compression plus efficaces
* Suppression des polices incorporées
* Définition des valeurs de transparence

### Etape Effectuer un rendu de formulaire PDF {#renderpdf}

Enregistre un formulaire créé dans Form Designer (XDP) dans un formulaire PDF.

>[!NOTE]
>
>Vous pouvez utiliser des variables pour spécifier le fichier de modèle pour les documents d’entrée. Conservez le chemin d’accès du fichier de modèle dans une variable de type Données de chaîne .

### Etape Protéger un document {#secure-document-step}

Chiffre, signe et certifie un document. AEM Forms prend en charge le chiffrement par mot de passe et au moyen d’un certificat. Vous pouvez également choisir entre plusieurs algorithmes pour signer des documents. SHA-256 et SH-512, par exemple. Vous pouvez également utiliser l’étape de processus pour étendre Reader aux documents PDF. L’étape de processus propose une option qui permet d’activer le décodage de code-barres, les signatures numériques, l’importation et l’exportation de données au format PDF et d’autres options.

### Etape Envoyer à l’imprimante {#send-to-printer-step}

Envoie un document directement à une imprimante. Cette étape prend en charge les systèmes d’accès aux imprimantes suivants :

* **Imprimante accessible directement** : une imprimante installée sur l’ordinateur utilisé est appelée imprimante accessible directement et l’ordinateur est appelé hôte de l’imprimante. Il peut s’agir d’une imprimante locale directement reliée à l’ordinateur.
* **Imprimante accessible indirectement** : l’imprimante installée sur un serveur d’impression est accessible depuis d’autres ordinateurs. Les technologies de type CUPS (Common Unix® Printing System) et le protocole LPD (Line Printer Daemon) permettent de se connecter à une imprimante réseau. Pour accéder à une imprimante accessible indirectement, indiquez l’adresse IP ou le nom d’hôte du serveur d’impression. Ainsi, vous pouvez envoyer un document vers un URI LPD lorsqu’un protocole LDP s’exécute sur le réseau. Ce système vous permet d’acheminer le document vers n’importe quelle imprimante connectée au réseau qui exécute un protocole LDP.

### Générer l’étape de sortie imprimée {#generatePrintedOutput}

L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL à partir d’une conception de formulaire et d’un fichier de données. Le fichier de données est fusionné avec la conception de formulaire et mis en forme pour l’impression. La sortie générée par cette étape peut être envoyée directement à une imprimante ou enregistrée en tant que fichier. Il est recommandé d’utiliser cette étape lorsque vous souhaitez utiliser des conceptions de formulaire ou des données provenant d’une application. Si vos conceptions de formulaire se trouvent sur le réseau, le système de fichiers local ou l’emplacement HTTP, utilisez l’opération generatePrintedOutput .

Par exemple, votre application nécessite la fusion d’une conception de formulaire avec un fichier de données. Les données contiennent des centaines d’enregistrements. En outre, la sortie doit être envoyée à une imprimante prenant en charge ZPL. La conception de formulaire et vos données d’entrée se trouvent dans une application. Utilisez l’opération generatePrintedOutput pour fusionner chaque enregistrement avec une conception de formulaire et envoyer la sortie à une imprimante prenant en charge ZPL.

L’étape Générer une sortie imprimée présente les propriétés suivantes :

**Propriétés d’entrée**

* **[!UICONTROL Sélectionnez le fichier de modèle à l’aide de]** : Spécifiez le chemin d’accès au fichier de modèle. Vous pouvez sélectionner le fichier de modèle à l’aide du chemin relatif à la charge utile, enregistré dans un chemin d’accès absolu ou à l’aide d’une variable de type de données Document . Par exemple, [Payload_Directory]/Workflow/data.xml. Si le chemin n’existe pas dans le référentiel crx, un administrateur peut créer le chemin avant de l’utiliser. De plus, vous pouvez également accepter la payload comme fichier de données d’entrée.

* **[!UICONTROL Sélectionnez le document de données à l’aide de]** : Spécifiez le chemin d’accès d’un fichier de données d’entrée. Vous pouvez sélectionner le fichier de données d’entrée à l’aide du chemin relatif à la charge utile, enregistré dans un chemin d’accès absolu ou à l’aide d’une variable de type de données Document . Par exemple, [Payload_Directory]/Workflow/data.xml. Si le chemin n’existe pas dans le référentiel crx, un administrateur peut créer le chemin avant de l’utiliser.

* **[!UICONTROL Format]** d’imprimante : Une valeur Print Format qui spécifie le langage de description de page à utiliser, lorsqu’un fichier XDC n’est pas fourni, pour générer le flux de sortie. Si vous fournissez une valeur littérale, sélectionnez l’une de ces valeurs :

   * **[!UICONTROL Custom PCL]** : Utilisez cette option pour spécifier un fichier XDC personnalisé pour PCL.
   * **[!UICONTROL PostScript personnalisé]** : Utilisez cette option pour spécifier un fichier XDC personnalisé pour PostScript.
   * **[!UICONTROL ZPL]** personnalisé : Utilisez cette option pour spécifier un fichier XDC personnalisé pour ZPL.
   * **[!UICONTROL Generic Color PCL (5c)]** : Utilisez une couleur générique PCL (5c).
   * **[!UICONTROL PostScript Level3]** générique : Utilisez PostScript Level 3 générique.
   * **[!UICONTROL ZPL 300 DPI]** : Utilisez ZPL 300 DPI. Le fichier zpl300.xdc est utilisé.
   * **[!UICONTROL ZPL 600 DPI]** : Utilisez ZPL 600 DPI. Le fichier zpl600.xdc est utilisé.
   * **[!UICONTROL Custom IPL]** : Utilisez cette option pour spécifier un fichier XDC personnalisé pour IPL.
   * **[!UICONTROL IPL 300 DPI]** : Utilisez IPL 300 DPI. Le fichier ipl300.xdc est utilisé.
   * **[!UICONTROL IPL 400 DPI]** : Utilisez IPL 400 DPI. Le fichier ipl400.xdc est utilisé.
   * **[!UICONTROL Custom TPCL]** : Utilisez cette option pour spécifier un fichier XDC personnalisé pour TPCL.
   * **[!UICONTROL TPCL 305 DPI]** : Utilisez TPCL 300 DPI. Le fichier tpcl305.xdc est utilisé.
   * **[!UICONTROL PCL 600 DPI]** : Utilisez TPCL 600 DPI. Le fichier tpcl600.xdc est utilisé.
   * **[!UICONTROL DPL]** personnalisé : Utilisez l’option pour spécifier un fichier XDC personnalisé DPL.
   * **[!UICONTROL DPL300DPI]** : Utilisez DPL 300 DPI. Le fichier dpl300.xdc est utilisé.
   * **[!UICONTROL DPL406DPI]** : Utilisez DPL 400 DPI. Le fichier dpl406.xdc est utilisé.
   * **[!UICONTROL DPL600DPI]** : Utilisez DPL 600 DPI. Le fichier dpl600.xdc est utilisé.

**Propriétés de sortie**

* **[!UICONTROL Enregistrez le document de sortie à l’aide de]** : Indiquez l’emplacement d’enregistrement du fichier de sortie. Vous pouvez enregistrer le fichier de sortie à un emplacement relatif à la charge utile, dans une variable, ou spécifier un emplacement absolu pour enregistrer le fichier de sortie. Si le chemin n’existe pas dans le référentiel crx, un administrateur peut créer le chemin avant de l’utiliser.

**Propriétés avancées**

* **[!UICONTROL Sélectionnez l’emplacement racine du contenu à l’aide de]** : La racine du contenu est une valeur string qui spécifie l’URI, la référence absolue ou l’emplacement dans le référentiel pour récupérer les ressources relatives utilisées par la conception de formulaire. Par exemple, si la conception de formulaire fait relativement référence à une image, comme ../myImage.gif, le fichier myImage.gif doit être situé dans repository://. La valeur par défaut est repository://, qui pointe vers le niveau racine du référentiel.

   Lorsque vous sélectionnez une ressource dans votre application, le chemin d’accès de l’URI de la racine du contenu doit présenter la structure appropriée. Par exemple, si un formulaire est sélectionné à partir d’une application nommée SampleApp et placé dans SampleApp/1.0/forms/Test.xdp, l’URI de la racine du contenu doit être spécifié comme suit : repository://administrator@password/Applications/SampleApp/1.0/forms/ ou repository:/Applications/SampleApp/1.0/forms/ (lorsque l’autorité est nulle). Lorsque l’URI de la racine de contenu est spécifié de cette manière, les chemins d’accès de toutes les ressources référencées dans le formulaire seront résolus par rapport à cet URI.

* **[!UICONTROL Sélectionnez le fichier XCI à l’aide de]** : Les fichiers XCI sont utilisés pour décrire les polices et les autres propriétés utilisées pour les éléments de conception de formulaire. Vous pouvez conserver un fichier XCI relatif à la charge utile, à un chemin d’accès absolu ou à l’aide d’une variable de type de données Document .

* **[!UICONTROL Paramètres régionaux]** : Indique la langue utilisée pour générer le document PDF. Si vous fournissez une valeur littérale, sélectionnez une langue dans la liste ou l’une de ces valeurs :
   * **Pour utiliser la valeur par défaut** du serveur : (Par défaut) Utilisez le paramètre Paramètres régionaux configuré sur le serveur AEM Forms. Le paramètre Paramètres régionaux est configuré à l’aide d’Administration Console. (Voir l’[aide de Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **Pour utiliser une valeur** personnalisée : Saisissez le code de paramètres régionaux dans la zone littérale ou sélectionnez une variable de chaîne contenant le code de paramètres régionaux. Pour obtenir une liste complète des codes des paramètres régionaux pris en charge, voir http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]** : Une valeur entière qui spécifie le nombre de copies à générer pour la sortie. La valeur par défaut est 1.

* **[!UICONTROL impression recto verso]** : Une valeur Pagination qui spécifie s’il faut utiliser l’impression recto ou recto verso. Les imprimantes prenant en charge PostScript et PCL utilisent cette valeur. Si vous fournissez une valeur littérale, sélectionnez l’une de ces valeurs :
   * **[!UICONTROL Duplex Long Edge]** : Utilisez l’impression recto verso et imprimez à l’aide de la pagination sur le bord long.
   * **[!UICONTROL Duplex Short Edge]** : Utilisez l’impression recto verso et imprimez à l’aide de la pagination sur le bord court.
   * **[!UICONTROL Simplex]** : Utilisez l’impression recto.
