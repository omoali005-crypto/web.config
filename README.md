const resetLevel = () => {
  setLevel(1);
};

const restartGame = () => {
  setScore(0);
  setTime(30);
  setGameOver(false);
  moveCoin();
};

