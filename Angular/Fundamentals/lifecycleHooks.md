## Lifecycle hooks

Komponenty w Angularze mają cykle życia zarządzane przez framework. Angular tworzy je, renderuje, tworzy i renderuje ich dzieci, sprawdza 
czy zmieniają się przypisane do nich dane, oraz niszczy komponenty przed usunieciem  ich z dzewa DOM.

Angular daje mozliwosc wykrycia tych momentow, oraz do wykonania czynnosci w momencie ich wystapienia.
Dyrektywy maja ten sam zestaw lifecycle hooks.

#### Lista lifecycle hooks:
1. ngOnChanges()
2. ngOnInit()
3. ngDoCheck()
4. ngAfterContentInit()
5. ngAfterContentChecked()
6. ngAfterViewInit()
7. ngAfterViewChecked()
8. ngOnDestroy()

### Overview 
Instancje dyrektyw i komponentów mają cykl życia, który Angular tworzy, aktualizuje i niszczy. 
Deweloperzy mogą wykorzystać kluczowe momenty w tym cyklu życia, implementując jeden lub więcej interfejsów przechwytujących cykl życia w bibliotece @angular/core.

Każdy interfejs ma pojedynczą metodę przechwytującą, której nazwa jest nazwą interfejsu poprzedzoną ng. 
Na przykład interfejs OnInit ma metodę przechwytującą o nazwie ngOnInit (), która wywołuje Angular krótko po utworzeniu komponentu.

```js
  export class PeekABoo implements OnInit {
  constructor(private logger: LoggerService) { }

  // implement OnInit's `ngOnInit` method
  ngOnInit() { this.logIt(`OnInit`); }

  logIt(msg: string) {
    this.logger.log(`#${nextId++} ${msg}`);
  }
}
```

Żadna dyrektywa ani żaden komponent nie będą implementować wszystkich lifecycle hooks. Angular wywołuje tylko hook method dyrektywy / komponentu, jeśli została wcześniej zdefiniowana.

### Lifecycle sequence
Po utworzeniu komponentu/dyrektywy po przez wywołanie konstruktora, Angular wywołuje lifecycle hook methods w okreslonej sekwencji, oraz w określonym czasie.

#### - ngOnChanges()
Odpowiad w momencie gdy Angular przypisze wartosci danych wejściowych, lub gdy je zmieni. Metoda ta przyjmuje obiek SimpleChanges z aktualnymi oraz poprzednimi wartościami właściwości (property values).
Jest wykonywana przed `ngOnInit()` oraz za każdym razem gdy zmienia sie jedna lub więcej z przypisanych właściwości wejściowych.

#### - ngOnInit()
Inicjalizuje dyrektywę / komponent po tym, jak Angular najpierw wyświetli właściwości związane z danymi i ustawi właściwości wejściowe dyrektywy / komponentu.
Wykonuje sie raz, zaraz po pierwszym `ngOnChanges()`.

#### - ngDoCheck()
Wykrywaj zmiany, których Angular nie może lub nie chce samodzielnie wykryć. Wywoływany podczas każdego uruchomienia detekcji zmian (change detection), zaraz po ngOnChanges () i ngOnInit ().

#### - ngAfterContentInit()
Odpowiada na zewnętrzne treści projektu Angular w widoku komponentu / widoku, w którym znajduje się dyrektywa. Wywoływana raz, po pierwszym ngDoCheck().

#### - ngAfterContentChecked() 
Odpowiada po sprawdzeniu przez Angulara treści rzutowanych na dyrektywę / komponent.
Wywoływana po ngAfterContentInit() oraz każdy kolejny ngDoCheck().

#### - ngAfterViewInit()
Odpowiada po zainicjalizowaniu przez Angulara widoków komponentu oraz widoków dzieci.
Wywoływana raz po pierwszymy ngAfterContentChecked().

#### - ngAfterViewChecked() 
Odpowiada po sprawdzeniu przez Angulara widoków oraz widoków dzieci.
Wywoływany po ngAfterViewInit() oraz każdy kolejny ngAfterContentChecked().

#### - ngOnDestroy() 
Czysci przed zniszczeniem przez Angulara komponentu/dyrektywy. Anuluje subskrypcję Observables i odłącza event handlers, aby uniknąć wycieków pamięci.
Wywoływany raz, tuż przed usunięciem kopmonentu lub dyrektywy przez Angulara.
