# Apache Atlas – Installation & Configuration
Apache Atlas provides data governance and metadata management.\
\
**Installation**
1. Install dependencies:
- Java (JDK)
- Apache Kafka
- HBase (or another supported backend)
2. Download and unpack Apache Atlas binary distribution.
3. Configure Atlas to point to your Kafka and HBase instances via configuration files.
4. Start services:
bash
```
./bin/atlas_start.py
```
**Configuration**
- Define metadata types, classifications, and entities.
- Integrate with data platforms and set up authentication/authorization (LDAP, Kerberos, etc.).
