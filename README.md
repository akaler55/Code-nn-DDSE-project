# DDSE_project-replication-_code-nn

## Steps For building C# and SQL language model
Requirements

* Torch (http://torch.ch/docs/getting-started.html)
* Cutorch
* antlr4 for parsing C# (pip install antlr4-python2-runtime)

Setup environment

`export PYTHONPATH=~/ Csharp_SQL/src/:~/ Csharp_SQL/src/sqlparse`
`export CODENN_DIR=~/ Csharp_SQL/`
`export CODENN_WORK=./workdir`

Build both csharp and sql datasets

Install modified sqlparse

`cd  Csharp_SQL/src/sqlparse/`
`sudo python setup.py install`

Build datasets

`cd Csharp_SQL/src/model`
`./buildData.sh`

Train codenn models and predict on test set

`./run.sh {sql|csharp}`

## Steps For building Python language model
Requirements

* torch==1.4.0
* transformers==2.5.0
* filelock

```shell
cd RoBERTa

lang=python #programming language
lr=5e-5
batch_size=64
beam_size=10
source_length=256
target_length=128
data_dir=../data/python
output_dir=model/$lang
train_file=$data_dir/$lang/train.txt
dev_file=$data_dir/$lang/valid.txt
eval_steps=1000
train_steps=50000 
pretrained_model= roberta-base

python code2nl/run.py --do_train --do_eval --model_type roberta --model_name_or_path $pretrained_model --train_filename $train_file --dev_filename $dev_file --output_dir $output_dir --max_source_length $source_length --max_target_length $target_length --beam_size $beam_size --train_batch_size $batch_size --eval_batch_size $batch_size --learning_rate $lr --train_steps $train_steps --eval_steps $eval_steps 
```
