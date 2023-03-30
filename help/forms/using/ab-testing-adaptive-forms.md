---
title: Créer et gérer des tests A/B pour les formulaires adaptatifs
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms s’intègre à Adobe Target qui permet d’exécuter des tests A/B pour que les formulaires adaptatifs améliorent l’expérience client et les taux de conversion.
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ccbb6a33c2ee8029d2e82d9098c07de18af166ac
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 43%

---

# Créer et gérer des tests A/B pour les formulaires adaptatifs{#create-and-manage-a-b-test-for-adaptive-forms}

|Négatifs|[!BADGE Arrêt]{type=negative tooltip="Cette fonctionnalité est désormais en fin de vie."}|
<div class="preview"> Le test A/B pour la fonctionnalité de formulaires adaptatifs a atteint la fin de vie et n’est plus pris en charge. </div>

## Présentation {#overview-br}

Il est probable que vos clients abandonnent un formulaire si l’expérience qu’il offre n’est pas engageante. Bien que cela soit frustrant pour les clients, cela peut également augmenter le volume et le coût de l’assistance pour votre entreprise. Il est essentiel et difficile d’identifier et de fournir une expérience client adaptée qui augmente le taux de conversion. Adobe Experience Manager Forms détient la clé de ce problème.

AEM Forms s’intègre à Adobe Target, une solution Adobe Marketing Cloud, afin de proposer des expériences client personnalisées et attrayantes sur plusieurs canaux numériques. L’une des fonctionnalités clés de Target est le test A/B qui vous permet de configurer rapidement des tests A/B simultanés, de présenter du contenu pertinent aux utilisateurs ciblés et d’identifier l’expérience qui entraîne un meilleur taux de conversion.

Avec AEM Forms, vous pouvez configurer et exécuter des tests A/B sur des formulaires adaptatifs en temps réel. Il fournit également des fonctionnalités de création de rapports personnalisables et prêtes à l’emploi pour visualiser les performances en temps réel de vos expériences de formulaire et identifier celle qui optimise l’engagement et la conversion des utilisateurs.

## Configuration et intégration de Target dans AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Avant de commencer à créer et analyser des tests A/B pour les formulaires adaptatifs, vous devez configurer votre serveur Target et l’intégrer à AEM Forms.

### Configuration de Target {#set-up-target}

Pour intégrer AEM à Target, vérifiez que vous disposez d’un compte Adobe Target valide. Lorsque vous vous inscrivez à Adobe Target, vous recevez un code client. Vous avez besoin du code client, de l’adresse électronique associée au compte Target et du mot de passe pour vous connecter AEM à Target.

