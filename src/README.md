# SRC Directory

The src directory should look like standard Java source directory structure. This directory is added to the classpath when executing Pipelines.

# Samples

## Global Vars

```
#!/usr/bin/env groovy
package com.cleverbuilder

class GlobalVars {
   static String foo = "bar"

   // refer to this in a pipeline using:
   //
   // import com.cleverbuilder.GlobalVars
   // println GlobalVars.foo
}
```

## Create a class

```
#!/usr/bin/env groovy
package com.cleverbuilder

class GlobalVars {
   static String foo = "bar"

   // refer to this in a pipeline using:
   //
   // import com.cleverbuilder.GlobalVars
   // println GlobalVars.foo
}
```