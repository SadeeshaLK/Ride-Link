# RideLink — Initial Main Branch

Shared initial base prepared from the supplied complete project. Requirements:
JDK 21, Maven 3.9.9 via the included wrapper, and MongoDB for services once added.
The original root and four service POMs are preserved. No application source,
service configuration, tests or completed service implementations are included.
Empty source folders are retained with .gitkeep files. This base cannot run the
service endpoints until members add their implementations.

## Member branches

| Member | Folder | Branch | Port |
| --- | --- | --- | --- |
| 1 | account-service | feature/account-service | 8081 |
| 2 | driver-service | feature/driver-service | 8082 |
| 3 | ride-service | feature/ride-service | 8083 |
| 4 | fare-service | feature/fare-service | 8084 |

## Put the base on main

Copy the CONTENTS of this extracted folder to the repository root. Include the
hidden .github, .mvn and .gitignore entries. Do not copy an archive's .git folder.
Use the existing clone and main branch if already initialized. Review existing
files before replacing them. If service source is already on main, copying this
base over it will NOT remove that source. Agree with the team before removing
existing service code; this archive is the starting point for an empty base.

For an existing clone with main:

```bash
git switch main
git pull --ff-only origin main
# Copy the base contents here, then review:
git status
git add pom.xml README.md .gitignore .github .mvn mvnw mvnw.cmd account-service driver-service ride-service fare-service
git commit -m "Initialize shared RideLink service structure"
git push origin main
```

For a NEW empty repository only:

```bash
git init -b main
git add .
git commit -m "Initialize shared RideLink service structure"
git remote add origin https://github.com/SadeeshaLK/Ride-Link.git
git push -u origin main
```

## Each member adds their code

Start from the updated main. Member 4 example:

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/fare-service
```

Copy ONLY fare-service/src from the full project into fare-service/src here,
including main Java, resources and test Java. Remove the .gitkeep files once
those folders contain source. Do not copy target or .git. The service POM is
already present, and the root POM already lists all four modules.

On Windows PowerShell:

```powershell
.\mvnw.cmd -pl fare-service -am test
git status
git add fare-service/src
git commit -m "Add fare and payment service implementation"
git push -u origin feature/fare-service
```

On Linux/macOS or Git Bash use ./mvnw instead of .\mvnw.cmd.
Other members follow the same steps with their assigned folder and branch.
If a branch name already exists, switch to it instead of creating it again.

Open a GitHub pull request with base main and compare your feature branch.
The repo maintainer reviews and merges it. Use Create a merge commit if the
team wants to preserve each original member commit in main's history.
Do not overwrite another member's service. Shared POM changes require review.

## Shared materials after service merges

The full archive's docs, Postman artifacts and machine-specific PowerShell
scripts are not part of this minimal initial base. Add reviewed shared docs and
integration tests in a separate PR after the services are merged. Keep the
original full ZIP as the source for each member's implementation.

## Verification

ZIP integrity, XML parsing, all module paths, parent coordinates and wrapper
files were checked. A Maven build was not executed here: this environment has
JDK 17 and no Maven installation; the project requires JDK 21. GitHub CI uses
JDK 21 and builds the current modules. Empty modules have no application tests.
