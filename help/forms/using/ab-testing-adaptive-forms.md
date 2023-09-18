---
title: Créer et gérer des tests A/B pour les formulaires adaptatifs
description: AEM Forms s’intègre à Adobe Target qui permet d’exécuter des tests A/B pour que les formulaires adaptatifs améliorent l’expérience client et les taux de conversion.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 61%

---

# Créer et gérer des tests A/B pour les formulaires adaptatifs{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE Arrêté]{type=negative tooltip="Cette fonctionnalité est désormais en fin de vie."}

<div class="preview"> Les tests A/B pour la fonctionnalité de formulaires adaptatifs ont atteint la fin de vie et ne sont plus pris en charge. </div>

## Présentation {#overview-br}

Vos clientes et clients sont susceptibles d’abandonner un formulaire si l’expérience qui en résulte n’est pas satisfaisante. Bien que cela soit frustrant pour les clients, cela peut également renverser le volume et les coûts d’assistance pour votre entreprise. Il est essentiel et difficile d’identifier et de fournir l’expérience client appropriée qui augmente le taux de conversion. Adobe Experience Manager Forms détient la clé de ce problème.

AEM Forms s’intègre à Adobe Target, une solution Adobe Experience Cloud, afin de proposer des expériences client personnalisées et attrayantes sur plusieurs canaux numériques. L’une des fonctionnalités clés de Target est le test A/B qui vous permet de configurer rapidement des tests A/B simultanés, de présenter du contenu pertinent aux utilisateurs ciblés et d’identifier l’expérience qui entraîne un meilleur taux de conversion.

Avec Adobe Experience Manager (AEM) Forms, vous pouvez configurer et exécuter des tests A/B sur des formulaires adaptatifs en temps réel. Il fournit également des fonctionnalités de création de rapports personnalisables et prêtes à l’emploi pour visualiser les performances en temps réel de vos expériences de formulaire et identifier celle qui optimise l’interaction client et la conversion des utilisateurs et utilisatrices.

## Configurer et intégrer Target à AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Avant de commencer à créer et analyser des tests A/B pour les formulaires adaptatifs, vous devez configurer votre serveur Target et l’intégrer à AEM Forms.

### Configurer Target {#set-up-target}

Pour intégrer AEM à Target, vérifiez que vous disposez d’un compte Adobe Target valide. Lorsque vous vous inscrivez à Adobe Target, vous recevez un code client. Vous avez besoin du code client, de l’adresse électronique associée au compte Target et du mot de passe pour vous connecter AEM à Target.

