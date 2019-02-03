## Environment Records

Są dwa rodzaje Environment Records: 
- declarative environment records
- object environment records

`Declarative environment records` są używane do definiowania efektu elementów składniowych języka ECMAScript, takich jak 
FunctionDeclarations, VariableDeclarations i Catch, który bezpośrednio wiąże powiązania identyfikatorów z wartościami języka ECMAScript.

`Object environment records` są używane do definiowania efektów elementów ECMAScriptowych takich jak WithStatement, 
które wiążą powiązania identyfikatorów z właściwościami jakiegoś obiektu.

Dla celów specyfikajci wartości environment recordów, są wartościami typu specyfikacji i można 
je uważać za istniejące w prostej hierarchii obiektowej, gdzie environment record jest abstrakcyjną klasą
z trzema konkretnymi subclasami:
- declarative env record
- object env record
- global env record

Function Environment Record and Module Environment Record są subclasami Declarative Env Recordu.

Klasa abstrakcyjna obejmuje abstrakcyjne metody specyfikacji. Te abstrakcyjne metody mają różne konkretne algorytmy dla każdej z konkretnych podklas.
Metody:
- HasBinding(N)
- CreateMutableBinding(N, D)
- CreateImmutableBinding(N, S)
- InitializeBinding(N, V)
- SetMutableBinding(N, V, S)
- GetBindingValue(N, S)
- DeleteBinding(N)
- HasThisBinding()
- HasSuperBinding()
- WithBaseObject()

