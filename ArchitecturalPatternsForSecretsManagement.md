# Architectural patterns for secrets management

A microservice based application consists of multiple microservices each performing a small focused role in the whole ecosystem. This means that every microservice needs to communicate securely with other microservices forming a secure mesh of services.

These microservices need to be available all the time. This would mean they need to have the credentails needed to prove their identity but these credentials need to be protected from exposure.

Several strategies are employed for securing sensitive data in microservices. This article helps declutter the choices into 3 categgories:
 - Patterns that prevent exposure of credentials
 - Patterns the minimise the use of the credential if exposed
 - Patterns that prevent exploit on the credentials even without exposure

 # Patterns that prevent disclosure
  
 Vaulted credentials made available through an in memory mount
