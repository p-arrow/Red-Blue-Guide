**>> General Information: [Z_Networks/Web Application.md](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Z_Networks/Web%20Application.md)**

## Methodology 

> Below guide is inpired by [Carlospolop](https://github.com/carlospolop/hacktricks/tree/master/pentesting)

> Aim to apply this methodology to each discovered domain, subdomain or IP with undetermined web server inside the scope

<br />

- Start by preparing a "notebook" to keep track of all your findings (to not forget any findings and keeping an overview!)
   - [Cherrytree](https://github.com/giuspen/cherrytree)
   - Mind Map
   - Simple Notepad
   - Excel
   - etc. 
- Identifying the **technologies** used by the web server
- Any **known vulnerability** of the version of the technology?
- Any **well known tech**?
- Any **useful trick** to extract more information?
- Any **specialized scanner** to run like wpscan?
- Any **general purpose scanner** to run? 
- Initial checks:
   - robots
   - sitemap
   - 404 error
   - SSL/TLS scan (if HTTPS)
- **Spider the web page** in order to find all possible files, folders and parameters being used
   - Anytime a new directory is discovered, it should be spidered
- **Directory Brute-Forcing**: Try to brute force all the discovered folders searching for new file and directories 
   - Anytime a new directory is discovered, it should be brute forced
- **Parameter Brute-Forcing**: Try to find hidden parameters
- Look out for backups of discovered files appending common backup extensions

**>> Once you have identified all the possible endpoints accepting user input, check for all kind of vulnerabilities related to it!**
