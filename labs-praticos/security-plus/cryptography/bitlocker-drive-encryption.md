# Lab: Configure BitLocker Drive Encryption

## Objetivo
Proteger os dados do volume de sistema (C:) de um computador corporativo 
contra acesso não autorizado em caso de roubo do disco rígido, configurando 
o BitLocker com o apoio do chip TPM da placa-mãe.

## Metodologia
- Habilitação e ativação do TPM (Trusted Platform Module) na BIOS
- Ativação do BitLocker no drive do sistema (C:)
- Backup da chave de recuperação na pasta de rede `\\CorpServer\BU-Office1`
- Criptografia do drive inteiro (Encrypt entire drive)
- Seleção do novo modo de criptografia (New encryption mode)
- Execução da verificação do sistema do BitLocker (system check)

## Processo
Parti do cenário proposto: o funcionário do Office 1 trabalha em um projeto 
sensível, e a gerência temia que, se o disco rígido do computador fosse 
roubado, as informações pudessem ser comprometidas. A solução foi 
criptografar todo o volume do sistema, aproveitando o TPM embutido na 
placa-mãe.

Primeiro, entrei na **BIOS** do computador, **habilitei** o TPM Security e 
depois o **ativei**. Sem essa etapa, o Windows não consegue usar o TPM para 
guardar a chave de criptografia do volume.

De volta ao Windows, liguei o **BitLocker** para o drive do sistema (C:). Na 
etapa de backup da chave de recuperação, escolhi a opção **Save to a file** 
e, em vez de salvar na pasta padrão (Documents), digitei o caminho de rede 
`\\CorpServer\BU-Office1` no campo de nome do arquivo, o que abriu a pasta 
do servidor, e salvei a chave lá. Guardar a chave em um local separado do 
computador é o que permite recuperar os dados caso o acesso normal ao drive 
seja perdido.

Em seguida, escolhi criptografar o **drive inteiro** (Encrypt entire drive), 
e não apenas o espaço em uso, e selecionei o **novo modo de criptografia** 
(New encryption mode). Por fim, deixei marcada a opção de executar a 
**verificação do sistema do BitLocker** antes de iniciar a criptografia, para 
confirmar que o computador consegue ler a chave corretamente na inicialização.

## Observações e aprendizado
O BitLocker é uma solução de **criptografia de disco completo (FDE, Full Disk 
Encryption)**, que protege **dados em repouso** (data at rest). Se o disco for 
removido e colocado em outra máquina, o conteúdo continua ilegível sem a 
chave.

Pontos que fixei durante o lab:

- O **TPM** é um chip de hardware que guarda as chaves de criptografia e 
  verifica a integridade do processo de inicialização. Ele precisa estar 
  habilitado e ativo na BIOS para o BitLocker usá-lo.
- A **chave de recuperação** deve ser guardada em local seguro e separado do 
  computador (aqui, um servidor da rede). Sem ela, perder o acesso normal ao 
  drive pode significar perder os dados.
- **Encrypt entire drive** criptografa também o espaço livre, o que é mais 
  seguro (impede a recuperação de dados antigos apagados), mas leva mais 
  tempo. Já **Used disk space only** é mais rápido, indicado para discos 
  novos.
- O **novo modo de criptografia** (XTS-AES) é o recomendado para discos fixos 
  internos, enquanto o modo compatível serve para unidades que serão usadas 
  em versões mais antigas do Windows.
- A **verificação do sistema** garante que o BitLocker consegue ler a chave 
  antes de criptografar, evitando que o computador fique sem conseguir 
  iniciar.
- Diferença para o **EFS**, que fiz em outro lab: o EFS criptografa arquivos 
  e pastas específicos, enquanto o BitLocker criptografa o **volume inteiro**. 
  Os dois podem ser usados juntos, e essa comparação cai com frequência na 
  prova do Security+.

Esse lab reforça o princípio de **confidencialidade** da tríade CIA: mesmo 
com acesso físico ao hardware, o atacante não consegue ler os dados.

## Resultado
Lab concluído com sucesso (6/6, 100%): TPM habilitado e ativado, BitLocker 
ligado no drive C:, chave de recuperação salva no CorpServer, drive inteiro 
criptografado no novo modo de criptografia e verificação do sistema 
executada.
