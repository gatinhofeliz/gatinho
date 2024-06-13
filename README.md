# gatinho
eu
let ballX, ballY; // Posições da bolinha
let ballVX, ballVY; // Velocidades da bolinha
let ballDiameter = 20; // Diâmetro da bolinha
let paddleX, paddleY; // Posições da raquete
let paddleWidth = 10, paddleHeight = 60; // Dimensões da raquete
let paddleSpeed = 5; // Velocidade da raquete

function setup() {
  createCanvas(400, 400); // Tamanho do canvas
  ballX = width / 2;
  ballY = height / 2;
  ballVX = 3;
  ballVY = 2;
  paddleX = width - 30;
  paddleY = height / 2 - paddleHeight / 2;
}

function draw() {
  background(0); // Fundo preto
  moveBall();
  displayBall();
  checkEdges();
  movePaddle();
  displayPaddle();
  checkPaddleCollision();
}

function moveBall() {
  ballX += ballVX;
  ballY += ballVY;
}

function displayBall() {
  fill(255); // Cor da bolinha branca
  ellipse(ballX, ballY, ballDiameter, ballDiameter);
}

function checkEdges() {
  if (ballX > width - ballDiameter / 2 || ballX < ballDiameter / 2) {
    ballVX *= -1;
  }
  if (ballY > height - ballDiameter / 2 || ballY < ballDiameter / 2) {
    ballVY *= -1;
  }
}

function movePaddle() {
  if (keyIsDown(UP_ARROW)) {
    paddleY -= paddleSpeed;
  }
  if (keyIsDown(DOWN_ARROW)) {
    paddleY += paddleSpeed;
  }
  // Impedir que a raquete saia da tela
  paddleY = constrain(paddleY, 0, height - paddleHeight);
}

function displayPaddle() {
  fill(255); // Cor da raquete branca
  rect(paddleX, paddleY, paddleWidth, paddleHeight);
}

function checkPaddleCollision() {
  if (ballX + ballDiameter / 2 > paddleX &&
      ballY > paddleY &&
      ballY < paddleY + paddleHeight) {
    ballVX *= -1;
  }
}
