## Object Internal Methods and Internal Slots

Reczywista semantyka obiektów w ECMAScripcie, jest definiowana za pomocą algorytmów nazywanych metodami wewnętrznymi (internal methods).
Każdy object w silniku ECMAScript jest powiązany z zestawem metod wewnętrznych, które definiują runtime beaviour. 
Internal methods nie są częściami języka ECMAScript. Są zdefiniowane wyłącznie w celu wyjaśnienia.
Jednak, każdy obiekt w ramach implementacji ECMAScript musi zachowywać się zgodnie z określonymi wewnętrznymi metodami z nim powiązanymi.
Dokładny sposób, w jaki jest to realizowane, zależy od implementacji.

Nazwy metod wewnętrznych są polimorficzne. Oznacza to, że różne wartości obiektów mogą wykonywać różne algorytmy, 
gdy nazwa wspólnej metody wewnętrznej, jest na nich wywoływana. Ten faktyczny obiekt, do którego odwołuje się metoda wewnętrzna, 
jest "celem" wywołania. Jeśli w czasie wykonywania implementacja algorytmu będzie próbować użyć wewnętrznej metody obiektu, 
którego obiekt nie obsługuje, zostanie zgłoszony wyjątek TypeError.

`Internal slots` Wewnętrzne gniazda odpowiadają stanowi wewnętrznemu związanemu z obiektami 
i używanemu przez różne algorytmy specyfikacji ECMAScript. Internal slots nie są właściwościami obiektu i nie są dziedziczone.
W zależnośći od konkretnej specyfikacji intrnal slotu, stan taki może składać się z wartości dowolnego typu języka ECMAScript
lub określonych wartości typu specyfikacji ECMAScript. O ile nie określono inaczej, wewnętrzne sloty są przydzielane 
jako część procesu tworzenia obiektu i nie mogą być dynamicznie dodawane do obiektu. O ile nie określono inaczej, początkowa 
wartość wewnętrznego gniazda jest wartością niezdefiniowaną (undefined).
Różne algorytmy w tej specyfikacji tworzą obiekty, które mają wewnętrzne gniazda.
Jednak język ECMAScript nie zapewnia bezpośredniego powiązania wewnętrznych slotów z obiektem.

Metody wewnętrzne i wewnętrzne gniazda są identyfikowane w ramach tej specyfikacji przy użyciu nazw ujętych w nawiasy kwadratowe [[ ]].

essential internal methods używane w tej specyfikacji, mają zastosowanie do wszystkich obiektów tworzonych lub manipulowanych przez kod ECMAScript.
Każdy obiekt musi mieć algorytmy dla wszystkich istotnych wewnętrznych metod. Jednak wszystkie obiekty nie muszą używać tych samych 
algorytmów dla tych metod.

| Internal Method | Signature	| Description |
|---------------- | --------- | ----------- |
| [[GetPrototypeOf]] | ( ) → Object / Null	| Określ obiekt, który zapewnia odziedziczone właściwości dla tego obiektu. Wartość pusta wskazuje, że nie ma żadnych dziedziczonych właściwości. |
| [[SetPrototypeOf]] | (Object / Null) → Boolean | Powiąż ten obiekt z innym obiektem, który zapewnia odziedziczone właściwości. Podanie wartości NULL oznacza, że ​​nie ma żadnych dziedziczonych właściwości. Zwraca wartość true, co oznacza, że ​​operacja została zakończona pomyślnie lub wartość false wskazuje, że operacja zakończyła się niepowodzeniem. |
| [[IsExtensible]] | ( ) → Boolean | Określ, czy dozwolone jest dodawanie dodatkowych właściwości do tego obiektu. |
| [[PreventExtensions]]	| ( ) → Boolean	| Określ, czy nowe właściwości mogą zostać dodane do tego obiektu. Zwraca wartość true, jeśli operacja zakończyła się pomyślnie, lub false, jeśli operacja zakończyła się niepowodzeniem. |
| [[GetOwnProperty]] | (propertyKey) → Undefined / Property Descriptor | Zwróć deskryptor właściwości dla własnej właściwości tego obiektu, którego kluczem jest propertyKey, lub niezdefiniowany, jeśli taka właściwość nie istnieje. |
| [[DefineOwnProperty]]	| (propertyKey, PropertyDescriptor) → Boolean	| Utwórz lub zmień własną właściwość, której kluczem jest propertyKey, aby stan był opisany przez właściwość PropertyDescriptor. Zwraca wartość true, jeśli właściwość została pomyślnie utworzona / zaktualizowana lub zawiera wartość false, jeśli nie można utworzyć lub zaktualizować właściwości. |
| [[HasProperty]]	| (propertyKey) → Boolean | Zwraca wartość typu Boolean wskazującą, czy ten obiekt ma już własną, czy odziedziczoną właściwość, której kluczem jest propertyKey. |
| [[Get]] | (propertyKey, Receiver) → any |	Zwróć wartość właściwości, której kluczem jest propertyKey z tego obiektu. |
| [[Set]]	| (propertyKey, value, Receiver) → Boolean	|  |
| [[Delete]] | (propertyKey) → Boolean |  |
| [[OwnPropertyKeys]] |	( ) → List of propertyKey |  |
