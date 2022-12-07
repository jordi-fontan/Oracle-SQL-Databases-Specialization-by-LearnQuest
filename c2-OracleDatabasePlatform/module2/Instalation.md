Installing Oracle Database and Creating a Database

This chapter describes how to install Oracle Database software and create a single instance Oracle Database.

If you are using an earlier release of Oracle Database and want to install a later release of the Oracle Database software, then you can upgrade your existing Oracle Database and use it with the new release of the database software. See "Upgrading a Database".

This chapter contains the following sections:

    Overview of Installing Oracle Database Software and Creating a Database

    Installing Oracle Database Software

    Creating and Managing a Database with DBCA

    Manually Installing the Database Sample Schemas Post-Installation

    Installation: Oracle By Example Series

Note:

This chapter provides an overview of how to install Oracle Database software and create a single instance Oracle Database. This chapter is not a complete installation guide for Oracle Database.

For more detailed information about installing Oracle Database software, see Oracle Database Installation Guide for your platform.
2.1 Overview of Installing Oracle Database Software and Creating a Database
To install your Oracle Database software, use Oracle Universal Installer (OUI). OUI is a graphical user interface utility that enables you to install new Oracle Database software. Online Help is available to guide you through the installation process.

During the installation process, you are given the opportunity to create a database. If you choose to do so, then OUI automatically starts Oracle Database Configuration Assistant (DBCA) to guide you through the process of creating and configuring a database.

Before you start the installation process, see the following sections for information about prerequisites and installation choices:

    Checking Oracle Database Installation Prerequisites

    Deciding on Oracle Database Installation Choices

If you do not create a database during installation, then you must run DBCA at some point after installation to create a database.

Note:

After you create a database, either during installation or as a standalone operation, you do not have to create another. Rather than requiring that you create multiple databases to accommodate different applications, you can separate data into different schemas within a single Oracle Database. See "About User Accounts" for more information about schemas.

Starting with Oracle Database 12c, it is also possible to create a multitenant container database (CDB) that can support zero, one, or many user-created pluggable databases (PDBs). All Oracle databases created before Oracle Database 12c are non-CDBs. This manual describes the OUI and DBCA options for creating CDBs and PDBs, and subsequent chapters provide information on managing CDBs and PDBs.

See Also:

    Oracle Multitenant Administrator's Guide for conceptual information about CDBs and PDBS

    Oracle Multitenant Administrator's Guide for information about managing CDBs and PDBs

2.1.1 Checking Oracle Database Installation Prerequisites
Before installing the software, Oracle Universal Installer (OUI) performs several automated checks to ensure that your computer fulfills the basic hardware and software requirements for an Oracle Database installation. If your computer does not meet a requirement, then an error message is displayed.

The requirements may vary depending upon the type of computer and operating system you are using, but some prerequisites include:

    There is a minimum of 1 GB of physical memory.

    Sufficient paging space is available.

    The appropriate service packs or patches for your operating system are installed.

    An appropriate file system format is being used.

See Also:

Oracle Database Installation Guide for your platform for more information about preinstallation requirements and tasks
2.1.2 Deciding on Oracle Database Installation Choices

Oracle Universal Installer (OUI) guides you through an interview phase where you specify your choices for installation and database creation. The exact sequence of steps depends on your operating system. As you progress through the installation, you are presented with choices on how to configure the database.

    Install Option for Oracle Database

    Installation Class for Oracle Database

    Installation Edition for Oracle Database

    Software Installation Directories for Oracle Database

    Database File Location for Oracle Database

    Database Identifiers for Oracle Database

    About Advanced Installation for Oracle Database

2.1.2.1 Install Option for Oracle Database

You can choose to create and configure a database, or to only install the database software.

You can create a preconfigured database or a custom-configured database during installation. If you choose not to create a database during installation, then you must run Database Configuration Assistant (DBCA) after installation to create a database.

Note:

If you choose to create and configure a database, then Oracle Universal Installer (OUI) will start DBCA at the end of the installation to configure the database.

If you choose to only install the database software using OUI, then you must manually run DBCA after the installation to create and configure the database. With this approach, more options are available for controlling database configuration.

Preconfigured databases are based on templates that Oracle provides or that you create. Each Oracle-provided template is optimized for a particular workload type. See Table 2-2 for information about the types of preconfigured databases.

If you choose to use a Desktop Class installation, then the general purpose database template is used. To create a custom database in which you configure your own database structure, see "About Advanced Installation for Oracle Database."

Note:

