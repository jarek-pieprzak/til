# Observable
Observable są kolekcją wielu wartości Lazy Push.

|      | SINGLE   | Multiple   |
|------|----------|------------|
| Pull | Function | Iterator   |
| Push | Promise  | Observable |

### Pull vs Push
Pull oraz push to dwa różne protokoły, opisujące jak data Producer może komunikować się z data Consumerem.

##### Pull
W systemie Pulla, Consumer określa kiedy otrzyma dane z data Producera. Data Producer jest nieświadomy kiedy dane zostną dostarczone do data Consumera.
Każda Funkcja w JavaScripcie jest "Pull system". Funkcja jest producentem danych, a kod wywołujący tę funkcję pochłania go przez "pulling" pojedynczej wartości zwracanej z jej wywołania.

EcmaScript2015 wprowadził generatory funkcji oraz iteratory (function*), kolejny rodzaj do Pull Systemu. Kod który wywołuje `iterator.next()` jes data Consumerem, "pullujący" wiele wartości z iteratora (data Producera).


|      | PRODUCER                                   | CONSUMER                                   |
|------|--------------------------------------------|--------------------------------------------|
| Pull | Pasywny: tworzy dane na żądanie            | Aktywny: decyduje, kiedy dane są wymagane. |
| Push | Aktywny: produkuje dane we własnym tempie  | Pasywny: reaguje na odbierane dane         |

##### Push
W systemie Push, data Producer określa kiedy wysłać dane do Consumera. Data Consumer jest nieświadomy kiedy otrzyma dane.

Aktualnie najczęsciej wykorzystywanym typem w Push systemie jest Promise. Promise (producent) zapewnia rozstrzygniętą 
wartość zarejestrowanych wywołań zwrotnych Callbacks (Konsumentów), ale w przeciwieństwie do funkcji,
to Promise jest odpowiedzialny za dokładne określenie, kiedy ta wartość jest "pushed" do wywołań zwrotnych (callbacks).

RxJS wprowadził nowy rodzaj do Push systemu w JavaScripcie - Observable. Observable jest data Producerem dla wielu wartości, pushowanych do Observers (data consumers).
  
  - Funkcje są lazily evaluated computation, która synchronicznie zwraca pojedynczą wartość przy wywołaniu.
  - Generatory są lazily evaluated computation, zwracają od zera do (potencjalnie) nieskonczonej ilosci wartości.
  - Promisy, mogą zwracać (ale nie muszą) pojedynczą wartość.
  - Observables są lazily evaluated computation, które mogą synchronicznie lub niesynchronicznie zwracac od zera do (potencjalnie) nieskonczonej ilosci wartości, od czasu w którym zastały wywałoane
 
 ### Observable jako generalizacja funkcji
 W przeciwieństwie do popularnych twierdzeń, Observables nie są jak EventEmittery ani jak Promisy dla wielu wartości. Observables mogą zachowywać się jak Event Emmitery w niektórych przypadkach, mianowicie kiedy są rozgłaszane przy użyciu RxJS Subjects, ale zazwyczaj nie zachowują się jak Event Emittery.

 ### Anatomia Observable
 Observables są tworzone przy użyciu `new Observable` lub creation operator, są obserwowane przez Observer, są subskrybowane za pomocą Obserwatora, wykonywane w celu dostarczania next / error / complete Obserwatorowi, a ich wykonanie może zostać usunięte.

Rdzeń Observable składa się z: 
  - tworzenia Observabla
  - subskrypcji do Observabla
  - execucji Observabla
  - utylizacji/unsubscribe Observabla
  
#### Tworzenie Observables
Konstruktor Observable przyjmuje jeden argument, funkcję `subscription`.
```js
  const obs = new Observable( function subscribe(subscriber) {
                subscriber.next('helllo')
              } )
```

#### Subcribing do Observables
Observable `obs` może być zasubskrybowana w ten sposób:
```js
  obs.subscribe(x => console.log(x));
```
To nie przypadek że `obs.subscribe` oraz `subscribe` w `new Observable(function subscribe(subscriber) {...})` mają tą samą nazwę. W bibliotece, są różne, ale dla celów praktycznych można uważać te koncepty jako takie same.

#### Executing Observables
Kod wewnątrz `new Observable(function subscribe(subscriber) {...})` reprezentuje "Observable execution", lazy computation, która ma miejsce tylko dla każdego Observera, który subskrybuje.
Egzekucja produkuje wiele wartości w czasie, zarówno synchronicznie jak i niesynchronicznie.

Są trzy typy wartości które egzekucja Observable może dostarczyć:
  - notification 'Next' - wysyła wartości - Number, String, Object itd.
  - notification 'Error' - wysyła JS Error lub wyjątek.
  - notification 'Complete' - nie wysyła wartości.
  


 
 
 
