# Análise de Vulnerabilidade na Cadeia de Suprimentos do Arch Linux AUR

## 📌 Visão Geral
Este repositório contém uma apresentação de pesquisa técnica que analisa um ataque à cadeia de suprimentos no **Arch Linux User Repository (AUR)**. O projeto investiga como invasores exploraram o repositório comunitário sequestrando pacotes órfãos para distribuir malware por meio de falsas atualizações e injeção de código.

## 🚨 Vetor de Ataque e Análise de Código
O ataque se aproveita da compilação cega de scripts `PKGBUILD` usando o comando `makepkg`. 
Inspecionando o `PKGBUILD` malicioso:
- **Vetor de Ataque:** A variável `source` é alterada para baixar cargas maliciosas.
- **Execução Maliciosa:** A função `package()` é sequestrada para executar comandos bash não autorizados durante a instalação.

## 💥 Consequências
Se executados, os pacotes comprometidos causam impactos severos ao sistema:
- Roubo de credenciais e chaves de segurança.
- Cryptojacking (sequestro de hardware para minerar criptomoedas).
- Acesso Root total para o invasor.
- Lockdown do sistema para conter os danos.

## 🛡️ Soluções Propostas e Mitigação
A pesquisa delineia estratégias práticas de resolução de problemas divididas em duas frentes:

**Soluções do Lado do Usuário:**
- **Regra de Ouro:** Leitura obrigatória do arquivo `PKGBUILD` antes de qualquer instalação.
- Verificação da procedência dos links de download e análise de comandos suspeitos na função `package`.
- Fim da "compilação cega": Nunca executar `makepkg` no automático sem revisão prévia.

**Soluções do Lado do Sistema (Política do Arch):**
- Política de congelamento permanente para pacotes abandonados.
- Regra de inatividade (congela após 18-24 meses) com cronômetro de depreciação.
- Obrigatoriedade de Fork (novo nome) para dar continuidade.
