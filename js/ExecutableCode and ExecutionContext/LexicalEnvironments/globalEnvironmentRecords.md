## Global Environment Records

Global environment record służy do reprezentowania najbardziej zewnętrznego zakresu,
który jest wspólny dla wszystkich elementów skryptu ECMAScript, które są przetwarzane we wspólnym realmie.
Global Env Record zapewnia powiązania dla wbudowanych globali, propertisów globalnego objectu, oraz dla wszystkich wysokopoziomowcyh deklaracji 
które występują w skrypcie.

Global Environment Record, logicznie jest pojedynczą wartością, 
ale jest określona jako połączenie zawierające object environment record oraz declarative env record.
