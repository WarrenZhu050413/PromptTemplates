Analyze how a specific feature is implemented across the full stack by tracing data flow: $ARGUMENTS

Follow these steps:
1. **Parse feature description**: Break down the feature requirements and identify key components (data collection, storage, API, UI)
2. **Search backend data sources**: Use Grep and Task tools to find data collection mechanisms, external APIs, monitoring exporters, file systems
3. **Analyze database schema**: Read model definitions, examine relationships, field types, and migration patterns
4. **Trace data transformation**: Find Django views, DRF serializers, business logic, and Celery tasks for async operations
5. **Map API endpoints**: Identify URL routing, authentication/permissions, query parameters, and filtering capabilities
6. **Examine frontend implementation**: Locate React components, state management, data fetching patterns, and real-time update mechanisms
7. **Document data flow**: Create a comprehensive flow diagram showing: Source → Backend → Database → API → Frontend → UI
8. **Identify patterns and conventions**: Note architecture patterns, naming conventions, mental models, and design principles

**Implementation Guidelines**:
- Use Task tool for broad searches across multiple files and complex investigations
- Use Grep for specific pattern matching and targeted searches
- Use Read tool to examine specific files identified during search
- Focus on actual implementation with specific file paths and line numbers
- Document missing components or broken data flows
- Identify integration points between different system layers

**Output Structure**:
1. **Backend Data Fetching**: External APIs, database queries, data sources, collection methods
2. **Database Schema**: Model definitions, relationships, constraints, indexes, migration patterns
3. **Views and Data Transformation**: Django views, serializers, business logic, Celery tasks
4. **URL/API Endpoints**: Routing structure, authentication, permissions, parameters
5. **UI Display**: React components, state management, real-time updates, user interactions
6. **Data Flow Diagram**: Complete source-to-UI flow visualization
7. **Key Patterns**: Architecture conventions, naming patterns, mental models
8. **Performance Considerations**: Caching, optimization, scaling, monitoring

**Analysis Focus**:
- Trace actual code implementation, not theoretical design
- Identify missing or incomplete implementations
- Document integration patterns between frontend and backend
- Note real-time update mechanisms (WebSocket, polling, etc.)
- Review performance optimization strategies

IMPORTANT: Always provide specific file paths and line numbers for all findings. Focus on actual implementation rather than assumptions.