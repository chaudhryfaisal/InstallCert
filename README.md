install-cert.jar

Java program written by Andreas Sterbenz, and posted on a blog in Oct, 2006:
https://blogs.oracle.com/gc/entry/unable_to_find_valid_certification

Link to Java program in Andreas' blog no longer works, but the source was linked in another blog:
http://nodsw.com/blog/leeland/2006/12/06-no-more-unable-find-valid-certification-path-requested-target

Usage:
* build or download [distro/install-cert.jar](https://github.com/chaudhryfaisal/InstallCert/blob/master/distro/install-cert.jar?raw=true):

```bash
mvn package
```

* Access server, and retrieve certificate (accept default certificate 1)

```bash
java jar distro/install-cert.jar [host]:[port]
```

* Follow console output to install to system store

# Example:

* run
```bash
java distro/install-cert.jar google.com:443
```

* follow console
```text
Loading KeyStore /usr/lib/jvm/java-6-sun-1.6.0.26/jre/lib/security/cacerts...
Opening connection to woot.com:443...
Starting SSL handshake...

javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target

<...>

Server sent 1 certificate(s):

 1 Subject O=Woot Inc, C=US, ST=Texas, L=Carrollton, CN=*.woot.com
   Issuer  CN=SecureTrust CA, O=SecureTrust Corporation, C=US
   sha1    4b 46 ca 6b 83 05 b3 51 ff c6 e7 9c fd b3 9b e3 3f 2e c4 53 
   md5     e8 a5 88 1b d5 67 bb fc 88 cc b1 c5 2b ac c4 7d 

Enter certificate to add to trusted keystore or 'q' to quit: [1]

[enter]

[
[
  Version: V3
  Subject: O=Woot Inc, C=US, ST=Texas, L=Carrollton, CN=*.woot.com
  Signature Algorithm: SHA1withRSA, OID = 1.2.840.113549.1.1.5

<...>

Added certificate to keystore 'jssecacerts' using alias 'woot.com-1'
Saving [woot.com-1] to woot.com-1.crt

#Delete if already exist ( you may need to run with sudo)
keytool -delete -alias "woot.com-1" -file "woot.com-1.crt" -storepass "changeit" -keystore "/usr/lib/jvm/java-6-sun-1.6.0.26/jre/lib/security/cacerts"

#Install ( you may need to run with sudo)
keytool -importcert -alias "woot.com-1" -file "woot.com-1.crt" -storepass "changeit" -keystore "/usr/lib/jvm/java-6-sun-1.6.0.26/jre/lib/security/cacerts"

```

* run from console
```bash
keytool -importcert -alias "woot.com-1" -file "woot.com-1.crt" -storepass "changeit" -keystore "/usr/lib/jvm/java-6-sun-1.6.0.26/jre/lib/security/cacerts"
```

```text
Owner: O=Woot Inc, C=US, ST=Texas, L=Carrollton, CN=*.woot.com
Issuer: CN=SecureTrust CA, O=SecureTrust Corporation, C=US

<...>

Trust this certificate? [no]:

yes

Certificate was added to keystore

```