# Lab: Encrypt Files with EFS (Encrypting File System)

## Objetivo
Proteger o conteúdo da pasta `D:\Finances` em um computador compartilhado, 
usando o EFS do Windows, para que usuários não autorizados não consigam ler 
os arquivos, e liberar o acesso de um usuário específico (John) a um dos 
arquivos adicionando o certificado de criptografia dele.

## Metodologia
- Criptografia da pasta `D:\Finances` e de todo o seu conteúdo (3 arquivos) 
  com o EFS
- Abertura das opções avançadas de atributos do arquivo `2023report.xls`
- Adição do certificado de criptografia do usuário John ao arquivo
- Validação da conclusão pela verificação do lab

## Processo
Parti do cenário proposto: um computador compartilhado no trabalho, onde o 
conteúdo da pasta `D:\Finances` precisava ficar protegido de usuários não 
autorizados. 

Primeiro, abri as propriedades da pasta `D:\Finances`, entrei em **Avançado** 
e marquei a opção **Criptografar o conteúdo para proteger os dados**. Ao 
aplicar, escolhi estender a criptografia à pasta, subpastas e arquivos, de 
modo que os 3 arquivos dentro dela também ficassem protegidos. A partir daí, 
o conteúdo passa a ser cifrado com a chave associada ao meu usuário, e outros 
usuários do mesmo computador não conseguem abrir os arquivos.

Em seguida, precisei dar acesso ao usuário John apenas ao arquivo 
`D:\Finances\2023report.xls`. Abri as propriedades do arquivo, fui em 
**Avançado > Detalhes** e usei a opção de **Adicionar** um usuário, 
selecionando o certificado de criptografia do John. Com isso, o certificado 
dele passou a constar na lista de usuários autorizados a descriptografar 
aquele arquivo específico, sem liberar o restante da pasta.

## Observações e aprendizado
O EFS é um recurso de **criptografia em nível de arquivo e pasta**, nativo do 
sistema de arquivos NTFS, que protege **dados em repouso** (data at rest). 
Ele funciona de forma transparente para o usuário dono: quem criptografou 
abre os arquivos normalmente, enquanto outros usuários recebem acesso negado, 
mesmo que tenham permissões NTFS sobre o arquivo.

Pontos que fixei durante o lab:

- O EFS é atrelado ao **certificado e à chave do usuário**. Para dar acesso a 
  outra pessoa, não basta compartilhar a senha: é preciso adicionar o 
  **certificado de criptografia** dela ao arquivo.
- O compartilhamento é feito **por arquivo**, e não por pasta. Por isso o 
  acesso do John foi concedido somente ao `2023report.xls`.
- Perder o certificado/chave EFS pode significar **perder o acesso aos dados**. 
  Por isso é importante fazer backup do certificado e da chave.
- O EFS depende do sistema de arquivos **NTFS** e de edições do Windows que o 
  suportam (como Pro e Enterprise).
- Diferença para o **BitLocker**: o BitLocker criptografa o **volume/disco 
  inteiro**, enquanto o EFS criptografa **arquivos e pastas específicos**. Os 
  dois podem ser usados juntos, e esse contraste cai com frequência na prova 
  do Security+.

Esse lab também conecta com o princípio de **confidencialidade** da tríade 
CIA, já que o objetivo foi impedir que usuários sem autorização consigam ler 
os dados.

## Resultado
Lab concluído com sucesso (2/2, 100%): pasta `D:\Finances` e seu conteúdo 
criptografados com EFS, e usuário John adicionado como autorizado para o 
arquivo `2023report.xls`.
