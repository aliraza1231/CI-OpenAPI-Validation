# Minimal Alerts OpenAPI Example

This is a minimal OpenAPI specification that reproduces the schema validation warning:
**"The example value does not conform with the associated type of schema definition"**

## Structure

```
minimal-alerts-example/
├── spec/
│   ├── openapi.yaml                    # Main OpenAPI specification
│   ├── components/
│   │   └── schemas/
│   │       └── samples/
│   │           ├── alertsJson.yaml     # Contains the problematic example
│   │           └── errors400Json.yaml  # Error response example
│   └── paths/
│       ├── alerts.yaml                 # GET/POST /alerts endpoints
│       └── alerts_~id~.yaml           # GET/PUT/DELETE /alerts/{id} endpoints
└── redocly.yaml                        # Linting configuration
```

## The Warning

The validation warning is caused by an intentional type mismatch in `spec/components/schemas/samples/alertsJson.yaml` on line 15:

```yaml
"name": 12345,  # This should be a string but is a number
```

According to the schema definition in `openapi.yaml`, the `name` field should be of type `string`, but the example provides a number (`12345`).

## How to Reproduce

1. Navigate to the minimal example directory:
   ```bash
   cd minimal-alerts-example
   ```

2. Run the linter to see the validation error:
   ```bash
   redocly lint spec/openapi.yaml
   ```

3. You should see multiple instances of the error:
   ```
   Example value must conform to the schema: `name` property type must be string.
   ```

## Fixing the Warning

To fix the warning, change line 15 in `spec/components/schemas/samples/alertsJson.yaml` from:
```yaml
"name": 12345,
```
to:
```yaml
"name": "12345",
```

## API Endpoints

This minimal example includes all CRUD operations for the alerts endpoint:

- `GET /alerts` - Retrieve all alerts
- `POST /alerts` - Create a new alert
- `GET /alerts/{id}` - Retrieve a specific alert
- `PUT /alerts/{id}` - Update a specific alert
- `DELETE /alerts/{id}` - Delete a specific alert

All endpoints reference the same sample data that contains the schema validation issue.

## Usage

This example can be used to:
1. Demonstrate the schema validation warning to external teams
2. Test OpenAPI validation tools and linters
3. Understand how example validation works in OpenAPI specifications
4. Reproduce and debug similar schema validation issues
