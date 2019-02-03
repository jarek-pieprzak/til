## Function Enviroment Records

Function Enviroment Record to deklaratywny Enviroment Record, który jest używany do 
reprezentowania zakresu najwyższego poziomu funkcji oraz jeśli funkcja nie jest funkcją strzałkową,
zapewnia powiązanie `this`a.

Function Environment Records mają dodatkowo pola statnu:
- [[THisValue]]
- [[ThisBindingStatus]]
- [[FunctionObject]]
- [[HomeObject]]
- [[NewTarget]]


Function Enviroment Records wspierają wszystkie metody Declarative Environment Recorda 
oraz mają te same specyfikacje dla wszystkich tych metod z wyjątkiem HasThisBinding() 
oraz HasSuperBinding(). Dodatkowo, Function Environment Records wykorzystuje metody: 
- BindThisValue(V)
- GetThisBinding()
- GetSuperBase()

Metody :
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