If you must create a new database, then Oracle recommends that you install a preconfigured database, which is faster and easier. You can customize the database after it has been created.
2.1.2.2 Installation Class for Oracle Database

The installation classes are Desktop Class and Server Class.

    Desktop Class—This installation class is most appropriate for laptop or desktop computers. It includes a starter database and requires minimal configuration.

    Server Class—This installation class is for servers, such as you would find in a data center, or used to support enterprise-level applications. Choose this installation class if you need access to advanced configuration options.

During a Desktop Class installation, you make only basic choices. For a Server Class installation, you choose either typical installation (where you make only basic choices) or advanced installation.

During a Desktop Class or a typical installation, Oracle Database automatically installs the sample schemas.
2.1.2.3 Installation Edition for Oracle Database

When you install Oracle Database during basic and advanced installations, you can choose a database edition.

For example, you can choose one of these database editions:

    Enterprise Edition—This installation type is the full-featured Oracle Database product that provides data management for enterprise-level applications. It is intended for mission-critical, high-security online transaction processing (OLTP) and data warehousing environments.

    Standard Edition 2—This installation type is designed for department or workgroup- level applications and for small and medium-sized enterprises (SMEs). It is engineered to provide core relational database management services and options. It installs an integrated set of management tools, full distribution, replication, Web features, and facilities for building business-critical applications.

2.1.2.4 Software Installation Directories for Oracle Database
You must specify the directory in which the Oracle Database software is installed, or the location where the product binary files are copied from the installation media. You must choose a location that has enough disk space to contain the software and is accessible by the operating system user performing the installation.

You also specify the location of the Oracle base directory, which is used by all Oracle software products installed on the server. The first time you install Oracle software on a server, you are prompted to specify the location of the inventory directory, called oraInventory. This directory provides a centralized inventory of all Oracle software products installed on the server. You should use the same value for the Oracle inventory directory each time you perform an Oracle software installation on the server.
2.1.2.5 Database File Location for Oracle Database

A database includes several files that store the user data, database metadata, and information required to recover from failures. As an administrator, you decide what kind of storage subsystem to use for these files.

You can select from the following options:

    File System—This default option creates database files that are managed by the file system of your operating system. You can specify the directory path where database files are to be stored. Oracle Database can create and manage the actual files.

    If you are not certain about which option to use, then select File System (the default).

    Automatic Storage Management—This option enables you to place your data files in Oracle Automatic Storage Management (Oracle ASM) disk groups. If you choose Oracle ASM, then Oracle Database automatically manages database file placement and naming. For environments with a large number of disks, this option simplifies database administration and maximizes performance. Oracle ASM performs software striping and mirroring at the file level for maximum storage flexibility, performance, and availability.

    Oracle ASM uses an Oracle ASM instance, which is distinct from the database instance, to configure and manage disk groups. A single Oracle ASM instance can provide storage for multiple databases on the same server.

    For more information, see Oracle Automatic Storage Management Administrator's Guide.

Note:

In past releases, Oracle ASM was installed as part of the Oracle Database installation. With Oracle Database 11g Release 2 (11.2), Oracle ASM is part of an Oracle Grid Infrastructure installation.

To use Oracle ASM for storing database files, you must have installed Oracle ASM and created one or more disk groups before performing the Oracle Database installation.
2.1.2.6 Database Identifiers for Oracle Database
These options include your global database name and system identifier (SID). The SID is a unique identifier that is used to distinguish this instance from other Oracle Database instances that you may create later and run concurrently on your system.

The global database name is the full name of the database that uniquely distinguishes it from any other database. The global database name is in the form database_name.database_domain, for example sales.example.com. The database name portion sales is a simple name you call your database. The database domain portion example.com specifies the database domain in which the database is located. Together, the database name and domain form the global database name.
2.1.2.7 About Advanced Installation for Oracle Database
During advanced installations using the Server Class method you are prompted to make the additional choices listed in this section, and the choices for a typical installation. The installation process provides default values for every choice.

