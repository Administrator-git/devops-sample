# devops-sample

Optional step arguments
Pipeline follows the Groovy language convention of allowing parentheses to be omitted around method arguments.

Many Pipeline steps also use the named-parameter syntax as a shorthand for creating a Map in Groovy, which uses the syntax [key1: value1, key2: value2]. Making statements like the following functionally equivalent:

git url: 'git://example.com/amazing-project.git', branch: 'master'
git([url: 'git://example.com/amazing-project.git', branch: 'master'])
For convenience, when calling steps taking only one parameter (or only one mandatory parameter), the parameter name may be omitted, for example:

sh 'echo hello' /* short form  */
sh([script: 'echo hello'])  /* long form */
