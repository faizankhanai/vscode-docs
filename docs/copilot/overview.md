n---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 04/03/2025
MetaDescription: Copilot is your AI pair programmer tool in Visual Studio Code. Get code suggestions as you type in the editor, or use natural language chat to ask about your code or start an editing session for implementing new feature and fixing bugs.
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot in VS Code

Copilot is your AI pair programmer tool in Visual Studio Code. Get code suggestions as you type in the editor, or use natural language chat to ask about your code or start an editing session for implementing new feature and fixing bugs.

VS Code integrates AI features seamlessly in your developer workflow. Choose the experience that is optimized for your specific scenario.

* **[AI Code completions](/docs/copilot/ai-powered-suggestions.md)**: start typing in the editor, and Copilot provides code suggestions based on your existing code that match your coding style.

* **[Natural language chat](/docs/copilot/chat/copilot-chat.md)**: use a conversational interface to ask about your codebase or make edits across your project. Switch between ask, edit, agent mode based on your needs.

* **[Smart actions](/docs/copilot/copilot-smart-actions.md)**: boost your developer productivity, from the terminal, source control operations, to debugging and testing code.

## Getting started

1. [Set up Copilot in VS Code](/docs/copilot/setup.md) and get started for free with a monthly limit of completions and chat interactions.

1. [Get started with the Copilot Quickstart](/docs/copilot/getting-started.md).

1. [Discover chat with the Chat Tutorial](/docs/copilot/chat/getting-started-chat.md).

## Make Copilot your own

Copilot adapts to your development workflow and can be customized to match your team's practices.

* **[Custom instructions](/docs/copilot/copilot-customization.md)**: describe your specific coding practices in Markdown and Copilot generates code that seamlessly matches your style.

* **[Language models](/docs/copilot/language-models.md)**: choose from several built-in fast-coding or reasoning models, or bring your own provider API key.

* **[Add tools](/docs/copilot/chat/chat-agent-mode.md#agent-mode-tools)**: extend your agentic coding session with tools from MCP servers or Marketplace extensions.

## Additional resources

You can read more about Copilot and how to use it in VS Code in the [GitHub Copilot documentation](https://docs.github.com/copilot/getting-started-with-github-copilot?tool=vscode).

Or check out the [VS Code Copilot Series](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt) on YouTube, where you can find more introductory content and programming-specific videos for using Copilot with [Python](https://www.youtube.com/watch?v=DSHfHT5qnGc), [C#](https://www.youtube.com/watch?v=VsUQlSyQn1E), [Java](https://www.youtube.com/watch?v=zhCB95cE0HY), [PowerShell](https://www.youtube.com/watch?v=EwtRzAFiXEM), [C++](https://www.youtube.com/watch?v=ZfT2CXY5-Dc), and more.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Action Dodge Game</title>
  <style>
    body { margin: 0; background: #111; overflow: hidden; }
    canvas { display: block; margin: auto; background: #222; }
  </style>
</head>
<body>
  <canvas id="gameCanvas" width="400" height="600"></canvas>
  <script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");

    const player = { x: 180, y: 550, width: 40, height: 40, color: "#0f0" };
    let obstacles = [];
    let gameOver = false;
    let speed = 2;
    let frameCount = 0;

    document.addEventListener("keydown", e => {
      if (e.key === "ArrowLeft" && player.x > 0) player.x -= 20;
      if (e.key === "ArrowRight" && player.x < canvas.width - player.width) player.x += 20;
    });

    function drawPlayer() {
      ctx.fillStyle = player.color;
      ctx.fillRect(player.x, player.y, player.width, player.height);
    }

    function drawObstacles() {
      ctx.fillStyle = "#f00";
      for (let obs of obstacles) {
        ctx.fillRect(obs.x, obs.y, obs.width, obs.height);
      }
    }

    function updateObstacles() {
      for (let obs of obstacles) {
        obs.y += speed;
      }
      obstacles = obstacles.filter(obs => obs.y < canvas.height);
    }

    function detectCollision() {
      for (let obs of obstacles) {
        if (
          player.x < obs.x + obs.width &&
          player.x + player.width > obs.x &&
          player.y < obs.y + obs.height &&
          player.y + player.height > obs.y
        ) {
          gameOver = true;
        }
      }
    }

    function spawnObstacle() {
      const x = Math.floor(Math.random() * (canvas.width - 40));
      obstacles.push({ x: x, y: 0, width: 40, height: 40 });
    }

    function gameLoop() {
      if (gameOver) {
        ctx.fillStyle = "#fff";
        ctx.font = "30px Arial";
        ctx.fillText("Game Over!", 120, 300);
        return;
      }

      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawPlayer();
      drawObstacles();
      updateObstacles();
      detectCollision();

      frameCount++;
      if (frameCount % 50 === 0) spawnObstacle();

      // 🎉 Interesting moment: Speed suddenly increases at 30 seconds
      if (frameCount === 900) {
        speed = 5;
        console.log("Speed Up!");
      }

      requestAnimationFrame(gameLoop);
    }

    gameLoop();
  </script>
</body>
</html>
