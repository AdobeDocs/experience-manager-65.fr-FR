---
title: Processus basé sur l’utilisation de Forms sur OSGi
description: Utiliser un processus AEM Forms pour automatiser et créer rapidement des révisions et des approbations pour les services de document de début
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3667'
ht-degree: 100%

---

# Processus basé sur l’utilisation de Forms sur OSGi{#forms-centric-workflow-on-osgi}

![hero-image](do-not-localize/header.png)

Les entreprises collectent les données à partir de centaines, voire de milliers de formulaires, de différents systèmes principaux et de sources de données en ligne ou hors ligne. Elles disposent également d’un ensemble dynamique de personnes pour prendre des décisions concernant les données, qui impliquent les processus de révision et d’approbation itératifs.

Avec les workflows de révision et d’approbation pour les audiences internes et externes, les grandes entreprises sont soumises à des tâches répétitives. Par exemple, la conversion d’un document PDF dans un autre format. Ces tâches prennent beaucoup de temps et mobilisent un grand nombre de ressources lorsqu’elles sont effectuées manuellement. Les entreprises ont également des obligations légales consistant à signer numériquement un document et à archiver des données de formulaire pour une utilisation ultérieure dans des formats prédéfinis.

## Présentation du processus basé sur l’utilisation de Forms sur OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Vous pouvez utiliser des workflows AEM pour créer rapidement des workflows basés sur des formulaires adaptatifs. Ces workflows peuvent être utilisés pour la révision et l’approbation, les flux de processus métier, le démarrage de Documents Services, l’intégration du processus de signature Adobe Sign et des opérations similaires. Par exemple, le traitement des demandes de carte de crédit, les workflows d’approbation de congés du personnel et l’enregistrement d’un formulaire en tant que document PDF. De plus, ces workflows peuvent être utilisés dans une entreprise ou sur le pare-feu réseau.

Avec le processus basé sur l’utilisation de Forms on OSGi, vous pouvez rapidement créer et déployer des processus pour différentes tâches sur la pile OSGi, sans avoir à installer la fonctionnalité Process Management complète sur la pile JEE. Le développement et la gestion des workflows utilisent les fonctionnalités de boîte de réception AEM et de workflows AEM habituelles. Les processus forment la base de l’automatisation des processus réels d’entreprise, qui s’étendent sur plusieurs systèmes logiciels, réseaux, services et même organisations.

Une fois configurés, ces workflows peuvent être déclenchés manuellement pour terminer une exécution ou un processus définis par programmation lorsque les personnes envoient un formulaire ou une lettre [Correspondence Management](/help/forms/using/cm-overview.md). Avec des fonctionnalités de workflow AEM améliorées, AEM Forms offre deux fonctionnalités distinctes mais similaires. Dans le cadre de votre stratégie de déploiement, vous devez décider laquelle vous convient le mieux. Référez-vous à la [comparaison](capabilities-osgi-jee-workflows.md) des workflows centrés sur les formulaires AEM sur OSGi et de la gestion des processus sur JEE. De plus, pour la topologie de déploiement, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

Le processus basé sur l’utilisation de Forms sur OSGi étend la [boîte de messagerie AEM](/help/sites-authoring/inbox.md) et fournit des composants supplémentaires (étapes) pour que l’éditeur du processus AEM ajoute la prise en charge des processus AEM basés sur l’utilisation d’AEM Forms. La boîte de réception AEM étendue dispose de fonctionnalités similaires à celles de l’[espace de travail AEM Forms](introduction-html-workspace.md). Avec la gestion des workflows basés sur l’intervention humaine (approbation, révision, etc.), vous pouvez utiliser des workflows AEM pour automatiser les opérations liées à [Document Services](/help/sites-developing/workflows-step-ref.md) (par exemple, la génération de PDF) et à la signature de documents (Adobe Sign) par voie électronique.

