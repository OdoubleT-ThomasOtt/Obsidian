# CodingConventions

## Purpose & Scope
Best practices for large-scale Blazor applications (.NET 6+/7+/8+), covering C# code, Razor components, folder structure, styling, testing, and performance. These conventions ensure consistent, maintainable, and scalable code across the entire eSource application.

---

## Core Principles

### Fundamental Rules
- **Single Responsibility**: One class per file, one responsibility per class
- **MVVM Pattern**: Strict separation of View, ViewModel, and ViewService
- **Dependency Injection**: Constructor injection preferred
- **Async/Await**: Always propagate async patterns with Async suffix
- **Nullability**: Enable nullable reference types (`<Nullable>enable</Nullable>`)
- **No Hardcoding**: Use constants and enums (SmartEnum) in CoreBusinessEnum project
- **Warning-Free**: Resolve all build warnings immediately

### Architecture Principles
- Entity Framework access only through CorePersistLayer
- ViewServices control all business logic for views
- Code-behind files delegate to ViewServices
- Repository pattern for data access abstraction

---

## Implementation Guidelines

### Project & Solution Structure

#### Solution Organization
- **Solution file** at root: `MyApp.sln`
- Each project uses **SDK-style** `.csproj`
- Namespace pattern: `ApplicationName.Directory.Structure` (e.g., `eSource.Core.CoreLayer`)
- Assembly naming: matches namespace pattern

#### Directory Structure
| Directory    | Subdirectory                                    | Description                                                                                                                    |
|--------------|-------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| **Core**     |                                                 | `Stores all core projects. Represented by a directory and solution folder.`                                                   |
|              | **CoreLayer**                                   | `General utilities, parsing, base classes`                                                                                    |
|              | **CoreLayerInterfaces**                         | `CoreLayer Interfaces`                                                                                                        |
|              | **CoreBusinessEnum**                            | `Constants and enumerations (SmartEnum)`                                                                                      |
|              | **CoreBusinessLayer**                           | `Reusable core business logic`                                                                                                |
|              | **CoreBusinessLayerInterfaces**                 | `CoreBusinessLayer Interfaces`                                                                                                |
|              | **CorePersistLayer**                            | `Database access using Entity Framework`                                                                                      |
|              | **CorePersistLayer/Repositories**               | `Repository implementations`                                                                                                  |
|              | **CorePersistLayerInterfaces**                  | `CorePersistLayer Interfaces`                                                                                                 |
|              | **CorePersistLayerInterfaces/Repositories**     | `Repository interfaces`                                                                                                       |
|              | **EntityFrameworkDataLayer**                    | `EF entities, context, and migrations`                                                                                        |
| **Frontend** |                                                 | `Stores all frontend projects. Represented by a directory and solution folder`                                                |
|              | **FrontendBusinessLayer**                       | `Frontend business logic`                                                                                                     |
|              | **FrontendBusinessLayer/Services/ViewServices** | `ViewServices controlling views`                                                                                              |
|              | **FrontendBusinessLayerInterfaces**             | `FrontendBusinessLayer Interfaces`                                                                                            |
|              | **FrontendModels**                              | `ViewModels for frontend`                                                                                                     |
|              | **Web**                                         | `Blazor Server application`                                                                                                   |
|              | **Web/IoC**                                     | `Autofac IoC definitions`                                                                                                     |
|              | **Web/Pages**                                   | `Razor pages and code-behind files`                                                                                           |

### MVVM Implementation Pattern

#### View (Razor Pages)
- Location: `/Frontend/Web/Pages/`
- Files: `.razor` and `.razor.cs` code-behind
- Responsibilities:
  - Presentation layer only (HTML, formatting)
  - Minimal business logic
  - Event delegation to ViewService
  - Single `_model` field in code-behind
  - StateHasChanged() calls
- Routing: `@attribute [Route("Route...")]`

#### ViewModels
- Location: `/Frontend/FrontendModels/`
- Responsibilities:
  - All UI state (IsLoading, ErrorMessage, etc.)
  - All form data
  - Validation logic
  - Helper methods for UI logic
  - No business logic or service calls

