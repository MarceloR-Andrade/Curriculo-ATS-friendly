# ATS Match & Boost - Seu currículo, lido como um robô de recrutamento lê.
Uma aplicação web que compara um currículo com uma vaga e devolve uma versão ATS friendly desse currículo.

Qual problema a sua aplicação resolve:

Esta aplicação resolve um dos maiores gargalos dos processos seletivos modernos: a barreira invisível dos sistemas ATS (Application Tracking Systems) e a dificuldade dos candidatos de adaptarem seus currículos de forma estratégica e honesta.

O problema detalhado e como a aplicação o soluciona:

1. O Problema (O Calvário do Candidato)
A barreira dos robôs (ATS): Hoje, a grande maioria das empresas (especialmente em tecnologia e grandes corporações) utiliza softwares de inteligência artificial e triagem automática para ler currículos antes de qualquer ser humano olhar. Se o currículo não contém as palavras-chave exatas exigidas pela vaga, ele é descartado automaticamente em segundos.

Falta de visibilidade: O candidato comum envia dezenas ou centenas de currículos idênticos e nunca entende por que não é chamado para entrevistas. Ele não sabe o que faltou ou qual era o grau de compatibilidade (match) com a vaga.

Esforço manual exaustivo: Ajustar manualmente o currículo para cada vaga específica — reescrevendo tópicos, buscando sinônimos e encaixando palavras-chave sem soar artificial — consome horas de trabalho mental.

Tentação da mentira vs. Insegurança: Muitos candidatos ficam tentados a inventar experiências ou habilidades que não possuem só para "passar pelo robô", o que gera um risco enorme em entrevistas técnicas ou de RH. Por outro lado, quem é honesto acaba ficando de fora por não saber destacar o que já tem da forma correta.

2. A Solução (Como a Aplicação Atua)
A aplicação atua como um consultor de carreira automatizado e ético, resolvendo o processo em etapas rápidas:

Diagnóstico Instantâneo: Ao colar a vaga e o currículo, a pessoa descobre imediatamente o seu percentual de match real e vê claramente o que o sistema da empresa está procurando (quais palavras-chave ela achou e quais faltaram).

Otimização Inteligente sem Mentiras: A inteligência artificial reescreve o currículo destacando as competências reais do candidato para alinhá-lo ao vocabulário da vaga, obedecendo estritamente à regra de ouro: melhorar a apresentação e o impacto, sem nunca inventar experiências inexistentes.

Praticidade para Envio (.docx): Permite exportar o resultado limpo e formatado diretamente para um arquivo do Word (.docx), facilitando ajustes finais e o envio imediato.

Especialização de Nicho: Foca em áreas de alta concorrência e exigência técnica (como Tecnologia e Primeiro Emprego), onde o uso de termos técnicos corretos define se o currículo é aprovado ou descartado.

Visibilidade e Progresso (Dashboard): Permite que o usuário acompanhe seu histórico de análises e veja a evolução do match de suas candidaturas ao longo do tempo, aprendendo a calibrar seus envios.


O mega prompt que você usou, e o que mudou nele até a versão final:

```
Crie uma aplicação web completa e responsiva chamada "Gerador de Currículo ATS-Friendly" (ATS Match & Boost), especializada em otimizar currículos para carreiras em tecnologia e candidatos de primeiro emprego.

### Diretriz Central Ética
A ferramenta deve destacar competências e reescrever pontos fracos com verbos de ação e impacto, preservando rigorosamente a integridade das informações reais do usuário — nunca inventar experiências falsas.

### Design System & Layout
- Cores: Fundo claro e limpo (slate-50 / white), texto e destaques em Slate escuro (slate-900), métricas de sucesso em Verde Esmeralda (emerald-600) e alertas em Âmbar suave (amber-100 / amber-800).
- Componentes: Interface moderna com Tailwind CSS, ícones Lucide React e componentes shadcn/ui.
- Responsividade total para desktop e mobile.

### Funcionalidades da Aplicação:
1. **Página Inicial / Analisador (`/`)**:
   - Cabeçalho com o nome do app, badge do nicho e link para o Histórico.
   - Seletor de nicho: "Tecnologia (Dev/Dados)" ou "Primeiro Emprego / Estágio".
   - Seção Split-View em duas colunas com contadores de caracteres:
     - Coluna Esquerda: Textarea para colar a "Descrição da Vaga".
     - Coluna Direita: Textarea para colar o "Currículo Atual".
   - Botão de ação destacado: "Analisar e Otimizar para ATS".

2. **Painel de Resultados e Diagnóstico**:
   - **Indicador de Compatibilidade (Match Score)**: Gráfico de gauge circular ou barra de progresso destacada de 0 a 100%.
   - **Palavras-chave Encontradas**: Badges em verde com os termos técnicos identificados em ambos os textos.
   - **Palavras-chave Ausentes**: Badges em âmbar mostrando termos críticos da vaga que não constam no currículo, acompanhados de dicas práticas de como incluí-los honestamente.
   - **Currículo Otimizado**: Área de visualização com o currículo reformatado em seções claras (Resumo Profissional, Habilidades Técnicas, Experiência/Projetos e Formação).
   - **Ações Rápidas**:
     - Botão "Copiar Texto Formatado" com feedback de toast.
     - Botão "Exportar Currículo" (gerando arquivo de texto limpo .txt e opção de impressão formatada em layout ATS A4 sem tabelas ou colunas quebradas).

3. **Dashboard e Histórico (`/dashboard`)**:
   - Cards com métricas rápidas: Total de análises realizadas e Média de pontuação.
   - Tabela de histórico com as últimas análises realizadas (armazenadas em LocalStorage nesta versão inicial), permitindo reabrir ou excluir análises antigas.

4. **Experiência do Usuário**:
   - Estados de carregamento animados durante a análise simulada.
   - Toasts de notificação para ações do usuário e estados vazios amigáveis com exemplos prontos de vaga e currículo para testar em um clique.
```
Como a análise funciona, da vaga colada até o currículo ajustado:

