﻿---
title: 'Opções de transporte em implantações híbridas do Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Opções de transporte em implantações híbridas do Exchange 2013/Exchange 2007
ms:assetid: 92d9e3ca-8d79-4872-9ff7-0067fcdbd434
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn151301(v=EXCHG.150)
ms:contentKeyID: 54652002
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opções de transporte em implantações híbridas do Exchange 2013/Exchange 2007

Este tópico está em andamento.  

_**Aplica-se a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Nas implantações híbridas, você pode ter caixas de correio que residem em sua organização local e em uma organização do Exchange e também em uma organização do Exchange Online. O transporte híbrido é um componente crítico para fazer com que essas duas organizações separadas pareçam ser uma organização combinada para os usuários e para as mensagens trocadas entre elas. O transporte híbrido faz com que a mensagens que trafegam entre destinatários de qualquer das organizações sejam autenticadas, criptografadas e transferidas usando o protocolo TLS e apareçam como “internas�? para componentes do Exchange, como regras de transporte, registro no diário e políticas de antispam. O transporte híbrido é configurado automaticamente pelo assistente de Configuração Híbrida no Exchange 2013

Para a configuração de transporte híbrido funcionar com o assistente de Configuração Híbrida, o ponto final SMTP local que aceita conexões do Microsoft Exchange Online Protection (EOP), que gerencia o transporte para a organização do Exchange Online, deve ser um servidor de Acesso para Cliente Exchange 2013, um servidor de Transporte de Borda Exchange 2013 ou um servidor de Transporte de Borda do Exchange Server 2010 Service Pack 3 (SP3).


> [!IMPORTANT]
> Não pode haver outros hosts ou serviços SMTP entre os servidores de Acesso para Cliente locais do Exchange 2013 ou servidores de Transporte de Borda do Exchange 2013/Exchange 2010 SP3 e o EOP. As informações adicionadas às mensagens para habilitar recursos de transporte híbrido são removidas quando passam através de um servidor diferente do Exchange 2013, de servidores pré-Exchange 2010 SP3 ou de um host SMTP. Se você possui servidores de Transporte de Borda do Exchange 2010 SP2 implantados em sua organização e deseja utilizá-los para transporte híbrido, eles devem ser atualizados para o Exchange 2010 SP3.



As mensagens de entrada enviadas para destinatários em ambas as organizações a partir de destinatários externos na Internet seguem uma rota de entrada comum. As mensagens de saída enviadas das organizações para destinatários externos na Internet podem seguir uma rota de saída comum ou podem ser enviadas através de rotas independentes.

