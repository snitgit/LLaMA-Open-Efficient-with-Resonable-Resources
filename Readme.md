# LLaMA Learning

 "... a collection of foundation language models ranging from 7B to 65B parameters. We train our models on trillions of tokens, and show that it is __possible to train state-of-the-art models__ using _publicly available datasets exclusively, without resorting to proprietary and inaccessible datasets_".[1]


### How to inference:
https://github.com/juncongmoo/pyllama

### Download Model:
https://github.com/shawwn/llama-dl

$ curl -o- https://raw.githubusercontent.com/shawwn/llama-dl/56f50b96072f42fb2520b1ad5a1d6ef30351f23c/llama.sh | bash


### Installation extend to conda previous environment on NLP

$ conda activate nlp

$ curl -o- https://raw.githubusercontent.com/shawwn/llama-dl/56f50b96072f42fb2520b1ad5a1d6ef30351f23c/llama.sh | bash

$  pip install pyllama

$ cd NLP/LLaMA

$ git clone https://github.com/juncongmoo/pyllama.git

$ cd pyllama

$ export CKPT_DIR=/home/snit.san/NLP/LLaMA/7B

$ export TOKENIZER_PATH=/home/snit.san/NLP/LLaMA/tokenizer.model


### Interfence on NVIDIA A100 
$ python inference_driver.py --ckpt_dir $CKPT_DIR --tokenizer_path $TOKENIZER_PATH

Prompt: ['I believe the meaning of life is']

🦙LLaMA: I believe the meaning of life is to become an adult and live happily ever after.
I believe the meaning of life is to become an adult and live happily ever after. So what do you think the meaning of life is? My answer is very simple because when I think of life, I think of myself. I think of myself doing activities that I enjoy. I think of myself going to school, playing with my family, and hanging out with friends. I think of myself becoming an adult and living happily ever after. To become an adult, I think I need to go to school, get my degree, and then get a job. I think that is where I am going to find the meaning of life. I can find the meaning of life by working at a job that I like. I think it is very important that you like what you are doing because you will be doing it for most of your life. I am going to go to school for computers so that I can get a degree. Then I can get a job working for a computer company and I will be doing what I like. I think that is the meaning of life. I think you can find the meaning of life by becoming an adult and living happily ever after.
What do you think is the meaning
****************************** GPU/CPU/Latency Profiling ******************************
[2023-03-10 20:05:04.269518 - 20:05:46.786883]  [100.00%] 🟢_root_time(42.5174)
                                                            [OH:454999us]
[2023-03-10 20:05:04.269518 - 20:05:29.769092]  [ 59.97%]    |___load_llama(25.4996)
[2023-03-10 20:05:29.845480 - 20:05:46.786883]  [ 39.85%]    l___generate(16.9414)

[  0.000 - 14779.000]  [100.00%] 🟢_root_total_gpu_memory_mb_nvidia_smi(14779.0000)
[  0.000 - 14399.000]  [ 97.43%]    |___load_llama(14399.0000)
[14399.000 - 14779.000]  [  2.57%]    l___generate(380.0000)

[      253.547 -      2349.547]  [100.00%] 🟢_root_get_memory_mb(2096.0000)
[      253.547 -      1376.176]  [ 53.56%]    |___load_llama(1122.6289)
[     1376.176 -      2349.547]  [ 46.44%]    l___generate(973.3711)


==========================================================================


### Start a web server

The following command will start a flask web server, actually fastAPI?:

$ conda install pydantic -c conda-forge

$ conda install fastapi -c conda-forge

$ conda install uvicorn  -c conda-forge 

$ cd apps/flask

$ python web_server_single.py  --ckpt_dir $CKPT_DIR --tokenizer_path $TOKENIZER_PATH


### Test with Postman alternative by command line json posting:
We can modify port to start up __fastapi__ such as 5000.

$  curl --header "Content-Type: application/json"   --request POST   --data '{  "prompts": ["I believe the meaning of life is" ],  "max_gen_len": 100,"temperature": 0.8,  "top_p": 0.95}' http://127.0.0.1:5000/llama/

#### The result :

{"responses":["I believe the meaning of life is to serve God and to be happy. When I am of service to others, I am happy. When I am happy, I am in a state of peace. When I am in a state of peace, I am in a state of oneness with God. When I am in a state of oneness with God, I am completely happy. It is a state of bliss, a state of joy, and I am complete. I am content and I am grateful for all that is."]}(qiskit-multi-node) snit.san@zeta:~/NLP/LLaMA/pyllama/apps/flask$


### Multiple GPUs:
$ export TARGET_FOLDER=/home/snit.san/NLP/LLaMA/
$ export MODEL_SIZE=13B


$ torchrun --nproc_per_node MP example.py --ckpt_dir $TARGET_FOLDER/$MODEL_SIZE --tokenizer_path $TARGET_FOLDER/tokenizer.model

#### For example 13B:
$ torchrun --nproc_per_node 2 example.py --ckpt_dir $TARGET_FOLDER/$MODEL_SIZE --tokenizer_path $TARGET_FOLDER/tokenizer.model



#### Different models require different MP values:

| Model Size | MP Rank |
|------------|---------|
| 7B         | 1       |
| 13B        | 2       |
| 30B        | 4       |
| 65B        | 8       |

### References and Student path
1. Original Paper

https://arxiv.org/abs/2302.13971

2. Paper on Video:

https://www.youtube.com/watch?v=E5OnoYF2oAk



3. Main source of learing

 https://github.com/juncongmoo/pyllama/tree/a8bf166571f228d2c988a26e31d8ce65612bc2da



Next ... ChatLLaMA:

https://github.com/juncongmoo/chatllama






