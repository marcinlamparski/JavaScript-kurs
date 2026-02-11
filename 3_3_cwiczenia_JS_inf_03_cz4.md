# 📝 SZABLON HTML - CZĘŚĆ 4 - DYNAMICZNE TWORZENIE ELEMENTÓW

Uczniowie pracują na tym pliku. Każde ćwiczenie ma swój HTML do modyfikacji poprzez JavaScript.

---

## 📚 SUPLEMENT - TWORZENIE I USUWANIE ELEMENTÓW DOM

Zanim zaczniesz ćwiczenia, przeczytaj to!

### Tworzenie nowych elementów:

| Metoda | Składnia | Co robi? |
|--------|----------|----------|
| **createElement()** | `document.createElement('tag')` | Tworzy nowy element HTML (jeszcze niewidoczny!) |
| **appendChild()** | `rodzic.appendChild(dziecko)` | Dodaje element na KONIEC rodzica |
| **append()** | `rodzic.append(dziecko)` | Jak appendChild, ale może dodać też tekst |
| **prepend()** | `rodzic.prepend(dziecko)` | Dodaje element na POCZĄTEK rodzica |
| **insertBefore()** | `rodzic.insertBefore(nowy, istniejący)` | Wstawia przed wskazanym elementem |

### Usuwanie elementów:

| Metoda | Składnia | Co robi? |
|--------|----------|----------|
| **remove()** | `element.remove()` | Usuwa element ze strony |
| **removeChild()** | `rodzic.removeChild(dziecko)` | Rodzic usuwa swoje dziecko |

### Nawigacja po DOM:

| Właściwość | Co zwraca? | Przykład |
|------------|------------|----------|
| **parentElement** | Rodzic elementu | `btn.parentElement` → div zawierający btn |
| **children** | Dzieci elementu (HTMLCollection) | `ul.children` → wszystkie li |
| **firstElementChild** | Pierwsze dziecko | `ul.firstElementChild` → pierwsze li |
| **lastElementChild** | Ostatnie dziecko | `ul.lastElementChild` → ostatnie li |

---

### Schemat tworzenia elementu:

```javascript
// KROK 1: Utwórz element (jeszcze niewidoczny!)
const nowyParagraf = document.createElement('p');

// KROK 2: Dodaj treść i style
nowyParagraf.innerHTML = 'To jest nowy paragraf!';
nowyParagraf.classList.add('moja-klasa');
nowyParagraf.style.color = 'blue';

// KROK 3: Dodaj do strony (teraz staje się widoczny!)
const kontener = document.getElementById('kontener');
kontener.appendChild(nowyParagraf);
```

### Schemat usuwania elementu:

```javascript
// SPOSÓB 1: Bezpośrednie usunięcie
const element = document.getElementById('doUsuniecia');
element.remove();

// SPOSÓB 2: Usuń rodzica klikniętego przycisku
btn.addEventListener('click', function() {
    this.parentElement.remove();  // usuwa div zawierający przycisk
});
```

### Tworzenie klasy CSS + dodanie przez JS:

```css
/* KROK 1: Zdefiniuj klasę w CSS */
.podswietlony {
    background-color: yellow;
    border: 2px solid orange;
    padding: 10px;
}
```

```javascript
// KROK 2: Dodaj klasę do elementu przez JS
const element = document.getElementById('box');
element.classList.add('podswietlony');
```

---

