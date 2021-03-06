flashgg
=======

Before you start, **please take note** of these warnings and comments:
* **N.B.** The setup script will check out many packages and take a while!
* **N.B.** You can ignore "error: addinfo_cache" lines. 

Supported releases:
* 10_2_9

 ```
 cmsrel CMSSW_10_2_9
 cd CMSSW_10_2_9/src
 cmsenv
 git cms-init
 cd $CMSSW_BASE/src 
 git clone -b dev_legacy_runII https://github.com/cms-analysis/flashgg 
 source flashgg/setup_10_2_X.sh
 ```

If everything now looks reasonable, you can build:
 ```
 cd $CMSSW_BASE/src
 scram b -j 4
 ```

And a very basic workflow test:
 ```
 cd $CMSSW_BASE/src/flashgg
 cmsRun MicroAOD/test/microAODstd.py processType=sig datasetName=glugluh # or processType=data depending on input file
 cmsRun Taggers/test/simple_Tag_test.py
 cmsRun Taggers/test/diphotonsDumper_cfg.py
 cmsRun Systematics/test/workspaceStd.py processId=ggh_125 doHTXS=1
 ```

These are just some test examples; the first makes MicroAOD from a MiniAOD file accessed via xrootd, 
the second produces tag objects and screen output from the new MicroAOD file,
and the other two process the MicroAOD file to test ntuple and workspace output.

The setup code will automatically change the initial remote branch's name to upstream to synchronize with the project's old conventions.  
The code will also automatically create an "origin" repo based on its guess as to where your personal flashgg fork is.
Check that this has worked correctly if you have trouble pushing.  (See setup_*.sh for what it does.)

