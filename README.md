# **Rapport de Projet — Atlantic Haven Hotels**

## **Examen Final Machine Learning & Data Science — M1**

Réalisé au sein de **ISPM — Madagascar** ([www.ispm-edu.com](https://www.ispm-edu.com))

---

### **1. Informations sur le Groupe**

Merci de lister tous les membres de l’équipe ayant effectivement participé au Hackathon.

#### Membre 1

- nom : LIOKA Ranarison 
- prénom(s) : Fiderana
- classe : IGGLIA 4
- numéro :  33
- rôle : développeur, analyste.

#### Membre 2

- nom : AINA RAKOTONDRAMBOLA 
- prénom(s) : Lova Nasaina
- classe : IGGLIA 4
- numéro : 06
- rôle : Lead Developer, Data Scientist

#### Membre 3

- nom : RASOAMAMPIONONA  
- prénom(s) : Honorine
- classe : ISAIA 4
- numéro : 02
- rôle : responsable de la modélisation, présentateur.

#### Membre 4

- nom : RAKOTOARISON 
- prénom(s) : Andonirina Robisaona
- classe : IGGLIA 4
- numéro : 13
- rôle : analyste, présentateur.

#### Membre 5

- nom : RAHERIMANANTENA 
- prénom(s) : Fedro Hubert
- classe : IGGLIA 4
- numéro : 20
- rôle : développeur, analyste.

#### Membre 6

- nom : ZAFINDRAMANGA 
- prénom(s) : Lubain Fadhel
- classe : IGGLIA 4
- numéro : 36
- rôle : développeur, analyste.

#### Membre 7

- nom : RAKOTOARIMANITRA 
- prénom(s) : Andy Franck
- classe : IGGLIA 4
- numéro : 12
- rôle : analyste, responsable de la modélisation, présentateur.

---

### **2. Résumé du Travail**

#### Problématique

Les annulations tardives de réservations entraînent une perte sèche pour Atlantic Haven Hotels en laissant des chambres vacantes impossibles à relouer à temps. Prédire suffisamment tôt la probabilité d'annulation permet d'anticiper la gestion des stocks, d'ajuster les politiques de surréservation intelligentes et de sécuriser les revenus sans pénaliser les clients fidèles.  

#### Méthodologie adoptée

Le jeu de données présentant une composante chronologique stricte, nous avons écarté la validation croisée aléatoire au profit d'un découpage temporel (les 80% de réservations les plus anciennes pour l'entraînement, les 20% les plus récentes pour la validation). Nous avons appliqué un pipeline de prétraitement robuste, créé de nouvelles variables temporelles et comportementales (taux d'annulation historique, délai par nuit), puis comparé une Régression Logistique (baseline) avec des algorithmes ensemblistes (Random Forest et HistGradientBoosting).

#### Résultats obtenus

Sur notre jeu de test, le meilleur F1-score obtenu est de 0,4681, avec la régression logistique, pour un seuil de décision de 0,50. Elle présente également le meilleur rappel (0,6755) et le meilleur ROC-AUC (0,6777) parmi les modèles évalués.

#### Mots-clés

Classification binaire, validation temporelle, F1-score, feature engineering, pipeline sklearn, concept drift, régression logistique.

---

### **3. Contenu du Repository**

Voici la liste des fichiers et liens importants permettant d’évaluer votre travail :


- *notebook.ipynb* : code complet de l’EDA, du prétraitement, de la modélisation et de l’évaluation — exécutable de bout en bout depuis un noyau vierge (sorties incluses) ;
- *submission.csv* : prédictions sur reservations_test.csv (2 000 lignes, 3 colonnes, ordre des identifiants préservé) ;
- *README.md* : présent rapport ;
- *requirements.txt* : dépendances nécessaires à la reproduction ;
- *scripts/* : versions scripts des étapes (EDA, features, modèles, analyse d'erreurs, soumission, génération du notebook).

*🔗 Liens utiles :*

- [**LIEN VERS LA VIDÉO DE PRÉSENTATION** — https://photos.app.goo.gl/Lfntc3fTLCp6HRmdAhttps://photos.app.goo.gl/Lfntc3fTLCp6HRmdA
- [Lien vers le dépôt GitHub](https://github.com/) (à compléter)

---
### *4. Résultats de Modélisation*

Les quatre modèles ont été entraînés et évalués sur le **même jeu de test**, avec `reservation_annulee` comme variable cible. Les métriques retenues sont le F1-score, la précision, le rappel et le ROC-AUC.

| Modèle | Paramètres principaux | F1-score | Précision | Rappel | ROC-AUC |
|---|---|---:|---:|---:|---:|
| Régression logistique — baseline | `max_iter=1000` | 0,4681 | 0,3582 | 0,6755 | 0,6777 |
| KNN | `k=15`, `weights=distance` | 0,1028 | 0,4444 | 0,0581 | 0,5762 |
| Forêt aléatoire | 300 arbres, `max_depth=15`, `min_samples_leaf=2`, `class_weight=balanced`** | 0,4009 | 0,3930 | 0,4092 | 0,6560 |
| XGBoost | 300 arbres, `learning_rate=0,05`, `max_depth=6` | 0,2022 | 0,4463 | 0,1308 | 0,6551 |

*Seuil de décision retenu :* seuil par défaut de **0,50** pour l'ensemble des modèles. Les résultats correspondent aux prédictions obtenues directement sur le jeu de test, sans optimisation supplémentaire du seuil de classification.

*Justification du choix du modèle final :*

La **régression logistique** présente les meilleures performances globales parmi les modèles évalués. Elle obtient le meilleur **F1-score (0,4681)**, le meilleur **rappel (0,6755)** ainsi que le meilleur **ROC-AUC (0,6777)**. Son rappel élevé signifie qu'elle parvient à identifier une proportion importante des réservations réellement annulées.

La **forêt aléatoire** constitue la deuxième meilleure approche avec un F1-score de **0,4009** et un rappel de **0,4092**. Elle offre ainsi un compromis intéressant entre précision et rappel, tout en permettant de modéliser des relations non linéaires entre les variables.

Le **KNN** et **XGBoost** présentent une accuracy relativement élevée, respectivement **0,7381** et **0,7338**, mais leurs rappels restent faibles (**0,0581** et **0,1308**). Leur bonne accuracy est donc insuffisante pour conclure à une bonne capacité de détection des annulations.

Dans le contexte de ce projet, le **rappel et le F1-score sont privilégiés par rapport à l'accuracy**, car l'objectif principal est de détecter les réservations susceptibles d'être annulées. La **régression logistique est donc retenue comme modèle final de cette première expérimentation**.

---
### **5. Réponses aux Questions d’Analyse**

*Répondez précisément aux questions ci-dessous. Utilisez des chiffres, tableaux ou références à vos graphiques pour justifier vos réponses.*

#### **Q1. Pourquoi utilise-t-on principalement le F1-score plutôt que l’accuracy pour cette tâche ?**

L'accuracy peut être trompeuse lorsque les classes sont déséquilibrées. Ici, l'objectif principal est de détecter les réservations annulées.
Le F1-score combine la précision et le rappel et permet donc d'évaluer simultanément la capacité du modèle à détecter les annulations et à limiter les fausses alertes.
Par exemple, KNN obtient une accuracy de 0,7381, mais un rappel très faible de 0,0581 et un F1-score de seulement 0,1028. À l'inverse, la régression logistique obtient un F1-score de 0,4681 et un rappel de 0,6755.

Ainsi, le F1-score est plus pertinent que l'accuracy pour cette tâche.

#### **Q2. Dans ce contexte, qu’est-ce qui est le plus grave : un faux positif ou un faux négatif ?**

Dans le contexte hôtelier :

Faux positif (FP) : le modèle prédit une annulation alors que la réservation est finalement maintenue.
Faux négatif (FN) : le modèle prédit une réservation maintenue alors qu'elle sera finalement annulée.

Le faux négatif est généralement plus problématique, car l'hôtel ne peut pas anticiper la perte de la réservation ni prendre de mesure préventive.

Cependant, les faux positifs doivent également être limités afin d'éviter des interventions inutiles auprès des clients.

#### **Q3. Quelles variables créées par feature engineering ont le plus amélioré votre modèle par rapport à la régression logistique de référence ?**

Les variables de feature engineering ayant apporté le plus de gain doivent être déterminées à partir de la comparaison entre la régression logistique baseline et la version finale.

#### **Q4. Pourquoi un découpage aléatoire simple peut-il produire une évaluation trompeuse sur ce dataset ?**

Un découpage aléatoire peut mélanger des réservations anciennes et récentes dans les ensembles d'entraînement et de test. Cela peut donner une estimation trop optimiste des performances, car le modèle est évalué sur des données provenant d'une période similaire à celle utilisée pour l'apprentissage.

Une validation temporelle est donc préférable : les données anciennes sont utilisées pour l'entraînement et les données plus récentes pour le test.

Cette stratégie reproduit mieux l'utilisation réelle du modèle, où l'on entraîne le système sur l'historique pour prédire les futures réservations.

#### **Q5. Quels profils ou scénarios de réservation sont les plus fréquemment associés aux annulations dans vos analyses ?**

Les annulations doivent être analysées à partir des caractéristiques observées dans les données. Les facteurs pouvant notamment être étudiés sont :

le délai entre la réservation et l'arrivée ;
le type de tarif et ses conditions de remboursement ;
la durée du séjour ;
le canal de réservation ;
l'historique d'annulations ;
le nombre de modifications de la réservation ;
le nombre de demandes spéciales.

Ces facteurs doivent être interprétés comme des caractéristiques associées aux réservations, et non comme des propriétés intrinsèques d'une région ou d'une population.

#### **Q6. Comment votre pipeline traite-t-il les valeurs manquantes et les catégories jamais observées pendant l’entraînement ?**

Les valeurs manquantes sont traitées dans le pipeline de prétraitement. Pour les variables numériques, une statistique calculée sur l'entraînement, comme la médiane, peut être utilisée. Pour les variables catégorielles, les valeurs inconnues peuvent être regroupées dans une catégorie dédiée.

L'encodage est configuré pour gérer les catégories qui n'ont jamais été observées pendant l'entraînement.

Les paramètres du prétraitement sont appris uniquement sur les données d'entraînement, puis appliqués aux données de validation et de test. Cela permet d'éviter la fuite de données.

#### **Q7. Selon vous, quelle action l’hôtel devrait-il entreprendre lorsqu’une réservation en cours présente une forte probabilité d’annulation ?**
L'hôtel ne devrait pas annuler automatiquement la réservation.

Une forte probabilité d'annulation peut déclencher une action préventive, par exemple :

envoyer un rappel au client ;
demander une confirmation ;
vérifier les conditions de la réservation ;
effectuer un suivi particulier de la réservation.

Le modèle doit donc être utilisé comme outil d'aide à la décision et non comme système de décision automatique.
#### **Q8. Votre modèle présente-t-il des performances comparables selon les régions ou les types de destination ?**
Les performances doivent être comparées séparément pour chaque région ou type de destination à l'aide du F1-score, du rappel et de la précision.

Les performances globales de la régression logistique sont :

F1-score : 0,4681
Rappel : 0,6755
ROC-AUC : 0,6777

Une analyse par sous-groupe est nécessaire pour déterminer si ces performances restent similaires. Les résultats des petits groupes doivent être interprétés avec prudence, car quelques erreurs peuvent fortement modifier les métriques.
#### **Q9. Analyse des erreurs**

Analysez au minimum :

- cinq faux positifs ;
- cinq faux négatifs ;
- les raisons possibles de ces erreurs ;
- une piste d’amélioration des données ou du modèle.

*(Votre réponse ici.)*

---

### **6. Conclusion et Recommandations**
La régression logistique est le meilleur modèle testé, avec un F1-score de 0,4681, un rappel de 0,6755 et un ROC-AUC de 0,6777. La forêt aléatoire arrive en deuxième position avec un F1-score de 0,4009. KNN et XGBoost ont une accuracy supérieure à 0,73, mais leurs faibles rappels montrent une mauvaise détection des annulations.

Le modèle reste donc imparfait et doit être utilisé comme outil d'aide à la décision, et non comme système automatique.

Recommandation opérationnelle

Lorsqu'une réservation présente une forte probabilité d'annulation, l'hôtel devrait déclencher une action préventive, comme l'envoi d'un rappel ou une demande de confirmation, plutôt que d'annuler directement la réservation. Le modèle devra également être réévalué régulièrement sur des données récentes afin de maintenir ses performances.
**Recommandation opérationnelle finale :**

*(Votre réponse ici.)*

---

### **7. Reproductibilité**

- version de Python :
- principales bibliothèques et versions :
- graine(s) aléatoire(s) :
- commande ou procédure d’exécution :
- durée approximative d’entraînement :
- environnement utilisé : *(local, Google Colab, Kaggle, etc.)*

---

### **8. Bibliographie**

*(Listez les livres, articles, documentations et liens ayant servi dans ce travail. Mentionnez également les outils d’IA générative utilisés et décrivez brièvement leur contribution.)*

- Référence 1 :
- Référence 2 :
- Référence 3 :
