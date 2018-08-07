<!-- TITLE: Debugging -->
<!-- SUBTITLE: Diverses informations sur les debuggers *nix et Windows.-->

# Debuggers 
* Sur windows nous avons **x64dbg** qui ressemble beaucoup à *OllyDbg* et complétement libre. (*Une vraie perle!*)
> Le GIT : https://github.com/x64dbg/x64dbg
* Sur les systèmes * nix il y a **gdb** ou encore **lldb** plus récent.

### Gdb
 
* Pour lancer une application qui doit lire des infos sur l'entrée standard. Il faut tout d'abord les placer dans un fichier:
 
```sh
perl -e 'print "A"x2000;' > myfile
gdb ./MonApp
run < myfile
```

* Pour print le contenu de la stack : `x/200x $sp`
* Pour print l'adresse d'une fonction : `print myfunc`