Le code client identifie le compte client Adobe Target et est utilisé comme un sous-domaine dans l’URL lors de l’appel du serveur Adobe Target. Avant de commencer, connectez-vous à [https://experience.adobe.com/](https://experience.adobe.com/) et, si vous y avez accès, consultez lʼoption [!DNL Adobe Target] dans la section [!UICONTROL Accès rapide].

### Intégration de Target dans AEM Forms {#integrate-target-in-aem-forms}

Pour intégrer un serveur Target en cours d’exécution à AEM Forms, procédez comme suit :

1. Sur le serveur AEM, accédez à https://&lt;*nom de lʼhôte*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Dans la section **Adobe Target**, cliquez sur **Afficher les configurations** puis sur l’icône **+** pour ajouter une nouvelle configuration.
Si vous configurez Target pour la première fois, cliquez sur **Configurer maintenant.**

1. Dans la boîte de dialogue Créer une configuration , spécifiez une **Titre** et éventuellement un **Nom** pour la configuration.

1. Cliquez sur **Créer**. La boîte de dialogue Modifier le composant s’ouvre.
1. Spécifiez les détails de votre compte Target, tels que le code client, l’adresse électronique et le mot de passe.
1. Sélectionnez **Rest** dans la liste déroulante Type d’API.

1. Cliquez sur **Se connecter à Adobe Target** pour lancer la connexion à Target. Si la connexion est réussie, le message Connexion réussie s’affiche. Cliquez sur **OK** dans le message et **OK** dans la boîte de dialogue. Le compte Target est configuré.

1. Créez une structure Target, comme décrit à la section [Ajout d’une structure](/help/sites-administering/target.md).

1. Rendez-vous sur https://&lt;*nom de lʼhôte*>:&lt;*port*>/system/console/configMgr.

1. Cliquez sur **Configuration d’AEM Forms Target**.
1. Sélectionnez une **Structure cible**.
1. Dans le **URL Target** , spécifiez toutes les URL où les tests A/B seront exécutés. Par exemple, https://&lt;*nom de lʼhôte*>:&lt;*port*>/ pour le serveur AEM Forms sur OSGi ou https://&lt;*nom de lʼhôte*>:&lt;*port*>/lc/ pour le serveur AEM Forms sur JEE.
 Si vous souhaitez configurer une URL Target pour une instance de publication à laquelle vos clients peuvent accéder à l’aide du nom d’hôte ou de l’adresse IP, vous devez configurer les deux comme des URL Target (via le nom d’hôte ainsi que l’adresse IP). Si vous configurez uniquement une des URL, votre test A/B ne s’exécutera pas pour les clients provenant de l’autre URL. Cliquez sur le signe **+** pour spécifier plusieurs URL.

1. Cliquez sur **Enregistrer**.

Votre serveur Target est intégré à AEM Forms. Vous pouvez désormais activer le test A/B si vous disposez d’une licence complète vous permettant d’utiliser Adobe Target.

Si vous disposez d’une licence complète vous permettant d’utiliser Adobe Target, démarrez le serveur selon les paramètres suivants après avoir intégré Target avec AEM Forms :

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Si une instance AEM s’exécute sur JBoss, démarrée en tant que procédure clé en main, dans le fichier `jboss\bin\standalone.conf.bat`, ajoutez le paramètre -Dabtesting.enabled=true dans l’entrée suivante :

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Outre le serveur jboss, vous pouvez ajouter l’argument jvm -Dabtesting.enabled=true dans le script de démarrage du serveur pour n’importe quel serveur d’applications. Vous pouvez désormais créer et exécuter des tests A/B pour les formulaires adaptatifs.

>[!NOTE]
>
>Si vous mettez à jour les URL Target configurées ultérieurement, veillez à mettre à jour les tests A/B en cours d’exécution afin qu’ils pointent vers les URL actuelles. Pour plus d’informations sur la mise à jour des tests A/B, voir [Mettre à jour le test A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## Création d’audiences dans AEM {#create-audiences-within-aem}

AEM permet de créer une audience et de l’utiliser pour un test A/B. L’audience que vous créez dans AEM est disponible dans AEM Forms. Pour créer des audiences dans AEM, procédez comme suit :

1. Dans l’instance d’auteur, appuyez sur **Adobe Experience Manager** > **Personnalisation** > **Publics**.

1. Dans la page Publics, appuyez sur **Créer un public > Créer le public cible**.
1. Dans la boîte de dialogue Configuration d’Adobe Target, sélectionnez une configuration Cible et cliquez sur **Ok**.
1. Sur la page Créer une audience , créez des règles. Les règles vous permettent de catégoriser l’audience. Par exemple, vous souhaitez catégoriser les audiences en fonction du système d’exploitation. Votre audience A provient de Windows et l’audience B de Linux.

   1. Pour catégoriser lʼaudience en fonction de Windows, dans la règle n°1, sélectionnez le type d’attribut **OS**. Dans la liste déroulante, sélectionnez **Windows.**

   1. Pour catégoriser lʼaudience en fonction de Linux, dans la règle n°2, sélectionnez le type d’attribut **OS**. Dans la liste **déroulante**, sélectionnez **Linux**, puis cliquez sur **Suivant**.

1. Spécifiez un nom pour le public créé, puis cliquez sur **Enregistrer**.

Vous pouvez sélectionner l’audience lorsque vous configurez les tests A/B pour un formulaire, comme illustré ci-dessous.

## Création d’un test A/B {#create-a-b-test}

Pour créer un test A/B pour un formulaire adaptatif, procédez comme suit.

1. Accédez à **Formulaires et Documents** à l’adresse https://&lt;*nom de lʼhôte*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Accédez au dossier contenant le formulaire adaptatif.
1. Cliquez sur le bouton **Sélectionner** dans la barre d’outils et sélectionnez le formulaire adaptatif.
1. Cliquez sur **Plus** dans la barre d’outils et sélectionnez **Configuration des tests A/B**. La page Configurer les tests A/B s’ouvre.

[ ](assets/ab-test-configure-1.png)

1. Spécifiez un **nom d’activité** pour le test A/B.

1. Dans la liste déroulante Audience , sélectionnez une audience à qui vous souhaitez proposer différentes expériences du formulaire. Par exemple : **Visiteurs utilisant Chrome**. La liste des audiences est renseignée à partir du serveur Target configuré.

1. Dans le **Distribution de l’expérience** pour les expériences A et B, spécifiez la répartition, en termes de pourcentage, afin de déterminer la distribution des expériences entre l’audience totale. Par exemple, si vous spécifiez 40, 60 pour les expériences A et B, respectivement, l’expérience A sera transmise à 40 % de l’audience et les 60 % restants verront l’expérience B.
1. Cliquez sur **Configurer**. Une boîte de dialogue s’affiche pour confirmer la création du test A/B.
1. Cliquez sur **Modifier l’expérience B** pour ouvrir le formulaire adaptatif en mode d’édition. Modifiez le formulaire pour créer une expérience différente de l’expérience A par défaut. Les variations possibles permises dans l’expérience B sont des modifications concernant :

   * CSS ou style
   * Ordre des champs dans différents panneaux ou le même panneau
   * Disposition de panneau
   * Titres des panneaux
   * Description, libellé et texte d’aide pour un champ
   * Scripts qui n’affectent pas ou n’interrompent pas le flux d’envoi
   * Validations (côté client et côté serveur)
   * Thème de l’expérience B (vous pouvez sélectionner un autre thème pour l’expérience B)

1. Accédez à l’interface utilisateur Forms and Documents, sélectionnez le formulaire adaptatif, puis cliquez sur **Plus**, puis sélectionnez **Démarrer le test A/B**.

Votre test A/B est maintenant en cours d’exécution et l’audience spécifiée recevra aléatoirement les expériences en fonction de la distribution spécifiée.

## Mettre à jour le test A/B {#update-a-b-test}

Vous pouvez mettre à jour l’audience et la répartition d’expérience d’un test A/B en cours d’exécution. Pour ce faire :

1. Dans l’interface utilisateur de Forms &amp; Documents, accédez au dossier contenant le formulaire adaptatif sur lequel le test A/B est exécuté.
1. Sélectionnez le formulaire adaptatif.
1. Cliquez sur **Plus** puis sélectionnez **Modifier le test A/B**. La page de mise à jour du test A/B s’ouvre.

1. Mettez à jour l’audience et la répartition d’expérience, selon les besoins.
1. Cliquez sur **Mettre à jour**.

## Afficher et analyser le rapport de test A/B {#view-and-analyze-a-b-test-report}

Une fois que vous avez activé l’exécution du test A/B pendant la période souhaitée, vous pouvez générer un rapport et contrôler quelle expérience a obtenu la meilleure conversion. Vous pouvez déclarer gagnante l’expérience la plus performante ou choisir d’exécuter un autre test A/B. Pour ce faire, procédez comme suit :

1. Sélectionnez le formulaire adaptatif, puis cliquez sur **Plus**, puis cliquez sur **Rapport de test A/B**. Le rapport s’affiche.

[ ](assets/ab-test-report-3.png)

1. Analysez le rapport et voyez si vous disposez de suffisamment de points de données pour décider quelle expérience a le mieux fonctionné. Vous pouvez choisir de continuer le même test A/B pendant plus longtemps ou de désigner une expérience probante et terminer le test A/B.
1. Pour déclarer qu’une expérience est probante et terminer les tests A/B, cliquez sur le bouton **Terminer le test A/B** sur le tableau de bord de génération de rapports. Une boîte de dialogue vous invite à déclarer l’une des deux expériences gagnantes. Sélectionnez l’expérience la plus probante et confirmez la fin du test A/B.
 Autrement, vous pouvez d’abord désigner une expérience gagnante en cliquant sur le bouton **Déclarer gagnante** de l’expérience correspondante. Vous êtes invité(e) à confirmer l’expérience gagnante. Cliquez sur **Oui** pour terminer le test A/B.

Si vous considérez que l’expérience A est la meilleure, le test A/B sera arrêté, et à partir de ce moment-là, seule l’expérience A sera transmise à tous les publics.