This guide describes, but does not document, these additional advanced installation choices. For more information, see Oracle Database Installation Guide for your platform.

    Product Languages

    You choose which language the software should use after it is installed. You can select multiple languages. The default value is English. If you choose a value other than English, it does not change the language used by the installation.

    Database Configuration Type

    You select a template to use when configuring the database. You can choose either General Purpose/Transaction Processing or Data Warehousing.

    Database Configuration Options

    You can choose how to configure the database created by the installer. You can select the memory size and management options, the character sets used to store data, the security options for database access, and whether the sample schemas should be installed.

    To complete the exercises in this guide and related course material, you must install the sample schemas. This data is also used in most examples throughout Oracle Database documentation. Oracle recommends that you install the sample schemas.

    This choice is a configuration option only during advanced installation. Sample schemas are installed by default during typical or Desktop class installations.

    Recovery Options

    During an advanced installation, you can configure backup and recovery optins for the database. If you choose this option, you must specify whether the recovery area should be stored on the local file system or in an Oracle ASM disk group.

    Note:

    To use Oracle ASM for recovery area storage, you must have installed Oracle ASM as part of an Oracle Grid Infrastructure installation and created one or more disk groups before performing the Oracle Database installation.

    Schema Passwords

    When you create a database, certain administrative user accounts are created automatically. You are prompted to enter the passwords for administrative accounts such as the SYS and SYSTEM accounts, which enable you to manage and administer the database. You can use the same password for each account, or specify passwords for each account individually. If you do not enter a secure password, you will receive a warning message during installation.

    Operating System Groups

    Administrative access to the database is granted by membership in certain operating system groups. You can choose the operating system group to be used for SYSDBA access (typically dba) and SYSOPER access (typically oper).

    The SYSDBA group identifies operating system user accounts that have database administrative privileges and can log in with SYSDBA access. The SYSOPER group is an optional group for users that should have limited database administrative privileges. See "SYSDBA and SYSOPER System Privileges" for more information about these groups and privileges.

2.2 Installing Oracle Database Software
This section briefly describes the steps for a system class installation. Most steps are common to all platforms and involve running Oracle Universal Installer (OUI). Platform-specific steps are noted. For further assistance, consult the online Help or the Oracle Database Installation Guide for your platform.

Note:

The following steps describe the OUI workflow for a host computer that has no previous Oracle software installed. If your host computer has Oracle software installed, then you may see a different workflow.

