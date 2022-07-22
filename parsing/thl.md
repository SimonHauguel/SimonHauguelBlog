# Vocabulaire

- On appele `alphabet` un ensemble _fini_ de symboles. On notera nos alphabets \\(\Sigma\\).
- Un `mot` est une suite finie de symboles \\(\in \Sigma\\).
- La `longueur` du mot \\(\omega\\), est l'entier naturel \\(l_{\omega} = |\omega|\\).
- Il existe un `unique` mot \\(\epsilon\\), tel que \\(|\epsilon| = 0\\).
- L'ensemble des mots d'un alphabet \\(\Sigma\\) est \\(\Sigma^*\\)
- Un `langage` \\(L\\) sur \\(\Sigma\\) est un ensemble de mots de \\(\Sigma\\). 

> Les symboles n'ont pas besoin d'avoir une définition mathématique, on leur demande simplement de pouvoir les distinguer. Le symbole `a` est le symbole `a`, mais n'est pas le symbole `b`.

Le fait qu'un langage est simplement un ensemble, nous gardons bien évidemment les opérations communes sur les ensembles.
Soit \\(L_1, L_2\\) deux langages sur \\(\Sigma\\), on a alors :
$$L_1 + L_2 = L_1 \cup L_2$$
$$L_1L_2 = L_1\times L_2 = \\{vw~|~v \in L_1, w \in L_2\\}$$
$$L_1 \setminus L_2 = \\{w~|~w \in L_1, w \notin L_2\\}$$
$$\overline{L_1} = \\{w \in \Sigma^* | w \notin L_1\\}$$

Les mots étant des suites finies, nous pouvons ainsi les concatener. Soit \\(v = v_1v_2\cdots v_n\\) et \\(w = w_1w_2\cdots w_m\\), alors \\(v\cdot w = v_1v_2\cdots v_nw_1w_2\cdots w_m\\).
On notera

Il est important de noter que \\((\Sigma^*, \cdot)\\), est un monoïde, avec \\(\epsilon\\) comme element neutre.

Soit \\(L\\) un langage, on a
$$L^0 = \\{\epsilon\\}$$
$$L^{n+1} = LL^n$$
$$L^* = \bigcup_{i\geq0}{L^i}$$

## Exemples

Soit \\(\Sigma = \\{a, b\\}\\), alors \\(\Sigma^* = \\{\epsilon, a, b, aa, ab, ba, bb, aaa, aab, \cdots\\}\\)

Soit \\(L\_p = \\{w \in \Sigma^*~|~l\_w~est~pair\\}\\) et \\(L_i = \\{w \in \Sigma^\*~|~l\_w~est~impair\\}\\), alors
$$\\{L_p, L_i\\}~est~une~partition~de~\Sigma^\*,~donc,~L_i + L_p = \Sigma^\*$$
$$L_pL_i = L_iL_p = L_i$$
$$L_pL_p = L_p$$

Soit \\(L_c\\), le langage du langage de programmation C sur la table ascii, alors
```c
#include <stdio.h>

int main() { printf("Hello, World"); return 0; }
```
est un mot de \\(L_c\\). 

\\(\overline{L_c}\\) est le langage des programmes syntaxiquement incorrects en C.
