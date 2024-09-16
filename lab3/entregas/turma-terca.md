## Modelo do aeropêndulo em malha aberta

Do laboratório realizado anteriormente, chegou-se ao seguinte modelo do aeropêndulo em malha aberta:

$$ G(s) = \frac{\theta(s)}{U(s)} = \frac{\gamma}{s^2 + \beta s + \alpha} \frac{1}{a_ms + 1} $$

Como o modelo utilizado não se encaixa em todas as faixas de potência aplicadas no aeropêndulo, encontrou-se as seguintes constantes para cada potência do aeropêndulo utilizado, a potência é representado em percentual:

| Potência(%) | $\alpha$ | $\beta$ | $\gamma$ |         $a_m$        |
|:-----------:|:--------:|:-------:|:--------:|:--------------------:|
|      5      | 36.4553  | 0.95199 |  1.0573  |        0.18815       |
|      15     | 30.5073  | 1.01710 |  0.8825  |        0.18181       |
|      25     | 24.0297  | 1.54890 |  0.6915  |        0.13342       |
|      35     | 16.2091  | 2.08180 |  0.4647  |        0.04516       |

## Modelo de controle pelo SISOtool

A partir dos pontos de operação encontrados do aeropêndulo, utilizou-se o "SISO Design" do Matlab para encontrar a função de transferência do controlador que possui a resposta desejada em cada ponto de operação. Assim, a função de transferência do controlador é dada por:

$$  C(s) = \frac{as^2 + bs + c}{s(s+N)}  $$

Desse modo, encontrou-se o seguinte conjunto de variáveis para cada potência:

| Potência(%) |    $a$   |   $b$   |    $c$   |
|:-----------:|:--------:|:-------:|:--------:|
|      5      |  0.0077  | 0.0330  |  0.2600  |
|      15     |  0.0067  | 0.0243  |  0.1730  |
|      25     |  0.0105  | 0.0364  |  0.2140  |
|      35     |  0.0170  | 0.0513  |  0.2130  |

### Modelo PID utilizado

Para o controle do aeropêndulo, foi utilizado o bloco lógico no simulink denominado por "PID Controller". O modelo da função de transferência do bloco é dado por:

$$ C(s) = K_p + \frac{K_i}{s} + \frac{K_p N}{1+\frac{N}{s}}$$

Utilizou-se $$N = 10$$. Assim, comprando ao modelo de controle anterior, é possível encontrar os valores das constantes do controlador PID a partir da seguinte relação matricial:

$$  
\left[ \begin{array}{ccc}  
1 & 0 & N \\  
N & 1 & 0 \\  
0 & N & 0  
\end{array} \right]  
\left[ \begin{array}{c}  
K_p \\  
K_i \\  
K_d  
\end{array} \right] =  
\left[ \begin{array}{c}  
a \\  
b \\  
c  
\end{array} \right]  
$$

Assim, os valores $K_p$, $K_i$ e $K_d$ encontrados para cada ponto de operação do aeropêndulo é dado por:

| Potência(%) |   $K_p$   |   $K_i$  |   $K_d$   |
|:-----------:|:---------:|:--------:|:---------:|
|      5      |   0.0007  |  0.0260  |   0.0007  |
|      15     |   0.0007  |  0.0173  |   0.0006  |
|      25     |   0.0015  |  0.0214  |   0.0009  |
|      35     |   0.0030  |  0.0213  |   0.0014  |

## Implementação no Simulink

A implementação no Simulink utilizou o bloco de função "PID Controller" para o controlador PID a partir dos parâmetros $K_p$, $K_i$ e $K_d$ encontrados. A seguir se encontra o esquema produzido no simulink:

![Minha Imagem] (./Imagem/Controlador_PID.jpeg)

Já a placa de aquisição de dados foi configurada a partir do seginte diagrama:

![Minha Imagem] (./Imagem/Aquisicao_dados.jpeg)

## Resultados

Com os modelos gerados do controlador PID, os parâmetros encontrados e a implementação no Simulink, obteve-se a seguinte resposta no experimento em laboratório:

Adicionar os gráficos de resultados
