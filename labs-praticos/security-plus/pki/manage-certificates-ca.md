# Lab: Manage Certificates on a Certificate Authority

## Objetivo
Realizar tarefas de gerenciamento de certificados em uma autoridade certificadora (CA) corporativa, incluindo aprovação e negação de solicitações pendentes, revogação de um certificado comprometido e reversão de uma revogação.

## Metodologia
- Acesso à máquina virtual CorpCA pelo Hyper-V Manager, no servidor CorpServer2
- Abertura do console Certification Authority pelo Server Manager
- Aprovação das solicitações pendentes de certificados de smart card
- Negação da solicitação pendente de certificado de servidor web
- Revogação de certificado com o motivo Key Compromise
- Reversão (unrevoke) de um certificado revogado

## Processo
Realizei o lab a partir do cenário proposto, no qual a CorpCA, a autoridade certificadora da rede, é um servidor convidado hospedado no CorpServer2. Primeiro, acessei a VM da CorpCA pelo **Hyper-V Manager** e abri o console **Certification Authority** pelo Server Manager.

Em **Pending Requests**, usei a opção **Issue** para aprovar as solicitações de certificado de **smart card** dos usuários `tsutton` e `mmallory`. Na mesma pasta, usei a opção **Deny** para negar a solicitação de certificado de servidor web do `CorpSrv12`.

Em seguida, em **Issued Certificates**, localizei o certificado do usuário `bchan.CorpNet.com`, que havia perdido o smart card, e o revoguei com o código de motivo **Key Compromise**. Por fim, em **Revoked Certificates**, localizei o certificado do `CorpDev3` e usei a opção **Unrevoke Certificate** para reativá-lo.

## Observações e aprendizado
Esse lab mostrou na prática o **ciclo de vida de um certificado** em uma PKI. Cada ação fica em uma pasta diferente do console da CA: aprovação e negação em *Pending Requests*, revogação em *Issued Certificates* e reversão em *Revoked Certificates*.

Também reforcei a escolha do **motivo de revogação**: o **Key Compromise** é usado quando a chave privada foi comprometida ou o dispositivo que a guarda foi perdido, como no caso do smart card do bchan. Além disso, aprendi que só é possível desrevogar um certificado que foi revogado com o motivo **Certificate Hold**, que é a única revogação reversível.

A revogação é publicada na **CRL (Certificate Revocation List)**, e os clientes também podem consultar o status do certificado por **OCSP**, o que garante que certificados comprometidos deixem de ser aceitos.

## Resultado
Lab concluído com sucesso (4/4, 100%), com tempo de 05:33: solicitações de smart card aprovadas, solicitação do CorpSrv12 negada, certificado do bchan revogado por Key Compromise e certificado do CorpDev3 desrevogado.
