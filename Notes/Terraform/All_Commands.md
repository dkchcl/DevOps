## Terraform Commands:
```
terraform --help
```

#### Main commands:

**1. init:**          - Prepare your working directory for other commands
  
**2. validate:**      - Check whether the configuration is valid
  
**3. plan:**          - Show changes required by the current configuration
  
**4. apply:**         - Create or update infrastructure
  
**5. destroy:**       - Destroy previously-created infrastructure

#### All other commands:
  
  **1. console:**       - Try Terraform expressions at an interactive command prompt
```
terraform console --help
```
```
  Usage: terraform [global options] console [options]
```
  Starts an interactive console for experimenting with Terraform
  interpolations.

  This will open an interactive console that you can use to type
  interpolations into and inspect their values. This command loads the
  current state. This lets you explore and test interpolations before
  using them in future configurations.

  This command will never modify your state.
```
Options:

  -state=path       Legacy option for the local backend only. See the local
                    backend's documentation for more information.

  -plan             Create a new plan (as if running "terraform plan") and
                    then evaluate expressions against its planned state,
                    instead of evaluating against the current state.
                    You can use this to inspect the effects of configuration
                    changes that haven't been applied yet.

  -var 'foo=bar'    Set a variable in the Terraform configuration. This
                    flag can be set multiple times.

  -var-file=foo     Set variables in the Terraform configuration from
                    a file. If "terraform.tfvars" or any ".auto.tfvars"
                    files are present, they will be automatically loaded.
```
  
  **2. fmt:**           - Reformat your configuration in the standard style
  ```
terraform fmt --help
```
```
Usage: terraform [global options] fmt [options] [target...]
```
  Rewrites all Terraform configuration files to a canonical format. All
  configuration files (.tf), variables files (.tfvars), and testing files
  (.tftest.hcl) are updated. JSON files (.tf.json, .tfvars.json, or
  .tftest.json) are not modified.

  By default, fmt scans the current directory for configuration files. If you
  provide a directory for the target argument, then fmt will scan that
  directory instead. If you provide a file, then fmt will process just that
  file. If you provide a single dash ("-"), then fmt will read from standard
  input (STDIN).

  The content must be in the Terraform language native syntax; JSON is not
  supported.
```
Options:

  -list=false    Don't list files whose formatting differs
                 (always disabled if using STDIN)

  -write=false   Don't write to source files
                 (always disabled if using STDIN or -check)

  -diff          Display diffs of formatting changes

  -check         Check if the input is formatted. Exit status will be 0 if all
                 input is properly formatted and non-zero otherwise.

  -no-color      If specified, output won't contain any color.

  -recursive     Also process files in subdirectories. By default, only the
                 given directory (or current directory) is processed.
```

**3. force-unlock:**  - Release a stuck lock on the current workspace
```
terraform force-unlock --help
```
```
Usage: terraform [global options] force-unlock LOCK_ID
```
  Manually unlock the state for the defined configuration.

  This will not modify your infrastructure. This command removes the lock on the
  state for the current workspace. The behavior of this lock is dependent
  on the backend being used. Local state files cannot be unlocked by another
  process.
```
Options:

  -force                 Don't ask for input for unlock confirmation.
```
  
**4. get:**           - Install or upgrade remote Terraform modules
```
terraform get --help
```
```
Usage: terraform [global options] get [options]
```
  Downloads and installs modules needed for the configuration in the
  current working directory.

  This recursively downloads all modules needed, such as modules
  imported by modules imported by the root and so on. If a module is
  already downloaded, it will not be redownloaded or checked for updates
  unless the -update flag is specified.

  Module installation also happens automatically by default as part of
  the "terraform init" command, so you should rarely need to run this
  command separately.
```
Options:

  -update               Check already-downloaded modules for available updates
                        and install the newest versions available.

  -no-color             Disable text coloring in the output.

  -test-directory=path  Set the Terraform test directory, defaults to "tests".
```
  
