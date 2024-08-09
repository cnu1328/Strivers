## Proxy Setup

**Steps:**

1. Open the terminal.

2. Open the APT configuration file with `gedit` using `sudo`:

```bash
    sudo gedit /etc/apt/apt.conf
```

This command will open the `apt.conf` file in the `gedit` text editor.

3. Copy the following statements into the `apt.conf` file. Make sure to replace `username` with your username and `urpassword` with your actual password:

```text
    Acquire::http::Proxy "http://username:urpassword@hostelinternet.rgukt.ac.in:3128/";
    Acquire::https::Proxy "http://username:urpassword@hostelinternet.rgukt.ac.in:3128/";
    Acquire::socks::Proxy "http://username:urpassword@hostelinternet.rgukt.ac.in:3128/";
    Acquire::ftp::Proxy "http://username:urpassword@hostelinternet.rgukt.ac.in:3128/";
```

4. Save the document and close `gedit`.

5. To check if the proxy configuration is working, run the following command in the terminal:

```bash
    sudo apt-get update
```

If everything is configured correctly, the update process should proceed without issues.

## C++ install in Ubuntu

1. **Step:1**

```bash

sudo apt update

```

2. **Step:2**

```bash

sudo apt install gcc g++

```

3. **Step:3**

```bash

gcc --version

g++ --version
```

## Install JDK in ubuntu

1. First open this [Link](https://www.oracle.com/java/technologies/downloads/) in web-browser
2. Download the `x64 Compressed Archive`
3. Go to the downloaded folder and extract it
4. Copy the below code

```bash

JAVA_HOME=jdk-install-dir
export JAVA_HOME
PATH=$JAVA_HOME/bin:$PATH
export PATH

```

5. Open terminal and enter

```bash
gedit .profile

```

6. Paste the copied code and save it

```bash

JAVA_HOME=(give the path folder)(example: /home/downloads/jdk-17.0.3)
export JAVA_HOME
PATH=$JAVA_HOME/bin:$PATH
export PATH

```

7. Now check it

```bash

java --version

```

## Install Eclipse in ubuntu

1. Search eclipse and download the jar file
2. Extract the files
3. Then open termial and type ./eclipse-inst
4. Install
5. OPen it

## Install MYSql to ubuntu

1. Type command in terminal `sudo apt-get install mysql-server`
2. To check installed `mysql --version`
3. Type to use mysql `sudo mysql -u root -p`

## Database Connectivity

```sql

Alter user 'root'@'localhost' identified with mysql_native_password by "password";

```
