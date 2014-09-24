gradle-openjpa
==============

gradle-plugin that enhances entity-classes with OpenJPA code

Usage
--------------
    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath 'at.schmutterer.oss.gradle:gradle-openjpa:0.1.0'
        }
    }

    apply plugin: 'openjpa'

    openjpa {
        //additional configuration if required
    }

Configuration Properties
--------------

These configuration properties can be passed to the openjpa-closure:

* __addDefaultConstructor__ (boolean) [default: true]

    The JPA spec requires that all persistent classes define a no-arg constructor.
    This flag tells the enhancer whether to add a protected no-arg constructor to any persistent classes that don't already have one.
* __connectionDriverName__ (String)

    This setting can be used to override any openjpa.ConnectionDriverName set in the persistence.xml.
    It can also be used if the persistence.xml contains no connection information at all.

    Example:

            openjpa {
                connectionDriverName 'com.mchange.v2.c3p0.ComboPooledDataSource'
            }

     This is most times used in conjunction with _connectionProperties_.
* __connectionProperties__ (Map)

    Used to define the credentials or any other connection properties.

    Example:

        openjpa {
            connectionProperties [
                driverClass:'com.mysql.jdbc.Driver',
                jdbcUrl:'jdbc:mysql://localhost/mydatabase',
                user:'root',
                password:,
                minPoolSize:5,
                acquireRetryAttempts:3,
                maxPoolSize:20
            ]
        }

     This is most times used in conjunction with _connectionDriverName_.
* __enforcePropertyRestrictions__ (boolean) [default:false]

    Whether to throw an exception when it appears that a property access entity is not obeying the restrictions placed on property access.

* __excludes__ (String[])

    List of excludes to scan searchDir to pass to the jobs.
    This option may be used to stop OpenJPA tasks from scanning non-JPA classes (which usually leads to warnings such as "Type xxx has no metadata")

    Example:

        openjpa {
            excludes ['**/notthese/*]
        }

* __includes__ (String[])

    List of includes to scan searchDir to pass to the jobs.
    This may be used to restrict the OpenJPA tasks to e.g. a single package which contains all the entities.

* __persistenceXmlFile__ (File)

    Used if a non-default file location for the persistence.xml should be used.
    If not specified, the default one in META-INF/persistence.xml will be used.
    Please note that this is not a resource location but a file path!

* __toolProperties__ (Map)

    Additional properties passed to the OpenJPA tools.
