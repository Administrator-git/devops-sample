# devops-sample

Optional step arguments
Pipeline follows the Groovy language convention of allowing parentheses to be omitted around method arguments.

Many Pipeline steps also use the named-parameter syntax as a shorthand for creating a Map in Groovy, which uses the syntax [key1: value1, key2: value2]. Making statements like the following functionally equivalent:

git url: 'git://example.com/amazing-project.git', branch: 'master'

git([url: 'git://example.com/amazing-project.git', branch: 'master'])

For convenience, when calling steps taking only one parameter (or only one mandatory parameter), the parameter name may be omitted, for example:

sh 'echo hello' /* short form  */

sh([script: 'echo hello'])  /* long form */

Agent Parameters:
** The "agent" section supports a few different types of parameters. These parameters can be applied at the top-level of the pipeline block or within each stage directive.
a). any: Execute the pipeline or stage on any available agent. For Example in pipeline: agent any
b). none: when applied at the top level of the pipeline block no global agent will be allocated for the entire pipeline run and each stage section will need to contain it's own agent section. For example in pipeline: agent none
c). label: Execute the pipeline or stage on an agent available in the jenkins environment with the provided label. For Example in pipeline: agent { label 'my-own-defined-label' }
    Label conditions can also be used. For example: agent { label 'my-label1 && my-label2' } or agent { label 'my-label1 || my-label2' }
d). node: agent { node { label 'labelName' } } behaves the same as agent { label 'labelName' }, but node allows for additional options (such as customWorkspace).
e). docker: * Execute the pipeline or stage, with the given container which will be dynamically provisoned on a node or on a node matching the optionally defined "label" parameter.
    * docker also optionally accepts an 'args' parameter which may contain arguments to pass directly to a 'docker run' invocation and an 'alwaysPull' option, which will force a docker pull even if the image name is already present. 
    For Example: agent { docker 'maven:3.8.1-adoptopenjdk-11' } or

agent {
    docker {
        image 'maven:3.8.1-adoptopenjdk-11'
        label 'my-defined-label'
        args  '-v /tmp:/tmp'
    }
}

   * docker also optionally accepts 'registryUrl' and 'registryCredentialsId' parameters which will help to specify the Docker Registry to use and it's credentials.The parameter registryCredentialsId could be used alone for private repositories within the docker hub. For Example:
   agent {
    docker {
        image 'myregistry.com/node'
        label 'my-defined-label'
        registryUrl 'https://myregistry.com/'
        registryCredentialsId 'myPredefinedCredentialsInJenkins'
    }
  }
f). dockerfile: * Execute the Pipeline, or stage, with a container built from a Dockerfile contained in the source repository.
                * In order to use this option, the Jenkinsfile must be loaded from either a Multibranch Pipeline or a Pipeline from SCM.
                * Conventionally this is the Dockerfile in the root of the source repository: agent { dockerfile true }.
                * If building a Dockerfile in another directory, use the dir option: agent { dockerfile { dir 'someSubDir' } }.
                * If your Dockerfile has another name, you can specify the file name with the filename option.
                * You can pass additional arguments to the docker build …​command with the additionalBuildArgs option, like agent { dockerfile { additionalBuildArgs '--build-arg foo=bar' } }.
                * For example, a repository with the file build/Dockerfile.build, expecting a build argument version:
           agent {
    // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
             dockerfile {
               filename 'Dockerfile.build'
               dir 'build'
               label 'my-defined-label'
               additionalBuildArgs  '--build-arg version=1.0.2'
               args '-v /tmp:/tmp'
             }
          }
                * dockerfile also optionally accepts a 'registryUrl' and 'registryCredentialsId' parameters which will help to specify the Docker Registry to use and its credentials. For example:
            agent {
              dockerfile {
                filename 'Dockerfile.build'
                dir 'build'
                label 'my-defined-label'
                registryUrl 'https://myregistry.com/'
                registryCredentialsId 'myPredefinedCredentialsInJenkins'
             }
          }
