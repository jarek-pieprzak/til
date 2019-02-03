## Lexical Environments

`Lexical Environments` to typ specyfikacji używany do definiwania powiązań pomiędzy identyfikatorami a określonymi 
zmiennymi i funkcjami w oparciu o zagnieżdżoną strukturę kodu.

Składa się z `Environment Record` i ewentualnie do nullowej referencji do zewnętrznego lexical environmentu.

`Lexical environment` powiązane jest zazwyczaj z określoną strukturą składni ECMAScriptowej takiej jak FunctionDeclaration, BlockStatement lub Catch.
Nowe środowisko leksykalne jest tworzone przy kazdej ewaluacji kodu. 

`Environment Record` zapisuje powiązania identyfikatorów, które są tworzone w ramach Lexical Environment. Jest on określany jako EnvironmentRecord środowiska leksykalnego.

Referencja do zewnętrznego środowiska jest używana do zobrazowania logicznego zagnieżdżenia wartości LexicalEnvironmentu.
Zewnętrzne odniesienie (wewnętrznego) środowiska leksykalnego jest odniesieniem do środowiska leksykalnego, które logicznie otacza wewnętrzne środowisko leksykalne.
Zewnętrzny Lexical Environment może mieć swój własny outer LexicalEnvironment. Środowisko leksyklane może być środowiskiem zewnętrznym dla wielu inner Lexical Environments.

`Global environment` to Lexical Environment nie mający zewnętrznego środowiska leksykalnego, co znaczy że jego referencja do środowiska zewnętrznego jest równa null.

`Environment Record środowiska globalnego` może być sprepopulowany powiązaniami identyfikatorów (identifier bindings) oraz zawierać powiązany obiekt globalny (global object) którego propertisy mogą zapewniać niektóre powiązania identyfikatorów global environment.
Gdy wykonywany jest kod ECMAScript, dodatkowe propertisy mogą być dodawane do obiektu globalnego, a propertisy początkowe mogą być modyfikowane.

Module Environment to środowisko leksykalne, które zawiera powiązania dla deklaracji najwyższego poziomu modułu. Zawiera również powiązania, które są jawnie (explicity) importowane przez moduł. Zewnętrznym środowiskiem dla ModuleEnvironment jest GlobalEnvironment.

Środowiskiem funkcji jest środowisko leksykalne odpowiadające inwokacji obiektu funkcji ECMAScript. FunctionEnvironment moze ustanowić nowe powiązanie dla `this`. Środowisko funkcyjne przechowuje również niezbędny stan do obsługi wywołań metod `super`.


#### Lexical Environment i Environment Record są tylko mechanizmami specyfikacji i nie muszą odpowiadać żadnemu konkretnemu artefaktowi ECMAScriptu. Nie ma możliwości na bezpośredni dostęp lub manipulowanie tymi mechanizmami.
