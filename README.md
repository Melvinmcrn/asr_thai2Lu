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


3. Coming soon
