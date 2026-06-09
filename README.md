# Projekt-FitnessApp-Szymon
Aplikacja webowa ASP.NET Core stworzona z myślą o kompleksowym zarządzaniu siłownią, treningami oraz dietą.
---

## Instrukcja instalacji i konfiguracji projektu
Aby uruchomić projekt w środowisku lokalnym (deweloperskim), należy postępować zgodnie z poniższymi krokami:
### 1. Wymagania wstępne
- Zainstalowany **.NET 8.0 SDK**.
- Zainstalowane środowisko programistyczne: **Visual Studio 2022**, **JetBrains Rider** lub **Visual Studio Code** z rozszerzeniem C# Dev Kit.
- Serwer bazy danych **Microsoft SQL Server** (np. SQL Server Express lub LocalDB) zainstalowany i uruchomiony.
### 2. Pobranie projektu
Skopiuj projekt z repozytorium do wybranego folderu na swoim komputerze:
```bash
git clone link do repozytorium
cd nazwa folderu/WebApplication1
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
