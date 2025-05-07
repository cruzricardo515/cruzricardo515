const canvas = document.getElementById('dragonCanvas');
const ctx = canvas.getContext('2d');
const pixelSize = 10; // Ajuste conforme necessário para o tamanho dos pixels
const dragonImage = [
    // Defina aqui os dados da sua imagem do dragão como arrays de cores
    // Por exemplo: ['#000', '#000', '#0F0', ...],
    // Cada subarray representa uma linha de pixels.
    // Use '#000' ou outra cor transparente para pixels vazios.

    // Exemplo simplificado e incompleto (você precisará completar com os dados da sua imagem):
    ['#000', '#000', '#000', '#FF8C00', '#FFD700', '#FFFF00', '#008000', '#8FBC8F', '#000'],
    ['#000', '#000', '#FF8C00', '#008000', '#3CB371', '#ADFF2F', '#008000', '#000', '#000'],
    // ... continue definindo todas as linhas do seu dragão
];

const fireFrames = [
    // Defina aqui os frames da animação do fogo (diferentes formatos da chama)
    // Cada frame será um array de arrays de cores.
    [
        ['#000', '#000', '#FFA500', '#FF4500', '#000'],
        ['#000', '#FFA500', '#FF8C00', '#FFA500', '#000'],
        ['#FFA500', '#FF8C00', '#FF0000', '#FF8C00', '#FFA500']
    ],
    [
        ['#000', '#FFA500', '#FF4500', '#000', '#000'],
        ['#FFA500', '#FF8C00', '#FFA500', '#000', '#000'],
        ['#FF8C00', '#FF0000', '#FF8C00', '#FFA500', '#000']
    ],
    // ... adicione mais frames de fogo
];

let wingFlapFrame = 0;
let fireFrameIndex = 0;
let firePosition = { x: 0, y: 0 }; // Posição inicial do fogo

function drawFrame(frameData) {
    frameData.forEach((row, y) => {
        row.forEach((color, x) => {
            if (color !== '#000' && color !== 'transparent') {
                ctx.fillStyle = color;
                ctx.fillRect(x * pixelSize, y * pixelSize, pixelSize, pixelSize);
            }
        });
    });
}

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Desenhar o dragão com a animação das asas (você precisará criar diferentes frames do dragão com as asas em posições diferentes)
    // Aqui é um exemplo conceitual, você precisará implementar os frames reais.
    const wingFrames = [dragonImage, /* outro frame com asas diferentes */];
    drawFrame(wingFrames[wingFlapFrame % wingFrames.length]);
    wingFlapFrame++;

    // Desenhar o fogo
    if (fireFrames.length > 0) {
        const currentFireFrame = fireFrames[fireFrameIndex % fireFrames.length];
        currentFireFrame.forEach((row, y) => {
            row.forEach((color, x) => {
                if (color !== '#000' && color !== 'transparent') {
                    ctx.fillStyle = color;
                    ctx.fillRect((firePosition.x + x) * pixelSize, (firePosition.y + y) * pixelSize, pixelSize, pixelSize);
                }
            });
        });
        fireFrameIndex++;
        // Atualizar a posição do fogo para dar a impressão de que está saindo da boca do dragão
        firePosition.x = /* Posição X da boca do dragão */;
        firePosition.y = /* Posição Y da boca do dragão */;
    }

    requestAnimationFrame(animate);
}

// Inicializar o canvas com as dimensões corretas baseadas na imagem do dragão
canvas.width = dragonImage[0].length * pixelSize;
canvas.height = dragonImage.length * pixelSize;

// Definir a posição inicial do fogo (relativa ao dragão)
firePosition.x = /* Coordenada X da boca do dragão */;
firePosition.y = /* Coordenada Y da boca do dragão */;

animate();
