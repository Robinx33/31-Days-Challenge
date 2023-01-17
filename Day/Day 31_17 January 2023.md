`17 January 2023`
## **Day 31 What I Have Learned**
***
## **DNS Rebinding**
- DNS rebinding changes the IP address of an attacker controlled machine name to the IP address of a target application, bypassing the same-origin policy and thus allowing the browser to make arbitrary requests to the target application and read their responses.
- ![image](https://unit42.paloaltonetworks.com/wp-content/uploads/2021/08/word-image-62.png)
***
## **Exploitation**
1. First, we need to make sure that the targeted service is vulnerable to DNS rebinding. It can be done with a simple curl request:

``` js
curl --header 'Host: <arbitrary-hostname>' http://<vulnerable-service>:8080
```
- If the server returns the expected result (e.g. the regular web page) then the service is vulnerable. If the server returns an error message (e.g. 404 or similar), the server has most likely protections implemented which prevent DNS rebinding attacks.
- if the service is vulnerable You Can Proceed to Step 2.
2. Register a domain.
3. Setup Singularity of Origin.
- Requirements
  1.  DNS domain name from a domain registrar such as gandi or namecheap. You need be able to add and edit your own DNS records for your domain.
  2. A Linux server instance from a hosting provider such as Linode, Amazon AWS, Google Cloud, Microsoft Azure etc.
  3. Golang version 1.16 or newer (while the code should compile with 1.11+, the following installation instruction are for 1.16+)
- Setup
  1. Configure appropriate DNS records to delegate the management of a test subdomain ("dynamic.your.domain.") of a domain you own ("your.domain.") to the Singularity's DNS server that we will deploy shortly:
  2. A Name: `rebinder`, IPv4: `ip.ad.dr.ss`.
  3. NS Name: `dynamic`, Hostname: `rebinder.your.domain.`. Note that the ending dot "." in the hostname is required.
  4. This sample setup informs DNS clients, including browsers, that `ip.ad.dr.ss` answers queries for any subdomains under `.dynamic.your.domain.`, e.g. `foo.dynamic.your.domain.`. This also permits one to access the Singularity management console using the `rebinder.your.domain`4 DNS name with a web browser
  5. If you would like to use the Hook and Control attack payload, you also need to setup a wildcard DNS record for your domain e.g. A Name: `*`, IPv4: `ip.ad.dr.ss`.
- On the Attacker Host
  1. Install Golang [Here](https://golang.org/doc/install).
  2. Obtain Singularity
  $ `git clone https://github.com/nccgroup/singularity`
  3. Compile
  $ `cd singularity/cmd/singularity-server`
 $ `go build`
 4. Deploy
 - Deploy the "html" directory in let's say `~/singularity`.
 - Deploy the singularity-server binary in `~/singularity`.
  $ `mkdir -p ~/singularity/html`
 $ `cp singularity-server ~/singularity/`
 $ `cp -r ../../html/* ~/singularity/html/`
5. Run
- Change to the newly created directory (e.g. cd `~/singularity/`) and start singularity-server with $`sudo ./singularity-server --HTTPServerPort  8080`. This will use a DNS rebinding strategy based on the content of the DNS query by default e.g. `s-ip.ad.dr.ss-127.0.0.1-<random_number>-fs-e.dynamic.your.domain` will return first `ip.ad.dr.ss`, the attacker host IP address, then `127.0.0.1` for subsequent queries for a limited period of time.
***
## **Resources**
- [DNS Rebinding](https://unit42.paloaltonetworks.com/dns-rebinding/).
- [What Is DNS Rebinding](https://www.paloaltonetworks.com/cyberpedia/what-is-dns-rebinding).
- [Attacking Private Networks with DNS Rebind](https://medium.com/@brannondorsey/attacking-private-networks-from-the-internet-with-dns-rebinding-ea7098a2d325).
## **Tools**
- [Singularity](http://rebind.it/singularity.html)
- Singularity of Origin is a tool to perform DNS rebinding attacks. It includes the necessary components to rebind the IP address of the attack server DNS name to the target machine's IP address and to serve attack payloads to exploit vulnerable software on the target machine.
***
## **The End**
