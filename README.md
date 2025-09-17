# Grid Forecast Engine

## General Information and Purpose

**Service Name/Title**: Grid Forecast Engine  
**Description and Purpose**: Provides loads and production forecast for MV and LV lines.  
**Owner/Contact Information**: Fabio Di Zazzo (Areti) <fabio.dizazzo@areti.it>  

---

## Functional Requirements

1. **MV Forecast**: Provide load and production forecasts for MV lines given line code and timeframe.  
2. **LV Forecast**: Provide load and production forecasts for LV lines given substation code and timeframe.  
3. **User Authentication and Authorization**: Protect resources and functionalities with proper authentication and authorization.  
4. **Audit Logging**: Track configuration modifications.  

---

## Non-Functional Requirements

- **Performance**: Forecasts calculation should be quick enough to leave time for optimization and/or corrective actions.  
- **Reliability and Availability**: The system should provide high availability (targeting 99%) and failover mechanisms.  
- **Security**:  
  - Authentication: Token-based authentication for both interactive and non-interactive methods.  
  - Authorization: Service operates mainly as a scheduled service, with manual intervention allowed for users with proper permissions.  
  - Data encryption and privacy compliance ensured.  
- **Privacy**: Compliant with data privacy regulations.  

---

## Service Interfaces

Resources are modelled after a **REST paradigm**.  

| Method | Path | Description |
|--------|------|-------------|
| **POST** | `[BASE_ADDRESS]/forecast/mv/{lineId}` | Returns forecast for an MV line |
| **POST** | `[BASE_ADDRESS]/forecast/lv/{substationId}` | Returns forecast for all LV lines under a single substation |
| **POST** | `[BASE_ADDRESS]/forecast/lv/{substationId}/{lvLineNumber}` | Returns forecast for a single LV line under a substation |

---

## Data Model

**TBD**  

---

## Integration and Dependencies

- **External dependencies**: TBD  
- **System dependencies**:  
  - IoT Platform: Dependent on the uplink channel for receiving up-to-date grid behaviour from non-substation sources.  
  - SCADAs: For receiving up-to-date grid behaviour from substations.  
  - Topology Provider: Must provide up-to-date or expected grid topology for the forecast timeframe.  
  - Databases, libraries, frameworks, and other internal tools.  
- **Third-party integrations**: TBD  
- **HEDGE-IOT Edge Devices/interfaces and cloud services integration**  
- **Integration with the App Store**: TBD  
- **Integration with the data space**: TBD  

---

## Security and Privacy

- **Data Sensitivity**: TBD  
- **Access Control**: API and Frontend usage requires authentication. Authenticated users may access only a subset of features based on their role and permissions.  
- **Audit Logs**: User actions that modify the system trigger audit log collection.  

---

## Performance Considerations

- Stress testing performed periodically.  
- Response times are continuously monitored.  

---

## Deployment and Environment

- **Configuration**: Environment-specific settings.  
- **CI/CD**: Continuous Integration/Deployment pipeline with:  
  - **Test Stage**:  
    - Audit: Check for known vulnerabilities at application and container level.  
    - Lint: Check for linting errors.  
    - Test: Run test suite.  
  - **Build Stage**:  
    - Build container image.  
    - Publish container image at a given registry.  
- **Monitoring and Logging**:  
  - Instrumented with Prometheus Metrics for resource consumption and application metrics.  
  - JSON logger for structured logging.  
  - OpenTelemetry-compatible traces.  

---

## Testing and Validation

- All commits are checked against a test suite.  
