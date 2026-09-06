# Ecossistema de Big Data na Nuvem (AWS EMR)

Este repositório contém a infraestrutura como código e scripts Python para execução de análise de dados utilizando MapReduce na AWS.

## Pré-requisitos
* Criar um *Key Pair* no console do EC2 e realizar o download do arquivo `.pem`.
* Obter seu *Access Key ID* e *Secret Access Key* na página de *Security Credentials* (IAM).
* Criar um ambiente virtual Linux/Ubuntu e instalar as dependências necessárias executando `pip install boto3 mrjob`.

## Estrutura do Data Lake (Amazon S3)
Acesse o console do S3 e crie uma estrutura baseada no padrão `dio-live-datalake` contendo as seguintes pastas:
* `s3://{seu_bucket}/data/`
* `s3://{seu_bucket}/output/`
* `s3://{seu_bucket}/temp/`

## Execução
1. Faça o upload do arquivo de texto (ex: `sherlock.txt`) para o diretório de dados no seu S3.
2. Configure suas credenciais e chaves SSH editando o arquivo `mrjob.conf`.
3. Execute o job apontando para o cluster EMR (que será criado dinamicamente pelo MrJob):
```bash
python3 src/LeoCorreia-wordcount-test.py -r emr s3://{seu_bucket}/data/sherlock.txt --output-dir=s3://{seu_bucket}/output/logs1 --cloud-tmp-dir=s3://{seu_bucket}/temp/
