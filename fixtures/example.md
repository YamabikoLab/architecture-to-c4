# Example Architecture

## 3. Context and Scope

### External Context

| ID | Name | Type | Summary |
| --- | --- | --- | --- |
| EXT_CLIENT | Client | External System | Sends architecture input. |

## 4. Solution Strategy

### Process Flow Views

#### Generation {#PV_GENERATION kind=normal}

| From | To | Kind | Meaning |
| --- | --- | --- | --- |
| EXT_CLIENT | RESP_GENERATE | normal | Requests generation. |

## 5. Building Block View

### Responsibility Inventory

| ID | Responsibility | Summary |
| --- | --- | --- |
| RESP_GENERATE | Generate DSL | Generates Structurizr DSL. |

### Ownership Boundaries

| ID | Name | Includes |
| --- | --- | --- |
| BOUNDARY_EXTERNAL | External | EXT_CLIENT |
| BOUNDARY_TOOL | Tool | RESP_GENERATE |

### Dependencies

| Dependent | Depends on | Reason |
| --- | --- | --- |
| RESP_GENERATE | EXT_CLIENT | Receives architecture input. |

### Dependency Views

| ID | Name | Includes |
| --- | --- | --- |
| DV_GENERATION | Generation dependencies | EXT_CLIENT RESP_GENERATE |

### Responsibility Details

#### Generate DSL {#RESP_GENERATE}

## 6. Runtime View

### Generate workspace {#RV_GENERATION}

| Step | Source | Target | Interaction |
| ---: | --- | --- | --- |
| 1 | EXT_CLIENT | RESP_GENERATE | Provides architecture input. |
