# TestingConventions

## Purpose & Scope
These conventions define standards for automated testing across all layers of the application. They ensure high-quality test coverage while maintaining efficiency through focused, meaningful tests that follow the YAGNI principle.

---

## Core Principles

### Fundamental Rules
- **Quality over Quantity**: Only implement truly necessary tests
- **Minimum Test Coverage**: Focus on critical business logic and main paths
- **Complete Namespaces**: Test projects mirror source project namespaces (e.g., `eSource.Core.CoreBusinessLayer.Tests`)
- **Test Independence**: Each test must be deterministic and independent
- **AAA Pattern**: Arrange-Act-Assert structure for all tests

### Testing Philosophy
- Test only what can break
- Focus on business-critical functionality
- Avoid testing framework code
- Prioritize integration over unit tests for trivial code
- Maintain 80%+ coverage for critical paths

---

## Implementation Guidelines

### Project Structure
```
Tests/
├── Core.Tests/              # Core Layer tests
│   ├── CorePersistLayer.Tests/
│   ├── CoreBusinessLayer.Tests/
│   └── EntityFramework.Tests/
├── Frontend.Tests/          # Frontend tests
│   └── Web.Tests/           # Blazor Component tests
├── Integration.Tests/       # Integration tests
└── chrome-devtools.Tests/        # E2E UI tests
```

### Test Levels

#### Unit Tests
- **Purpose**: Test individual methods and classes in isolation
- **Focus**: Business logic, edge cases, error conditions
- **Tools**: xUnit, Moq for mocking
- **Location**: Match source project structure
- **Naming**: `MethodName_Scenario_ExpectedResult()`

#### Integration Tests
- **Purpose**: Verify component interactions
- **Focus**: Database operations, API endpoints, service integrations
- **Tools**: In-memory database, WebApplicationFactory
- **Setup**: Proper test environment initialization and teardown
- **Data**: Use Bogus for test data generation

#### UI Tests (E2E)
- **Purpose**: Test complete user workflows
- **Focus**: Critical user journeys, form validations
- **Tools**: chrome-devtools for browser automation
- **Execution**: Separate test server profile (port 5288)
- **Coverage**: Happy paths and key error scenarios

#### Mobile/Responsive Testing
- **Purpose**: Verify responsive layouts and mobile UX quality without physical devices
- **Tools**: chrome-devtools MCP for device emulation (95%+ accuracy)
- **Approach**: Device emulation with specific viewport sizes
- **Coverage**: Mobile (<640px), Tablet (640-1023px), Desktop (≥1024px)
- **When to Use**: Any User Story involving responsive layouts or mobile-specific features
- **Alternative**: Physical device testing for production-critical features or final validation

**Standard Viewport Sizes**:
```
Mobile Devices:
- 320px × 568px  (iPhone SE 1st gen, small phones)
- 375px × 667px  (iPhone SE 2nd/3rd gen, iPhone 6/7/8)
- 390px × 844px  (iPhone 13/14)
- 393px × 852px  (iPhone 15)
- 414px × 896px  (iPhone Pro Max)

Tablet Devices:
- 768px × 1024px (iPad, standard tablets)
- 820px × 1180px (iPad Air)

Desktop:
- 1024px × 768px (small laptop)
- 1440px × 900px (standard desktop)
- 1920px × 1080px (full HD)
```

**Chrome DevTools MCP Tools**:
- `mcp__chrome-devtools__resize_page(width, height)` - Set viewport size
- `mcp__chrome-devtools__take_snapshot()` - Verify layout structure
- `mcp__chrome-devtools__take_screenshot()` - Visual documentation
- `mcp__chrome-devtools__evaluate_script()` - Test scroll behavior and interactions
- `mcp__chrome-devtools__list_console_messages()` - Check for layout errors

**Testing Procedure**:
1. Navigate to page with `navigate_page`
2. For each viewport size: resize → snapshot → verify layout → screenshot
3. Test interactions (scroll, nav, buttons) with `evaluate_script`
4. Verify no console errors or layout issues
5. Document results with screenshots

**Limitations**:
- Real touch gestures not possible (use scroll simulation instead)
- Some browser-specific behaviors may differ slightly from physical devices
- Haptic feedback and device-specific features not testable
- Network conditions (3G/4G) require separate emulation

**When Physical Devices Are Required**:
- Touch gesture quality assessment (swipe smoothness, momentum)
- Production-critical e-commerce or payment flows
- Browser-specific bugs that only appear on real devices
- Final stakeholder acceptance testing

