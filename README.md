# UQAC-Movie-Recommender-Atelier2

# Movie Recommender System avec K-Means et KNN

## 1. Présentation du projet

Ce dépôt contient une implémentation complète d’un **système de recommandation de films** basé sur une combinaison de **clustering K-Means** et de **filtrage collaboratif K-Nearest Neighbors (KNN)**. L’objectif est de prédire pour un utilisateur donné la note qu’il pourrait attribuer à un film qu’il n’a pas encore vu, puis de générer une liste de recommandations diversifiées.  

L’algorithme s’articule autour de deux grandes phases :

1. **Réduction de dimension & clustering des films**  
# Movie Recommender System avec K-Means et KNN

## 1. Présentation du projet

Ce dépôt contient une implémentation complète d’un **système de recommandation de films** basé sur une combinaison de **clustering K-Means** et de **filtrage collaboratif K-Nearest Neighbors (KNN)**. L’objectif est de prédire pour un utilisateur donné la note qu’il pourrait attribuer à un film qu’il n’a pas encore vu, puis de générer une liste de recommandations diversifiées.  

L’algorithme s’articule autour de deux grandes phases :

1. **Réduction de dimension & clustering des films**  
   - On regroupe les films en un nombre restreint de clusters (via K-Means) afin d’atténuer la forte dimensionnalité et la sparsité des données.
   - Chaque film obtient un label de cluster, et chaque utilisateur est résumé par ses notes moyennes par cluster.

2. **Filtrage collaboratif pondéré (KNN) dans l’espace des clusters**  
   - Pour chaque nouvel utilisateur (ou utilisateur existant à évaluer), on calcule la similarité (corrélation de Pearson) entre utilisateurs dans cet espace “clusters × utilisateurs”.
   - Lorsqu’on veut estimer la note qu’un utilisateur donnerait à un film, on :
     1. Identifie le cluster du film.
     2. Sélectionne les k utilisateurs les plus similaires ayant noté ce même cluster.
     3. Agrège leurs notes par une moyenne pondérée (pondération par la similarité).
     4. Éventuellement, on applique une petite pénalité pour diversifier les recommandations par cluster.

Le projet s’appuie sur la base de données MovieLens 100k (ML-100k), fournie par le GroupLens Research Lab, qui comprend :

- Les évaluations (`u.data`), format : `user_id`, `movie_id`, `rating`, `timestamp`
- Les informations utilisateurs (`u.user`), format : `user_id`, `age`, `gender`, `occupation`, `zip_code`
