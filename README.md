# 🛡️ Keylogger Educacional — Bootcamp Santander Cibersegurança 2025

> **Aviso legal e ético**  
> Este projeto foi desenvolvido **exclusivamente para fins educacionais** no **Bootcamp Santander – Cibersegurança 2025**. O objetivo é demonstrar como keyloggers funcionam e, principalmente, como detectá-los e mitigá-los. **O uso não autorizado deste código para capturar dados de terceiros é ilegal e antiético.** Execute-o somente em ambientes controlados, com consentimento explícito e dados fictícios.

---

## 📘 Sobre o projeto

Exercício do bootcamp que implementa, em Python, um keylogger simples usando a biblioteca `pynput`. O propósito é entender vetores de captura de entrada, riscos associados e contramedidas defensivas — não criar ferramentas ofensivas prontas para uso malicioso.

O código de referência captura teclas, formata espaços e enters, agrega num buffer `log` e exemplifica uma forma de exfiltração (envio por e-mail) para fins didáticos.

---

## 🧩 Componentes e funcionamento (alto nível)

- **Captura de entrada:** `pynput.keyboard.Listener` monitora eventos de teclado e chama `on_press`.
- **Buffer em memória:** a variável `log` armazena os pressionamentos até serem processados.
- **Formatação básica:** espaços, enters e backspaces são representados para leitura posterior.
- **Mecanismo de exfiltração demonstrativo:** função `enviar_email()` envia periodicamente o conteúdo do buffer para um endereço (exemplo).
- **Scheduler simples:** `threading.Timer` reexecuta `enviar_email()` em intervalos (ex.: 60s).
- **Execução:** o listener roda em loop até interrompido.
---

## ⚠️ Uso seguro — demonstração em laboratório

1. **Ambiente isolado:** execute apenas em VMs/sandboxes sem conexão a redes sensíveis.  
2. **Dados falsos:** só use contas e arquivos fictícios.  
---

## 🛡️ Como se defender contra keyloggers (medidas práticas)

### 1. Camadas técnicas
- **EDR / Antivírus com detecção comportamental:** monitoram hooks de teclado, listeners e processos que manipulam input.  
- **Application allowlisting:** permite somente execução de binários e scripts aprovados.  
- **Bloqueio de execução de scripts em endpoints:** políticas para Python, PowerShell, macros etc.  
- **Proteção de egress (egress filtering & DLP):** detectar/blockar exfiltração por e-mail, HTTP(S), FTP.  
- **Firewalls de endpoint e rede:** impedir conexões não autorizadas de saída.

### 2. Autenticação e redução de impacto
- **MFA (autenticação multifator):** reduz risco mesmo se credenciais forem capturadas.  
- **Gerenciadores de senhas & preenchimento automático:** diminuem digitação manual de credenciais.  
- **Privilégios mínimos:** limitar conta de usuário para reduzir acesso a dados sensíveis.

### 3. Monitoramento e detecção
- **Anomalias de processo:** alertas para processos que ficam escutando eventos de input ou gravando muitos logs.  
- **Monitoramento de arquivos e integridade (FIM):** detectar criação de arquivos de log suspeitos.  
- **Inspeção de tráfego:** identificar padrões de upload contínuo ou e-mails gerados por processos não autorizados.

### 4. Controles organizacionais
- **Políticas de segurança:** treinar usuários para não executar anexos/softwares desconhecidos.  
- **Gestão de patches:** manter OS e software atualizados para reduzir vetores de instalação.  
- **Restrição de dispositivos USB:** bloquear dispositivos que possam carregar malware.
---

## 🔎 Indicadores de Comprometimento (IoCs) e sinais
- Processos Python ou desconhecidos iniciando listeners de input.  
- Criação de arquivos de texto com conteúdo sensível (logs de teclas).  
- Tráfego SMTP/HTTP/HTTPS para domínios ou IPs incomuns logo após atividade de usuário.  
- Aumento anômalo de uso de CPU/disk por processos não críticos.  
---

## 🚨 Procedimento de resposta (resumo rápido)
1. **Isolar**: desconectar endpoint da rede para interromper exfiltração.  
2. **Preservar evidências**: coletar imagens de memória, logs, listagens de processos e conexões.  
3. **Analisar alcance**: quais contas e sistemas foram afetados; houve exfiltração?  
4. **Remediar**: limpar/remover artefatos;, se necessário, reformatar ou reimager a máquina.  
5. **Restaurar credenciais**: alterar senhas e revisar acessos a partir de um sistema limpo.  
6. **Reportar e aprender**: comunicar conforme políticas (internas/legais) e ajustar controles.
---

## 🧑‍💻 Autor
**Cosme Ribeiro**  
Estudante de Desenvolvimento de Sistemas – SENAI Prof. Vicente Amato  
Bootcamp Santander – Cibersegurança 2025  


