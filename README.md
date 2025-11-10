# Keylogger — Projeto do Bootcamp de Cibersegurança (README)

> **Aviso importante (ética & legal)**  
> Este repositório contém código de um *keylogger* criado como exercício acadêmico durante um bootcamp de cibersegurança. **Uso não autorizado** de keyloggers para capturar credenciais ou dados pessoais de terceiros é ilegal e antiético.

---

## Sumário
- Descrição
- Escopo do projeto
- Arquitetura (visão geral)
- Como funciona (alto nível)
- Uso seguro (ambiente de teste recomendado)
- Medidas de proteção e mitigação (como se defender)
- Boas práticas e recomendações pós-comprometimento
- Licença & contatos

---

## Descrição
Este projeto é uma implementação educacional de um keylogger em Python (biblioteca `pynput`) que captura pressionamentos de tecla e demonstra um mecanismo simplificado de envio (por e-mail) para fins de análise. O objetivo do exercício foi entender vetores de captura de entrada e as implicações de segurança associadas — tanto do ponto de vista ofensivo quanto defensivo.

---

## Escopo do projeto
- **Propósito:** aprendizado e demonstração de conceitos de captura de teclado e análise de riscos.
---

## Arquitetura (visão geral)
- **Componente de captura:** listener de teclado (biblioteca de entrada).
- **Armazenamento temporário:** buffer em memória (variável `log`).
- **Canal de exfiltração (demonstrativo):** envio periódico por e-mail (SMTP) para fins didáticos.
- **Scheduler simples:** timer que periodicamente tenta enviar o conteúdo coletado.

> Observação: o envio por e-mail aqui é apenas ilustrativo — em um cenário real existem controles de rede que dificultam/exigem autenticação forte para envio SMTP externo. Não coloque credenciais reais em repositórios públicos.

---

## Como funciona (alto nível)
1. Um listener captura pressionamentos de tecla do usuário.
2. Cada tecla válida é concatenada em um buffer em memória.
3. Periodicamente (intervalo configurável), o buffer é enviado para um destino (no exemplo, por e-mail) e então esvaziado.
4. O listener roda até que o processo seja encerrado.

> Não inclua no README instruções passo-a-passo para implantação em ambientes produtivos, nem credenciais reais.

---

## Uso seguro (apenas em laboratório)
Se for necessário demonstrar o projeto em sala de aula ou avaliação:
- Execute **somente** em máquinas de teste isoladas (VMs sem acesso a redes sensíveis).
- Use contas e dados **falsos** — nunca dados reais de terceiros.
- Obtenha **autorização por escrito** de todos os participantes e do responsável pelo ambiente.
- Evite enviar logs para servidores públicos; armazene localmente ou em um repositório controlado e temporário.

---

## Medidas de proteção e mitigação — Como se proteger contra keyloggers

### 1. Educação e políticas
- **Conscientização**: treinar usuários para não executar softwares desconhecidos e desconfiar de anexos e links.
- **Políticas de privilégio mínimo**: evitar que usuários tenham permissões desnecessárias que permitam instalar ou executar software arbitrário.

### 2. Camadas técnicas
- **Antivírus / EDR**: soluções de detecção comportamental (Endpoint Detection & Response) identificam padrões de keylogging (listeners de teclado, gravação em massa, exfiltração).
- **Application allowlisting (whitelisting)**: permitir apenas aplicações confiáveis por política; impede execução de binários não autorizados.
- **Controle de execução de scripts**: restringir execução de scripts (PowerShell, Python, etc.) em máquinas de usuários finais.
- **Network e Data Loss Prevention (DLP)**: monitorar e bloquear tráfego SMTP/HTTP suspeito e prevenir exfiltração de dados sensíveis.
- **Firewalls de saída**: bloquear ou controlar conexões SMTP/HTTP/FTP não autorizadas para a Internet.
- **Atualizações e correções**: manter SO e software atualizados para reduzir vetores de ataque.

### 3. Autenticação e proteção de conta
- **Autenticação multifator (MFA)**: mesmo que credenciais sejam capturadas, MFA reduz risco de acesso não autorizado.
- **Gerenciadores de senhas**: preenchi­mento automático por gerenciadores reduz a digitação de senhas (e portanto a captura via keylogger tradicional).
- **Troca periódica de credenciais** e monitoramento de uso incomum (login de locais suspeitos).

### 4. Medidas específicas no endpoint
- **Monitoramento de processos**: investigar processos que mantêm hooks de teclado ou abrem arquivos de log.
- **Verificação de inicialização/autoexecução**: revisar autoruns e serviços para detectar persistência.

### 5. Ferramentas de detecção manual
- Monitorar conexões de rede inesperadas.
- Buscar processos desconhecidos que abrem sockets ou manipulam eventos de input.
- Examinar logs de sistemas de detecção/antivírus para alertas.

---

## Resposta a um possível comprometimento (passos recomendados)
1. **Isolar** a máquina da rede (desconectar para evitar exfiltração contínua).
2. **Capturar evidências** (logs, imagens de memória) se for necessário para investigação forense — antes de reiniciar ou alterar o sistema.
3. **Executar análise com EDR/antivírus** e, se identificado malware, seguir o procedimento da equipe de segurança (remediação ou reimage).
4. **Trocar credenciais** acessadas a partir daquela máquina (a partir de um dispositivo limpo).
5. **Auditar** contas, acessos e verificar atividades suspeitas (logs de autenticação, serviços em nuvem).
---

