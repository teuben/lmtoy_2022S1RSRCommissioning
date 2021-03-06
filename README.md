# 2022S1RSRCommissioning

This is mostly for linechecks now, but also includes historic data from 2018 (50m), 
and 2014,2015,2016 (32m)

The following RSR projects were done in this 2022 session:

       ProjectId     <ObsNum  mode    object

 	2021-S1-MX-26    100441  RSR     PG.../IRAS...   ?
	2021-S1-US-17    100101  RSR     J1557+1540      ?
	2021-S1-US-19    100474  RSR     Cyg_X-1         ?
	2021-S1-MX-34    100394  RSR     NGP*            Alfredo
	2021-S1-UM-11    100334  RSR     J*.*            MinYun

# sources

The command

      lmtinfo.py grep 2022 LineCheck Bs | awk '{print $5}' | sort | uniq -c

should give something like this

      2 1051+213
      1 1146+399
      3 3c279
     21 I10565
     12 I12112
     16 I17208
      2 I23365
      1 ObsNum
      2 bllac
      8 mwc349a

According to http://wiki.lmtgtm.org/lmtwiki/RSR%20Spectral%20Line%20Check?action=AttachFile&do=view&target=LineCheckSources.pdf
the fluxes of the sources we cover here are (for 32m dish)

      I10565      68 mK
      I17208      60 mK
      I23365      16 mK


# How to run

Normally the command
     
     ./mk_runs.py
	 
generates the text file for slurm, but currently RSR cannot run in parallel. But when it does,
this will be the command

      slurm_lmtoy.sh linecheck.run1

to run *everything* (historic data too).  And

      slurm_lmtoy.sh linecheck.run2
	  
to run the combinations.

## current hack

Since the RSR pipeline code is not parallel yet, this script needs to be run serially. For this a hack is needed:

      sbatch_lmtoy.sh obsnum=1 bash `pwd`/linecheck.run1
	  
since we are faking obsnum=1, only one such script can be run.  As of Jul 19, 2022, the code can be run in parallel,
and thus

      sbatch_lmtoy.sh linecheck.run1

can be used instead.


## Historic data

This script generator also has the historic (2018 in 50m, an 2014,15,16 with a 32m dish) added, but adding an 'a' to the source name.
See also http://wiki.lmtgtm.org/lmtwiki/RSR%20Spectral%20Line%20Check and 
http://wiki.lmtgtm.org/lmtwiki/RSR%20Spectral%20Line%20Check?action=AttachFile&do=view&target=LineCheckSources.pdf
