
### **YAML**
is a human-readable data serialization format used mainly for configuration files.
YAML is designed to be easy for both people and machines to read and write.

### Key Characteristics of YAML

1. **Human-Readable** 🧑‍💻
    
    - YAML uses indentation and whitespace instead of symbols like `{}`, `:`, or `,`, making it more intuitive and easier to read.
2. **Data Serialization Format** 📜
    
    - YAML is not a programming language; instead, it is a format for structuring and representing data, typically used in configuration files.
3. **Flexible Data Types** 📂
    
    - YAML supports various data types, including:
        - **Scalars**: Single values like strings, numbers, booleans
        - **Lists**: Ordered sequences of items
        - **Dictionaries** (or maps): Key-value pairs, similar to JSON objects
4. **Widely Used in Configuration Files** 🛠️
    
    - YAML is the preferred format for many configuration files in software development and DevOps tools, like Ansible, Kubernetes, Docker Compose, and more.

### YAML Syntax Basics
**Key-Value Pairs**:
```
name: John Doe
age: 30

```
**Lists**:
```
hobbies:
  - reading
  - hiking
  - coding

```
**Nested Structures**:
```
address:
  street: 123 Main St
  city: Springfield
  zip: 12345

```
**Lists of Dictionaries**:
```
employees:
  - name: Alice
    role: Developer
  - name: Bob
    role: Manager

```
Examples of YAML Use Cases
**Docker Compose**
**Kubernetes Configuration**
**Ansible Playbook**