#### ViewServices
- Location: `/Frontend/FrontendBusinessLayer/Services/ViewServices/`
- Responsibilities:
  - All business logic
  - Backend service communication
  - State transformations
  - Async operations
  - Required `Init()` method for initialization

#### Anti-Patterns to Avoid
- Multiple individual fields in code-behind
- Direct service calls from code-behind
- Business logic in code-behind or ViewModels
- Cross-layer dependencies (Frontend → Repository)
- Mixing UI state and business state

### Razor Component Guidelines
- **Interactive Server Components** with streaming rendering
- Each component requires code-behind file
- No `@code` blocks in .razor files
- Events processed in code-behind, delegated to ViewService
- Directives at top: `@page`, `@inject`, `@using`

#### Component Parameters
```csharp
[Parameter] public int OrderId { get; set; }
[Parameter] public EventCallback<Order> OnSelected { get; set; }
```

### Data Access Pattern
- Entity Framework access **only** through CorePersistLayer
- Context usage restricted to CorePersistLayer
- All other projects use CorePersistLayer services
- Repository pattern for all data operations

---

## Standards & Specifications

### Naming Conventions

| Item                  | Convention               | Example                             |
|-----------------------|--------------------------|-------------------------------------|
| **Namespaces**        | PascalCase, match folder | `ApplicationName.Pages.Admin`       |
| **Classes / Structs** | PascalCase               | `OrderService`, `UserDto`           |
| **Interfaces**        | I… (PascalCase)          | `IOrderRepository`                  |
| **Methods**           | PascalCase, Async suffix | `GetOrdersAsync()`                  |
| **Properties**        | PascalCase               | `public int OrderId { get; set; }`  |
| **Fields**            | `_camelCase` (private)   | `private readonly ILogger _logger;` |
| **Constants**         | PascalCase               | `public const int MaxRetries = 5;`  |
| **Component Files**   | PascalCase.razor         | `OrderList.razor`                   |
| **Code-Behind Files** | PascalCase.razor.cs      | `OrderList.razor.cs`                |

### C# Code Style

#### Formatting
```csharp
public class Foo
{
    #region constructor
    
    public void Bar()
    {
        // one tab per indent
    }
    
    #endregion
}
```

#### Region Organization (in order, only if content exists). Between the content and the region has to be an empty line
1. `#region Usings` - using statements
2. `#region Event Definitions` - event definitions
3. `#region Consts` - constants
4. `#region Enums` - enumerations
5. `#region Fields` - private fields
6. `#region Dependency Injection` - public properties which are injected
7. `#region Properties` - public properties which are not injected
8. `#region Constructor` - constructors
9. `#region Lifecycle Methods` - events of the component
10. `#region Methods` - all methods
   - `#region Private` - private methods
   - `#region Protected` - protected methods
   - `#region Public` - public methods
11. `#region Interface Methods` - all methods implemented by an interface
12. `#region Events` - event handlers

### CSS & Styling
- **No CSS isolation** per component
- Use global styles for component-specific rules
- Follow existing Bootstrap 5 patterns
- BEM naming convention for custom styles

---

## Best Practices

### State Management
- Scoped services for UI state
- Never use static fields for mutable state
- Minimize re-render triggers

### Error Handling & Logging
- Centralize try/catch in services, not components
- Log at appropriate levels (Debug, Information, Warning, Error)
- Surface user-friendly messages in UI
- Use correlation IDs for tracking

### Performance
- Lazy loading where appropriate
- Minimize component re-renders
- Batch database operations
- Use caching strategically

### Security & Accessibility
- ARIA attributes where needed
- Alt attributes on all images
- Validate input on client AND server
- Encode outputs to prevent XSS
- Use Antiforgery protection
- HTTPS redirection and HSTS for production

### Documentation
- XML docs for public APIs:
```csharp
/// <summary>
/// Retrieves all orders for a given customer.
/// </summary>
Task<IEnumerable<Order>> GetOrdersAsync(int customerId);
```
- Inline comments only for complex logic

---

## Quality Assurance

