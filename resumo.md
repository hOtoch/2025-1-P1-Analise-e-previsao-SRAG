# Dataset

O dataset escolhido é o dataset de Síndrome Gripal Aguda Grave oficial do SUS. Esse dataset se integra com o SIVEP-Gripe (https://www.gov.br/saude/pt-br/assuntos/noticias/2020/abril/covid-19-registro-de-casos-suspeitos-no-e-sus-ve), um sistema criado pelo Ministério da Saúde para cadastrar todos os casos de gripe com complicações (dispneia, saturação < 95 %, desconforto respiratório, etc.) mesmo que os pacientes não tenham sido hospitalizados.

Tanto hospitais públicos quanto privados devem preencher o formulário no SIVEP-Gripe.

# Informações Gerais

O item de informações gerais do dataset fala da evolução temporal das notificações e da distribuição desses dados pela população.

## Evolução temporal

Está mostrado no gráfico que com o início da implementação do sistema ele foi rapidamente adotado, atingindo o pico durante a pandemia em 2021.

TODO: Mostrar a evolução de cada uma das doenças separado (identificado pela coluna CLASSI_FIN).

## Comparação homem vs mulher

Não sei explicar porque a distribuição ficou diferente.

## Comparação das notificações por idade com IBGE

A distribuição das notificações por idade é bem diferente da distribuição etária da população segundo o IBGE (dados de 2022). Provavelmente porque neste dataset estão apenas os casos graves de gripe, que acontece com mais frequência em pessoas mais velhas e crianças.

## Comparação das notificações por raça com IBGE

Difícil afirmar a causa da diferença entre o número de notificações e a distribuição da população pela raça. Meu palpite é subnotificação de população parda e negra por uso menos frequente do serviço de saúde por essas populações.

# Predição da Classificação Final baseado nos sintomas

Nessa seção selecionei apenas as colunas de sintomas do dataset original e a coluna de classificação final com o objetivo de tentar prever a classificação ou fazer um clusterização.

## Verificação estatística da influência dos sintomas na classificação final

Para verificar se os sintomas tinham informação útil para fazer a classificação fiz um teste de hipótese com o teste do Qui-Quadrado. O teste mostrou que todos os sintomas têm influência sobre a classificação final, com p-valor quase nulo (<< 0.05).

Imaginei que dessa forma seria possível fazer uma classificação/clusterização dos casos.

## Tentativa de clusterização com PCA

Fiz a clusterização com o PCA, mas não deu certo. A covid que tem mais casos tomou todo o gráfico e as outras classificações ficaram espalhadas sem padrão visível. Este resultado foi um indício de que as classificações no espaço de sintomas não são linearmente separáveis.


## Tentativas de classificação

Separei o dataset em treino e teste e tentei fazer uma classificação com os seguintes algoritmos:
- KNN
- Decision Tree
- SVM
- Naive Bayes

Como eram muitos dados, usei apenas 1% a 10% do dataset para treinar e testar os modelos.

Em todos usei k-fold cross validation com `k=10`, calculei a acurácia e o desvio padrão e gerei a matriz de confusão.

Todos tiveram resultados ruins, próximos de 50% de acurácia.

# Classificação de gravidade

TODO: Seguir o mesmo método do item anterior, mas tentando prever a evolução da doença (óbito ou alta, coluna EVOLUCAO)
