# Jaice.com
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Anime Battle Arena</title>

<style>
* {
    box-sizing: border-box;
    user-select: none;
}

body {
    margin: 0;
    background: radial-gradient(circle, #24245c, #070713);
    color: white;
    font-family: Arial, sans-serif;
    overflow: hidden;
}

h1 {
    text-align: center;
    margin: 8px;
    color: #fff;
    text-shadow: 0 0 15px #8b5cff;
}

#game {
    position: relative;
    width: 95%;
    max-width: 1000px;
    height: 560px;
    margin: auto;
    overflow: hidden;

    background:
        radial-gradient(circle at 50% 20%, #493c9e 0%, transparent 35%),
        linear-gradient(#17172f, #080810);

    border: 3px solid #fff;
    box-shadow: 0 0 30px #744cff;
}

/* Moon */

#moon {
    position: absolute;
    width: 100px;
    height: 100px;
    background: #fff;
    border-radius: 50%;
    right: 80px;
    top: 50px;
    box-shadow: 0 0 50px white;
}

/* Ground */

#ground {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 90px;
    background: linear-gradient(#242438, #090910);
    border-top: 3px solid #555;
}

/* Characters */

.fighter {
    position: absolute;
    width: 65px;
    height: 110px;
    bottom: 90px;
    border-radius: 35px 35px 15px 15px;

    transition:
        transform .08s,
        left .08s,
        right .08s;

    z-index: 5;
}

/* Player */

#player {
    left: 120px;

    background:
        linear-gradient(
            90deg,
            #25cfff,
            #174bff,
            #6b00ff
        );

    box-shadow:
        0 0 15px #00d9ff,
        0 0 35px #633cff;
}

/* Enemy */

#enemy {
    right: 120px;

    background:
        linear-gradient(
            90deg,
            #ff3030,
            #8c0000,
            #ff6a00
        );

    box-shadow:
        0 0 15px #ff2b2b,
        0 0 35px #ff5a00;
}

/* Aura */

.aura {
    position: absolute;
    width: 100px;
    height: 130px;
    border-radius: 50%;
    left: -18px;
    top: -10px;

    animation: aura 0.4s infinite alternate;
    pointer-events: none;
}

#player .aura {
    box-shadow:
        0 0 20px #00eaff,
        0 0 50px #0066ff;
}

#enemy .aura {
    box-shadow:
        0 0 20px #ff0000,
        0 0 50px #ff5500;
}

@keyframes aura {
    from {
        transform: scale(.9);
        opacity: .5;
    }

    to {
        transform: scale(1.15);
        opacity: 1;
    }
}

/* Health */

.healthBox {
    position: absolute;
    top: 15px;
    width: 38%;
    height: 28px;
    background: #171717;
    border: 2px solid white;
    border-radius: 10px;
    overflow: hidden;
    z-index: 10;
}

#playerHealth {
    left: 20px;
}

#enemyHealth {
    right: 20px;
}

.healthBar {
    height: 100%;
    width: 100%;
    transition: width .25s;
}

#playerBar {
    background: linear-gradient(90deg,#00ffff,#176aff);
}

#enemyBar {
    background: linear-gradient(90deg,#ff0000,#ff7300);
}

/* Energy */

#energyBox {
    position: absolute;
    top: 50px;
    left: 20px;
    width: 38%;
    height: 12px;
    background: #111;
    border: 1px solid white;
}

#energyBar {
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg,#9b00ff,#00eaff);
}

/* Damage effects */

.hit {
    animation: hit .15s;
}

@keyframes hit {
    0% { transform: translateX(0); }
    25% { transform: translateX(-15px); }
    50% { transform: translateX(15px); }
    100% { transform: translateX(0); }
}

/* Power projectile */

.projectile {
    position: absolute;
    width: 35px;
    height: 35px;
    border-radius: 50%;

    background: radial-gradient(
        circle,
        white,
        #00eaff,
        #0066ff,
        transparent
    );

    box-shadow:
        0 0 15px #00eaff,
        0 0 40px #0066ff;

    z-index: 8;
}

/* Explosion */

.explosion {
    position: absolute;
    width: 100px;
    height: 100px;
    border-radius: 50%;

    background: radial-gradient(
        circle,
        white,
        yellow,
        orange,
        red,
        transparent
    );

    animation: explode .35s forwards;
    pointer-events: none;
}

@keyframes explode {
    from {
        transform: scale(.2);
        opacity: 1;
    }

    to {
        transform: scale(2);
        opacity: 0;
    }
}

/* Controls */

#controls {
    text-align: center;
    padding: 8px;
}

button {
    border: 2px solid white;
    border-radius: 10px;

    background: linear-gradient(
        135deg,
        #5020ff,
        #00aaff
    );

    color: white;
    font-weight: bold;

    padding: 12px 15px;
    margin: 3px;

    box-shadow: 0 0 12px #482cff;

    cursor: pointer;
}

button:active {
    transform: scale(.9);
}

#message {
    text-align: center;
    height: 28px;
    font-size: 20px;
    font-weight: bold;
    text-shadow: 0 0 10px white;
}
</style>
</head>

<body>

<h1>⚔️ ANIME BATTLE ARENA ⚔️</h1>

