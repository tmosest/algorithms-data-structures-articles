---
titre: LeetCode 2916. Subarrays Élément distinct Somme des carrés II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD = 1000000007LL;

struct Fenwick {
l'élément n;
vecteur <long> bitA, bitB;
Fenwick(int sz = 0) { init(sz); }
vide init(int sz) {
n = sz + 2; // espace supplémentaire pour les mises à jour r+1
bitA. attribuer(n + 2, 0);
bitB.assign(n + 2, 0);
}
vide interne Ajouter(vecteur <long long> &bit, int idx, long long val) {
Valeur %= MOD;
si (val < 0) valeur += MOD;
pendant que (idx <= n) {
bit[idx] += valeur;
si (bit[idx] >= MOD) bit[idx] -= MOD;
idx += idx & -idx;
}
}
plage de vides Ajouter(int l, int r, long long val) { // 1-based indices inclusivement
interne(bitA, l, val);
interneAdd(bitA, r + 1, -val);
interneAjouter(bitB, l, val * (l - 1) % MOD);
bitB, r + 1, -(val * r % MOD);
}
long préfixe longSum(int k) { // somme de f[1..k] inclusivement
longue sommeA = 0, sommeB = 0;
int idx = k;
pendant la période (idx > 0) {
bitA[idx];
si (sumA >= MOD) suma -= MOD;
idx -= idx & -idx;
}
idx = k;
pendant la période (idx > 0) {
sumB += bitB[idx];
si (sommeB >= MOD) sumb -= MOD;
idx -= idx & -idx;
}
longue rés longue = (somme * k) % MOD;
res += sumB;
si (res >= MOD) res -= MOD;
retour rés;
}
longue distance Somme(int l, int r) { // somme de f[l.r] inclusivement
si (l > r) retourne 0;
long long res = préfixeSum(r) - préfixeSum(l - 1);
si (res < 0) res += MOD;
retour rés;
}
};

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

l'élément n;
si (!(cin >> n)) retourner 0;
vecteur <int> a(n);
pour (int i = 0; i < n; ++i) cin >> a[i];

const int MAX_VAL = 100000; // selon les contraintes
vecteur<int> lastPos(MAX_VAL + 1, -1);

Fenwick fw(n);
long an = 0;
long dpPrev = 0; // dp pour i-1

pour (int i = 0; i < n; ++i) {
valeur int = a[i];
int prevIdx = lastPos[val];
l, r;
Si (prevIdx) -1) {
l = 1;
r = i + 1; // les positions sont basées sur 1
} autre {
l = prevIdx + 2; // parce que prevIdx est basé sur 0
r = i + 1;
}
long sum_f = fw.rangeSum(l, r);
long dp = (dpPrev + 2 * sum_f % MOD + (i - prevIdx)) % MOD;
ans += dp;
si (ans >= MOD) ans -= MOD;
fw.rangeAjouter(i + 1, i + 1, 1); // ajouter 1 à la position i+ 1
lastPos[val] = i;
dpPrev = dp;
}

cout << ans % MOD << "\n";
retour 0;
}