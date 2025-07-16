# Análise de Incidente de Segurança: Ataque de Negação de Serviço (SYN Flood)

*Estudo de caso prático desenvolvido durante o <a href="https://www.coursera.org/google-certificates/cybersecurity-certificate">Certificado Profissional de Cibersegurança do Google</a>, focado na análise de logs de rede para identificação e resposta a ameaças.*

---

### ⚠️ Nota Importante sobre Ética e Segurança dos Dados

Este projeto foi desenvolvido em um ambiente de laboratório 100% controlado e simulado, como parte do currículo do **Google Cybersecurity Professional Certificate**.

Todos os dados, incluindo logs e capturas de pacotes, são inteiramente fictícios. Os endereços IP utilizados, como `192.0.2.1`, `198.51.100.14` e `203.0.113.0`, são blocos de rede **TEST-NET**, reservados pela IETF (Internet Engineering Task Force) na RFC 5737 especificamente para uso em documentação e exemplos.

**Nenhuma informação de sistemas reais, redes de produção ou dados confidenciais de usuários está exposta neste repositório.** A apresentação destes dados segue as melhores práticas éticas da indústria de segurança cibernética.

---

### Contexto do Cenário

Como analista de segurança, fui designado para investigar a causa de uma interrupção de serviço no servidor web de uma empresa. Usuários relatavam erros de "connection timeout", impedindo o acesso a funcionalidades críticas do negócio.

O objetivo deste projeto foi utilizar técnicas de análise de pacotes para diagnosticar o problema, documentar os achados em um relatório técnico e propor um plano de mitigação.

### Análise e Relatório do Incidente

A investigação dos logs de rede revelou que o servidor estava sofrendo um **Ataque de Negação de Serviço (DoS) do tipo SYN Flood**. A análise inicial dos pacotes no Wireshark já indicava um padrão de comunicação suspeito, como pode ser visto na evidência abaixo.

![Evidência do Log de Tráfego TCP/HTTP](https://github.com/cleyandson/case-study-syn-flood/blob/8fcc6e1ba7d5cbd87151e172fbbf82d8715f9b8f/Documents/log-wireshark.png)

A análise aprofundada confirmou que um único endereço IP malicioso (`203.0.113.0`) estava inundando o servidor com solicitações de conexão TCP (`SYN`), mas sem completá-las.

Essa tática esgotou os recursos do servidor, que se tornou incapaz de responder às conexões de usuários legítimos. As principais evidências que confirmaram o ataque foram os erros de `Connection Timeout` e os pacotes `TCP [RST, ACK]` enviados a clientes válidos.

### Plano de Mitigação e Recomendações

Com base na análise, um plano de ação foi estruturado para conter a ameaça e aumentar a resiliência da infraestrutura:

**Contenção Imediata:** Bloqueio do IP de origem (`203.0.113.0`) na firewall da rede para cessar o ataque imediatamente.
**Mitigação 1:** Ativação de **SYN Cookies** no sistema operacional do servidor para validar conexões antes de alocar recursos.
**Mitigação 2:** Implementação de políticas de **Rate Limiting** para limitar a taxa de novas conexões por endereço IP.

### Relatório Completo em PDF
* [**Relatório de incidente de cibersegurança**](https://github.com/cleyandson/case-study-syn-flood/blob/8fcc6e1ba7d5cbd87151e172fbbf82d8715f9b8f/Documents/PT-BR%20Cybersecurity%20incident%20report.pdf)

### Conclusão

Em conclusão, a análise da causa raiz determinou que o incidente foi um ataque de negação de serviço (SYN Flood). A situação foi resolvida através de um plano de contenção imediato e da recomendação de mitigações estratégicas.

---
*A condução deste estudo de caso reforça a importância de traduzir evidências técnicas em ações de negócio, demonstrando competências práticas em análise de rede, resposta a incidentes e planejamento de segurança para proteger ativos críticos.*
