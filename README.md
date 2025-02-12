
```
   _______                    _  ___ _         ___
  |__   __|         _        | |/ (_) |      _|   \
     | | ___   ___ | |       | ' / _| |_      |    \
_____| |/ _ \ / _ \| |_______|  < | | __|_____|     \_______
_____| | (_) | (_) | |_______| . \| | |_ _____.      _______|
     |_|\___/ \___/|_____|   |_|\_\_|\__|     |     /
                                             _|    /
                                              |___/                         
                                      
           __       __  __                        _       
          /  |_    |  \/  |                      | |      
         /   |     | \  / | __ _  __ _  ___ _ __ | |_ ___ 
 _______/    |_____| |\/| |/ _` |/ _` |/ _ \ '_ \| __/ _ \_________
|_______      _____| |  | | (_| | (_| |  __/ | | | ||  __/_________
        \    |     |_|  |_|\__,_|\__, |\___|_| |_|\__\___|
         \   |_                 __/ |                   
          \__|                 |___/       
  
                                            
```



# CspGeneretor v1.3 (unofficial Script)  #
![Magento Logo](https://www.evemilano.com/wp-content/uploads/2017/06/Magento_logo.png)

Logo by Magento Adobe [Link site official](https://business.adobe.com/products/magento/magento-commerce.html)

![Supported Python versions](https://img.shields.io/badge/python_3.11-blue.svg)

This script allows you to generate magento CSP module with few simple clicks.
Form creation is completely dynamic.
The module version, name, report type, and soon also the policy value id.
The id can be of two types incremental, from 0 to X or by hostname, ex id=cloudflare host=cloudflare.com

In the script there is already a default host list but using a log file you can also generate a custom host list which will be inserted in the csp_whitelist.xml file. (the script automatically recognizes the type CSP Code)

The default list will be updated over time to simplify module creation

# Help
Usage: CspGeneretor.py [-h] [--nameModule NAMEMODULE] [--fileLog FILELOG] [--version VERSION] [--setId SETID]
               [--trt TRT] [--tra TRA]


options:

$~~~~~~~~~~~$  -h, --help            show this help message and exit
  
$~~~~~~~~~~~$  --nameModule          Name Module CSP
  
$~~~~~~~~~~~$  --fileLog FILELOG     Path file Log
  
$~~~~~~~~~~~$  --version VERSION     Version Module
  
$~~~~~~~~~~~$  --setId SETID         Id value (for the moment it is only numerical)
  
$~~~~~~~~~~~$  --trt TRT             Type report storefront
  
$~~~~~~~~~~~$  --tra TRA             Type report admin
  
  
Tool:

$~~~~~~~~~~~$  -cc CC             Run a log file cleanup (-cc 1)
  
$~~~~~~~~~~~$  -st ST             Run Step to Step CSP script (-st 1)
  
$~~~~~~~~~~~$  -mf1 MF1           Merge 2 whitelists (-mf1 "fileLog1.log")
  
$~~~~~~~~~~~$  -mf2 MF2           Merge 2 whitelists (-mf2 "fileLog2.log")


 
---------------------------

# Tool
- # Create Module CSP (tool 1)
  # Step 1
  Using DevTool for save log or using default whitelist (Right click on log in console and save file)
  
  ![Save File Log](https://blogger.googleusercontent.com/img/a/AVvXsEjmkRMaFKBbKdfARUDh1nbBCTAgOpwuPaWmM3NSLl1eBs2qRaCCBybMggtjMa5Q3Su1ngwpjejOiPqgF-SmNuKJZr-g4o4arlSC3At8dheurT4kQrsDs9f3wqAyBIKzsaCF7LYLkufmG6_Z8Zq30h6Cea3RlSNPjYMwoYEeovC02-hrqBEEJVsde9d4)



  # Step 2
  Run the script and insert
  
  1 Name Module --nameModule
   
  2 Add log file name --fileLog (if needed)
  
  3 Add version --version (by default it is set to 1)
  
  4 Add type Id --setId (0=number 1=name Host for the moment it is only numerical)
  
  5 Add value for type report storefront --trt (0 or 1)
  
  6 Add value for type report admin --tra (0 or 1)


   ```
   #Pre-Set
   python3 CspGeneretor.py --nameMod "Csp_base" --fileLog "error.log" --version "1.0" --setId 0 --trt 1 --tra 1
   ```
  
  or 
  Run the script step to step

   ```
   #StepToStep
   python3 CspGeneretor.py -st
   ```
  
  # Step 3 
  
  1 Import Module On Project 
  
  2 Run `php bin/magento setup:upgrade`, `php bin/magento setup:di:compile` and `php bin/magento cache:flush`
  
  3 Good job
  

- # Clear File Log (Tool 2)
   
   Remove all not CSP errors from the log file
  
   ```
   python3 CspGeneretor.py -cc "error.log"
   ```

- # Merge Whitelist (Tool 3)
   Merge two whitelists and remove duplicate host
   ```
   python3 CspGeneretor.py -mf1 "etc/csp_whitelist1.xml" -mf2 "etc/csp_whitelist2.xml"
   ```

---------------------------

# Info

# Type CSP Code
- default-src -> The default policy. 

- style-src -> Defines the sources for stylesheets. 

- font-src -> Defines which sources can serve fonts.

- object-src -> Defines the sources for the ,, and elements.

- script-src -> Defines the sources for JavaScript elements.

- img-src	-> Defines the sources from which images can be loaded.

- form-action -> Defines valid endpoints for submission from tags.

- media-src -> Defines the sources from which images can be loaded.

- manifest-src -> Defines the allowable contents of web app manifests.

- base-url -> Defines which URLs can appear in a page’s <base> element.

- frame-ancestors -> Defines the sources that can embed the current page.

- child-src	-> Defines the sources for workers and embedded frame contents.

- connect-src	-> Defines the sources that can be loaded using script interfaces.

---------------------------

# Type Content Security Policy:

- report only – Magento reports the policy violations but does not act upon it. It is mainly used for debugging. CSP works in this mode by default.

- restrict mode – Magento acts in the case of policy violations.

---------------------------

# Status Script


| Tool  | Status    
|---------|---------|
| Tool 1  | Work partly   |
| Tool 2  | Everything Works    |
| Tool 3  | Everything Works    |


- # (Tool 1)
## Type CSP Code 
### Work

- script-src
- style-src
- font-src
- frame-ancestors
- connect-src
- img-src

### Not Work

- default-Src 
- base-Url 
- child-Src 
- form-action 	
- manifest-src 
- media-src 
- object-src 

## Auto detect Domains (detect host in log file)
### Work
| Letter  | Tld    
|---------|-----------|
| a | ac ad ae af ag ai al am an ao aq ar as at au aw ax az aero asia
| b | ba bb bd be bf bg bh bi bj bm bn bo br bs bt bv bw by bz biz
| c | ca cc cd cf cg ch ci ck cl cm cn co cr cu cv cx cy cz cat com coop
| d | de dj dk dm do dz ec ee eg eh er 
| e | es et eu edu
| f | fi fj fk fm fo fr 
| g | ga gb gd ge gf gg gh gi gl gm gn gp gq gr gs gt gu gw gy gov
| h | hk hm hn hr ht hu 
| i | id ie il im in io iq ir is it int info
| j | je jm jo jp jobs
| k | ke kg kh ki km kn kp kr kw ky kz 
| l | la lb lc li lk lr       
| m | mil mobi

### Not Work 
- All the others

