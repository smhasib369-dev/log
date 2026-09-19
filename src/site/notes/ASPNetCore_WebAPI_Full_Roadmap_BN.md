---
{"dg-publish":true,"permalink":"/asp-net-core-web-api-full-roadmap-bn/","dg-note-properties":{}}
---

- **ASP.NET Core Web API — পূর্ণ roadmap ও nested mindmap**

  - **ভিত্তি:** .NET 10 LTS, ASP.NET Core 10 এবং EF Core 10; যাচাই: ১৯ সেপ্টেম্বর ২০২৬। [Official support policy](https://dotnet.microsoft.com/en-us/platform/support/policy/dotnet-core)
  - **পরিধি:** production HTTP API; prerequisites, framework, data, security, integration, testing, deployment এবং প্রয়োজনভিত্তিক specialization।
  - **পড়ার ক্রম:** phase ও chapter নম্বর ধরে; জানা topic-এর practical gate পারলে এগিয়ে যাবে। প্রথম API থেকেই ছোট tests; testing phase-এ বিস্তারিত কৌশল।
  - **Priority:** সাধারণ production API-তে ব্যবহার ও ভুলের প্রভাব ধরে আমার engineering judgment।
    - **অপরিহার্য:** core কাজ ও correctness-এর ভিত্তি।
    - **প্রয়োজনভিত্তিক:** project-এ লাগলে implementation শেখা।
    - **বিশেষায়িত:** role বা system-এর প্রয়োজন অনুযায়ী branch বাছাই।
  - **AI যুগে depth**
    - **গভীর:** নিজে execution ব্যাখ্যা, design, debug, failure predict ও AI code review।
    - **ব্যবহারিক:** docs/AI নিয়ে implement, modify ও test; result নিজে যাচাই।
    - **পরিচিতি:** কাজ, সীমা ও কখন লাগবে বোঝা; branch গ্রহণ করলে ব্যবহারিক/গভীর পর্যায়ে যাওয়া।
  - **Inheritance:** মূল topic-এর priority ও depth তার সব subtopic-এ প্রযোজ্য; আলাদা লেখা থাকলে সেটিই প্রযোজ্য।
  - **Trade-offs:** একই সিদ্ধান্তের লাভ, খরচ, সীমা ও alternative; যেখানে বাস্তব choice আছে সেখানে একাধিক trade-off।

1. **Foundation — ভাষা, HTTP ও development tools**

    - **01. Computer, network ও web foundations**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Computer ও runtime**
        - Process
        - Thread
        - Stack ও heap
        - Memory allocation
        - Filesystem ও permissions
        - Environment variables
      - **Network**
        - Client ও server
        - IP address
        - Port
        - Socket
        - DNS resolution
        - TCP connection
        - TLS handshake ও certificates
        - HTTP/1.1
        - HTTP/2
        - HTTP/3 — পরিচিতি
      - **Request journey**
        - Browser বা API client
        - DNS
        - CDN
        - Reverse proxy
        - Load balancer
        - Application server
        - Database ও downstream service
      - **Web boundaries**
        - URI ও URL
        - Origin: scheme, host, port
        - Same-origin policy
        - Cookies
        - Stateless request processing

      - **Trade-offs**
        - HTTP/1.1, HTTP/2 ও HTTP/3: transport ক্ষমতা আলাদা; server, proxy ও client support মিলিয়ে নির্বাচন।
        - Reverse proxy: TLS ও routing কেন্দ্রীয়ভাবে সামলায়; অতিরিক্ত hop এবং trusted-header configuration লাগে।
        - Stateless application instances: scale-out সহজ; প্রয়োজনীয় state database বা অন্য shared store-এ রাখতে হয়।

    - **[02. HTTP semantics ও request–response contract](https://httpwg.org/specs/rfc9110.html)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Request structure**
        - Method
        - Target path
        - Query string
        - Headers
        - Body
      - **Response structure**
        - Status code
        - Headers
        - Body
      - **Methods**
        - GET
        - HEAD
        - POST
        - PUT
        - PATCH
        - DELETE
        - OPTIONS
        - TRACE ও CONNECT — পরিচিতি
      - **Semantics**
        - Safe methods
        - Idempotent methods
        - Cacheability
        - Content negotiation
        - Redirect semantics
      - **Status codes**
        - 200, 201, 202, 204
        - 206 ও 416 — range requests
        - 301, 302, 303, 304, 307, 308
        - 400, 401, 403, 404, 405
        - 406, 409, 410, 412, 413, 415, 422, 429
        - 500, 502, 503, 504
      - **Headers**
        - Content-Type
        - Accept
        - Authorization
        - Location
        - Cache-Control
        - ETag
        - If-Match
        - If-None-Match
        - Retry-After
        - Vary
      - **Representations**
        - JSON
        - Form URL encoding
        - Multipart form data
        - Binary content
        - Streaming

      - **Trade-offs**
        - PUT ও PATCH: সম্পূর্ণ desired state পাঠানো সহজ contract দেয়; partial update কম payload দিলেও field ও concurrency rules বাড়ায়।
        - Offset pagination: page jump সহজ; বড় offset ব্যয়বহুল এবং concurrent changes-এ ফল সরে যেতে পারে।
        - Cursor pagination: বড় dataset-এ ধারাবাহিক traversal ভালো; arbitrary page jump ও cursor design কঠিন।
        - Synchronous response ও 202 job: তাৎক্ষণিক ফল সহজ; দীর্ঘ কাজে asynchronous job ভালো হলেও status tracking লাগে।

    - **[03. C# language foundations](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Program structure**
        - Statements ও expressions
        - Variables ও constants
        - Scope
        - Namespaces
        - using directives
        - Top-level statements
      - **Type system**
        - Value types
        - Reference types
        - Numeric types
        - bool ও char
        - string
        - object
        - var
        - Nullable value types
        - Nullable reference types
        - Type conversion
        - Boxing ও unboxing
      - **Operators ও control flow**
        - Arithmetic ও comparison
        - Logical ও short-circuit operators
        - Null-conditional operator
        - Null-coalescing operators
        - if ও switch
        - Pattern matching
        - for, foreach, while
        - break, continue, return
      - **Methods**
        - Parameters ও return values
        - Optional ও named arguments
        - Overloading
        - ref, out, in — ব্যবহারিক
        - params
      - **Data correctness**
        - decimal ও monetary precision
        - DateTime
        - DateTimeOffset
        - DateOnly ও TimeOnly
        - TimeSpan
        - Guid
        - Parsing ও TryParse
        - Culture-sensitive formatting

      - **Trade-offs**
        - decimal ও double: অর্থের দশমিক হিসাবের জন্য decimal উপযোগী; scientific calculation-এ range ও performance-এর চাহিদা ভিন্ন।
        - var ও explicit type: verbosity কমানো বনাম local readability; inferred type অস্পষ্ট হলে explicit type সহায়ক।
        - Nullable annotations: compile-time ভুল ধরতে সাহায্য করে; external input-এর runtime validation তবুও প্রয়োজন।

    - **04. OOP, composition ও C# type design**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Types**
        - Class
        - Struct
        - Record class
        - Record struct — ব্যবহারিক
        - Enum
        - Interface
        - Abstract class
      - **Members**
        - Fields
        - Properties
        - get ও set
        - init
        - required
        - Constructors
        - Primary constructors — ব্যবহারিক
        - Static members
        - Access modifiers
      - **Object behavior**
        - Encapsulation
        - Inheritance
        - Polymorphism
        - Method overriding
        - Method hiding
        - Composition
        - Equality ও identity
        - GetHashCode contract
        - Immutability
      - **Language tools**
        - Extension methods
        - Delegates
        - Lambda expressions
        - Closures
        - Func ও Action
        - Events — প্রয়োজনভিত্তিক; ব্যবহারিক
        - Attributes ও reflection — ব্যবহারিক

      - **Trade-offs**
        - Composition ও inheritance: composition-এ behavior বদলানো সহজ; inheritance-এ shared contract শক্ত হলেও coupling বাড়ে।
        - Record ও class: value-oriented DTO-তে record সুবিধাজনক; entity identity ও mutable lifecycle-এ class স্বাভাবিক হতে পারে।
        - Interface ও concrete class: boundary ও test substitution স্পষ্ট হয়; প্রতিটি class-এর জন্য interface বানালে অপ্রয়োজনীয় abstraction বাড়ে।
        - Immutability: accidental mutation কমে; পরিবর্তনে নতুন object ও mapping প্রয়োজন হতে পারে।

    - **05. Generics, collections ও LINQ**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Generics**
        - Generic types
        - Generic methods
        - Type constraints
        - Generic interfaces
        - Covariance ও contravariance — পরিচিতি
      - **Collections**
        - Array
        - `List<T>`
        - `Dictionary<TKey,TValue>`
        - `HashSet<T>`
        - `Queue<T>`
        - `Stack<T>`
        - `IReadOnlyCollection<T>`
        - Immutable collections — প্রয়োজনভিত্তিক
        - Concurrent collections — প্রয়োজনভিত্তিক
      - **Collection costs**
        - Lookup complexity
        - Insert ও removal cost
        - Enumeration cost
        - Memory overhead
      - **LINQ operations**
        - Where
        - Select
        - SelectMany
        - OrderBy ও ThenBy
        - GroupBy
        - Join ও GroupJoin
        - LeftJoin ও RightJoin — .NET 10; ব্যবহারিক
        - Any ও All
        - First ও FirstOrDefault
        - Single ও SingleOrDefault
        - Count ও aggregates
        - Distinct ও set operations
        - Skip ও Take
        - ToList ও ToDictionary
      - **Execution model**
        - `IEnumerable<T>`
        - `IQueryable<T>`
        - `IAsyncEnumerable<T>`
        - Deferred execution
        - Materialization
        - Multiple enumeration
        - Expression trees — ব্যবহারিক

      - **Trade-offs**
        - List ও Dictionary: ordered iteration সহজ বনাম দ্রুত key lookup; dictionary-তে hashing ও memory cost থাকে।
        - Deferred execution: query composition সম্ভব; execution time ও repeated enumeration ভুল বোঝার ঝুঁকি বাড়ে।
        - IQueryable ও IEnumerable: provider SQL তৈরি করতে পারে বনাম in-memory execution; boundary বদলালে performance বদলায়।
        - LINQ ও explicit loop: expressive query বনাম allocation ও hot-path control; profiling অনুযায়ী নির্বাচন।

    - **06. Async, exceptions, cancellation ও resource lifetime**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Async foundations**
        - Task
        - `Task<T>`
        - async
        - await
        - I/O-bound কাজ
        - CPU-bound কাজ
        - Async all the way
        - Task.WhenAll
        - Task.WhenAny
        - async void সীমা
        - .Result ও .Wait সমস্যা
      - **Cancellation**
        - CancellationToken
        - CancellationTokenSource
        - Linked tokens
        - Timeouts
        - Cooperative cancellation
        - Cancellation propagation
      - **Exceptions**
        - try, catch, finally
        - throw ও rethrow
        - Exception filters
        - Custom exceptions
        - Async exception propagation
        - Expected failure ও unexpected exception
      - **Resources**
        - IDisposable
        - using
        - IAsyncDisposable
        - await using
        - Stream lifetime
      - **Concurrency**
        - Race conditions
        - Shared mutable state
        - lock
        - SemaphoreSlim
        - Bounded concurrency
        - Thread-pool starvation
      - **Advanced — প্রয়োজনভিত্তিক; পরিচিতি**
        - ValueTask
        - SynchronizationContext
        - ConfigureAwait
        - Channels

      - **Trade-offs**
        - Async I/O: অপেক্ষার সময় thread আটকে থাকে না; cancellation ও failure flow সঠিকভাবে propagate করতে হয়।
        - Task.WhenAll: independent কাজের latency কমতে পারে; unbounded fan-out downstream service ও database overload করে।
        - Task.Run: CPU কাজ অন্য thread-এ চালায়; API-তে blocking I/O-কে এভাবে ঢাকলে বাড়তি thread-pool চাপ পড়ে।
        - Exceptions ও Result-style failure: unexpected failure propagation সহজ বনাম explicit business outcomes; mixed convention review কঠিন করে।

    - **07. .NET SDK, project structure, Git ও developer workflow**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **.NET platform**
        - SDK
        - Runtime
        - CLR
        - BCL
        - ASP.NET Core shared framework
        - Target framework
        - NuGet packages
      - **Project files**
        - .csproj
        - PackageReference
        - ProjectReference
        - .slnx
        - .sln compatibility
        - Solution folders ও filesystem folders
        - global.json
        - Directory.Build.props
        - Directory.Packages.props — প্রয়োজনভিত্তিক
      - **CLI**
        - dotnet new
        - dotnet restore
        - dotnet build
        - dotnet run
        - dotnet watch
        - dotnet test
        - dotnet publish
        - Package ও tool management
      - **Editor**
        - VS Code বা Visual Studio
        - Breakpoints
        - Step into ও step over
        - Watch ও call stack
        - HTTP request files
        - curl বা API client
      - **Git**
        - Working tree, staging, commits
        - Branches
        - Merge ও rebase
        - Conflict resolution
        - Revert ও reset
        - Pull request review
        - .gitignore
        - Secret-free commits
      - **Quality**
        - .editorconfig
        - Formatting
        - Analyzers
        - Build warnings
        - Dependency version review
        - Transitive dependencies
        - packages.lock.json ও locked restore

      - **Trade-offs**
        - এক project ও multiple projects: শুরুতে navigation সহজ; আলাদা projects dependency boundaries enforce করে কিন্তু build/configuration বাড়ায়।
        - SDK pinning: team ও CI-তে reproducibility; নিয়মিত patch/update management লাগে।
        - Package adoption: implementation সময় কমে; compatibility, maintenance ও license যাচাইয়ের দায়িত্ব যোগ হয়।

    - **Practical gate**
      - ছোট C# program, HTTP request ব্যাখ্যা এবং Git-এ reproducible project তৈরি।

2. **ASP.NET Core platform — startup থেকে endpoint**

    - **[08. Host, Kestrel ও application lifecycle](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Hosting model**
        - Generic Host
        - WebApplicationBuilder
        - WebApplication
        - Program.cs
        - Minimal hosting ও Minimal APIs-এর পার্থক্য
      - **Startup sequence**
        - CreateBuilder
        - Service registration
        - Build
        - Middleware registration
        - Endpoint registration
        - Run ও RunAsync
      - **Kestrel**
        - Listening addresses
        - Ports
        - HTTP endpoints
        - HTTPS endpoints
        - Development certificate
        - HTTP protocol configuration
        - Connection limits
      - **Hosting topology**
        - Direct Kestrel
        - Reverse proxy
        - IIS in-process
        - IIS out-of-process
        - HTTP.sys — Windows-specific; বিশেষায়িত; পরিচিতি
        - Linux process hosting
      - **Lifetime**
        - Startup failures
        - ApplicationStarted
        - ApplicationStopping
        - ApplicationStopped
        - Graceful shutdown
        - Shutdown timeout
      - **Compatibility — প্রয়োজনভিত্তিক; পরিচিতি**
        - Startup.cs pattern
        - Older hosting APIs

      - **Trade-offs**
        - Direct Kestrel ও reverse proxy: সরল deployment বনাম centralized TLS/routing; proxy trust ও forwarded headers configure করতে হয়।
        - Graceful shutdown: চলমান request শেষ করার সুযোগ; deployment-এর termination deadline-এর মধ্যে কাজ শেষ করতে হয়।
        - Framework-dependent ও self-contained publish: ছোট artifact বনাম runtime bundling; runtime patching-এর দায়িত্ব বদলায়।

    - **[09. Dependency Injection ও service lifetimes](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Concepts**
        - Dependency
        - Inversion of Control
        - Dependency Inversion Principle
        - Composition root
        - Explicit dependencies
      - **Container**
        - IServiceCollection
        - ServiceDescriptor — ব্যবহারিক
        - IServiceProvider
        - Registration ও resolution
        - Constructor injection
        - Factory registration
        - Instance registration
      - **Lifetimes**
        - Transient
        - Scoped
        - Singleton
        - Request scope
        - Explicit scope
        - IServiceScopeFactory
        - CreateAsyncScope
      - **Correctness**
        - Captive dependency
        - Scope validation
        - Singleton thread safety
        - Disposal ownership
        - Circular dependency
        - BuildServiceProvider misuse
        - Service locator trade-off
      - **Additional patterns — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Multiple implementations
        - `IEnumerable<T>` resolution
        - Open generic registration
        - Keyed services
        - TryAdd registrations
        - Decorator registration

      - **Trade-offs**
        - Transient, scoped ও singleton: creation cost, isolation ও shared-state safety-এর ভারসাম্য; lifetime performance-only সিদ্ধান্ত নয়।
        - Constructor injection ও service locator: dependencies স্পষ্ট থাকে বনাম dynamic lookup; locator dependency review কঠিন করে।
        - Built-in container ও external container: কম dependency বনাম অতিরিক্ত features; দ্বিতীয় container complexity ও lifetime integration বাড়ায়।
        - Keyed services: একই contract-এর implementation বাছাই সহজ; অতিরিক্ত keys business logic-এ ছড়িয়ে পড়তে পারে।

    - **[10. Configuration, environments, secrets ও Options](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Configuration sources**
        - appsettings.json
        - appsettings.{Environment}.json
        - Environment variables
        - Command-line arguments
        - User Secrets
        - External secret store
        - Provider precedence
        - Hierarchical keys ও double underscore
      - **Environments**
        - Development
        - Staging
        - Production
        - DOTNET_ENVIRONMENT
        - ASPNETCORE_ENVIRONMENT
        - Hosting-model-dependent environment precedence
        - launchSettings.json-এর local scope
      - **Options**
        - Strongly typed binding
        - `IOptions<T>`
        - `IOptionsSnapshot<T>`
        - `IOptionsMonitor<T>`
        - Named options
        - Configure ও PostConfigure
        - Options validation
        - ValidateOnStart
        - Reload behavior ও provider support
      - **Secrets**
        - Local ও production separation
        - Connection strings
        - Secret rotation
        - Managed identity — প্রয়োজনভিত্তিক
        - Redaction

      - **Trade-offs**
        - IOptions, Snapshot ও Monitor: স্থির configuration, request-scoped refresh ও change notification—lifetime ও consistency চাহিদা অনুযায়ী নির্বাচন।
        - Fail-fast validation: ভুল configuration startup-এ ধরা পড়ে; deployment-এ dependency/config readiness নিশ্চিত করতে হয়।
        - Environment variables ও secret store: সহজ deployment বনাম centralized rotation/access control; secret-store availability ও integration cost থাকে।
        - Live reload: restart ছাড়াই পরিবর্তন; in-flight operation একই configuration দেখবে কি না তা নির্ধারণ করতে হয়।

    - **[11. HttpContext, request body ও response lifecycle](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/use-http-context?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **HttpContext**
        - Request
        - Response
        - User
        - Items
        - RequestServices
        - RequestAborted
        - TraceIdentifier
        - Connection
        - Features — পরিচিতি
      - **Request**
        - Method
        - Scheme
        - Host
        - Path
        - PathBase
        - QueryString
        - Query
        - RouteValues
        - Headers
        - Cookies
        - Body
        - ReadFormAsync
      - **Body processing**
        - Forward-only stream
        - EnableBuffering
        - Rewind position
        - Buffer thresholds ও size limits
        - Stream disposal ownership
        - BodyReader — প্রয়োজনভিত্তিক; পরিচিতি
      - **Response**
        - StatusCode
        - ContentType
        - Headers
        - Cookies
        - Body
        - HasStarted
        - OnStarting
        - OnCompleted — প্রয়োজনভিত্তিক; পরিচিতি
      - **Context safety**
        - Request lifetime
        - Thread safety
        - IHttpContextAccessor
        - Background কাজের জন্য প্রয়োজনীয় data copy

      - **Trade-offs**
        - Body buffering: পুনরায় পড়া সম্ভব; memory/disk ব্যবহার, payload limit ও rewind সামলাতে হয়।
        - Streaming: বড় response-এ memory কম লাগে; partial response শুরু হলে error contract বদলানো কঠিন।
        - HttpContextAccessor: গভীর layer থেকে context পাওয়া সহজ; HTTP coupling ও implicit dependency বাড়ে।
        - Items: request-local data ভাগ করা সহজ; typed contract না রাখলে key collision ও hidden dependency বাড়ে।

    - **[12. Middleware — pipeline, branching ও custom components](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Prerequisite connection**
        - HTTP request ও response
        - Delegates ও lambdas
        - async ও await
        - DI lifetimes
      - **Pipeline**
        - RequestDelegate
        - Before next
        - await next
        - After next
        - Forward execution
        - Reverse-order unwinding
        - Short-circuiting
        - Terminal middleware
      - **Registration — ব্যবহারিক**
        - app.Use
        - next() overload
        - next(context) overload
        - app.Run(handler)
        - app.Run()
      - **Branches — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Map
          - Path matching
          - Path ও PathBase
          - Nested branches — পরিচিতি
        - MapWhen
          - Predicate
          - `Func<HttpContext, bool>`
          - Separate pipeline
        - UseWhen
          - Predicate
          - Rejoin conditions
          - Short-circuit behavior
      - **Custom middleware — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Built-in feature selection
        - Inline middleware
        - Convention-based class
        - Public constructor ও RequestDelegate
        - Invoke ও InvokeAsync
        - HttpContext parameter ও Task return
        - `UseMiddleware<T>`
        - Registration extension method
      - **Dependency safety — গভীর**
        - App-lifetime construction
        - Constructor injection
        - Method injection of scoped services
        - Shared mutable state
      - **Factory activation — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - IMiddleware
        - Per-request activation
        - Scoped বা transient registration
        - Scoped constructor dependencies
        - IMiddlewareFactory — বিশেষায়িত; পরিচিতি
        - Create ও Release — পরিচিতি
        - Explicit argument limitation
      - **Ordering ও failures**
        - Exception handling placement
        - Routing ও endpoint execution
        - CORS, authentication ও authorization order
        - Automatically added middleware
        - Response.HasStarted
        - Cancellation ও cleanup
      - **Verification**
        - Execution-order tracing
        - Request-duration logging
        - Conditional rejection
        - Branch ও rejoin tests
        - Middleware integration testing

      - **Trade-offs**
        - Built-in ও custom middleware: maintenance কমানো বনাম বিশেষ behavior; custom code-এর ordering, security ও tests নিজের দায়িত্ব।
        - Inline ও class: ছোট logic দ্রুত লেখা বনাম reusable component; class extraction navigation ও configuration বাড়ায়।
        - Conventional ও IMiddleware: app-lifetime instance বনাম request activation; scoped injection-এর পদ্ধতি ও allocation profile বদলায়।
        - MapWhen ও UseWhen: isolated branch বনাম conditional rejoin; common processing কোথায় হবে তা স্পষ্ট করতে হয়।
        - Short-circuit: অপ্রয়োজনীয় downstream কাজ বাঁচে; প্রয়োজনীয় logging/security/headers বাদ পড়ছে কি না যাচাই দরকার।

    - **[13. Routing, endpoints ও link generation](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Endpoint routing**
        - Route matching
        - Endpoint selection
        - Endpoint metadata
        - UseRouting
        - Endpoint execution
        - GetEndpoint
      - **Route templates**
        - Literal segments
        - Route parameters
        - Optional parameters
        - Default values
        - Route constraints
        - Catch-all parameters
        - Multiple routes
        - Ambiguous matches
        - Route precedence
      - **Controller routing**
        - Attribute routing
        - Controller ও action route combination
        - HTTP method attributes
        - Token replacement
        - Conventional routing — পরিচিতি
      - **Minimal API routing**
        - MapGet, MapPost, MapPut, MapPatch, MapDelete
        - MapMethods
        - MapGroup
        - Group metadata
        - Named endpoints
      - **Link generation**
        - LinkGenerator
        - CreatedAtAction
        - CreatedAtRoute
        - URL encoding
      - **Boundaries**
        - Route constraint ও input validation
        - Middleware Map ও endpoint Map methods
        - 404 ও 405 behavior

      - **Trade-offs**
        - Attribute routes ও route groups: route endpoint-এর কাছে থাকে বনাম shared prefix/metadata; অতিরিক্ত grouping discoverability কমাতে পারে।
        - Constraints: ambiguous route আলাদা করে; validation হিসেবে ব্যবহার করলে intended 400-এর বদলে 404 আসতে পারে।
        - Named link generation: hard-coded URL কমে; endpoint names ও route values maintain করতে হয়।

    - **Practical gate**
      - একটি API-তে startup, DI, middleware order ও route matching নিজে trace করা।

3. **API implementation — endpoints, contracts ও errors**

    - **[14. Controllers ও action results](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Controller setup**
        - AddControllers
        - MapControllers
        - ControllerBase
        - Controller ও ControllerBase-এর পার্থক্য
        - ApiController attribute
        - Constructor injection
      - **Actions**
        - Public action methods
        - NonAction
        - Attribute routing
        - HTTP method attributes
        - Action parameters
        - CancellationToken
      - **Return types**
        - Specific DTO type
        - IActionResult
        - `ActionResult<T>`
        - Task<`ActionResult<T>`>
        - `IAsyncEnumerable<T>` — প্রয়োজনভিত্তিক
      - **Response helpers**
        - Ok
        - Created
        - CreatedAtAction
        - CreatedAtRoute
        - Accepted
        - NoContent
        - BadRequest
        - Unauthorized
        - Forbid
        - NotFound
        - Conflict
        - Problem
        - ValidationProblem
        - File
      - **Metadata**
        - Produces
        - Consumes
        - ProducesResponseType
      - **Controller boundaries**
        - Thin action methods
        - Service delegation
        - HTTP-to-application mapping

      - **Trade-offs**
        - Controllers: conventions, filters ও established structure পাওয়া যায়; বেশি ceremony এবং MVC-specific pipeline শেখা লাগে।
        - `ActionResult<T>` ও IActionResult: typed success contract বনাম flexible results; documentation ও client generation-এ explicit response types সহায়ক।
        - Thin controller: transport ও business logic আলাদা হয়; অতিরিক্ত pass-through service বানালে navigation বাড়ে।

    - **[15. Minimal APIs ও endpoint organization](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Route handlers**
        - Lambda handler
        - Method-group handler
        - Async handler
        - DI parameters
        - CancellationToken
        - HttpContext parameter
      - **Endpoint registration**
        - MapGet
        - MapPost
        - MapPut
        - MapPatch
        - MapDelete
        - MapMethods
        - MapGroup
      - **Response types**
        - IResult
        - Results helpers
        - TypedResults
        - `Results<T1,T2,...>`
        - JSON responses
        - File ও stream responses
      - **Metadata ও organization**
        - WithName
        - WithTags
        - Produces metadata
        - RequireAuthorization
        - Endpoint extension methods
        - Feature folders
        - Group-level conventions
      - **Parameter binding**
        - Inferred sources
        - Explicit sources
        - AsParameters
        - TryParse
        - BindAsync — প্রয়োজনভিত্তিক
      - **Validation ও filters**
        - .NET 10 built-in validation
        - AddValidation
        - Endpoint-level validation configuration
        - DisableValidation
        - Validation type discovery ও assembly boundary
        - Endpoint filters
        - MVC pipeline থেকে পার্থক্য

      - **Trade-offs**
        - Minimal APIs: কম ceremony ও explicit endpoint composition; বড় application-এ grouping ও feature organization সচেতনভাবে করতে হয়।
        - Controllers ও Minimal APIs: team convention, filters, binding needs ও AOT target অনুযায়ী নির্বাচন; project বড় হওয়া একমাত্র মাপকাঠি নয়।
        - TypedResults ও IResult: stronger response metadata বনাম flexible return type; multiple-result signatures বড় হতে পারে।
        - Lambda ও extracted handler: local readability বনাম reuse/test navigation; Program.cs বড় হলে extraction সহায়ক।

    - **[16. Models, DTOs ও model binding](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Model roles**
        - Request DTO
        - Response DTO
        - Domain model
        - Persistence entity
        - View model — পরিচিতি
      - **Contract shape**
        - Create request
        - Update request
        - Partial update request
        - List item response
        - Detail response
        - Nullable ও omitted fields
        - required ও runtime requirements
      - **Binding sources**
        - FromRoute
        - FromQuery
        - FromBody
        - FromForm
        - FromHeader
        - FromServices
        - FromKeyedServices — প্রয়োজনভিত্তিক
      - **Controller binding**
        - ApiController source inference
        - Simple types
        - Complex types
        - Collections ও dictionaries
        - Prefix matching
        - Missing values
        - Conversion errors
        - ModelState
        - Body input formatter
        - Single-body consumption
      - **Minimal API binding**
        - Source inference rules
        - Service inference
        - AsParameters
        - `IParsable<T>` বা TryParse
        - BindAsync ও custom binding — প্রয়োজনভিত্তিক
      - **Customization — বিশেষায়িত; পরিচিতি**
        - IModelBinder
        - IModelBinderProvider
        - Value providers

      - **Trade-offs**
        - Entity expose করা ও DTO: কম mapping বনাম stable external contract; DTO overposting ও data leakage নিয়ন্ত্রণে সাহায্য করে।
        - এক DTO reuse ও operation-specific DTO: কম types বনাম আলাদা create/update rules; reuse অপ্রাসঙ্গিক nullable fields বাড়াতে পারে।
        - Inferred ও explicit binding: কম attributes বনাম স্পষ্ট contract; ambiguous বা security-sensitive input-এ explicit source সহায়ক।
        - Custom binder: repeated parsing কেন্দ্রীভূত হয়; framework coupling ও debugging effort বাড়ে।

    - **[17. JSON serialization, formatters ও partial updates](https://learn.microsoft.com/en-us/aspnet/core/web-api/jsonpatch?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **[System.Text.Json](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/overview)**
        - Serialization
        - Deserialization
        - JsonSerializerOptions
        - Property naming policy
        - PropertyNameCaseInsensitive
        - JsonPropertyName
        - JsonIgnore
        - Null handling
        - Enum representation
        - Number handling
        - Date/time representation
        - Required-member handling
        - MaxDepth
        - Reference cycles
        - Polymorphism configuration
        - Custom converters — প্রয়োজনভিত্তিক
        - Source generation — প্রয়োজনভিত্তিক
      - **JSON configuration boundaries**
        - MVC JsonOptions
        - Minimal API HttpJsonOptions
        - HttpClient serializer options
      - **Formatting**
        - Input formatters
        - Output formatters
        - Content negotiation
        - Accept ও Content-Type
        - 406 ও 415
        - XML support — বিশেষায়িত; পরিচিতি
      - **Partial updates — প্রয়োজনভিত্তিক; গভীর**
        - Omitted field ও explicit null
        - Operation-specific patch DTO
        - JSON Patch
        - add, remove, replace
        - move, copy, test
        - System.Text.Json-based patch package in .NET 10
        - Allowed paths ও operations
        - Validation after patch
        - Concurrency protection

      - **Trade-offs**
        - System.Text.Json ও Newtonsoft.Json: framework alignment ও source-generation সুবিধা বনাম legacy feature compatibility; migration behavior যাচাই প্রয়োজন।
        - String enums ও numeric enums: readability বনাম payload size; rename ও নতুন values-এর compatibility ভাবতে হয়।
        - JSON Patch: flexible partial update; allowed operations, field authorization ও malicious payload সীমা আলাদা করে enforce করতে হয়।
        - Reference preservation ও explicit DTO projection: graph স্বয়ংক্রিয়ভাবে serialize করা বনাম সহজ public contract; persistence graph সরাসরি প্রকাশে coupling বাড়ে।

    - **[18. Validation, mapping ও business invariants](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Validation layers**
        - Parsing failure
        - Shape ও field validation
        - Cross-field validation
        - Business rules
        - Authorization rules
        - Database constraints
      - **Data annotations**
        - Required
        - Range
        - StringLength
        - MinLength ও MaxLength
        - RegularExpression
        - EmailAddress
        - Compare
        - Custom ValidationAttribute
        - IValidatableObject
      - **Framework behavior**
        - Controller ModelState
        - ApiController automatic 400
        - ValidationProblemDetails
        - Nullable reference type inference
        - Minimal API validation registration in .NET 10
        - [Microsoft.Extensions.Validation in .NET 10](https://learn.microsoft.com/en-us/aspnet/core/release-notes/aspnetcore-10.0?view=aspnetcore-10.0#validation-apis-moved-to-microsoftextensionsvalidation)
        - Framework-specific behavior differences
      - **[FluentValidation](https://docs.fluentvalidation.net/en/latest/aspnet.html) — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - `AbstractValidator<T>`
        - RuleFor
        - Conditional rules
        - Nested validators
        - Collections
        - Async rules
        - Explicit ValidateAsync
        - Legacy MVC automatic-validation limitations
      - **Mapping**
        - Manual mapping
        - Extension method mapping
        - Query projection
        - Mapping library selection — প্রয়োজনভিত্তিক
        - Null ও collection mapping
        - Mapping tests
      - **Invariants**
        - Race-safe uniqueness
        - Domain state transitions
        - Database enforcement

      - **Trade-offs**
        - Data annotations ও external validators: ছোট rules কাছে রাখা বনাম complex rules আলাদা রাখা; দ্বিতীয়টিতে registration ও execution flow বাড়ে।
        - Database pre-check ও unique constraint: friendly error-এর জন্য pre-check সহায়ক; concurrent requests সামলাতে database constraint প্রয়োজন।
        - Manual mapping ও mapping library: explicit review ও debugging বনাম boilerplate কমানো; convention, license ও hidden transformations যাচাই করতে হয়।
        - Fail-fast ও aggregated errors: দ্রুত failure বনাম client-এর একবারে সব সংশোধন; rule dependencies ও resource cost বিবেচ্য।

    - **[19. MVC filters ও endpoint filters](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **MVC filter pipeline**
        - Authorization filters
        - Resource filters
        - Action filters
        - Exception filters
        - Result filters
        - Always-run result filters — পরিচিতি
      - **Filter mechanics**
        - Synchronous filters
        - Asynchronous filters
        - Before ও after execution
        - Short-circuiting
        - Global scope
        - Controller scope
        - Action scope
        - Order
        - Attribute-based registration
        - DI registration
        - ServiceFilter
        - TypeFilter
      - **Endpoint filters**
        - IEndpointFilter
        - EndpointFilterInvocationContext
        - Arguments
        - next
        - Result inspection
        - Group filters
        - Filter factories — পরিচিতি
      - **Boundaries**
        - Middleware coverage
        - MVC-specific coverage
        - Endpoint-specific coverage
        - Exception-filter limitations
        - Authorization policy preference

      - **Trade-offs**
        - Middleware ও filters: pipeline-wide behavior বনাম action/handler context; প্রয়োজনের চেয়ে বড় scope side effects বাড়ায়।
        - Global ও local filters: consistent rules বনাম endpoint-specific control; global filter-এর exceptions maintain করতে হয়।
        - Attribute ও DI filter: declaration কাছে রাখা বনাম dependency-managed implementation; attribute construction ও lifetime rules বুঝতে হয়।

    - **20. REST API design ও contract evolution**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Design foundations**
        - Resources
        - Representations
        - Uniform interface
        - Statelessness
        - Cacheability
        - Layered system
        - Hypermedia — বিশেষায়িত; পরিচিতি
      - **Resource modeling**
        - Collection ও item endpoints
        - Resource naming
        - Nested resource boundaries
        - Action-oriented operations
        - Public identifiers
      - **Read contracts**
        - Filtering
        - Sorting
        - Projection
        - Pagination
        - Stable ordering
        - Maximum page size
        - Search semantics
      - **Write contracts**
        - Create ও Location
        - Update ও replace
        - Partial update
        - Delete semantics
        - Bulk operations
        - Idempotency keys
        - ETag ও If-Match
        - Conflict handling
      - **Long-running operations**
        - 202 Accepted
        - Job identifier
        - Status endpoint
        - Polling intervals
      - **Compatibility**
        - Additive changes
        - Breaking changes
        - Enum evolution
        - Nullability changes
        - Deprecation ও migration window

      - **Trade-offs**
        - Resource-oriented ও action endpoints: uniform contract বনাম স্পষ্ট business command; domain operation জোর করে CRUD বানালে অর্থ হারায়।
        - Response envelope: uniform metadata সুবিধা; HTTP status ও ProblemDetails-এর ওপর অতিরিক্ত wrapper client complexity বাড়াতে পারে।
        - Bulk endpoint: কম network round trips; partial failure, authorization ও transaction scope জটিল হয়।
        - Idempotency key: retry-safe business operation; key retention, request fingerprint ও atomic result storage লাগে।

    - **[21. Exception handling ও standard error contract](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/error-handling?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Failure categories**
        - Binding error
        - Validation error
        - Business conflict
        - Authentication failure
        - Authorization failure
        - Missing resource
        - Dependency failure
        - Unexpected exception
      - **Error pipeline**
        - Developer exception page
        - UseExceptionHandler
        - IExceptionHandler
        - Handler registration order
        - AddProblemDetails
        - IProblemDetailsService
        - Status code pages
        - Already-started response
        - Cancellation handling
      - **[Problem Details](https://www.rfc-editor.org/rfc/rfc9457)**
        - application/problem+json
        - type
        - title
        - status
        - detail
        - instance
        - Extension members
        - Stable error code
        - Trace identifier
        - ValidationProblemDetails
      - **Diagnostics**
        - Log once
        - Stack trace preservation
        - Sensitive-data redaction
        - Handled-exception diagnostics in .NET 10
        - Client-safe message

      - **Trade-offs**
        - Central handler: consistent errors ও কম duplication; local domain context সঠিকভাবে handler পর্যন্ত নিতে হয়।
        - Exceptions ও explicit failure results: unexpected failure propagation বনাম predictable business outcomes; mapping convention স্থির রাখতে হয়।
        - Detailed error ও minimal error: debugging সুবিধা বনাম information exposure; client message ও internal diagnostics আলাদা রাখার প্রয়োজন।
        - 400 ও 422 validation policy: framework default-এর সরলতা বনাম semantic distinction; contract consistency ও client expectations গুরুত্বপূর্ণ।

    - **[22. OpenAPI, API documentation, versioning ও clients](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/openapi/overview?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **OpenAPI foundations**
        - Specification ও document
        - Paths ও operations
        - Parameters
        - Request bodies
        - Responses
        - Schemas
        - Security schemes
        - Operation IDs
        - Examples
        - XML documentation comments
      - **ASP.NET Core OpenAPI**
        - AddOpenApi
        - MapOpenApi
        - Document generation
        - Build-time generation
        - Document transformers
        - Operation transformers
        - Schema transformers
        - Multiple documents
        - [.NET 10 OpenAPI 3.1 support](https://learn.microsoft.com/en-us/aspnet/core/release-notes/aspnetcore-10.0?view=aspnetcore-10.0#openapi-31-support)
      - **Documentation UI**
        - Swagger UI
        - Scalar
        - UI ও OpenAPI specification-এর পার্থক্য
        - Production exposure policy
      - **[API versioning](https://github.com/dotnet/aspnet-api-versioning/wiki) — প্রয়োজনভিত্তিক**
        - URL-segment versioning
        - Query-string versioning
        - Header versioning
        - Media-type versioning
        - Asp.Versioning integration
        - Default version policy
        - Supported/deprecated version reporting
        - Unsupported-version response
        - Versioned API Explorer
        - Deprecation
        - Backward-compatible rollout
      - **Clients**
        - Generated SDK
        - Handwritten client
        - Schema drift detection
        - Contract compatibility checks

      - **Trade-offs**
        - Built-in OpenAPI ও third-party generation: framework integration বনাম অতিরিক্ত ecosystem features; plugins ও migration compatibility যাচাই প্রয়োজন।
        - URL ও header versioning: discoverability/caching সরলতা বনাম URI স্থির রাখা; tooling ও consumer support ভিন্ন হতে পারে।
        - Generated ও handwritten clients: contract consistency ও কম boilerplate বনাম custom behavior; generated diff ও compatibility review লাগে।
        - Public interactive docs: onboarding সহজ; production access ও sensitive examples নিয়ন্ত্রণ করতে হয়।

    - **Practical gate**
      - DTO, validation, ProblemDetails ও OpenAPI-সহ একটি CRUD API; success এবং failure paths যাচাই।

4. **Data — SQL, EF Core ও persistence correctness**

    - **23. Relational modeling ও SQL foundations**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Relational concepts**
        - Database
        - Schema
        - Table
        - Row ও column
        - Primary key
        - Foreign key
        - Alternate key
        - Composite key
        - Unique constraint
        - Check constraint
        - Default constraint
        - NOT NULL
      - **Data types**
        - Integer
        - Decimal precision ও scale
        - Text ও Unicode
        - Date/time
        - UUID বা uniqueidentifier
        - Binary
        - JSON columns — প্রয়োজনভিত্তিক
        - Provider-specific types
      - **Relationships**
        - One-to-one
        - One-to-many
        - Many-to-many
        - Junction table
        - Optional ও required relationships
        - Referential integrity
        - Cascade delete
        - Restrict ও set-null behavior
      - **Model quality**
        - First normal form
        - Second normal form
        - Third normal form
        - Denormalization
        - Natural ও surrogate keys
        - Soft-delete data model
        - Audit fields
        - Time-zone policy
        - Money ও currency representation

      - **Trade-offs**
        - Normalization ও denormalization: update consistency বনাম read simplicity; duplicated data synchronization বাড়ায়।
        - Integer ও UUID keys: compact indexes বনাম independent ID generation; distribution, index behavior ও public-ID exposure বিবেচ্য।
        - Cascade delete ও explicit delete: automatic integrity বনাম deletion control; বড় graph-এ accidental data loss এড়ানোর design দরকার।
        - Soft ও hard delete: recovery/history বনাম storage, uniqueness ও query-filter complexity।

    - **24. SQL querying, indexes ও transactions**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **SQL operations**
        - CREATE, ALTER, DROP
        - INSERT
        - SELECT
        - UPDATE
        - DELETE
        - Parameterized statements
      - **Query composition**
        - WHERE
        - ORDER BY
        - DISTINCT
        - INNER JOIN
        - LEFT JOIN
        - RIGHT ও FULL JOIN — প্রয়োজনভিত্তিক
        - CROSS JOIN
        - GROUP BY
        - HAVING
        - Aggregates
        - Subqueries
        - EXISTS
        - CTEs
        - Window functions — প্রয়োজনভিত্তিক
        - Views
      - **Indexes**
        - B-tree concepts
        - Clustered ও nonclustered — provider-specific
        - Composite index ও column order
        - Covering index
        - Filtered বা partial index
        - Index selectivity
        - Sargability
        - Query execution plan
      - **Transactions**
        - ACID
        - Commit ও rollback
        - Isolation levels
        - Dirty reads
        - Non-repeatable reads
        - Phantom reads
        - Locking
        - MVCC — provider-specific
        - Deadlocks
        - Optimistic concurrency
        - Pessimistic concurrency

      - **Trade-offs**
        - Index যোগ: targeted reads দ্রুত হয়; writes, storage ও maintenance cost বাড়ে।
        - Higher isolation: anomalies কমে; blocking, retries বা version-storage cost বাড়তে পারে।
        - Offset ও keyset query: page numbering সহজ বনাম efficient stable traversal; unique ordering ও index design জরুরি।
        - Application query ও stored procedure: codebase-এ logic দৃশ্যমান বনাম database-side control; deployment, portability ও team ownership বদলায়।

    - **[25. EF Core setup, DbContext ও change tracking](https://learn.microsoft.com/en-us/ef/core/dbcontext-configuration/)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **EF Core setup**
        - ORM responsibilities
        - Provider selection
        - EF/provider version compatibility
        - DbContext
        - `DbSet<T>`
        - `DbContextOptions<T>`
        - AddDbContext
        - Connection string configuration
      - **Context lifetime**
        - Unit of work
        - Scoped lifetime
        - Thread-safety limitation
        - Await each operation
        - Disposal
        - IDbContextFactory — প্রয়োজনভিত্তিক
      - **Change tracking**
        - Added
        - Unchanged
        - Modified
        - Deleted
        - Detached
        - Original values
        - Current values
        - Change detection
        - Identity resolution
        - Relationship fixup
      - **Queries**
        - Tracking query
        - AsNoTracking
        - AsNoTrackingWithIdentityResolution
        - QueryTrackingBehavior
      - **Boundaries**
        - DbContext pooling
        - Database connection pooling
        - Context ও connection ownership

      - **Trade-offs**
        - Tracking ও no-tracking: change persistence সহজ বনাম read-only overhead কমানো; identity resolution ও later updates-এর প্রয়োজন বিবেচ্য।
        - Scoped context ও context factory: এক request-এর unit of work সহজ বনাম পৃথক operation lifetime; transaction boundaries স্পষ্ট রাখতে হয়।
        - Context pooling: setup allocation কমতে পারে; tenant/request-specific mutable state reset না হলে data isolation ভাঙতে পারে।
        - EF Core ও direct SQL: development speed ও mapping বনাম query-level control; generated SQL বোঝার প্রয়োজন থাকে।

    - **[26. EF Core model configuration ও relationships](https://learn.microsoft.com/en-us/ef/core/modeling/)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Model configuration**
        - Conventions
        - Data annotations
        - Fluent API
        - OnModelCreating
        - `IEntityTypeConfiguration<T>`
        - Configuration precedence
        - Assembly configuration discovery
      - **Entity properties**
        - Table ও schema mapping
        - Column names ও types
        - Required properties
        - Maximum length
        - Precision ও scale
        - Unicode
        - Default values
        - Computed columns
        - Value generation
      - **Keys ও indexes**
        - Primary keys
        - Composite keys
        - Alternate keys
        - Unique indexes
        - Composite indexes
      - **Relationships**
        - Principal ও dependent
        - Foreign key
        - Navigation property
        - Collection navigation
        - One-to-one
        - One-to-many
        - Many-to-many skip navigations
        - Explicit join entity ও payload
        - Self-referencing relationship
        - Required ও optional relationship
        - Delete behavior
        - Shadow foreign key
        - Backing fields — প্রয়োজনভিত্তিক
      - **Modeling extensions — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Value converters
        - Value comparers
        - Complex types
        - Owned entity types
        - JSON mapping — provider/version-specific

      - **Trade-offs**
        - Annotations ও Fluent API: model-এর কাছে সহজ configuration বনাম centralized, richer mapping; দুই জায়গায় contradictory rules এড়াতে হয়।
        - Skip navigation ও explicit join entity: সহজ many-to-many বনাম relationship metadata; join-এ quantity/date থাকলে explicit model দরকার।
        - Complex type ও owned entity: value-oriented mapping বনাম entity identity semantics; version, provider ও mapping limitations বিবেচ্য।
        - Value converter: domain-friendly type রাখা যায়; SQL translation, querying ও comparison behavior পরীক্ষা করতে হয়।

    - **[27. Migrations, schema evolution ও data seeding](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/applying)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Migration workflow**
        - dotnet-ef tool
        - Design-time DbContext creation
        - Add migration
        - Model snapshot
        - Up
        - Down
        - Update database
        - Remove unapplied migration
        - Migration history table
      - **Review**
        - Generated SQL
        - Destructive changes
        - Rename ও drop/add distinction
        - Default data backfill
        - Large-table migration cost
        - Branch conflicts
      - **Deployment**
        - Migration scripts
        - Idempotent scripts
        - Migration bundles
        - Separate migration credentials
        - Expand-contract rollout
        - Backward-compatible schema
        - Roll-forward ও rollback
        - Backup ও restore rehearsal
      - **[Seeding](https://learn.microsoft.com/en-us/ef/core/modeling/data-seeding)**
        - UseSeeding
        - UseAsyncSeeding
        - Idempotent initialization
        - HasData model-managed data
        - Test fixtures
      - **Alternatives**
        - Database-first scaffolding
        - Reverse-engineering customization
        - EnsureCreated সীমা

      - **Trade-offs**
        - App-start migration ও deployment-step migration: local simplicity বনাম deployment control; production-এ permissions ও concurrent startup ভাবতে হয়।
        - Code-first ও database-first: code-driven evolution বনাম existing database ownership; schema changes-এর authoritative source ঠিক করতে হয়।
        - UseSeeding ও HasData: initialization logic বনাম migration-managed fixed data; dynamic values ও external dependencies আলাদা বিষয়।
        - Destructive rollback ও roll-forward: দ্রুত schema ফেরানো বনাম data preservation; applied data transformation সব সময় উল্টানো যায় না।

    - **[28. EF Core queries, related data ও pagination](https://learn.microsoft.com/en-us/ef/core/querying/)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Query pipeline**
        - LINQ expression
        - Provider translation
        - SQL execution
        - Materialization
        - Server evaluation
        - Client evaluation boundaries
        - Async terminal operators
      - **Projection**
        - Select DTO
        - Anonymous projection
        - Aggregates
        - Grouping
        - Joins
        - [LeftJoin ও RightJoin in EF 10](https://learn.microsoft.com/en-us/ef/core/what-is-new/ef-core-10.0/whatsnew)
      - **Related data**
        - Eager loading
        - Include
        - ThenInclude
        - Filtered Include
        - Explicit loading
        - Lazy loading
        - N+1 queries
        - Navigation fixup effects
      - **Query shape**
        - Single queries
        - Split queries
        - Cartesian explosion
        - Buffering
        - Streaming
      - **Pagination**
        - Skip ও Take
        - Keyset pagination
        - Stable unique ordering
        - Composite cursor
        - Total count cost
        - Page size limits
      - **Inspection**
        - ToQueryString
        - SQL logging
        - Query tags
        - CancellationToken

      - **Trade-offs**
        - Eager, explicit ও lazy loading: predictable queries, selective loading ও convenience; round trips ও N+1 risk ভিন্ন।
        - Projection ও Include: ছোট response-oriented query বনাম entity graph; projection-এ update tracking workflow আলাদা।
        - Single ও split query: fewer round trips বনাম duplication কমানো; consistency window ও network latency বিবেচ্য।
        - Streaming ও buffering: lower peak memory বনাম connection দীর্ঘক্ষণ খোলা থাকা; client cancellation ও partial failure সামলাতে হয়।

    - **[29. EF Core writes, transactions ও concurrency](https://learn.microsoft.com/en-us/ef/core/saving/concurrency)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Writing data**
        - Add ও AddRange
        - Attach
        - Update
        - Remove
        - SaveChanges
        - SaveChangesAsync
        - Generated values
        - Disconnected entities
        - Property-level updates
        - Relationship updates
      - **Transaction boundaries**
        - SaveChanges transaction
        - Explicit transaction
        - Multiple SaveChanges calls
        - Savepoints
        - Shared transaction — প্রয়োজনভিত্তিক
        - Execution strategy
        - Transaction ও retry interaction
      - **Concurrency**
        - Lost update
        - Concurrency token
        - SQL Server rowversion
        - Application-managed token
        - DbUpdateConcurrencyException
        - Client-wins ও store-wins policy
        - Reload ও merge
        - HTTP If-Match integration
      - **Integrity**
        - Unique-constraint violations
        - DbUpdateException
        - Race-safe insertion
        - Idempotent command
        - External side-effect boundary
      - **Set-based operations — প্রয়োজনভিত্তিক**
        - ExecuteUpdate
        - ExecuteDelete
        - Change-tracker bypass
        - Explicit concurrency predicates

      - **Trade-offs**
        - Optimistic ও pessimistic concurrency: low-contention throughput বনাম proactive locking; conflicts, deadlocks ও retry policy আলাদা।
        - Tracked writes ও ExecuteUpdate/Delete: entity behavior ও change tracking বনাম set-based efficiency; tracker sync ও concurrency checks নিজের দায়িত্ব।
        - বড় transaction ও ছোট transaction: atomic scope বড় করা বনাম কম lock duration; external calls transaction-এর মধ্যে রাখলে failure cost বাড়ে।
        - Automatic retry: transient failure recovery; operation replay-safe না হলে duplicate effects ঘটতে পারে।

    - **[30. EF Core performance ও advanced mapping](https://learn.microsoft.com/en-us/ef/core/performance/efficient-querying)**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **Performance diagnosis — গভীর**
        - Slow query identification
        - Execution plan
        - Index usage
        - Query count
        - Projection size
        - Materialization allocation
        - Connection pool pressure
      - **Optimization**
        - Compiled queries
        - Parameterized query shapes
        - DbContext pooling
        - Batch writes
        - Compiled models — বিশেষায়িত
        - Provider-specific SQL
      - **[Query filters](https://learn.microsoft.com/en-us/ef/core/querying/filters)**
        - Soft-delete filter
        - Tenant filter
        - Named filters in EF 10
        - IgnoreQueryFilters
        - Required-navigation interaction
      - **Advanced mapping — বিশেষায়িত; পরিচিতি**
        - Table-per-hierarchy
        - Table-per-type
        - Table-per-concrete-type
        - Discriminators
        - Keyless entity types
        - Database views
        - Table splitting
        - Entity splitting
        - Temporal tables — provider-specific
        - Spatial data — provider-specific
        - JSON column queries — provider-specific
      - **Extensibility — বিশেষায়িত; পরিচিতি**
        - SaveChanges interceptors
        - Command interceptors
        - Audit stamping
        - Connection interceptors
        - Raw SQL composition

      - **Trade-offs**
        - Compiled queries: hot path-এ overhead কমতে পারে; dynamic query flexibility ও maintenance trade-off আছে।
        - Global filters: default tenant/soft-delete scope সহজ; bypass paths ও navigation joins review করা লাগে, এগুলো পূর্ণ authorization নয়।
        - TPH, TPT ও TPC: schema compactness, normalization ও polymorphic query cost আলাদা; workload দিয়ে নির্বাচন।
        - Interceptor: cross-cutting কাজ কেন্দ্রীভূত হয়; hidden behavior, ordering ও testability-এর cost বাড়ে।

    - **[31. ADO.NET, Dapper ও alternative data stores](https://github.com/DapperLib/Dapper)**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **ADO.NET**
        - DbConnection
        - DbCommand
        - DbParameter
        - DbDataReader
        - ExecuteReader
        - ExecuteScalar
        - ExecuteNonQuery
        - Async operations
        - Transactions
        - Disposal
      - **Dapper**
        - Parameter binding
        - Query mapping
        - Multi-mapping
        - Multiple result sets
        - Buffered ও unbuffered reads
        - Transaction sharing
      - **Data-store selection**
        - SQL Server
        - PostgreSQL
        - SQLite
        - MySQL-compatible providers
        - Provider compatibility
      - **NoSQL — বিশেষায়িত; পরিচিতি**
        - Document model
        - Key-value model
        - Wide-column model
        - Graph model
        - Partition key
        - Indexing
        - Consistency model
        - Transaction boundaries
        - MongoDB বা Cosmos DB integration
      - **Specialized storage — পরিচিতি**
        - Search index
        - Time-series store
        - Vector index
        - Object storage

      - **Trade-offs**
        - EF Core ও Dapper: model/tracking সুবিধা বনাম SQL control; hand-written SQL, mapping ও schema synchronization-এর দায়িত্ব বদলায়।
        - এক ORM ও mixed data access: consistency ও simplicity বনাম targeted optimization; shared transactions ও duplicate mapping সামলাতে হয়।
        - Relational ও document database: joins/constraints বনাম aggregate-shaped access; access pattern, partitioning ও consistency আগে নির্ধারণ।
        - SQLite ও production server database: lightweight local setup বনাম production behavior fidelity; collation, types ও query semantics এক নাও হতে পারে।

    - **Practical gate**
      - Real relational database-এ CRUD, relationships, migrations, pagination ও concurrent-update handling।

5. **Security — identity থেকে resource authorization**

    - **[32. Authentication architecture, OAuth ও OpenID Connect](https://www.rfc-editor.org/rfc/rfc9700)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Identity concepts**
        - Authentication
        - Authorization
        - Principal
        - ClaimsIdentity
        - ClaimsPrincipal
        - Claims
        - Roles
        - Permissions
      - **ASP.NET Core authentication**
        - Authentication schemes
        - Default scheme
        - Authenticate
        - Challenge
        - Forbid
        - Sign-in ও sign-out
        - Multiple schemes
        - Policy schemes — প্রয়োজনভিত্তিক
      - **Credential models**
        - Cookie authentication
        - Bearer authentication
        - API keys — প্রয়োজনভিত্তিক
        - Client certificates — বিশেষায়িত
      - **Standards**
        - OAuth 2.0 authorization
        - OpenID Connect authentication
        - Authorization server
        - Resource server
        - Public ও confidential client
        - Authorization code ও PKCE
        - Client credentials
        - Device authorization — বিশেষায়িত
        - Discovery metadata
        - Access token
        - ID token
        - Refresh token
        - Scopes ও consent
        - Redirect URI validation
        - state ও nonce
      - **Trust boundaries**
        - Token issuer ও token validator
        - Access token ও ID token-এর আলাদা উদ্দেশ্য
        - Legacy implicit/password flows-এর ঝুঁকি

      - **Trade-offs**
        - Cookie ও bearer token: browser session integration বনাম cross-client API use; CSRF, token storage ও refresh responsibilities ভিন্ন।
        - Managed identity provider ও self-hosted authority: কম operational burden বনাম control; cost, availability ও maintenance ownership বদলায়।
        - API key ও user identity: simple application identification বনাম user-level permission; key একাই rich user authorization দেয় না।
        - BFF ও browser-held tokens: browser-এ token exposure কমানো বনাম অতিরিক্ত backend/session layer; CSRF ও proxy behavior configure করতে হয়।

    - **[33. JWT bearer validation ও token lifecycle](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/configure-jwt-bearer-authentication?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **JWT structure**
        - Header
        - Payload
        - Signature
        - Base64url
        - Signed ও encrypted token
        - JWS ও JWE — ব্যবহারিক
      - **Validation**
        - AddAuthentication
        - AddJwtBearer
        - Authority
        - Audience
        - Issuer
        - Signature verification
        - Algorithm restrictions
        - Signing keys
        - JWKS
        - exp ও nbf
        - Clock skew
        - Required claims policy
        - Claim mapping ও role claim type
        - Invalid ও expired token behavior
      - **Lifecycle**
        - Token acquisition through issuer
        - Short-lived access tokens
        - Refresh token storage
        - Refresh rotation
        - Reuse detection
        - Revocation
        - Key rotation
        - Logout semantics
        - Scope validation
      - **Operational safety**
        - HTTPS metadata
        - Token redaction
        - Token-in-query leakage
        - Multi-issuer scheme separation
        - Test-only token generation
        - Production authority integration

      - **Trade-offs**
        - JWT ও opaque token: local validation ও distributed verification বনাম centralized introspection/revocation; token size ও authority dependency বদলায়।
        - Short ও long access-token lifetime: replay window কমানো বনাম refresh traffic ও availability dependency।
        - Symmetric ও asymmetric signing: simple shared secret বনাম পৃথক signing/verification keys; distributed trust ও rotation complexity ভিন্ন।
        - Stateless validation ও revocation lookup: fast verification বনাম immediate revocation; extra state ও network/cache dependency লাগে।

    - **[34. ASP.NET Core Identity ও account lifecycle](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/identity-api-authorization?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Identity components**
        - IdentityUser
        - IdentityRole
        - UserManager
        - SignInManager
        - RoleManager
        - IUserStore
        - EF Core stores
        - Custom user properties
      - **Account lifecycle**
        - Registration
        - Email normalization
        - Password hashing
        - Password policy
        - Email confirmation
        - Login
        - Logout
        - Lockout
        - Rate limiting
        - Password reset
        - Change password
        - Change email
        - Security stamp
        - Account disable/delete
      - **Additional authentication**
        - External login
        - Two-factor authentication
        - Recovery codes
        - Passkeys ও WebAuthn — প্রয়োজনভিত্তিক; ব্যবহারিক
      - **Identity endpoints**
        - AddIdentityApiEndpoints
        - MapIdentityApi
        - Cookie mode
        - Proprietary bearer-token mode
        - Identity API bearer tokens-এর non-JWT format
        - OAuth/OIDC authority থেকে scope-এর পার্থক্য
      - **Cookie behavior**
        - HttpOnly
        - Secure
        - SameSite
        - Expiration
        - Sliding expiration
        - .NET 10 known API endpoints-এর 401/403 behavior

      - **Trade-offs**
        - Identity ও external identity provider: account data/control নিজের কাছে বনাম hosted lifecycle; MFA, recovery, security updates ও availability-এর দায়িত্ব বদলায়।
        - Identity API tokens ও standard OAuth/OIDC tokens: simple first-party authentication বনাম interoperability/delegation; integration requirements দেখে নির্বাচন।
        - HttpOnly cookies: JavaScript দিয়ে token পড়া কঠিন; browser-এর authenticated requests ও CSRF এখনও সামলাতে হয়।
        - Password ও passkeys: compatibility/familiarity বনাম phishing resistance; enrollment, recovery ও device support পরিকল্পনা দরকার।

    - **[35. Authorization, policies ও resource ownership](https://learn.microsoft.com/en-us/aspnet/core/security/authorization/policies?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Basic authorization**
        - Authorize
        - AllowAnonymous
        - RequireAuthorization
        - Authenticated user requirement
        - 401 challenge
        - 403 forbid
      - **Permission models**
        - Role-based authorization
        - Claim-based authorization
        - Permission-based authorization
        - Policy-based authorization
      - **Policies**
        - AuthorizationPolicy
        - Requirements
        - IAuthorizationRequirement
        - `AuthorizationHandler<T>`
        - Multiple requirements
        - Multiple handlers
        - Success ও explicit failure
        - Default policy
        - Fallback policy
        - Dynamic policy provider — বিশেষায়িত
      - **Resource authorization**
        - IAuthorizationService
        - Resource-based handler
        - Ownership
        - Tenant boundary
        - Object-level access
        - Property-level access
        - Function-level access
        - Query-level data scoping
      - **Verification**
        - Anonymous user
        - Wrong role
        - Wrong owner
        - Cross-tenant identifier
        - Disabled account
        - Stale permission

      - **Trade-offs**
        - Roles ও permissions: simple administration বনাম fine-grained control; permission modeling ও policy maintenance বাড়ে।
        - Token claims ও database permission lookup: fast local decision বনাম fresh permissions; stale token, cache invalidation ও extra query trade-off থাকে।
        - Endpoint policy ও resource handler: coarse permission দ্রুত যাচাই বনাম ownership-aware decision; actual resource/context resolve করতে হয়।
        - Default-deny policy: accidental public endpoint কমে; intended anonymous endpoints স্পষ্টভাবে চিহ্নিত করতে হয়।

    - **[36. API security, CORS, CSRF ও data protection](https://api-security.owasp.org/editions/2023/en/0x11-t10/)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **OWASP API risk coverage**
        - Object-level authorization failures
        - Broken authentication
        - Property-level exposure ও mass assignment
        - Unrestricted resource consumption
        - Function-level authorization failures
        - Sensitive business-flow abuse
        - SSRF
        - Security misconfiguration
        - API inventory gaps
        - Unsafe downstream API consumption
      - **Input ও output safety**
        - SQL parameterization
        - Path traversal prevention
        - Command argument validation
        - Header injection prevention
        - Request size limits
        - Response data minimization
        - Sensitive log redaction
      - **Browser boundaries**
        - Same-origin policy
        - CORS policy
        - Allowed origins
        - Allowed methods
        - Allowed headers
        - Exposed headers
        - Credentials
        - Preflight requests
        - CORS-এর server-to-server সীমা
        - CSRF ও automatic cookie submission
        - Antiforgery tokens
        - SameSite cookie behavior
        - XSS ও token storage
      - **Transport ও secrets**
        - HTTPS
        - HTTPS redirection
        - HSTS
        - Host filtering ও AllowedHosts
        - TLS termination
        - Trusted forwarded headers
        - Certificate validation
        - Secret rotation
        - Least-privilege DB credentials
      - **Data Protection — ব্যবহারিক**
        - Key ring
        - Key persistence
        - Shared keys across instances
        - Application isolation
        - Encryption at rest
      - **Abuse controls**
        - Login throttling
        - Request rate limits
        - Costly-operation limits
        - Security audit events

      - **Trade-offs**
        - Broad ও specific CORS policy: integration সহজ বনাম browser access control; credentials-এর সঙ্গে explicit origins প্রয়োজন।
        - Client-side ও server-side validation: দ্রুত feedback বনাম authoritative enforcement; server-side checks বাদ দেওয়ার বিকল্প নেই।
        - Detailed audit ও data minimization: incident investigation সহজ হয়; retention, access control ও sensitive-data exposure cost বাড়ে।
        - Shared Data Protection keys: multi-instance cookies/tokens কাজ করে; key access, persistence ও rotation রক্ষা করতে হয়।
        - Application rate limit ও edge protection: fine-grained user policy বনাম upstream traffic absorption; একটির scope অন্যটির সমান নয়।

    - **37. Multi-tenancy ও tenant isolation**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Tenant model**
        - Tenant identity
        - User-tenant membership
        - Tenant roles
        - Tenant resolution
        - Trusted host/subdomain
        - Token claim
        - Validated route/header
      - **Data isolation**
        - Shared tables ও TenantId
        - Schema per tenant
        - Database per tenant
        - Composite unique keys
        - Foreign-key tenant consistency
        - EF query filters
        - Filter bypass review
      - **Request scope**
        - Tenant context
        - Scoped dependencies
        - DbContext pooling reset
        - Tenant-aware authorization
      - **Cross-cutting isolation**
        - Cache keys
        - File paths
        - Background jobs
        - Message metadata
        - Logs ও metrics
        - Rate-limit partitions
      - **Operations**
        - Tenant provisioning
        - Tenant migrations
        - Tenant deletion/export
        - Noisy-neighbor control
        - Cross-tenant tests

      - **Trade-offs**
        - Shared tables ও separate databases: cost ও centralized operation বনাম stronger isolation; migrations, connections ও operational burden বাড়ে।
        - Tenant claim ও request header: issuer-backed identity বনাম flexible routing; client-supplied tenant selector-এর membership যাচাই প্রয়োজন।
        - Global filters ও explicit predicates: default scoping বনাম visible query constraints; bypass ও raw SQL paths উভয়ক্ষেত্রে audit দরকার।
        - Per-tenant cache/rate partitions: isolation ও fairness; key cardinality, memory ও configuration count বাড়ে।

    - **Practical gate**
      - দুই user ও দুই role দিয়ে unauthorized, forbidden, ownership ও token-expiry cases পরীক্ষা।

6. **Integrations — outbound HTTP, background work ও messaging**

    - **[38. HttpClient, connection management ও typed clients](https://learn.microsoft.com/en-us/dotnet/fundamentals/networking/http/httpclient-guidelines)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **HTTP client model**
        - HttpClient
        - HttpRequestMessage
        - HttpResponseMessage
        - HttpContent
        - HttpMessageHandler
        - SocketsHttpHandler
      - **Requests**
        - BaseAddress ও relative URI resolution
        - Per-request headers
        - Authorization header
        - JSON content
        - Form content
        - Multipart content
        - SendAsync
        - Request message reuse limitation
      - **Responses**
        - Status inspection
        - EnsureSuccessStatusCode
        - ProblemDetails parsing
        - ReadFromJsonAsync
        - ResponseHeadersRead
        - Streaming
        - Disposal ownership
      - **Connection lifecycle**
        - Connection pools
        - DNS refresh
        - PooledConnectionLifetime
        - Idle timeout
        - MaxConnectionsPerServer
        - Socket exhaustion
      - **IHttpClientFactory**
        - Basic client
        - Named client
        - Typed client
        - Handler pooling
        - HandlerLifetime
        - Typed-client lifetime
        - CookieContainer sharing
        - Handler DI scope boundaries
      - **Pipeline**
        - DelegatingHandler
        - Authentication handler
        - Logging ও tracing
        - Request cancellation
        - Timeout ownership
        - Test handler

      - **Trade-offs**
        - Long-lived client ও factory client: কম setup বনাম centralized configuration/handlers; উভয়ের connection lifetime সঠিক রাখতে হয়।
        - Named ও typed client: runtime selection বনাম compile-time API wrapper; string keys ও class count-এর trade-off থাকে।
        - ResponseHeadersRead: দ্রুত streaming শুরু ও কম buffering; stream lifetime ও body-read cancellation নিজের দায়িত্ব।
        - Shared default headers ও per-request headers: কম repetition বনাম request isolation; user-specific token shared mutable settings-এ রাখা বিপজ্জনক।

    - **[39. Resilience, timeouts, retries ও idempotency](https://learn.microsoft.com/en-us/dotnet/core/resilience/http-resilience)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Failure classification**
        - Transient failure
        - Permanent failure
        - Timeout
        - Cancellation
        - Network failure
        - Dependency overload
      - **Timeout design**
        - Connection timeout
        - Per-attempt timeout
        - Total request timeout
        - End-to-end deadline
        - Cancellation propagation
      - **Retry policy**
        - Retryable operations
        - Retryable status classification
        - Exponential backoff
        - Jitter
        - Retry-After
        - Retry budget
        - Maximum attempts
        - Unsafe-method policy
        - Replayable request body
      - **Protection patterns**
        - Circuit breaker
        - Concurrency limiter
        - Rate limiter
        - Bulkhead isolation
        - Fallback
        - Hedging — বিশেষায়িত; পরিচিতি
      - **.NET integration**
        - Microsoft.Extensions.Http.Resilience
        - AddStandardResilienceHandler
        - Custom resilience pipeline
        - Avoid duplicate retry layers
      - **Idempotency**
        - Safe ও idempotent-এর পার্থক্য
        - Idempotency key
        - Request fingerprint
        - Atomic deduplication
        - Response replay
        - Retention window

      - **Trade-offs**
        - Retry: transient fault recover হয়; duplicate side effects, latency এবং retry storm বাড়তে পারে।
        - Circuit breaker: failing dependency-তে চাপ কমে; threshold ভুল হলে healthy recovery-ও দেরি হতে পারে।
        - Short timeout: resource দ্রুত মুক্ত হয়; slow-but-valid operation বেশি fail করতে পারে।
        - Hedging: tail latency কমতে পারে; duplicate requests ও downstream cost বাড়ে, replay-safe operation দরকার।
        - Fallback: partial availability পাওয়া যায়; stale বা incomplete ফল client contract-এ স্পষ্ট হতে হয়।

    - **40. Webhooks ও third-party service integration**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Outbound integration design**
        - Provider client abstraction
        - Authentication credentials
        - Environment separation
        - Request ও response mapping
        - Provider error translation
        - Rate limits
        - Timeout ও retry policy
      - **Webhook receiver**
        - Raw request body
        - Signature verification
        - Timestamp validation
        - Replay prevention
        - Secret rotation
        - Event identifier
        - Deduplication
        - Durable acceptance
        - Fast acknowledgment
        - Asynchronous processing
      - **Webhook sender**
        - Subscriber registration
        - Endpoint verification
        - Signed delivery
        - Delivery identifiers
        - Retry schedule
        - Failed-delivery retention
        - Dead-letter handling
        - Replay operation
      - **Consistency**
        - Out-of-order events
        - Versioned event schema
        - Idempotent state transition
        - Reconciliation job
        - Audit trail
      - **Safety**
        - Callback URL validation
        - SSRF protection
        - Sensitive payload redaction

      - **Trade-offs**
        - Webhook ও polling: কম latency ও কম unnecessary requests বনাম receiver/retry complexity; polling সহজ হলেও quota ও delay বাড়ে।
        - Immediate processing ও queued processing: এক request-এ ফল পাওয়া বনাম reliable fast acknowledgment; queue-তে eventual consistency আসে।
        - Full event payload ও resource reference: fewer follow-up calls বনাম smaller event; freshness, privacy ও provider availability dependency বদলায়।
        - Strict ordering ও idempotent reconciliation: sequence সহজ বোঝা বনাম higher throughput; out-of-order events-এর recovery strategy লাগে।

    - **[41. Hosted services, workers ও scheduled jobs](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Hosted service model**
        - IHostedService
        - BackgroundService
        - StartAsync
        - ExecuteAsync
        - StopAsync
        - IHostedLifecycleService — প্রয়োজনভিত্তিক; পরিচিতি
        - Worker Service project
        - [.NET 10 ExecuteAsync startup behavior](https://learn.microsoft.com/en-us/dotnet/core/compatibility/extensions/10.0/backgroundservice-executeasync-task)
      - **Lifetime ও scopes**
        - Singleton hosted-service lifetime
        - IServiceScopeFactory
        - Scoped DbContext
        - CancellationToken
        - Graceful shutdown
        - Exception behavior
        - Resource disposal
      - **Scheduling**
        - PeriodicTimer
        - Delay loop
        - Overlapping execution
        - Cron semantics
        - Time zones ও daylight saving
        - Missed runs
        - Duplicate execution
      - **Queues**
        - `Channel<T>`
        - Bounded capacity
        - Backpressure
        - Worker concurrency
        - Durable queue alternative
      - **Job reliability**
        - Idempotency
        - Retries
        - Checkpoints
        - Dead-letter jobs
        - Distributed job coordination
        - Job status
      - **Scheduler tools — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Hangfire
        - Quartz.NET
        - Managed scheduler

      - **Trade-offs**
        - In-process worker ও separate worker: simple deployment বনাম independent scaling/failure isolation; দ্বিতীয়টিতে deployment ও communication বাড়ে।
        - In-memory Channel ও durable broker: low overhead বনাম restart-safe delivery; memory queue-তে process loss-এর কাজ হারাতে পারে।
        - PeriodicTimer ও durable scheduler: সহজ periodic কাজ বনাম persistent schedules/retries; scheduler storage ও operations লাগে।
        - High worker concurrency: throughput বাড়ে; database, API quotas ও lock contention সীমা মানতে হয়।

    - **42. Messaging, events, outbox ও delivery guarantees**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Messaging foundations**
        - Command
        - Event
        - Queue
        - Publish/subscribe
        - Producer
        - Consumer
        - Message envelope
        - Correlation identifier
      - **Broker selection — ব্যবহারিক**
        - RabbitMQ বা Azure Service Bus
        - Kafka-style event log — বিশেষায়িত
        - Routing
        - Consumer groups
        - Partitions
      - **Delivery**
        - At-most-once
        - At-least-once
        - Acknowledgment
        - Publisher confirmation
        - Redelivery
        - Deduplication
        - Idempotent consumer
        - Ordering scope
        - Retry delay
        - Dead-letter queue
        - Poison messages
      - **Consistency patterns**
        - Transactional outbox
        - Outbox dispatcher
        - Inbox/deduplication store
        - Business operation ও message atomicity
        - Eventual consistency
        - Saga ও compensation — বিশেষায়িত
      - **Contracts ও operations**
        - Event schema evolution
        - Backward compatibility
        - Correlation ও trace propagation
        - Consumer lag
        - Replay
        - Exactly-once দাবির transaction scope
        - [Broker reliability ও acknowledgments](https://www.rabbitmq.com/docs/reliability)

      - **Trade-offs**
        - Synchronous HTTP ও messaging: immediate response/flow visibility বনাম buffering ও loose temporal coupling; eventual consistency ও tracing কঠিন হয়।
        - Queue ও event log: job distribution বনাম replayable history; retention, partitioning ও consumer operation ভিন্ন।
        - At-least-once delivery: retry দিয়ে reliability; duplicate handling ছাড়া business correctness নিশ্চিত হয় না।
        - Outbox: local data ও event intent atomic রাখা যায়; dispatcher, retention ও duplicate delivery সামলাতে হয়।
        - Saga: long workflow ছোট local transactions-এ ভাগ হয়; compensation সব operation-এর সত্যিকারের rollback নয়।

    - **Practical gate**
      - Timeout, retry, duplicate request ও process restart-এর মধ্যেও external integration সঠিক রাখা।

7. **Production features — caching, limits, files ও communication**

    - **[43. Caching, Redis, HybridCache ও HTTP caching](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/hybrid?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Cache foundations**
        - Cache key
        - Hit ও miss
        - TTL
        - Absolute expiration
        - Sliding expiration
        - Eviction
        - Cache-aside
        - Invalidation
        - Stale data
        - Cache stampede
      - **Application caches**
        - IMemoryCache
        - IDistributedCache
        - Redis integration
        - Serialization
        - HybridCache
        - Local ও distributed levels
        - Request coalescing
        - Size limits
        - Tag-based invalidation semantics
      - **HTTP caching**
        - Cache-Control
        - Public ও private
        - no-store ও no-cache
        - ETag
        - Last-Modified
        - Conditional GET
        - Vary
        - Response caching middleware
      - **[Output caching](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/output?view=aspnetcore-10.0)**
        - Server-controlled policy
        - Endpoint policies
        - Variation by route/query/header
        - Cache locking
        - Eviction tags
        - Authenticated-response policy
      - **Correctness**
        - User ও tenant key isolation
        - Cache invalidation after writes
        - Multi-instance consistency
        - Cache outage behavior
        - Sensitive-data retention
      - **[Session state](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/app-state?view=aspnetcore-10.0) — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - ISession
        - AddSession
        - UseSession
        - Session cookie
        - Idle timeout
        - Distributed session backing store
        - Concurrent session update semantics

      - **Trade-offs**
        - Memory ও distributed cache: lower latency/simple setup বনাম shared state; distributed cache-এ network, serialization ও availability dependency থাকে।
        - Long ও short TTL: higher hit rate বনাম freshness; workload ও invalidation reliability অনুযায়ী নির্বাচন।
        - Output ও data cache: পুরো response reuse বনাম reusable underlying data; variation keys ও authorization isolation আলাদা।
        - HybridCache: common caching flow ও stampede protection সহজ; multi-node freshness ও backend availability তবুও design করতে হয়।
        - Cache invalidation ও expiration-only: fresh data বনাম simpler operation; stale-read tolerance স্পষ্ট থাকতে হয়।

    - **[44. Rate limiting, timeouts, compression ও performance](https://learn.microsoft.com/en-us/aspnet/core/performance/rate-limit?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Rate limiting**
        - Fixed window
        - Sliding window
        - Token bucket
        - Concurrency limiter
        - Partition keys
        - Per-user policy
        - Per-tenant policy
        - Global ও endpoint policy
        - Queue limit
        - Queue order
        - 429 response
        - Retry-After
        - Authentication/routing order
        - Per-instance ও global quota distinction
      - **Resource controls**
        - [Request timeout policy](https://learn.microsoft.com/en-us/aspnet/core/performance/timeouts?view=aspnetcore-10.0)
        - AddRequestTimeouts
        - UseRequestTimeouts
        - Per-endpoint timeout policy
        - Request body limit
        - Header limit
        - Upload limit
        - Pagination limit
        - Outbound concurrency
        - Connection limits
      - **Compression — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - Response compression
        - Brotli
        - Gzip
        - MIME types
        - HTTPS compression considerations
        - Request decompression
        - Decompressed-size limits
      - **Performance reasoning**
        - Throughput
        - Latency percentiles
        - CPU-bound ও I/O-bound bottleneck
        - Allocation ও GC pressure
        - Blocking code
        - Thread-pool starvation
        - Backpressure
        - Async streaming
        - Measurement before optimization

      - **Trade-offs**
        - Fixed ও sliding window: simple counters বনাম smoother limits; state ও implementation cost বাড়ে।
        - Token bucket ও concurrency limit: burst allowance বনাম in-flight work cap; request rate ও resource pressure আলাদা সমস্যা।
        - Queueing ও immediate rejection: temporary burst absorb করা বনাম bounded latency; লম্বা queue timeout ও memory cost বাড়ায়।
        - Compression: bandwidth কমে; CPU cost ও small-response overhead বাড়তে পারে।
        - In-app ও gateway quota: endpoint/user-aware control বনাম multi-instance/edge enforcement; deployment topology অনুযায়ী দুটিই লাগতে পারে।

    - **[45. File uploads, downloads ও object storage](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/file-uploads?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: গভীর*

      - **Uploads**
        - multipart/form-data
        - IFormFile
        - Multiple files
        - Buffered upload
        - Streaming upload
        - Resumable uploads — বিশেষায়িত; পরিচিতি
        - Integrity checksums — প্রয়োজনভিত্তিক
        - MultipartReader — প্রয়োজনভিত্তিক
        - Cancellation
        - Temporary files
        - Cleanup
      - **Validation**
        - Maximum size
        - Extension allowlist
        - Content-type checks
        - File signature validation
        - Generated storage name
        - Path traversal prevention
        - Scan/quarantine workflow
        - Form endpoint antiforgery
      - **Storage**
        - Local filesystem
        - Database binary storage
        - Object storage
        - Private container/bucket
        - Metadata in relational database
        - Signed upload/download URL
        - Expiration
        - Orphan cleanup
      - **Downloads**
        - File results
        - Content-Disposition
        - Content-Type
        - Range requests
        - ETag ও Last-Modified
        - Streaming
        - Per-file authorization
        - CDN policy
      - **Static assets — প্রয়োজনভিত্তিক; পরিচিতি**
        - UseStaticFiles
        - MapStaticAssets
        - Public ও protected file boundaries

      - **Trade-offs**
        - Buffered ও streamed upload: implementation সহজ বনাম lower memory; streamed parsing, validation ও cleanup জটিল হয়।
        - Local disk ও object storage: simple single-node operation বনাম durable scalable storage; network access, permissions ও cost যোগ হয়।
        - API-proxied ও signed direct transfer: centralized transfer control বনাম কম application bandwidth; signed URL lifetime ও scope সীমিত রাখতে হয়।
        - Database blobs ও external files: transactional convenience বনাম database size/backup cost; external storage-এ metadata consistency সামলাতে হয়।

    - **[46. Realtime APIs — SSE, WebSockets ও SignalR](https://learn.microsoft.com/en-us/aspnet/core/signalr/introduction?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **Communication models**
        - Polling
        - Long polling
        - Server-Sent Events
        - WebSockets
      - **SSE**
        - text/event-stream
        - Event data
        - Event identifier
        - Reconnection
        - Last-Event-ID
        - Cancellation
        - [.NET 10 ServerSentEvents result](https://learn.microsoft.com/en-us/aspnet/core/release-notes/aspnetcore-10.0?view=aspnetcore-10.0#support-for-server-sent-events-sse)
      - **WebSockets**
        - Handshake
        - Send ও receive loops
        - Message framing
        - Close handshake
        - Heartbeats
        - Backpressure
        - Connection limits
      - **SignalR**
        - Hubs
        - Strongly typed hubs
        - IHubContext
        - Clients
        - Users
        - Groups
        - Server-to-client invocation
        - Client-to-server invocation
        - Streaming
        - Authentication
        - Authorization
        - Group membership validation
      - **Scale ও reliability**
        - Reconnect
        - Message loss/replay policy
        - Redis backplane
        - Managed SignalR service
        - Load-balancer affinity requirements
        - Token logging precautions

      - **Trade-offs**
        - Polling ও SSE: simple request model বনাম timely one-way updates; persistent connections ও reconnect behavior সামলাতে হয়।
        - SSE ও WebSockets: server-to-client events সহজ বনাম bidirectional protocol; WebSockets-এ বেশি connection/message management লাগে।
        - Raw WebSocket ও SignalR: protocol control বনাম higher-level hub/group support; framework conventions ও scale requirements গ্রহণ করতে হয়।
        - Self-hosted ও managed realtime service: operational control বনাম কম connection-management burden; cost ও provider dependency বদলায়।

    - **[47. gRPC ও service-to-service contracts](https://learn.microsoft.com/en-us/aspnet/core/grpc/?view=aspnetcore-10.0)**

      *Priority: বিশেষায়িত · Depth: পরিচিতি*

      - **Protocol foundations**
        - HTTP/2
        - Protocol Buffers
        - .proto schema
        - Field numbers
        - Generated client/server types
      - **RPC shapes**
        - Unary
        - Server streaming
        - Client streaming
        - Bidirectional streaming
      - **ASP.NET Core integration — branch নিলে ব্যবহারিক**
        - Service implementation
        - Endpoint mapping
        - Channel reuse
        - Client factory
        - Metadata
        - Status codes
        - Deadlines
        - Cancellation
        - Interceptors
        - Authentication ও authorization
      - **Compatibility ও operations**
        - Schema evolution
        - Reserved field numbers
        - Message size limits
        - Load balancing
        - Proxy compatibility
        - gRPC-Web
        - JSON transcoding — পরিচিতি

      - **Trade-offs**
        - REST/JSON ও gRPC: broad client compatibility ও human readability বনাম compact typed RPC; browser/proxy support যাচাই দরকার।
        - Unary ও streaming RPC: simple call lifecycle বনাম continuous data; deadlines, backpressure ও reconnect জটিল হয়।
        - Generated contract: compile-time consistency; schema evolution ও field-number discipline কঠোরভাবে maintain করতে হয়।

    - **48. Alternative API models — GraphQL ও OData**

      *Priority: বিশেষায়িত · Depth: পরিচিতি*

      - **[GraphQL](https://graphql.org/learn/)**
        - Schema ও types
        - Query
        - Mutation
        - Subscription
        - Resolver
        - Arguments
        - Variables
        - Nullable fields
        - Pagination
        - DataLoader
        - N+1 prevention
        - Field authorization
        - Query depth/complexity limits
        - Persisted operations
        - Error contract
        - .NET server library selection
      - **[OData](https://learn.microsoft.com/en-us/odata/webapi-8/overview)**
        - Entity Data Model
        - Routing
        - $filter
        - $select
        - $expand
        - $orderby
        - $top
        - $skip
        - $count
        - Allowed query options
        - Query validation
        - Expansion ও result limits
        - Version/provider compatibility

      - **Trade-offs**
        - REST ও GraphQL: operation-specific contracts ও HTTP caching সহজ বনাম client-shaped data; resolver authorization ও query-cost control বাড়ে।
        - GraphQL flexibility: over-fetching কমতে পারে; N+1, nested query cost ও caching strategy সচেতনভাবে সামলাতে হয়।
        - OData ও custom query parameters: standardized rich querying বনাম tighter endpoint control; database exposure ও query limits review করতে হয়।

    - **49. Search, filtering ও search-index integration**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **Database search**
        - Exact match
        - Prefix match
        - Case sensitivity
        - Collation
        - LIKE ও index behavior
        - Full-text search
        - Ranking
        - Paging
      - **Dedicated search engine — বিশেষায়িত**
        - Document mapping
        - Inverted index
        - Analyzer
        - Tokenization
        - Language handling
        - Relevance scoring
        - Facets
        - Autocomplete
        - Typo tolerance
        - Search-after pagination
      - **Consistency**
        - Database as source of truth
        - Index synchronization
        - Outbox/CDC — প্রয়োজনভিত্তিক
        - Reindexing
        - Alias switching
        - Stale-result handling
      - **Security**
        - Tenant-aware index/query
        - Result authorization
        - Query-cost limits

      - **Trade-offs**
        - Database search ও dedicated index: fewer components বনাম rich relevance/scalability; synchronization ও eventual consistency যোগ হয়।
        - Write-time indexing ও asynchronous indexing: immediate visibility বনাম write decoupling; indexing failure ও delay policy দরকার।
        - Shared ও per-tenant index: low operational overhead বনাম isolation; shard/index count ও routing complexity বাড়ে।

    - **[50. Globalization, time zones ও localized API behavior](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **Culture**
        - CultureInfo
        - CurrentCulture
        - CurrentUICulture
        - Invariant culture
        - Request culture providers
        - Accept-Language
        - Supported cultures
      - **ASP.NET Core localization**
        - RequestLocalizationOptions
        - UseRequestLocalization
        - IStringLocalizer
        - Resource files
        - Localized validation messages
      - **API contract stability**
        - Stable machine-readable error codes
        - Localized human messages
        - Invariant identifiers ও keys
        - Unicode normalization
        - Case comparison rules
      - **Time correctness — গভীর**
        - UTC instants
        - DateTimeOffset
        - Named time zone
        - DateOnly
        - Local wall-clock schedules
        - Daylight-saving transitions
        - Ambiguous ও invalid local times
        - Clock abstraction
        - TimeProvider

      - **Trade-offs**
        - Localized messages ও stable error codes: user-friendly text বনাম machine contract stability; client logic message text-এর ওপর নির্ভর করা উচিত নয়।
        - UTC instant ও local schedule: past event-এর নির্দিষ্ট সময় বনাম ভবিষ্যৎ recurring local intent; offset একা named time-zone rules ধরে না।
        - Culture-aware ও ordinal comparison: natural-language behavior বনাম predictable identifier matching; field-এর উদ্দেশ্য অনুযায়ী নির্বাচন।

    - **Practical gate**
      - প্রয়োজনীয় feature বেছে নিয়ে load, cancellation, isolation ও failure behavior পরীক্ষা।

8. **Architecture — maintainable application ও system boundaries**

    - **[51. Application architecture ও code organization](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Design principles**
        - Separation of concerns
        - Cohesion
        - Coupling
        - Encapsulation
        - SOLID
        - DRY
        - KISS
        - YAGNI
        - Dependency direction
      - **Application layers**
        - API/transport
        - Application use cases
        - Domain
        - Infrastructure
        - Persistence
      - **Organization styles**
        - Layered architecture
        - Feature folders
        - Vertical slices
        - Clean Architecture
        - Modular monolith
      - **Boundaries**
        - DTO ও domain model
        - Service interfaces
        - External integration adapters
        - Persistence boundary
        - Transaction boundary
        - Module contracts
        - Dependency inversion
      - **Practical structure**
        - One project ও multiple projects
        - Composition root
        - Cross-cutting concerns
        - Dependency registration extensions
        - Architecture decision records
        - Architecture tests — প্রয়োজনভিত্তিক

      - **Trade-offs**
        - Layered ও vertical slices: technical consistency বনাম feature locality; cross-feature duplication ও dependency rules সচেতনভাবে সামলাতে হয়।
        - Clean Architecture: infrastructure বদলানো ও domain testing সহজ; ছোট CRUD-এ অতিরিক্ত interfaces/mapping maintenance বাড়াতে পারে।
        - Modular monolith: এক deployment-এ module boundaries; boundary enforce না করলে shared database ও direct calls coupling বাড়ায়।
        - DRY ও local duplication: shared fixes সহজ বনাম independent feature evolution; premature abstraction unrelated features জোড়া লাগাতে পারে।

    - **52. Domain modeling, CQRS ও practical design patterns**

      *Priority: প্রয়োজনভিত্তিক · Depth: ব্যবহারিক*

      - **Domain modeling**
        - Entity identity
        - Value object
        - Invariant
        - Aggregate
        - Aggregate root
        - Domain service
        - Domain event
        - Bounded context
        - Ubiquitous language
        - Rich ও anemic model
      - **CQRS**
        - Command
        - Query
        - Separate handlers
        - Read model
        - Write model
        - Same database option
        - Separate store option
        - Validation pipeline
        - Transaction behavior
      - **Patterns**
        - Repository
        - Unit of Work
        - Specification
        - Strategy
        - Factory
        - Adapter
        - Decorator
        - Chain of Responsibility
        - Mediator
        - Observer
        - State machine
        - Builder
        - Fluent interface ও Builder-এর পার্থক্য
      - **Implementation choices**
        - Direct service call
        - Mediator library
        - Handwritten dispatcher
        - Result type
        - Domain exceptions
      - **Advanced — বিশেষায়িত; পরিচিতি**
        - Event sourcing
        - Event replay
        - Snapshots
        - Event schema migration

      - **Trade-offs**
        - Direct DbContext ও repository: EF capabilities সরাসরি ব্যবহার বনাম domain-specific abstraction; generic wrapper EF-এর উপরে শুধু duplication হতে পারে।
        - Simple service ও CQRS: কম moving parts বনাম read/write workflow separation; CQRS-এর জন্য দুই database বাধ্যতামূলক নয়।
        - Direct call ও mediator: explicit navigation বনাম centralized behaviors; indirection, registration ও package/license dependency বাড়ে।
        - Rich domain ও CRUD model: invariants কেন্দ্রীভূত করা বনাম simpler data operations; business complexity অনুযায়ী বিনিয়োগ।
        - Event sourcing ও state storage: history/rebuild capability বনাম simple current-state queries; versioning, replay ও operational cost অনেক বাড়ে।

    - **53. Distributed systems ও service architecture**

      *Priority: বিশেষায়িত · Depth: পরিচিতি*

      - **System foundations**
        - Partial failure
        - Network latency
        - Distributed state
        - Consistency models
        - Eventual consistency
        - CAP under network partition
        - Clock skew
        - Idempotency
      - **Service architecture**
        - Service boundaries
        - Independent deployment
        - Database ownership
        - API gateway
        - Backend for Frontend
        - Service discovery
        - Load balancing
        - Reverse proxy ও YARP
      - **Communication**
        - Synchronous calls
        - Asynchronous messages
        - Contract evolution
        - Distributed tracing
        - Timeout budgets
        - Retry amplification
      - **Consistency patterns**
        - Outbox
        - Saga
        - Compensation
        - Distributed locks
        - Lease expiry
        - Fencing tokens
        - Deduplication
      - **Scaling**
        - Horizontal scaling
        - Stateless application nodes
        - Database bottlenecks
        - Read replicas
        - Partitioning
        - Sharding
        - Multi-region replication

      - **Trade-offs**
        - Monolith ও microservices: local transactions/সহজ operations বনাম independent deployment; network failures ও distributed consistency cost যোগ হয়।
        - Shared database ও service-owned data: সহজ joins বনাম autonomy; ownership আলাদা হলে cross-service data composition লাগে।
        - Strong ও eventual consistency: immediate invariant visibility বনাম availability/latency flexibility; business tolerance আগে নির্ধারণ করতে হয়।
        - Distributed lock: কাজ coordinate করা যায়; lease loss, clock assumptions ও fencing ছাড়া correctness নিশ্চিত হয় না।
        - Read replica: read capacity বাড়ে; replication lag ও read-after-write consistency সামলাতে হয়।

    - **Practical gate**
      - Feature boundary, dependency direction ও transaction boundary ব্যাখ্যা করে একটি module আলাদা করা।

9. **Verification ও diagnostics — behavior, load ও production evidence**

    - **54. Unit testing ও testable application design**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Testing foundations**
        - Test behavior
        - Arrange-Act-Assert
        - Positive case
        - Negative case
        - Boundary case
        - Equivalence classes
        - Deterministic tests
      - **Framework selection**
        - xUnit
        - NUnit
        - MSTest
        - Test runner
        - Assertions
        - Parameterized tests
      - **Test boundaries**
        - Pure functions
        - Domain invariants
        - Use-case orchestration
        - Validation
        - Mapping
        - Failure mapping
      - **Test doubles**
        - Stub
        - Fake
        - Mock
        - Spy
        - External boundary substitution
        - Avoid mocking internal implementation
      - **Reliability**
        - TimeProvider
        - Deterministic identifiers
        - Async tests
        - Cancellation tests
        - Shared-state isolation
        - Test naming
        - Coverage interpretation
        - Property-based tests — বিশেষায়িত
        - Mutation testing — বিশেষায়িত

      - **Trade-offs**
        - Mock ও real collaborator: fast isolation বনাম realistic behavior; অতিরিক্ত mocking implementation-coupled tests তৈরি করে।
        - High coverage ও meaningful assertions: executed lines দেখা যায় বনাম business correctness যাচাই; percentage একা confidence দেয় না।
        - TDD ও test-after: design feedback আগে পাওয়া বনাম exploratory implementation flexibility; behavior-focused tests দুই পথেই প্রয়োজন।

    - **[55. Integration, database ও contract testing](https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **ASP.NET Core tests**
        - `WebApplicationFactory<Program>`
        - TestServer
        - Test HttpClient
        - Configuration override
        - Service override
        - Environment setup
        - Test authentication scheme
        - Production auth configuration checks
      - **Endpoint assertions**
        - Status code
        - Headers
        - Response schema
        - ProblemDetails
        - Validation errors
        - Authorization
        - Ownership
        - Tenant isolation
      - **Database tests**
        - Real production database provider
        - Testcontainers — প্রয়োজনভিত্তিক
        - Test database lifecycle
        - Migration application
        - Seed fixtures
        - Cleanup ও isolation
        - Transactions
        - Unique constraints
        - Concurrent updates
        - SQLite behavior differences
        - EF InMemory limitations
      - **Contract tests**
        - OpenAPI compatibility
        - Consumer/provider contracts
        - External HTTP test server
        - Webhook signature fixtures
        - Message schema compatibility

      - **Trade-offs**
        - EF InMemory ও real provider: quick setup বনাম SQL/constraint fidelity; relational integration behavior বাস্তব provider-এ যাচাই জরুরি।
        - Shared ও isolated test database: কম startup cost বনাম parallel test isolation; cleanup strategy ভিন্ন হয়।
        - Mocked authentication ও real token validation: focused authorization test বনাম deployment auth confidence; দুই test-এর উদ্দেশ্য আলাদা।
        - Contract ও end-to-end tests: targeted compatibility feedback বনাম full-system coverage; broader test ধীর ও failure diagnosis কঠিন হতে পারে।

    - **56. Load testing, security verification ও failure testing**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Load model**
        - Concurrent users
        - Request rate
        - Arrival pattern
        - Realistic data volume
        - Warmup
        - Steady load
        - Spike test
        - Stress test
        - Soak test
      - **Measurements**
        - Throughput
        - p50
        - p95
        - p99
        - Error rate
        - CPU
        - Memory
        - GC
        - Database connections
        - Queue depth
      - **Failure tests**
        - Dependency timeout
        - 429 ও Retry-After
        - Duplicate delivery
        - Database conflict
        - Process restart
        - Cancellation
        - Cache outage
        - Broker outage
      - **Security regression**
        - Missing token
        - Invalid audience/issuer
        - Expired token
        - Cross-user identifier
        - Cross-tenant identifier
        - Overposting
        - Oversized upload
        - Path manipulation
        - CORS ও CSRF policy
      - **Tools — প্রয়োজনভিত্তিক**
        - k6 বা JMeter
        - BenchmarkDotNet
        - Dependency scanner
        - Static ও dynamic analysis

      - **Trade-offs**
        - Microbenchmark ও load test: isolated code cost বনাম whole-system behavior; একটির ফল দিয়ে অন্যটি ধরে নেওয়া যায় না।
        - Production-like ও simplified environment: realistic bottleneck বনাম lower test cost; topology/data differences ফল বদলায়।
        - Broad end-to-end suite ও targeted failure tests: full journey coverage বনাম fast diagnosis; reliability অনুযায়ী test mix বেছে নিতে হয়।

    - **[57. Logging, metrics, tracing ও production debugging](https://learn.microsoft.com/en-us/dotnet/core/diagnostics/observability-with-otel)**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Logging**
        - `ILogger<T>`
        - Log levels
        - Categories
        - Structured message templates
        - EventId
        - Logging scopes
        - Exception logging
        - HTTP logging middleware
        - Request/response body logging policy
        - Redaction
        - Sampling
        - Source-generated logging — প্রয়োজনভিত্তিক
      - **Metrics**
        - Counters
        - Histograms
        - Gauges
        - Request duration
        - Request errors
        - Active requests
        - Pool saturation
        - Queue depth
        - Cardinality limits
      - **Tracing**
        - Activity
        - ActivitySource
        - TraceId
        - SpanId
        - Parent-child spans
        - W3C trace context
        - Baggage
        - HTTP ও database instrumentation
      - **OpenTelemetry**
        - Resource attributes
        - Service name/version
        - Instrumentation
        - OTLP exporter
        - Collector
        - Backend selection
        - Sampling policy
      - **Debugging**
        - Correlate logs, metrics ও traces
        - dotnet-counters
        - dotnet-trace
        - dotnet-dump
        - dotnet-monitor — প্রয়োজনভিত্তিক
        - Memory leak
        - Thread-pool starvation
        - Slow SQL
        - Request-path diagnosis

      - **Trade-offs**
        - Detailed logging: diagnosis সহজ; I/O, storage, privacy ও signal-to-noise cost বাড়ে।
        - High-cardinality metrics: fine-grained breakdown; memory/storage cost দ্রুত বাড়ে, user ID-এর মতো labels এড়ানোর design প্রয়োজন।
        - Full tracing ও sampling: complete request evidence বনাম lower cost; rare error visibility ও sampling policy সামঞ্জস্য করতে হয়।
        - Vendor SDK ও OpenTelemetry: vendor-specific convenience বনাম portability; exporter/backend capabilities আলাদা হতে পারে।

    - **Practical gate**
      - Real database integration tests, failure tests ও traces দিয়ে API behavior ব্যাখ্যা করা।

10. **Delivery ও operations — deploy, observe, recover**

    - **[58. Publishing, Linux hosting, containers ও reverse proxy](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/proxy-load-balancer?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Publish outputs**
        - Release build
        - Framework-dependent publish
        - Self-contained publish
        - Runtime Identifier
        - Single-file publish — প্রয়োজনভিত্তিক
        - Configuration ও secrets separation
      - **Linux hosting**
        - Process permissions
        - Working directory
        - systemd service
        - Environment configuration
        - Logs
        - Restart policy
        - Firewall ও listening ports
      - **Containers**
        - Dockerfile
        - Build context
        - .dockerignore
        - Multi-stage build
        - SDK ও runtime images
        - Non-root user
        - Exposed ও published ports
        - Volumes
        - Container networking
        - Image tags ও digests
        - Health checks
        - Compose for local dependencies
      - **Reverse proxy**
        - Nginx বা IIS
        - TLS certificate
        - TLS termination
        - Forwarded Headers Middleware
        - Known proxies/networks
        - Scheme ও host forwarding
        - PathBase
        - Upload/time-out limits
      - **Runtime operations**
        - Graceful termination
        - Read-only filesystem considerations
        - Persistent file/key storage
        - Startup diagnostics

      - **Trade-offs**
        - VM ও container: familiar process control বনাম reproducible packaging; image, networking ও orchestration knowledge যোগ হয়।
        - Framework-dependent ও self-contained: smaller artifact বনাম bundled runtime; runtime update ও artifact size trade-off থাকে।
        - Mutable tag ও pinned digest: সহজ update বনাম deterministic deployment; pinned image নিয়মিত refresh করতে হয়।
        - Proxy trust restrictions: authentic client metadata পাওয়া যায়; load-balancer topology বদলালে configuration maintain করতে হয়।

    - **59. CI/CD, release strategy ও supply-chain maintenance**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Continuous integration**
        - Restore
        - Build
        - Formatting/analyzers
        - Unit tests
        - Integration tests
        - Contract checks
        - Vulnerability scanning
        - Secret scanning
        - Package restore trust
        - License review
      - **Artifacts**
        - Versioned build artifact
        - Container registry
        - Immutable deployment artifact
        - SBOM — প্রয়োজনভিত্তিক
        - Artifact provenance — প্রয়োজনভিত্তিক
      - **Deployment pipeline**
        - Environment configuration
        - Secret injection
        - Workload identity
        - Staging
        - Migration step
        - Smoke tests
        - Deployment verification
        - Rollback trigger
      - **Infrastructure as code — প্রয়োজনভিত্তিক**
        - Bicep বা Terraform
        - Environment parameterization
        - Plan ও preview
        - State management
        - Drift detection
        - Secret-safe state storage
      - **Release strategy**
        - Rolling deployment
        - Blue-green deployment
        - Canary release
        - Backward-compatible APIs
        - Expand-contract database change
      - **Feature management — প্রয়োজনভিত্তিক**
        - Feature flags
        - Percentage rollout
        - Tenant targeting
        - Kill switch
        - Flag retirement
      - **Maintenance**
        - SDK ও runtime patches
        - Dependency updates
        - Breaking-change review
        - Reproducible builds

      - **Trade-offs**
        - Rolling ও blue-green: lower duplicate infrastructure cost বনাম fast environment switch; mixed-version compatibility বা extra capacity লাগে।
        - Canary ও all-at-once: limited exposure ও feedback বনাম simpler rollout; useful metrics ও traffic routing প্রয়োজন।
        - Feature flag: deploy ও release আলাদা করা যায়; stale flags, configuration combinations ও test matrix বাড়ে।
        - Auto dependency updates ও scheduled batches: faster patching বনাম controlled change volume; compatibility checks ও review ownership দরকার।

    - **[60. Cloud deployment, health checks, reliability ও recovery](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks?view=aspnetcore-10.0)**

      *Priority: অপরিহার্য · Depth: ব্যবহারিক*

      - **Hosting choices**
        - Managed web application hosting
        - Container hosting
        - Virtual machine
        - Azure App Service বা Container Apps
        - Equivalent AWS/GCP service — প্রয়োজনভিত্তিক
        - Kubernetes — বিশেষায়িত; পরিচিতি
        - Serverless constraints — বিশেষায়িত
      - **Health checks**
        - AddHealthChecks
        - MapHealthChecks
        - IHealthCheck
        - Healthy
        - Degraded
        - Unhealthy
        - Liveness
        - Readiness
        - Startup probe
        - Dependency checks
        - Probe endpoint access
      - **Scaling**
        - Multiple instances
        - Shared state ও key ring
        - Autoscaling signals
        - Connection budgets
        - Database capacity
        - Cache/broker capacity
      - **Reliability**
        - SLI
        - SLO
        - Error budget
        - Alert thresholds
        - Runbook
        - Incident triage
        - Post-incident review
      - **Recovery**
        - Database backups
        - Restore testing
        - Point-in-time recovery
        - RPO
        - RTO
        - Secret/key recovery
        - Regional outage plan — বিশেষায়িত
      - **Cost**
        - Compute
        - Storage
        - Egress
        - Logs/traces
        - Capacity headroom

      - **Trade-offs**
        - Managed hosting ও VM/Kubernetes: কম operational কাজ বনাম greater infrastructure control; cost ও team expertise অনুযায়ী নির্বাচন।
        - Liveness ও readiness: process restart decision বনাম traffic acceptance; dependency outage-কে অকারণে restart loop বানানো উচিত নয়।
        - Aggressive autoscaling: burst সামলানো যায়; downstream database সীমা ও extra cost নিয়ন্ত্রণ করতে হয়।
        - Frequent backups: smaller potential data-loss window; storage, runtime overhead ও restore complexity বাড়ে।
        - Tighter SLO: user reliability বাড়ে; engineering effort, redundancy ও capacity cost বাড়ে।

    - **[61. Runtime internals, Native AOT, Aspire ও legacy migration](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/aot/native-aot-tutorial?view=aspnetcore-10.0)**

      *Priority: প্রয়োজনভিত্তিক · Depth: পরিচিতি*

      - **Runtime understanding**
        - IL
        - JIT compilation
        - Tiered compilation
        - Dynamic PGO
        - Garbage collection generations
        - Large Object Heap
        - Server GC
        - Allocation profiling
      - **Advanced performance — বিশেষায়িত**
        - `Span<T>`
        - `Memory<T>`
        - `ArrayPool<T>`
        - System.IO.Pipelines
        - UTF-8 processing
        - Source generators
        - Reflection cost
      - **Native AOT**
        - Ahead-of-time compilation
        - Startup time
        - Deployment size
        - Trimming
        - Reflection compatibility
        - JSON source generation
        - Package compatibility
        - ASP.NET Core feature support
      - **[Aspire](https://aspire.dev/get-started/what-is-aspire/) — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - AppHost
        - Local service orchestration
        - Service defaults
        - Service discovery
        - Health ও telemetry integration
        - Deployment target separation
      - **Legacy migration — প্রয়োজনভিত্তিক; ব্যবহারিক**
        - .NET Framework Web API 2
        - System.Web ও ASP.NET Core boundary
        - Startup.cs ও minimal hosting
        - Newtonsoft.Json compatibility
        - Unsupported runtime upgrades
        - Authentication behavior changes
        - Package/provider compatibility
        - Incremental migration

      - **Trade-offs**
        - JIT ও Native AOT: mature dynamic feature support বনাম startup/memory advantages; framework ও package compatibility সীমা থাকতে পারে।
        - Low-level optimization: hot-path allocation কমতে পারে; complexity ও maintenance বাড়ে, profiling evidence প্রয়োজন।
        - Aspire orchestration: local multi-service setup সহজ; production deployment ও operational ownership আলাদাভাবে ঠিক করতে হয়।
        - Big-bang ও incremental migration: একবারে cleanup বনাম smaller rollout risk; transitional adapters ও দুই system maintain করতে হতে পারে।

    - **Practical gate**
      - CI দিয়ে staging deploy; health checks, migration plan ও rollback/recovery rehearsal।

11. **AI যুগে কাজ — engineering judgment ও optional AI features**

    - **62. AI-assisted backend development ও শেখার depth**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **নিজে গভীরভাবে বুঝতে হবে**
        - HTTP semantics
        - Data model ও invariants
        - DI lifetimes
        - Async ও cancellation
        - Authorization ও ownership
        - Transactions ও concurrency
        - SQL execution behavior
        - Error boundaries
        - Debugging
        - Security review
        - Operational failure modes
      - **AI/docs নিয়ে ব্যবহারিক implementation**
        - Endpoint boilerplate
        - DTO skeleton
        - Explicit mapping draft
        - Test skeleton
        - OpenAPI examples
        - Docker/CI draft
        - Routine refactoring
      - **AI workflow**
        - ছোট ও নির্দিষ্ট task
        - Acceptance criteria
        - Relevant project context
        - Version ও package constraints
        - Proposed diff inspection
        - Build
        - Targeted tests
        - Failure-case verification
        - Documentation check
        - Commit review
      - **Review questions**
        - Invented package/API আছে কি না
        - Lifetime mismatch আছে কি না
        - Cross-user বা cross-tenant leak আছে কি না
        - N+1 বা full-table scan হচ্ছে কি না
        - Retry duplicate effect তৈরি করছে কি না
        - Cancellation ও cleanup ঠিক কি না
        - Test শুধু implementation নকল করছে কি না
      - **Data handling**
        - Secrets বাদ দেওয়া
        - Production data minimization
        - Repository instruction boundaries
        - Untrusted content ও prompt injection

      - **Trade-offs**
        - AI-generated boilerplate: implementation দ্রুত হয়; correctness, version compatibility ও design ownership নিজের থাকে।
        - বড় change একবারে ও ছোট verified change: বেশি generation speed বনাম reviewability; বড় diff-এ subtle errors খুঁজে পাওয়া কঠিন।
        - AI-generated tests: coverage ideas দ্রুত আসে; independent expected behavior না দিলে tests একই ভুলকে বৈধ দেখাতে পারে।
        - Syntax memorization ও conceptual mastery: routine syntax docs থেকে পাওয়া যায়; design/debugging-এর জন্য execution model ও invariants নিজে বোঝা জরুরি।

    - **[63. LLM-enabled API features — optional specialization](https://genai.owasp.org/llm-top-10/)**

      *Priority: বিশেষায়িত · Depth: পরিচিতি*

      - **Integration foundations**
        - Model API client
        - Structured output
        - Schema validation
        - Streaming response
        - Cancellation
        - Timeout
        - Rate limits
        - Token budget
        - Cost tracking
      - **Retrieval**
        - Embeddings
        - Chunking
        - Vector search
        - Hybrid search
        - Retrieval-Augmented Generation
        - Source attribution
        - Retrieval evaluation
        - Tenant/user access filtering
      - **Tool calling**
        - Tool schema
        - Input validation
        - Least-privilege credentials
        - User authorization
        - Idempotent actions
        - Approval boundaries
      - **Safety ও reliability**
        - Prompt injection
        - Untrusted retrieved content
        - Sensitive-data leakage
        - Output validation
        - Hallucination evaluation
        - Regression datasets
        - Model/version changes
        - Trace redaction
        - Human review where required

      - **Trade-offs**
        - General generation ও retrieval: simple integration বনাম context-grounded answers; indexing, permissions ও evaluation যোগ হয়।
        - Larger model ও smaller model: capability/latency/cost-এর ভারসাম্য; task-specific evaluation দিয়ে নির্বাচন।
        - Model tool autonomy: workflow দ্রুত হয়; permission scope, irreversible action ও untrusted-input boundaries enforce করতে হয়।
        - Streaming: perceived latency কমে; partial output, client disconnect ও error recovery জটিল হয়।

    - **Practical gate**
      - AI-generated change-এর assumptions, authorization, SQL ও tests নিজে review এবং explain করা।

12. **Projects ও mastery milestones — শেখাকে backend দক্ষতায় রূপ দেওয়া**

    - **64. Progressive projects, review gates ও portfolio**

      *Priority: অপরিহার্য · Depth: গভীর*

      - **Project 1 — Single-service CRUD API**
        - Resource model
        - Controller বা Minimal API
        - Request DTO
        - Response DTO
        - Validation
        - ProblemDetails
        - OpenAPI
        - Logging
        - Unit tests
      - **Project 2 — Database-backed business API**
        - Relational model
        - EF Core relationships
        - Migrations
        - Filtering
        - Sorting
        - Pagination
        - Unique constraints
        - Concurrency conflict
        - Real-provider integration tests
      - **Project 3 — Authenticated multi-user API**
        - Identity provider বা Identity integration
        - Authentication
        - Role/permission policy
        - Ownership
        - Tenant isolation — প্রয়োজন হলে
        - CORS/CSRF policy
        - Security regression tests
      - **Project 4 — Production integration**
        - Typed HttpClient
        - Timeout ও retry
        - Idempotency
        - Webhook
        - Background processing
        - Cache
        - File/object storage — প্রয়োজন হলে
        - Traces ও metrics
      - **Project 5 — Delivery ও operations**
        - Container
        - CI pipeline
        - Staging deployment
        - Production configuration
        - Migration rollout
        - Health checks
        - Load test
        - Alert
        - Backup/restore rehearsal
        - Rollback বা roll-forward rehearsal
      - **Mastery check**
        - Request থেকে response পর্যন্ত flow ব্যাখ্যা
        - Generated SQL ব্যাখ্যা
        - Concurrent update predict ও reproduce
        - Cross-user access test
        - Failure case debug
        - নির্বাচিত design-এর একাধিক trade-off ব্যাখ্যা
        - AI ছাড়া ছোট feature design; docs দিয়ে implementation
      - **Portfolio**
        - README
        - Setup instructions
        - API examples
        - Architecture decisions
        - Test evidence
        - Deployment link
        - Known limitations
        - Measured performance result

      - **Trade-offs**
        - এক বড় project ও progressive projects: integrated domain depth বনাম ছোট feedback loops; scope নিয়ন্ত্রণ ও completion discipline জরুরি।
        - Feature count ও production correctness: বেশি demo capability বনাম reliable behavior; authorization, consistency ও tests ছাড়া CRUD count সীমিত মূল্য দেয়।
        - সব specialization শেখা ও role-focused selection: broad awareness বনাম দ্রুত practical mastery; job/project প্রয়োজন অনুযায়ী একটি branch গভীর করা।

    - **Practical gate**
      - একটি deployed API-এর request, database change, authorization decision ও production failure নিজে explain করা।
