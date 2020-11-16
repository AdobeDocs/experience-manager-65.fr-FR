---
title: Développement de projets AEM à l’aide d’Eclipse
seo-title: Développement de projets AEM à l’aide d’Eclipse
description: Ce guide décrit comment utiliser Eclipse pour le développement de projets basés sur AEM
seo-description: Ce guide décrit comment utiliser Eclipse pour le développement de projets basés sur AEM
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 76%

---


# Développement de projets AEM à l’aide d’Eclipse{#how-to-develop-aem-projects-using-eclipse}

Ce guide décrit comment utiliser Eclipse pour le développement de projets basés sur AEM.

>[!NOTE]
>
>Adobe fournit désormais les [outils de développement AEM pour Eclipse](/help/sites-developing/aem-eclipse.md) qui vous aident à développer des solutions AEM avec Eclipse.

## Présentation {#overview}

Pour commencer le développement d’AEM avec Eclipse, procédez comme suit :

Chacune des étapes suivantes est expliquée plus en détail dans le reste de cette rubrique d’aide.

* Installation d’Eclipse 4.3 (Kepler)
* Configuration du projet AEM basé sur Maven
* Préparation de la prise en charge des JSP pour Eclipse dans le POM Maven
* Importation du projet Maven dans Eclipse

>[!NOTE]
>
>Cette rubrique est basée sur Eclipse 4.3 (Kepler) et AEM 5.6.1.

## Installation d’Eclipse {#install-eclipse}

Téléchargez « Eclipse IDE for Java EE Developers » (Environnement de développement intégré Eclipse pour développeurs Java EE) depuis la [page des téléchargements d’Eclipse](https://www.eclipse.org/downloads/).

Installez Eclipse en suivant les [instructions d’installation](https://wiki.eclipse.org/Eclipse/Installation).

## Configuration du projet AEM basé sur Maven {#set-up-your-aem-project-based-on-maven}

Next, set up your project using Maven as described in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Préparation de la prise en charge des JSP pour Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse peut également fournir une assistance lors de l’utilisation des JSP, par exemple pour

* le renseignement automatique des bibliothèques de balises
* la reconnaissance par Eclipse des objets définis par &lt;cq:defineObjects /> et &lt;sling:defineObjects />

Pour que cela fonctionne :

1. Follow the instructions on [How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Ajoutez la section &lt;build /> suivante au POM du module de contenu.

   Maven d’Eclipse prend en charge le plugin m2e, ne prend pas en charge le plugin maven-jspc-plugin et cette configuration indique à m2e d’ignorer le plugin et la tâche associée consistant à nettoyer les résultats de la compilation temporaire.

   This is not a problem: as noted in [How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), the maven-jspc-plugin in this setup is only used to validate that JSPs compile as part of the build process. Eclipse signale déjà les problèmes rencontrés dans les JSP et ne se repose pas sur ce plugin Maven pour le faire.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Importation du projet Maven dans Eclipse {#import-the-maven-project-into-eclipse}

1. Dans Eclipse, sélectionnez File (Ficher) > Import (Importer)...
1. Dans la boîte de dialogue d’importation, sélectionnez Maven > Existing Maven Projects (Projets Maven existants), puis cliquez sur Next (Suivant).

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Saisissez le chemin d’accès au dossier de niveau supérieur du projet et cliquez sur Select All (Tout sélectionner) et Finish (Terminer).

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Vous êtes à présent prêt à utiliser Eclipse pour développer le projet AEM, notamment la saisie semi-automatique.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >If you include `/libs/foundation/global.jsp` or other JSPs in `/libs`, you will need to copy that to your project so Eclipse can resolve the inclusion. En même temps, vous devez vous assurer qu’ils ne sont pas inclus dans le module de contenu Maven. How to achieve this is described in [How to Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

