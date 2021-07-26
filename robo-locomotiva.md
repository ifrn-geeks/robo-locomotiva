IFRN GEEKS
Manual do robô locomotiva


Itens necessários:
* 1x Arduino Uno;
* 1x Ponte H L298N;
* 1x Kit Chassi 2WD;
* 1x Bateria 9V;
* 1x Conector p/ bateria 9V – Arduino;
* 2x Sensores infravermelhos/ultrassônico;
* 4x Pilhas AA;
* Jumpers diversos;
* Ferro de solda;
* Chave Philips.
Modo de montagem:
Passo 01: 
Após abrir o kit, pegue a base e posicione as quatro rodas bobas em um retângulo, como na imagem abaixo:
  



Passo 02:
Com a chave Philips, parafuse-os na base, e em seguida, coloque a roda boba sobre eles.
  
 
Passo 03:
Pegue o ferro de solda e solde os fios nos motores.
  

Passo 04:
Posicione os suportes do motor e, com a chave Philips, parafuse-os.
  

Passo 05:
Vire a base e, em seguida, fixe o interruptor, assim como o suporte das pilhas, utilizando a chave Philips.
  



Passo 06:
Adicione o interruptor em série com as pilhas. Para esse intuito, basta cortar o fio positivo (na imagem é o vermelho) e soldá-lo no interruptor.
  





Passo 07:
Com o último passo, a parte física está montada, só faltando posicionar os componentes eletrônicos ao longo da base.
  



Código:
//Definição dos pinos de controle do motor
#define M1 9 // Pino_Velocidade 1º Motor ( 0 a 255)_ Porta ATV_A ponte H;
#define M2 11 //Pino_Velocidade 2º Motor ( 0 a 255) _ Porta ATV_B ponte H;
#define dir1 8 //Pino_Direção do 1º Motor: Para frente / Para trás (HIGH ou LOW)_ porta IN1 ponte H;
#define dir2 10 //Pino_Direção do 2º Motor: Para frente / Para trás (HIGH ou LOW)_ porta IN3 ponte H;
//Definição dos pinos dos sensores
#define pin_S1 7
#define pin_S2 6
bool Sensor1 = 0;
bool Sensor2 = 0;
//variável responsável por controlar a velocidade dos motores
int velocidade = 150;
void setup(){
//Setamos os pinos de controle dos motores como saída
pinMode(M1, OUTPUT);
pinMode(M2, OUTPUT);
pinMode(dir1, OUTPUT);
pinMode(dir2, OUTPUT);
//Setamos a direção inicial do motor como 0, isso fará com que ambos os motores girem para frente
digitalWrite(dir1, LOW);
digitalWrite(dir2, LOW);
//Setamos os pinos dos sensores como entrada
pinMode(pin_S1, INPUT);
pinMode(pin_S2, INPUT);
}
void loop(){
//Neste processo armazenamos o valor lido pelo sensor na variável que armazena tais dados.
Sensor1 = digitalRead(pin_S1);
Sensor2 = digitalRead(pin_S2);
//Aqui está toda a lógica de comportamento do robô: Para a cor branca atribuímos o valor 0 e, para a cor preta, o valor 1.
if((Sensor1 == 0) && (Sensor2 == 0)){ // Se detectar na extremidade das faixas duas cores brancas
analogWrite(M1, velocidade); // Ambos motores ligam na mesma velocidade
analogWrite(M2, velocidade);
}
if((Sensor1 == 1) && (Sensor2 == 0)){ // Se detectar um lado preto e o outro branco
analogWrite(M1, 0); // O motor 1 desliga
analogWrite(M2, velocidade); // O motor 2 fica ligado, fazendo assim o carrinho virar
}
if((Sensor1 == 0) && (Sensor2 == 1)){ // Se detectar um lado branco e o outro preto
analogWrite(M1, velocidade); //O motor 1 fica ligado
analogWrite(M2, 0); // O motor 2 desliga, fazendo assim o carrinho virar no outro sentido
}
}




Referências:
https://blog.eletrogate.com/robo-seguidor-de-linha-tutorial-completo/


https://www.filipeflop.com/blog/projeto-robo-seguidor-de-linha-arduino/