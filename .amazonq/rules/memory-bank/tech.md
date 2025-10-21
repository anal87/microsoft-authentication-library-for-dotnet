# MSAL.NET Technology Stack

## Programming Languages and Versions

### Primary Language
- **C#** - Latest language version with modern language features
- **Target Frameworks**: Multi-targeting approach supporting:
  - .NET 8.0 (primary target based on global.json)
  - .NET Framework 4.6.2+
  - .NET Standard 2.0
  - Platform-specific targets (iOS, Android, UWP)

### Configuration Languages
- **MSBuild XML** - Project files and build configuration
- **JSON** - Configuration files, package management
- **YAML** - CI/CD pipeline definitions
- **PowerShell** - Build automation scripts

## Build System and Dependencies

### Build Infrastructure
- **MSBuild** - Primary build system with custom targets
- **Solution Structure**: Multiple solution files for different scenarios:
  - `LibsAndSamples.sln` - Main development solution
  - `CrossPlatform.slnf` - Cross-platform development filter
  - `PerformanceTests.sln` - Performance testing focused solution

### Package Management
- **NuGet** - Dependency management with centralized package versions
- **Directory.Packages.props** - Central package version management
- **PackageReference** - Modern package reference format

### Key Dependencies
- **Microsoft.VisualStudio.Threading.Analyzers** - Threading best practices enforcement
- **Microsoft.CodeAnalysis.NetAnalyzers** - Code quality analysis
- **System.Text.Json** - JSON serialization (modern .NET)
- **Newtonsoft.Json** - JSON serialization (legacy compatibility)

## Development Tools and Configuration

### Code Quality
- **EditorConfig** - Consistent code formatting across the project
- **Code Analysis** - Static analysis with Microsoft analyzers
- **Strong Naming** - Assembly signing with MSAL.snk key file
- **Warnings as Errors** - Strict compilation settings

### Testing Framework
- **MSTest** - Primary testing framework
- **BenchmarkDotNet** - Performance benchmarking
- **Moq** - Mocking framework for unit tests
- **Selenium** - Web UI automation testing

### CI/CD Pipeline
- **Azure DevOps** - Build and release pipelines
- **GitHub Actions** - Additional automation workflows
- **Multi-platform builds** - Windows, macOS, Linux support

## Platform-Specific Technologies

### Windows Desktop
- **Windows Forms** - Traditional Windows desktop UI
- **WPF** - Modern Windows desktop applications
- **WinUI 3** - Latest Windows app platform
- **WAM (Web Account Manager)** - Native Windows authentication broker

### Mobile Platforms
- **.NET MAUI** - Cross-platform mobile and desktop framework
- **Xamarin.iOS** - iOS-specific implementations
- **Xamarin.Android** - Android-specific implementations

### Web Technologies
- **ASP.NET Core** - Web application integration
- **System.Net.Http** - HTTP client for network operations
- **WebView2** - Modern web view control for authentication flows

## Development Commands

### Build Commands
```bash
dotnet build LibsAndSamples.sln          # Build main solution
dotnet test                               # Run all tests
dotnet pack                               # Create NuGet packages
```

### Testing Commands
```bash
dotnet test --configuration Release      # Release mode testing
dotnet test --logger trx                 # Generate test reports
dotnet run --project PerformanceTests    # Run performance benchmarks
```

### Development Workflow
```bash
dotnet restore                           # Restore NuGet packages
dotnet build --no-restore               # Build without restore
dotnet test --no-build                  # Test without rebuild
```

## Security and Compliance

### Cryptography
- **System.Security.Cryptography** - .NET cryptographic APIs
- **Platform-specific crypto** - Hardware security module integration
- **Certificate management** - X.509 certificate handling

### Compliance Features
- **FIPS compliance** - Federal Information Processing Standards support
- **Government cloud** - Sovereign cloud authentication support
- **Telemetry controls** - Privacy-compliant data collection

## Performance Optimization

### Benchmarking
- **Continuous performance monitoring** - Automated performance regression detection
- **Memory profiling** - Heap allocation optimization
- **Network optimization** - HTTP connection pooling and retry logic

### Caching Strategy
- **Multi-level caching** - In-memory and persistent token storage
- **Cache encryption** - Platform-specific secure storage
- **Cache partitioning** - Multi-tenant cache isolation