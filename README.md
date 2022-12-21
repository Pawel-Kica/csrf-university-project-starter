### Instrukcja projekt CSRF

Przygotowaliśmy przykładową aplikacje blog, która w obecnym stanie jest podatna na atak **Cross Site Request Forgery**. Poniżej znajduje sie instrukcja która pozwoli **Ci samodzielnie** w pierwszej części, zaatakować naszą stronę, a następnie w części drugiej dowiesz się jak skutecznie zabezpieczać aplikacje przed tą podatnością. 

### Część 0 - konfiguracja środowiska
- Rekomendowany edytor kodu - Visual Studio Code
- Sklonuj następujące repozytorium - https://github.com/Pawel-Kica/csrf-university-project-starter
- Przejdź do sklonowanego repozytorium na swojej maszynie
- W terminalu wykonaj następujące komendy
    - npm install

- Aby uruchomić aplikacje, użyj jednej z poniższych komend
    - ```npm run dev``` - serwer deweloperski
    - ```npm run start``` - serwer statyczny

- Jeżeli używasz edytora Visual studio code (a powinieneś), zainstaluj rozszerzenie "Live Server"
    - używając polecenia - ```code --install-extension ritwickdey.liveserver```
    - poprzez graficzny interfejs

- Następnie uruchom rozszerzenie
    - klikając przycisk **Go Live** znajdujący się na pasku w prawym dolnym rogu
    - poprzez użycie skrótu klawiszowego (```⌘+shift+P``` lub ```ctrl+shift+P```) otwórz laucher i wpisz ```Open with live server```

- W przypadku jeżeli nie używasz edytora Visual Studio Code, znajdź sposób na zahostowanie plików HTML

### Część 1 - atak
---
**1. Usunięcie konta zalogowanego użytkownika**

Zmodyfikuj plik ```vulnerable-delete.html```, tak aby zawierał formularz z następującymi parametrami
- action - ```http://localhost:3000/deleteAccount```
- method - ```POST```
- target - ```frame``` lub ```_blank``` (więcej informacji znajdziesz **[tutaj](https://www.w3schools.com/tags/att_form_target.asp)** )
- id - unikalny identyfikator formularza

Następnie dodaj do tego pliku kod w języku javascript, który spowoduje wysłanie formularza bez ingerencji użytkownika

Po wykonaniu powyższych czynności, wejście na stronę ```http://localhost:5500/vulnerable-delete.html``` będąc zalogowanym, powinno spowodować usunięcie konta użytkownika.

---
**2. Dodanie posta w imieniu zalogowanego użytkownika**

Zmodyfikuj plik ```vulnerable-add.html``` podobnie jak w podpunkcie 1, ze zmienionym paramtetrem **action** - ```http://localhost:3000/addPost```

Umieść wewnątrz formularza element ```input``` z następującymi parametrami:
- name - ```content```
- type - ```submit```
- id - unikalny identifikator pola input
- value - treść którą chcesz umieścić w poście

Następnie dodaj do tego pliku kod w języku javascript, który spowoduje wysłanie formularza bez ingerencji użytkownika

Po wykonaniu powyższych czynności, wejście na stronę ```http://localhost:5500/vulnerable-add.html``` powinno spowodować dodanie nowego postu jako zalogowany użytkownik.

---
##### Zadbaj o to aby ataki były całkowicie niewidoczne dla użytkownika (więcej informacji znajdziesz **[tutaj](https://www.w3schools.com/css/css_display_visibility.asp)** )

### Część 2 - obrona

**1. Obrona przed niechcianym usunięciem konta za pomocą ukrytej wartości dodanej do formularza**

Zainstaluj paczkę npm potrzebną do ochrony przeciwko atakami CSRF za pomocą komendy ```npm i csrf```

W pliku ```app.js``` stwórz ```middleware``` umożliwiający generację sekretnych tokenów, poprzez dodanie następującej linijki:
- ```const csrfProtection = csrf({cookie: true});```

Dodaj powyższy ```middleware``` na route ```GET /deleteAccount``` oraz ```POST /deleteAccount``` i zastąp zawartość funkcji renderującej strone ```deleteAccount``` następującym kodem
- ```res.render('deleteAccount', {csrfToken: req.csrfToken()});```

Wewnątrz formularza w pliku ```deleteAccount.ejs``` umieść element typu input
- ```<input type="hidden" name="_csrf" value="<%= csrfToken %>">```

Otwórz narzędzia dewelopera w swojej przeglądarce i zlokalizuj ukryty token **csrf**.

---
Spróbuj samodzienie zabezpieczyć routy ```GET oraz POST /addPost```.