## 🎯 SZABLON HTML DO PRACY

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>INF.03 - JavaScript Część 4 - Tworzenie elementów</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }

        header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .task {
            background: white;
            border-radius: 10px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
        }

        .task-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .task-number {
            display: inline-block;
            background: #a6c1ee;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            text-align: center;
            line-height: 40px;
            font-weight: bold;
            margin-right: 15px;
            font-size: 1.2em;
        }

        .task-title {
            color: #333;
            font-size: 1.3em;
        }

        .difficulty {
            margin-left: 20px;
            color: #a6c1ee;
            font-weight: bold;
        }

        .difficulty-star {
            color: #ffa500;
            letter-spacing: 1px;
        }

        .task-content {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 6px;
            border-left: 4px solid #a6c1ee;
        }

        .task-content p {
            margin: 10px 0;
            color: #555;
            line-height: 1.6;
        }

        /* Style dla przycisków */
        .demo-btn {
            padding: 12px 24px;
            background: #a6c1ee;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            margin: 5px;
            transition: all 0.3s ease;
        }

        .demo-btn:hover {
            background: #8faee0;
        }

        .demo-btn-small {
            padding: 6px 12px;
            background: #e57373;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
            margin-left: 10px;
        }

        .demo-btn-small:hover {
            background: #c62828;
        }

        /* Kontenery na elementy */
        .demo-container {
            min-height: 100px;
            background: #f5f5f5;
            border: 2px dashed #ccc;
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
        }

        .demo-box {
            padding: 15px;
            background: #fff;
            border: 2px solid #a6c1ee;
            border-radius: 6px;
            margin: 10px 0;
        }

        /* Style dla list */
        .demo-list {
            list-style: none;
            padding: 0;
        }

        .demo-list li {
            padding: 12px 15px;
            background: #fff;
            border: 1px solid #ddd;
            border-radius: 6px;
            margin: 8px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* Inputy */
        input[type="text"] {
            padding: 10px 14px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 14px;
            margin: 5px;
            width: 250px;
        }

        input:focus {
            border-color: #a6c1ee;
            outline: none;
        }

        .info-box {
            background: #e3f2fd;
            padding: 10px;
            border-radius: 4px;
            margin: 10px 0;
            border-left: 4px solid #2196f3;
        }

        .css-code {
            background: #263238;
            color: #aed581;
            padding: 10px 15px;
            border-radius: 6px;
            font-family: 'Courier New', monospace;
            margin: 10px 0;
            font-size: 13px;
        }

        footer {
            text-align: center;
            color: white;
            margin-top: 40px;
            opacity: 0.8;
        }

     

        /* Klasy pomocnicze (gotowe) */
        .hidden { display: none; }
        .nowy-element {
            background: #e8f5e9;
            border: 2px solid #4caf50;
            padding: 10px;
            margin: 5px 0;
            border-radius: 4px;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🚀 JavaScript - Egzamin INF.03</h1>
            <p>Część 4 - Dynamiczne tworzenie i usuwanie elementów</p>
        </header>

        <!-- ĆWICZENIE 1 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">1</div>
                <div class="task-title">Utwórz klasę CSS i dodaj przez JS</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong></p>
                <p>1. W sekcji <code>&lt;style&gt;</code> utwórz klasę <code>.zaznaczony</code> z żółtym tłem (#fffde7), pomarańczową ramką (3px solid #ffc107) i paddingiem 15px.</p>
                <p>2. Napisz kod JS, który po kliknięciu przycisku doda tę klasę do elementu "box1".</p>
                <div class="css-code">
                    .zaznaczony { background-color: ???; border: ???; padding: ???; }
                </div>
                <button class="demo-btn" id="btn1">Dodaj klasę .zaznaczony</button>
                <div id="box1" class="demo-box">Ten element dostanie nową klasę</div>
            </div>
        </div>

        <!-- ĆWICZENIE 2 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">2</div>
                <div class="task-title">Utwórz klasę w stylach CSS "ważny" i przełączaj</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong></p>
                <p>1. Utwórz klasę <code>.wazny</code> z: czerwonym tłem (#ffebee), lewą ramką (5px solid #f44336), ciemno-czerwonym tekstem (#c62828), pogrubieniem.</p>
                <p>2. Po kliknięciu przycisku PRZEŁĄCZAJ (toggle) tę klasę na elemencie "box2".</p>
                <button class="demo-btn" id="btn2">Przełącz .wazny</button>
                <div id="box2" class="demo-box">Kliknij przycisk kilka razy</div>
            </div>
        </div>

        <!-- ĆWICZENIE 3 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">3</div>
                <div class="task-title">Dwie klasy - sukces i błąd</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong></p>
                <p>1. Utwórz klasę <code>.sukces</code> (zielone tło #e8f5e9, zielona ramka #4caf50, zielony tekst #2e7d32).</p>
                <p>2. Utwórz klasę <code>.blad</code> (czerwone tło #ffebee, czerwona ramka #f44336, czerwony tekst #c62828).</p>
                <p>3. Przycisk "Sukces" dodaje klasę .sukces (i usuwa .blad). Przycisk "Błąd" dodaje klasę .blad (i usuwa .sukces).</p>
                <button class="demo-btn" id="btnSukces">Sukces</button>
                <button class="demo-btn" id="btnBlad">Błąd</button>
                <div id="box3" class="demo-box">Status: oczekiwanie...</div>
            </div>
        </div>

        <!-- ĆWICZENIE 4 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">4</div>
                <div class="task-title">createElement - utwórz paragraf</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu przycisku utwórz nowy element <code>&lt;p&gt;</code> z tekstem "Nowy paragraf!" i dodaj go do kontenera "container4".</p>
                <div class="info-box">💡 Schemat: createElement() → innerHTML → appendChild()</div>
                <button class="demo-btn" id="btn4">Dodaj paragraf</button>
                <div id="container4" class="demo-container">
                    <p>Istniejący paragraf</p>
                </div>
            </div>
        </div>

        <!-- ĆWICZENIE 5 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">5</div>
                <div class="task-title">createElement - utwórz element z klasą</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu utwórz nowy <code>&lt;div&gt;</code>, nadaj mu klasę "nowy-element", ustaw tekst "Dodano nowy element!" i dodaj do kontenera "container5".</p>
                <button class="demo-btn" id="btn5">Dodaj div z klasą</button>
                <div id="container5" class="demo-container">
                    <!-- Tu pojawią się nowe elementy -->
                </div>
            </div>
        </div>

        <!-- ĆWICZENIE 6 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">6</div>
                <div class="task-title">createElement - dodaj element listy</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu utwórz nowy element <code>&lt;li&gt;</code> z tekstem "Nowy element listy" i dodaj go do listy "list6".</p>
                <button class="demo-btn" id="btn6">Dodaj do listy</button>
                <ul id="list6" class="demo-list">
                    <li>Element 1</li>
                    <li>Element 2</li>
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 7 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">7</div>
                <div class="task-title">remove() - usuń element po kliknięciu</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu przycisku "Usuń" usuń element "box7" ze strony.</p>
                <div class="info-box">💡 element.remove() - usuwa element z DOM</div>
                <button class="demo-btn" id="btn7">Usuń box</button>
                <div id="box7" class="demo-box">Ten element zostanie usunięty</div>
            </div>
        </div>

        <!-- ĆWICZENIE 8 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">8</div>
                <div class="task-title">remove() - usuń kliknięty element</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Dodaj addEventListener do KAŻDEGO elementu z klasą "usuwany". Po kliknięciu w element, ten element ma się usunąć (użyj <code>this.remove()</code>).</p>
                <div class="demo-container">
                    <div class="demo-box usuwany" style="cursor: pointer;">Kliknij mnie aby usunąć (1)</div>
                    <div class="demo-box usuwany" style="cursor: pointer;">Kliknij mnie aby usunąć (2)</div>
                    <div class="demo-box usuwany" style="cursor: pointer;">Kliknij mnie aby usunąć (3)</div>
                </div>
            </div>
        </div>

        <!-- ĆWICZENIE 9 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">9</div>
                <div class="task-title">parentElement - usuń rodzica</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Każdy przycisk "X" ma usunąć CAŁY element listy (swojego rodzica). Użyj <code>this.parentElement.remove()</code>.</p>
                <div class="info-box">💡 parentElement zwraca rodzica elementu (element nadrzędny)</div>
                <ul id="list9" class="demo-list">
                    <li>Zadanie 1 <button class="demo-btn-small usun-rodzica">X</button></li>
                    <li>Zadanie 2 <button class="demo-btn-small usun-rodzica">X</button></li>
                    <li>Zadanie 3 <button class="demo-btn-small usun-rodzica">X</button></li>
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 10 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">10</div>
                <div class="task-title">Dodaj element z wartości input</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu przycisku pobierz tekst z inputa "input10", utwórz nowy element <code>&lt;li&gt;</code> z tym tekstem i dodaj do listy "list10". Wyczyść input po dodaniu.</p>
                <div style="margin: 10px 0;">
                    <input type="text" id="input10" placeholder="Wpisz tekst...">
                    <button class="demo-btn" id="btn10">Dodaj</button>
                </div>
                <ul id="list10" class="demo-list">
                    <li>Przykładowy element</li>
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 11 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">11</div>
                <div class="task-title">Dodaj element z przyciskiem usuwania</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Jak ćwiczenie 10, ale każdy nowy element listy ma mieć też przycisk "X" do usunięcia. Musisz utworzyć przycisk, dodać mu addEventListener i appendChild do li.</p>
                <div class="info-box">💡 Utwórz: li → dodaj tekst → utwórz button → addEventListener na button → appendChild button do li → appendChild li do ul</div>
                <div style="margin: 10px 0;">
                    <input type="text" id="input11" placeholder="Wpisz zadanie...">
                    <button class="demo-btn" id="btn11">Dodaj z X</button>
                </div>
                <ul id="list11" class="demo-list">
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 12 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">12</div>
                <div class="task-title">Licznik elementów</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Wyświetlaj na bieżąco liczbę elementów w liście "list12". Użyj <code>element.children.length</code> do policzenia dzieci.</p>
                <div style="margin: 10px 0;">
                    <input type="text" id="input12" placeholder="Nowy element...">
                    <button class="demo-btn" id="btnDodaj12">Dodaj</button>
                    <button class="demo-btn" id="btnUsunOstatni12">Usuń ostatni</button>
                </div>
                <p>Liczba elementów: <strong id="counter12">2</strong></p>
                <ul id="list12" class="demo-list">
                    <li>Element startowy 1</li>
                    <li>Element startowy 2</li>
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 13 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">13</div>
                <div class="task-title">Mini TODO - dodawanie i usuwanie</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Stwórz prostą listę TODO: wpisz zadanie, kliknij "Dodaj", zadanie pojawi się z przyciskiem "Usuń". Kliknięcie "Usuń" usuwa zadanie.</p>
                <div style="margin: 10px 0;">
                    <input type="text" id="todoInput" placeholder="Co masz do zrobienia?">
                    <button class="demo-btn" id="todoAdd">Dodaj zadanie</button>
                </div>
                <ul id="todoList" class="demo-list">
                </ul>
            </div>
        </div>

        <!-- ĆWICZENIE 14 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">14</div>
                <div class="task-title">Dodaj komentarz</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Po kliknięciu "Dodaj komentarz" utwórz div z klasą "demo-box", wstaw tekst z inputa, dodaj do kontenera. Sprawdź czy input nie jest pusty!</p>
                <div style="margin: 10px 0;">
                    <input type="text" id="commentInput" placeholder="Napisz komentarz...">
                    <button class="demo-btn" id="commentAdd">Dodaj komentarz</button>
                </div>
                <div id="comments" class="demo-container">
                    <div class="demo-box">Przykładowy komentarz</div>
                </div>
            </div>
        </div>

        <!-- ĆWICZENIE 15 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">15</div>
                <div class="task-title">Wyczyść wszystkie elementy</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Przycisk "Wyczyść wszystko" ma usunąć WSZYSTKIE elementy z kontenera "container15". Użyj <code>innerHTML = ''</code> lub pętli z remove().</p>
                <div style="margin: 10px 0;">
                    <button class="demo-btn" id="btnDodaj15">Dodaj element</button>
                    <button class="demo-btn" id="btnWyczysc15" style="background: #e57373;">Wyczyść wszystko</button>
                </div>
                <div id="container15" class="demo-container">
                    <div class="demo-box">Element 1</div>
                    <div class="demo-box">Element 2</div>
                    <div class="demo-box">Element 3</div>
                </div>
            </div>
        </div>

        <!-- ĆWICZENIE 16 -->
        <div class="task">
            <div class="task-header">
                <div class="task-number">16</div>
                <div class="task-title">Lista zakupów</div>
                <div class="difficulty">Trudność: <span class="difficulty-star">⭐⭐⭐</span></div>
            </div>
            <div class="task-content">
                <p><strong>Polecenie:</strong> Stwórz listę zakupów: dodawanie produktów, usuwanie pojedynczych produktów (X), wyświetlanie liczby produktów. Walidacja: nie dodawaj pustych!</p>
                <div style="margin: 10px 0;">
                    <input type="text" id="productInput" placeholder="Nazwa produktu...">
                    <button class="demo-btn" id="productAdd">Dodaj produkt</button>
                </div>
                <p>Produktów na liście: <strong id="productCount">0</strong></p>
                <ul id="shoppingList" class="demo-list">
                </ul>
            </div>
        </div>

        <footer>
            <p>Przygotowanie do egzaminu INF.03 - Tworzenie elementów DOM</p>
            <p style="margin-top: 10px; font-size: 0.9em;">📚 JavaScript | 💻 DOM | ➕ createElement | ➖ remove</p>
        </footer>
    </div>

    <!-- TU UCZNIOWIE WPISUJĄ SWÓJ KOD -->
    <script>
        // =============================================
        // ĆWICZENIA 1-3: Pamiętaj o utworzeniu klas CSS!
        // =============================================

        // ĆWICZENIE 1
        // W CSS utwórz: .zaznaczony { background-color: #fffde7; border: 3px solid #ffc107; padding: 15px; }
        // document.getElementById('btn1').addEventListener('click', function() {
        //     document.getElementById('box1').classList.add('zaznaczony');
        // });

        // ĆWICZENIE 4 - przykład createElement
        // document.getElementById('btn4').addEventListener('click', function() {
        //     const nowyP = document.createElement('p');
        //     nowyP.innerHTML = 'Nowy paragraf!';
        //     document.getElementById('container4').appendChild(nowyP);
        // });

        // ĆWICZENIE 9 - przykład parentElement
        // const przyciski = document.querySelectorAll('.usun-rodzica');
        // przyciski.forEach(function(btn) {
        //     btn.addEventListener('click', function() {
        //         this.parentElement.remove();
        //     });
        // });

    </script>
</body>
</html>
```

**Instrukcja dla uczniów:**
1. Skopiuj ten HTML na swój dysk
2. Otwórz w VS Code
3. **ĆWICZENIA 1-3:** Najpierw utwórz klasy CSS w sekcji `<style>`!
4. W sekcji `<script>` piszesz kod JavaScript
5. Otwórz plik w przeglądarce (Live Server)
6. Testuj: dodawaj elementy, usuwaj, obserwuj zmiany

---

## 📋 LISTA ĆWICZEŃ (bez rozwiązań)

### Tworzenie klas CSS (Ćwiczenia 1-3)

| Nr | Temat | Opis |
|----|-------|------|
| 1 | Utwórz klasę i dodaj | Zdefiniuj .zaznaczony w CSS, dodaj przez classList.add |
| 2 | Utwórz klasę i przełączaj | Zdefiniuj .wazny, użyj classList.toggle |
| 3 | Dwie klasy (sukces/błąd) | Zdefiniuj .sukces i .blad, przełączaj między nimi |

### createElement + appendChild (Ćwiczenia 4-6)

| Nr | Temat | Opis |
|----|-------|------|
| 4 | Utwórz paragraf | createElement('p') + appendChild |
| 5 | Utwórz div z klasą | createElement + classList.add + appendChild |
| 6 | Dodaj element listy | createElement('li') + appendChild do ul |

### remove() (Ćwiczenia 7-8)

| Nr | Temat | Opis |
|----|-------|------|
| 7 | Usuń element przyciskiem | element.remove() |
| 8 | Usuń kliknięty element | this.remove() w addEventListener |

### parentElement (Ćwiczenia 9)

| Nr | Temat | Opis |
|----|-------|------|
| 9 | Usuń rodzica | this.parentElement.remove() |

### Praktyczne zastosowania (Ćwiczenia 10-16)

| Nr | Temat | Opis |
|----|-------|------|
| 10 | Dodaj z inputa | Pobierz value, utwórz element, dodaj |
| 11 | Element z przyciskiem X | Utwórz li + button wewnątrz |
| 12 | Licznik elementów | children.length |
| 13 | Mini TODO | Dodawanie + usuwanie zadań |
| 14 | Komentarze | Dodawanie komentarzy + walidacja |
| 15 | Wyczyść wszystko | Usuwanie wszystkich dzieci |
| 16 | Lista zakupów | Pełny projekt z licznikiem |

Miejsce do wysłania zadań: https://www.dropbox.com/request/Fwbnkz1c4QaeFtATG97f
