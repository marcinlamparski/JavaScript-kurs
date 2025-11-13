# Lekcja: Stringi i Wyrażenia Regularne w JavaScript

## Cel lekcji

Po ukończeniu tej lekcji będziesz w stanie:
- Pracować z ciągami znaków (stringami) w JavaScript
- Wykorzystywać wbudowane metody do manipulacji tekstem
- Rozumieć podstawy wyrażeń regularnych
- Zastosować wyrażenia regularne do walidacji i transformacji danych

---

## 1. Wprowadzenie do Stringów w JavaScript

### 1.1 Czym jest string?

**String** to ciąg znaków reprezentujący tekst. W JavaScript stringi są jednym z podstawowych typów danych (primitives).

```javascript
// Sposób deklaracji stringów
const napis1 = "Cześć Świecie";  // cudzysłów
const napis2 = 'Cześć Świecie';  // apostrof
const napis3 = `Cześć Świecie`;  // template literal

console.log(typeof napis1); // "string"
```

### 1.2 Właściwości i dostęp do znaków

Każdy string ma właściwość `length` (długość) i możliwość dostępu do poszczególnych znaków poprzez indeks:

```javascript
const tekst = "JavaScript";

console.log(tekst.length);      // 10
console.log(tekst[0]);          // "J"
console.log(tekst[4]);          // "S"
console.log(tekst.charAt(0));   // "J" (alternatywa)
```

### 1.3 Template Literals - zaawansowana deklaracja

Template literals (szablony stringów) oferują wygodę umieszczania zmiennych i wyrażeń wewnątrz stringów:

```javascript
const imie = "Ania";
const wiek = 17;

// Tradycyjne złączanie
const powitanie1 = "Cześć, " + imie + "! Masz " + wiek + " lat.";

// Template literal
const powitanie2 = `Cześć, ${imie}! Masz ${wiek} lat.`;

console.log(powitanie2); // "Cześć, Ania! Masz 17 lat."

// Wyrażenia w template literals
const suma = `2 + 3 = ${2 + 3}`;
console.log(suma); // "2 + 3 = 5"
```

---

## 2. Metody pracy ze Stringami

### 2.1 Metody zwracające części stringa

#### `substring()`, `substr()`, `slice()`

Metody te służą do wyodrębniania fragmentów stringa.

```javascript
const tekst = "JavaScript";

// substring(start, end) - od indeksu start do end (end nie wliczony)
console.log(tekst.substring(0, 4));   // "Java"

// substr(start, length) - od indeksu start, ilość znaków
console.log(tekst.substr(0, 4));      // "Java"

// slice(start, end) - podobnie do substring, ale obsługuje indeksy ujemne
console.log(tekst.slice(0, 4));       // "Java"
console.log(tekst.slice(-6));         // "Script" (ostatnie 6 znaków)
```

#### `split()`

Dzieli string na tablicę elementów na podstawie separatora:

```javascript
const csv = "imie,nazwisko,wiek";
const dane = csv.split(",");
console.log(dane); // ["imie", "nazwisko", "wiek"]

const wyrazy = "Kot pies ptak".split(" ");
console.log(wyrazy); // ["Kot", "pies", "ptak"]

// Brak argumentu - tablica z całym stringiem
const wszystko = csv.split();
console.log(wszystko); // ["imie,nazwisko,wiek"]
```

### 2.2 Metody wyszukiwania

#### `indexOf()`, `lastIndexOf()`

Zwracają indeks pierwszego/ostatniego wystąpienia szukanego tekstu:

```javascript
const email = "student@technikum.edu.pl";

console.log(email.indexOf("@"));         // 7
console.log(email.lastIndexOf("."));     // 21
console.log(email.indexOf("x"));         // -1 (nie znaleziono)
```

#### `includes()`, `startsWith()`, `endsWith()`

Metody zwracające wartość logiczną:

```javascript
const haslo = "Haslo123!@";

console.log(haslo.includes("123"));      // true
console.log(haslo.startsWith("Has"));    // true
console.log(haslo.endsWith("!@"));       // true
console.log(haslo.includes("xyz"));      // false
```

### 2.3 Transformacja tekstu

#### `toUpperCase()`, `toLowerCase()`

