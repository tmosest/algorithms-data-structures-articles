---
titre: LeetCode 3013. Diviser un sous-réseau de distribution avec un coût minimum II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue longue résolution (vecteur const<long>& a, long long k, long d) {
n = (int)a.size();
si (k <= 1) retourner a[0]; // une seule sous-tribution nécessaire
besoin int = (int)k - 1; // nombre de subarrays à choisir
longue longue meilleure = LLONG_MAX;
long long sumSel = 0; // somme courante des éléments sélectionnés

set<pair<long long,int>> non utilisé; // éléments non encore dans la fenêtre actuelle
set<pair<long long,int>> cur; // éléments actuels de la fenêtre (maintien trié)

int r = 0; // dernier indice ajouté aux valeurs inutilisées
pour (int l = 1; l <= n-1; ++l) {
// ajouter l s'il n'a pas encore été ajouté
si (r < l) {
pendant la période (r < l) {
++r;
non utilisé.insérer({a[r], r});
}
}

int cible = (int)min(long long)l + d, (long long)n - 1);
pendant que (r < cible) {
++r;
non utilisé.insérer({a[r], r});
}

// déplacer les éléments les plus petits de non utilisés à cur jusqu'à ce que cur ait des éléments 'nécessités'
pendant que ((int)cur.size() < need && !unused.vide()) {
auto it = non utilisé.begin(); // plus petit élément
cur.insert(*it);
sumSel += it->premier;
non utilisé.erase(it);
}

// conserver les plus petits éléments 'besoin' en cur
pendant que (!cur.vide() && !non utilisé.vide() &&
cur.rbegin()->premier > non utilisé.degin()->premier) {
auto itCur = prev(cur.end());
sumSel -= itCur->premier;
non utilisé.insérer(*itCur);
cur.erase(itCur);

auto itUn = non utilisé.degin();
c. insérer(*itUn);
sumSel += itUn->premier;
non utilisé.erase(itUn);
}

si ((int)cur.size() == besoin)
best = min(meilleur, sumSel);

// supprimer l'élément à la position l avant l'itération suivante
auto itCurL = cur.find({a[l], l});
si (itCurL != cur.end()) {
cur.erase(itCurL);
sumSel -= a[l];
} autre {
non utilisé.erase({a[l], l});
}
}

le meilleur retour + a[0];
}