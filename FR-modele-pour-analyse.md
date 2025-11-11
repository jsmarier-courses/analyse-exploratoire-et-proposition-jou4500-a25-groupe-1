**11 Novembre 2025**<br>
**CMN4500-C00 Sujets spéciaux - JOU-A00 Journalisme numérique II**<br>
**Antoine Fontaine, Jean-Marie Yard, Luna Baczynski**<br>
**Présenté à Jean-Sébastien Marier**<br>

# Analyse exploratoire de données (AED) et proposition

Utilisez un croisillon (`#`) pour créer un intertitre de niveau 1 comme celui-ci.

## Avant-propos

Pour ce travail, vous devez extraire des données d’un site Internet ou d’une base de données. Vous devez ensuite nettoyer et analyser votre jeu de données, trouver une histoire potentielle et créer une visualisation. Votre travail doit clairement expliquer votre processus. Vous devez écrire environ 1500 à 2000 mots et inclure des captures d’écran montrant les différentes étapes de votre analyse. Votre travail doit être rédigé avec le format Markdown et être publié sur GitHub.

J'assigne différentes versions de ce projet à mes étudiants en journalisme numérique et en « data storytelling » depuis déjà quelques années. La structure générale de ce travail est basée sur celle du [*Guide du datajournalisme*](http://jplusplus.github.io/guide-du-datajournalisme/index.html). La présente version est également inspirée du programme [Key Capabilities in Data Science](https://extendedlearning.ubc.ca/programs/key-capabilities-data-science) offert par l'Université de la Colombie-Britannique (UBC).

**Voici quelques ressources utiles pour ce travail :**

