---
title: Configuration et configuration des sites de référence en libre-service We.Finance et Employee
seo-title: Configuration et configuration des sites de référence en libre-service We.Finance et Employee
description: Les sites de référence AEM Forms décrivent comment utiliser AEM Forms pour implémenter un flux de bout en bout dans une entreprise.
seo-description: Les sites de référence AEM Forms décrivent comment utiliser AEM Forms pour implémenter un flux de bout en bout dans une entreprise.
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '2864'
ht-degree: 48%

---


# Configuration et configuration des sites de référence en libre-service We.Finance et Employee{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms fournit une implémentation de site de référence pour démontrer la manière dont AEM Forms permet à des organisations gouvernementales et du secteur des services financiers de transformer leurs transactions complexes en expériences numériques simples et attrayantes, n’importe où, n’importe quand et sur n’importe quel périphérique.

Le site de référence We.Finance tire des cas d&#39;utilisation réels pour engager le dialogue avec les clients existants et potentiels, dès le début jusqu&#39;à la gestion des correspondances et transactions de manière personnalisée et rentable.

Les sites de référence vous permettent d’explorer et de voir en action les principales fonctionnalités suivantes d’AEM Forms.

* Simplification de la création de formulaires adaptatifs attrayants et réactifs et de communications interactives.
* Communications interactives pour créer des communications client interactives, personnalisées et réactives qui s&#39;adaptent au paramètre et à la mise en page du périphérique.
* Intégration des données permettant de se connecter à des sources de données disparates afin de préremplir et d’envoyer des données de formulaire par le biais d’un modèle de données de formulaire.
* Processus des formulaires pour automatiser les processus d’entreprise.
* Fonctionnalités de traitement et de gestion des données utilisateur.
* Intégration avec Adobe Sign garantissant une signature et un envoi sécurisé des formulaires adaptatifs.
* Intégration avec Adobe Target pour fournir des recommandations ciblées et effectuer les tests A/B, pour augmenter le retour sur investissement d’un formulaire.
* Intégration à Adobe Analytics pour mesurer les performances d’un formulaire ou d’une campagne et prendre des décisions éclairées.
* Amélioration de l’expérience de remplissage des formulaires.

Les sites de référence offrent des ressources réutilisables que vous pouvez utiliser comme modèles pour créer vos propres ressources.

* Intégration avec Adobe Sign garantissant une signature et un envoi sécurisé des formulaires adaptatifs.

* Intégration avec Adobe Sign garantissant une signature et un envoi sécurisé des formulaires adaptatifs.

## Conditions préalables et étapes et de la configuration des sites de référence {#prerequisites-and-steps-to-set-up-reference-sites}

Avant de configurer le site de référence, assurez-vous que vous disposez des éléments suivants :

* **AEM Essentials** AEM QuickStart, package du module complémentaire AEM Forms et packages de sites de référence. See [AEM Forms releases](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) for add-on and reference sites packages details.

* **Un service SMTP** Vous pouvez utiliser n’importe quel service SMTP.

