# YR-Fragments
MC configurations for the YR 

----- cmsdriver recipe for YR campaign -----

1. GEN-SIM 

cmsDriver.py Configuration/GenProduction/python/BPH-PhaseIITDRFall17GS-00001-fragment.py --fileout file:BPH-PhaseIITDRFall17GS-00001.root --mc --eventcontent RAWSIM --datatier GEN-SIM --conditions 93X_upgrade2023_realistic_v2 --beamspot HLLHC14TeV --step GEN,SIM --nThreads 2 --geometry Extended2023D17 --era Phase2_timing --python_filename BPH-PhaseIITDRFall17GS-00001_1_cfg.py --no_exec --customise Configuration/DataProcessing/Utils.addMonitoring -n 5051 || exit $? ; 

2. DIGI-RECO 

cmsDriver.py step1 --fileout file:BPH-PhaseIITDRFall17DR-00001_step1.root --mc --eventcontent FEVTDEBUGHLT --pileup NoPileUp --customise SLHCUpgradeSimulations/Configuration/aging.customise_aging_1000,Configuration/DataProcessing/Utils.addMonitoring --datatier GEN-SIM-DIGI-RAW --conditions 93X_upgrade2023_realistic_v2 --beamspot HLLHC14TeV --step DIGI:pdigi_valid,L1,DIGI2RAW,HLT:@fake --nThreads 8 --geometry Extended2023D17 --era Phase2_timing --python_filename BPH-PhaseIITDRFall17DR-00001_1_cfg.py --no_exec -n 960 || exit $? ; 

cmsDriver.py step2 --filein file:BPH-PhaseIITDRFall17DR-00001_step1.root --fileout file:BPH-PhaseIITDRFall17DR-00001.root --mc --eventcontent RECOSIM --runUnscheduled --customise SLHCUpgradeSimulations/Configuration/aging.customise_aging_1000,Configuration/DataProcessing/Utils.addMonitoring --datatier GEN-SIM-RECO --conditions 93X_upgrade2023_realistic_v2 --beamspot HLLHC14TeV --step RAW2DIGI,L1Reco,RECO --nThreads 8 --geometry Extended2023D17 --era Phase2_timing --python_filename BPH-PhaseIITDRFall17DR-00001_2_cfg.py --no_exec -n 960 || exit $? ; 

3. AODSIM/MINIAODSIM

cmsDriver.py step1 --filein "dbs:/BdToKstarMuMu_BMuonFilter_SoftQCDnonD_TuneCP5_14TeV-pythia8-evtgen/PhaseIITDRFall17DR-noPU_93X_upgrade2023_realistic_v2-v1/GEN-SIM-RECO" --fileout file:BPH-PhaseIISpr18AODMiniAOD-00001.root --mc --eventcontent AODSIM,MINIAODSIM --runUnscheduled --datatier AODSIM,MINIAODSIM --conditions 93X_upgrade2023_realistic_v5 --beamspot HLLHC14TeV --customise_commands "process.AODSIMoutput.outputCommands.append('keep recoTrackExtras_generalTracks_*_*')" --step PAT --nThreads 8 --geometry Extended2023D17 --era Phase2_timing --python_filename BPH-PhaseIISpr18AODMiniAOD-00001_1_cfg.py --no_exec --customise Configuration/DataProcessing/Utils.addMonitoring -n 1920 || exit $? ; 

