---
title: BioJava:CookBook:BioSQL:SetupOracle
permalink: wiki/BioJava%3ACookBook%3ABioSQL%3ASetupOracle
---

BioJava and BioSQL/Oracle HOWTO
-------------------------------

**What you'll need**

### Bio\*

You'll need the latest version of BioJava to take advantage of the full
functionality of BioSQL. This can be downloaded from biojava.org. You'll
also need the latest Oracle BioSQL schema. Originally an alternative
schema was available, however BioJava is recommended for use only with
the official schema.

-   Original: by Hilmar Lapp, the original BioSQL schema takes full
    advantage of Oracle's security mechanisms and produces a high
    quality schema. To download the schema, go to
    [cvs.open-bio.org](http://cvs.open-bio.org/) and select the biosql
    project. Navigate to and download the entire
    biosql-schema/sql/biosql-ora folder.

<!-- -->

-   Alternative (deprecated): by Len Trigg, this version sits entirely
    inside a single user account, requiring no sysdba access to install.
    You'll have to ask for a copy of the script from the
    [biosql-l](http://obda.open-bio.org/mailman/listinfo/biosql-l)
    mailing lists.

Both options are fully functional and compatible with both BioJava and
BioPerl. This document only discusses the Original schema.

### Oracle

Obviously, you'll need an Oracle database, using the most up-to-date
JDBC drivers you can find. BioJava has been tested with BioSQL using
Oracle 9i and 10g. For the Original schema, you'll also need sysdba
access, or get your DBA to help you if you do not have this yourself.
Things that require sysdba access/DBA assistance include creating
tablespaces (or being assigned one to use), creating or assigning roles,
and creating or assigning additional user accounts other than your own,
if you intend to install BioSQL outside of your own account. If your DBA
does any of this for you, then you will need to comment out the
appropriate steps in

BS-create-all.sql

before running the installer.

-   Tablespaces are created in BS-create-tablespaces.sql.
-   Roles are created in BS-create-roles.sql.
-   Users are created in BS-create-users.sql.
-   Global roles and users are defined in BS-defs-local.sql (see below
    on how to set this up).

### Bugfixing

During the production of this document, in cooperation with Hilmar Lapp,
all potential problems that were identified with the default BioSQL
setup scripts were resolved. However there may still be issues unique to
your environment so keep a careful eye open during installation.

One interesting bug that is not related to BioSQL but may cause you
grief is to do with the built-in ODM Blast functionality in Oracle 10g.
ODM Blast will throw "table or view does not exist" errors if you pass
it a cursor over a table that is in fact a synonym (eg. biosequence and
bioentry in any of the users you have granted biosql\_user or
biosql\_loader to). You can only run ODM Blast over actual physical
tables or views, and not synonyms of them.

### Installation

Make sure you have set the $ORACLE\_SID environment variable to the
correct database before running the scripts. There may be occasional
requirements to reconnect to the database, and if it is not set, you may
end up running the scripts against the wrong database. Alternatively,
you can append "@SID" to your passwords each time you are prompted for
them during setup, where "SID" is the SID of your database.

The installation requires the creation of three tablespaces (May be
created or assigned for you by your DBA) - one for data, one for
indexes, one for LOB objects. Decide where you will be keeping the
database files for these, and what you will call the tablespaces. Don't
create them yet though, just write down the names. As always it is good
practice to keep the data and index tablespaces on separate disks to
prevent IO bottlenecks, but you can probably safely put the data and LOB
tablespaces on the same disk.

You will also need to decide on names for the two basic roles that
BioSQL uses (May be created or assigned for you by your DBA) - the
base\_user role which contains just enough privileges to connect to the
database, and the schema\_creator role, which contains the privileges
required to create database objects in a schema. Again, don't create
them just yet.

Now, copy BS-defs.sql to BS-defs-local.sql and edit it. You should check
every entry in it carefully, particularly the names and locations of the
tablespace files to be created, and the names of the two roles you just
decided on above. You will also choose names for the various default
BioSQL roles and users. biosql\_owner is the actual owner of the schema
that should already exist and have had the schema\_creator role granted
to it, you'll need to define its password here too. biosql\_user is a
role to be granted to people who need read-only access to the BioSQL
database, biosql\_loader is a role designed for general read/write
access, whilst biosql\_admin has full read-write permission on the
schema.

Once you have edited the BS-defs-local.sql script appropriately, you
need to create the two base roles of base\_user and schema\_creator
manually. Create them by running something similar to the following
script whilst logged in as sysdba, from inside the biosql-ora directory:

`  @BS-defs-local`  
`  create role &base_user;`  
`  grant `  
`  CREATE SESSION,`  
`  CREATE SYNONYM`  
`  to &base_user;`  
`  create role &schema_creator;`  
`  grant `  
`  CREATE PROCEDURE,`  
`  CREATE ROLE,`  
`  CREATE SEQUENCE,`  
`  CREATE SESSION,`  
`  CREATE SYNONYM,`  
`  CREATE TRIGGER,`  
`  CREATE TYPE,`  
`  CREATE VIEW,`  
`  CREATE TABLE,`  
`  CREATE PUBLIC SYNONYM,`  
`  DROP PUBLIC SYNONYM`  
`  to &schema_creator`  
`  with admin option;`

If you want some basic users set up, edit the BS-create-users.sql script
to look at the sample users it will create for you automatically. If you
don't want them, or want different names etc., comment them out or edit
them.

The final stage before actual installation is to edit the
BS-create-all.sql script to ensure that only the steps you require are
carried out. If you already have predefined tablespaces and don't want
it to create new ones, comment out the line that reads
@BS-create-tablespaces. You should do the same for @BS-create-users and
@BS-create-roles as necessary. Likewise if you don't want any default
data loaded into the database, comment out the line near the end that
reads @BS-prepopulate-db.

Make sure you have commented/uncommented the appropriate parts of
section 9 of BS-create-all.sql. The BS-create-Biosql-API2 script it
refers to is an alternative to BS-create-Biosql-API, which works much
better with BioJava. This is because BioJava has no flexibility about
column names in tables. The API2 version of the script ensures that the
column names are exactly the same as what BioJava expects by using
views. But, no matter which you run, everything will still work fine
with BioPerl).

Now, log into your Oracle database and create the BioSQL database by
typing:

`  @BS-create-all`

It will prompt you for the sysdba user and password if necessary (unless
you commented out these parts), maybe a couple of times. You might want
to spool the output to see what happens, but you'll find that half of it
doesn't appear in the spool file, because BioSQL is using spool itself
to generate dynamic scripts on the fly. If you've done everything right,
the only messages you should get are a few Table or view does not exist
style messages, referring to the attempts by the script to drop old
objects before recreating new ones.

During installation you may be prompted for the sysdba username and
password a couple of times. This is required only to create roles,
tablespaces, and users.

If something goes wrong, you can safely rerun the script without
dropping anything first as it will drop the database objects from the
previous attempt first. It will however leave behind the tablespaces,
users, and roles. You can always just drop the users and tablespaces
that have been created if it really messes up, and start again from
scratch.

Now, your database has been installed! The only remaining step is to log
in to each user who will be using BioSQL, and run the usersyns.sql
script that the installation generated for you in the biosql-ora
directory. This script creates the synonyms for the BioSQL objects and
allows the users to see them. This script should not have any errors at
all. If it does, edit it and check it closely for things like misplaced
linebreaks etc.

Note that if your users can't connect or can't get the appropriate
permissions to do what you want them to do, try re-running the
BS-create-roles script as sysdba, then the BS-grants script as the
biosql\_owner user. Disconnect and reconnect as the user having trouble
and it should be fixed.

### Testing

Any BioJava script should work fine.

THE END!

[Richard Holland](User:Rholland "wikilink"), December 2004, updated May
2005

### Addendum

With the new BioJavaX extensions, you will find that data saved to
BioSQL by the old BioJava/BioSQL bindings will not get interpreted
correctly by BioJavaX, and vice versa. This is because the old bindings
used significantly different ways of representing the same information
within the database, whereas the new bindings in BioJavaX do it more
intelligently and make better use of the various tables available. In
fact, BioJavaX is also be able to read/write most data saved into BioSQL
by BioPerl, which was not possible with the old bindings.

To convert data saved by the old BioJava into data readable by the new
BioJavaX, is is necessary to extract the database to a suitable file
format (eg. Genbank) using the old BioJava, then delete all the data
from the database. Then, use BioJavaX to parse the files you created and
save the data back into the database.