### Code Review Checklist
- [ ] Single responsibility per class
- [ ] MVVM pattern correctly implemented
- [ ] No hardcoded values
- [ ] All warnings resolved
- [ ] Proper async/await usage
- [ ] Dependency injection used correctly
- [ ] Repository pattern for data access
- [ ] XML documentation for public APIs
- [ ] No business logic in views or ViewModels
- [ ] ViewService has Init() method
- [ ] Code-behind delegates to ViewService
- [ ] Constants/enums in CoreBusinessEnum
- [ ] SmartEnum used for enumerations
- [ ] Regions properly organized

### Validation Criteria
- Build produces zero warnings
- All public APIs documented

---

## Examples

### ViewService Implementation
```csharp
public class OrderViewService : IOrderViewService
{
    private readonly IOrderRepository _orderRepository;
    
    public OrderViewService(IOrderRepository orderRepository)
    {
        _orderRepository = orderRepository;
    }
    
    public async Task InitAsync(OrderViewModel model)
    {
        model.IsLoading = true;
        model.Orders = await _orderRepository.GetOrdersAsync();
        model.IsLoading = false;
    }
}
```

### Code-Behind Pattern
```csharp
public partial class OrderList : ComponentBase
{
    [Inject] private IOrderViewService ViewService { get; set; }
    
    private OrderViewModel _model = new();
    
    protected override async Task OnInitializedAsync()
    {
        await ViewService.InitAsync(_model);
    }
    
    private async Task HandleOrderSelected(Order order)
    {
        await ViewService.SelectOrderAsync(_model, order);
        StateHasChanged();
    }
}
```

---

## Notes & Exceptions

### Special Considerations
- File headers omitted in favor of XML documentation
- CSS isolation avoided for better global style management
- Interactive Server Components require SignalR consideration
- SmartEnum required for all enumerations (no standard enums)

### Framework-Specific Notes
- Blazor Server with .NET 8.0 specific patterns
- Entity Framework Core
- Autofac for advanced DI scenarios

---

## Validation Architecture

### Core Principle
**Server-side validation only** - No client-side validation to avoid duplicate messages.

### Implementation Rules

#### 1. ViewModels
- Inherit from `BaseEditViewModel`
- Implement validation in `Validate()` method
- **NO DataAnnotations attributes**

```csharp
public class TenderEditViewModel : BaseEditViewModel
{
    public override IEnumerable<ValidationResult> Validate(ValidationContext context)
    {
        if (string.IsNullOrWhiteSpace(Name))
            results.Add(new ValidationResult("Name is required", new[] { nameof(Name) }));
    }
}
```

#### 2. ViewServices
- Use `ValidationUtility.ValidateAndTransferErrors()`
- Return bool (true = success, false = validation failed)

```csharp
if (ValidationUtility.ValidateAndTransferErrors(model, model.ValidationErrors))
{
    model.ErrorMessage = "Please correct validation errors.";
    return false;
}
```

#### 3. Razor Components
- Use `EditContext` (not Model binding)
- Create `ValidationMessageStore` for server errors
- **NO** `<DataAnnotationsValidator />`
- Button with `type="button"` and `@onclick`

```csharp
// .razor.cs
_editContext = new EditContext(_model);
_messageStore = new ValidationMessageStore(_editContext);

// Transfer server errors after save attempt
foreach (var error in _model.ValidationErrors)
{
    _messageStore.Add(new FieldIdentifier(_model, error.Key), error.Value);
}
_editContext.NotifyValidationStateChanged();
```

```razor
@* .razor *@
<EditForm EditContext="_editContext">
    <InputText @bind-Value="_model.Name" />
    <ValidationMessage For="@(() => _model.Name)" />
    <button type="button" @onclick="HandleSaveAsync">Save</button>
</EditForm>
```

### Quick Checklist
✅ ViewModel extends BaseEditViewModel  
✅ Validation in Validate() method  
✅ ViewService uses ValidationUtility  
✅ EditContext binding (not Model)  
✅ No DataAnnotationsValidator  
✅ Server errors → ValidationMessageStore

**References**: See `/Frontend/Web/Components/Pages/Purchasing/Tenders/TenderDetailsPage.razor` for complete example

---

End of CodingConventions