```javascript
const tekst = "JavaScript";

console.log(tekst.toUpperCase());    // "JAVASCRIPT"
console.log(tekst.toLowerCase());    // "javascript"
```

#### `trim()`

Usuwa białe znaki z początku i końca:

```javascript
const tekst = "  JavaScript  ";

console.log(tekst.trim());           // "JavaScript"
console.log(tekst.trimStart());      // "JavaScript  "
console.log(tekst.trimEnd());        // "  JavaScript"
```

#### `replace()`, `replaceAll()`

Zastępuje tekst:

```javascript
const tekst = "Uczę się JavaScriptu. JavaScript to fajny.";

// replace - zamienia pierwsze wystąpienie
console.log(tekst.replace("JavaScript", "JS"));
// "Uczę się JSu. JavaScript to fajny."

// replaceAll - zamienia wszystkie wystąpienia
console.log(tekst.replaceAll("JavaScript", "JS"));
// "Uczę się JSu. JS to fajny."
```

#### `repeat()`

Powtarza string n razy:

```javascript
console.log("JS".repeat(3));         // "JSJS
"
console.log("=".repeat(10));         // "=========="
```

#### `padStart()`, `padEnd()`

Uzupełnia string do wymaganej długości:

```javascript
const numer = "123";

console.log(numer.padStart(6, "0"));  // "000123"
console.log(numer.padEnd(6, "."));    // "123..."
```

### 2.4 Metoda `match()` - most do wyrażeń regularnych

```javascript
const tekst = "Mam 17 lat i mój numer to 123456789";

// Wyszukanie liczb za pomocą wyrażenia regularnego
const liczby = tekst.match(/\d+/g);
console.log(liczby); // ["17", "123456789"]
```

---

## 3. Wprowadzenie do Wyrażeń Regularnych (Regex)

### 3.1 Czym są wyrażenia regularne?

**Wyrażenie regularne** (regex, regular expression) to wzorzec opisujący zbiór stringów. Służy do wyszukiwania, walidacji i manipulacji tekstem.

```javascript
// Składnia wyrażenia regularnego
const wzorzec = /pattern/flags;

// Przykłady
const prosty = /cześć/;           // prosty tekst
const zaZnakami = /\d+/;          // jedna lub więcej cyfr
const zFlagami = /javascript/i;   // flaga i = case insensitive
```

### 3.2 Podstawowe znaki specjalne

| Znaki | Znaczenie | Przykład |
|-------|-----------|---------|
| `.` | Dowolny znak (poza nową linią) | `/a.c/` pasuje do "abc", "adc" |
| `\d` | Dowolna cyfra (0-9) | `/\d+/` pasuje do "123" |
| `\D` | Dowolny znak NIE-cyfra | `/\D+/` pasuje do "abc" |
| `\w` | Litera, cyfra, `_` | `/\w+/` pasuje do "var_1" |
| `\s` | Biały znak (spacja, tab, enter) | `/\s+/` pasuje do spacji |
| `\S` | Nie-biały znak | `/\S+/` pasuje do "tekst" |
| `[ ]` | Zestaw znaków | `/[aeiou]/` pasuje do samogłosek |
| `[^ ]` | Zanegowany zestaw | `/[^0-9]/` pasuje do NIE-cyfr |

### 3.3 Kwantyfikatory

Określają ilość powtórzeń:

| Kwantyfikator | Znaczenie | Przykład |
|--------------|-----------|---------|
| `*` | 0 lub więcej | `/ab*c/` pasuje do "ac", "abc", "abbc" |
| `+` | 1 lub więcej | `/ab+c/` pasuje do "abc", "abbc" (nie "ac") |
| `?` | 0 lub 1 | `/ab?c/` pasuje do "ac", "abc" |
| `{n}` | Dokładnie n | `/a{3}/` pasuje do "aaa" |
| `{n,m}` | Od n do m | `/a{2,4}/` pasuje do "aa", "aaa", "aaaa" |
| `{n,}` | n lub więcej | `/a{2,}/` pasuje do "aa", "aaa", itp. |

### 3.4 Zakotwiczenie

Określają pozycję w tekście:

