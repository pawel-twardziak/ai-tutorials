# Jak stworzyć prostego agenta AI w AnythingLLM - Kompletny poradnik

## Wprowadzenie

AnythingLLM to wszystko-w-jednym aplikacja AI, która umożliwia RAG, agentów AI i wiele więcej bez kodowania czy problemów z infrastrukturą. Agenci to w zasadzie LLM, które mają dostęp do prostych narzędzi.

W tym poradniku pokażemy, jak stworzyć prostego agenta AI używając **Agent Flows** - bezkodem sposób budowania umiejętności agencyjnych. Zbudowany dla każdego.

---

## Krok 1: Instalacja AnythingLLM Desktop

### Pobieranie aplikacji

1. **Przejdź na stronę**: [anythingllm.com/desktop](https://anythingllm.com/desktop)
2. **Wybierz odpowiednią wersję** dla swojego systemu:
   - **macOS**: Upewnij się, że pobierasz właściwy plik `.dmg`:
     - Dla Apple Silicon (M1/M2/M3): AnythingLLMDesktop-AppleSilicon.dmg
     - Dla Intel: standardowa wersja
   - **Windows**: AnythingLLMDesktop.exe
   - **Linux**: AppImage

### Instalacja

**Windows:**
1. Kliknij pobrany plik AnythingLLMDesktop.exe aby zainstalować
2. Ponieważ aplikacja jest niepodpisana, Windows Defender może chcieć potwierdzić, że na pewno chcesz uruchomić tę aplikację

**macOS:**
1. Otwórz plik `.dmg` i przeciągnij logo AnythingLLM do folderu Aplikacje

**Linux:**
- Uruchom plik AppImage

---

## Krok 2: Podstawowa konfiguracja

### Pierwsze uruchomienie

1. **Uruchom AnythingLLM** z pulpitu
2. **Wybierz dostawcę LLM**:
   - Możesz wybrać między AnythingLLM lub Ollama (zalecam AnythingLLM dla tego tutoriala)
3. **Wybierz model**:
   - Na przykład, możesz wybrać Phi-2: model 2.7B od Microsoft
4. **Zapisz zmiany** - oprogramowanie automatycznie pobierze model i wszystko skonfiguruje

### Tworzenie workspace'a

AnythingLLM organizuje twoje dokumenty w tak zwane workspace'y. Workspace'y są jak wątek konwersacji, który utrzymuje twoje dokumenty w kontenerach.

1. Stwórz nowy workspace
2. Nadaj mu opisową nazwę (np. "Mój pierwszy agent")

---

## Krok 3: Aktywacja agentów AI

### Włączanie funkcji agentów

1. Przejdź do ustawień workspace'a i nawiguj do menu konfiguracji agenta
2. **Wybierz umiejętności** dla swojego agenta:
   - Umiejętności oznaczone jako "Default" są domyślnymi umiejętnościami, których nie można wyłączyć
   - Niektóre narzędzia jak RAG, Podsumowywanie Dokumentów i Skrobanie Stron są włączone domyślnie

### Dostępne narzędzia domyślne

Twój agent będzie miał dostęp do kilku potężnych narzędzi:

- **RAG Search**: Możesz użyć wyszukiwania RAG pytając agenta o coś jak "@agent czy możesz sprawdzić co już wiesz o AnythingLLM?"
- **Web Browsing**: Narzędzie przeglądania sieci pozwala agentowi szukać w internecie i dawać odpowiedzi na twoje pytania
- **Web Scraping**: Narzędzie skrobania sieci pozwala agentowi skrobać stronę internetową i dawać odpowiedzi na twoje pytania
- **Chart Generation**: Narzędzie generowania wykresów pozwala agentowi tworzyć wykresy na podstawie podanego promptu/danych

---

## Krok 4: Tworzenie prostego Agent Flow

### Dostęp do edytora Flow

1. Aby stworzyć nowy flow, przejdź do strony umiejętności agenta w swoim workspace'ie i kliknij przycisk "Create Flow"
2. To otworzy konstruktor flow z pustym płótnem

### Podstawowe bloki

Gdy po raz pierwszy otworzysz konstruktor flow, zobaczysz puste płótno z kilkoma podstawowymi blokami. Są to fundamenty każdego flow:

Każdy nowy flow zaczyna się trzema podstawowymi blokami:
- **Flow Information Block** - Definiuje nazwę i opis flow
- **Flow Variables Block** - Ustawia wszelkie zmienne potrzebne w twoim flow

### Dodawanie funkcjonalności

Aby dodać funkcjonalność do swojego flow, musisz dodać bloki. Kliknij przycisk "Add Block" między istniejącymi blokami, aby zobaczyć dostępne opcje

---

## Krok 5: Przykład - Agent do monitorowania HackerNews

Stwórzmy praktycznego agenta, który będzie monitorował HackerNews pod kątem określonych tematów.

### Konfiguracja flow

1. **Flow Information Block**:
   - Nazwa: "HackerNews Monitor"
   - Opis: "Ten agent pomoże ci szybko znaleźć artykuły na tematy, które cię interesują"

2. **Flow Variables Block**:
   - Zmienna: `hackerNewsURLPath` (dla określenia, którą stronę HackerNews skrobać)

### Dodanie bloku Web Scraper

1. **Kliknij "Add Block"** i wybierz **Web Scraper**
2. **Konfiguracja**:
   - URL do skrobania: `https://news.ycombinator.com/${hackerNewsURLPath}`
   - Zmienna wynikowa: `pageContentFromSite`

### Dodanie bloku LLM Instruction

1. **Dodaj kolejny blok**: **LLM Instruction**
2. **Konfiguracja**:
   - Zmienne wejściowe: zmienne do wysłania do LLM
   - Instrukcje: Instrukcje do wysłania do LLM
   
   **Przykład instrukcji**:
   ```
   Przeanalizuj zawartość HackerNews i znajdź artykuły związane z {topic}. 
   Zwróć wyniki jako linki markdown z krótkimi opisami.
   ```

### Testowanie agenta

Po skonfigurowaniu flow:

1. **Zapisz** swój flow
2. **Użyj agenta** wpisując: @agent "Znajdź posty związane z AI na HackerNews"
3. **Obserwuj rezultaty**: Flow zwróci odpowiednie artykuły jako klikalne linki markdown

---

## Krok 6: Dostępne bloki do rozwijania agenta

Możesz rozbudować swojego agenta używając różnych bloków:

### Domyślne bloki

- **Web Scraper**: Do pobierania zawartości ze stron internetowych
- **API Call**: Umożliwia dynamiczną interakcję z dowolnym zewnętrznym API
- **LLM Instruction**: Do przetwarzania danych przez LLM
- **Read File**: Do odczytywania plików
- **Write File**: Do zapisywania plików

### Przykłady rozwinięć

1. **Dodaj blok API Call** dla integracji z zewnętrznymi usługami
2. **Użyj Read/Write File** do przechowywania wyników
3. **Łącz multiple flows** dla złożonych zadań

---

## Krok 7: Używanie agenta

### Rozpoczęcie sesji agenta

Wystarczy, że użyjesz @agent, aby rozpocząć sesję agenta. Podczas sesji agenta nie musisz wzmiankować agenta przez @agent, możesz po prostu kontynuować rozmowę z agentem jak z LLM.

### Przykłady poleceń

- `@agent` - rozpocznij sesję
- "@agent czy możesz wykonać wyszukiwanie w sieci na temat 'Co to jest problem z MKBHD i Humane AI Pin?' i dać mi kluczowe informacje, które muszę wiedzieć"
- "@agent czy możesz podsumować zawartość na https://docs.anythingllm.com/features/chat-logs"

---

## Wskazówki i rozwiązywanie problemów

### Wybór odpowiedniego modelu

Nie wszystkie modele LLM działają dobrze jako agenci. Główny problem, który widzimy z agentami, to ludzie, którzy chcą używać mniejszego modelu parametrycznego, który jest silnie skwantyzowany i chcą uzyskać jakość interakcji narzędziowych na poziomie GPT.

**Zalecenia**:
- Używaj modeli chmurowych (nieskwantyzowanych), które są zazwyczaj dramatycznie lepsze w podążaniu za instrukcjami
- Mniejsze modele z 4-bitową kwantyzacją nie będą odpowiadać poprawnie jako agent przez większość czasu, ale ten sam model z 8-bitową kwantyzacją da lepszą odpowiedź jako Agent

### Sprawdzanie działania narzędzi

Gdy narzędzie jest rzeczywiście wywołane, zobaczysz to, co nazywamy wyjściem "myśli" w interfejsie użytkownika.

Jeśli nie widzisz tego, agent prawdopodobnie "halucynuje" działanie narzędzia.

---

## Podsumowanie

Agent flows są bardzo elastycznym sposobem budowania umiejętności agencyjnych i w zależności od mocy twojego LLM, możesz nawet oczekiwać, że LLM połączy wiele flows razem, aby wykonać zadanie.

Teraz masz podstawową wiedzę, aby:
1. ✅ Zainstalować i skonfigurować AnythingLLM
2. ✅ Stworzyć swojego pierwszego agenta AI
3. ✅ Użyć Agent Flows bez kodowania
4. ✅ Rozbudować agenta o dodatkowe funkcjonalności

**Następne kroki**: Eksperymentuj z różnymi blokami i stwórz agentów dostosowanych do swoich potrzeb!