# HospitalDeviceCheck

This ASP.NET Core MVC application allows hospital staff to manage medical devices and locations, and record device checks (e.g., AED, temperature) securely with Azure AD authentication.

## Features
- Manage locations and devices (admin CRUD screens)
- Record device checks (staff screens)
- SQL Server backend with Dapper ORM
- Secure authentication via Azure AD

## Setup
1. Update `appsettings.json` with your SQL Server and Azure AD details.
2. Apply the schema in your SQL Server instance.
3. Run `dotnet restore`, then `dotnet run`.

## Database Schema
```sql
CREATE TABLE Locations (
    Id INT IDENTITY PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Description NVARCHAR(255)
);

CREATE TABLE Devices (
    Id INT IDENTITY PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Type NVARCHAR(50),
    SerialNumber NVARCHAR(100),
    LocationId INT FOREIGN KEY REFERENCES Locations(Id)
);

CREATE TABLE DeviceChecks (
    Id INT IDENTITY PRIMARY KEY,
    DeviceId INT FOREIGN KEY REFERENCES Devices(Id),
    CheckedBy NVARCHAR(100),
    CheckType NVARCHAR(50),
    Value NVARCHAR(100),
    CheckedAt DATETIME NOT NULL DEFAULT GETDATE()
);
```