<div id="game">

    <div id="moon"></div>

    <div class="healthBox" id="playerHealth">
        <div class="healthBar" id="playerBar"></div>
    </div>

    <div class="healthBox" id="enemyHealth">
        <div class="healthBar" id="enemyBar"></div>
    </div>

    <div id="energyBox">
        <div id="energyBar"></div>
    </div>

    <div id="player" class="fighter">
        <div class="aura"></div>
    </div>

    <div id="enemy" class="fighter">
        <div class="aura"></div>
    </div>

    <div id="ground"></div>

</div>

<div id="message">
    🔥 FIGHT!
</div>

<div id="controls">

    <button onclick="attack()">
        👊 ATTACK
    </button>

    <button onclick="powerBlast()">
        🔵 ENERGY BLAST
    </button>

    <button onclick="dash()">
        💨 DASH
    </button>

    <button onclick="ultimate()">
        🌟 ULTIMATE
    </button>

    <button onclick="restart()">
        🔄 RESTART
    </button>

</div>

<script>

let playerHP = 100;
let enemyHP = 100;

let energy = 100;

let attacking = false;
let ultimateCooldown = false;

const player =
    document.getElementById("player");

const enemy =
    document.getElementById("enemy");

const playerBar =
    document.getElementById("playerBar");

const enemyBar =
    document.getElementById("enemyBar");

const energyBar =
    document.getElementById("energyBar");

const message =
    document.getElementById("message");


/* Update UI */

function update() {

    playerBar.style.width =
        playerHP + "%";

    enemyBar.style.width =
        enemyHP + "%";

    energyBar.style.width =
        energy + "%";
}


/* Basic attack */

function attack() {

    if (enemyHP <= 0) return;

    let damage =
        Math.floor(Math.random() * 8) + 8;

    enemyHP -= damage;

    enemy.classList.add("hit");

    setTimeout(() => {
        enemy.classList.remove("hit");
    }, 150);

    message.innerText =
        "👊 COMBO HIT! -" + damage;

    createExplosion(enemy);

    update();

    enemyCounter();

    checkWin();
}


/* Energy blast */

function powerBlast() {

    if (energy < 20 || enemyHP <= 0)
        return;

    energy -= 20;

    message.innerText =
        "🔵 ENERGY BLAST!";

    const blast =
        document.createElement("div");

    blast.className = "projectile";

    let x = player.offsetLeft + 50;

    blast.style.left = x + "px";
    blast.style.bottom = "130px";

    document.getElementById("game")
        .appendChild(blast);

    let move = setInterval(() => {

        x += 15;

        blast.style.left =
            x + "px";

        if (
            x >
            enemy.offsetLeft - 20
        ) {

            clearInterval(move);

            blast.remove();

            let damage =
                Math.floor(Math.random() * 15) + 15;

            enemyHP -= damage;

            createExplosion(enemy);

            message.innerText =
                "💥 BLAST HIT! -" + damage;

            update();

            enemyCounter();

            checkWin();
        }

    }, 20);

    update();
}


/* Dash */

function dash() {

    let current =
        player.offsetLeft;

    player.style.left =
        Math.min(current + 100, 700) + "px";

    message.innerText =
        "💨 DASH!";

    setTimeout(() => {

        player.style.left =
            current + "px";

    }, 300);
}


/* Ultimate */

function ultimate() {

    if (
        energy < 60 ||
        ultimateCooldown ||
        enemyHP <= 0
    ) return;

    energy -= 60;

    ultimateCooldown = true;

    message.innerText =
        "🌟 ULTIMATE ATTACK!!!";

    let damage = 40;

    enemyHP -= damage;

    createExplosion(enemy);

    enemy.style.transform =
        "scale(1.4) rotate(10deg)";

    setTimeout(() => {

        enemy.style.transform =
            "scale(1) rotate(0deg)";

    }, 400);

    update();

    checkWin();

    setTimeout(() => {

        ultimateCooldown = false;

    }, 5000);
}


/* Enemy attack */

function enemyCounter() {

    if (enemyHP <= 0) return;

    setTimeout(() => {

        let damage =
            Math.floor(Math.random() * 7) + 4;

        playerHP -= damage;

        player.classList.add("hit");

        setTimeout(() => {
            player.classList.remove("hit");
        }, 150);

        message.innerText =
            "🔥 ENEMY ATTACK! -" + damage;

        update();

        if (playerHP <= 0) {

            playerHP = 0;

            message.innerText =
                "💀 YOU LOST!";
        }

    }, 500);
}


/* Explosion effect */

function createExplosion(target) {

    const explosion =
        document.createElement("div");

    explosion.className =
        "explosion";

    explosion.style.left =
        (target.offsetLeft - 20) + "px";

    explosion.style.bottom =
        "100px";

    document.getElementById("game")
        .appendChild(explosion);

    setTimeout(() => {
        explosion.remove();
    }, 400);
}


/* Win */

function checkWin() {

    if (enemyHP <= 0) {

        enemyHP = 0;

        message.innerText =
            "🏆 VICTORY! ENEMY DEFEATED!";
    }

    if (playerHP <= 0) {

        playerHP = 0;

        message.innerText =
            "💀 DEFEAT!";
    }

    update();
}


/* Restart */

function restart() {

    playerHP = 100;
    enemyHP = 100;
    energy = 100;

    player.style.left =
        "120px";

    enemy.style.right =
        "120px";

    enemy.style.transform =
        "scale(1)";

    message.innerText =
        "🔥 FIGHT!";

    update();
}


/* Slowly regenerate energy */

setInterval(() => {

    if (energy < 100) {

        energy += 2;

        update();
    }

}, 500);

update();

</script>

</body>
</html>
