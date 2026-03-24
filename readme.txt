#readme file is under tracking


DATABASE SECURITY CHECKER VERSION 2.0.0.6
__________________________________________
1.1 Overview
Configuring and maintaining secure authentication protocols such as Kerberos and TLS can be complex and challenging. These protocols require precise settings and proper environment configurations, making the setup process intricate. Authentication issues often lead to cryptic and difficult-to-diagnose errors, necessitating significant troubleshooting efforts. The need to manage multiple configuration files, environment variables, and certificates further complicates the process. Incorrect settings can cause authentication failures, leading to prolonged downtimes and potential security vulnerabilities. The lack of comprehensive diagnostic tools worsens these issues, making it hard to identify the root cause of problems. As a result, database administrators and IT security teams spend considerable time and resources ensuring these protocols are correctly implemented and maintained. dbsecchk addresses these challenges by simplifying the validation, troubleshooting, and remediation processes for Kerberos and TLS configurations.

1.2 Purpose
dbsecchk is designed to review Kerberos and TLS setups, identifying issues in these configurations. It provides clear actionable steps for remediation, ensuring correct environment settings.

1.3 Scope
This documentation covers the installation, configuration, usage, and troubleshooting of the dbsecchk tool. It does not cover the detailed workings of Kerberos and TLS protocols themselves.
__________________________________________
 
2. Getting Started
2.1 System Requirements
•	Linux: Oracle Linux 7 and above
•	Windows: Windows 2016 and above
•       AIX :IBM AIX 7.2 and above 
2.2 Installation
Prerequisites
•	Either the ORACLE_HOME environment variable must be set, or ensure that SQL*Plus is available and functioning correctly on the system.
•	The user must have the necessary permissions to edit the working folder.
Installation Steps
1.	Copy the Binary Executable: Copy dbsecchk to the desired directory on your host machine.
2.	Run the Tool: Navigate to the directory and run:
________________________________________________________________
$dbsecchk -h
usage: dbsecchk [-h] [-tnsalias TNSALIAS] [-user [ADMIN_USERNAME]]
                [-password [ADMIN_PASSWORD]] [-client] [-server] [-kerberos]
                [-adbs] [-tls] [-mtls] [-tnsadmin DIRECTORY] [-mode MODE]
                [-wallet_path WALLET_PATH] [-report] [-complete] [-V] [-debug]

dbsecchk (Database Security Checker) validates the Database Authentication Configurations.

optional arguments:
  -h, --help            show this help message and exit
  -tnsalias TNSALIAS    Provide TNS ALIAS/Connect String
  -user [ADMIN_USERNAME], --admin_username [ADMIN_USERNAME]
                        Optional, Provide User Name
  -password [ADMIN_PASSWORD], --admin_password [ADMIN_PASSWORD]
                        Optional, Provide Password
  -client               Set to validate client configurations
  -server               Set to validate server configurations
  -kerberos             Set to validate kerberos configurations
  -adbs                 Set to validate ADBS Server configurations
  -tls                  Set to validate one-way tls configuration
  -mtls                 Set to validate Mutual Authentication configurations
  -tnsadmin DIRECTORY, --directory DIRECTORY
                        Set TNS_ADMIN location to validate
  -mode MODE, --mode MODE
                        Optional, Set mode to login to Database e.g. sysdba, sysoper etc
  -wallet_path WALLET_PATH
                        Optional, Set the wallet path for validation
  -report, --generate_files
                        Optional, Generate HTML and text report files
  -complete, --generate_complete
                        Generate HTML and report
  -V, --version         Current version
  -debug, --debug       Enable Tracing
________________________________________________________________

This command displays usage information and verifies the tool is ready to use.
Key Execution Points
Environment Variable Requirements:
1.	Primary Requirement:
Either the ORACLE_HOME environment variable must be set, or ensure that SQL*Plus is available and functioning correctly on the system.
2.	Optional Configuration:
Optionally, set the TNS_ADMIN and LD_LIBRARY_PATH environment variables if they are not already set.
If TNS_ADMIN and LD_LIBRARY_PATH are not explicitly set, their values will be derived from ORACLE_HOME if it is defined.


Example Execution
Assuming your TNS_ADMIN directory is /opt/oracle/network/admin:
$ export  ORACLE_HOME=/opt/oracle/product/19c/dbhome_1
$ export  TNS_ADMIN=/opt/oracle/network/admin
$ dbsecchk -tls –server



2.3 Supported Authentication Protocols
•	Kerberos: Network Authentication Protocol for secure identity verification.
•	TLS/MTLS: Transport Layer Security and Mutual Transport Layer Security for encrypted communication.