Toutes les étapes des processus AEM Forms prennent en charge l’utilisation de variables. Les variables permettent aux étapes de processus de contenir et de transmettre des métadonnées entre les étapes au moment de l’exécution. Vous pouvez créer différents types de variables pour stocker différents types de données. Vous pouvez également créer des collections de variables pour stocker plusieurs instances de données associées et du même type. En règle générale, vous utilisez une variable ou une collection de variables lorsque vous devez prendre une décision en fonction de la valeur qu’elle contient ou pour stocker des informations dont vous aurez besoin ultérieurement dans un processus. Pour plus d’informations sur l’utilisation de variables dans ces composants (étapes) de processus basés sur Forms, voir [Processus basé sur l’utilisation de Forms sur OSGi - Guide de référence des étapes](../../forms/using/aem-forms-workflow-step-reference.md). Pour plus d’informations sur la création et la gestion des variables, voir [Variables dans les processus AEM](../../forms/using/variable-in-aem-workflows.md).

Le diagramme suivant illustre le processus complet de création, d’exécution et contrôle d’un processus basé sur l’utilisation de Forms sur OSGi.

![introduction-à-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Avant de commencer {#before-you-start}

* Un workflow est une représentation d’un processus métier réel. Préparez votre processus métier réel et la liste des personnes participant au processus métier. Par ailleurs, préparez les éléments associés (formulaires adaptatifs, documents PDF, etc.) avant de créer un workflow.
* Un workflow peut se composer de plusieurs étapes. Ces étapes sont répertoriées dans la boîte de réception AEM et facilitent la progression de rapport du workflow. Divisez votre processus métier en étapes logiques.
* Vous pouvez configurer l’étape Affecter une tâche des workflows AEM pour envoyer des notifications par e-mail aux utilisateurs et utilisatrices, ou aux personnes désignées. Ainsi, [autorisez les notifications par e-mail](#configure-email-service).
* Un workflow peut également utiliser Adobe Sign pour les signatures numériques. Si vous envisagez d’utiliser Adobe Sign dans un processus, [configure Adobe Sign pour AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) avant de l’utiliser dans un processus.

## Créer un modèle de processus {#create-a-workflow-model}

Un modèle de workflow se compose de la logique et du flux d’un processus métier. Il se compose d’une série d’étapes. Ces étapes sont des composants d’AEM. Vous pouvez étendre les étapes de workflow avec des paramètres et des scripts pour proposer davantage de fonctionnalités et de contrôle, selon les besoins. AEM Forms fournit quelques étapes supplémentaires par rapport aux étapes AEM prêtes à l’emploi. Pour obtenir la liste détaillée des étapes AEM et AEM Forms, consultez [Référence sur les étapes de workflow AEM](/help/sites-developing/workflows-step-ref.md) et [Référence sur les étapes du workflow basé sur l’utilisation de Forms on OSGi](../../forms/using/aem-forms-workflow.md).

AEM fournit une interface utilisateur intuitive pour créer un modèle de workflow en suivant les étapes de workflow fournies. Pour des instructions détaillées afin de créer un modèle de workflow, consultez [Création de modèles de workflow](/help/sites-developing/workflows-models.md). L’exemple suivant fournit des instructions détaillées pour créer un modèle de workflow pour un workflow d’approbation et de révision :

>[!NOTE]
>
>Vous devez être membre du groupe d’édition de workflow pour créer ou modifier un modèle de workflow.

### Création d’un modèle pour un processus d’approbation et de révision {#create-a-model-for-an-approval-and-review-workflow}

Le workflow d’approbation et de révision est destiné aux tâches qui nécessitent une intervention humaine pour une prise de décisions. L’exemple suivant crée un modèle de workflow pour une demande de prêt immobilier à remplir par un conseiller ou une conseillère bancaire. Une fois remplie, la demande est envoyée pour approbation. Par la suite, la demande approuvée est envoyée au demandeur pour les signatures électroniques à l’aide d’Adobe Sign.

L’exemple est disponible en tant que package joint ci-dessous. Importez et installez l’exemple à l’aide du gestionnaire de packages. Vous pouvez également effectuer les opérations suivantes afin de créer manuellement le modèle de workflow de la demande :

Cet exemple crée un modèle de workflow pour une demande de prêt immobilier à remplir par un conseiller ou une conseillère bancaire. Une fois remplie, la demande est envoyée pour approbation. Par la suite, la demande approuvée est envoyée au client ou à la cliente pour les signatures électroniques à l’aide d’Adobe Sign. Vous pouvez importer et installer l’exemple à l’aide du gestionnaire de packages.

[Obtenir le fichier](assets/example-mortgage-loan-application.zip)

1. Ouvrez la console Modèles de processus. L’URL par défaut est `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Sélectionnez **Créer**, puis **Créer un modèle**. La boîte de dialogue Ajouter un modèle de processus s’ouvre.
1. Saisissez **Titre** et **Nom** (facultatif). par exemple, une demande de prêt immobilier. Sélectionnez **Terminé**.
1. Sélectionnez le workflow que vous venez de créer, puis choisissez **Modifier**. Désormais, vous pouvez ajouter des étapes de processus pour créer une logique d’entreprise. Lorsque vous créez un modèle de processus pour la première fois, il contient :

   * Les étapes Début de flux et Fin de flux. Ces étapes définissent le début et la fin du workflow. Ces étapes sont obligatoires et ne peuvent pas être modifiées ou supprimées.
   * Un exemple d’étape Participant, dont le nom est Étape 1. Cette étape est configurée pour affecter un élément de travail à l’utilisateur administrateur. Supprimez cette étape.

1. Activez les notifications électroniques. Vous pouvez configurer le processus basé sur l’utilisation de Forms sur OSGi pour qu’il envoie des notifications électroniques aux utilisateurs ou personnes désignées. Effectuez les configurations suivantes pour activer les notifications électroniques :

   1. Accédez au gestionnaire de configuration AEM à l’adresse `https://[server]:[port]/system/console/configMgr`.
   1. Ouvrez la configuration du **[!UICONTROL Service de messagerie Day CQ]**. Spécifiez une valeur pour les champs **[!UICONTROL Nom d’hôte du serveur SMTP]**, **[!UICONTROL Port du serveur SMTP]** et **[!UICONTROL Adresse de l’expéditeur]**. Cliquez sur **[!UICONTROL Enregistrer]**.
   1. Ouvrez la configuration de **[!UICONTROL Day CQ Link Externalizer]**. Dans le champ **[!UICONTROL Domaines]**, spécifiez le nom de hôte /l’adresse IP et le numéro de port réels pour les instances locale, de l’auteur et de publication. Cliquez sur **[!UICONTROL Enregistrer]**.

1. Créez des étapes de workflow. Un workflow peut se composer de plusieurs étapes. Ces étapes sont affichées dans la boîte de réception AEM et signalent la progression du workflow.

   Pour définir une étape, sélectionnez l’icône ![info-circle](assets/info-circle.png) pour ouvrir les propriétés de modèle de workflow, ouvrez l’onglet **Étapes**, ajoutez des étapes au modèle de workflow et sélectionnez **Enregistrer et fermer**. Pour l’exemple de demande de prêt immobilier, créez des étapes : demande de prêt, état de la demande de prêt, documents à signer et document de prêt signé.

1. Glissez-déposez l’explorateur d’étapes **Affecter une tâche** dans le modèle de processus. Faites-en la première étape du modèle.

   Le composant de tâche affecte la tâche créée par workflow à un utilisateur, une utilisatrice ou à un groupe. Lors de l’affectation de la tâche, vous pouvez utiliser le composant pour spécifier un formulaire adaptatif ou un fichier PDF non interactif pour la tâche. Le formulaire adaptatif est requis pour accepter une saisie des utilisateurs et utilisatrices et un fichier PDF non interactif ou un formulaire adaptatif en lecture seule est utilisé pour les workflows de révision uniquement.

   Vous pouvez également utiliser l’étape pour contrôler le comportement de la tâche. Par exemple, lors de la création d’un document d’enregistrement automatique, affectez la tâche à un utilisateur, une utilisatrice ou un groupe spécifique, le chemin des données envoyées, le chemin des données pré-renseignées et les actions par défaut. Pour obtenir des informations détaillées sur les options de l’étape d’affectation de tâche, consultez le document [Référence sur les étapes du processus basé sur l’utilisation de Forms sur OSGi](../../forms/using/aem-forms-workflow.md).

   ![workflow-editor](assets/workflow-editor.png)

   Pour l’exemple de demande de prêt immobilier, configurez l’étape Affecter une tâche pour utiliser un formulaire adaptatif en lecture seule et afficher le document PDF une fois la tâche terminée. Par ailleurs, sélectionnez le groupe d’utilisateurs autorisé à approuver la demande de prêt. Dans l’onglet **Actions**, désactivez l’option **Envoyer**. Créez une variable **actionTaken** de type de données de chaîne et spécifiez la variable en tant que **Variable d’itinéraire**. Par exemple, actionTaken. Ajoutez également les itinéraires Approuver et Refuser. Les itinéraires sont affichés sous forme d’actions distinctes (boutons) dans la boîte de réception AEM. Le workflow sélectionne une branche en fonction de l’action (bouton) sélectionnée par l’utilisateur ou l’utilisatrice.

   Vous pouvez importer l’exemple de package, disponible pour téléchargement au début de la section, pour l’ensemble complet des valeurs de tous les champs de l’étape configurée Attribuer une tâche, par exemple la demande de prêt immobilier.

1. Faites glisser et déposez le composant Division OU de l’explorateur d’étapes vers le modèle de workflow. L’étape de division OU divise le processus et une seule branche est active par la suite. Cette étape permet d’ajouter des chemins de traitement conditionnels dans le processus. Vous ajoutez des étapes de processus à chaque branche selon vos besoins.

   Vous pouvez définir l’expression de routage d’une branche à l’aide d’une définition de règle, d’un script ECMA ou d’un script externe.

   Utilisez l’éditeur d’expressions pour créer des expressions de routage pour les branches 1 et 2. Ces expressions de routage permettent de sélectionner une branche en fonction de l’action de l’utilisateur dans la boîte de réception AEM.

   **Expression de routage pour la branche 1**

   Lorsqu’un utilisateur clique sur le bouton **Approuver** dans la boîte de réception AEM, la Branche 1 est activée.

   ![OU Exemple de fractionnement](assets/orsplit_branch1_active_new.png)

   **Expression de routage pour la branche 2**

   Lorsqu’un utilisateur clique sur **Refuser** dans la boîte de réception AEM, la Branche 2 est activée.

   ![OU Exemple de fractionnement](assets/orsplit_branch2_active_new.png)

   Pour plus d’informations sur la création d’expressions de routage à l’aide de variables, consultez [Variables dans les processus AEM Forms](../../forms/using/variable-in-aem-workflows.md).

1. Ajoutez d’autres étapes de processus pour créer une logique d’entreprise.

   Pour l’exemple de prêt immobilier, ajoutez un document d’enregistrement généré, deux étapes Affecter une tâche et une étape de signature de document pour la Branche 1 du modèle, comme affiché dans l’image ci-dessous. Une étape Affecter une tâche consiste à afficher et envoyer des **documents de prêt à signer au demandeur** et un autre composant de tâche consiste à **afficher les documents signés**. Ajoutez également un composant Affecter une tâche à la branche 2. Il est activé lorsqu’un utilisateur clique sur Refuser dans la boîte de réception AEM.

   Pour obtenir l’ensemble complet des valeurs de tous les champs des étapes Attribuer une tâche, de l’étape Document d’enregistrement et de l’étape Signer le document configurées pour l’exemple de demande de prêt immobilier, importez l’exemple de package, disponible pour téléchargement au début de cette section.

   Le modèle de workflow est prêt. Vous pouvez lancer le workflow via différentes méthodes. Pour plus de détails, consultez [Lancement d’un workflow basé sur l’utilisation de Forms on OSGi](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## Créer une demande de processus basée sur l’utilisation de Forms {#create-a-forms-centric-workflow-application}

La demande est le formulaire adaptatif associé au workflow. Lorsqu’une demande est envoyée via la boîte de réception, elle lance le processus associé. Pour rendre un workflow Forms disponible en tant que demande dans la boîte de réception AEM et l’application AEM Forms, procédez comme suit pour créer une demande de workflow :

>[!NOTE]
>
>Vous devez être membre du groupe administrateur-fd pour être en mesure de créer et de gérer les demandes de processus.

1. Sur votre instance de création AEM, accédez à ![tools-1](assets/tools-1.png) > **[!UICONTROL Formulaires]** > **[!UICONTROL Gérer la demande de processus]** et appuyez sur **[!UICONTROL Créer]**.
1. Dans la fenêtre Créer la demande de processus, saisissez des données dans les champs suivants et appuyez sur **Créer**. Une nouvelle demande est créée et est répertoriée dans l’écran Demandes de processus.

<table>
 <tbody>
  <tr>
   <td>Champ</td>
   <td>Description</td>
  </tr>
  <tr>
   <td>Titre</td>
   <td>Le titre est visible dans la boîte de réception AEM et permet aux utilisateurs et utilisatrices de sélectionner une demande. Assurez-vous qu’il soit descriptif. Par exemple, Demande d’ouverture de compte d’épargne.<br /> </td>
  </tr>
  <tr>
   <td>Nom </td>
   <td>Indiquez le nom de la demande. Tous les caractères autres que les lettres, chiffres, tirets et traits de soulignement ont été remplacés par des tirets. </td>
  </tr>
  <tr>
   <td>Description</td>
   <td>La description est visible dans la boîte de réception AEM. Fournissez des informations détaillées sur la demande dans les champs de description. Par exemple, Objectif de la demande.<br /> </td>
  </tr>
  <tr>
   <td>Formulaire adaptatif</td>
   <td><p>Spécifiez le chemin d’un formulaire adaptatif. Lorsqu’un utilisateur ou une utilisatrice commence une demande, le formulaire adaptatif spécifié est affiché.</p> <p><strong>Remarque :</strong> Les demandes de processus ne prennent pas en charge les formulaires et documents PDF de plus d’une page ou qui nécessitent un défilement sur l’iPad d’Apple. Lorsqu’une demande est ouverte sur un iPad d’Apple et que la longueur du formulaire adaptatif ou du document PDF dépasse une page, les champs de formulaire et le contenu de la deuxième page sont perdus.</p> </td>
  </tr>
  <tr>
   <td>Groupes d’accès</td>
   <td><p>Sélectionnez un groupe. La demande est visible dans la boîte de réception AEM uniquement pour les membres du groupe sélectionné. L’option Accès au groupe permet de sélectionner tous les groupes du groupe d’utilisateurs du processus. </p> <br /> </td>
  </tr>
  <tr>
   <td>Service de préremplissage</td>
   <td>Sélectionnez un <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">service de préremplissage</a> pour le formulaire adaptatif.<br /> </td>
  </tr>
  <tr>
   <td>Modèle de workflow</td>
   <td>Sélectionnez un <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">modèle de workflow</a> pour la demande. Un modèle de processus se compose de la logique et du flux de processus d’entreprise. </td>
  </tr>
  <tr>
   <td>Chemin d'accès au fichier de données</td>
   <td>Spécifiez le chemin du fichier de données dans le référentiel crx. Le chemin est relatif à la charge utile de formulaire adaptatif et contient le nom du fichier de données. Intégrez toujours le nom complet du fichier, y compris son extension, le cas échéant. Par exemple, [charge utile]/data.xml. </td>
  </tr>
  <tr>
   <td>Chemin d’accès à la pièce jointe</td>
   <td>Spécifiez le chemin du fichier de pièces jointes dans le référentiel crx. Le chemin d’accès à la pièce jointe est relatif à l’emplacement de la charge utile. Par exemple, [charge utile]/data.xml. </td>
  </tr>
  <tr>
   <td>Chemin d’accès au document d’enregistrement</td>
   <td>Spécifiez le chemin d’accès au fichier Document d’enregistrement dans le référentiel crx. Le chemin est relatif à l’emplacement de la charge utile du formulaire adaptatif. Intégrez toujours le nom complet du fichier, y compris son extension, le cas échéant. Par exemple, [charge utile]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Lancement d’un processus basé sur l’utilisation de Forms sur OSGi {#launch}

Vous pouvez lancer ou de déclencher un processus basé sur l’utilisation de Forms en :

* [Envoyer une demande depuis la boîte de réception AEM](#inbox)
* [Envoyant une demande depuis l’application AEM Forms](#afa)

* [Envoi d’un formulaire adaptatif](#af)
* [Utilisant le dossier de contrôle](#watched)

* [Envoyer une communication interactive ou une lettre](#letter)

### Envoyer une demande depuis la boîte de réception AEM {#inbox}

La demande de processus que vous avez créée est disponible en tant qu’application dans la boîte de réception. Les utilisateurs ou utilisatrices qui sont membres du groupe d’utilisateurs et d’utilisatrices de worflow peuvent renseigner et envoyer la demande qui déclenche le workflow associé. Pour plus d’informations sur l’utilisation de la boîte de réception AEM pour envoyer des demandes et gérer des tâches, voir [Gestion des applications et des tâches Forms dans la boîte de réception AEM](../../forms/using/manage-applications-inbox.md).

### Envoyant une demande depuis l’application AEM Forms {#afa}

L’application AEM Forms se synchronise avec un serveur AEM Forms et vous permet de modifier les données de formulaire, les tâches, les applications de workflow et les informations enregistrées (brouillons/modèles) dans votre compte. Pour plus d’informations, consultez [Application AEM Forms](/help/forms/using/aem-forms-app.md) et les articles connexes.

### Envoi d’un formulaire adaptatif {#af}

Vous pouvez configurer des actions d’envoi d’un formulaire adaptatif pour démarrer un workflow lors de l’envoi du formulaire adaptatif. Les formulaires adaptatifs fournissent l’action d’envoi **Appeler un workflow AEM** pour démarrer un workflow lors de l’envoi d’un formulaire adaptatif. Pour obtenir des informations détaillées sur l’action d’envoi, consultez [Configuration de l’action d’envoi](../../forms/using/configuring-submit-actions.md). Pour envoyer un formulaire adaptatif via l’application AEM Forms, activez la synchronisation avec l’application AEM Forms dans les propriétés du formulaire adaptatif.

Vous pouvez configurer la synchronisation, l’envoi et le déclenchement d’un workflow depuis l’application AEM Forms. Pour plus de détails, consultez la section [Utilisation d’un formulaire](/help/forms/using/working-with-form.md).

### Utilisation d’un dossier de contrôle {#watched}

Un administrateur ou une administratrice (un membre du groupe administrateur-fd) peut configurer un dossier réseau pour exécuter un workflow préconfiguré lorsqu’un utilisateur ou une utilisatrice y place un fichier (tel qu’un fichier PDF). Une fois que le workflow est terminé, vous pouvez enregistrer le fichier de sortie dans un dossier de sortie spécifié. Un tel dossier est appelé [Dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md). Effectuez la procédure suivante pour configurer un dossier de contrôle afin de lancer un workflow :

1. Sur votre instance d’auteur AEM, accédez à ![Outils-1](assets/tools-1.png) > **[!UICONTROL Formulaires]** > **[!UICONTROL Configurer le dossier de contrôle]**.  Une liste de dossiers de contrôle déjà configurés s’affiche.
1. Sélectionnez **[!UICONTROL Nouveau]**. Une liste des champs s’affiche. Spécifiez une valeur pour les champs suivants afin de configurer un dossier de contrôle pour un workflow :

<table>
 <tbody>
  <tr>
   <td>Champ</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Nom</code></td>
   <td>Indiquez le nom du dossier de contrôle. Ce champ prend uniquement en charge les caractères alphanumériques.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Chemin </code></td>
   <td>Spécifiez l’emplacement physique du dossier de contrôle. Dans un environnement organisé en cluster, utilisez un dossier réseau partagé accessible à partir du nœud du cluster AEM.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Traiter les fichiers avec</code></td>
   <td>Sélectionnez l’option <span class="uicontrol">Workflow </code>. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modèle de processus</code></td>
   <td>Sélectionnez un modèle de processus.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modèle de fichier de sortie</code></td>
   <td>Indiquez la structure de répertoires pour les fichiers de sortie et les répertoires. Vous pouvez également spécifier un <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">modèle pour les fichiers de sortie et les répertoires</a>.</td>
  </tr>
 </tbody>
</table>

1. Sélectionnez **Avancé**. Spécifiez une valeur pour le champ suivant puis cliquez sur **Créer**. Le dossier de contrôle est configuré pour lancer un processus. Désormais, chaque fois qu’un fichier est placé dans le répertoire d’entrée du dossier de contrôle, le processus spécifié est déclenché.

   | Champ | Description |
   |---|---|
   | Filtre de mappeur de charge | Lorsque vous créez un dossier de contrôle, il crée une structure de dossier dans le référentiel crx. La structure de dossier peut servir de charge utile au workflow. Vous pouvez écrire un script pour mapper un workflow AEM pour accepter les entrées de la structure du dossier de contrôle. Une implémentation prête à l’emploi est disponible et répertoriée dans le Filtre de mappeur de charge. Si vous ne disposez pas d’une implémentation personnalisée, choisissez l’implémentation par défaut. |

   L’onglet Avancé contient davantage de champs. La plupart de ces champs contiennent une valeur par défaut. Pour en savoir plus sur tous les champs, voir l’article [Création ou configuration d’un dossier de contrôle](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

### Envoi d’une communication interactive ou d’une lettre {#letter}

Vous pouvez associer et exécuter un workflow basé sur l’utilisation de Forms sur OSGi lors de l’envoi d’une communication interactive ou d’une lettre. Dans le système de gestion de contenu, les workflows sont utilisés pour le post-traitement de communications interactives et de lettres. Par exemple, l’envoi d’e-mail, l’impression, la télécopie ou l’archivage des lettres finales. Pour les étapes détaillées, voir [Post-traitement des communications interactives et des lettres](../../forms/using/submit-letter-topostprocess.md).

## Autres configurations {#additional-configurations}

### Configuration du service de messagerie {#configure-email-service}

Vous pouvez utiliser les étapes Affecter une tâche et Envoyer un e-mail des workflows AEM pour envoyer un e-mail. Effectuez les étapes suivantes pour spécifier les serveurs de messagerie et les autres configurations requises pour l’envoi d’e-mails :

1. Accédez au gestionnaire de configuration AEM à l’adresse `https://[server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration du **[!UICONTROL Service de messagerie Day CQ]**. Spécifiez une valeur pour les champs **[!UICONTROL Nom d’hôte du serveur SMTP]**, **[!UICONTROL Port du serveur SMTP]** et **[!UICONTROL Adresse de l’expéditeur]**. Cliquez sur **[!UICONTROL Enregistrer]**.
1. Ouvrez la configuration de **[!UICONTROL Day CQ Link Externalizer]**. Dans le champ **[!UICONTROL Domaines]**, spécifiez le nom de hôte /l’adresse IP et le numéro de port réels pour les instances locale, de l’auteur et de publication. Cliquez sur **[!UICONTROL Enregistrer]**.

### Purge des instances de processus {#purge-workflow-instances}

Réduire le nombre d’instances de workflow améliore les performances du moteur de workflow. Vous pouvez donc purger régulièrement les instances de workflow terminées ou en cours d’exécution du référentiel. Pour plus d’informations, consultez [Purge régulière des instances de workflow](/help/sites-administering/workflows-administering.md#regular).

## Paramétrer les données sensibles aux variables de workflow et les stocker dans des magasins de données externes {#externalize-wf-variables}

Toutes les données envoyées à partir de formulaires adaptatifs vers des workflows [!DNL Experience Manager] peuvent avoir des PII (informations d’identification personnelles) ou SPD (données personnelles sensibles) des utilisateurs et utilisatrices finaux de votre entreprise. Toutefois, il n’est pas obligatoire de stocker vos données dans le [Référentiel JCR](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html?lang=fr) d’[!DNL Adobe Experience Manager]. Vous pouvez externaliser le stockage des données des utilisateurs et utilisatrices finaux dans votre stockage de données géré (par exemple, le stockage Azure Blob) en paramétrant les informations dans les [variables de workflow](/help/forms/using/variable-in-aem-workflows.md).

Dans un workflow [!DNL Adobe Experience Manager] Forms, les données sont traitées et transmises par une série d’étapes de workflow au moyen de variables de workflow. Ces variables sont des propriétés nommées ou des paires clé-valeur stockées dans le nœud de métadonnées des instances de workflow ; par exemple, `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. Ces variables de workflow peuvent être externalisées dans un référentiel autre que JCR, puis traitées par des workflows [!DNL Adobe Experience Manager]. [!DNL Adobe Experience Manager] fournit une API `[!UICONTROL UserMetaDataPersistenceProvider]` pour stocker les variables de workflow dans votre stockage externe géré. Pour en savoir plus sur l’utilisation de variables de workflow pour les magasins de données détenus par les client(e)s dans [!DNL Adobe Experience Manager], reportez-vous à [Administration des variables de workflow pour les magasins de données externes](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] fournit l’[exemple](https://github.com/adobe/workflow-variable-externalizer) suivant pour stocker des variables d’un mappage de métadonnées de workflow vers le stockage Azure Blob, à l’aide de l’API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). Sur les lignes similaires, vous pouvez utiliser l’exemple comme guide d’utilisation de l’API [UserMetaDataPersistenceProvider] afin d’externaliser les variables de workflow de tout autre stockage de données externe vers [!DNL Adobe Experience Manager] et les gérer.

>[!NOTE]
>
>Lorsque vous stockez vos variables de workflow dans un stockage de données externe, reportez-vous aux conseils de la section [consignes relatives au stockage de données externe des workflows](#guidelines-workflows-external-data-storage).

### Installer l’exemple d’implémentation de l’API de workflow

Pour stocker des variables de workflow dans votre stockage Azure Blob géré :
1. Installez l’[exemple](https://github.com/adobe/workflow-variable-externalizer) d’API de workflow [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) comme suit :

   1. Dans le répertoire racine du projet, exécutez la commande `mvn clean install` avec Maven 3.

   1. Pour déployer le lot et le module de contenu à créer, exécutez `mvn clean install -PautoInstallPackage`.

   1. Pour déployer uniquement le lot vers l’auteur, exécutez `mvn clean install -PautoInstallBundle`.

1. Initialisez les propriétés suivantes dans le fichier de configuration OSGi de l’externaliseur dans le module de contenu `ui.config` :

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

Voici les objectifs (et exemples) de ces propriétés :

* **accountKey** est la clé secrète pour autoriser l’accès.

* **accountName** est le compte Azure où les données doivent être stockées.

* **endpointSuffix**, par exemple `core.windows.net`.

* **containerName** est le conteneur dans le compte où les données doivent être stockées. L’exemple suppose que le conteneur existe.

* **protocol**, par exemple `https` ou `http`.

1. Configurez le modèle de workflow dans [!DNL Adobe Experience Manager]. Pour savoir comment configurer le modèle de workflow pour un stockage externe, reportez-vous à [Configurer le modèle de workflow](#configure-aem-wf-model).

### Configurer le modèle de workflow dans [!DNL Adobe Experience Manager] pour le stockage de données externe {#configure-aem-wf-model}

Pour configurer un modèle de workflow AEM pour le stockage de données externe :

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflows]** > **[!UICONTROL Modèles]**.

1. Sélectionnez un nom de modèle et sélectionnez **[!UICONTROL Modifier]**.

1. Sélectionnez l’icône Informations sur la page, puis **[!UICONTROL Ouvrir les propriétés]**.

1. Sélectionnez **[!UICONTROL Externaliser le stockage des données de workflow]**.

1. Sélectionnez **[!UICONTROL Enregistrer et fermer]** pour enregistrer les propriétés.

### Recommandations pour les workflows d’AEM pour le stockage de données externes {#guidelines-workflows-external-data-storage}

Voici nos recommandations concernant l’utilisation des workflows [!DNL Adobe Experience Manager] et le stockage de données externe (par exemple, le serveur de stockage Microsoft Azure) :

* Utilisez des variables pour stocker des données lors de la définition de fichiers de données d’entrée et de sortie et de pièces jointes dans les étapes du modèle de workflow. Ne sélectionnez pas les options **[!UICONTROL Relatif à la charge]** et **[!UICONTROL Disponible sur un chemin absolu]**. Les options **[!UICONTROL Relatif à la payload]** et **[!UICONTROL Disponible sur un chemin absolu]** ne s’affichent pas automatiquement lorsque vous [configurez un modèle de workflow  [!DNL Adobe Experience Manager]  pour le stockage de données externe](#configure-aem-wf-model).

* Utilisez des variables pour stocker le fichier de données et les pièces jointes lors de l’envoi d’un formulaire adaptatif à un workflow AEM. Ne sélectionnez pas l’option **[!UICONTROL Relatif à la payload]** lors de l’envoi d’un formulaire adaptatif à un workflow [!DNL Adobe Experience Manager]. L’option **[!UICONTROL Relatif à la payload]** ne s’affiche pas automatiquement une fois que vous avez [configuré un modèle de workflow  [!DNL Adobe Experience Manager]  pour le stockage des données externe](#configure-aem-wf-model).

* N’utilisez pas d’étape de workflow [!DNL Adobe Experience Manager] personnalisé dans un modèle de workflow pour stocker des données dans le référentiel [!UICONTROL CRX DE].

* Lorsque vous [configurez un modèle de workflow  [!DNL Adobe Experience Manager]  pour le stockage externe des données](#configure-aem-wf-model), ne créez pas de colonnes personnalisées pour la [!UICONTROL boîte de réception] [!DNL Adobe Experience Manager], car les valeurs des colonnes personnalisées ne sont pas récupérées si l’élément de travail de la [!UICONTROL boîte de réception] [!DNL Adobe Experience Manager] appartient à un workflow marqué pour le stockage externe.
