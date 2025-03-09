#### Main commands:

**1. init:**          - Prepare your working directory for other commands
```
Usage: terraform [global options] init [options]
```
  Initialize a new or existing Terraform working directory by creating 
  initial files, loading any remote state, downloading modules, etc.   

  This is the first command that should be run for any new or existing 
  Terraform configuration per machine. This sets up all the local data 
  necessary to run Terraform that is typically not committed to version
  control.

  This command is always safe to run multiple times. Though subsequent runs
  may give errors, this command will never delete your configuration or
  state. Even so, if you have important information, please back it up prior        
  to running this command, just in case.
  
```
Options:

  -backend=false          Disable backend or HCP Terraform initialization
                          for this configuration and use what was previously        
                          initialized instead.

                          aliases: -cloud=false

  -backend-config=path    Configuration to be merged with what is in the
                          configuration file's 'backend' block. This can be
                          either a path to an HCL file with key/value
                          assignments (same format as terraform.tfvars) or a        
                          'key=value' format, and can be specified multiple
                          times. The backend type must be in the configuration      
                          itself.

  -force-copy             Suppress prompts about copying state data when
                          initializating a new state backend. This is
                          equivalent to providing a "yes" to all confirmation       
                          prompts.

  -from-module=SOURCE     Copy the contents of the given module into the target     
                          directory before initialization.

  -get=false              Disable downloading modules for this configuration.       

  -input=false            Disable interactive prompts. Note that some actions may   
                          require interactive prompts and will error if input is    
                          disabled.

  -lock=false             Don't hold a state lock during backend migration.
                          This is dangerous if others might concurrently run        
                          commands against the same workspace.

  -lock-timeout=0s        Duration to retry a state lock.

  -no-color               If specified, output won't contain any color.

  -json                   If specified, machine readable output will be
                          printed in JSON format.

  -plugin-dir             Directory containing plugin binaries. This overrides all  
                          default search paths for plugins, and prevents the        
                          automatic installation of plugins. This flag can be used  
                          multiple times.

  -reconfigure            Reconfigure a backend, ignoring any saved
                          configuration.

  -migrate-state          Reconfigure a backend, and attempt to migrate any
                          existing state.

  -upgrade                Install the latest module and provider versions
                          allowed within configured constraints, overriding the
                          default behavior of selecting exactly the version
                          recorded in the dependency lockfile.

  -lockfile=MODE          Set a dependency lockfile mode.
                          Currently only "readonly" is valid.

  -ignore-remote-version  A rare option used for HCP Terraform and the remote backend       
                          only. Set this to ignore checking that the local and remote       
                          Terraform versions use compatible state representations, making   
                          an operation proceed even when there is a potential mismatch.     
                          See the documentation on configuring Terraform with
                          HCP Terraform or Terraform Enterprise for more information.       

  -test-directory=path    Set the Terraform test directory, defaults to "tests".
  ```
  
**2. validate:**      - Check whether the configuration is valid
```
Usage: terraform [global options] validate [options]
```
  Validate the configuration files in a directory, referring only to the   
  configuration and not accessing any remote services such as remote state,
  provider APIs, etc.

  Validate runs checks that verify whether a configuration is syntactically
  valid and internally consistent, regardless of any provided variables or
  existing state. It is thus primarily useful for general verification of
  reusable modules, including correctness of attribute names and value types.

  It is safe to run this command automatically, for example as a post-save
  check in a text editor or as a test step for a re-usable module in a CI
  system.

  Validation requires an initialized working directory with any referenced
  plugins and modules installed. To initialize a working directory for
  validation without accessing any configured remote backend, use:
      terraform init -backend=false

  To verify configuration in the context of a particular run (a particular
  target workspace, input variable values, etc), use the 'terraform plan'
  command instead, which includes an implied validation check.
```
Options:

  -json                 Produce output in a machine-readable JSON format,
                        suitable for use in text editor integrations and other
                        automated systems. Always disables color.

  -no-color             If specified, output won't contain any color.

  -no-tests             If specified, Terraform will not validate test files.

  -test-directory=path  Set the Terraform test directory, defaults to "tests".
  ```

**3. plan:**          - Show changes required by the current configuration
  
**4. apply:**         - Create or update infrastructure
  
**5. destroy:**       - Destroy previously-created infrastructure
