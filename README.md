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



### Część 2 - obrona