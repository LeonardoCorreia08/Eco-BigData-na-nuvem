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

## Instruções

* Acessar S3: https://s3.console.aws.amazon.com/s3/ 
  * Criar estrutura de data lake : _dio-live-datalake_
  * Criar estrutura de pastas:
    * _data_
    * _output_
    * _temp_
* Acessar EMR: https://console.aws.amazon.com/elasticmapreduce/
    * O cluster será criado pelo MrJob e não pelo console
    * Infraestrutura como código 
* Criar chave SSH
    * Acessar  Console do EC2: https://console.aws.amazon.com/ec2/ -> Key Pairs -> Create Key Pair	
    * Download .pem file
* Obter Id e chave secreta AWS para configurar MrJob
   * Profile
   * My Security Credentials: https://console.aws.amazon.com/iam/home?region={region}#/security_credentials
   * Access Keys - Create new access key
   * Fazer download - única chance de visualizar

## Execução
1. Faça o upload do arquivo de texto (ex: `sherlock.txt`) para o diretório de dados no seu S3.
2. Configure suas credenciais e chaves SSH editando o arquivo `mrjob.conf`.
3. Execute o job apontando para o cluster EMR (que será criado dinamicamente pelo MrJob):
```bash
python3 src/LeoCorreia-wordcount-test.py -r emr s3://{seu_bucket}/data/sherlock.txt --output-dir=s3://{seu_bucket}/output/logs1 --cloud-tmp-dir=s3://{seu_bucket}/temp/
