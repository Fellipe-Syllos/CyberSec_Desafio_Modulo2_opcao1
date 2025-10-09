## 🛡️ Relatório Técnico: Defesa e Monitoramento com ModSecurity CRS em Ambiente Docker

Este é um **Relatório Técnico de Coleta e Análise de Evidências** que documenta a configuração, execução e resultados de um ambiente de laboratório focado na **detecção e mitigação de ataques web** utilizando um Web Application Firewall (**WAF**).

O projeto foi desenvolvido por **Fellipe Syllos** no contexto do módulo 2 de Defesa e Monitoramento da **Escola Vai na Web** em parceria com a **Kensei CyberSec**.

---

### 📝 Sumário Executivo

O principal objetivo deste projeto foi comprovar a eficácia de um WAF baseado em **ModSecurity** com o **OWASP Core Rule Set (CRS)** na proteção de uma aplicação web vulnerável.

* **Ataques Simulados:** Foram realizados **testes de exploração controlada** com ataques comuns, como **SQL Injection (SQLi)** e **Cross-Site Scripting (XSS)**.
* **Resultado:** O WAF **detectou e bloqueou** as ameaças em tempo real, gerando logs e retornando o **código HTTP 403 (Forbidden)**.
* **Conclusão:** O laboratório validou com sucesso a capacidade de defesa do WAF, reforçando a importância da **defesa em profundidade** e da **análise proativa de logs**.

---

### ⚙️ Arquitetura do Ambiente

O ambiente foi configurado em uma **rede Docker** para simular o fluxo de ataque e defesa.

| Contêiner | Imagem Base | Função |
| :--- | :--- | :--- |
| **`waf_modsec`** | `owasp/modsecurity-crs:nginx-alpine` | **Proxy reverso** com **ModSecurity** e **CRS** configurados (o WAF). |
| **`dvwa`** | `vulnerables/web-dvwa` | **Aplicação vulnerável** (Damn Vulnerable Web Application) usada para simulação de ataques web. |
| **`kali_lab35`** | `labs-kali_lab35` | **Ambiente de ataque controlado** para execução dos testes de penetração. |
| **`dozzle`** | `amir20/dozzle:latest` | **Visualização em tempo real** dos logs dos contêineres. |

O ataque partiu do contêiner **`Attacker`** (Kali Linux) via **HTTP** na porta `8080` em direção ao **WAF**.

---

### 🛡️ Resposta a Incidente (NIST IR)

A resposta aos incidentes simulados seguiu as etapas do ciclo **NIST IR**:

* **Detecção:** O ModSecurity gerou **alertas** identificando padrões de SQLi e XSS.
* **Contenção:** O WAF **bloqueou** os acessos maliciosos, retornando o código `403`.
* **Erradicação e Recuperação:** Nenhum impacto residual foi detectado, e o serviço permaneceu **íntegro e funcional**.

---

### 🔑 Recomendações

Com base nos resultados, são feitas as seguintes recomendações para fortalecer o monitoramento e a defesa:

* Implementar **monitoramento contínuo** dos logs.
* Integrar alertas do ModSecurity a um **SIEM corporativo**.
* Ativar o modo **'anomaly scoring'** com *thresholds* ajustados.
* Revisar periodicamente as **regras CRS**.
* Realizar **simulações regulares de ataque** para validação.

---

### 📅 Data e Autor

* **Autor:** Fellipe Syllos
* **Data:** 28/09/2025
* **Ambiente:** Laboratório Docker - ModSecurity CRS + DVWA + Kali Linux
