## Terraform Block 


**Terraform block hierarchy** consists of several levels of nested blocks that define the configuration of infrastructure resources. Here's a high-level breakdown of the hierarchy and its structure in a visual diagram form:

---

### **Terraform Block Hierarchy Overview**

1. **Terraform Configuration File**
   - Top-level file containing all Terraform configuration.
   - Consists of multiple blocks.

2. **Blocks**
   - Key components like `provider`, `resource`, `data`, `module`, `output`, and `variable`.

3. **Attributes**
   - Key-value pairs or nested structures within blocks.

---

### **Diagram**

```plaintext
Terraform Configuration File (.tf or .tf.json)
├── terraform (Block)
│   ├── backend
│   └── required_providers
├── provider (Block)
│   └── provider-specific configuration
├── resource (Block)
│   ├── type (e.g., aws_instance, google_compute_instance)
│   └── attributes
├── module (Block)
│   ├── source
│   ├── variables
│   └── outputs
├── data (Block)
│   ├── type (e.g., aws_ami)
│   └── attributes
├── variable (Block)
│   ├── type
│   ├── default
│   └── description
├── output (Block)
│   └── value
└── locals (Block)
    └── key-value pairs for reusable values
```

---
