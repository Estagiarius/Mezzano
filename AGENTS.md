```markdown
# Diretrizes para Agentes de IA - Projeto Mezzano

Bem-vindo, colega agente de IA! Este arquivo fornece diretrizes para ajudar você a entender e contribuir com o projeto Mezzano.

## Visão Geral do Projeto

Mezzano é um sistema operacional escrito inteiramente em Common Lisp, desde o kernel até as aplicações de usuário. Ele possui seu próprio compilador, runtime, interface gráfica, pilha de rede e drivers de dispositivo.

**Principais Objetivos do Mezzano:**
*   Explorar as capacidades do Common Lisp para desenvolvimento de sistemas.
*   Fornecer um ambiente Lisp interativo e completo.
*   Ser um sistema operacional "hackeável" e compreensível.

## Informações Técnicas Essenciais

*   **Linguagem Principal:** Common Lisp.
    *   Espera-se que o código siga as boas práticas e o estilo idiomático do Common Lisp.
    *   Preste atenção ao gerenciamento de pacotes (sistemas ASDF, `defpackage`, importação/exportação de símbolos).
*   **Arquiteturas Suportadas:**
    *   x86-64
    *   ARM64
    *   Código específico de arquitetura geralmente reside em subdiretórios nomeados apropriadamente (ex: `compiler/backend/x86-64/`, `supervisor/arm64/`).
*   **Sistema de Build:**
    *   O sistema é construído usando um processo de "cold generation" e "cross-compilation".
    *   Arquivos `.asd` são usados para definir sistemas carregáveis com ASDF.
    *   Ferramentas relevantes estão em `tools/` e `compiler/`.
*   **Estrutura de Diretórios Chave:**
    *   `applications/`: Aplicações de exemplo e utilitários.
    *   `compiler/`: O compilador Mezzano Lisp.
    *   `drivers/`: Drivers de dispositivo.
    *   `file/`: Sistemas de arquivos e operações relacionadas.
    *   `gui/`: Interface gráfica do usuário.
    *   `net/`: Pilha de rede.
    *   `runtime/`: Suporte de runtime para o Lisp compilado.
    *   `supervisor/`: O kernel e funcionalidades de baixo nível.
    *   `system/`: Implementação do core do Common Lisp e funcionalidades do sistema.
    *   `tools/`: Ferramentas de build e desenvolvimento.

## Diretrizes de Codificação

1.  **Estilo de Código:**
    *   Siga o estilo de código predominante nos arquivos existentes.
    *   Use nomes de variáveis e funções descritivos.
    *   Comente código complexo ou não óbvio.
    *   Mantenha linhas com um comprimento razoável (geralmente até 80-100 colunas, mas seja flexível onde fizer sentido).
    *   Use espaços para indentação, não tabs. A indentação padrão é de 2 espaços.

2.  **Comentários:**
    *   Comentários devem ser escritos em inglês para consistência com a base de código existente.
    *   Use `;;;` para comentários de nível superior (documentação de funções, seções).
    *   Use `;;` para comentários de implementação dentro de funções.
    *   Use `;` para comentários ao final de uma linha de código.

3.  **Commits:**
    *   Siga as convenções de commit do Git (assunto conciso, corpo detalhado se necessário).
    *   Mantenha os commits pequenos e focados em uma única mudança lógica.

4.  **Testes:**
    *   Atualmente, o projeto não possui um framework de testes formalizado e extensivo visível na estrutura de arquivos principal.
    *   Ao adicionar novas funcionalidades ou corrigir bugs, considere como testar suas mudanças. Isso pode envolver:
        *   Testes interativos no REPL do Mezzano.
        *   Criação de pequenas aplicações de teste em `applications/`.
        *   Adição de código de teste condicional (ex: sob uma feature flag ou variável dinâmica).
    *   Se você identificar áreas onde testes automatizados seriam benéficos, discuta a possibilidade de introduzi-los.

5.  **Trabalhando com Código Específico de Arquitetura:**
    *   Ao modificar ou adicionar código que interage diretamente com hardware ou que é específico de uma arquitetura (x86-64, ARM64), certifique-se de que suas mudanças são corretas para a(s) arquitetura(s) alvo.
    *   Coloque o código específico da arquitetura nos diretórios apropriados.
    *   Procure por abstrações existentes que possam ser usadas para minimizar a duplicação de código entre arquiteturas.

6.  **Gerenciamento de Pacotes (Common Lisp):**
    *   Preste atenção às definições de pacotes (`defpackage`) e ao uso de `in-package`.
    *   Exporte apenas os símbolos que são destinados ao uso público por outros pacotes.
    *   Use prefixos de pacote ou importações locais para evitar conflitos de símbolos.

## Como Executar/Testar e Fluxo de Trabalho de Desenvolvimento

*   **Construção e Execução:**
    *   A execução do Mezzano geralmente envolve a construção de uma imagem de disco e a execução em um emulador (como QEMU, VirtualBox) ou hardware real.
    *   O `README.md` menciona que imagens pré-construídas estão disponíveis e recomenda 2GB de RAM, um NIC virtio-net e um controlador de áudio Intel HDA para VirtualBox/QEMU.
    *   Para construir a partir do código-fonte, consulte o repositório MBuild: `https://github.com/froggey/MBuild`.
    *   O sistema suporta snapshotting: `(mezzano.supervisor:snapshot)` no REPL salva o estado atual da máquina, que é restaurado na próxima inicialização. Isso pode ser útil para desenvolvimento iterativo.

