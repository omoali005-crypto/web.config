
import { useState, useEffect } from "react";
import "./App.css";

function App() {
  const [score, setScore] = useState(0);
  const [level, setLevel] = useState(1);
  const [time, setTime] = useState(30);
  const [position, setPosition] = useState({ x: 0, y: 0 });
  const [gameOver, setGameOver] = useState(false);
  const [highscore, setHighscore] = useState(0);

  const moveCoin = () => {
    const maxX = 350;
    const maxY = 350;

    const randomX = Math.floor(Math.random() * maxX);
    const randomY = Math.floor(Math.random() * maxY);

    setPosition({ x: randomX, y: randomY });
  };

  const handleClick = () => {
    if (gameOver) return;

    const newScore = score + 1;
    setScore(newScore);

    if (newScore > highscore) {
      setHighscore(newScore);
    }

    if ((newScore) % 5 === 0) 
  setLevel((prev) => prev + 1);

    moveCoin();
  };

  useEffect(() => {
    if (gameOver) return;

    if (time === 0) {
      setGameOver(true);
      return;
    }

    const timer = setInterval(() => {
      setTime((prev) => prev - 1);
    }, 1000);

    return () => clearInterval(timer);
  }, [time, gameOver]);

  useEffect(() => {
    moveCoin();
  }, []);

const resetLevel = () => {
  setLevel(1);
};

const restartGame = () => {
  setScore(0);
  setTime(30);
  setGameOver(false);
  moveCoin();
};

  return (
    <div>
      <h1>🪙 Coin Clicker</h1>
      <p>Poeng: {score}</p>
      <p>Level: {level}</p>
      <p>Highscore: {highscore}</p>
      <p>Tid igjen: {time} sek</p>
      <button onClick={resetLevel}>Reset Level</button>


      <div id="game-area">
        {!gameOver && (
          <div
            id="coin"
            onClick={handleClick}
            style={{
              left: position.x,
              top: position.y,
                width: 50 - level * 3,
                 height: 50 - level * 3,
            }}
          ></div>
        )}
      </div>

      {gameOver && (
        <div>
          <h2>Game Over!</h2>
          <button onClick={restartGame}>Spill igjen</button>
        </div>
      )}
    </div>
  );
}

export default App;


left: position.x + "px",
top: position.y + "px",
width: (50 - level * 3) + "px",
height: (50 - level * 3) + "px",



body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #1e1e2f;
    color: white;
}

#game-area {
    background-color: #2c2c44;
    margin: 20px auto;
    position: relative;
    border-radius: 10px;
}

#coin {
   
    background-color: gold;
    border-radius: 50%;
    position: absolute;
    cursor: pointer;
    transition: all 0.2s;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    margin-top: 10px;
    border: none;
    border-radius: 5px;
    background-color: gold;
    cursor: pointer;
}

width: `${Math.max(30, 50 - level * 3)}px`,
height: `${Math.max(30, 50 - level * 3)}px`,