Le code client identifie le compte client Adobe Target et est utilisé comme un sous-domaine dans l’URL lors de l’appel du serveur Adobe Target. Avant de commencer, connectez-vous à [https://experience.adobe.com/](https://experience.adobe.com/) et, si vous y avez accès, consultez lʼoption [!DNL Adobe Target] dans la section [!UICONTROL Accès rapide].

### Intégration d’un serveur Target en cours d’exécution à AEM Forms {#integrate-target-in-aem-forms}

1. Sur le serveur AEM, accédez à https://&lt;*nom de lʼhôte*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Dans le **Adobe Target** , cliquez sur **Afficher les configurations** puis la fonction **+** pour ajouter une configuration.
Si vous configurez une cible pour la première fois, cliquez sur **Configurez maintenant.**

1. Dans la boîte de dialogue Créer une configuration, spécifiez un **titre** et éventuellement un **nom** pour la configuration.

1. Cliquez sur **Créer**. La boîte de dialogue Modifier le composant s’ouvre.
1. Spécifiez les détails de votre compte Target, tels que le code client, l’adresse e-mail et le mot de passe.
1. Sélectionnez **Rest** dans la liste déroulante Type d’API.

1. Cliquez sur **Connexion à Adobe Target** vous pouvez donc initialiser la connexion à Target. Si la connexion est réussie, le message Connexion réussie s’affiche. Cliquez sur **OK** dans le message et **OK** dans la boîte de dialogue. Le compte Target est configuré.

1. Créez une structure Target, comme décrit à la section [Ajout d’une structure](/help/sites-administering/target.md).

1. Rendez-vous sur https://&lt;*nom de lʼhôte*>:&lt;*port*>/system/console/configMgr.

1. Cliquez sur **Configuration de Target dans AEM Forms**.
1. Sélectionnez un **framework Target**.
1. Dans le **URL Target** , spécifiez toutes les URL où s’exécutent les tests A/B. Par exemple, https://&lt;*hostname*>:&lt;*port*>/ pour le serveur AEM Forms sur OSGi ou https://&lt;*hostname*>:&lt;*port*>/lc/ pour AEM Forms Server on JEE.
Pensez à configurer une URL Target pour une instance de publication à laquelle vos clients peuvent accéder à l’aide du nom d’hôte ou de l’adresse IP. Dans ce cas, vous devez configurer comme URL Target en utilisant le nom d’hôte et l’adresse IP. Si vous configurez uniquement l’une des URL, votre test A/B ne s’exécute pas pour les clients provenant de l’autre URL. Cliquez sur le signe **+** pour spécifier plusieurs URL.

1. Cliquez sur **Enregistrer**.

Votre serveur Target est intégré à AEM Forms. Vous pouvez désormais activer le test A/B si vous disposez d’une licence complète vous permettant d’utiliser Adobe Target.

Si vous disposez d’une licence complète pour utiliser Adobe Target, démarrez le serveur avec les paramètres suivants après avoir intégré Target avec AEM Forms :

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Si l’instance AEM s’exécute sur JBoss®, démarrée en tant que service à partir de la clé en main, dans `jboss\bin\standalone.conf.bat` Ajoutez le paramètre -Dabtesting.enabled=true dans l’entrée suivante :

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Outre le serveur JBoss®, vous pouvez ajouter l’argument jvm -Dabtesting.enabled=true dans le script de démarrage du serveur pour n’importe quel serveur d’applications. Vous pouvez à présent créer et exécuter des tests A/B pour les formulaires adaptatifs.

>[!NOTE]
>
>Si vous mettez à jour les URL Target configurées ultérieurement, veillez à mettre à jour tous les tests A/B actifs pour qu’ils pointent vers les URL mises à jour. Pour plus d’informations sur la mise à jour des tests A/B, consultez [Mettre à jour le test A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## Créer des audiences dans AEM {#create-audiences-within-aem}

AEM vous permet de créer une audience et de l’utiliser pour un test A/B. L’audience que vous créez dans AEM est disponible dans AEM Forms. Pour créer des audiences dans AEM, procédez comme suit :

1. Dans l’instance d’auteur, appuyez sur **Adobe Experience Manager** > **Personnalisation** > **Publics**.

1. Dans la page Publics, appuyez sur **Créer un public > Créer le public cible**.
1. Dans la boîte de dialogue Configuration d’Adobe Target, sélectionnez une configuration Cible et cliquez sur **Ok**.
1. Sur la page Créer une audience, créez des règles. Les règles vous permettent de catégoriser l’audience. Par exemple, vous souhaitez catégoriser les audiences en fonction du système d’exploitation. Votre audience A provient de Windows et l’audience B de Linux®.

   1. Pour catégoriser une audience en fonction de Windows, dans la #1 de règle, sélectionnez le **SE** type d’attribut. Dans la liste déroulante, sélectionnez **Windows.**

   1. Pour classer l’audience en fonction de Linux®, dans #2 de règle, sélectionnez le **SE** type d’attribut. Dans la **When** , sélectionnez **Linux®**, puis cliquez sur **Suivant**.

1. Spécifiez un nom pour le public créé, puis cliquez sur **Enregistrer**.

Vous pouvez sélectionner l’audience lorsque vous configurez le test A/B d’un formulaire, comme illustré ci-dessous.

## Créer un test A/B pour un formulaire adaptatif {#create-a-b-test}

1. Accédez à **Formulaires et Documents** à l’adresse https://&lt;*nom de lʼhôte*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Accédez au dossier contenant le formulaire adaptatif.
1. Cliquez sur l’outil **Sélectionner** dans la barre d’outils et sélectionnez le formulaire adaptatif.
1. Cliquez sur **Plus** dans la barre d’outils, puis sélectionnez **Configuration des tests A/B**. La page de configuration des tests A/B s’ouvre.

[](assets/ab-test-configure-1.png)

1. Spécifiez un **nom d’activité** pour le test A/B.

1. Dans la liste déroulante Audience, sélectionnez une audience pour laquelle vous souhaitez proposer différentes expériences du formulaire. Par exemple, **visiteurs et visiteuses utilisant Chrome**. La liste des audiences est renseignée à partir du serveur Target configuré.

1. Dans les champs **Distribution d’expérience** pour les expériences A et B, spécifiez la répartition, sous forme de pourcentage, pour déterminer la répartition des expériences dans l’audience totale. Par exemple, si vous spécifiez 40, 60 pour les expériences A et B, respectivement, l’expérience A est transmise à 40 % de l’audience et les 60 % restants voient l’expérience B.
1. Cliquez sur **Configurer**. Une boîte de dialogue s’affiche pour confirmer la création du test A/B.
1. Cliquez sur **Modifier l’expérience B** vous pouvez ainsi ouvrir le formulaire adaptatif en mode d’édition. Modifiez le formulaire en créant une expérience différente de l’expérience A par défaut. Les variations possibles autorisées dans l’expérience B sont des modifications dans :

   * CSS ou style
   * Ordre des champs dans différents panneaux ou le même panneau
   * Disposition de panneau
   * Titres de panneau
   * Description, libellé et texte d’aide pour un champ
   * Scripts qui n’affectent pas ou n’interrompent pas le flux d’envoi
   * Validations (côté client et côté serveur)
   * Thème de l’expérience B (vous pouvez sélectionner un autre thème pour l’expérience B)

1. Accédez à l’interface utilisateur Formulaires et documents, sélectionnez le formulaire adaptatif, cliquez sur **Plus**, puis sélectionnez **Démarrer le test A/B**.

Votre test A/B est maintenant en cours d’exécution et l’audience spécifiée reçoit les expériences de manière aléatoire en fonction de la distribution spécifiée.

## Mise à jour du test A/B {#update-a-b-test}

Vous pouvez mettre à jour l’audience et la répartition d’expérience d’un test A/B en cours d’exécution.

Pour mettre à jour le test A/B :

1. Dans l’interface utilisateur Formulaires et documents, accédez au dossier contenant le formulaire adaptatif sur lequel le test A/B s’exécute.
1. Sélectionnez le formulaire adaptatif.
1. Cliquez sur **Plus** puis sélectionnez **Modifier le test A/B**. La page de mise à jour du test A/B s’ouvre.

1. Mettez à jour l’audience et la répartition d’expérience, si nécessaire.
1. Cliquez sur **Mettre à jour**.

## Afficher et analyser le rapport de test A/B {#view-and-analyze-a-b-test-report}

Une fois que vous avez activé l’exécution du test A/B pendant la période souhaitée, vous pouvez générer un rapport et contrôler quelle expérience a obtenu la meilleure conversion. Vous pouvez déclarer gagnante l’expérience la plus performante ou choisir d’exécuter un autre test A/B.

Pour afficher et analyser le rapport de test A/B :

1. Sélectionnez le formulaire adaptatif, cliquez sur le bouton **Plus**, puis cliquez sur **Rapport du test A/B**. Le rapport s’affiche.

[](assets/ab-test-report-3.png)

1. Analysez le rapport et voyez si vous disposez de suffisamment de points de données pour décider quelle expérience a le mieux fonctionné. Vous pouvez choisir de continuer le même test A/B pendant plus longtemps ou de désigner une expérience probante et terminer le test A/B.
1. Pour désigner un gagnant et terminer le test A/B, cliquez sur le bouton **Fin du test A/B** dans le tableau de bord des rapports. Une boîte de dialogue vous invite à désigner comme gagnante l’une des deux expériences. Sélectionnez l’expérience la plus probante et confirmez la fin du test A/B.
 Autrement, vous pouvez d’abord désigner une expérience gagnante en cliquant sur le bouton **Déclarer gagnante** de l’expérience correspondante. Vous êtes invité(e) à confirmer l’expérience gagnante. Cliquez sur **Oui** pour terminer le test A/B.

Si vous avez sélectionné l’expérience A comme expérience gagnante, le test A/B est mis fin et, à partir de ce moment, seule l’expérience A est transmise aux audiences.