* [Page *Syntaxe de base pour l’écriture et la mise en forme* de GitHub](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
* [Le répertoire modèle pour ce projet au cas où vous effaceriez quelque chose par accident](https://github.com/jsmarier/jou4100_jou4500_mpad2003_project2_template)

Avez-vous remarqué comment créer un hyperlien? En langage Markdown, on met le texte cliquable entre une paire de crochets et l'adresse URL entre parenthèses.

Pour créer une liste non ordonnée, il suffit de mettre une étoile (`*`) devant chaque item.

## 1. Introduction

Dans le cadre de notre analyse exploratoire, nous allons analyser un jeu de données de la Ville d’Ottawa (https://ouverte.ottawa.ca/datasets/08575ef82f854ce6a2b275adbf06a00f/explore)  venant  du questionnaire détaillé du recensement de 2021. Notre étude portera sur l’enjeu   suivant : les heures de départ de travail pour la ville d’Ottawa. Nous allons ainsi nous demander quelle est l’heure de pointe dans les différents quartiers d’Ottawa? 
Dans cette partie,  les informations que nous prendrons vont être tirées du questionnaire détaillé importé dans Google Feuilles de Calcul. Afin de réaliser notre analyse, nous allons extraire les lignes que nous considérons importantes pour l’ensemble du travail. Nous allons travailler sur les lignes 2589 jusqu’à 2595 qui contiennent le total des heures de départ pour le travail pour la population âgée de plus de 15 ans. 
Puis, nous allons déterminer  les moyens de transports dépendamment des quartiers entre les lignes 2575 jusqu'à 2582 afin de déterminer s'ils ont un impact quelconque sur le choix de ces heures de départs. Puis la durée de navettage où l’information des lignes 2583 à 2588 et enfin leurs destination des lignes 2570 à 2574 afin de déterminer à quel point les durées de trajets peuvent varier selon l’endroit ou les fonctionnaires habitent.  Dans un premier temps, nous allons nettoyer les données afin de vérifier s’il n’existe pas de doublure ou d’erreur (espace etc). Nous avons pu observer que le jeu de données est long et part de la ligne 1 jusqu'à 2605 ce qui démontre à quel point chaque aspect de la vie à Ottawa a été traité dans le cadre de l’étude de recensement. Ainsi que tous les quartiers sans exception se sont engagés dans le recensement.  
PS: ce qui nous a  beaucoup impressionné, c’est le nombre de langue maternelle pour la population dans les ménages privés (ligne 437-ligne 1445) qui couvre ainsi 708 langues incluses dans le recensement. Bien que cette partie du recensement ne rentre pas nécessairement dans notre étude, il est important de souligner la qualité du questionnaire de recensement. 
 

## 2. Obtenir les données
J’ai importé le document contenant les données dans une nouvelle feuille de calcul dans Google Sheets. Une fois l’importation complétée, la feuille a été générée automatiquement. Celle-ci comprend 2 603 lignes et 26 colonnes de A à Z. À première analyse, toutes les données paraissent arrondies à la demi-dizaine, les données apparaissent propres, il n’y a aucun doublon, mais il y a tout de même des espaces blancs en surplus.

 ![jeu de donnée original](<Jeu de donnée original.png>)
 *Figure 1 : Jeu de Donnée original dans Google sheets.*

https://docs.google.com/spreadsheets/d/1Rkwp3R_odl47SIoTNsi8TdOu9TUpCFzRyJuqffCiZ9Q/edit?usp=sharing

Heure de départ - Variables ordinales (Intervalles de temps)
Les rangées 2589 à 2595, qui énumèrent les intervalles d’heures de départ, par exemple entre 5 h et 5 h 59 ou encore entre midi et 4 h 59, contiennent des variables ordinales.
Ces catégories peuvent être organisées dans un ordre logique croissant (du plus tôt au plus tard). Toutefois, les différences entre les groupes ne sont pas nécessairement uniformes.
 
Principal mode de transport - Variables nominales
Les rangées 2575 à la 2582 rangée, montre la variable de principal mode de transport pour la population active occupée de 15 ans et plus. Ces rangées représentent des catégories distinctes, sans hiérarchie naturelle, purement descriptives. Une variable nominale sert à identifier un nom, une étiquette ou une catégorie sans relation d’ordre entre les valeurs (par exemple : automobile, transport en commun, marche). (Statistics Canada, 2021)
 
Quartiers d’étude - Variables nominales
Les colonnes géographiques qui correspondent aux quartiers d’étude représentent une variable nominale. Chaque quartier par exemple, Orléans-Ouest-Innes - Quartier 2 et Gloucester-Southgate - Quartier 10 permet de regrouper les données en fonction de régions géographiques spécifiques. Ces catégories n’ont pas d’ordre hiérarchique ni de valeur numérique inhérente.
 
Un aspect intéressant à noter est que la liste des quartiers dans les données du jeu manque le quartier numéro 13, passant directement du 12 au 14. Le quartier de Rideau-Rockcliffe n’est pas associé à un numéro.
 
Question après avoir examiné les données brutes.
 
-   Quels sont les secteurs où habitent les fonctionnaires de la fonction publique à Ottawa (centre-ville, banlieue ou zone rurale) ? En outre, quelles sont les tendances en matière d’heures de départ et de temps de trajet quotidien par quartier pour se rendre au travail, ce qui permettrait de déterminer les heures de pointe dans la ville ?



## 3. Comprendre les données

### 3.1. Analyse VIMA

 ### 1. Durée de navetage
 
Si nous prenons la durée de trajet, nous observons que les données sont valides d’apparence et sont des variables ordinales si nous prenons la durée de navettage en minutes. Nous avons dans la colonne A, la durée de navettage comprise de 15 à 29 minutes (ligne 2) , puis celle 30 à 44 minutes (ligne 3) , ensuite 45 à 59 minutes (ligne 4) , aussi 60 minutes et plus (ligne 5) , mais encore celle de moins de 15 minutes (ligne 6) et enfin le total de la durée de navettage pour la population active (ligne 7).  Ces données permettent de faire une comparaison entre les durées les plus courtes et les plus longues sur un intervalle d'une heure de temps. Puis dans les colonnes allant de B jusqu'à Z nous avons le nom des quartiers. La section de la durée de navettage possède des données invalides. Un simple calcul d’addition des différentes durée de navettage différentes selon les quartiers (somme B2:B6, ou somme C2:C6, ou encore D2:D6, ainsi de suite) montre que le total  de la durée de navettage pour la population active pour tous les quartiers sont presques toutes fausses. Les totaux générés par le programme Google Sheets (donc automatiquement) montrent qu’il existe une divergence entre le total initial donné par le recensement de la ville  et celui calculé par le programme. Nous pouvons dire qu’il s’agit d’une donnée invalide car une donnée invalide affiche des valeurs qui paraissent impossibles (Exactitude et validation des données : méthodes pour assurer la qualité des données, statistiques Canada, 2021) . Le nombre total de répondant est valide seulement pour sept quartiers: Orléans Est-Cumberland - Quartier 1 (13965) , Gloucester-Southgate - Quartier 10 (14390) , Beacon Hill-Cyrville - Quartier 11 (9360) , Somerset - Quartier 14 (10610) , Rivière - Quartier 16 (12585) , Orléans Sud-Navan - Quartier 19 (14680) , Rideau-Jock - Quartier 21 (7890) (rempli en orange dans notre feuille de calcul)  . 
Tandis que pour le reste, le total que nous donne le recensement est à 5 ou 10 chiffres de différence du total calculé par le programme comme c’est le cas de la ville d’Ottawa qui nous donne un total de répondant de 275695 alors qu’il s’agit de 275700. Nous avons réussi à corriger cette marge d’erreur la grâce au calcul suivant par exemple: =SOMME(K2:K6) 
Pourquoi est-il important de souligner ces marges d'erreurs là ?  
Il s’agit d’un document de recensement publié par la ville d’Ottawa pourrait servir à des reportages (comme le nôtre) et ces données se doivent d'être exacts. C’est pour cela qu’il faut rester prudent et vérifier les valeurs qui nous sont donnés, surtout si ce sont des calculs d’addition que nous même pouvons faire et vérifier.
Les données ne sont pas manquantes non plus car toutes les cases sont remplies par les valeurs numériques indiquant qu’un bon nombre de répondant ont participé au recensement  dans la ville d’Ottawa (275 700 au total  pour être précis). Il n’existe pas vraiment de données aberrantes. C'est-à-dire des données qui sont inégales au reste, trop importantes ou moins importantes de façon significative. 
[Questionnaire détaillé du recensement de 2021 - Données par quartier. .pdf](https://github.com/user-attachments/files/23487429/Questionnaire.detaille.du.recensement.de.2021.-.Donnees.par.quartier.pdf)





 ### 2. Principal mode de transport

 Pour le principal mode de transport, la colonne A est une variable catégorique nominale car elle prend en compte des valeurs non quantifiables (Statistiques Canada, 2021) . La deuxième ligne indique le total des modes principaux de transport. Nous avons les  “automobiles, camions ou fourgonnettes” dans la troisième ligne, ensuite, nous avons “automobiles, camions ou fourgonnettes  - conducteur” dans la quatrième ligne, puis il y a les “automobiles, camions ou fourgonnettes - passager” dans la cinquième  ligne, puis le transport en commun dans la sixième ligne ensuite la bicyclette dans la huitième ligne et enfin les autres moyens de transports dans la neuvième ligne. La ligne 10 existe comme séparateur entre les modes de transports et la proportion en pourcentage du nombre d’automobilistes. Le reste des colonnes partant de B a Z indiquent la dimension géographique de l'étude qui sont les différents quartiers de la ville d’Ottawa. 
Nous pouvons remarquer que les données  semblent être valides. Néanmoins nous pensons qu’il aurait été préférable de séparer automobile, camions et fourgonnette dans des cas spécifiques afin de déterminer quels sont les modes de transport réellement utilisés au lieu de regrouper ces trois modes de transport en une seule. Il aurait été ainsi plus judicieux d’en faire de même pour les transports en commun car il existe le bus, mais aussi le train qu’on aurait pu séparer en deux cases distinctes, puis les usagers qui utilisent le bus et le train l’un après ou avant l’autre. Ces données sont valides mais auraient pu être plus spécifiques. Les données Invalides sont nombreuses. Chaque total allant de la case B2 à B9 comprend le nombre total de répondant exact de chaque quartier pour les modes de transport énumérés plus haut.  Sauf pour les transports en commun (3105) dans la colonne B 6, le reste des nombres est inexact de 5 ou 25 personnes comme c’est le cas par exemple pour la ligne 5 qui indique initialement 21570 répondants alors que notre calcul indique 21575 répondants ou même les utilisateurs utilisant la bicyclette (ligne 8)  qui indique 4265 alors que notre calcul nous indique plutôt 4245. Le calcul doit comprendre la somme des modes de transport de tous les quartiers que l’on additionne par la suite entre elles (Somme=C8:Z8 par exemple). Il n’existe cependant pas de données manquantes ou aberrantes. 
[Questionnaire détaillé du recensement de 2021 - Données par quartier..pdf](https://github.com/user-attachments/files/23487455/Questionnaire.detaille.du.recensement.de.2021.-.Donnees.par.quartier.pdf)



Avant d'utiliser les données ou de les transmettre aux intervenants qui le feront, assurez-vous de décrire l'exactitude des données. Il est important de documenter la façon dont nous avons exploré la validité et l'exactitude des données et celles dont vous avez nettoyé ou amélioré les données. Les utilisateurs de données utilisent ces renseignements pour savoir comment se servir des données de façon responsable (Exactitude et validation des données : méthodes pour assurer la qualité des données, statistiques Canada, 2021). 
Ainsi, nous avons rempli les cases qui affichaient le nombre total des recensement qui etaient valides de couleur jaune (fort).  https://docs.google.com/spreadsheets/d/1Rkwp3R_odl47SIoTNsi8TdOu9TUpCFzRyJuqffCiZ9Q/edit?gid=327113468#gid=327113468 . 

### 3.2. Nettoyage des données

<ins>Méthode 1:</ins> Regroupement (Clustering) dans OpenRefine
J’ai utilisé la fonction Clustering dans OpenRefine afin de détecter des doublures ou variations orthographiques dans la colonne « Population active selon l’industrie »
J’ai sélectionné la cellule à nettoyer, puis j’ai choisi l’option Édit cells, ensuite Clusters and edits, et enfin l’option Cluster. Le logiciel a alors affiché le message suivant : « No clusters were found with the selected method. » Cela signifie que les données de cette colonne étaient déjà uniformes et ne contenaient pas de valeurs presque identiques.

 
<ins>Méthode 2 :</ins> Outil de nettoyage des données dans Google Sheets
J’ai utilisé la fonction « donnée », puis « nettoyé les données » dans Google Sheets afin de repérer des doublures, espaces inutiles ou incohérences dans le jeu de données
L’outil n’a proposé aucune suggestion de nettoyage pour les pages 1, 2 et 4, ce qui indique que ces tableaux étaient déjà bien formatés et cohérents.
Cependant, les pages 3 (Principal mode transport), 5 (Toutes les professions) et 6 (Population active selon l’industrie) contenaient des cellules avec des espaces blanc.
Pour régler ce problème, j’ai utilisé la fonction DÉCOUPER, qui permet d’éliminer les espaces en début, en fin ou en double au sein d’un texte.
Après avoir appliqué cette fonction sur l’ensemble des cellules concernées, les valeurs ont été nettoyées. Cette étape a permis de rendre uniforme les données et de prévenir d’éventuelles erreurs lors de nos prochaines étapes
J’ai également utilisé l’outil de « statistiques des données » afin de m’assurer qu’aucune erreur n’avait été faite lors des étapes précédentes de nettoyage.
 
<ins>Méthode 3 :</ins> Figer les lignes et les colonnes pour faciliter la vérification
Afin de faciliter la navigation dans le jeu de données et d’assurer une vérification exacte, j’ai utilisé la fonction « Affichage ensuite figer 1 ligne et 1 colonne » dans Google Sheets.
Cette option permet de garder visibles les en-têtes de colonnes et les identifiants de rangée lors du défilement du tableau.
Cette méthode ne modifie pas les données, mais elle améliore la vérification visuelle de nos données

![Donnée nettoyée page 1](<Donnée nettoyée.png>)
*Figure 2 : Page 1 nettoyée .*

![Donnée nettoyé page 5](<Donnée nettoyée2.png>)
*Figure 3 : Page 5 nettoyée .*

### 3.3. Analyse exploratoire des données (AED)

Insérez votre texte ici.

**Cette section doit inclure une capture d'écran de votre tableau croisé dynamique, comme ceci :**

![](pivot-table-screen-capture.png)<br>
*Figure 2 : Ce tableau croisé dynamique montre...*

**Cette section doit aussi inclure une capture d'écran de votre graphique exploratoire, comme ceci :**

![](chart-screen-capture.png)<br>
*Figure 3 : Ce graphique exploratoire montre...*

## 4. Récit potentiel

Les données de la première analyse nous servent de point de départ afin de déterminer l’heure de pointe à Ottawa. Nous savons maintenant que la majorité des Ottaviens partent le matin entre 7 h et 7 h 59.

C’est le cas dans la plupart des quartiers. Cette analyse manque cependant de contexte pour en faire une histoire complète. L’heure de pointe matinale ne se résume pas à l’heure de départ, mais aussi au moyen de transport utilisé, à la distance à parcourir pour se rendre au travail et dépend également de la situation géographiqe des différents pôles d’emploi de la ville.

Le jeu de données peut répondre à certaines de ces questions. Nous l’avons vu dans la deuxième analyse sur l’utilisation de l’autombile selon les quartiers. Pour en savoir davantage sur le déroulement de l’heure de pointe, nous pourrions également interroger un chroniqueur à la circulation. Le travail de ces personnes consiste généralement à rapporter les événements qui se produisent sur le réseau routier dans les médias (surtout à la radio) et connaissent donc très bien les habitudes de déplacement des gens de leur région.

L’heure de pointe est également vécue différemment selon si l’on vit au centre-ville ou en périphérie, ou encore si on est un usager du transport en commun ou un automobiliste. Il serait donc intéressant d'interroger des représentants d’association d’usagers du transport en commun comme le groupe des usagers de transport en commun d'Ottawa (Le groupe des usagers de transport en commun d'Ottawa, n.d.) ou encore une association d’un quartier où l’heure de pointe est particulièrement dense pour les automobilistes. À Stitsville par exemple, un automobiliste rapporte dans le Ottawa Citizens devoir attendre jusqu’à 90 minutes dans la circulation sur l’autoroute 417 (Baldin, 2025). Selon cet article, des travaux de construction sur l’autoroute seraient notamment en cause. La qualité du service d’OC Transpo et le retour au bureau des fonctionnaires est également mentionné. On pourrait également questionner des syndicats de fonctionnaires fédéraux. Ces derniers avaient exprimé des craintes lors de l’annonce du retour au bureau trois jours par semaine (Côté-Sroka, 2024) quant aux transports à l’heure de pointe, selon cet article de Radio-Canada.


## 5. Conclusion

Ce travail est une participation active groupale. Il s’agit d’un long travail donc le processus fut pas mal complexe. En effet, l’analyse VIMA constituait une charge assez importante de notre travail car nous devions vérifier l'exactitude des jeux de données que nous avons utilisés. Il existe de nombreuses erreurs dans le jeu de données initial que nous avons dû corriger avant de réaliser notre tableau croisé et la retranscription de notre devoir sous forme de map dans datawrapper. Nous dirons que l’aspect le plus gratifiant a été notre maîtrise en avance  des logiciel Open refiner par lesquels nous etions deja habitue avec la fonction Cluster dans le cadre de notre cours de journalisme, ainsi que le datawrapper Map a été plutôt simple d’usage pour retranscrire les heures de pointes selon les quartiers en utilisant des couleurs qui seront facile à lire pour un public plus large.  


## 6. Références

Baldin, N. (2025, October 29). *Why is traffic so bad on Highway 417 in Ottawa? Ottawa Citizen.* Retrieved November 7, 2025, from https://ottawacitizen.com/feature/why-is-traffic-so-bad-on-highway-417-in-ottawa

Côté-Sroka, E. (2024, September 5). *Plus de jours au bureau, mais pas plus d’autobus pour les fonctionnaires.* Radio-Canada. Retrieved November 7, 2025, from https://ici.radio-canada.ca/nouvelle/2102251/retour-bureau-fonctionnaire-oc-transpo-sto-ottawa-gatineau

Le groupe des usagers de transport en commun d'Ottawa. (n.d.). *À propos de nous.* https://www.ottawatransitriders.ca/. https://www.ottawatransitriders.ca/about

Statistics Canada. (2021, September 2). *4.2 Types de variables.* https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch8/5214817-fra.htm

Exactitude et validation des données : méthodes pour assurer la qualité des données, statistics Canada,  2021: 
https://www.statcan.gc.ca/fr/afc/litteratie-donnees/catalogue/892000062020008 



