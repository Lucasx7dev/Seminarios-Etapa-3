# Seminarios-Etapa-3
Projeto: Sistema de Acessibilidade Auditiva com LEDs de Nível de Som

// Projeto: Sistema de Acessibilidade Auditiva com LEDS.
// Descrição: Converte som em sinais visuais coloridos e vibração

int pinoSom = A0;     // Sensor de som analógico 
int ledVerde = 9;     // Som leve
int ledAmarelo = 10;  // Som médio
int ledVermelho = 11; // Som forte
int motor = 6;        // Motor vibracall 

//  ajuste de intensidade sonora (0–1023)
int limiteBaixo = 200;   // Som leve
int limiteMedio = 400;   // Som médio
int limiteAlto  = 700;   // Som forte

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(motor, OUTPUT);

  Serial.begin(9600);
  Serial.println("Sistema de acessibilidade com LEDs iniciado.");
}

void loop() {
  int valorSom = analogRead(pinoSom); // Lê intensidade do som
  Serial.print("Som detectado: ");
  Serial.println(valorSom);

  // Desliga tudo antes de atualizar
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);
  digitalWrite(motor, LOW);

  if (valorSom > limiteAlto) {
    // Som forte (alarme, campainha)
    digitalWrite(ledVermelho, HIGH);
    digitalWrite(motor, HIGH);
    delay(1000);
  } 
  else if (valorSom > limiteMedio) {
    // Som médio (voz alta, aviso)
    digitalWrite(ledAmarelo, HIGH);
    delay(800);
  } 
  else if (valorSom > limiteBaixo) {
    // Som leve (voz próxima)
    digitalWrite(ledVerde, HIGH);
    delay(500);
  }

  delay(100);
}
