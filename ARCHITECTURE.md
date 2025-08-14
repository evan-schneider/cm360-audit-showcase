# System Architecture

## Core Components
- **Main Engine** - 3,500+ lines of automation logic
- **Configuration UI** - HTML interfaces for management
- **External Config System** - Separated user settings from source code
- **Batch Processing** - Scalable execution across multiple teams

## Data Flow
1. **Email Integration** → Fetches campaign reports from labeled email threads
2. **File Processing** → Merges Excel/ZIP files, normalizes data structures
3. **Analysis Engine** → Applies team-specific rules and thresholds
4. **Report Generation** → Creates formatted Excel with conditional highlighting
5. **Distribution** → Sends targeted emails to team stakeholders

## Scalability Features
- **Configurable batch sizes** (default: 2 configs per batch)
- **Automatic batch function generation** for new team additions
- **Execution time limit handling** through intelligent chunking
- **Parallel processing coordination** with conflict avoidance

## Security Architecture
- **External configuration separation** - User settings isolated from source code
- **Role-based access control** through configuration sheet permissions
- **Staging vs production modes** with admin override capabilities
- **Authorization monitoring** with automatic reauth workflows

## Processing Pipeline

### Stage 1: Data Acquisition
- Gmail API integration with label-based filtering
- Multi-format file support (Excel, CSV, ZIP archives)
- Intelligent header detection and data normalization

### Stage 2: Business Logic Engine
`
Campaign Data → Threshold Evaluation → Exclusions Filter → Flag Generation
`

### Stage 3: Report Assembly
- Dynamic sorting (flagged items prioritized by volume)
- Conditional formatting and highlighting
- Excel export with embedded business rules

### Stage 4: Distribution
- Team-specific recipient resolution
- Attachment optimization and email quota management
- Summary reporting for administrative oversight

## Design Patterns
- **Factory Pattern** - Configuration management
- **Strategy Pattern** - Multiple exclusion types
- **Observer Pattern** - Trigger management
- **Template Method** - Standardized audit workflow

## Performance Optimizations
- **Batched spreadsheet operations** to minimize API calls
- **Smart caching** of configuration data and results
- **Efficient Drive folder management** with path optimization
- **Conditional processing** to skip unnecessary operations
