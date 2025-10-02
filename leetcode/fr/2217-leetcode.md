---
titre: LeetCode 2217. Trouvez le palindrome Avec longueur fixe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**K‐th Palindrome – une solution basée sur les mathématiques* *

Pour une longueur fixe `L` nous ne **pas** devons énumérer tous les nombres `L`.
Un palindrome est complètement déterminé par sa moitié gauche* – la moitié droite est juste
l'inverse.
Donc nous devons seulement considérer les chiffres

«» "
10^(ceil(L/2)-1) , 10^(ceil(L/2)-1)+1 , ..., 10^(ceil(L/2))-1
«» "

«ceil(L/2)» est le nombre de chiffres de la moitié gauche.

-----------------------------------------------------------------------------------

- Oui. 1. Combien de palindromes de longueur L existent?

«» "
nombre(L) = 9 * 10^(ceil(L/2)-1)
«» "

`10^(ceil(L/2)-1)` est la plus petite moitié gauche (`1 0 ... 0`), le chiffre le plus élevé
ne peut être "0". Le facteur `9` provient des éventuels chiffres d'entrée `1...9`.

-----------------------------------------------------------------------------------

- Oui. 2. Construire le palindrome k

Pour un «k» donné (de 1‐base):

«» "
moitié = (k-1) + 10^(ceil(L/2)-1) # moitié gauche en entier
gauche = str(demi)
droite = gauche[:len(gauche)-L%2] # laisser tomber le chiffre du milieu si L est impair
pal = gauche + droite[::-1] # concaténate & inverse
«» "

Toute l'expression est retournée en entier 64 bits ("long" en Java,
`int`/`long` en Python).

-----------------------------------------------------------------------------------

- Oui. 3. Code (Java)

"Java
solution de classe {
privé long getPalindrome(long k, int miLen, int L) {
longue gaucheNum = (k - 1) + (long)Math.pow(10, miLen - 1); // partie gauche
Chaîne gauche = Long.toString(gaucheNum);
Chaîne droite = gauche.substring(0, gauche.longueur() - (L % 2)); // chute au milieu
retour Long.parseLong(gauche + nouveau StringBuilder(droite).reverse());
}

public longues[] kthPalindrome(int[] requêtes, int L) {
int n = requêtes. longueur;
long[] ans = nouveau long[n];

(L + 1) / 2; // ceil(L/2)
longueur maxCnt = 9L * (long)Math.pow(10, miLen - 1); // 9 * 10^(miLen-1)

pour (int i = 0; i < n; ++i) {
longue k = requêtes[i];
si (k > maxCnt) {
as[i] = -1;
} autre {
ans[i] = getPalindrome(k, halfLen, L);
}
}
le retour des an;
}
}
«» "

-----------------------------------------------------------------------------------

- Oui. 4. Code (Python)

'`python
Solution de classe:
def kthPalindrome(self, requêtes: List[int], intLength: int) -> Liste[int]:
moitié = (longueur intérieure + 1) // 2
base = 10 ** (demi - 1) # plus petite moitié gauche
max_cnt = 9 * 10 ** (demi - 1)

ans = []
pour k dans les requêtes :
si k > max_cnt:
Annexe(-1)
Sinon:
gauche = str(base + k - 1)
droite = gauche[::-1]
s'il s'agit d'intLength % 2 == 1:
droite = droite[1:] # laisser tomber le chiffre médian
ans.append(int(gauche + droite))
retour et
«» "

-----------------------------------------------------------------------------------

- Oui. 5. Pourquoi cela fonctionne

* Le nombre de palindromes de longueur `L` est au plus `9 * 10^(ceil(L/2)-1)`, ce qui correspond
confortablement dans un entier 64 bits pour les contraintes du problème.
* Le `k`-th moitié gauche est simplement le `k`-th nombre dans la gamme
«[10^(ceil(L/2)-1) , 10^(ceil(L/2))-1]».
* En miroir de cette moitié nous obtenons le palindrome immédiatement – pas de dénombrement,
Pas de récursion, pas d'utilisation de mémoire énorme.

-----------------------------------------------------------------------------------

**Résultat**

L'algorithme s'exécute dans l'espace auxiliaire « O(="queries=") » et « O(1) »,
résoudre le problème efficacement même pour les limites maximales.