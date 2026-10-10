# Student Operations

This is a console application for registering students and creating enrollment requests. It uses Entity Framework Core for the database and Hangfire for background processing.

## What the project demonstrates

- Registering students
- Creating enrollment requests
- Immediate and delayed Hangfire jobs
- Recurring processing of pending requests
- Continuation jobs for enrollment confirmation
- Batch processing
- Automatic retries for a simulated temporary failure
- Processing history stored in SQL Server

## Project structure

- `StudentOperations.Domain` contains the models.
- `StudentOperations.Application` contains the service interface and Hangfire job class.
- `StudentOperations.Infrastructure` contains the database context and service implementation.
- `StudentOperations.Console` contains the program setup and menu.

## Requirements

- .NET SDK 10
- SQL Server LocalDB
- EF Core CLI tool

Install the EF Core tool if it is not already available:

```powershell
dotnet tool install --global dotnet-ef --version 10.0.12
```

## Database setup

The project uses two LocalDB databases:

- `StudentOperationsDb` for students, enrollment requests, and processing logs
- `StudentOperationsHangfireDb` for Hangfire jobs

The EF Core migration files are already included in:

```text
StudentOperations.Infrastructure/Data/Migrations
```

From the solution folder, restore, build, and apply the migration:

```powershell
dotnet restore
dotnet build
dotnet ef database update `
  --project StudentOperations.Infrastructure `
  --startup-project StudentOperations.Console
```

Create a LocalDB database named `StudentOperationsHangfireDb` in SQL Server Management Studio or SQL Server Object Explorer. Hangfire creates its own tables when the application starts.

## Run the project

From the solution folder:

```powershell
cd StudentOperations.Console
dotnet run
```

Use the Console menu to register students, create requests, and test each job type.

## Submission evidence

The repository contains the source code, EF Core migration files, and setup instructions. Screenshots of the application and database records are included in the submitted PDF.
