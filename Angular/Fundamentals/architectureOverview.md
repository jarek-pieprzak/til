## Architecture Overview

Angular jest platformą i frameworkiem do budowania klienckich aplikacji z wykorzystaniem HTMLa i TypeScriptu.
Jest napisany w TypeScripcie. Zawiera głowne oraz opcjonalne funkcjonalniści TypeScriptu, które są importowane do aplikacji.

Podstawowymi blokami aplikacji w Angularze są NgModules, które zapewniają kontekst kompilacji dla komponentów. 
NgModules zbiera powiązany kod do functional sets; aplikajca w Angularze jest definiowana jako set of NgModules. 
Kazda aplikacja ma conajmniej jeden modół główny (root module), który zapewnia ładowanie początkowe (bootsrap) i zazwyczaj ma dużo feature modules.

- Komponenty definiują widoki, które są zestawami elementów ekranu, które Angular może wybierać i modyfikować zgodnie z logiką programu i danymi.
- Komponenty korzystają z serwisów, które zapewniają określoną funkcjonalność niezwiązaną bezpośrednio z widokami. Service providers mogą być
wstrzykiwane(injected) do komponentów jako zależności, co sprawia, że kod jest modułowy, nadaje się do ponownego użycia i jest wydajny.

Zarówno komponenty, jak i usługi są po prostu klasami, z dekoratorami, które zaznaczają ich typ i dostarczają metadanych, 
które mówią Angularowi, jak ich używać.

- Metadane klasy komponentu kojarzą ją z szablonem, który definiuje widok. Szablon łączy zwykły kod HTML z dyrektywami Angular 
i wiążącym znacznikiem, który umożliwia Angularowi zmodyfikowanie kodu HTML przed wyświetleniem go.
- Metadane(metadata) dla service class udostępniają informacje wymagane przez Angulara do udostępnienia 
ich poprzez wstrzyknięcie zależności (DI dependency injection).

### Moduły (Modules)

Moduły w Angularze (NgModules) różnią się i wzbogacają moduły zawarte w ES2015. 
Moduł NgModule deklaruje kontekst kompilacji dla zestawu komponentów, który jest dedykowany dla domeny aplikacji, 
przepływu pracy lub ściśle powiązanego zestawu możliwości. 
Moduł NgModule może powiązać swoje komponenty z powiązanym kodem, na przykład servicami, w celu utworzenia functional units.

Kazżda aplikacja Angularowa ma root module, konwencjonalnie nazwany AppModule, który zapewnia mechanizm ładowania początkowego,
który uruchamia aplikację. Aplikacja z reguły zawiera wiele modułów funkcjonalnych.

Tak jak moduły JavaScriptowe, NgModules mogą importować funkcjonalności z innych NgModules,
oraz pozwalają na exportowanie oraz używanie swoich własnych funkcjonalności przez inne NgModules.

Uporządkowanie kodu w odrębne moduły funkcjonalne pomaga w zarządzaniu rozwojem złożonych aplikacji 
i projektowaniu pod kątem ponownego wykorzystania. Ponadto ta technika pozwala wykorzystać lazy-loading 
- czyli ładowanie modułów na żądanie - w celu zminimalizowania ilości kodu, który należy załadować podczas uruchamiania.

`Więcej na temat Modułów w przeznaczonym dla nich pliku.`

### Components

Każda apka Angularowa ma conajmniej jeden komponent -> root component, który łączy hierarchię komponentów z DocumentObjectModel (DOM). 
Każdy komponent definiuje klasę, która zawiera dane aplikacji i logikę, jest powiązana z szablonem HTML, 
który definiuje widok wyświetlany w środowisku docelowym (target environment).

Dekorator `@Component` identyfikuje klasę bezpośrednio pod nią jako komponent, oraz zapewnia `szablon(template)`
i powiązane `metadata` dotyczące konkretnego komponentu.

`Więcej później..`

### Templates, directives oraz data binding.