```javascript
const tekst = "Liczby: 123 456";

// ^ - początek stringa
console.log(/^Liczby/.test(tekst));     // true
console.log(/^123/.test(tekst));        // false

// $ - koniec stringa
console.log(/456$/.test(tekst));        // true
console.log(/123$/.test(tekst));        // false

// \b - granica wyrazu
console.log(/\b123\b/.test(tekst));     // true
```

### 3.5 Flagi

Flagi modyfikują zachowanie wyrażenia regularnego:

```javascript
const tekst = "JavaScript javascript JavaScript";

// Bez flagi - przypadek ważny
console.log(tekst.match(/javascript/));    // null

// Flaga i - case insensitive
console.log(tekst.match(/javascript/i));   // ["JavaScript"]

// Flaga g - global (wszystkie wystąpienia)
console.log(tekst.match(/javascript/g));   // ["javascript"]

// Flagi g i i razem
console.log(tekst.match(/javascript/gi));  // ["JavaScript", "javascript", "JavaScript"]

// Flaga m - multiline (^ i $ działają na linie)
const multiline = "Linia 1\nLinia 2";
console.log(/^Linia 2/m.test(multiline));  // true
```

### 3.6 Podstawowe metody pracy z Regex

#### `test()` - sprawdzenie czy wzorzec pasuje

```javascript
const email = "student@school.pl";
const wzorzecEmail = /@/;

console.log(wzorzecEmail.test(email));   // true
```

#### `match()` - wyszukanie dopasowań w stringu

```javascript
const tekst = "Kod: 123, PIN: 456";

const liczby = tekst.match(/\d+/g);
console.log(liczby);    // ["123", "456"]

// Bez flagi g - zwraca pierwszy match z dodatkowymi informacjami
const pierwsza = tekst.match(/\d+/);
console.log(pierwsza);  // ["123", index: 5, input: "Kod: 123, PIN: 456"]
```

#### `replace()` z wyrażeniami regularnymi

```javascript
const tekst = "Mam 1 kota i 2 psy";

// Zamienianie liczb na słowo "wiele"
const rezultat = tekst.replace(/\d+/g, "wiele");
console.log(rezultat);  // "Mam wiele kota i wiele psy"
```

#### `search()` - indeks pierwszego dopasowania

```javascript
const tekst = "Uczę się w technikum";

console.log(tekst.search(/w /));    // 8
console.log(tekst.search(/xyz/));   // -1 (nie znaleziono)
```

### 3.7 Przykłady praktyczne

**Walidacja numeru telefonu (polska):**

```javascript
const numer = "123456789";
const wzorzec = /^\d{9}$|^\d{3}-\d{3}-\d{3}$/;

console.log(wzorzec.test("123456789"));        // true
console.log(wzorzec.test("123-456-789"));      // true
console.log(wzorzec.test("12345"));            // false
```

**Wyodrębnianie domen z adresów email:**

```javascript
const email = "student@technikum.edu.pl";
const domena = email.match(/@(.+)$/);

console.log(domena[1]);  // "technikum.edu.pl"
```

**Czyszczenie tekstu z cyfr:**

```javascript
const tekst = "Rok 2024, wersja 3.0";
const wyczyszczony = tekst.replace(/\d+/g, "");

console.log(wyczyszczony);  // "Rok , wersja ."
```

---

## 4. Podsumowanie kluczowych pojęć

| Pojęcie | Opis |
|---------|------|
| **String** | Ciąg znaków, podstawowy typ danych |
| **Metody stringów** | Funkcje działające na stringach (indexOf, replace, split, itp.) |
| **Wyrażenie regularne** | Wzorzec do wyszukiwania i transformacji tekstu |
| **Znaki specjalne** | `\d`, `\w`, `\s`, `.`, itd. - zawężają wzorzec |
| **Kwantyfikatory** | `+`, `*`, `?`, `{n}` - określają ilość powtórzeń |
| **Flagi** | `i`, `g`, `m` - modyfikują zachowanie regex |
| **Test** | Sprawdzenie czy string pasuje do wzorca |
| **Match** | Znalezienie wszystkich dopasowań |

---

## 5. Zadania Praktyczne

### Zadanie 1: Transformacja danych osobowych

**Poziom: Łatwy**

Dana jest tablica zawierająca dane pracowników w formacie: `"IMIE NAZWISKO"` (wszystkie wielkie litery).

