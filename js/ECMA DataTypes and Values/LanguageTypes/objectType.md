## Object Type

Obiekt, logicznie jest kolekcją propertisów. Każdy propertis jest zarówno data property jak i accessor property.
- data property - wiąże wartośćklucza z wartością języka ECMAScript oraz zestawem atrybutów bool
- accessor property - wiąże wartość klucza z jedną lub dwoma funkcjami dodatkowymi (accessor functions), oraz zestawm atrybutów bool.
Funkcje dodatkowe są używane do przechowywania lub odzyskiwania wartości ECMAScriptowych które są powiązane z property.

Properties są identyfikowane za pomocą wartości klucza(key value). Key value jest zarówno wartością String jak i wartością Symbola.
Wszystkie wartości String oraz Symbol, włączając w to pusty ciąg znaków, są prawidłowe jak property keys. Property name jest to klucz który jest ciągiem znaków (String value).
Indexy są liczone od +0 do (2^32 - 1).

Property keys są wykorzystywane do uzysknia dostępu do properties oraz ich wartości. Są dwa sposoby: get oraz set.
Odpowiednio do odczytywania wartości (get retrieval) oraz przypisywania wartości (set assigment).

Właściwości dostępne przez `get` oraz `set` zawierają własne wartości(properties) które są bezpośrednią częścią obiektu, 
oraz properties odziedziczone z innego powiązanego obiektu poprzez relacje dziedziczenia własności.
Dziedziczone właściwości(propertisy) mogą być własnymi lub odziedziczonymi właściwościami powiązanego obiektu.
Key values muszą być unikalne. NIe mogą się powtarzać.


Wszystkie obiekty są logicznymi kolekcjami właściwości, ale istnieje wiele form obiektów, które różnią się semantyką dostępu i manipulowania ich właściwościami.
Obiekty zwykłe są najczęstszą formą obiektów i mają domyślną semantykę obiektów.
