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
 
 