2.4 Key Features
•	Ease of Use: A simple command-line executable with straightforward operation.
•	Cross-Platform Compatibility: Supports both Linux and Windows environments.
•	Database Support: Compatible with Oracle database versions, including 23c, 21c, and 19c.
•	Validation: Verifies all mandatory environment variables, configuration files, and parameters.
•	Error Tracing: Offers comprehensive error diagnostics for effective troubleshooting.
•	Recommendations: Provides actionable solutions in easy-to-read reports.
•	Report Generation: Delivers detailed reports in multiple formats:
o	HTML Report: Comprehensive and user-friendly for web viewing.
o	Text Report: Simplified format for quick reading and sharing.
o	Command Line Output Report (Default): Direct output for seamless integration with other command-line tools and scripts.

__________________________________________

 
3. Quick Start Guide
3.1  Instructions for Using the dbsecchk Tool
1. Extract the dbsecchk.zip Archive  
   - Unzip the archive to retrieve the following files:  
     - Linux binary: `linux/dbsecchk`  
     - Windows executable: `windows/dbsecchk.exe`  
2. Copy the Appropriate Binary  
   - Copy the binary executable file suitable for your operating system to your host machine.  
3. Navigate to the Binary Directory  
   - Change to the directory containing the binary executable.  
4. Set the ORACLE_HOME Environment Variable  
   - Ensure that the `ORACLE_HOME` environment variable is correctly set.  
   - If `ORACLE_HOME` is unavailable, ensure `SQL*Plus` is accessible. (At least one of these must be available: `ORACLE_HOME` or `SQL*Plus`.)  
5. Handle the TNS_ADMIN Variable (if required)  
   - If `TNS_ADMIN` is not set, the tool will automatically assume a default path: `ORACLE_HOME/network/admin`.  
6. Check Tool Usage  
   - Run the following command to view the usage details:  
     ./dbsecchk --help
7. Execute the Tool  
   - Use the provided command to run the tool via the Command Line Interface (CLI).  

Supported Environments
The tool can operate in View-based and Shiphome environments. No Python-related environment variables are required for its operation.
Output and Report Location
The tool generates outputs and reports in the working folder. Ensure the user has write permissions for the working directory.
Review the Report
Use a web browser to review the generated reports, or any relevant information provided by the tool.

__________________________________________

4. Command Usage
4.1 One-Way TLS - Client
dbsecchk -tls -client -tnsalias <tnsalias> -tnsadmin <TNS_ADMIN (optional)>
Parameters
•	-tls: Enables One-Way TLS validation.
•	-client: Specifies client-side configuration.
•	-tnsalias <tnsalias>: Specifies the TNS alias.
•	-tnsadmin <TNS_ADMIN(optional)>: Optional parameter to specify the directory path of Oracle Net Services configuration files.
 
4.2 One-Way TLS - Server
dbsecchk -tls -server -tnsadmin <TNS_ADMIN(optional)>
Parameters
•	-tls: Enables One-Way TLS validation.
•	-server: Specifies server-side configuration.
•	-tnsadmin <TNS_ADMIN(optional)>: Optional parameter to specify the directory path of Oracle Net Services configuration files.


__________________________________________

5. Use Cases
Use Case 1: Mutual TLS (mtls)
Scenario: Validating client for mTLS authentication. Below report shows that the wallet does not exist at the configured location for the WALLET_LOCATION parameter.
$ dbsecchk -client -mtls
Enter TNS_ALIAS/Connect String: orclpdbtls
Enter username:
Enter password:

Checking Mutual TLS Authentication: Failed
Validation error encountered in the configuration at:
WALLET_DIRECTORY:/apps/oracle/product/19c/dbhome_1/client

Recommendation/Fix: Wallet path does not exist, make sure wallet is configured at /apps/oracle/product/19c/dbhome_1/client

Environment:
ORACLE_HOME: /apps/oracle/product/19c/dbhome_1
TNS_ADMIN: /apps/oracle/product/19c/dbhome_1/network/admin

 
Use Case 2: One-way TLS (tls)
Scenario: Validating server configuration for One-way TLS.
$ dbsecchk -server -tls

Checking One way TLS Authentication: Failed
Validation error encountered in the configuration at:
SSL_CLIENT_AUTHENTICATION: Value set in listener.ora is: 'TRUE'
Value set in sqlnet.ora is: 'TRUE'

Recommendation/Fix: Configure `SSL_CLIENT_AUTHENTICATION = FALSE` in sqlnet.ora and listener.ora for One-Way TLS Authentication.

Environment:
ORACLE_HOME: /apps/oracle/product/19c/dbhome_1
TNS_ADMIN: /apps/oracle/product/19c/dbhome_1/network/admin

__________________________________________

