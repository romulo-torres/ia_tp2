# IA - Trabalho 2 - Classificação de lixo para reciclagem

Este repositório contém o trabalho 2 para a disciplina de Inteligência Artificial, focado na análise e modificação de um notebook jupyter contendo um classificador de imagens multiclasse para resíduos recicláveis.

Esse trabalho feito pelos alunos:

- Arthur Vinício Capucho Silva - 22351675
- Giovana Lins Cavalcanti - 22352925
- Pedro Barreto de Souza - 22351231
- Nycksandro Lima dos Santos - 22351228
- Rômulo Fernandes Torres - 22351220
- Ronald Vieira Cardoso da Silva - 22352934

## 1. Descrição do Projeto

O objetivo do trabalho é analisar o processo e resultados de um modelo de Rede Neural Convolucional (CNN) capaz de classificar imagens de lixo em seis categorias distintas:

 * Papel (paper)
 * Papelão (cardboard)
 * Plástico (plastic)
 * Vidro (glass)
 * Metal (metal)
 * Lixo Orgânico/Rejeito (trash)

O projeto utiliza o dataset [TrashNet](https://github.com/garythung/trashnet), que consiste em 2.527 imagens divididas nessas seis classes e o notebook [Trash/Garbage Type Detection using CNN](https://www.kaggle.com/code/farnazmirfeizi/trash-garbage-type-detection-using-cnn) como um framework base para treinamento de modelos.

## 2. Metodologia

O notebook detalha os seguintes passos:

Carregamento: 

  - As imagens são carregadas e normalizadas. 

Tratamento de dados: 

- Devido ao dataset ser pequeno com apenas 2.527 imagens e desbalanceado, por exemplo a classe trash tem apenas 137 imagens, técnicas de data augmentation como rotação, zoom e inversão foram aplicadas ao conjunto de treino para evitar overfitting e melhorar a generalização.
- Foi utilizado o ImageDataGenerator do Keras para dividir o dataset em conjuntos de treino e validação.
- Definimos o tamanho do ``batch_size`` para 32 e as dimensões dos dados de entrada para 224x224.

Construção do Modelo: 

- Desabilitamos as otimizações do tensorflow para permitir que usassemos placas de vídeo para treinar o modelo.
- Foi implementada uma arquitetura de CNN Sequencial, consistindo em blocos de Conv2D e MaxPooling2D, seguidos por um classificador com camadas Flatten, Dense e Dropout para regularização. A camada de saída utiliza softmax para a classificação multiclasse.

Treinamento: 

- O modelo foi compilado com o otimizador Adam. 
- Para garantir um treinamento robusto e eficiente, utilizamos class_weight para forçar o modelo a aprender com as classes desbalanceadas (como 'trash'). 
- Além disso, o treino foi monitorado por Callbacks: 
  - ModelCheckpoint salvou a melhor versão do modelo (baseado na val_accuracy).
  - EarlyStopping preveniu o overfitting (sobreajuste) interrompendo o treino quando o val_loss parava de melhorar.
  - ReduceLROnPlateau ajustou a taxa de aprendizado automaticamente para refinar o modelo quando ele chegava em um platô de performance.

## 3. Resultados

Após o treinamento e ajuste do modelo, a acurácia final obtida no conjunto de validação foi 75.06% com o val_loss de 0.7401.

Uma análise detalhada dos resultados, incluindo a matriz de confusão e o impacto do data augmentation, pode ser encontrada diretamente no notebook.

## 4. Como Executar

 * Clone este repositório.
 * Tenha um ambiente com TensorFlow e Scikit-learn instalados.
 * Baixe o conjunto de dados e configure o seu diretório.
 * Execute o notebook classificacao_lixo.ipynb.