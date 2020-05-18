# Readme First 
part of class project
https://github.com/ekapolc/ASR_classproject

Step ::

#0. Install docker kaldi image
    you must have docker in you computer 
    kaldi is most capitible with linux base OS

    docker run -it -v <path_to_backup_folder>:/data burin010n/kaldi /bin/bash

#1. Mount data folder to docker 

    1.1 Make sure 
        "$(pwd)" == Datapath which these folder are extracted. 
        
        in docker :: 
        Dicratory is yesno kaldi example

        1.1.1 Mount data and run docker 

        docker run -v "<Mount diratory>":/kaldi/egs/yesno/s5/data -it <your images kaldi_id>

        eg. docker run -v "$(pwd)":/kaldi/egs/yesno/s5/data -it   my use image idbfc630204570

        # kaldi_id can check from 
            1.1.1.1 docker images 
            1.1.1.2 find copy burin010n/kaldi  and copy #IMAGE ID  
   1.2 make sure director format in  ../data in docker is
   
        data 
        ├───train_yesno
        
        │   ├───text
        
        │   ├───utt2spk
        
        │   ├───spk2utt
        
        │   └───wav.scp
        
        └───test_yesno
        
            ├───text
            
            ├───utt2spk
            
            ├───spk2utt
            
            └───wav.scp
            
        └───dict
        
            ├───lexicon.txt
            
            ├───silence_phones.txt
            
            ├───optional_silence.txt
            
            └───phones.txt
            
        └───sound
        
            ├───text
            
            ├───utt2spk
            
            ├───spk2utt
            
            └───wav.scp

# 2. Generate Dict
    run in /kaldi/egs/yesno/s5/ directory in docker

    utils/prepare_lang.sh to check in your directory
    eg.
        utils/prepare_lang.sh 'data/dict/' 'SIL' ' data/dict/temp' 'data/lang'
     
     utils/prepare_lang.sh <RAW_DICT_PATH> <OOV> <TEMP_DIR> <OUTPUT_DIR>
        <RAW_DICT_PATH>: data/local/dict
        <OOV>: "<SIL>"
        <TEMP_DIR>: Could be anywhere. I'll just put a new directory tmp inside dict.
        <OUTPUT_DIR>: This output will be used in further training. Set it to data/lang.


# 3. Feature extraction and training

// use this to run  
// in progess 

steps/make_mfcc.sh --nj  'data/train/' 'data/train/' 'data/mfcc/train/'

curent problem :: 
    steps/make_mfcc.sh --nj data/train/ data/train/ data/mfcc/train/
    
     utils/validate_data_dir.sh: data/train//utt2spk has wrong format.
     
    seq: invalid floating point argument: 'data/train/'
    
    Try 'seq --help' for more information.
    
    steps/make_mfcc.sh: [info]: no segments file exists: assuming wav.scp indexed by utterance.
    seq: invalid floating point argument: 'data/train/'
    
    Try 'seq --help' for more information.
    Usage: split_scp.pl [--utt2spk=<utt2spk_file>] in.scp out1.scp out2.scp ...
       or: split_scp.pl -j num-jobs job-id [--one-based] [--utt2spk=<utt2spk_file>] in.scp [out.scp]
    where 0 <= job-id < num-jobs, or 1 <= job-id <- num-jobs if --one-based.
