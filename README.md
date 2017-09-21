# Contoso University
This project is from the Tutorial.  One change is to make use of a SQL database in a container via docker-compose.


## Things to Remember

### Initialize a dotnet MVC project

```bash
dotnet new mvc
dotnet restore
```

### Setup the CSProj correctly to support EF

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
    <PackageReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Design" Version="2.0.0"/>
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0"/>
  </ItemGroup>

  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0"/>
  </ItemGroup>
```

### Connection Strings

```json
"ConnectionStrings": {
    "LocalDB": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity1;Trusted_Connection=True;MultipleActiveResultSets=true",
    "DockerSQL": "Server=localhost,1433;;User Id=sa;password=PasswordAzure@123;Database=ContosoUniversity;MultipleActiveResultSets=true"
  }
```

>Make sure you use the correct DB Context in the startup.cs

```cs
services.AddDbContext<SchoolContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

services.AddDbContext<SchoolContext>(options => options.UseSqlite("Data Source=ContosoUniversity.db"));
```


### Generator Commands

dotnet aspnet-codegenerator controller \
  -name StudentsController \
  -m Student \
  -dc SchoolContext \
  --relativeFolderPath Controllers \
  --useDefaultLayout \
  --referenceScriptLibraries
