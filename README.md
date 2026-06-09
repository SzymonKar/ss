# Projekt-FitnessApp-Szymon
Aplikacja webowa ASP.NET Core stworzona z myślą o kompleksowym zarządzaniu siłownią, treningami oraz dietą.
---
## 📖 Dokumentacja Projektu
### 1. Opis Projektu
**Projekt-FitnessApp-Szymon** to kompleksowa aplikacja internetowa stworzona z myślą o osobach trenujących oraz zarządzających klubami fitness. Aplikacja została zrealizowana w oparciu o architekturę wielowarstwową z wykorzystaniem nowoczesnego frameworka **ASP.NET Core (wersja .NET 8.0)**, a za warstwę dostępu do danych oraz mapowanie obiektowo-relacyjne (ORM) odpowiada **Entity Framework Core** we współpracy z bazą danych Microsoft SQL Server.
Głównym celem systemu jest automatyzacja oraz ułatwienie zarządzania treningami, planami dietetycznymi, grafikami zajęć grupowych, jak również asortymentem i zamówieniami dla klientów siłowni. Dzięki wbudowanemu systemowi uwierzytelniania opartemu o **ASP.NET Core Identity**, aplikacja dba o bezpieczeństwo i integralność danych każdego użytkownika, oferując dedykowane panele dla poszczególnych ról.
### 2. Opis Zrealizowanych Funkcjonalności
W ramach projektu wdrożono szeroki wachlarz modułów, które pokrywają najważniejsze aspekty funkcjonowania centrum fitness. Kluczowe zrealizowane funkcjonalności to:
* **Autoryzacja i Profile Użytkowników:** Rejestracja, logowanie oraz zarządzanie kontem za pomocą Identity. Aplikacja przechowuje profile użytkowników wraz z ich przypisaniami (`UserFitnessAssignment`) i pozwala na śledzenie wskaźników fizycznych.
* **Zarządzanie Treningami:** Baza ćwiczeń i maszyn, podział na partie mięśniowe oraz sekcje. Użytkownik ma możliwość układania planów treningowych i przypisywania do nich poszczególnych pozycji planu i sesji (`TrainingSession`).
* **Zarządzanie Dietą:** System pozwala na tworzenie pełnych jadłospisów i diet, organizowanych według dni (`DietPlanDay`) oraz posiłków (`Meal`), w tym zarządzanie produktami i wartościami odżywczymi.
* **Zajęcia Fitness i Harmonogramy:** Tworzenie grafików zajęć (`ClassSchedule`) i konkretnych wydarzeń (`ClassEvent`), co ułatwia zarządzanie rezerwacjami i harmonogramem trenerów.
* **Śledzenie Postępów:** Moduł wprowadzania parametrów treningowych i sylwetkowych (`ProgressEntry`) w czasie, pozwalający na wizualizację efektów i modyfikację celów na bieżąco.
* **Sklep / Zamówienia:** Realizacja e-commerce dla suplementów lub karnetów, umożliwiająca przeglądanie produktów (`Product`), składanie zamówień (`Order`) oraz tworzenie pozycji zamówień (`OrderItem`).
---
## ⚙️ Wykorzystane biblioteki i technologie
Projekt został oparty o framework **.NET 8.0** oraz **ASP.NET Core**. W projekcie wykorzystano następujące pakiety NuGet (wraz z ich wersjami):
- **Microsoft.AspNetCore.Identity.EntityFrameworkCore** (wersja `8.*`) - Dostarcza mechanizmy autoryzacji i uwierzytelniania w oparciu o Entity Framework Core (np. rejestracja, logowanie użytkowników, role).
- **Microsoft.AspNetCore.Identity.UI** (wersja `8.*`) - Domyślne interfejsy i widoki dla systemu Identity (gotowe strony logowania, rejestracji i zarządzania kontem).
- **Microsoft.EntityFrameworkCore.SqlServer** (wersja `8.0.27`) - Provider Entity Framework Core dla bazy danych Microsoft SQL Server, umożliwiający komunikację z bazą relacyjną.
- **Microsoft.EntityFrameworkCore.Design** (wersja `8.*`) oraz **Microsoft.EntityFrameworkCore.Tools** (wersja `8.0.27`) - Narzędzia wspierające tworzenie i aplikowanie migracji bazy danych (np. komendy `Add-Migration`, `Update-Database`).
- **Microsoft.VisualStudio.Web.CodeGeneration.Design** (wersja `8.*`) - Narzędzie wspierające scaffolding (automatyczne generowanie kodu kontrolerów i widoków).
---
## 🚀 Instrukcja instalacji i konfiguracji projektu
Aby uruchomić projekt w środowisku lokalnym (deweloperskim), należy postępować zgodnie z poniższymi krokami:
### 1. Wymagania wstępne
- Zainstalowany **.NET 8.0 SDK**.
- Zainstalowane środowisko programistyczne: **Visual Studio 2022**, **JetBrains Rider** lub **Visual Studio Code** z rozszerzeniem C# Dev Kit.
- Serwer bazy danych **Microsoft SQL Server** (np. SQL Server Express lub LocalDB) zainstalowany i uruchomiony.
### 2. Pobranie projektu
Skopiuj projekt z repozytorium do wybranego folderu na swoim komputerze:
```bash
git clone https://github.com/Szymon/Projekt-FitnessApp-Szymon.git
cd Projekt-FitnessApp-Szymon/WebApplication1
```
### 3. Konfiguracja połączenia z bazą danych
W pliku `appsettings.json` (lub `appsettings.Development.json`) sprawdź wartość klucza `ConnectionStrings`. Domyślnie ciąg połączenia powinien wskazywać na Twoją lokalną instancję bazy danych SQL Server:
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=FitnessAppDB;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```
*Dostosuj wartość (np. `Server=localhost\\SQLEXPRESS`), w zależności od posiadanego serwera SQL.*
### 4. Przygotowanie bazy danych (Migracje)
Upewnij się, że narzędzia Entity Framework Core (`dotnet ef`) są zainstalowane globalnie. W terminalu (w folderze z plikiem `WebApplication1.csproj`) uruchom komendę, aby zaktualizować (lub utworzyć) bazę danych wraz ze schematem wymaganym przez aplikację:
```bash
dotnet tool install --global dotnet-ef
dotnet ef database update
```
*Alternatywnie, korzystając z Konsoli Menedżera Pakietów (Package Manager Console) w Visual Studio, uruchom:*
```powershell
Update-Database
```
### 5. Uruchomienie aplikacji
Aplikację można uruchomić z poziomu środowiska IDE (np. przyciskiem "Run" / klawisz F5 w Visual Studio) lub w terminalu korzystając z komendy:
```bash
dotnet run
```
Aplikacja zostanie zbudowana, a w konsoli pojawi się informacja o adresie lokalnym (najczęściej `http://localhost:5000` lub `https://localhost:5001`), pod którym dostępna jest platforma.
