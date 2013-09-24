# Database migration tools - a comparison

Build and release management of software is a common thing in companies. Some use rather old build tools to ensure it, like Ant, some of it use Maven or Gradle. Every build tool has in common, that you have some sort of versioning of your software artifacts.  
However, database versioning isn't as common as it should be. In some companies, you can call yourselve even lucky, if the database scripts needed for a release, are managed in the source control system. 

# Requirements
Of course the requirements for such a tool can be very specific. Some requirements can be:
* support for working with branches in the VCS (since Git is used as VCS, feature branches are very common)
* ability to rollback database upgrades
* persisted schema version and upgrade history
* optional: easy script maintenance (use of SQL etc.)

# Suitable tools
The following tools were chosen as base of the evaluation:
* [Flyway](www.flywaydb.org)
* [dbmigrate](https://code.google.com/p/dbmigrate)
* [Liquibase](www.liquibase.org)