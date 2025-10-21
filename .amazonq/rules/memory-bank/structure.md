# MSAL.NET Project Structure

## Directory Organization

### Core Source Code (`src/`)
- **`Microsoft.Identity.Client/`** - Main MSAL library with core authentication logic
- **`Microsoft.Identity.Client.Desktop/`** - Desktop-specific extensions (Windows Forms, WPF)
- **`Microsoft.Identity.Client.Desktop.WinUI3/`** - WinUI 3 platform support
- **`Microsoft.Identity.Client.Broker/`** - Native broker integration for enhanced security
- **`Microsoft.Identity.Client.Extensions.Msal/`** - Additional utilities and extensions

### Test Infrastructure (`tests/`)
- **`Microsoft.Identity.Test.Unit/`** - Comprehensive unit test suite
- **`Microsoft.Identity.Test.Integration.netcore/`** - .NET Core integration tests
- **`Microsoft.Identity.Test.Integration.netfx/`** - .NET Framework integration tests
- **`Microsoft.Identity.Test.Performance/`** - Performance benchmarking tests
- **`Microsoft.Identity.Test.Common/`** - Shared test utilities and mocks
- **`Microsoft.Identity.Test.LabInfrastructure/`** - Lab environment test infrastructure
- **`Microsoft.Identity.Test.E2e/`** - End-to-end testing for Managed Identity scenarios

### Development Applications (`tests/devapps/`)
- **Platform-specific test apps**: Desktop (WinForms, WPF), Console, Web API
- **Mobile test apps**: MAUI, iOS, Android applications
- **Specialized scenarios**: WAM integration, Managed Identity, Kerberos, FOCI testing
- **Cache extension demos**: Token cache extensibility examples

### Cache Compatibility (`tests/CacheCompat/`)
- **Cross-platform cache testing**: Ensures token cache compatibility across MSAL versions
- **Java interoperability**: Tests cache compatibility with MSAL Java
- **Version migration**: Validates cache format migrations

### Build and Configuration
- **`build/`** - Build scripts, pipeline definitions, and configuration files
- **`docs/`** - Technical documentation and design specifications
- **`prototype/`** - Experimental features and proof-of-concept implementations

## Core Components and Relationships

### Authentication Flow Architecture
- **Public Client Applications**: Desktop and mobile app authentication
- **Confidential Client Applications**: Server-side and daemon application authentication
- **Token Cache**: Persistent and in-memory token storage with encryption
- **Authority Resolution**: Azure AD, B2C, and ADFS endpoint management
- **Network Layer**: HTTP client abstraction with retry and throttling logic

### Platform Abstraction
- **Platform Proxy**: Abstracts platform-specific functionality (UI, storage, networking)
- **Broker Integration**: Native authentication broker communication
- **Web UI**: Platform-specific web view implementations for interactive authentication

### Security Components
- **Cryptography**: Token encryption, key management, and secure storage
- **Certificate Handling**: Client certificate authentication support
- **Proof of Possession**: Advanced security token binding

## Architectural Patterns

### Dependency Injection
- Service locator pattern for platform-specific implementations
- Factory pattern for creating authentication contexts and token cache instances

### Async/Await Pattern
- Comprehensive async support throughout the authentication pipeline
- Cancellation token support for long-running operations

### Builder Pattern
- Fluent API for configuring authentication requests and client applications
- Method chaining for intuitive developer experience

### Observer Pattern
- Event-driven architecture for authentication state changes
- Telemetry and logging integration points

### Strategy Pattern
- Multiple authentication flow implementations
- Platform-specific UI and storage strategies