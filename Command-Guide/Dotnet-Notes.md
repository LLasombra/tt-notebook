## .net core setup
  1. Install ASP .Net Core
    \\192.168.1.19\Development\Casino\Software\DotNetCore
  2. VS Code(Visual Studio Code) 
    Add plugin C#, C# Extensions
  3. velo-data-integration\src\DataIntegration.Web  dir run: dotnet run
  4. open http://localhost:5000/swagger

## create .net core project
  - dotnet new mvc -n xxxProjectName  `创建 xxxProjectName .net core mvc项目`
  - dotnet new sln -n xxxProjectName  `新建 xxxProjectName.csproj file`
  - dotnet sln xxxProjectName.sln add xxxProjectName\xxxProjectName.csproj  `添加子项目 csproj 到主项目 csproj`

## .net core debug
  1. Program.cs
  ``` C#
  public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
      WebHost.CreateDefaultBuilder(args)
      .UseDefaultServiceProvider(options => { options.ValidateScopes = false; })
      .UseUrls("http://192.168.111.85:6006/")
      .UseSetting("detailedErrors", "true")
  ```
  3. appsettings.json
  ``` json
  "ConnectionStrings": {
    "TableDB": "Server=VELO-QA-DB01\\DEV1;Database=Dev1_Integration;User Id=sa; Password=sa"
  },
  ```
  4. remove oauth
    4.1 Startup.cs  -> // ConfigureAuthentication(services);
    4.2 TableFillCreditController -> // [Authorize]

## ETL, OLAP deploy:
- ETL:
  1. delete Integration Services Catalogs -> SSISDB, and Create SSISDB (pwd: abc123_), and Create Folder: velo
  2. Edit (D:\deploy\ETL\Deployment) Deploy_SSISPoject.ps1 and modify parameter: $SQLInstance = "VELO-QA-DB01\dev1"       $FolderName = "velo", and run
  3. exec Util_CreateEnvironment.sql, modify: @environment_name = N'velo-qa1' and ConnectionString
  4. exec Util_LinkEnvironmentToProject.sql, modify: @environment_name nvarchar(128) = N'velo-qa1'
  5. modify Integration Services Catalogs -> Environments -> velo-xx -> Properties -> Variables -> pwd = sa
- OLAP: 
  use visual studio, modify config: 
  1. EstimatedWinloss -> Properties -> Deplotment -> Target Info
  2. Data Sources -> EstimatedWinlossDW.ds -> Open-> General -> Connection string Edit
  3. build, and deploy
- 删了dw的数据，然后启动job同步到dw，最后deploy，如果不行删除Integration Services Catalogs的SSISDB再重复上诉步骤;
- EstimatedWinLoss init之后需要设置Roles  - IIS  -  General -> Full control   /  Membership  Add -> IUSR

## Reset db:
1. open mm management -> reset   (http://velo-qa-web01/ -> Demo Console -> Reset All  will get error, and no problem)
2. run reset bat script (should be disable the job at first) (D:\project\velo-Mockup\Service\Server\Modules\GamingPlatform.DemoDataProvider\RestoreDBScripts\Reset_Local_QA1_Area) -> reset-xx.bat
3. mstsc web01 and open VProgramSync - Shortcut files ->VProgramSync.exe at desktop (just local qa1 env)
4. enable job, and check job and process estimatedwinloss db

## init dw db：
  - gradlew initEstimatedWinLossDB -PenvironmentName=dev1            
  need modify job config:
  - Table_ProcessWinLossCube:
    - server: localhost  --> localhost\dev1
  - Table_SyncGamingHierachy:
    - package 
      - server: localhost --> velo-qa-db01\dev1
      - package: \SSISDB\velo\EstimatedWinLossTableConfig\ETLGamingHierarchies.dtsx
    - configuration 
      - parameters:
      - connection managers:
      - configuration advanced:

## Command
- ei-is 5.8 db: `gradlew initWSO2ISDB -PenvironmentName=local --rerun-tasks`
- ei-bps db: `gradlew initWSO2EIBPSDB -PenvironmentName=qa1 --rerun-tasks`
- Run command line in directory "source"
  - mvn clean package -DskipTests
- Run command line in directory "build\camp-dist"
  - gradlew clean customizeCamp -PenvironmentName=local --rerun-tasks
- gradlew clean customizeCamp -PenvironmentName=local -PbuildVariant=TableOnly --rerun-tasks
- open jMeter
  - gradlew jmGui -PenvironmentName=qa1          
- build ESB EI
  - gradlew customizeEI
- gradlew clean campDBCommonInit -PenvironmentName=dev1
- gradlew campDBCommonDBLink -PenvironmentName=dev1
- gradlew updateESBArtifact
- init camp db pm db
  - gradlew clean initCampDB -PenvironmentName=azureqa2
- gradlew clean concatSqlCampCommon -PenvironmentName=azureqa2
- Generate reset script
  - gradlew clean concatSqlCampCommon -PenvironmentName=qa1

## DB Upgrade - flyway migration:
- integration db:
  - gradlew flywayRepairTableIntegrationDB -PenvironmentName=local
  - gradlew flywayMigrateTableIntegrationDB -PenvironmentName=local
- dw db:
  - gradlew flywayRepairEstimatedWinLossDB -PenvironmentName=local
  - gradlew flywayMigrateEstimatedWinLossDB -PenvironmentName=local

