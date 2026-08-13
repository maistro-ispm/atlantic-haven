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
- rôle : Lead Developer

#### Membre 2

- nom : AINA RAKOTONDRAMBOLA 
- prénom(s) : Lova Nasaina
- classe : IGGLIA 4
- numéro : 06
- rôle : Data Scientist

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

*(Indiquez le meilleur F1-score obtenu sur votre jeu de validation, les principales métriques complémentaires et une découverte importante issue de votre analyse.)*

#### Mots-clés

Classification binaire, validation temporelle, F1-score, feature engineering, pipeline sklearn, concept drift, régression logistique.

---

### **3. Contenu du Repository**

Voici la liste des fichiers et liens importants permettant d’évaluer votre travail :

- **notebook.ipynb** : code complet de l’EDA, du prétraitement, de la modélisation et de l’évaluation ;
- **submission.csv** : prédictions sur `reservations_test.csv` ;
- **README.md** : présent rapport complété ;
- **requirements.txt** : dépendances nécessaires à la reproduction du projet *(si nécessaire)* ;
- *(ajoutez ici les autres fichiers utiles sans inclure les fichiers temporaires).* 

**🔗 Liens utiles :**

- [**LIEN VERS LA VIDÉO DE PRÉSENTATION** — Google Drive ou YouTube](https://www.youtube.com/)
- [Lien vers le dépôt GitHub](https://github.com/)
- [Lien vers une autre ressource — facultatif](https://www.google.com/)

---

### **4. Résultats de Modélisation**

Présentez les résultats obtenus sur **le même jeu de validation** afin que la comparaison soit valide.

| Modèle | Paramètres principaux | F1-score | Précision | Rappel | ROC-AUC |
|---|---|---:|---:|---:|---:|
| Régression logistique — baseline |  |  |  |  |  |
| Modèle 2 |  |  |  |  |  |
| Modèle 3 |  |  |  |  |  |
| Modèle final |  |  |  |  |  |

**Seuil de décision retenu :** *(votre réponse ici)*

**Justification du choix du modèle final :**

*(Votre réponse ici. Ne vous limitez pas au score : considérez la stabilité, l’interprétabilité, les erreurs et le coût métier.)*

---

### **5. Réponses aux Questions d’Analyse**

*Répondez précisément aux questions ci-dessous. Utilisez des chiffres, tableaux ou références à vos graphiques pour justifier vos réponses.*

#### **Q1. Pourquoi utilise-t-on principalement le F1-score plutôt que l’accuracy pour cette tâche ?**

*(Votre réponse ici.)*

#### **Q2. Dans ce contexte, qu’est-ce qui est le plus grave : un faux positif ou un faux négatif ?**

*(Définissez d’abord les deux erreurs dans le contexte hôtelier, puis justifiez votre réponse. Une réponse nuancée est possible.)*

#### **Q3. Quelles variables créées par feature engineering ont le plus amélioré votre modèle par rapport à la régression logistique de référence ?**

*(Listez les variables, expliquez leur construction et quantifiez le gain observé.)*

#### **Q4. Pourquoi un découpage aléatoire simple peut-il produire une évaluation trompeuse sur ce dataset ?**

*(Expliquez votre stratégie de validation temporelle et indiquez les dates ou proportions utilisées.)*

#### **Q5. Quels profils ou scénarios de réservation sont les plus fréquemment associés aux annulations dans vos analyses ?**

- *(profil ou scénario 1)*
- *(profil ou scénario 2)*
- *(profil ou scénario 3)*
- *(...)*

*Attention : décrivez des circonstances observables et des interactions entre variables. Ne présentez pas une région ou une population comme étant intrinsèquement à risque.*

#### **Q6. Comment votre pipeline traite-t-il les valeurs manquantes et les catégories jamais observées pendant l’entraînement ?**

*(Votre réponse ici. Précisez comment vous avez évité la fuite de données.)*

#### **Q7. Selon vous, quelle action l’hôtel devrait-il entreprendre lorsqu’une réservation en cours présente une forte probabilité d’annulation ?**

*(Votre réponse ici. Proposez une intervention proportionnée qui n’annule pas automatiquement la réservation du client.)*

#### **Q8. Votre modèle présente-t-il des performances comparables selon les régions ou les types de destination ?**

*(Présentez au moins une comparaison chiffrée et discutez les limites liées aux petits sous-groupes.)*

#### **Q9. Analyse des erreurs**

Analysez au minimum :

- cinq faux positifs ;
- cinq faux négatifs ;
- les raisons possibles de ces erreurs ;
- une piste d’amélioration des données ou du modèle.

*(Votre réponse ici.)*

---

### **6. Conclusion et Recommandations**

*(Résumez en un court paragraphe les performances, les limites et les conditions raisonnables d’utilisation du modèle.)*

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
