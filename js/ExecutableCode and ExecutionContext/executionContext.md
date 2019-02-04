## Execution context

To narzędzie specyfikacji, które jest używane do śledzenie przebiegu wywoływania (runtime evaluation) kodu przez implementację ECMASriptu.
W jednym czasie może istnieć jedynie jeden execution context przypadający na jednego agenta, który wykonuje kod. (running execution cntext)
Wszystkie odwołania do running execution context w tej specyfikacji odnoszą sie do działającego kontekstu wywołania otaczającego go agenta.

Execution context stack (stos kontekstu wywołania) jest używany do śledzenia kontekstu wywołania. 
Running execution context jest zawsze na szczycie stosu. 

Nowy context wywołania jest tworzony, gdy (control?) kontrola jest przenoszona z kodu wykonywanego powiązanego z aktualnym 
running execution contextem do kodu wykonywalnego który nie jest powiązany z tym kontekstem wywołania. 
Nowo powstały execution context jest jest pushowany na stack i staje sie aktualnym running execution contextem.

Kontekst wykonania zawiera informacje o stanie implementacji niezbędne do śledzenia postępów wykonywania skojarzonego kodu.
Komponenty stanu dla wszystkich kontekstów wykonania: 
- code evaluation state - Dowolny stan potrzebny do perform, suspend, and resume evaluation of the code powiązanego z tym kontekstem wykonania.
- function - jeśli ten kontekst wywołania evaluuje kod function obiektu, wtedy wartość tego komponentu jest tym function objectem. 
Jeśli kontekst ocenia (evaluating) kod skryptu lub modułu, wartość jest pusta (null).
- Realm - Realm Record, z którego powiązany kod uzyskuje dostęp do zasobów ECMAScript.
- ScripOrModule - Rekord modułu lub rekord skryptu, z którego pochodzi powiązany kod. Jeśli nie ma oryginalnego skryptu lub modułu, 
tak jak w przypadku oryginalnego execution kontekstu utworzonego w InitializeHostDefinedRealm, wartość jest nullem.

Ewaluacja kodu z running execution contextu może być wstrzymana w różnych miejscach zdefiniowanych w tej specyfikacji. 
W momencie gdy aktualny running execution context zostaje wstrzymany, inny execution context może stać aktualnym running execution contextem i oceniać jego kod.
W późniejszym czasie suspended execution context może stać się znowu running execution contextem oraz może wznowić ewaluacje kodu z miejsca w którym został wstrzymany.
Przejście bieżącego stanu kontekstu wykonawczego do innych kontekstów wykonawczych zwykle odbywa się w sposób podobny do stosu. (last-in, first-out)
Jednak niektóre z elementów ECMAScriptu wymagają przejścia innego niż LIFO.

Kontekst wykonania jest czysto-teoretycznym mechanizmem specyfikacji i nie musi odpowiadać żadnemu konkretnemu artefaktowi implementacji ECMAScriptowej.
Kod ECMAScript nie może uzyskać bezpośredniego dostępu do kontekstu wykonania ani obserwować jego działania.
