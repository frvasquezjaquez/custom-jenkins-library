# SRC Directory

The src directory should look like standard Java source directory structure. This directory is added to the classpath when executing Pipelines.

# Samples

## 1. Global Vars

**file path**:  `bpd-jenkins-lib/src/org/bpd/GlobalVars.groovy`
```
#!/usr/bin/env groovy
package org.bpd

class GlobalVars {
   static String foo = "bar"

   // refer to this in a pipeline using:
   //
   // import org.bpd.GlobalVars
   // println GlobalVars.foo
}
```
**Use in pipeline**
```
@Library('library-name')_

import org.bpd.GlobalVars
pipeline {
    agent any
    stages {
        stage('Demo'){
            steps{
               echo 'The value of foo is : ' + GlobalVars.foo
            }
        }
    }
}
```

## 2. Create a class

**file path**:  `bpd-jenkins-lib/src/org/bpd/GlobalVars.groovy`
```
#!/usr/bin/env groovy
package org.bpd

class SampleClass {
   String name
   Integer age

   def increaseAge(Integer years) {
      this.age += years
   }
}
```
**Use in pipeline**
```
@Library('library-name')_

import org.bpd.SampleClass

pipeline {
    agent any
    stages {
        stage('Demo'){
            steps{
                script{
                    def person = new SampleClass()
                    person.age = 21
                    person.increaseAge(10)
                    echo 'Incremented age, is now : ' + person.age
                }
            }
        }
    }
}
```

## 3. Run steps commands

Library classes cannot directly call `steps` such as `sh` or `git`. The best approach is to pass `the steps` explicitly using this to a library class, in a constructor, or just one method.

**file path**:  `bpd-jenkins-lib/src/org/bpd/Utilities.groovy`
```
class Utilities implements Serializable {
  def steps
  Utilities(steps) {this.steps = steps}
  
  def mvn(args) {
    steps.sh "${steps.tool 'Maven'}/bin/mvn -o ${args}"
  }
}

```
**Use in pipeline**
```
@Library('utils')_

import org.bpd.Utilities
def utils = new Utilities(this)
pipeline {
    agent any
    stages {
        stage('Demo'){
            steps{
                script{
                    utils.mvn 'clean package'
                }
            }
        }
    }
}
```