```javascript
const pracownicy = [
  "JAN KOWALSKI",
  "ANNA NOWAK",
  "PIOTR LEWANDOWSKI"
];
```

**Polecenie:**
Stwórz funkcję `formatujPracowników(tablica)`, która przekształci imiona i nazwiska na format PascalCase (pierwsza litera wielka, reszta mała).

**Oczekiwany wynik:**
```javascript
["Jan Kowalski", "Anna Nowak", "Piotr Lewandowski"]
```

**Wskazówka:** Użyj metod `toLowerCase()`, `charAt()`, `toUpperCase()` i `slice()`.

---

### Zadanie 2: Walidacja adresu email

**Poziom: Łatwy-Średni**

**Polecenie:**
Stwórz funkcję `czySzwaladomyEmail(email)`, która sprawdzi czy email ma prawidłowy format.

Prosty regex dla emaila: `^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`

**Testy:**
```javascript
czySzwaladomyEmail("student@technikum.edu.pl");  // true
czySzwaladomyEmail("admin@example.com");         // true
czySzwaladomyEmail("zle_email@");                // false
czySzwaladomyEmail("brak.znaku.at.com");         // false
```

**Wskazówka:** Użyj metody `.test()` wyrażenia regularnego.

---

### Zadanie 3: Ekstrakcja danych z teksture

**Poziom: Średni**

Dana jest wiadomość SMS zawierająca kod potwierdzający:

```javascript
const wiadomosc = "Twój kod potwierdzający to 458293. Ważny przez 10 minut.";
```

**Polecenie:**
Stwórz funkcję `wyodrębnijKod(tekst)`, która wyodrębni i zwróci wyłącznie kod (sekwencję 6 cyfr).

**Oczekiwany wynik:**
```javascript
wyodrębnijKod(wiadomosc); // "458293"
```

**Wskazówka:** Użyj `match()` z wyrażeniem regularnym szukającym dokładnie 6 cyfr.

---

### Zadanie 4: Zamazywanie danych wrażliwych

**Poziom: Średni**

Dana jest lista numerów kart kredytowych:

```javascript
const karty = [
  "1234 5678 9012 3456",
  "9876 5432 1098 7654"
];
```

**Polecenie:**
Stwórz funkcję `zamazNumer(numer)`, która zakaże wszystkie cyfry oprócz ostatnich 4.

**Oczekiwany wynik:**
```javascript
zamazNumer("1234 5678 9012 3456"); // "**** **** **** 3456"
```

**Wskazówka:** Użyj `replace()` z wyrażeniem regularnym zamienia cyframi na `*`.

---

### Zadanie 5: Parser adresów URL

**Poziom: Średni-Trudny**

Dana jest lista adresów URL:

```javascript
const urls = [
  "https://github.com/user/repo",
  "http://example.com/path/to/page",
  "https://api.service.pl/v1/endpoint"
];
```