**5. graph:**         - Generate a Graphviz graph of the steps in an operation
```
terraform graph --help
```
```
Usage: terraform [global options] graph [options]
```
  Produces a representation of the dependency graph between different
  objects in the current configuration and state.

  By default the graph shows a summary only of the relationships between
  resources in the configuration, since those are the main objects that
  have side-effects whose ordering is significant. You can generate more
  detailed graphs reflecting Terraform's actual evaluation strategy
  by specifying the -type=TYPE option to select an operation type.

  The graph is presented in the DOT language. The typical program that can
  read this format is GraphViz, but many web services are also available
  to read this format.
```
Options:

  -plan=tfplan     Render graph using the specified plan file instead of the
                   configuration in the current directory. Implies -type=apply.

  -draw-cycles     Highlight any cycles in the graph with colored edges.
                   This helps when diagnosing cycle errors. This option is
                   supported only when illustrating a real evaluation graph,
                   selected using the -type=TYPE option.

  -type=TYPE       Type of operation graph to output. Can be: plan,
                   plan-refresh-only, plan-destroy, or apply. By default
                   Terraform just summarizes the relationships between the
                   resources in your configuration, without any particular
                   operation in mind. Full operation graphs are more detailed
                   but therefore often harder to read.

  -module-depth=n  (deprecated) In prior versions of Terraform, specified the
                   depth of modules to show in the output.
```

**6. import:**        - Associate existing infrastructure with a Terraform resource
```
terraform import --help
```
```
Usage: terraform [global options] import [options] ADDR ID
```
  Import existing infrastructure into your Terraform state.

  This will find and import the specified resource into your Terraform
  state, allowing existing infrastructure to come under Terraform
  management without having to be initially created by Terraform.

  The ADDR specified is the address to import the resource to. Please
  see the documentation online for resource addresses. The ID is a
  resource-specific ID to identify that resource being imported. Please
  reference the documentation for the resource type you're importing to
  determine the ID syntax to use. It typically matches directly to the ID
  that the provider uses.

  This command will not modify your infrastructure, but it will make
  network requests to inspect parts of your infrastructure relevant to
  the resource being imported.
```
Options:

  -config=path            Path to a directory of Terraform configuration files
                          to use to configure the provider. Defaults to pwd.
                          If no config files are present, they must be provided
                          via the input prompts or env vars.

  -input=false            Disable interactive input prompts.

  -lock=false             Don't hold a state lock during the operation. This is
                          dangerous if others might concurrently run commands
                          against the same workspace.

  -lock-timeout=0s        Duration to retry a state lock.

  -no-color               If specified, output won't contain any color.

  -var 'foo=bar'          Set a variable in the Terraform configuration. This
                          flag can be set multiple times. This is only useful
                          with the "-config" flag.

  -var-file=foo           Set variables in the Terraform configuration from
                          a file. If "terraform.tfvars" or any ".auto.tfvars"
                          files are present, they will be automatically loaded.

  -ignore-remote-version  A rare option used for the remote backend only. See
                          the remote backend documentation for more information.

  -state, state-out, and -backup are legacy options supported for the local
  backend only. For more information, see the local backend's documentation.
```
  
  login         Obtain and save credentials for a remote host
  
  logout        Remove locally-stored credentials for a remote host
  
  metadata      Metadata related commands
  
  modules       Show all declared modules in a working directory
  
  output        Show output values from your root module
  
  providers     Show the providers required for this configuration
  
  refresh       Update the state to match remote systems
  
  show          Show the current state or a saved plan
  
  state         Advanced state management
  
  taint         Mark a resource instance as not fully functional
  
  test          Execute integration tests for Terraform modules
  
  untaint       Remove the 'tainted' state from a resource instance
  
  version       Show the current Terraform version
  
  workspace     Workspace management


#### Global options (use these before the subcommand, if any):

  -chdir=DIR    Switch to a different working directory before executing the
                given subcommand.
  
  -help         Show this help output, or the help for a specified subcommand.
  
  -version      An alias for the "version" subcommand.
