# List-S3-AWS
### Script para listagem de buckets s3 e seus tamanhos.

Etapa 1: (Vai abrir um editor e automaticamente criar o arquivo “buckets.sh”)

  -     #vi buckets.sh

Etapa 2: (Dentro do editor que foi aberto na etapa acima, você cola esse código abaixo, salva e fecha o arquivo “buckets.sh”)

  -     #!/bin/bash

        while IFS= read -r bucket_name; do
            size=$(aws s3api list-objects --bucket "$bucket_name" --output json --query "sum(Contents[].Size)" --no-paginate)
            size_gb=$(awk "BEGIN{printf \"%.2f\", $size / 1024 / 1024 / 1024}")
            echo "Bucket: $bucket_name"
            echo "Tamanho: $size_gb GB"
            echo ""
        done < $buckets.txt

Etapa 3: (Para alterar as permissões do arquivo “buckets.sh” o tornando executável)

  -     chmod +x buckets.sh

Etapa 4: (Esse comando vai listar todos os buckets da conta, e printar apenas a terceira coluna do retorno, que é a coluna dos nomes, já salvando e criando automaticamente o arquivo “buckets.txt” que é onde o retorno será armazenado)

  -     aws s3 ls | awk {'print $3'} > buckets.txt

Etapa 5: (Comando para executar o script que vai retornar o tamanho e o nome dos buckets, o arquivo “Buckets_size.txt” será gerado automaticamente e armazenará o retorno do nosso script)

  -     ./buckets.sh buckets.txt > Buckets_sizes.txt

Etapa 6: (Para ver o arquivo que contém os dados dos buckets, que foi criado na etapa acima)
  -     cat Buckets_sizes.txt
  
  - Obs: (Esse script roda dentro do CloudShell na AWS, e vai listar os buckets referente a conta que você estiver logado)
