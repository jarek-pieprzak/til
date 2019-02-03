## Object environment records

Każdy Object Environment Record jest powiązany z obiektem nazywanym jego obiektem wiążącym. Object Environment Recordd
łączy zestaw string identyfierów, które bezpośrednio odpowiadają do nazw propertisów
ich obiektu wiążącego. 

Property keys które nie są ciągami znaków, nie są zawarte w zbiorze bound identifiers/
Zarówno własne, jak i odziedziczone właściwości są zawarte w zbiorze niezależnie od atrybutu [[Enumerable]].

Ponieważ propertisy mogą być dynamicznie dodawane i usuwane z obiektu, zestaw identyfikatorów zboudowanych 
przez `object env record`, może się potencjalnie zmieniać jako efekt uboczny jakiejkolwiek operacji,
która dodaje lub usuwa propertisy.

Wszelkie powiązanie które zostały stworzone jako wynik efektu ubocznego są uważane za wiązania zmienne (mutable binding) 
nawet jeśli strybut Writtable konkretnego property ma wartość `false`. 

**Wiązania zmienne (Immutable bindings) nie istnieją dla** `Object env records`.
