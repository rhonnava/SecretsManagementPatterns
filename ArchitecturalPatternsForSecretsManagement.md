# Architectural patterns for secrets management

A microservice based application consists of multiple microservices each performing a small focused role in the whole ecosystem. This means that every microservice needs to communicate securely with other microservices forming a secure mesh of services.

These microservices need to be available all the time. This would mean they need to have the credentails needed to prove their identity but these credentials need to be protected from exposure.

Several strategies are employed for securing sensitive data in microservices. This article helps declutter the choices into 3 concerns:
 - Patterns that prevent exposure of credentials
 - Patterns the minimise the use of the credential if exposed
 - Patterns that prevent exploit on the credentials even without exposure

## Patterns that prevent disclosure
  
### 1. Vaulted credentials made available through an in memory mount
**Description** 
Vault is one of the microservices in the ecosystem and its independant standalone reponsibility in the ecosystem is secrets management. This may include:
 - Protecting the secret at rest.
 - Lifecycle management of the secrets like versioning, periodic rotation of secrets, etc
 - Make secrets available to authorized microservices through a REST API.

Consumer services do not persist the secrets. Instead they fetch the secrets and maintain them in their runtime memory. This makes disclosure a lot more harder to scan the runtime memory of a running process. 

There are several ways in which applications can read these secrets. It can be through


**How does it address the concern of preventing disclosure**
 - Prevents persistence of the credentials in clear text at any point in time
 - Makes the credentials available to the services at any point in time
 - Using a simple file systems ACLs these credentials can be locked down for access only by the required user if and group that the service. 
 - This ensure that access to the secrets from the file system is not possible
 
 
