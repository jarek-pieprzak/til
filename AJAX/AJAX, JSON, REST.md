# AJAX

## Ajax czyli Asynchronous JavaScript and XML to technologia, która umożliwia nam ściąganie i wysyłanie części danych bez porzeby przeładowania całej strony.

Zanim przejdziemy do pracy z Ajaxem, musimy przejść przez trochę teorii, która będzie nam się non stop przewijać przy pracy z ajaxem.

___
# Protokół HTTP
Działanie internetu w większości opiera się o protokół HTTP.
Ale jak on właściwie działa?
Przeglądarka wysyła do serwera żądanie wraz ze swoimi nagłówkami. Wśród tych nagłówków są informacje takie jak rodzaj przeglądarki, jakie typy danych ona obsługuje, rodzaj cache itp.

![alt text](http://kursjs.pl/kurs/ajax/request.png)
Serwer odbiera te żądanie, przetwarza, po czym wysyła odpowiedź (np kod strony, kod grafiki) poprzedzoną odpowiednimi nagłówkami, typem danych (np. hej - właśnie wysłałem ci grafikę) i statusem odpowiedzi (np. 200, 404, 301, 500).
Najczęściej spotykane statusy odpowiedzi to:

| Status | Co oznacza? |
|-----|-------------------------------------------------|
| 200 | Wszystko ok, połączenie zakończyło się sukcesem |
| 301 | Strona została przeniesiona na inny adres       |
| 404 | Nie ma takiej strony                            |
| 418 | Jestem czajniczkiem                             |
| 500 | Błąd serwera                                    |

Przeglądarka dostaje odpowiedź czyli nagłówki i ciało odpowiedzi.

![alt text](http://kursjs.pl/kurs/ajax/response.png)

Zaczyna czytać ciało odpowiedzi.
Dochodzi do momentu, gdzie np. za pomocą link dołączone są style do strony. Przeglądarka wysyła kolejne żądanie (wraz z nagłówkami), serwer je przetwarza i odsyła wraz ze swoimi nagłowkami.
W tych dołączonych stylach autor użył @import, które służy do dołączania innych plików css. Przeglądarka natrafia na takie @include i znowu wysyła odpowiednie żądanie do odpowiedniego serwera. Ale dalej w kodzie autor umieścił grafiki img. Przeglądarka natrafia na nie i znowu - wysyła odpowiednie rządnia, a w odpowiedzi dostaje jakiś wynik. Ten wynik zależny jest od tego co wyśle serwer. I tak w koło, aż cały dokument nie zostanie wczytany...

W powyższym opisie kilka rzeczy ma szczególne znaczenie. Pierwszą z nich jest status, czyli oznaczenie, czy dane połączenie się zakończyło sukcesem (202) lub np. niepowodzeniem, bo dany adres nie istnieje (404).

Drugim bardzo ważnym nagłówkiem jest jest Content/type, który określa typ MIME danych. Jeżeli dla przykładu serwer wyśle nam stronę html, ale jako typ text/plain, wtedy w naszej przeglądarce strona wyświetli się jako plik tekstowy. Podobnie z całą resztą zasobów - gdy serwer wyśle grafikę png jako text/plain, w naszej przeglądarce zobaczymy tekstowy śmietnik. Idąc dalej nasz serwer mógłby wysłać skrypt php jako png - wystarczy, że wyśle go wraz z nagłówkami image/png

Trzecia bardzo ważną właściwością każdego połączenia jest jego typ. Każde połączenie może być jakiegoś typu. Jeżeli wejdziesz do debugera i zakładki Network, a następnie odświeżysz tą stronę, zobaczysz, że większość połączeń będzie typu GET. Dlatego, że pobieramy dane. Takich typów jest kilka:

Ostatnią właściwością takich połączeń jest to, że są bezstanowe. Oznacza to, że jedno połączenie totalnie nie wie nic na temat drugiego połączenia. Są to jakby oddzielne byty. Jasne - w naszej aplikacji możemy trzymać jakieś zmienne itp, które zbierają dane. Ale same połączenia o sobie nic nie wiedzą. Dla nich nie ma to totalnie znaczenia.
___
# REST
Kolejnym tematem, który będzie nam się przewijał przy pracy z Ajax będzie REST czyli Representational State Transfer. Co to takiego? Pewna konwencja, wzór, a w zasadzie cytując wikipedię styl architektury

Wyobraź sobie, że w celu pobierania/wysyłania danych będziemy dynamicznie łączyć się na adres:
```javascript
const ourApiUrl = "http://kursjs.pl/bohaterowie";
```
To co powyżej to główny adres naszej "aplikacji na serwerze" (a właściwie miejsca do którego możemy się łączyć by pobierać czy wysyłać dane). 
Architektura REST to zbiór zasad, które określają, jak powinieneś zbudować odpowiednie endpointy (adresy), by inni programiści mogli się w nich odnaleźć.


| Metoda HTTP | Adres                          | Opis                                            |
|-------------|--------------------------------|-------------------------------------------------|
| GET         | http://kursjs.pl/bohaterowie   | Pobranie całej listy bohaterów                  |
| GET         | http://kursjs.pl/bohaterowie/1 | Pobranie danych bohatera o id 1                 |
| POST        | http://kursjs.pl/bohaterowie   | Wysłanie nowego bohatera                        |
| PUT         | http://kursjs.pl/bohaterowie/1 | Aktualizacja/edycja bohatera o id 1             |
| PATCH       | http://kursjs.pl/bohaterowie/1 | Aktualizacja jednej właściwości bohatera o id 1 |
| DELETE      | http://kursjs.pl/bohaterowie/1 | Usunięcie bohatera o id 1                       |

Teraz jeżeli dasz mi adres "http://kursjs.pl/bohaterowie" to ja wiedząc, że stosujesz REST mogę założyć, że gdy chcę dodać nowego użytkownika, dane powinienem wysłać za pomocą połączenia typu POST na adres ""http://kursjs.pl/bohaterowie". Ale już edytując dane jakiegoś użytkownika, pewnie wyślę dane za pomocą PATCH na adres "http://kursjs.pl/bohaterowie/jakies_id". Jasne - bez opisu bym nie podchodził, ale przynajmniej jakieś założenia mogę zrobić...

Bardzo fajny artykuł na ten temat znajduje się pod adresem https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/.

___
# XML
Asynchronous JavaScript and XML - widzisz tą końcówkę? Oznacza ona, że nasze dynamiczne połączenia będą operować głównie na XML.
Faktycznie - na początku tak było. Gdy powstawała ta technologia, głównym formatem przesyłanych danych był XML.

Problem z tym formatem jest taki, że po pierwsze jego zapis jest dość długi, więc przesyłając małe dane mamy prawie dwukrotny narzut przesyłanych informacji tylko dlatego, że składnia XML nie jest zwięzła:
```javascript
<?xml version="1.0"?>
<catalog>
   <book id="bk101">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <description>An in-depth look at creating applications
      with XML.</description>
   </book>
   <book id="bk102">
      <author>Ralls, Kim</author>
      <title>Midnight Rain</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <description>A former architect battles corporate zombies</description>
   </book>
</catalog>
```
Dodatkowo poza długim zapisem pobieranie takich danych przypomina spacerowanie po drzewie dom, co też nie jest najprzyjemniejszą rzeczą na świecie - zwłaszcza gdy działasz na sporej ilości danych. Poniżej bardzo prosty przykład, a już musimy stosować dość skomplikowane zapisy:
```javascript
function loadDoc() {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            myFunction(this);
        }
    };
    xhttp.open("GET", "books.xml", true);
    xhttp.send();
}

function myFunction(text) {
    const parser = new DOMParser();
    const xmlDoc = parser.parseFromString(text.response, "text/xml");
    const books = xmlDoc.querySelectorAll('book');
    [].forEach.call(books, function(book) {
        const title = book.querySelector('title').firstChild.nodeValue;
        const author = book.querySelector('author').firstChild.nodeValue;
        const genre = book.querySelector('genre').firstChild.nodeValue;
        const price = Number(book.querySelector('price').firstChild.nodeValue);
        const description = book.querySelector('description').firstChild.nodeValue;
        console.log(title, author, gender, price, description);
    });
}

loadDoc();
```
___
# JSON
XML działa, ale zabawa z nim nie jest najprzyjemniejsza. Dlatego właśnie powstał format JSON, który bardzo uprościł prace na przesyłanych danych.

Format JSON do złudzenia przypomina klasyczne literały w JS
```javascript
{
    "catalog" : [
        {
            "id" : "bg101",
            "author" : "Gambardella, Matthew",
            "title" : "XML Developer's Guide",
            "genre" : "Computer",
            "price" : 44.95,
            "description" : "An in-depth look at creating applications with XML."
        },
        {
            "id" : "bg102",
            "author" : "Ralls, Kim",
            "title" : "Midnight Rain",
            "genre" : "Fantasy",
            "price" : 5.95,
            "description" : "A former architect battles corporate zombies"
        }
    ]
}
```
Jest jednak kilka różnic, które go odróżnia od obiektów:

- Oczywiście żadnych metod - to tylko dane, więc mają tylko właściwości
- Nazwy kluczy piszemy w cudzysłowach
- Żadnych komentarzy
- Żadnych pojedynczych cudzysłowów - tylko podwójne
- Po ostatniej właściwości nie może być przecinka (w js może być)
- Teksty piszemy w jednej linii - nawet te wielolinijkowe. Musimy tutaj zastować jakieś znaki nowej linii, które potem odpowiednio    skonwertujemy.

Skoro JSON tak przypomina obiekty JS, to czy praca na nich też przypomina pracę na obiektach JS? Jak najbardziej:
```javascript
function myFunction(resp) {
    resp.forEach(function(book) {

        //book to nasz obiekt
        const id = book.id;
        const author = book.author;
        const title = book.title;
        const genre = book.genre;
        const price = book.price;
        const description = book.description;

        //lub za pomocą dekompozycji w ES6
        {id, author, title, genre, price, description} = book;
    }
}
```
Format json najczęściej zapisuje się w plikach z rozszerzeniem .json.
Aby sprawdzić poprawność naszego JSON, wystarczy skorzystać z narzędzia https://jsonlint.com/.

W ramach mini treningu użyj tego narzędzia i popraw poniższy JSON:
```javascript
{
    "data" : {
            "id" : 1000,
            'name' : "Marcin",
            "surname" : "Domanski",
            "user_type" : "admin",
            "privilages" : [
                "edit_post",
                "add_post",
                'delete_post'
                'delte_user',
                'edit_user'
            ]
        },
}
```
___
# Obiekt JSON
W pracy z formatem JSON w JS bardzo pomocny okaże się obiekt JSON. Nie jest to typ obiektów (więc nie używamy go z new), a pojedynczy obiekt, który udostępnia nam 2 metody: stringify i parse. Pierwsza z nich zamienia obiekt na jednolinijkowy string. Druga z nich zamienia zakodowany w string obiekt na obiekt JS:
```javascript
const ob = {
    name : "Piotr",
    subname : "Nowak"
}

const obStr = JSON.stringify(ob);
console.log(obStr); //{"name":"Piotr","subname":"Nowak"}

console.log( JSON.parse(obStr) ); //nasz wcześniejszy obiekt
```
Do czego to może się przydać? Przykładowo do wysyłania danych na serwer w formacie JSON, lub np. do wstawiania obiektów do dataset
___
# Czym się łączyć?
Gdy powstał Ajax, nasz wybór był dość ograniczony.
Mieliśmy dostęp do obiektu XMLHtppRequest. Praca z tym obiektem nie zawsze jest najwygodniejsza, dlatego bardzo szybko powstały do niego różnego rodzaju nakładki.
Jedną z najczęściej używanych jest ajax w jQuery, która to implementacja udostępnia bajecznie proste w obsłudze metody do zabawy asynchronicznymi połączeniami (xhr).
W dzisiejszych czasach w modzie jest krytykowanie jQuery (czego jestem przeciwnikiem), więc pojawiło się kilka ciekawych rozwiązań, z których warto korzystać.

Najpopularniejsze biblioteki do obsługi Ajaxa to:

- jQuery
- Axios
- Superagent
- Fetch
Ajaxem w jQuery zajmiemy się w dziale o jQuery.

W tym dziale skoncentrujemy się na natywnych rozwiązaniach udostępnianych przez czyste JS.

Do obsługi AJAX w czystym Javascrip (czasami zwanym Vanilla JS) wykorzystamy jeden z 2 sposobów: użyjemy obietków typ XMLHttpRequest(), lub api zwanego Fetch.
___
# Pobieranie danych i CORS
Żeby pobrać i wysyłać dane, musimy mieć miejsce dokąd będziemy się łączyć.

Od razu mówię - "leniwe" podejście się nie sprawdzi. Jeżeli robisz swoje strony jako pliki html na pulpicie (albo w dowolnym katalogu na dysku) i chcesz dynamicznie pobrać na stronę plik, który leży tuż obok naszego pliku html (a może gdzieś indziej na dysku), to ci się nie uda.

Przeglądarki w dzisiejszych czasach mają zabezpieczenia, by nie było możliwe pobieranie danych skądkolwiek - w tym bezpośrednio z dysku komputera. Nie ważne, że zastosujesz relatywne ścieżki, wskażesz idealnie miejsce na dysku - nie da się.

Ale czemu właściwie się nie da?

Rozchodzi się o zabezpieczenia typu CORS - Cross-Origin Resource Sharing.
Połączenia typu XHR (czyli właśnie te dynamiczne) można normalnie wykonywać tylko w obrębie własnej domeny (np. jako autor tej strony mogę się łączyć tylko na swój serwer http://kursjs.pl, który leży właśnie na tej samej domenie), lub do serwerów, które wyraźnie dadzą ci znać, że możesz od nich pobierać dane.
A jak dają znać? Wysyłając odpowiedni nagłówek:
```script
Access-Control-Allow-Origin "*"
Access-Control-Allow-Methods: "GET,POST,OPTIONS,DELETE,PUT"
```
Pierwszy nagłówek wskazuje na domeny, które mogą wykonywać dynamiczne połączenia na ten serwer. Gwiazdka oznacza dowolną domenę. Drugi nagłówek określa możliwe typy połączeń.

Poniżej przykładowa odpowiedź z jednego z publicznych api:

![alt text](http://kursjs.pl/kurs/ajax/cors-header.png)

W bardzo wielu przypadkach gdy się połączysz z jakimś serwisem by pobrać dane, w twojej konsoli pojawi się złowieszczy komunikat

![alt text](http://kursjs.pl/kurs/ajax/cors-error.png)

Oznacza on, że nie możesz się dynamicznie łączyć z serwerem. Jeżeli wiesz dobrze, że adres jest poprawny i powinieneś móc się połączyć, od razu męcz administratorów serwera, bo prawdopodobnie dali ciała i nie wysyłają ci powyższych nagłówków...

Wracamy na chwilę do naszych plików na pulpicie. Wiesz już dlaczego nie możesz pobrać pliku który leży tuż obok? Właśnie z tego samego powodu - CORS.
___
# Serwer lokalny
Żeby móc pobierać/wysyłać dane, musisz je serwować z jakiegoś serwera. W ramach testu będziemy korzystać często z https://jsonplaceholder.typicode.com/, czyli przykładowego API, które udostępnia nam testowe dane.

Takich przykładowych API (bo tak takie "zbiory endpointów" się nazywają) jest mnóstwo i bardzo łatwo je w necie znaleźć. Wystarczy wpisać w google "public api". Nasa ma swoje, jakieś ministerstwa pogody itp. Tutaj masz przykładową listę darmowych api z których będziesz mógł pobierać dane.

Jeżeli chcesz pracować na własnych danych, wtedy czeka cię instalacja własnego serwera - może być lokalny. Ja osobiście jestem używam PHP. Dlatego też na moim komputerze mam zainstalowany serwer lokalny Xampp. Proces instalacji opisałem w tym artykule. W artykule używam virtualnych hostów, ale nie potrzeba tego. Wystarczy działać na localhoscie. Wtedy do głównego katalogu ze stronami (htdocs) dorzućmy plik .htaccess z treścią
```script
Header add Access-Control-Allow-Origin "*"
Header add Access-Control-Allow-Methods: "GET,POST,OPTIONS,DELETE,PUT"
```
Dzięki temu nie będzie problemów z połączeniami. Jak włączymy taki serwer, będziemy mogli pobierać dane łącząc się na http://localhost lub na http://127.0.0.1

Ale to nie jedyne możliwe podejście. Można np. dla serwera wykorzystać NodeJS i Express do którego też są odpowiednie rozszerzenia umożliwiające wysyłanie takich nagłówków. Przykładowy artykuł jak zbudować proste API możesz znaleźć pod adresem https://scotch.io/tutorials/build-a-restful-api-using-node-and-express-4 (w ogóle dobra strona, wiec polecam czytać).

## Istnieją też inne metody radzenia sobie z CORS. Większość z nich zależy od danej technologii której używany. Są też proste - tymczasowe rozwiązania - takie jak dodatki do przeglądarek, które pozwalają wyłączyć te zabezpieczenia.
## Czy polecam to podejście? Gdy trzeba coś na szybko przetestować - da radę. Ale pamiętaj, że użytkownik w wiekszości przypadków nie będzie miał zainstalowanego takiego rozszerzenia, więc tak naprawdę problemu nie rozwiązujesz.
___
# json-server
Nie oszukujmy się. Powyższe metody są pracochłonne. Nawet jeżeli ściągniesz powyższą paczkę, to i tak zanim cokolwiek dodasz, troszkę będziesz musiał się napisać.

Kolejnym możliwym rozwiązaniem jest użycie json-server. Jest to gotowe narzędzie, które daje nam wszystkie funkcjonalności dodawania, edycji, wczytywania itp.

Instalujemy nasz serwer globalnie na cały komputer poleceniem:
```
npm install json-server -g
```
Jeżeli instalacja pokaże czerwone błędy, możliwe, że ich przyczyną są błędne uprawnienia. Albo wtedy odblokujemy w danym folderze pliki np poleceniem suno chmod 777 *.* albo po prostu odpalimy powyższą instalację poprzedzając ją słowem sudo

Możemy teraz w dowolnym katalogu odpalić go za pomocą polecenia:
```
json-server --watch nazwa-pliku.json
```
Gdzie nazwa-pliku.json to plik json, który będzie naszą pseudo bazą danych. Przykładowo gdybyśmy chcieli by w naszym API były 2 tabele z użytkownikami i filmami, wtedy taki plik mógłby mieć postać:
```javascript
{
    "users" : [
        {
            "id" : 0,
            "name" : "Marcin",
            "surname" : "Nowak"
        },
        {
            "id" : 0,
            "name" : "Piotr",
            "surname" : "Kowalski"
        }
    ],
    "movies" : [
        {
            "id" : 0,
            "name" : "Gayver",
            "genre" : "sf"
        },
        {
            "id" : 1,
            "name" : "Poznaj mojego tatę",
            "surname" : "comedy"
        }
    ]
}
```
Po odpaleniu takiego serwera w konsoli pojawią się linki, na które możemy się łączyć:
```
Resources
http://localhost:3000/users
http://localhost:3000/movies

Home
http://localhost:3000
```
Można więc stworzyć już plik index.html (w dowolnym miejscu) i pobrać dane:
```javascript
fetch('http://localhost:3000/users')
    .then(res = > res.json())
    .then(res => {
        console.log(res)
    })
```