O funcionamento da análise é um fluxo inteligente de processamento de texto e engenharia de prompt que transforma dados brutos em uma estratégia de recrutamento precisa.

O passo a passo de como a aplicação processa a vaga colada até entregar o currículo ajustado acontece da seguinte forma:

1. Ingestão e Normalização dos Dados
Entrada: O usuário cola a Descrição da Vaga (que contém os requisitos, tecnologias, responsabilidades e diferenciais) e o Currículo Atual.

Segmentação: O sistema lê os dois blocos de texto e separa conceitualmente a vaga em blocos de exigências (ex: linguagens, metodologias, tempo de experiência, soft skills) e o currículo em blocos de histórico profissional (experiências passadas, formação, competências).

2. Extração de Palavras-Chave e Cálculo de Match (Diagnóstico)
Varredura de Requisitos: A IA analisa a descrição da vaga para extrair as palavras-chave críticas (ex: React, TypeScript, Metodologias Ágeis, AWS).

Cruzamento de Dados: Ela verifica quais dessas palavras-chave estão presentes no currículo original do candidato e quais estão ausentes.

Pontuação (%): Com base na proporção de termos encontrados versus exigidos, o motor calcula o índice de compatibilidade inicial (Match Score, ex: 68%). O painel separa visualmente o que foi encontrado (em verde) do que falta (em amarelo/alerta).

3. Otimização Baseada em Regras Éticas (O Núcleo da IA)
Esta é a etapa mais sensível e inteligente da aplicação, dividida em dois pilares:

Adaptação de Linguagem (ATS-Friendly): O sistema reescreve os tópicos de experiência do candidato para usar o mesmo vocabulário e sinônimos encontrados na descrição da vaga. Se a vaga pede "gestão de projetos orientados a dados" e o currículo diz "criação de relatórios", a IA ajusta o termo para refletir com mais profissionalismo a mesma realidade.

O Guardrail Ético (Zero Invenção): A instrução central impede a IA de alucinar ou inventar. Ela nunca adiciona um cargo que o usuário não exerceu, uma ferramenta que ele nunca tocou ou uma certificação que ele não tem. Ela trabalha exclusivamente com o material fornecido pelo candidato, mudando apenas a forma de apresentação, a clareza, o impacto e a ordem dos argumentos.

4. Especialização por Nicho
Conforme o nicho escolhido (Tecnologia ou Primeiro Emprego):

No nicho de Tech, a IA prioriza destacar stack tecnológica, arquitetura de software, métricas de performance e repositórios/projetos.

No nicho de Primeiro Emprego, onde o candidato tem pouca ou nenhuma experiência formal, a IA muda o foco para destacar projetos acadêmicos, trabalhos voluntários, cursos livres, soft skills, atividades extracurriculares e disposição para aprendizado.

5. Empacotamento e Persistência
Geração do Resultado: A aplicação exibe o currículo revisado em uma visualização limpa e pronta para uso.

Salvamento no Banco (Supabase): Toda a análise (vaga, pontuação, palavras-chave e versão gerada) é salva de forma segura na conta do usuário, alimentando o Dashboard para que ele possa acompanhar a evolução do seu match ao longo das candidaturas.

Que ajustes você pediu depois da primeira geração, e por quê: Tentei editar alguns títulos e pedir a exportação em word, formatado para envio ao recrutador, porém não tinha mais créditos!

O endereço da aplicação publicada:

https://honest-match-resume-guide.lovable.app/?id=85df08d4-fe53-465d-bd5d-c0f45dce43a4

Prints de tela do sistema funcionando:

<img width="1358" height="799" alt="image" src="https://github.com/user-attachments/assets/0186d754-75fb-42a8-99f9-5269293b972e" />

<img width="1443" height="826" alt="image" src="https://github.com/user-attachments/assets/387a184f-2f7b-41d7-9c6b-efc8a7b8afc5" />

<img width="1369" height="894" alt="image" src="https://github.com/user-attachments/assets/775972ab-ddf7-4086-893c-92acb908cac7" />



