## Global Environment Records

Global environment record służy do reprezentowania najbardziej zewnętrznego zakresu,
który jest wspólny dla wszystkich elementów skryptu ECMAScript, które są przetwarzane we wspólnym realmie.
Global Env Record zapewnia powiązania dla wbudowanych globali, propertisów globalnego objectu, oraz dla wszystkich wysokopoziomowcyh deklaracji 
które występują w skrypcie.

Global Environment Record, logicznie jest pojedynczą wartością, 
ale jest określona jako połączenie zawierające object environment record oraz declarative env record.
Object Env Recor ma jako obiekt podstawowy obiekt globalny powiązanego Realm Recordu. Ten obiekt globalny jest wartością zwracaną przez metodę GetThisBinding globalnego environment recorda.

Właściwości mogą być tworzone bezpośrednio na obiekcie globalnym. Stąd, object environment record globalnego env recordu może zawierać
oba wiązania utworzone jawnie prze FunctionDeclarations,  GeneratorDeclaration, AsyncFunctionDeclaration, AsyncGeneratorDeclaration, or VariableDeclaration oraz wiązania tworzone niejawnie (implicity) jako właściwości obiektu globalnego.
Aby określić które wiązania są jawnie utowrzone za pomocą deklaracji, global environment record zawiera listę powiązanych nazw korzystając 
z metod CreateGlobalVarBinding and CreateGlobalFunctionBinding. 