---

## Standards & Specifications

### Required Testing Packages
```xml
<!-- Core Testing -->
<PackageReference Include="xUnit" />
<PackageReference Include="Moq" />
<PackageReference Include="FluentAssertions" />
<PackageReference Include="Coverlet.collector" />

<!-- Blazor Testing -->
<PackageReference Include="bUnit" />

<!-- Data Testing -->
<PackageReference Include="Microsoft.EntityFrameworkCore.InMemory" />
<PackageReference Include="Bogus" />

```

### Test Naming Conventions
```csharp
// Unit Test Example
[Fact]
public async Task GetOrdersAsync_WithValidCustomerId_ReturnsOrderList()
{
    // Arrange
    var customerId = 123;
    
    // Act
    var result = await _service.GetOrdersAsync(customerId);
    
    // Assert
    result.Should().NotBeEmpty();
}
```

### Test Organization
```csharp
public class OrderServiceTests
{
    #region Setup
    private readonly IOrderService _service;
    
    public OrderServiceTests()
    {
        // Test setup
    }
    #endregion
    
    #region GetOrders Tests
    [Fact]
    public async Task GetOrders_ValidRequest_ReturnsOrders() { }
    #endregion
    
    #region CreateOrder Tests
    [Fact]
    public async Task CreateOrder_ValidData_CreatesOrder() { }
    #endregion
}
```

---

## Best Practices

### Test Development
- Write tests before or immediately after implementation
- Use descriptive test names explaining scenario and expectation
- Keep tests focused on single behavior
- Use test data builders for complex objects
- Avoid logic in tests - they should be simple

### Test Maintenance
- Update tests when requirements change
- Remove obsolete tests promptly
- Refactor tests alongside production code
- Keep test code DRY with helper methods
- Document complex test scenarios

### Performance
- Use in-memory databases for speed
- Parallelize test execution where possible
- Mock external dependencies
- Share expensive setup across tests
- Clean up resources properly

---

## Quality Assurance

### Test Coverage Requirements
- **Critical Business Logic**: 80%+ coverage
- **Data Access Layer**: Integration tests required
- **UI Components**: Key workflows tested with chrome-devtools
- **Error Paths**: At least one test per error scenario
- **Edge Cases**: Boundary conditions tested

### Test Review Checklist
- [ ] Tests follow AAA pattern
- [ ] Test names clearly describe scenario
- [ ] No hardcoded test data (use builders/generators)
- [ ] Tests are independent and deterministic
- [ ] Proper cleanup in teardown
- [ ] Appropriate use of mocking
- [ ] FluentAssertions used for readability
- [ ] Tests run quickly (< 1 second for unit tests)

---

## Examples

### Unit Test Example
```csharp
[Fact]
public async Task CalculateDiscount_PremiumCustomer_AppliesTwentyPercent()
{
    // Arrange
    var customer = new CustomerBuilder()
        .WithPremiumStatus()
        .Build();
    var orderAmount = 100m;
    
    // Act
    var discount = _calculator.CalculateDiscount(customer, orderAmount);
    
    // Assert
    discount.Should().Be(20m);
}
```

### Integration Test Example
```csharp
[Fact]
public async Task CreateOrder_ValidRequest_PersistsToDatabase()
{
    // Arrange
    using var scope = _factory.Services.CreateScope();
    var dbContext = scope.ServiceProvider.GetRequiredService<AppDbContext>();
    var orderData = new Faker<Order>()
        .RuleFor(o => o.CustomerName, f => f.Name.FullName())
        .Generate();
    
    // Act
    var response = await _client.PostAsJsonAsync("/api/orders", orderData);
    
    // Assert
    response.Should().BeSuccessful();
    var savedOrder = await dbContext.Orders.FirstOrDefaultAsync();
    savedOrder.Should().NotBeNull();
    savedOrder.CustomerName.Should().Be(orderData.CustomerName);
}
```
---

## Notes & Exceptions

### Special Considerations
- Minimum test implementation per YAGNI principle
- Focus on ROI - test where bugs are likely
- Integration tests often more valuable than unit tests for simple CRUD
- chrome-devtools tests only for critical user paths
- Consider maintenance cost when adding tests

### Framework-Specific Notes
- bUnit for Blazor component testing
- Use TestServer for API integration tests
- Leverage EF Core in-memory database for data layer tests
- chrome-devtools requires separate test server configuration

---

End of TestingConventions