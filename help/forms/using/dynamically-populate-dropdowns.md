---
title: Remplissage dynamique des listes déroulantes
seo-title: Remplissage dynamique des listes déroulantes
description: Procédure pour remplir de façon dynamique des listes déroulantes en fonction d’une certaine logique
seo-description: Procédure pour remplir de façon dynamique des listes déroulantes en fonction d’une certaine logique
uuid: b3408aee-ac24-43af-a380-a5892abf0248
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: ad6db3fd-0d26-4241-bf73-be74b7f6e509
docset: aem65
exl-id: 64b88423-aaae-4258-bf48-73df5c9353ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 100%

---

# Remplissage dynamique des listes déroulantes {#dynamically-populating-drop-down-lists}

## Prérequis {#prerequisites}

* [Création de lots OSGI](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr&amp;CID=RedirectAEMCommunityKautuk)
* [Développement de composants AEM](/help/sites-developing/components.md)
* [Création de formulaires adaptatifs](../../forms/using/creating-adaptive-form.md)
* [Création d’un formulaire adaptatif](../../forms/using/introduction-forms-authoring.md)

## Procédure pour remplir de façon dynamique des listes déroulantes {#procedure-to-dynamically-populate-drop-down-lists}

Supposons que vous souhaitez remplir la liste déroulante **Etat** en fonction d’une valeur que vous sélectionnez dans la liste déroulante **Pays**. Si vous sélectionnez Australie dans la liste déroulante **Pays**, la liste déroulante **Etat** affiche les états de l’Australie. La procédure ci-dessous décrit la marche à suivre.

1. Créez un projet avec les modules suivants :

   * Le lot contenant la logique pour remplir la liste déroulante, en l’occurrence une servlet.
   * Le contenu, qui incorpore le fichier .jar et possède une ressource de liste déroulante. La servlet pointe vers cette ressource.

1. Créez une servlet basée sur le paramètre de requête Pays, qui renvoie un tableau contenant les noms des états du pays.

   ```java
   @Component(metatype = false)
   @Service(value = Servlet.class)
   @Properties({
           @Property(name = "sling.servlet.resourceTypes", value = "/apps/populatedropdown"),
           @Property(name = "sling.servlet.methods", value = {"GET", "POST"}),
           @Property(name = "service.description", value = "Populate states dropdown based on country value")
   })
   public class DropDownPopulator extends SlingAllMethodsServlet {
       private Logger logger = LoggerFactory.getLogger(DropDownPopulator.class);
   
       protected void doPost(SlingHttpServletRequest request,
                             final SlingHttpServletResponse response)
               throws ServletException, IOException {
           response.setHeader("Access-Control-Allow-Origin", "*");
           response.setContentType("application/json");
           response.setCharacterEncoding("UTF-8");
           try {
               String US_STATES[] = {"0=Alabama",
                       "1=Alaska",
                       "2=Arizona",
                       "3=Arkansas",
                       "4=California",
                       "5=Colorado",
                       "6=Connecticut",
                       "7=Delaware",
                       "8=Florida",
                       "9=Georgia",
                       "10=Hawaii",
                       "11=Idaho",
                       "12=Illinois",
                       "13=Indiana",
                       "14=Iowa",
                       "15=Kansas",
                       "16=Kentucky",
                       "17=Louisiana",
                       "18=Maine",
                       "19=Maryland",
                       "20=Massachusetts",
                       "21=Michigan",
                       "22=Minnesota",
                       "23=Mississippi",
                       "24=Missouri",
                       "25=Montana",
                       "26=Nebraska",
                       "27=Nevada",
                       "28=New Hampshire",
                       "29=New Jersey",
                       "30=New Mexico",
                       "31=New York",
                       "32=North Carolina",
                       "33=North Dakota",
                       "34=Ohio",
                       "35=Oklahoma",
                       "36=Oregon",
                       "37=Pennsylvania",
                       "38=Rhode Island",
                       "39=South Carolina",
                       "40=South Dakota",
                       "41=Tennessee",
                       "42=Texas",
                       "43=Utah",
                       "44=Vermont",
                       "45=Virginia",
                       "46=Washington",
                       "47=West Virginia",
                       "48=Wisconsin",
                       "49=Wyoming"};
               String AUSTRALIAN_STATES[] = {"0=Ashmore and Cartier Islands",
                       "1=Australian Antarctic Territory",
                       "2=Australian Capital Territory",
                       "3=Christmas Island",
                       "4=Cocos (Keeling) Islands",
                       "5=Coral Sea Islands",
                       "6=Heard Island and McDonald Islands",
                       "7=Jervis Bay Territory",
                       "8=New South Wales",
                       "9=Norfolk Island",
                       "10=Northern Territory",
                       "11=Queensland",
                       "12=South Australia",
                       "13=Tasmania",
                       "14=Victoria",
                       "15=Western Australia"};
               String country = request.getParameter("country");
               JSONArray stateJsonArray = new JSONArray();
               if (country.length() > 0) {
                   if ("australia".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : AUSTRALIAN_STATES) {
                           stateJsonArray.put(state);
                       }
                   } else if ("unitedstates".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : US_STATES) {
                           stateJsonArray.put(state);
                       }
                   }
                   response.setContentType("application/json");
                   response.getWriter().write(stateJsonArray.toString());
               }
   
           } catch ( Exception e) {
               logger.error(e.getMessage(), e);
           }
       }
   }
   ```

1. Créez un nœud de liste déroulante sous une hiérarchie de dossiers spécifique dans les applications (par exemple, créez un nœud sous /apps/myfolder/demo). Veillez à ce que le paramètre `sling:resourceType` du nœud soit identique à celui vers lequel la servlet pointe (/apps/populatedropdown).

   ![Création d’un nœud de liste déroulante](assets/dropdown-node.png)

1. Empaquetez le nœud de contenu et incorporez le fichier .jar à un emplacement spécifique (par exemple /apps/myfolder/demo/install/). Déployez le même fichier sur le serveur.
1. Créez un formulaire adaptatif et ajoutez deux listes déroulantes, Pays et Etat, à ce dernier. La liste Pays peut contenir les noms des pays. La liste Etat peut remplir de manière dynamique les noms des états pour le pays sélectionné dans la première liste.

   Ajoutez les noms des pays à afficher dans la liste Pays. Dans la liste Etat, ajoutez un script pour la remplir selon le nom du pays de la liste Pays.

   ![Ajout de noms de pays](assets/country-dropdown.png) ![Ajout d’un script pour renseigner les noms d’état](assets/state-dropdown.png) ![Listes déroulantes Pays et États ensemble ](assets/2dropdowns.png)

   ```javascript
   JSON.parse(
       $.ajax({
           url: "/apps/myfolder/demo/dropdown",
           type: "POST",
           async: false,
           data: {"country": country.value},
            success: function(res){},
            error : function (message) {
                 guideBridge._guide.logger().log(message);
                 successFlag = false;
                 }
              })
   .responseText);
   ```

Package de contenu contenant un exemple de formulaire adaptatif (demo/AFdemo) avec le code ci-dessus implémenté.

[Obtenir le fichier](assets/dropdown-demo-content-1.0.1-snapshot.zip)
