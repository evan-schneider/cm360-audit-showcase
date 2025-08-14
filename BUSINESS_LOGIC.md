# Business Logic & Audit Rules Engine

## Audit Rules Framework

### Core Flag Types

#### 1. Volume Anomaly Detection (Clicks > Impressions)
**Purpose**: Identifies potential data quality issues where click counts exceed impression counts.

**Business Impact**: 
- Prevents billing discrepancies
- Identifies tracking implementation issues
- Ensures data integrity for reporting

**Implementation Logic**:
`
IF (campaign_volume >= threshold) AND (clicks > impressions) AND (not_excluded)
THEN flag_as_volume_anomaly
`

#### 2. Flight Date Compliance (Out of Flight Dates)
**Purpose**: Monitors campaigns running outside their scheduled date ranges.

**Business Impact**:
- Ensures proper campaign lifecycle management
- Prevents unauthorized spending
- Maintains campaign schedule compliance

**Implementation Logic**:
`
IF (campaign_volume >= threshold) AND (current_date NOT BETWEEN start_date AND end_date) AND (not_excluded)
THEN flag_as_flight_violation
`

#### 3. Creative Specification Validation (Pixel Size Mismatch)
**Purpose**: Detects mismatches between creative pixel sizes and placement specifications.

**Business Impact**:
- Prevents display rendering issues
- Ensures creative quality standards
- Maintains brand presentation consistency

**Implementation Logic**:
`
IF (campaign_volume >= threshold) AND (creative_pixels != placement_pixels) AND (not_excluded)
THEN flag_as_specification_mismatch
`

#### 4. Fallback Creative Monitoring (Default Ad Serving)
**Purpose**: Alerts when ads are serving from default/fallback creatives.

**Business Impact**:
- Identifies campaign setup issues
- Prevents poor user experience
- Ensures intended creative delivery

**Implementation Logic**:
`
IF (campaign_volume >= threshold) AND (ad_type CONTAINS "default") AND (not_excluded)
THEN flag_as_fallback_serving
`

## Smart Threshold System

### Dynamic Volume Assessment
The system intelligently selects evaluation criteria based on campaign performance patterns:

`javascript
// Pseudo-code demonstrating dynamic threshold logic
const impressionVolume = Number(row.impressions);
const clickVolume = Number(row.clicks);

// Determine primary metric for threshold evaluation
const primaryMetric = Math.max(impressionVolume, clickVolume);
const thresholdMet = (
  impressionVolume >= teamThresholds.minImpressions || 
  clickVolume >= teamThresholds.minClicks
);

if (thresholdMet && meetsFlagCriteria) {
  applyFlag();
}
`

### Threshold Benefits
- **Volume-Appropriate Sensitivity** - Avoids flagging low-impact campaigns
- **Team Customization** - Different sensitivity levels per team
- **Metric Flexibility** - Adapts to impression-heavy vs click-heavy campaigns
- **False Positive Reduction** - Focuses attention on significant issues

## Advanced Exclusions Engine

### Exclusion Strategies

#### 1. Placement ID Exclusions
**Use Case**: Known exceptions requiring permanent exclusion
**Example**: Test placements, specific partner arrangements
**Scope**: Exact match on placement identifier

#### 2. Site Name Exclusions  
**Use Case**: Platform-specific behavior patterns
**Example**: YouTube pre-roll campaigns, social media placements
**Scope**: All placements from specified sites

#### 3. Name Fragment Exclusions
**Use Case**: Campaign naming convention patterns
**Example**: Campaigns containing "test", "social", "video"
**Scope**: Partial string matching in placement names

### Exclusion Hierarchy
`
Global Exclusions (all flags) → Flag-Specific Exclusions → Volume Thresholds → Flag Evaluation
`

## Processing Intelligence

### Priority-Based Processing
1. **Volume Sorting** - Higher impact issues surface first
2. **Flag Categorization** - Different highlighting for different issue types
3. **Context Preservation** - Maintains audit trail for exclusion decisions
4. **Batch Optimization** - Efficient processing across large datasets

### Quality Assurance Features
- **Data Validation** - Input sanitization and format standardization
- **Consistency Checking** - Cross-validation of configuration settings
- **Error Recovery** - Graceful handling of malformed data
- **Audit Logging** - Comprehensive tracking of all processing decisions

## Business Value Delivery

### Operational Efficiency
- **Automated Detection** - Eliminates manual QA processes
- **Intelligent Filtering** - Reduces false positive noise
- **Prioritized Reporting** - Focuses attention on high-impact issues
- **Scalable Processing** - Handles enterprise-scale campaign volumes

### Risk Mitigation
- **Compliance Monitoring** - Ensures adherence to campaign parameters
- **Quality Assurance** - Maintains creative and technical standards
- **Data Integrity** - Validates tracking and measurement accuracy
- **Process Standardization** - Consistent evaluation across all teams
