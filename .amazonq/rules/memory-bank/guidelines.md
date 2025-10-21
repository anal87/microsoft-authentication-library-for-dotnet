# MSAL.NET Development Guidelines

## Code Quality Standards

### Licensing and Copyright
- **Consistent licensing**: All files must include Microsoft copyright header with MIT License reference
- **Third-party attribution**: External code (like JSON.NET) includes original license headers with proper attribution
- **Copyright format**: Use `// Copyright (c) Microsoft Corporation. All rights reserved.` followed by `// Licensed under the MIT License.`

### Namespace and Assembly Organization
- **Hierarchical namespacing**: Follow `Microsoft.Identity.Client.[Feature].[SubFeature]` pattern
- **Internal visibility**: Core implementation classes marked as `internal` to hide implementation details
- **Public API surface**: Only essential classes and methods exposed publicly
- **Assembly boundaries**: Clear separation between client library and platform-specific extensions

### Error Handling and Validation
- **Comprehensive validation**: Use `ValidationUtils.ArgumentNotNull()` for parameter validation
- **Custom exceptions**: Leverage MSAL-specific exception hierarchy (`MsalException`, `MsalServiceException`, `MsalClientException`)
- **Error codes**: Consistent error code constants defined in `MsalError` class
- **Correlation IDs**: All requests include correlation IDs for tracing and debugging

### Logging and Telemetry
- **Structured logging**: Use `ILoggerAdapter` with different log levels (Info, Warning, Error, Verbose)
- **PII protection**: Separate PII and non-PII logging with `InfoPii()`, `ErrorPii()` methods
- **Telemetry events**: Comprehensive telemetry through `ApiEvent` class for performance monitoring
- **Conditional logging**: Check `IsLoggingEnabled()` before expensive logging operations

## Architectural Patterns

### Async/Await Implementation
- **Consistent async suffix**: All async methods end with `Async` suffix
- **ConfigureAwait(false)**: Always use `ConfigureAwait(false)` in library code to avoid deadlocks
- **CancellationToken support**: All async operations accept `CancellationToken` parameters
- **Task return types**: Use `Task<T>` for async methods returning values, `Task` for void operations

### Builder Pattern Usage
- **Fluent API design**: Method chaining for configuration (e.g., `WithAuthority().WithScope()`)
- **Immutable configuration**: Builder creates immutable configuration objects
- **Validation at build**: Validate configuration when `Build()` or `Execute()` is called
- **Optional parameters**: Use builder pattern for optional parameters instead of method overloads

### Factory and Service Locator Patterns
- **Service bundle**: Central `IServiceBundle` for dependency injection and service location
- **Platform abstraction**: `IPlatformProxy` abstracts platform-specific functionality
- **HTTP management**: Centralized HTTP client management through `IHttpManager`
- **Token cache abstraction**: `ICacheSessionManager` provides cache operations abstraction

### Request/Response Pattern
- **Base request class**: All authentication flows inherit from `RequestBase`
- **Parameter objects**: Use dedicated parameter objects (`AuthenticationRequestParameters`)
- **Response standardization**: Consistent `AuthenticationResult` return type across flows
- **Token response handling**: Centralized token response processing and caching

## Coding Conventions

### Naming Standards
- **Private fields**: Use underscore prefix (`_fieldName`) for private fields
- **Constants**: Use PascalCase for public constants, UPPER_CASE for internal constants
- **Method names**: Descriptive method names indicating action and return type
- **Boolean properties**: Use `Is`, `Has`, `Can`, `Should` prefixes for boolean properties

### Memory Management
- **IDisposable implementation**: Proper disposal of HTTP clients, streams, and other resources
- **Using statements**: Consistent use of `using` statements for disposable resources
- **Static caching**: Careful static field usage with proper cleanup mechanisms
- **Weak references**: Use weak references where appropriate to prevent memory leaks

### Thread Safety
- **Immutable objects**: Prefer immutable objects for thread safety
- **Concurrent collections**: Use `ConcurrentDictionary` and similar collections for shared state
- **Lock mechanisms**: Use `SemaphoreSlim` for async-compatible locking
- **Static field protection**: Protect static fields with appropriate synchronization

### Performance Optimization
- **String operations**: Use `StringBuilder` for multiple string concatenations
- **Collection initialization**: Pre-size collections when final size is known
- **Lazy initialization**: Use lazy initialization for expensive operations
- **Caching strategies**: Multi-level caching (memory, persistent) with appropriate expiration

## Testing Patterns

### Test Structure
- **AAA pattern**: Arrange, Act, Assert structure in all tests
- **Test method naming**: Descriptive names indicating scenario and expected outcome
- **Test categories**: Use `[TestCategory]` attributes for test organization
- **Data-driven tests**: Use `[DataRow]` for parameterized tests

### Mocking and Isolation
- **HTTP mocking**: Use `MockHttpManager` for HTTP request/response mocking
- **Dependency injection**: Mock dependencies through constructor injection
- **Test doubles**: Create test-specific implementations for complex dependencies
- **Isolation**: Each test should be independent and not rely on other tests

### Test Data Management
- **Test constants**: Centralized test constants in `TestConstants` class
- **Resource files**: External test data in resource files with `[DeploymentItem]`
- **Test helpers**: Reusable test setup methods in helper classes
- **Cleanup**: Proper test cleanup with `TestInitialize` and `TestCleanup`

## Security Best Practices

### Credential Handling
- **Secure storage**: Use platform-specific secure storage for sensitive data
- **Memory protection**: Clear sensitive data from memory after use
- **Certificate validation**: Proper X.509 certificate validation and handling
- **Token encryption**: Encrypt tokens in persistent storage

### Network Security
- **TLS enforcement**: Always use HTTPS for network communications
- **Certificate pinning**: Validate server certificates against expected values
- **Timeout configuration**: Appropriate timeouts to prevent hanging requests
- **Retry policies**: Implement exponential backoff for failed requests

### Input Validation
- **Parameter validation**: Validate all input parameters for null, format, and range
- **URL validation**: Validate and sanitize URLs before making requests
- **Scope validation**: Validate OAuth scopes against allowed patterns
- **Authority validation**: Validate authority URLs against known patterns

## API Design Principles

### Backward Compatibility
- **Versioning strategy**: Maintain backward compatibility within major versions
- **Obsolete attributes**: Mark deprecated APIs with `[Obsolete]` and migration guidance
- **Default values**: Provide sensible defaults for optional parameters
- **Extension methods**: Use extension methods for additional functionality

### Developer Experience
- **IntelliSense support**: Comprehensive XML documentation for all public APIs
- **Error messages**: Clear, actionable error messages with guidance
- **Code examples**: Include usage examples in XML documentation
- **Debugging support**: `[DebuggerStepThrough]` on wrapper methods to improve debugging

### Configuration Management
- **Hierarchical configuration**: Support multiple configuration sources with precedence
- **Environment-specific settings**: Support for different environments (dev, test, prod)
- **Feature flags**: Use feature flags for experimental or platform-specific features
- **Validation**: Validate configuration at startup with clear error messages