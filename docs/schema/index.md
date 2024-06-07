# Schema File

Schema is the definition which matches user's data model such as database schema. It encompasses the basic constraints and relationships between entities. The schema file is written in YAML format and contains the two required properties:
- **name**: The name of the schema, which serves as an ID to pair with the plan file.
- **entities**: A set of entity definitions. At least one entity is required. Entities with the same name are considered duplicates, and this will cause the data generation to fail.

:::tip
A schema should be defined using alphanumerical characters and underscore only. If you have other characters in your data model, you can use them as alias in output control file. 
:::

## Entity
An entity is the fundamental unit of data generation. It represents a distinct and recognizable object in the data model. The data for each entity will be stored in a distinct output file. An entity consists of two mandatory properties:

- **name**: The name of the entity serves as an identifier; no two entities can have the same name.
- **properties**: A set of property definitions. At least one property is required.

```yaml title="Sample schema comprise 'users' entity with single 'id' property"
name: "quickstart"
entities:
  - name: "users"
    properties:
      - name: "id"
        type: "sequence"
``` 

### Property
A property is a field in an entity that represents a specific attribute of the entity. Each property includes the following fields:

- **name**: [required] Serves as an identifier; no two properties can have the same name under the same entity.
- **[type](./schema/data-type)**: [required] Specifies the target data type.
- **[index](./schema/property-index)**: An index enforces a unique constraint on one or multiple properties under the same entity.
- **[constraints](./schema/constraints)**: A list of redefined constraints that provide rules for data generation.
- **[reference](./schema/reference)**: Refers to a property in another entity.

```yaml title="Sample 'country' entity with three properties"
  - name: country
    properties:
      - name: "id"
        type: "sequence"
        index:
          id: 0
      - name: "name"
        type: "text"
        constraints:
          - type: size
            min: 5
            max: 20
      - name: "code"
        type: "text"
        constraints:
          - type: "length"
            max: 2
          - type: "char_group"
            groups:
              - "ascii_uppercase_letters"
```