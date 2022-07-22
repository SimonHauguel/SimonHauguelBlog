# Introduction

Cette introduction aux algorithmes de [parsing](#parser) traite le problème du point de vue d'un informaticien pour des informaticiens. [Parser](#parser) est un terme large, qui s'applique dans d'autres domaines que l'informatique, mais nous ni nous n'attarderons pas.

Les parsers sont des outils très pratiques pour écrire des compilateurs ou interpréteurs, ils se placent dans la phase dit du `front-end`. Les Informaticiens les plus habiles pourront aisément écrire un parser, mais il ne sera probable que cela soit inefficace, soit qui ne pas scale ou pas suffisamment en pratique. C'est pourquoi nous voulons donner des algorithmes robustes, non-naïf, et efficients.

Pour pleinement comprendre, et appréhender ce sujet d'étude, il est préférable de faire un détour vers la [théorie des langages](TODO). Nous passerons en revue les [langages rationnels](TODO) et [automates déterministes](TODO) puis les [langages algébriques](TODO).

Finalement, nous nous attaquerons tardivement mais bien préparés, au sujet principal de ce tutoriel que sont les parsers. Nous finirons par un exemple concret, implémenté en [Lean](https://leanprover.github.io/).
## Parser
Actuellement nous manquons d'outils pour définir ce qu'est un parser. Mais nous pouvons a minima donner une intuition de son utilité. 
> Un parser, ou analyseur syntaxique en français, est un algorithme qui consomme un flux de [symboles](TODO), et génère  *dynamiquement* *la* structure de données associée.

Dans cette définition, il est important de noter 2 choses : 

- le parser génère __*la*__ structure de données associée.
- La structure est générée __*dynamiquement*__.

Pour le premier point, il est notable de comprendre que notre parseur ne doit pas générer plusieurs structures de données, et ne doit pas choisir entre plusieurs structures. Mais doit nous fournir un unique résultat. Par exemple si nous voulons parser l'expression arithmétique suivante `"a + b + c"`, que devons-nous obtenir ? `a + (b + c)` ou `(a + b) + c` ? Évidemment, cela n'a pas d'importance au point de vue sémantique, mais faisons abstraction de l'associativité de `+`, ce n'est pas le sujet. Nous n'avons pas envie d'obtenir et de manipuler ces deux formes. Ce que nous souhaitons en revanche c'est obtenir une unique structure, celle qu'il nous semble la plus adaptée.

Pour le second point, la structure est générée non pas après avoir consumé le flux, mais pendant qu'il le consume. Ne nous attardons pas sur ce point dans l'immédiat, mais cette précision nous sera utile quand nous allons parler des parsers LL est LR. Il est donc important de le garder en tete pour le reste de cette introduction.

## Lexer

Il est important de parler des [lexers](#lexer). Un [lexer](#lexer) consume un flux de symboles, mais retourne un flux de lexemes. Un lexeme n'est rien de plus qu'un symbole doté d'un tag, cela enrichit notre flux d'entrée, et peut simplifier le travail du parser.
Voici un exemple :
```c
while (true) { a; }
```
La résultante de l'étape de lexing depuis ce flux d'entrée (en langage C) sera par exemple :
```c
[RESERVEDWHILE, OPENPARENS, IDENTIFIER<"true">, OPENBRACKET, IDENTIFIER<"a">, SEMICOLON, CLOSEBRACKET]
```
À noter que dans notre exemple, nous perdons des informations : l'emplacement des lexemes dans le flux original, les caractères "inutiles" (espace, tabulation, retour à la ligne).

Nous faisons généralement cette passe avant le [parsing](#parser).
Même s'il est possible de penser qu'il est toujours une bonne chose de faire cette analyse, on dit difficilement non à une couche supplémentaire d'abstraction. Mais en réalité, il nous faut noter que la passe du lexer n'est en aucun cas une necessité, et peut, dans certains cas, complexifier inutilement le code.


