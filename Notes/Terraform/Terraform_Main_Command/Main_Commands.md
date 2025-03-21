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
```
Usage: terraform [global options] plan [options]
```
  Generates a speculative execution plan, showing what actions Terraform
  would take to apply the current configuration. This command will not
  actually perform the planned actions.

  You can optionally save the plan to a file, which you can then pass to
  the "apply" command to perform exactly the actions described in the plan.

Plan Customization Options:

  The following options customize how Terraform will produce its plan. You
  can also use these options when you run "terraform apply" without passing
  it a saved plan, in order to plan and apply in a single command.
  
```
  -destroy            Select the "destroy" planning mode, which creates a plan
                      to destroy all objects currently managed by this
                      Terraform configuration instead of the usual behavior.

  -refresh-only       Select the "refresh only" planning mode, which checks
                      whether remote objects still match the outcome of the
                      most recent Terraform apply but does not propose any
                      actions to undo any changes made outside of Terraform.

  -refresh=false      Skip checking for external changes to remote objects
                      while creating the plan. This can potentially make
                      planning faster, but at the expense of possibly planning
                      against a stale record of the remote system state.

  -replace=resource   Force replacement of a particular resource instance using
                      its resource address. If the plan would've normally
                      produced an update or no-op action for this instance,
                      Terraform will plan to replace it instead. You can use
                      this option multiple times to replace more than one object.

  -target=resource    Limit the planning operation to only the given module,
                      resource, or resource instance and all of its
                      dependencies. You can use this option multiple times to
                      include more than one object. This is for exceptional
                      use only.

  -var 'foo=bar'      Set a value for one of the input variables in the root
                      module of the configuration. Use this option more than
                      once to set more than one variable.

  -var-file=filename  Load variable values from the given file, in addition
                      to the default files terraform.tfvars and *.auto.tfvars.
                      Use this option more than once to include more than one
                      variables file.

Other Options:

  -compact-warnings          If Terraform produces any warnings that are not
                             accompanied by errors, shows them in a more compact
                             form that includes only the summary messages.

  -detailed-exitcode         Return detailed exit codes when the command exits.
                             This will change the meaning of exit codes to:
                             0 - Succeeded, diff is empty (no changes)
                             1 - Errored
                             2 - Succeeded, there is a diff

  -generate-config-out=path  (Experimental) If import blocks are present in
                             configuration, instructs Terraform to generate HCL
                             for any imported resources not already present. The
                             configuration is written to a new file at PATH,
                             which must not already exist. Terraform may still
                             attempt to write configuration if the plan errors.

  -input=true                Ask for input for variables if not directly set.

  -lock=false                Don't hold a state lock during the operation. This
                             is dangerous if others might concurrently run
                             commands against the same workspace.

  -lock-timeout=0s           Duration to retry a state lock.

  -no-color                  If specified, output won't contain any color.

  -out=path                  Write a plan file to the given path. This can be
                             used as input to the "apply" command.

  -parallelism=n             Limit the number of concurrent operations. Defaults
                             to 10.

  -state=statefile           A legacy option used for the local backend only.
                             See the local backend's documentation for more
                             information.
```                      
  
**4. apply:**         - Create or update infrastructure
```
Usage: terraform [global options] apply [options] [PLAN]
```
  Creates or updates infrastructure according to Terraform configuration
  files in the current directory.

  By default, Terraform will generate a new plan and present it for your
  approval before taking any action. You can optionally provide a plan
  file created by a previous call to "terraform plan", in which case
  Terraform will take the actions described in that plan without any
  confirmation prompt.
  
```
Options:

  -auto-approve          Skip interactive approval of plan before applying.

  -backup=path           Path to backup the existing state file before
                         modifying. Defaults to the "-state-out" path with
                         ".backup" extension. Set to "-" to disable backup.

  -compact-warnings      If Terraform produces any warnings that are not
                         accompanied by errors, show them in a more compact
                         form that includes only the summary messages.

  -destroy               Destroy Terraform-managed infrastructure.
                         The command "terraform destroy" is a convenience alias
                         for this option.

  -lock=false            Don't hold a state lock during the operation. This is
                         dangerous if others might concurrently run commands
                         against the same workspace.

  -lock-timeout=0s       Duration to retry a state lock.

  -input=true            Ask for input for variables if not directly set.

  -no-color              If specified, output won't contain any color.

  -parallelism=n         Limit the number of parallel resource operations.
                         Defaults to 10.

  -state=path            Path to read and save state (unless state-out
                         is specified). Defaults to "terraform.tfstate".

  -state-out=path        Path to write state to that is different than
                         "-state". This can be used to preserve the old
                         state.

  -var 'foo=bar'         Set a value for one of the input variables in the root
                         module of the configuration. Use this option more than
                         once to set more than one variable.

  -var-file=filename     Load variable values from the given file, in addition
                         to the default files terraform.tfvars and *.auto.tfvars.
                         Use this option more than once to include more than one
                         variables file.
```
  If you don't provide a saved plan file then this command will also accept
  all of the plan-customization options accepted by the terraform plan command.
  For more information on those options, run:
  ```
      terraform plan -help
  ```

**5. destroy:**       - Destroy previously-created infrastructure
```
Usage: terraform [global options] destroy [options]
```
  Destroy Terraform-managed infrastructure.

  This command is a convenience alias for:
```
      terraform apply -destroy
```

  This command also accepts many of the plan-customization options accepted by
  the terraform plan command. For more information on those options, run:
      terraform plan -help
