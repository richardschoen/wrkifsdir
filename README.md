# Work with IFS Directories - An useful 5250 alternative to WRKLNK 
The WRKIFSDIR command is a useful, extensible WRKLNK-like 5250 directory explorer for the Integrated File System (IFS).   

You can define your own user defined options which makes this utility very useful in today's world of open source apps on IBM i.   

The code has been adapted from the IFSPOP utility by Ted Holt/Mark Keck published back in 2013.    

IFSPOP was a nod to the old S/36 POP utility which was the predecessor for PDM on IBM i.   

Here's the original article, but original download no longer available so I packaged it into a save file format so you can build and run it on your IBM i.   

# Installing 
Simply upload the save file to ```/tmp/wrkifsdir.savf``` and run the following commands.

Create the temporary save file    
```CRTSAVF FILE(QTEMP/TEMPSAVF)```  

Copy from the IFS to temporary save file     
```
CPYFRMSTMF FROMSTMF('/tmp/wrkifsdir.savf')              
           TOMBR('/qsys.lib/qtemp.lib/tempsavf.file')   
           MBROPT(*REPLACE)                             
           CVTDTA(*NONE)                                
```           

Restore the WRKIFSDIR library from save file   
```RSTLIB SAVLIB(WRKIFSDIR) DEV(*SAVF) SAVF(QTEMP/TEMPSAVF) ```

Create the objects in the WRKIFSDIR library    
```
CRTCLPGM PGM(WRKIFSDIR/SRCWRKBLDC) SRCFILE(WRKIFSDIR/QCLSRC)

CALL PGM(WRKIFSDIR/SRCWRKBLDC)

```         

Using the WRKIFS command
```

Go to menu
GO WRKIFSDIR/WRKIFSDIR

Just use the command
WRKIFSDIR/WRKIFSDIR
```

The 5250 interface will be shown by default, but if you prompt you can specify a starting IFS directory that exists.
```
Ex: WRKIFSDIR DIR('/tmp')
```

Have fun and let me know if you create any good user defined options for ```WRKIFSDIR```





