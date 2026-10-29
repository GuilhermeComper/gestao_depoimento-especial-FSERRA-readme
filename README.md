CONTEXTO TÉCNICO E ARQUITETURA DO PROJETO (Versão 6.2):
1. Planilha Base:
   - Aba principal: "Agendamentos" (Colunas: Data do Pedido, Nº PROCESSO, DATA DO D.E, HORÁRIO, STATUS, MOTIVO/OBS, Vara, Responsável, Vítima, Link de Acesso / ID, E-mails dos Convidados, Adicionado à Agenda?).
   - Aba de cache local (oculta): "DB_Agenda" (Armazena eventos locais das agendas Google para busca ultrarrápida sem estourar cotas da API).

2. Funcionalidades Ativas no Código:
   - Fluxo de Inicialização (onOpen): Dispara primeiro a verificação de pendências instantânea e roda a sincronização do banco local (DB_Agenda) em segundo plano com tela de splash/loading no painel lateral.
   - Pop-up de Pendências na Abertura: Puxa todos os processos com status "Pendente" (com ou sem data marcada) e audiências dos próximos 5 dias incompletas (sem link ou fora da agenda), exibindo em destaque o campo "MOTIVO/OBS". Se não houver nada, exibe modal verde confirmando que está tudo em dia.
   - Localizador Lateral (Sidebar):
     * Formatação limpa de data/horário (ex: "26/10/2026 às 13:00"), sem resíduos de fusos GMT ou anos de 1899.
     * Busca por processo (com/sem zeros e pontuação), vítima, data, sala passiva ou responsável.
     * Botão "🎯 Ir para Linha X" para focar e selecionar a linha correspondente direto na planilha.
     * Janela central de detalhes expandida (HTML modal).
     * Card de diagnóstico orientativo caso a busca retorne vazia (sugestão de atualizar banco, checar e-mails ou novos termos).
   - Automações em Segundo Plano:
     * Leitura e categorização automática de e-mails do Gmail com etiquetas ("Processado_DE").
     * Sincronização de eventos futuros diretamente para o Google Calendar ("DEPOIMENTO ESPEC - DE").
     * Relatório diário/boletim das 12h enviado por e-mail com resumo visual dos próximos 15 dias.