Template - to kombinacja HTML z (Angular markups) znaczniki Angulara które mogą modyfikować elementy HTML zanim zostaną wyświetlone.
Template directives - zapewniają logikę programu, a binding markup (wiążący znacznik) łączy dane aplikacji z DOM.
Są dwa typy data bindingu:
- `event binding` - pozwala Twojej aplikacji reagować na dane wprowadzone przez użytkownika 
w środowisku docelowym poprzez aktualizację danych aplikacji
- `property binding` - pozwala interpolować wartości, które są obliczane z danych aplikacji do kodu HTML.

Zanim widok zostanie wyświetlony, Angular ewaluuje dyrektywy oraz rozwiązuje syntax bindingów w templatcie, aby zmodyfikować elementy HTML oraz DOM,
w oparciu o dane oraz logike programu. Angular wspiera `two-way data binding`, oznacza to, że zmiany w DOM, takie jak wybory użytkownika, 
są również odzwierciedlone w danych programu.

Szablony mogą korzystać z potoków (pipes) w celu poprawy wygody użytkownika poprzez transformację wartości wyświetlanych. 
Na przykład pipe, aby wyświetlić daty i wartości walut odpowiednie dla lokalizacji użytkownika. 
Angular dostarcza wstępnie zdefiniowane potoki dla typowych transformacji, możmożna również zdefiniować własne potoki.

`Później....`

### Services and dependency injecting

W przypadku danych lub logiki, która nie jest powiązana z określonym widokiem, i które chcesz używać pomiędzy komponentami, 
tworzymy `service class`. Klasa serwisu jest jest bezpośrednio poprzedzona dekoratorem @Injectable().
Dekorator udostępnia metadane, które umożliwiają wstrzykiwanie usługi do składników klienta jako zależności.

Dependency Ijection (DI) pozwala na utrzymanie klas komponentów w sposób estetyczny i wydajny.
Nie pobierają danych z serwera, nie zatwierdzają danych wprowadzonych przez użytkownika ani nie logują się bezpośrednio do konsoli; delegują takie zadania do serwisów.

`Później..`

### Routing 

Angularowy moduł `Router` oferuje usługę, która pozwala zdefiniować ścieżkę nawigacji między różnymi stanami aplikacji i wyświetlić hierarchie w aplikacji. Jest wzorowany na znanych konwencjach nawigacji w przeglądarce:
- wprowadź url w pasku, aby przejść do konkretnej strony
- kliknij link na stronie a przeglądarka przejdzie do nowej strony
- kliknij przeglądarkowe wstecz aby cofnąć się do poprzedniej strony.

Router odwzorowuje ścieżki URL paths do widoków zamiast stron. Gdy użytkownik wykonuje działanie, takie jak kliknięcie łącza, które może załadować nową stronę w przeglądarce, router przechwytuje zachowanie przeglądarki i wyświetla lub ukrywa hierarchie widoku.

Jeśli router stwierdzi, że bieżący stan aplikacji wymaga określonej funkcjonalności, a moduł, który ją definiuje, nie został załadowany, router może wczytać moduł na żądanie (lazy demand).

Router interpretuje URL zgodnie z regułami nawigacji w widoku aplikacji i stanem danych. Możesz przechodzić do nowych widoków, gdy użytkownik kliknie przycisk lub wybierze z dropboxa albo w odpowiedzi na inny bodziec z dowolnego źródła. Router rejestruje aktywność w historii przeglądarki, więc przyciski wstecz i do przodu również działają.

Aby zdefiniować reguły nawigacji, łączysz ścieżki nawigacji ze swoimi komponentami. Ścieżka używa składni podobnej do adresu URL, która integruje dane programu, w bardzo podobny sposób, jak składnia szablonu integruje widoki z danymi programu. 
Następnie można zastosować logikę programu, aby wybrać widoki do pokazania lub ukrycia, w odpowiedzi na dane wprowadzone przez użytkownika lub własne reguły dostępu.

![Drag Racing](https://angular.io/generated/images/guide/architecture/overview2.png) 