To perform a basic installation:

    Log on to your computer as a member of the administrative group that is authorized to install Oracle Database software and to create and run the database.

    Refer to your operating system-specific documentation or contact your system administrator to determine whether you have the necessary privileges and permissions to install new software.
    Do one of the following:

        If you are installing from distribution media, then insert the distribution media for the database into your computer.

        The Autorun feature opens the Select a Product to Install window automatically.

        If you downloaded the installation software from the Oracle Web site, then follow the instructions on the site to run the Oracle Universal Installer. Or, see the Oracle Database Installation Guide for your platform.
    The first window that appears is the Configuration Option window. Choose the Create and configure a database single instance option. Or, you also have the option of choosing to only install the database software, but then you must create a database in an additional step after the software is installed. If you are currently using a previous version of Oracle Database, choose Upgrade an existing database. After you have chosen an option, click Next.

    The System Class window appears.
    Choose Server Class.

    You can choose the Server Class option to customize your installation. For example, you use this method to configure Oracle Automatic Storage Management for your database, install the Sample Schemas, or configure backup and recovery options.

    The steps for a Desktop Class installation are similar to the steps for a Server Class installation, but fewer choices are required to install the database.

    Click Next.

    The Install Type window appears.
    Choose Typical install and click Next.
    If you choose Advanced install, some of the installation steps are not documented in this guide. For more information about the advanced choices, see "About Advanced Installation for Oracle Database". Also see Oracle Database Installation Guide for your platform.

    Note:

    On Microsoft Windows operating systems only, the Specify Oracle Home User window appears. This window enables you to use a non-administrator, low privileged Windows User Account as the Oracle Home User. This option is recommended for database installation to ensure that Oracle services run with limited privileges. For single instance databases, you can also choose to allow the Oracle Installer to create a new Windows User Account (local user only) which will then be used as the Oracle Home User.

    If you decline this option, all the services will be installed and will run as the System user.

    See Oracle Database Administrator’s Reference for Microsoft Windows for more information about this feature.

    The Typical Installation window appears.
    Provide the following configuration details for the database:

        Oracle base— The Oracle base directory helps to facilitate the organization of multiple Oracle software installations. See Oracle Database Installation Guide for your platform for more information about ORACLE_BASE.

        If you did not set the ORACLE_BASE environment variable before starting OUI, then the Oracle base directory is created in an app/username/directory on the first existing and writable directory from /u01 through /u09 for UNIX and Linux systems, or on the disk drive with the most available space for Windows systems. If /u01 through /u09 does not exist on the UNIX or Linux system, then the default location is user_home_directory/app/username.

        You can click Browse to find the directory you want to act as the Oracle base directory.

        Software location—The software location is the Oracle home for your database. You must specify a new Oracle home directory for each new installation of Oracle Database software. By default, the Oracle home directory is a subdirectory of the Oracle base directory.

        You can click Browse to find the directory where you want to install the Oracle Database software.

        Storage type—You can choose either File system or Oracle Automatic Storage Management.

        Database file location—The database file location is the location where Oracle Database files are stored. By default, this location is Oracle_base/oradata. You can click Browse to select a different location.

        Database edition—Select either Enterprise Edition or Personal Edition (Microsoft Windows platforms only). See "Installation Edition for Oracle Database".

        OSDBA group (Linux and UNIX platforms only)—Specify the operating system DBA group. Host computer users in this group have administrative privileges on the database. This group is typically named dba. Refer to Oracle Database Installation Guide for Linux or for your UNIX platform for more details.

        Global database name—Enter the fully qualified global database name. See "Database Identifiers for Oracle Database" for more information about global database names.

        Administrative password—Specify the initial password for administrator accounts such as the SYS and SYSTEM accounts. If the password you choose is not a secure password, a warning message will be displayed.

        Create as Container database: Enable this option to create the database as a multitenant container database (CDB) that can support zero, one, or many user-created pluggable databases (PDBs).

        If you want Database Configuration Assistant (DBCA) to create a PDB when it creates the CDB, specify the PDB name in the Pluggable database name field.

    After you enter the required information, click Next.

    For first time installations on Linux and UNIX operating systems only, if Oracle software has not previously been installed on this server, then the Create Inventory window appears. If this is not the first installation attempt on this server, then the Perform Prerequisite Checks window appears.
    If the Create Inventory windows appears, specify a directory for installation files and the name of an operating system group that has write permissions for that directory.

    If this is the first time you are installing any Oracle software on this computer, then the Create Inventory Directory window appears. You must specify a local directory for the inventory, which OUI uses to keep track of all Oracle software installed on the computer. This information is used while applying patches or upgrading an existing installation, and while deinstalling Oracle software. Note that this directory is different from the Oracle home directory. The recommended value for the inventory directory is Oracle_base/../oraInventory, or one level above the Oracle base directory, in the oraInventory subdirectory. If your Oracle base directory is /u01/app/oracle, then the Oracle inventory directory defaults to /u01/app/oraInventory.

    In this window you can also specify the operating system group that has write permissions on the inventory directory. This prevents other users from writing over the Oracle product installation files.

    After you enter a directory path and specify an operating system group, click Next to continue.

    The Perform Prerequisite Checks window appears.
    If any checks failed, then take corrective actions.

    OUI performs several environment checks and indicates whether the check was a success, or resulted in a warning or failure. Details of the checks are provided in the displayed window. The installation can proceed only when all checks have a status of either Succeeded or Warning. If any of the environment checks failed, then they must be resolved manually. See "Checking Oracle Database Installation Prerequisites" for more information.

    If all the prerequisite checks passed, or after you click Next, the Summary window appears.
    Review the installation summary, then click Install to start the installation.

    The Install Product window appears, showing the installation progress.
    For Linux and UNIX operating systems only, you are prompted to run configuration scripts. To run root scripts automatically, select Automatically run configuration scripts. Alternatively, you can run the configuration scripts manually as the root user. Run the scripts and then click OK.

    When the installation is complete, the Finish window appears.
    Make note of the information in the Finish window, then click Close to exit OUI.

    Your installation and database creation is now complete.

    You use Oracle Enterprise Manager Database Express (EM Express) to perform common database administration tasks.

    Use the URL for EM Express that is provided in the Finish window to start EM Express, specifying your database hostname instead of 'localhost.' When EM Express prompts you for your username and password, log in as a user with DBA privilege (such as SYSTEM).

    Note:

    By default, DBCA picks a free port from the 5500 to 5599 range to use as the EM Express port.

    If you want a particular port to be used as the EM Express port, specify that port using the DBEXPRESS_HTTPS_PORT operating system environment variable before starting OUI or DBCA.

    For more information on setting environment variables, see "Configuring the Operating System Environment Variables."

    See Also:

        Oracle Multitenant Administrator's Guide for conceptual information about CDBs and PDBs.

        Oracle Multitenant Administrator's Guide for information about managing CDBs and PDBs.

        "SYS and SYSTEM Users" for information about the recommended alternative to using the SYSTEM account for day-to-day administrative tasks.

        "Getting Started with Database Administration" for more information about using EM Express.

