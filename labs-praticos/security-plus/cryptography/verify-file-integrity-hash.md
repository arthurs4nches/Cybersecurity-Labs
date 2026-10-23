# Lab: Verify File Integrity with Hashing (PowerShell)

## Objetivo
Verificar a integridade de um arquivo baixado (`Release.zip`) calculando o seu 
hash MD5 com o PowerShell e comparando com o hash original armazenado em um 
arquivo de texto, para confirmar se o arquivo foi alterado.

## Metodologia
- Abertura do PowerShell como Administrador
- Cálculo do hash MD5 do arquivo `Release.zip` com `Get-FileHash`
- Leitura do hash original armazenado em `release821hash.txt`
- Comparação dos dois hashes com o operador `-eq`
- Conclusão sobre a integridade do arquivo

## Processo
Comecei tentando calcular o hash pelo CMD com `certutil -hashfile`, mas o 
comando retornou o erro de que `certutil` não é reconhecido como comando 
interno ou externo. Em vez de insistir no CMD, mudei para o PowerShell, que 
é a ferramenta que o lab pedia.

No PowerShell, digitei inicialmente `Get -Filehash`, com espaço, e recebi o 
erro "Get is not recognized". O nome correto do cmdlet é `Get-FileHash`, tudo 
junto. Corrigido isso, o erro passou a ser "Cannot find path": usei o caminho 
`C:\Users\Administrator\Downloads\Release.zip`, mas o arquivo estava em 
`C:\Downloads`, uma pasta na raiz do disco. Conferindo a barra de endereço do 
Explorador de Arquivos, ajustei o comando para:

```powershell
Get-FileHash C:\Downloads\Release.zip -Algorithm MD5
```

Com o hash do arquivo em mãos, abri o `release821hash.txt` no Bloco de Notas 
para ver o hash original e comparei os dois com o `-eq`, colando cada valor 
entre aspas:

```powershell
"HASH_ORIGINAL" -eq "HASH_CALCULADO"
```

O PowerShell retornou `False`, indicando que os hashes são diferentes. Na 
primeira tentativa, esqueci as aspas e o PowerShell tentou executar o hash 
como se fosse um comando, o que também gerou erro.

## Observações e aprendizado
O resultado `False` mostra que o `Release.zip` **não é idêntico ao original**: 
ele foi corrompido ou modificado. Essa é a ideia central de **integridade** 
(a letra "I" da tríade CIA): um hash funciona como uma impressão digital do 
arquivo, e qualquer alteração, mesmo de um único bit, muda completamente o 
valor. Na prática, um arquivo com hash divergente não deve ser executado nem 
confiado.

Pontos técnicos que fixei durante o lab:

- `certutil` é uma alternativa nativa do Windows 
  (`certutil -hashfile <arquivo> MD5`), mas pode não estar disponível 
  dependendo do ambiente.
- `Get-FileHash` devolve um objeto; para pegar só o texto do hash usa-se 
  `(Get-FileHash <arquivo> -Algorithm MD5).Hash`.
- Não existe um cmdlet `Get-CompareHash`: a comparação é feita com `-eq` 
  entre os dois valores.
- Strings no PowerShell precisam estar entre aspas para serem comparadas 
  como texto.
- Atenção ao caminho: `C:\Downloads` é diferente de 
  `C:\Users\<usuário>\Downloads`.
- O `-eq` não diferencia maiúsculas de minúsculas, o que é adequado para 
  hashes hexadecimais.

Também aprendi que o lab pontua pelos **comandos exatos** esperados no roteiro 
(`Get-FileHash Release.zip -a md5`, `Get-Content release821hash.txt` e `-eq`), 
e não apenas pelo resultado. Mesmo com a resposta final correta, os passos 
feitos de forma diferente (caminho completo, `-Algorithm` no lugar de `-a`, 
leitura do `.txt` manualmente no Bloco de Notas em vez de `Get-Content`) não 
foram contabilizados na primeira avaliação.

Por fim, o MD5 é considerado um algoritmo fraco para uso real por ser 
vulnerável a colisões; em cenários reais o recomendado é SHA-256 
(`-Algorithm SHA256`).

## Resultado
Resposta da questão do lab correta (os hashes **não** correspondem), 
confirmando que o `Release.zip` foi alterado. Na primeira avaliação o lab 
marcou 1/4 (25%) por divergência no formato dos comandos esperados, o que 
serviu de aprendizado sobre seguir o roteiro ao pé da letra, depois fiz 4/4 (100%) 
seguindo exatamente o roteiro e comandos esperados pelo lab.
