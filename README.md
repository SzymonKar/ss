Aplikacja korzysta z SQL Servera. Kontekst bazy danych to:

```text
ApplicationDbContext
```

Kontekst dziedziczy po:

```text
IdentityDbContext<IdentityUser, IdentityRole, string>
```

Dzieki temu baza zawiera zarowno tabele aplikacyjne, jak i tabele ASP.NET Identity.

Przykladowe tabele aplikacyjne:

- `PlanyTreningowe`
- `Cwiczenia`
- `PozycjePlanu`
- `PartieMiesniowe`
- `Maszyny`
- `Sekcje`
- `Meals`
- `Diets`
- `DietPlanDays`
- `ClassEvents`
- `ClassSchedules`
- `UserProfiles`
- `UserFitnessAssignments`
- `UserTrainingSessions`
- `ProgressEntries`
- `Products`
- `Orders`
- `OrderItems`

Migracje EF znajduja sie w katalogu:

```text
Migrations/
```

Program uruchamia migracje automatycznie przy starcie aplikacji:

```csharp
await dbContext.Database.MigrateAsync();
```

## 6. Role i uprawnienia

W projekcie zdefiniowano dwie role:

- `Klient`
- `Trener`

Rola `Trener` otrzymuje dodatkowe uprawnienia:

- `gym.manage_structure` - zarzadzanie struktura silowni,
- `users.assign_plans` - przypisywanie planow i diet uzytkownikom,
- `classes.manage` - zarzadzanie zajeciami,
- `store.manage` - zarzadzanie sklepem.

Uprawnienia sa wykorzystywane w politykach autoryzacji Razor Pages.

## 7. Konfiguracja

Connection string znajduje sie w plikach:

```text
appsettings.json
appsettings.Development.json
```

Domyslna konfiguracja laczy sie z lokalnym SQL Serverem:

```text
Server=localhost,1433;Database=FitnessAppDb;User Id=sa;Password=FitnessApp123!;TrustServerCertificate=True;Encrypt=True;MultipleActiveResultSets=true
```

Uwaga: haslo i connection string sa dobre do srodowiska lokalnego. W wersji produkcyjnej powinny byc przeniesione do zmiennych srodowiskowych albo bezpiecznego magazynu sekretow.

## 8. Uruchomienie projektu lokalnie

### Wymagania

- .NET SDK 8
- Docker Desktop albo lokalny SQL Server
- Visual Studio 2022 / Rider / VS Code

### Krok 1: uruchom baze danych

W katalogu `WebApplication1/` uruchom:

```bash
docker compose up -d
```

Plik `docker-compose.yml` uruchamia kontener SQL Server 2022 na porcie `1433`.

### Krok 2: uruchom aplikacje

W katalogu projektu uruchom:

```bash
dotnet run
```

Przy starcie aplikacja wykona migracje bazy danych i utworzy role oraz uprawnienia.

### Krok 3: otworz aplikacje

Po uruchomieniu wejdz w adres pokazany w konsoli, np.:

```text
https://localhost:xxxx
```

## 9. Nawigacja w aplikacji

Glowne sekcje dostepne w menu:

- Sekcja treningowa
- Trening
- Sesje
- Progres
- Trening w plenerze
- Moj profil
- Diety
- Baza posilkow
- Moje diety
- Zajecia
- Sklep
- Produkty
- Zamowienia

Czesc opcji jest widoczna lub dostepna tylko dla uzytkownika z rola `Trener`.

## 10. Najwazniejsze pliki

- `Program.cs` - konfiguracja aplikacji, Identity, autoryzacji, repozytoriow, sesji i endpointu pogodowego.
- `Data/ApplicationDbContext.cs` - konfiguracja tabel, relacji i ograniczen bazy danych.
- `Data/IdentitySeedData.cs` - tworzenie rol i uprawnien.
- `Security/AppRoles.cs` - stale nazw rol.
- `Security/AppPolicies.cs` - stale nazw polityk autoryzacji.
- `Security/AppPermissions.cs` - stale nazw uprawnien.
- `docker-compose.yml` - lokalny SQL Server.
- `Pages/Shared/_Layout.cshtml` - glowny layout i menu aplikacji.

## 11. Podsumowanie

FitnessApp to rozbudowana aplikacja webowa dla silowni lub trenera personalnego. Laczy funkcje zarzadzania planami treningowymi, dieta, zajeciami, postepami uzytkownikow i sklepem. Projekt ma klasyczna architekture ASP.NET Core Razor Pages z Entity Framework Core, repozytoriami, migracjami bazy danych oraz mechanizmem rol i uprawnien.
