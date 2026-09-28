## Objetivo
Identificar tentativas de engenharia social (phishing, spear phishing e hoax) 
em uma caixa de e-mails simulada, classificando cada mensagem como segura ou maliciosa.

## Metodologia
- Análise do remetente (nome de exibição vs. endereço real)
- Verificação de links: passar o mouse sobre cada link para conferir 
  se a URL de destino correspondia ao texto exibido
- Inspeção de anexos (tipo de arquivo, contexto da mensagem)
- Identificação de erros de digitação/gramática
- Análise do tom da mensagem (urgência, ameaça, apelo à autoridade)

## Processo
Analisei uma caixa de entrada com diversos e-mails suspeitos, aplicando 
a metodologia acima a cada mensagem antes de decidir se ela deveria ser 
mantida ou deletada.

Em vários e-mails, o texto do link não correspondia à URL real de destino — 
uma técnica clássica de phishing. Em dois casos, o link levava diretamente 
a um endereço IP puro, sem qualquer disfarce de domínio, o que é um forte 
indicador de atividade maliciosa (empresas legítimas não distribuem 
conteúdo através de IPs nus).

Também identifiquei anexos enviados com mensagens genéricas, sem contexto, 
claramente elaboradas para induzir o clique (uma tática de lure-based 
vector). Um dos casos mais relevantes foi um anexo apresentado como imagem, 
mas cujo link real apontava para um arquivo .exe — um padrão típico de 
malware disfarçado (executable file lure).

Outro e-mail se destacou por combinar múltiplos erros de digitação com um 
tom de urgência extrema, ameaçando a exclusão da conta do usuário caso ele 
não realizasse login imediatamente através do link fornecido — uma 
combinação clássica das técnicas de motivação "urgency" e "threatening" 
usadas em engenharia social.

## Erro cometido e aprendizado
Durante o lab, deletei incorretamente um e-mail que era legítimo. Ele 
apresentava um selo verde ao lado do remetente, sem nenhuma indicação 
textual do que ele representava. Como o link embutido na mensagem apontava 
para um domínio .xyz (pouco comum e sem relação clara com a organização), 
interpretei esse conjunto de sinais como suspeito e optei por deletar o 
e-mail.

Na correção, descobri que o selo indicava uma assinatura digital verificada 
(hash + criptografia), que comprovava a autenticidade e integridade da 
mensagem — ou seja, o e-mail era, de fato, legítimo.

**Aprendizado:** esse caso reforçou que uma assinatura digital verificada 
é um indicador de confiança mais forte do que a aparência superficial de 
um domínio. Da próxima vez, buscarei explorar mais a interface antes de 
decidir (ex: clicar diretamente no ícone de verificação para checar se há 
mais detalhes disponíveis), em vez de basear a decisão apenas na 
combinação de sinais visuais sem confirmar seu significado técnico.

## Resultado
8/9 (89%) de acerto no lab.
