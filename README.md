# Seminarios-Etapa-4
Sistema de Acessibilidade Auditiva com LEDs e Display LCD

Um projeto desenvolvido para auxiliar pessoas com deficiência auditiva através da conversão de som em sinais visuais utilizando LEDs coloridos e um display LCD.

Contexto do Problema

Pessoas com perda auditiva têm grande dificuldade em perceber sons importantes do ambiente, como:

Chamadas de voz

Batidas na porta

Alarmes ou avisos sonoros

Isso pode afetar a segurança, a independência e a comunicação no dia a dia.

Pensando nisso, nossa equipe desenvolveu um sistema que identifica o nível de som e o converte em alertas visuais.

Objetivo do Projeto

Criar um dispositivo acessível que:

 Detecta o volume do som ambiente usando um sensor (simulado por potenciômetro no Tinkercad)
 Acende LEDs de diferentes cores conforme a intensidade do som
 Exibe o valor do som e alertas no display LCD
 Ajuda pessoas com deficiência auditiva a perceber sinais do ambiente

 Além de apenas mostrar o nível do som, agora o sistema interpreta o tipo de aviso, dependendo da intensidade captada:

Baixa: “Hora do Lanche”  Sinal suave     
Média: “Chamada”   Chamado para sala 
Alta:“Hora da Saída”  Sinal forte       
Muito Alta:“ALARME!” Emergência   

Objetivo

Oferecer apoio acessível a estudantes surdos ou com deficiência auditiva, permitindo que eles vejam na tela o significado do som que está acontecendo no ambiente.

Funcionamento

O sensor de som (simulado por potenciômetro no Tinkercad):

Capta o nível sonoro

O Arduino compara com limites pré-definidos

Acende o LED correspondente

Mostra na tela LCD 16x2 o tipo de aviso

Gera um alerta visual claro e imediato

Componentes

Arduino Uno

Potenciômetro (sensor de som simulado)

LCD 16x2 com I2C

3 LEDs (verde, amarelo, vermelho)

Resistores

Protoboard

Jumpers

Codico para o arduino:


#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

int pinoSom = A0; 
int ledVerde = 9;
int ledAmarelo = 10;
int ledVermelho = 11;

// Limites ajustáveis
int limiteLanche = 250;      // som leve
int limiteChamada = 450;     // som médio
int limiteSaida = 650;       // som alto
int limiteAlarme = 800;      // som muito alto

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);

  Serial.begin(9600);

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Sistema Sonoro");
  delay(1200);
}

void loop() {
  int som = analogRead(pinoSom);
  
  // Apaga LEDs
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Som: ");
  lcd.print(som);

  lcd.setCursor(0, 1);

  if (som > limiteAlarme) {
    digitalWrite(ledVermelho, HIGH);
    lcd.print("ALARME !!!");
  }
  else if (som > limiteSaida) {
    digitalWrite(ledVermelho, HIGH);
    lcd.print("Hora da SAIDA");
  }
  else if (som > limiteChamada) {
    digitalWrite(ledAmarelo, HIGH);
    lcd.print("CHAMADA");
  }
  else if (som > limiteLanche) {
    digitalWrite(ledVerde, HIGH);
    lcd.print("Hora do LANCHE");
  }
  else {
    lcd.print("Ambiente calmo");
  }

  delay(200);
}
imagem da simulação feita no Tinkercad:
<img width="1917" height="985" alt="image" src="https://github.com/user-attachments/assets/8aff0966-7e05-4f11-8c34-1a1ef905c9cc" />

prototipo base:

<img width="1536" height="1024" alt="prototipo_base" src="https://github.com/user-attachments/assets/90cb868b-e897-4ed2-b76c-23275fa33d23" />
prototipo inicial:
<img width="353" height="443" alt="prototipo inicial" src="https://github.com/user-attachments/assets/0478d86c-9389-48f6-92f6-5aed9a878a48" />



Equipe:

Lucas Manoel

Gabriel de Paula Lima

Pedro Tooda

Andre Luiz

Vitor Rezende




