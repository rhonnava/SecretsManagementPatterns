# Architectural patterns for secrets management

A microservice based application consists of multiple microservices each performing a small focused role in the whole ecosystem. This means that every microservice needs to communicate securely with other microservices forming a secure mesh of services.

These microservices need to be available all the time. This would mean they need to have the credentails needed to prove their identity but these credentials need to be protected from exposure.

Several strategies are employed for securing sensitive data in microservices. This article helps declutter the choices into 3 concerns:
 - Patterns that prevent exposure of credentials
 - Patterns the minimise the use of the credential if exposed
 - Patterns that prevent exploit on the credentials even without exposure
 - Detect and tracing after the fact

## Patterns that prevent disclosure
  
### 1. Vaulted credentials made available through an in memory mount
**Description** 
Vault is one of the microservices in the ecosystem and its independant standalone reponsibility in the ecosystem is secrets management. This may include:
 - Protecting the secret at rest.
 - Lifecycle management of the secrets like versioning, periodic rotation of secrets, etc
 - Make secrets available to authorized microservices through a REST API.

Consumer services do not persist the secrets. Instead they fetch the secrets and maintain them in their runtime memory. This makes disclosure a lot more harder to scan the runtime memory of a running process. 

There are several ways in which applications can read these secrets. 
 - Through REST API integration into the Vault
 - Through a secrets client daemon that makes the secrets available for the application in an in-memory file system mount with file system ACLs.
 - In a container based environment secrets are made available through a client daemon running in a sidecar container.


**How does it address the concern of preventing disclosure**
 - Prevents persistence of the credentials in clear text at any point in time
 - Ensure the credentials are available to the services at runtime always, without the need for any manual intervention.
 - Using a simple file systems ACLs these credentials can be locked down for access only by the required user and group that the service runs as. 
 - This reduced the possiblity of copy and offline access to the secrets
 
 ### 2. Solving the bootstrap problem
  - All cloud providers ensure secrets are tied to resources like VMs on which the application runs. Access to application resources is over an OAuth token, which is provided by a metadata service, accessible only by a link local address.
  - These are shortlived tokens
  
 ### 3. Preventing human intervention in the password generation andd provisioning process
 Dynamic secrets
 
 ### 4. Centralizing trust
 - Cloud based services centralize trust through IAM service
 - No sprawl of secrets management provided by each application
 
