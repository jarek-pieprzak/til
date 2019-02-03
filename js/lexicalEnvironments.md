## Lexical Environments

Lexical Environments to typ specyfikacji używany do definiwania powiązań pomiędzy identyfikatorami a określonymi 
zmiennymi i funkcjami w oparciu o zagnieżdżoną strukturę kodu.

Składa się z Environment Record i ewentualnie do nullowej referencji do zewnętrznego lexical environmentu.

Lexical environment powiązane jest zazwyczaj z określoną strukturą składni ECMAScriptowej takiej jak FunctionDeclaration, BlockStatement lub Catch.
Nowe środowisko leksykalne jest tworzone przy kazdej ewaluacji kodu. 

Environment Record zapisuje powiązania identyfikatorów, które są tworzone w ramach Lexical Environment. Jest on określany jako EnvironmentRecord środowiska leksykalnego.

Referencja do zewnętrznego środowiska jest używana do zobrazowania logicznego zagnieżdżenia wartości LexicalEnvironmentu.
Zewnętrzne odniesienie (wewnętrznego) środowiska leksykalnego jest odniesieniem do środowiska leksykalnego, które logicznie otacza wewnętrzne środowisko leksykalne.
Zewnętrzny Lexical Environment może mieć swój własny outer LexicalEnvironment. Środowisko leksyklane może być środowiskiem zewnętrznym dla wielu inner Lexical Environments.

Global environment to Lexical Environment nie mający zewnętrznego środowiska leksykalnego, co znaczy że jego referencja do środowiska zewnętrznego jest równa null.

Environment Record środowiska globalnego może być 
