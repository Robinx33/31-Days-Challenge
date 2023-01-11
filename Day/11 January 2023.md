`11 January 2023`
## **Day 25 What I Have Learned**
***
## **Rsync Service**:
- Rsync is a utility for transferring and synchronizing files between two servers (usually Linux). 
- It is usually used on Linux systems.
- Sync is determined by checking the file sizes and timestamps. 
- It is usually found running on Port - 873
- However, due to the weak configurations, it is often an interesting attacker vector to gain unauthorized access to sensitive data, and sometimes the means to obtain a shell on the system.
- Remotely accessing directories shared through Rsync requires two things, file share access and file permissions.
- File Share Access can be defined in /etc/Rsyncd.conf to provide anonymous or authenticated access.
## **Enumration & Issues**
1. Finding a Rsync Server
- Run a port scan using nmap, you can use below command
`nmap -sS -sV -p873 <ip> `
2. Enumeration Steps
- List Directory
`rsync 127.0.0.1:: `
- List Sub Directory
`rsync 127.0.0.1::files`
- List Directories & Files Recursively
`rsync -r 127.0.0.1::files/tmp/`
- Downloading Files & Folders
`rsync 127.0.0.1::files/tmp/test.txt`
`rsync -r 127.0.0.1::files/tmp`
- Uploading Files & Folders
`rsync ./file.txt 127.0.0.1::files/test`
`rsync -r ./folder 127.0.0.1:files/test`

***
## **Resources**
- [Enumerating rsync servers with examples](https://medium.com/@minimalist.ascent/enumerating-rsync-servers-with-examples-cc3718e8e2c0)..
- [Linux Hacking Case Studies Part 1: Rsync](https://www.netspi.com/blog/technical/network-penetration-testing/linux-hacking-case-studies-part-1-rsync/).
***
## **The End**