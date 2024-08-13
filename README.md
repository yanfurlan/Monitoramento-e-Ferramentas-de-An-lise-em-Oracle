Monitoramento e Ferramentas de Análise em Oracle

V$SQL: É uma visão dinâmica (view) que fornece informações sobre as SQL queries que estão sendo executadas ou que já foram executadas no banco de dados. Ela armazena detalhes como o texto SQL, número de execuções, tempo gasto, e uso de recursos. É muito útil para identificar queries que estão consumindo muitos recursos.

AWR (Automatic Workload Repository): É um recurso que coleta, processa e mantém estatísticas de desempenho do banco de dados. AWR armazena snapshots periódicos das métricas de desempenho do banco de dados, que podem ser usados para gerar relatórios detalhados. Esses relatórios ajudam a identificar problemas de performance, gargalos e tendências no banco de dados.

ADDM (Automatic Database Diagnostic Monitor): É uma ferramenta que analisa automaticamente as informações coletadas pelo AWR para identificar e diagnosticar problemas de desempenho no banco de dados. Ele sugere ações corretivas e classifica os problemas por impacto no desempenho, ajudando a priorizar o que deve ser resolvido primeiro.

    Prática: Projeto de Monitoramento de Desempenho

Objetivo: Monitorar queries em execução e analisar o desempenho do banco de dados usando V$SQL, AWR e ADDM.

    Passos do Projeto

        1. Utilizar V$SQL para Monitorar Queries em Execução

            Conecte-se ao banco de dados Oracle.
            Execute a query abaixo para monitorar queries que estão em execução:

            SELECT sql_id, child_number, executions, elapsed_time, cpu_time, sql_text
            FROM V$SQL
            WHERE executions > 0
            ORDER BY elapsed_time DESC;

            Anote os sql_id e sql_text das queries que estão consumindo mais tempo.

        2. Gerar um Relatório AWR

            Gere um relatório AWR para analisar o desempenho do banco de dados:

            EXEC DBMS_WORKLOAD_REPOSITORY.create_snapshot;


            Após um período de atividade no banco de dados, gere um relatório AWR:

            /rdbms/admin/awrrpt.sql

            Escolha o intervalo de snapshots que deseja analisar e salve o relatório.

        3. Analisar o Relatório AWR

            Abra o relatório gerado e verifique as seguintes seções:

            Top SQL by Elapsed Time: Identifique as queries que estão consumindo mais tempo.
            Instance Efficiency: Analise a eficiência geral do banco de dados.
            Wait Events: Veja quais eventos de espera estão impactando o desempenho.

        4. Utilizar ADDM para Diagnóstico

            Execute o ADDM para obter sugestões de melhorias:
            
            /rdbms/admin/addmrpt.sql

            Revise o relatório gerado para entender os principais problemas de desempenho identificados e as recomendações fornecidas.

Conclusão

Este projeto fornece uma base sólida para monitorar e analisar o desempenho de um banco de dados Oracle usando ferramentas essenciais como V$SQL, AWR e ADDM. Esses recursos são fundamentais para garantir que o banco de dados esteja funcionando de maneira eficiente e para identificar possíveis áreas de otimização.
