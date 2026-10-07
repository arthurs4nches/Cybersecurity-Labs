# Lab: Hide Data with Steganography (OpenStego)

## Objetivo
Ocultar o conteúdo de um arquivo de texto dentro de uma imagem usando o 
OpenStego, protegê-lo com senha e depois extrair os dados para confirmar 
que a esteganografia funcionou corretamente.

## Metodologia
- Abertura do OpenStego pela busca da barra de tarefas
- Seleção do arquivo de mensagem (message file), do arquivo de cobertura 
  (cover file) e do arquivo de saída (output stego file)
- Proteção dos dados embutidos com senha
- Extração dos dados a partir da imagem gerada
- Verificação da integridade do arquivo recuperado

## Processo
Realizei o lab no OpenStego a partir do cenário proposto. Primeiro, 
selecionei o **arquivo de mensagem** `John.txt`, que continha os dados a 
serem ocultados, e o **arquivo de cobertura** `gear.png`, a imagem que 
serviria de "hospedeira". Em seguida, defini o **arquivo de saída** como 
`send.png`, a imagem final com os dados embutidos, e protegi o conteúdo 
com a senha definida pelo lab antes de executar a opção **Hide Data**.

Para validar o resultado, usei a função **Extract Data**, apontando 
`send.png` como arquivo de entrada e a pasta `Export` como destino, 
informando a mesma senha. Por fim, abri o `John.txt` extraído pelo 
Explorador de Arquivos, confirmando que o conteúdo foi recuperado 
integralmente.

## Observações e aprendizado
Esse lab deixou clara a diferença entre **esteganografia** e 
**criptografia**: a esteganografia esconde a *existência* da mensagem, 
enquanto a criptografia esconde o *conteúdo*. Aqui as duas técnicas foram 
combinadas, já que o dado ficou oculto na imagem e ainda protegido por 
senha, o que dificulta tanto a detecção quanto a leitura.

Também ficou claro o lado ofensivo e defensivo da técnica: ela pode ser 
usada para exfiltração discreta de dados ou comunicação encoberta, o que 
torna importante que equipes de segurança saibam identificar sinais como 
arquivos de imagem com tamanho incomum ou diferenças em relação ao 
original, além de usar ferramentas de estegoanálise.

## Resultado
Lab concluído com sucesso (3/3, 100%): dados ocultos em `send.png`, 
protegidos por senha, extraídos e verificados.