Você deve escolher como encaminhar mensagens de entrada e de saída quando planejar e configurar a implantação híbrida. A rota adotada pelas mensagens de entrada e de saída enviadas e recebidas por destinatários na organização local e na organização do Exchange Online depende do seguinte:

  - Deseja rotear correio de entrada da Internet para ambas as suas caixas de correio, local e do Exchange Online, por meio do Office 365 e o EOP ou em sua organização no local?
    
    Você pode optar por encaminhar mensagens de entrada da Internet para ambas as organizações através de sua organização local ou através do EOP e da organização do Exchange Online. O roteamento que as mensagens de entrada para ambas as organizações toma depende de se você habilita o transporte de email centralizado ou não em sua implantação híbrida.

  - Deseja rotear os emails de saída para destinatários externos de sua organização do Exchange Online pela sua organização local (transporte de email centralizado) ou deseja roteá-los diretamente para a Internet?
    
    Conhecido como transporte de email centralizado, você pode encaminhar todas as mensagens de caixas de correio no Exchange Online através da organização local antes que elas sejam transmitidas para a Internet. Essa abordagem é útil em cenários de conformidade onde todas as mensagens de entrada e de saída da Internet devem ser processadas por servidores locais. Alternativamente, você pode configurar o Exchange Online para encaminhar mensagens a destinatários externos diretamente na Internet.
    

    > [!TIP]
    > O transporte de email centralizado somente é recomendado para organizações com necessidades de transporte relacionadas a conformidade específicas. Nossa recomendação para organizações do Exchange típicas é não habilitar o transporte de email centralizado.



  - Você deseja implantar um servidor de Transporte de Borda em sua organização local?
    
    Se não deseja expor seus servidores internos do Exchange 2013 unidos por domínio diretamente à Internet, implante os servidores de Transporte de Borda do Exchange 2013 ou servidores de Transporte de Borda do Exchange 2010 SP3 em sua rede de perímetro. Para obter mais informações sobre adição de um servidor de Transporte de Borda à sua implantação híbrida, consulte [Servidores de Transporte de Borda nas implantações híbridas do Exchange 2013/Exchange 2007](edge-transport-servers-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

Independentemente de como você encaminha mensagens enviadas e recebidas da Internet, todas as mensagens enviadas entre a organização local e a organização do Exchange Online utilizam transporte seguro. Para obter mais informações, consulte [Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md), posteriormente neste tópico.

Para saber mais sobre como essas opções afetam o roteamento de mensagens em sua organização, consulte [Roteamento de transporte em implantações híbridas do Exchange 2013/Exchange 2007](transport-routing-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

## Proteção do Exchange Online em implantações híbridas

O EOP é um serviço online prestado pela Microsoft e utilizado por muitas empresas para proteger suas organizações locais contra vírus, spam, golpes de phishing e violações de políticas. No Office 365, o EOP é usado para proteger organizações do Exchange Online contra as mesmas ameaças. Quando você se inscreve no Office 365, a empresa do EOP é criada automaticamente que é associada à sua organização do Exchange Online.

A empresa do EOP contém várias configurações de transporte de mensagens que você pode ajustar para sua organização do Exchange Online. Você pode especificar quais domínios SMTP devem ser oriundos de endereços IP específicos, exigir certificados TLS e SSL (Secure Sockets Layer), ignorar políticas de conformidade e muito mais. O EOP é a porta de entrada para sua organização do Exchange Online. Todas as mensagens, independentemente da origem, devem passar pelo EOP antes que cheguem às caixas de correio de sua organização do Exchange Online. Adicionalmente, todas as mensagens enviadas por sua organização do Exchange Online devem passar pelo EOP antes de chegarem à Internet.

Quando você configura uma implantação híbrida com o assistente de Configuração Híbrida, todas as configurações de transporte são automaticamente ajustadas em sua organização local e na empresa do EOP incluída em sua organização do Exchange Online. O assistente de Configuração Híbrida define todos os conectores de entrada e de saída e outras configurações dessa empresa do EOP para proteger as mensagens enviadas entre a organização local e a organização do Exchange Online, encaminhando as mensagens para o destino certo. Se deseja definir configurações de transporte personalizadas para sua organização do Exchange Online, você também as ajustará nessa empresa do EOP.

## Comunicação confiável

Para ajudar a proteger os destinatários na organização local e na organização do Exchange Online e assegurar que as mensagens enviadas entre as organizações não sejam interceptadas e lidas, o transporte entre a organização local e o EOP é configurado de modo a usar TLS forçado. O transporte TLS usa certificados Secure Sockets Layer (SSL) fornecidos por uma Autoridade de Certificação (CA) terceirizada. Mensagens entre EOP e a organização do Exchange Online também usam TLS.

Ao usar o transporte TLS forçado, os servidores de envio e recebimento examinam o certificado configurado no outro servidor. O nome do assunto ou um dos nomes de assunto alternativos (SAN) configurado nos certificados deve corresponder ao FQDN que o administrador especificou explicitamente no outro servidor. Por exemplo, se o EOP for configurado para aceitar e proteger mensagens enviadas do FQDN mail.contoso.com, o servidor de Acesso para Cliente ou de Transporte de Borda local de envio deve ter um certificado SSL com mail.contoso.com no nome de entidade ou no SAN. Se essa exigência não for atendida, a conexão será recusada pelo EOP.


> [!TIP]
> O FQDN usado não precisa corresponder ao nome de domínio de email dos destinatários. O único requisito é que o FQDN no nome de assunto do certificado ou SAN corresponda ao FQDN que os servidores de recebimento ou envio estão configurados para aceitar.



Além de usar o TLS, as mensagens entre as organizações são tratadas como "internas�?. Essa abordagem permite que as mensagens ignorem configurações antispam e outros serviços.

Saiba mais sobre certificados SSL e segurança de domínio em [Requisitos de certificado para implantações híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) e [Noções básicas de Certificados TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

