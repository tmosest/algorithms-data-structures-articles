-...
Título: LeetCode 2916. Subarrays Distinct Element Sum of Squares II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
#include יbits/stdc++.h
usando std namespace;

const long MOD = 1000007LL;

struct Fenwick {}
int n;
vector realizado largo tiempo bitA, bitB;
Fenwick(int sz = 0) { init(sz); }
vacio init(int sz) {}
n = sz + 2; // espacio extra para actualizaciones r+1
bitA.assign(n + 2, 0);
bitB.assign(n + 2, 0);
}
vacío interno Add(vector realizado largo largo tiempo &bit, int idx, long long val) {
Val %= MOD;
si (valo 0) val += MOD;
mientras (idx) {}
bit[idx] += val;
si (bit[idx] MOD) bit[idx] -= MOD;
idx += idx " -idx;
}
}
rango de vacío Add(int l, int r, long long val) { // 1-based indices inclusive
internalAdd(bitA, l, val);
internalAdd(bitA, r + 1, -val);
internalAdd(bitB, l, val * (l - 1) % MOD);
internalAdd(bitB, r + 1, -(val * r % MOD));
}
largo tiempo prefijoSum(int k) { // sum of f[1..k] inclusivo inclusivo
long sumA = 0, sumB = 0;
int idx = k;
mientras que (idx 0) {
sumA += bitA[idx];
si MOD) sumA -= MOD;
idx -= idx & -idx;
}
idx = k;
mientras que (idx 0) {
sumB += bitB[idx];
si (sumB >= MOD) sumB -= MOD;
idx -= idx & -idx;
}
long res = (sumA * k) % MOD;
res += sumB;
si (res >= MOD) res -= MOD;
restitución;
}
largo alcance Sum(int l, int r) { // sum of f[l.r] inclusive
si (l > r) retorno 0;
long res = prefixSum(r) - prefixSum(l - 1);
si (res iere 0) res += MOD;
restitución;
}
};

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int n;
si (!(cin  título n)) devuelve 0;
vector:
para (int i = 0; i) no; ++i) cin >

const int MAX_VAL = 100000; // as per constraints
vector implicado últimoPos(MAX_VAL + 1, -1);

Fenwick fw(n);
ans largos = 0;
largo largo dpPrev = 0; // dp para i-1

para (int i = 0; i) {}
int val = a[i];
int prevIdx = lastPos[val];
int l, r;
(prevIdx == -1) {
l = 1;
r = i + 1; // las posiciones están basadas en 1
. ♫ ... {
l = prevIdx + 2; // porque prevIdx está basado en 0
r = i + 1;
}
long sum_f = fw.rangeSum(l, r);
largo dp = (dpPrev + 2 * sum_f % MOD + (i - prevIdx) % MOD;
as += dp;
-= MOD;
fw.rangeAdd(i + 1, i + 1, 1); // añadir 1 a la posición i+ 1
lastPos[val] = i;
dpPrev = dp;
}

cout se hizo un porcentaje de MOD se hizo "\n"
retorno 0;
}