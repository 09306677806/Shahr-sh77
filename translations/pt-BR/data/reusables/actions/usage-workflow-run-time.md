- **Tempo de execução do fluxo de trabalho** - {% ifversion fpt or ghec or ghes > 3.2 or ghae-issue-6469 %}Cada execução do fluxo de trabalho é limitada a 35 dias. Se a execução de um fluxo de trabalho atingir esse limite, a execução do fluxo de trabalho será cancelada. Este período inclui duração de execução e tempo gasto em espera e aprovação.{% else %}Cada execução de fluxo de trabalho é limitada a 72 horas. Se a execução de um fluxo de trabalho atingir esse limite, a execução do fluxo de trabalho será cancelada.{% endif %}