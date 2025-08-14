# Enterprise Configuration Management

## Multi-Team Architecture

### Scalable Configuration System
The system supports multiple independent team configurations, each with:

- **Isolated Gmail labels and filters** for data acquisition
- **Dedicated Drive folder hierarchies** for file organization
- **Team-specific recipient lists** with CC functionality
- **Custom threshold settings** per team and flag type
- **Independent exclusion rules** for false positive management

### Configuration Isolation Benefits
- **Security** - Teams only access their own configurations
- **Flexibility** - Each team can optimize thresholds for their campaigns
- **Scalability** - New teams can be added without affecting existing workflows
- **Maintenance** - Configuration changes don't impact source code

## External Configuration Architecture

### Separation of Concerns
`
Source Code (Private) ←→ Configuration Sheets (Shared) ←→ End Users
`

### Configuration Components

#### 1. Recipients Management
- **Primary Recipients** - Main notification targets
- **CC Recipients** - Secondary stakeholders
- **Active Status** - Enable/disable team configurations
- **No-Flag Email Control** - Option to suppress "no issues" notifications

#### 2. Thresholds Configuration
- **Flag Type Mapping** - Different rules for different issue types
- **Volume Thresholds** - Minimum impressions/clicks for flag activation
- **Team Customization** - Independent sensitivity settings
- **Active Status** - Enable/disable specific threshold rules

#### 3. Exclusions Management
- **Placement ID Exclusions** - Specific placement overrides
- **Site Name Exclusions** - Entire site filtering
- **Name Fragment Exclusions** - Pattern-based campaign filtering
- **Global vs Flag-Specific** - Flexible rule application scope

## Configuration Workflow

### Setup Process
1. **Initial Deployment** - Source code deployed to Google Apps Script
2. **External Sheet Creation** - Configuration spreadsheet established
3. **Team Onboarding** - Gmail labels, Drive folders, and settings configured
4. **Validation Testing** - Configuration validation and test audits
5. **Production Activation** - Daily triggers enabled

### Ongoing Management
- **Self-Service Configuration** - Teams can modify their own settings
- **Real-Time Validation** - Dropdown lists prevent configuration errors
- **Sync Mechanisms** - Changes propagated between systems
- **Audit Trail** - Configuration changes tracked and logged

## Business Logic Configuration

### Flag Type Definitions
- **clicks_greater_than_impressions** - Volume anomaly detection
- **out_of_flight_dates** - Campaign timing compliance
- **pixel_size_mismatch** - Creative specification validation
- **default_ad_serving** - Fallback creative monitoring

### Threshold Strategy
`
Configuration → Volume Assessment → Threshold Selection → Flag Evaluation
`

### Exclusion Hierarchy
1. **Global Exclusions** (apply to all flag types)
2. **Flag-Specific Exclusions** (apply to individual flag types)
3. **Volume Thresholds** (minimum activity levels)
4. **Active Status** (enable/disable rules)

## Configuration Metrics

### System Coverage
- **Multiple team configurations** actively managed
- **Flexible threshold matrix** (teams × flag types)
- **Comprehensive exclusion rules** across placement types
- **Automated validation** preventing configuration errors

### Operational Benefits
- **Reduced false positives** through intelligent exclusions
- **Team autonomy** in configuration management
- **Consistent reporting** across all teams
- **Scalable architecture** for organizational growth