*   **Interação e Teste:**
    *   Muitas vezes, o teste de novas funcionalidades pode ser feito interativamente dentro do REPL do Mezzano uma vez que o sistema está em execução.
    *   `M-F10` abre um REPL.
    *   O `doc/quickstart.md` lista vários atalhos globais e comandos de edição de linha úteis para interagir com o sistema.
    *   O Swank (servidor SLIME) está disponível na porta 4005, permitindo uma conexão de um ambiente de desenvolvimento Lisp externo para depuração e desenvolvimento interativo. Configure o encaminhamento de porta no seu VM.

*   **Desenvolvimento Típico (Inferido):**
    1.  **Configurar o Ambiente:** Tenha um ambiente Common Lisp funcional e as ferramentas de build do Mezzano (MBuild).
    2.  **Obter o Código:** Clone o repositório Mezzano.
    3.  **Construir a Imagem:** Use o MBuild para compilar o sistema e criar uma imagem de disco.
    4.  **Executar no Emulador:** Inicie a imagem em QEMU ou VirtualBox.
    5.  **Modificar Código:** Edite os arquivos `.lisp` relevantes no seu ambiente de desenvolvimento.
    6.  **Recarregar/Recompilar (Dentro do Mezzano ou Reconstruindo):**
        *   Para algumas mudanças, pode ser possível recompilar e carregar arquivos Lisp diretamente no REPL do Mezzano ou via Swank.
        *   Para mudanças mais significativas (ex: no supervisor, compilador), uma reconstrução completa da imagem pode ser necessária.
    7.  **Testar:** Use o REPL, crie aplicações de teste, ou use Swank para interagir e verificar suas mudanças.
    8.  **Snapshot (Opcional):** Use `(mezzano.supervisor:snapshot)` para salvar um estado funcional para rápida iteração.
    9.  **Iterar:** Repita os passos de modificação, recarga/rebuild e teste.

## "Coisas a Evitar" / Anti-padrões (Sugestões Gerais)

*   **Ignorar o Gerenciamento de Memória:** Embora o Lisp tenha GC, em um SO, especialmente no kernel (supervisor) e drivers, é crucial estar ciente das alocações e do potencial impacto no desempenho. Evite alocações desnecessárias em caminhos críticos.
*   **Bloquear o Sistema Indevidamente:** Tenha cuidado com operações de longa duração ou bloqueantes em threads críticas que possam impedir a resposta do sistema.
*   **Introduzir Incompatibilidades de Arquitetura:** Ao trabalhar em código de baixo nível, certifique-se de que as mudanças são compatíveis com ambas as arquiteturas (x86-64, ARM64) ou use condicionais de arquitetura apropriados.
*   **Quebrar a Interatividade:** Mezzano valoriza a interatividade. Mudanças que dificultem o uso do REPL ou a depuração devem ser cuidadosamente consideradas.
*   **Negligenciar a Documentação Existente:** O sistema já possui documentação (`doc/`, `README.md`). Consulte-a antes de fazer suposições.
*   **Modificar APIs Públicas Sem Consideração:** Se estiver alterando funções ou macros usadas por outros módulos, avalie o impacto.

## Recursos Adicionais

*   **README.md:** Contém informações gerais sobre o projeto, links para imagens pré-construídas e o sistema de build MBuild.
*   **doc/:** Contém documentação mais detalhada sobre vários aspectos do sistema.
    *   `doc/quickstart.md`: Guia de início rápido, essencial para entender a interação básica, atalhos e o editor.
    *   `doc/manual.md`: Manual do sistema.
*   **Repositório MBuild:** `https://github.com/froggey/MBuild` para instruções de build.
*   **Comunidade IRC:** `#mezzano` na Libera Chat para ajuda e discussões.

## Considerações Finais

*   Este é um projeto complexo e único. Não hesite em ler o código existente extensivamente para entender como as coisas funcionam. A capacidade de explorar o sistema em execução via REPL e Swank é uma grande vantagem.
*   Se algo não estiver claro, ou se você tiver sugestões para melhorar estas diretrizes, por favor, mencione.

Obrigado por ajudar a melhorar o Mezzano!
```
