If you add some specific files to the same folder as GAM.exe (or gam.py), you can alter the behavior of GAM.  Each file has to exist to do its job - there is no specific content required in the file.

` nocache.txt `
The cache will be disabled at the cost of some performance.
https://groups.google.com/d/msg/google-apps-manager/j24xT9lGYYY/bn-m4kud-hoJ

` noupdatecheck.txt `
Update checks will be disabled.  (Helpful when running GAM from an unattended batch file.)
https://groups.google.com/d/msg/google-apps-manager/RAKFcr7Y7Vs/2obG5hU43hYJ

` nobrowser.txt `
Use during initial installation and configuration on a computer without a web browser. GAM will display a link which you can copy and open from a computer running a browser in order to manually authorize.

` debug.gam `
Show debugging output
/google-apps-manager/source/browse/trunk/gam.py - line 166