**Polecenie:**
Stwórz funkcję `rozbudujURL(url)`, która zwróci obiekt zawierający:
- `protokol` (http lub https)
- `domena` (część między :// a pierwszym /)
- `sciezka` (część po domenie)

**Oczekiwany wynik:**
```javascript
rozbudujURL("https://github.com/user/repo");
// {
//   protokol: "https",
//   domena: "github.com",
//   sciezka: "/user/repo"
// }
```

**Wskazówka:** Użyj `match()` z wyrażeniem regularnym zawierającym grupy `()`.

---

### Zadanie 6: Walidacja i czyszczenie formularza

**Poziom: Trudny**

Masz funkcję reprezentującą dane z formularza:

```javascript
const dane = {
  imie: "  JAN  ",
  nazwisko: "  KOWALSKI  ",
  email: "jan.kowalski@EXAMPLE.COM",
  telefon: "123-456-789"
};
```

**Polecenie:**
Stwórz funkcję `walidujIZaczyscDane(dane)`, która:
1. Usuwa białe znaki z początku i końca każdego pola (trim)
2. Konwertuje imię i nazwisko na format z pierwszą wielką literą
3. Konwertuje email na małe litery
4. Sprawdza czy telefon ma tylko cyfry (minimum 9)
5. Zwraca obiekt z czyszczonym danymi ORAZ obiekt `bledy` zawierający ewentualne problemy

**Oczekiwany wynik:**
```javascript
walidujIZaczyscDane(dane);
// {
//   dane: {
//     imie: "Jan",
//     nazwisko: "Kowalski",
//     email: "jan.kowalski@example.com",
//     telefon: "123456789"
//   },
//   bledy: []  // Brak błędów jeśli wszystko OK
// }

// Lub w przypadku błędu:
// {
//   dane: { ... },
//   bledy: ["Telefon musi zawierać minimum 9 cyfr"]
// }
```

**Wskazówka:** Łącz metody stringów z wyrażeniami regularnymi. Pamiętaj o kopiowaniu obiektu aby nie modyfikować oryginału.

---

## 6. Klucz odpowiedzi (Rozwiązania)

### Rozwiązanie Zadania 1

```javascript
function formatujPracowników(tablica) {
  return tablica.map(pracownik => {
    const slowa = pracownik.toLowerCase().split(" ");
    return slowa
      .map(slowo => slowo.charAt(0).toUpperCase() + slowo.slice(1))
      .join(" ");
  });
}
```

### Rozwiązanie Zadania 2

```javascript
function czySzwaladomyEmail(email) {
  const wzorzec = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  return wzorzec.test(email);
}
```

### Rozwiązanie Zadania 3

```javascript
function wyodrębnijKod(tekst) {
  const dopasowanie = tekst.match(/\d{6}/);
  return dopasowanie ? dopasowanie[0] : null;
}
```

### Rozwiązanie Zadania 4

```javascript
function zamazNumer(numer) {
  return numer.replace(/\d(?=.{4})/g, "*");
}
// Wyjaśnienie: \d(?=.{4}) dopasowuje cyfrę jeśli za nią są jeszcze 4 znaki
```

### Rozwiązanie Zadania 5

```javascript
function rozbudujURL(url) {
  const wzorzec = /^(https?):\/\/([^\/]+)(\/.*)?$/;
  const dopasowanie = url.match(wzorzec);
  
  if (!dopasowanie) return null;
  
  return {
    protokol: dopasowanie[1],
    domena: dopasowanie[2],
    sciezka: dopasowanie[3] || ""
  };
}
```

### Rozwiązanie Zadania 6

```javascript
function walidujIZaczyscDane(dane) {
  const bledy = [];
  
  // Kopiowanie danych aby nie modyfikować oryginału
  const czyszczaneDane = { ...dane };
  
  // Czyszczenie imienia i nazwiska
  czyszczaneDane.imie = czyszczaneDane.imie
    .trim()
    .toLowerCase()
    .charAt(0)
    .toUpperCase() + czyszczaneDane.imie.trim().toLowerCase().slice(1);
  
  czyszczaneDane.nazwisko = czyszczaneDane.nazwisko
    .trim()
    .toLowerCase()
    .charAt(0)
    .toUpperCase() + czyszczaneDane.nazwisko.trim().toLowerCase().slice(1);
  
  // Czyszczenie emaila
  czyszczaneDane.email = czyszczaneDane.email.trim().toLowerCase();
  
  // Walidacja i czyszczenie telefonu
  const samoLiczby = czyszczaneDane.telefon.replace(/\D/g, "");
  if (samoLiczby.length < 9) {
    bledy.push("Telefon musi zawierać minimum 9 cyfr");
  } else {
    czyszczaneDane.telefon = samoLiczby;
  }
  
  // Walidacja emaila
  if (!/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test(czyszczaneDane.email)) {
    bledy.push("Błędny format emaila");
  }
  
  return {
    dane: czyszczaneDane,
    bledy: bledy
  };
}
```

---

## 7. Materiały do samodzielnej nauki

- **MDN Web Docs - String**: Pełna dokumentacja metod stringów
- **MDN Web Docs - Regular Expressions**: Szczegółowy przewodnik po regex
- **Regex101.com**: Interaktywny tester wyrażeń regularnych
- **RegexPal.com**: Kolejny narzędzie do testowania regex online

---

**Opracował**: Szkolenie JavaScript - Technikum Informatyczne

**Data**: 2025

**Wersja**: 1.0