* **Compte de développeur Adobe Sign et application d’API Adobe Sign** Pour utiliser les fonctionnalités de signature numérique, un compte de développeur Adobe Sign est requis. Voir [Adobe Sign](https://acrobat.adobe.com/fr/fr/why-adobe/developer-form.html).

* Instance en cours d&#39;exécution de Microsoft Dynamics 365 à intégrer aux AEM Forms. Pour exécuter le site de référence, vous importez les données d&#39;exemple dans l&#39;instance Microsoft Dynamics afin de préremplir la communication interactive utilisée dans le site de référence.
* Instance en cours d’exécution d’AEM avec le module complémentaire Forms. Pour plus d’informations, reportez-vous à la section [Installation et configuration d’AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Effectuez les étapes suivantes dans l’ordre recommandé pour installer et configurer les sites de référence.

<table>
 <tbody>
  <tr>
   <th><strong>Étape</strong></th>
   <th><strong>Configurer</strong></th>
   <th><strong>Notes</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">Installer et configurer AEM Forms</a></td>
   <td>Auteur et publication</td>
   <td>Installez et configurez des instances d’auteur et de publication AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="#ssl">Configurer SSL</a></td>
   <td>Auteur et publication<br /> </td>
   <td>Activez HTTP via SSL pour sécuriser les communications avec Adobe Sign.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Configuration de Day CQ Link Externalizer (Externalisateur du lien vers Day CQ)</a></p> </td>
   <td>Auteur et publication<br /> </td>
   <td><p>Les cas d’utilisation de site de référence fournissent des messages électroniques pour diverses transactions. Ce paramètre est requis pour la diffusion de la newsletter par courrier électronique. Cela permet d’assurer que les URL et les images pointent vers une instance de publication. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Configuration du service de messagerie Day CQ</a></td>
   <td>Auteur et publication</td>
   <td>Requis pour les communications par courrier électronique.</td>
  </tr>
  <tr>
   <td><a href="#xss">Remplacement de la configuration XSS par défaut</a></td>
   <td>Publication </td>
   <td>Utilisé pour remplacer les caractères $, { et } bloqués par la sécurité xss.</td>
  </tr>
  <tr>
   <td><a href="#aemds">Configurer les paramètres AEM DS</a></td>
   <td>Création</td>
   <td>Configurez AEM DS pour l’envoi de formulaire sur l’instance de publication et les processus de traitement sur l’instance d’auteur.</td>
  </tr>
  <tr>
   <td><a href="#refsite">Déployer les packages des sites de référence</a></td>
   <td>Création</td>
   <td>Déployez les packages des sites de référence sur l’instance d’auteur AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Importation d’exemples de données dans Microsoft Dynamics</a></td>
   <td>Auteur et publication</td>
   <td>Importer les données d’exemple pour la demande de carte de crédit, la demande de prêt immobilier et la présentation de la demande d’assurance habitation</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Configurer le service cloud OAuth pour Microsoft Dynamics</a></td>
   <td>Auteur et publication</td>
   <td>Configurez le service cloud OAuth en AEM Forms pour activer la communication entre les AEM Forms et Microsoft Dynamics. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Configurer le planificateur Adobe Sign</a></td>
   <td>Auteur et publication<br /> </td>
   <td>Modifiez la configuration du planificateur pour vérifier l’état toutes les deux minutes.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">Configurer le service cloud Adobe Sign de site de référence</a></td>
   <td>Auteur et publication<br /> </td>
   <td>Une configuration qui comprend des packages de sites de référence et qui doit être reconfigurée avec des informations d’identification valides.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">Configurer le service de configuration commun aux formulaires pour les utilisateurs anonymes</a></td>
   <td>Publication </td>
   <td>La configuration permet l’envoi, la signature et le Document de génération d’enregistrements pour les utilisateurs anonymes.</td>
  </tr>
  <tr>
   <td><a href="#fdm">Modifier le fichier Swagger du service Rest pour le modèle de données du formulaire</a></td>
   <td>Auteur et publication<br /> </td>
   <td>Modifiez le service pour votre environnement.</td>
  </tr>
 </tbody>
</table>

## Installer et configurer AEM Forms {#installandconfigureaemform}

Install and deploy AEM Forms as described in [Installing and configuring AEM Forms on OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>Configurez les agents de réplication et d’inversion de la réplication s’il existe plusieurs instances de publication ou si les instances d’auteur et de publication se trouvent sur des ordinateurs différents.

## Configurer SSL {#ssl}

La configuration SSL est requise pour communiquer avec les serveurs Adobe Sign. For detailed steps, see [Enabling HTTP Over SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Do not configure force SSL on `/etc/map` folder.

## Configuration de Day CQ Link Externalizer (Externalisateur du lien vers Day CQ){#externalizer}

In AEM, the **Externalizer** is an OSGI service that allows you to programmatically transform a resource path (e.g. /path/to/my/page) into an external and absolute URL (for example, https://www.mycompany.com/path/to/my/page) by prefixing the path with a pre-configured DNS. Voir [Externalisation des URL](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>N’externalisez pas vers l’URL HTTPS si vous utilisez certificat autosigné pour SSL.
>
>En outre, vous devez utiliser localhost plutôt que hostname pour le serveur local.

Effectuez les étapes suivantes sur les instances d’auteur et de publication :

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **Day CQ Link Externalizer** configuration.
La boîte de dialogue Day CQ Link Externalizer s’ouvre à des fins d’édition de la configuration.
1. Dans la boîte de dialogue Day CQ Link Externalizer, dans le champ Domaines :

   * Sur l’instance de rédaction, spécifiez une URL de publication accessible depuis n’importe quel système externe. Par exemple, un nom d’hôte ou un serveur Web de publication.
   * Sur l’instance de publication, indiquez les URL de rédaction et de publication.

1. Sur les instances d’auteur et de publication, assurez-vous que l’URL du serveur local est indiquée dans le champ des domaines.
1. Appuyez sur **Save** (Enregistrer). Patientez un moment le temps que tous les services redémarrent.

## Configuration du service de messagerie Day CQ {#cqmail}

Une mise en œuvre de site de référence nécessite que les courriers électroniques soient envoyés aux exemples d’utilisateurs lorsqu’ils remplissent les formulaires et les envoient. La configuration du service de messagerie Day CQ vous permet de fournir des détails de serveur SMTP pour envoyer des courriers électroniques automatisés aux clients. Voir [Configuration des notifications par courrier électronique](/help/sites-administering/notification.md).

Procédez comme suit pour configurer le service de messagerie sur l’instance de publication :

1. Go to OSGi Configuration at https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Find and tap **Day CQ Mail Service** to open it for configuration.
1. Indiquez les valeurs hostname et de port du serveur SMTP.
1. Appuyez sur **Enregistrer.**

>[!NOTE]
>
>Vous pouvez utiliser votre service SMTP d’entreprise ou des services publics comme Gmail. Pour la configuration du service SMTP, voir la documentation correspondante.

## Remplacement de la configuration XSS par défaut {#xss}

Les modèles de courrier électronique pour le site de référence We.Finance contiennent des liens personnalisés dans les courriers électroniques. Ces liens possèdent un espace réservé tel que `${placeholder}`. Ces espaces réservés sont remplacés par des valeurs réelles avant l’envoi des courriers électroniques. La configuration de protection XSS par défaut pour AEM n’autorise pas les accolades (**{ }**) dans l’URL d’un contenu HTML. Cependant, vous pouvez remplacer la configuration par défaut en procédant comme suit sur l’instance de publication :

1. Copiez `/libs/cq/xssprotection/config.xml` dans `/apps/cq/xssprotection/config.xml`.
1. Ouvrez `/apps/cq/xssprotection/config.xml`.
1. In the `common-regexps` section, modify the `onsiteURL` entry as follows and save the file.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Les accolades (**{}**) sont incluses en tant que caractères acceptés dans l’URL du contenu HTML.

Après la configuration du serveur SMTP, essayez de remplir un formulaire à l’aide de Sarah Rose et de l’enregistrer en tant que brouillon. Lorsque vous enregistrez en tant que brouillon, vous obtenez une option permettant de recevoir le brouillon par courrier électronique. Lorsque vous appuyez sur le bouton **Envoyer un courrier électronique**, si vous recevez un courrier électronique contenant un lien vers le brouillon de la demande, votre configuration de courrier électronique est correcte. Assurez-vous que vous vous connectez en utilisant les identifiants de Sarah pour afficher le brouillon.

## Configurer les paramètres AEM DS {#aemds}

Les paramètres du service AEM DS sont requis sur l’instance de publication pour les communications par courrier électronique dans les cas d’utilisation du site de référence. Pour obtenir des instructions détaillées sur la configuration du service AEM DS sur l’instance de publication, voir [Configuration des paramètres](../../forms/using/configuring-the-processing-server-url-.md)AEM DS.

Pour les sites de référence AEM Forms, dans le service des paramètres d’AEM DS, spécifiez l’URL du serveur de publication au lieu de celle du serveur de traitement.

>[!CAUTION]
>
>Do not put `/lc` in the processing server URL if you are configuring it for AEM Forms OSGi.

## Déployer les packages des sites de référence {#refsite}

Installez les packages de sites de référence à l&#39;aide de [Software Distribution](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html).

* [Package de site de référence FSI AEM Forms](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-FSI-REF-SITE)
* [Package du site de référence Gov AEM Forms](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-GOV-REF-SITE)

To learn more about how to use packages , see [How to Work With Packages](/help/sites-administering/package-manager.md).

Une fois que vous avez installé les packages et avez lancé les instances de rédaction et de publication, consultez les URL suivantes dans votre navigateur :

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

Si votre installation est terminée, vous pouvez accéder aux pages d’accueil des sites de référence et We.Finance.

## (Optional) Import sample data into Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

Les sites de référence des demandes de prêt immobilier et d&#39;assurance automobile sont configurés pour utiliser les enregistrements de Microsoft Dynamics. Le package de site de référence installe une entité personnalisée et des exemples d&#39;enregistrements que vous pouvez importer dans Microsoft Dynamics pour exécuter le site de référence. Effectuez les étapes suivantes pour migrer et configurer les données d’exemple :

Pour importer l&#39;entité personnalisée pour la demande d&#39;assurance automatique :

1. Téléchargez le package de la solution **WeFinanceAutoInsurance_1_0.zip** depuis `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` votre instance d’auteur AEM.
1. In your Microsoft Dynamics instance, go to **Settings > Solutions** and click **Import**. Sélectionnez et importez le package.

Pour importer l&#39;entité personnalisée pour la demande d&#39;assurance automatique :

1. Téléchargez le package **AEMFormsFSIRefsite_1_0.zip** depuis `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`. Sélectionnez et importez le package.

1. In your Microsoft Dynamics instance, go to **Settings > Solutions** and click **Import**. Sélectionnez et importez le package.

Pour importer les enregistrements de contrat d&#39;assurance et de client :

1. Download the **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv**, and **home mortgage** data files from the following locations on your AEM author instance:

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Dans votre instance Microsoft Dynamics, procédez comme suit :

   * Go to **Sales** > **We.Finance Customers** and click **Import**.

   * Go to **Sales** > **We.Finance Auto Insurance** and click **Import**.

   * Go to **Sales** > **We.Finance Home Mortgage** and click **Import**.

## Configurer le service cloud OAuth pour Microsoft Dynamics {#configure-oauth-cloud-service-for-microsoft-dynamics}

Configurez le service cloud OAuth en AEM Forms pour activer la communication entre les AEM Forms et Microsoft Dynamics. Effectuez les étapes suivantes pour configurer le Cloud Service OAuth sur les instances d’auteur et de publication AEM :

1. On AEM author instance, go to **Tools** > **Cloud Services** > **Data Sources** > **global**. Appuyez sur l&#39;icône **Refsite Dynamics Integration** et sur Properties (Propriétés).
1. Accédez au compte Microsoft Azure Active Directory. Ajoutez l’URL de configuration du service cloud copiée dans le paramètre **URL de réponse** pour votre application enregistrée. Enregistrez la configuration.
1. In the Authentication Settings tab, specify **Service Root**, **Client Id**, **Client Secret**, and **Resource URL** for your Microsoft Dynamics instance. Click **Connect to OAuth** that redirects to the Microsoft Dynamics login page.
1. Entrez vos informations de connexion. Une fois connecté, vous êtes redirigé vers la page de configuration du service cloud AEM Forms. Cliquez sur **Enregistrer et fermer**. La configuration du service cloud est enregistrée.
1. Go to **Forms** > **Data Integrations** > **We.Finance**. Sélectionnez Assurance automatique (Dynamics) et cliquez sur Modifier. Les entités Microsoft Dynamics sont répertoriées sous l&#39;onglet Sources de données. Attendez que toutes les entités soient récupérées de Microsoft Dynamics et répertoriées sous l&#39;onglet Sources de données.
1. Select the **AutoInsuranceRenewal entity** and click **Test Model Object**. In the input request section, specify the value for customer ID as “900001” and click **Test**. La section Output affiche les enregistrements extraits de Microsoft Dynamics pour l&#39;ID de client 900001.
1. In the input request section, specify the value for customer ID as “900001” and click **Test**. La section Output affiche les enregistrements extraits de Microsoft Dynamics pour l&#39;ID de client 900001.
1. Répétez les étapes 1 à 6 sur l’instance de publication.

## Configurer le planificateur Adobe Sign {#scheduler}

Effectuez les étapes suivantes sur les instances d’auteur et de publication :

1. Go to AEM Web Configuration console at `https://'[server]:[port]'system/console/configMgr`.
1. Find and tap **[!UICONTROL Adobe Sign Configuration Service]** to open it for configuration.
1. Configurez l’**[!UICONTROL expression du planificateur de mise à jour d’état]** comme suit : **0 0/2 * * * ?** .

   >[!NOTE]
   >
   >La configuration du planificateur ci-dessus vérifie l’état du service Adobe Sign toutes les deux minutes.

1. Appuyez sur **[!UICONTROL Enregistrer]**.

## Configurer le service cloud Adobe Sign de site de référence {#sign-service}

Effectuez les étapes suivantes sur les instances d’auteur et de publication :

1. Go to **Tools** > **Cloud Services** > **Adobe Sign** > **global**. Sélectionnez Signe **du site de référence** AEM Forms et appuyez sur Propriétés.

   >[!CAUTION]
   >
   >Ensure that the `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL is added to the redirect URL list of OAuth configuration of Adobe Sign API application.

1. Indiquez l’ID client et le secret de la configuration OAuth d’application Adobe Sign.
1. (Optional) Select the **[!UICONTROL Enable Adobe Sign for attachments also]** option, and tap **[!UICONTROL Connect to Adobe Sign]**. Cela permet d’ajouter les fichiers joints à un formulaire adaptatif au document Adobe Sign envoyé à des fins de signature.
1. Tap **[!UICONTROL Connect to Adobe Sign]** and log in with your Adobe Sign credentials.

## Configurer le service de configuration commun aux formulaires {#anonymous}

Effectuez les étapes suivantes sur l’instance de publication pour autoriser l’accès des utilisateurs anonymes :

1. Go to AEM Web Configuration console at `https://'[server]:[port]'/system/console/configMgr`.
1. Find and tap **[!UICONTROL Forms Common Configuration Service]** to open it for configuration.
1. Configure the **[!UICONTROL Allow]** field for **[!UICONTROL All Users]**.
1. Appuyez sur **[!UICONTROL Enregistrer]**.

## Modifier le service Rest pour le modèle de données de formulaire {#fdm}

Effectuez les étapes suivantes sur les instances d’auteur et de publication :

1. Accédez à CRXDE à `https://'[server]:[port]'/crx/de/index.jsp`.
1. Accédez à **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** et ouvrez le fichier swagger.
1. Mettez à jour les paramètres d’hôte et de port en fonction de votre environnement.
1. Enregistrez les paramètres.
1. (Instance **Auteur uniquement**) Accédez à **Outils** > **Cloud Service** > Sources de **données > global.****** Sélectionnez **roi-rest** et appuyez sur **Properties**.Appuyez sur **Authentication Settings** et définissez **Authentication Type sur Basic Authentication.****** Spécifiez `admin`/ `admin`comme nom d’utilisateur/mot de passe pour accéder au service. Appuyez sur **Save &amp; Close** (Enregistrer et fermer). 

## Intégration à Marketing Cloud {#integrate-with-marketing-cloud}

Vous pouvez intégrer les AEM Forms à Adobe Analytics et à l&#39;Adobe Target. Bien que Adobe Analytics vous aide à générer des rapports et à analyser les performances des formulaires adaptatifs, l’Adobe Target vous aide à fournir des expériences personnalisées et à effectuer des tests A/B pour les formulaires adaptatifs.

Procédez comme suit pour configurer Adobe Analytics et l’Adobe Target en AEM Forms.

### Configuration d’Adobe Analytics {#configureanalytics}

L’intégration d’Adobe Analytics à AEM Forms vous permet de surveiller et d’analyser la manière dont vos clients interagissent avec vos formulaires et documents. Il vous aide à identifier et à résoudre les problèmes et à agir pour augmenter le taux de conversion.

Pour tester cette fonctionnalité sur le site de référence, configurez votre compte Analytics tel que décrit dans [Configuration des analyses et des rapports](../../forms/using/configure-analytics-forms-documents.md).

Pour générer un rapport, les données sources sont regroupées avec les sites de référence. Avant d’utiliser les données de base, procédez comme suit :

1. Assurez-vous que les configurations des analyses We.Finance sont disponibles dans les AEM cloud services. Vous pouvez trouver les services cloud de l’une des manières suivantes :

   * Accédez à **[!UICONTROL Outils>Cloud Service>Cloud Service]** hérités ou accédez à https://&lt;hôte>:&lt;port>/libs/cq/core/content/tools/cloudservices.html.
   * In the **[!UICONTROL Cloud Services]** page, under **[!UICONTROL Adobe Analytics]** section, click `Show Configurations`. Vous pouvez voir les configurations We.Finance disponibles. Cliquez pour ouvrir la configuration. Dans la page de configuration, cliquez sur **[!UICONTROL Modifier]**. Indiquez une Société valide, un nom d’utilisateur, un secret partagé (mot de passe) et un centre de données, puis cliquez sur **[!UICONTROL Se connecter à Analytics]**. Une fois la boîte de dialogue Connexion réussie, cliquez sur **[!UICONTROL OK]** dans la boîte de dialogue de configuration. Configurez la structure sous la configuration Analytics comme décrit dans la section [Configuration de Analytics et des rapports](../../forms/using/configure-analytics-forms-documents.md).

1. Accédez à https://&lt;*hôte*>:&lt;*port*>/system/console/configMgr et procédez comme suit :

   * In the **[!UICONTROL Web Console Configuration]** page, find and click **[!UICONTROL AEM Forms Analytics Configuration]**.

   * Dans le champ **[!UICONTROL Cadre]** SiteCatalyst de la boîte de dialogue Configuration de Analytics AEM Forms, sélectionnez we-finance (nous-finance) ou we-gov (nous-gov).
   * Cliquez sur **[!UICONTROL Enregistrer]** et laissez la page s’actualiser.

1. Accédez au gestionnaire de formulaires à l’adresse https://&lt;hôte>:&lt;port>/aem/forms et procédez comme suit :

   * Ouvrez le dossier We.Finance, puis sélectionnez le formulaire pour lequel vous souhaitez afficher le rapport.
   * Dans la barre d’outils des actions, cliquez sur Rapport d’analyse. Une fois que vous avez activé les analyses pour le formulaire, cliquez sur Rapport d’analyse. Vous constatez qu’un rapport vide a été généré. Après la génération d’un rapport vierge, vous devez fournir les données d’origine fournies avec le module de site de référence pour générer le rapport d’analyse à des fins de démonstration.

   Les sites de référence fournissent au rapports d’analyse des données de base sur les cas d’utilisation des cartes de crédit, des prêts hypothécaires et des allocations familiales.

### Configuration de Target {#configure-target}

Le site de référence bénéficie de l’intégration d’Adobe Target à AEM Forms, ce qui vous permet d’incorporer du contenu ciblé et personnalisé dans des documents adaptatifs. Ce module permet également la création de tests A/B pour les formulaires adaptatifs.

Pour tester l’intégration au site de référence, procédez comme suit pour configurer Target dans AEM :

1. Start the author quickstart with the jvm argument `-Dabtesting.enabled=true` to enable A/B testing on the server.

   >[!NOTE]
   >
   >Si l’instance AEM s’exécute sur JBoss, démarré en tant que service à partir de l’installation clé en main, ajoutez le `-Dabtesting.enabled=true` paramètre dans l’entrée suivante du `jboss\bin\standalone.conf.bat` fichier :
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Accédez à l’adresse `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. In the **[!UICONTROL Adobe Target]** section, click **[!UICONTROL Show Configurations]**. Vous pouvez voir la configuration de la Cible We.Finance disponible. Cliquez pour ouvrir la configuration. Dans la page de configuration, cliquez sur **[!UICONTROL Modifier]**. The **[!UICONTROL Edit Component]** dialog for the configuration opens.

1. Indiquez vos code client, adresse électronique et mot de passe associés à votre compte Target. Sélectionnez le type d’API **[!UICONTROL REST]**.
1. Cliquez sur **[!UICONTROL Se connecter à Adobe Target]**. Une fois le compte de Cible configuré, cliquez sur **[!UICONTROL OK]**. Vous pouvez voir que la configuration empaquetée comporte une structure de Cible.

1. Accédez à `https://<hostname>:<port>/system/console/configMgr`.

1. Cliquez sur **[!UICONTROL AEM Forms Target Configuration]**.
1. Sélectionnez une structure de Cible.
1. Dans le champ **[!UICONTROL Target URLs]**, indiquez l’URL vers AEM Forms. Par exemple : `https://<hostname>:<port>/`.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

Les cas d’utilisation de demandes de carte de crédit et de demandes de prêt immobilier montrent comment effectuer des tests A/B et comment présenter un rapport à des fins de démonstration. Pour les procédures pas à pas, voir Présentation [du site de référence](../../forms/using/finance-reference-site-walkthrough.md)We.Finance.

## Etape suivante {#next-step}

Vous êtes maintenant prêt à explorer le site de référence. Pour en savoir plus sur le processus et les étapes relatifs au site de référence, consultez la section :

* [Présentation du site de référence We.Finance](../../forms/using/finance-reference-site-walkthrough.md) 
* [Présentation du site de référence de libre-service dédié aux employés](../../forms/using/employee-self-service-reference-site.md)

