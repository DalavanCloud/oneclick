Oneclick is supporting tool used to automate some of the workload when using [EACirc Framework](https://github.com/crocs-muni/EACirc/wiki). Usually EACirc have to be executed in many different configurations and each configuration multiple times. After execution, the results from each workunit have to be processed into bigger picture. Doing this process by hand is time consuming and prone to errors. In answer to this, Oneclick was developed. Aim of this project is to do most of the mind-numbing work instead of researchers so that they can spend their time with researching things, not Bash scripts.

Currently Oneclick allows user to:
* Generate multiple different configuration files for EACirc based on simple rules.
* Generate scripts used for running of EACirc on remote server as well as scripts for download of results.
* Post-process output of multiple EACirc runs, detect errors or inconsistencies and give final result of whole run.

For more information and details see [project wiki pages](https://github.com/crocs-muni/oneclick/wiki).

## Guick Start Guide
### Linux
```
git submodule init
git submodule update
mkdir build
cd build
ccmake ...
make
```

## Authors
The framework is developed at the [Centre for Research on Cryptography and Security (formerly Laboratory of Security and Applied Cryptography)](https://www.fi.muni.cz/research/crocs/), [Masaryk University](http://www.muni.cz/), Brno, Czech Republic.

* **Petr Švenda** 2014-now (project lead)
* **Ľubomír Obrátil** 2014-now (Development)
 
## License
EACirc is licenced under MIT Licence, Copyright (c) 2012 Centre for Research on Cryptography and Security. For details on MIT Licence, see file MITLicence.md.

Some sub-parts of the project have their own licencing conditions. The brief list of such sub-parts follows. For up-to-date list of third party code consult [the project's wiki](https://github.com/crocs-muni/oneclick/wiki/Additional-libraries-and-dependencies).

* **TyniXML**  
TyniXML was created by Lee Thomason and is distributed under the zlib/libpng License (full licence included in the project, located at EACirc/tinyXML/). For further details see [project's website](http://www.grinninglizard.com/tinyxml/) or [project's SourceForge site](http://sourceforge.net/projects/tinyxml).
