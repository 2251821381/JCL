# JCL
<<Joint Contrastive Learning for Prompt-Based Few-Shot Language Learners>>
if you want to run our code ,you should first  download all dataset acoording to  the download_dataset.sh, and then, run the train.py .
The dataset download address is https://nlp.cs.princeton.edu/projects/lm-bff/datasets.tar
1. cd data
bash download_dataset.sh
2.python tools/generate_k_shot_data.py
3.for seed in 13 21 42 87 100   #### random seeds for different train-test splits
do
    for bs in 40   #### batch size
    do
        for lr in 1e-5    #### learning rate for MLM loss
        do
            for supcon_lr in 1e-5    #### learning rate for SupCon loss
            do
                TAG=exp \
                TYPE=prompt-demo \
                TASK=sst-5 \
                BS=$bs \
                LR=$lr \
                SupCon_LR=$supcon_lr \
                SEED=$seed \
                MODEL=roberta-base \
                bash run_experiment.sh
            done
        done
    done
done

rm -rf result/
# model.png
<img width="751" alt="model2" src="https://user-images.githubusercontent.com/40848730/221091908-3f0409e1-f1da-476f-af3e-20b7596ae17c.png">
# observation.png
<img width="815" alt="observation" src="https://user-images.githubusercontent.com/40848730/221091914-aaf8bc10-4dc4-4a89-8928-b432f0818c47.png">

